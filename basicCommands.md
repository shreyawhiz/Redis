We can use the command SET to store the value "fido" at key "server:name":

`SET server:name "fido"`

Redis will store our data permanently, so we can later ask "What is the value stored at key server:name?" and Redis will reply with "fido":

`GET server:name => "fido"`


Other common operations provided by key-value stores are 
`DEL` to delete a given key and associated value, 
`SET-if-not-exists` (called SETNX on Redis) that sets a key only if it does not already exist, and 
`INCR` to atomically increment a number stored at a given key:


    `SET connections 10
    INCR connections => 11
    INCR connections => 12
    DEL connections
    INCR connections => 1`
	
	

Redis can be told that a key should only exist for a certain length of time. 
This is accomplished with the `EXPIRE and TTL commands`.

    `SET resource:lock "Redis Demo"
    EXPIRE resource:lock 120`
	
This causes the key resource:lock to be deleted in 120 seconds. 
You can test how long a key will exist with the TTL command. It returns the number of seconds until it will be deleted.

    TTL resource:lock => 113
    // after 113s
    TTL resource:lock => -2
	
The `-2 for the TTL of the key means that the key does not exist (anymore)`. 
A `-1 for the TTL of the key means that it will never expire`. Note that if you SET a key, its TTL will be reset.


    SET resource:lock "Redis Demo 1"
    EXPIRE resource:lock 120
    TTL resource:lock => 119
    SET resource:lock "Redis Demo 2"
    TTL resource:lock => -1

