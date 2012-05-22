# Iteratees #

Whenever data is processed, there is a producer i.e. the code reading the file, and the consumer i.e. the code parsing the incoming text.

An iteratee is a functional way of reading a file where both the consumer and producer can indicate they are done. Given

	trait ProducerState
	trait ConsumerState

let's make a bunch of possible states (or signals)

	class EndOfFile extends ProducerState
	class More 	    extends ProducerState

	class Done extends ConsumerState
	class More extends ConsumerState

The iteratee is a function that reads the producer state, and if there is More data will read the data. The iteratee function is created by the consumer.

	f: ProducerState => ConsumerState

The producer must create a method that _accepts_ an iteratee. The producer decides how to proceed based on the ConsumerState returned at each step.

## Missing Pieces ##

ProducerState and ConsumerState actually need to contain fields to make all this useful. If the ProducerState is More, it should contain a field with the next chunk of data (Let's assume all data types are String)

	class More(val data: String) extends ProducerState

Thus, the function can decide how to proceed based on the input like this:
	
	def f(p: ProducerState) : ConsumerState = {
		case EndOfFile => Done
		case m: More => // do something with m.data
					    // return Done or More
	}

The ConsumerState also provides a field. Instead of calling the same f each time, the More ConsumerState provides _the next_ f to be called. 
	
	class More(next: ProducerState => ConsumerState) extends ConsumerState

The iteratee provided by the consumer has a chance to swap out or modify the next iteratee called by the producer. When the iteratee is full, it simply returns Done and the producer code will know to stop.


