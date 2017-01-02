Redis also supports several more complex data structures. 
`A list is a series of ordered values. `
Some of the important commands for interacting with lists are `RPUSH, LPUSH, LLEN, LRANGE, LPOP, and RPOP`. 
You can immediately begin working with a key as a list, as long as it doesn't already exist as a different type.

RPUSH puts the new value at the end of the list.

	RPUSH friends "Alice"
    RPUSH friends "Bob"
	
	
LPUSH puts the new value at the start of the list.

    LPUSH friends "Sam"


LRANGE gives a subset of the list. 

It takes the index of the first element you want to retrieve as its first parameter and the index of the last element you want to retrieve as its second parameter. 
A value of -1 for the second parameter means to retrieve elements until the end of the list.


    LRANGE friends 0 -1 => 1) "Sam", 2) "Alice", 3) "Bob"
    LRANGE friends 0 1 => 1) "Sam", 2) "Alice"
    LRANGE friends 1 2 => 1) "Alice", 2) "Bob"
	
	

LLEN returns the current length of the list.

    LLEN friends => 3

LPOP removes the first element from the list and returns it.

    LPOP friends => "Sam"

RPOP removes the last element from the list and returns it.

    RPOP friends => "Bob"

Note that the list now only has one element:

    LLEN friends => 1
    LRANGE friends 0 -1 => 1) "Alice"
