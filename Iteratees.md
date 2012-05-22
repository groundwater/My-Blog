# Iteratees #

Whenever data is processed, there is a producer and comsumer.
For example, a program that reads and parses a JSON file contains code that reads the file (i.e. the producer)
and code that parses the data stream (i.e. the consumer)

An iteratee is a functional way of exchanging data where both the consumer and producer can indicate they are done. 
Functional programming is beneficial because 
there are no concurrency issues or race conditions when scaling across multiple threads.

Let's get started with an example, abstractly any exchange of data will require a producer and consumer object.
Now the crux of an iteratee is that while it is a functional approach to data exchange, 
both parties are capable of signaling the other during the transaction.
Signals are sent as objects that satisfy a generic `State` or `Signal` trait,
but it is advisable to use different signal types for the consumer and producer.

	trait ConsumerState
	trait ProducerState

These signals can be anything, but for our example the two signals are `Done` and `More`.

	class Done extends ProducerState
	class More extends ProducerState

	class Done extends ConsumerState
	class More extends ConsumerState

The iteratee binds the consumer and producer together, using states to coordinate the data exchange.

The iteratee is a function created by the consumer satisfying the following signature:

	f: ProducerState => ConsumerState

The consumer controls the function logic, 
the consumer must write a function to properly respond to the possible states returned by the producer.
When the iteratee is called with a `Done` argument type, the consumer knows the producer is out of data 
and should end the exchange.

The producer, on the other hand, must create a method that _accepts_ an iteratee. 
Throughout the data exchange, the iteratee is called many times by the producer.
When the iteratee returns a `Done`, the consumer no longer wishes to receive any more data.
The producer must honour this request, and should end the exchange.

## Missing Pieces ##

ProducerState and ConsumerState actually need to contain fields to make all this useful. 
If the ProducerState is More, 
it should contain a field with the next chunk of data (Let's assume all data types are String)

	class More(val data: String) extends ProducerState

Thus, the function can decide how to proceed based on the input like this:
	
	def f(p: ProducerState) : ConsumerState = {
		case EndOfFile => Done
		case m: More => // do something with m.data
					    // return Done or More
	}

The ConsumerState also provides a field. Instead of calling the same f each time, 
the More ConsumerState provides _the next_ f to be called. 
	
	class More(next: ProducerState => ConsumerState) extends ConsumerState

The iteratee provided by the consumer has a chance to swap out or modify the next iteratee called by the producer.
When the iteratee is full, it simply returns Done and the producer code will know to stop.


