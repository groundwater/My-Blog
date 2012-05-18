Scala implicits are hotly debated. A lot of Scala guides suggest avoiding them altogether. Implicits are can easily be misused, but using them correctly actually makes for *better* design.

I started a small side project in Scala for HBase. This article is *not* about HBase, it is about using implicits, however a small amount of HBase back story will be necessary.

HBase is a data store modeled after Google's Big Table. HBase contains tables which key-value stores. Every key and every value must be converted to an array of bytes before storage.

Using the Java API directly is rather cumbersome, here is the Scala code to store a simple object.

    case class Person(fName: String, lName: String, uid: String)
    
    val person = Person("Bill","Fakerston","billfakerston")
    
    val table: HTableInterface = ...
    
    // the row key is the person's uid
    val put: Put = new Put(person.uid)
    
    // hbase rows are multi-dimentional, keys have a family, as well as a name
    put.addColumn(
      //|<--- family ---->|<---- column name --->|<----- value to store ---->|
        Bytes.toBytes("d"),Bytes.toBytes("fName"),Bytes.toBytes(person.fName))
    put.addColumn(
        Bytes.toBytes("d"),Bytes.toBytes("lName"),Bytes.toBytes(person.lName))
    
    table.put(put)
    

I have no doubt that a compitent programmer would abstract much of this away. That is exactly what I am doing, however I will utilize implicts to help.

## A Little Prep Work

I like decoupling everything. In Java this is a pain because it usually means 50 extra class files. In scala, it can be as few as one line per extra class.

I will use a `Data` trait as the interface between all data to be stored, and the byte stream required by HBase.

    trait Data {
        def bytes: Array[Byte]
    }
    

Now normally this means a whole damn lot of subclassing. We will seee shortly that Scala implicits let us side-step this subclassing nightmare entirely.

We need a bit more scaffolding before proceeding:

    case class Row( row: Data )
    case class Item( family: Data, column: Data, item: Data )
    case class Entry( row: Row, items: Iterable[Item] )
    
    trait Table {
        def commit( entry: Entry )
    }
    

The table implementation is not important for this article, just realize that enough information is contained in the mutate object to store it using the native Java interface.

## Implicits Beat Method Overloading

I know none of you are looking forward to subclassing `Data` for each object you wish to store. Just for kicks, let's try it once for a `String`:

    class StringData(string: String) extends Data {
        def bytes: Array[Byte] = Bytes.toBytes(string)
    }
    

Not so bad, storing a `User` under this interface is just:

    val table: Table = ...
    val user = User("Emily","Robertson","emrob")
    table.commit( Entry( Row( 
        StringData(user.uid), 
        List(
            Item(StringData("d"),StringData("fName"),user.fName),
            Item(StringData("d"),StringData("lName"),user.lName))
        )))
    

Most programmers would see this and create function to handle the conversion, ending up with something like:

    val table: Table = ...
    val user = User("Emily","Robertson","emrob")
    table.commit( UserToEntry(user) )
    

### Enter Implicits

Whenever there is a type mismatch, the compiler will search for an implicit conversion between the two types. The companion object is one of those places, let us define:

    object Data {
        implicit def fromString(string: String): Data = {
            new Data(){
                lazy val bytes = Bytes.toBytes(string)
            }
        }
    }
    

We can now write code such as the following:

    table.commit( 
        Entry(Row(user.uid), 
        List(
            Item("d","fName",user.fName),
            Item("d","lName",user.lName))))
    

Notice how neither `Item` nor `Row` needed to know how to handle a `String` argument. Let's define a few more implicits for `Data`:

        object Data {
            implicit def fromString ...
            implicit def fromInt(int: Int): Data = {
                new Data(){
                    lazy val bytes = Bytes.toBytes(int)
                }
            }
            implicit def fromProtocolBuffer( protobuf: Message ): data = {
                new Data(){
                    lazy val btyes = protobuf.toByteArray()
                }
            }
        }
    }
    

We can mix and match converted types in the same method call:

    val message: Message = // some protocol buffer
    Item( 12, "hello", message )
    

Here `Item` does not need an overloaded method for each possible combination of arguments.

Now let's make defining rows even easier:

    object Row {
        implicit def fromData[D <% Data](data: D): Row = {
            Row(data)
        }
    }
    

The generics syntax `[D <% Data]` means "anything that can be converted to Data". Thus we can now write:

    val Entry = Entry("rowkey", List( ... ))
    

With a little help from the `Entry` companion object we can make this even slicker:

    object Entry {
        def apply(row: Data, family: Data, column: Data, value: Data) = {
            Entry( Row(row), List(
                Item(family,column,value)
            ))
        }
    }
    

For single item updates, you can now write

    Entry( "emrob", "d", 123, protobuf )
    

We have not done any method overloading, but have provided an conveninece method.

## Overriding Defauls

Implicits are searched for starting in the local scope, proceeding out. Finally the companion objects of the concerned types is searched. Library authors should provide implicit conversions in the companion objects. A developer can easily place an implicit in a tighter scope, overriding the default behaviour.

For example, perhaps a clever developer has implemented a much faster protocol buffer serializer. To use it in place of the default serializer place an implicit conversion in local scope:

    implicit def convertProtobuf(message: Message): Data = {
        myAwesomeSerializer(message)
    }
    
    val item = Item("d","buffer",message)
    

## Discussion

Implicit conversions beat method overloading and complex class heirarchies. Don't be afraid of them, embrace them.
