Scala Macros

A scala macro is a way to type check DSLs during compilation.

These DSLs might be written as a string for example.
Think of a prepared SQL statement, something like:

	"SELECT * FROM users;"

Normally compilation will succeed whether or not the string contains correct SQL.
An error would not occur until the program attempts to access the database at runtime.
Even then, until the string is used as a database query, no error will occur.
In a complicated runtime, catching and logging that error can be non-trivial.

By using a macro, the scala compiler invokes additional tools to check that the string is correct SQL.
Should you make a SQL syntax error, this will be discovered during compilation, with a link to the exact failed line.

A few more uses I can think of:
	
	* type checking JSON, XMl, HTML
	* spell check strings
	  (imagine compile time errors for misspelled words! haha)

