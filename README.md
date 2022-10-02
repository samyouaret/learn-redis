# learn-redis
Learning Redis

## Keys

Setting a key in redis is fairly simple

    SET key value [EX seconds]

To read the key

    GET key

to increment or decrement a key

    INCR age 10
    DECR age 10
    INCRBY age 5

Ro get TTL of a key use: 

    TTL key_name

## Exists, Not exists

We can use `XX`(exists) `NX`(not exist) when using `SET` command example

    SET name Samy NX

Or
    SETNX name Samy

This tells redis to set the name value to Samy only if the key `name` does not exist.

To check if key exists we use

    exists key

### Get multiple keys at once

    MGET key1 key2

### Scan and keys

There are two ways to get all keys

    KEYS

this will block, and gets all keys

    SCAN slot(offet) MATCH customer:1* [count batch_size]

    SCAN 0 MATCH customer:1* [count 100]

EACH time it return next offset, until no more keys it returns 0.

## Delete keys

there are two ways to delete keys in redis

    DEL key_name

    Unlink key_name

## Hash tables

A hash table is record contains key, value pairs, to set a hash table use command:

    HSET  user:123 username samyouaret email sam@mail.com id 1

Get field inside the record

    HGET  user:123 username

To get all key-value pairs

    HGETALL  user:123 username

To scan all key-value pairs

    HSCAN  user:123 0 username

To get all values

    HVALS  user:123 username

To get all keys

    HKEYS  user:123 username

To get list of keys

    HMGET  user:123 username email

To delete a field from hashlist

    HDEL user:123 username

## Lists

Redis stores lists as linked list, and track the head/tail of it. It cloud contains only string elements. we can push either on left or right, althout there is way to insert into a given index but its performance is O(n).

    RPUSH playlist 100

At the beginning

    LPUSH playlist 100

top `pop` an element use

    LPOP playlist
    
    RPOP playlist

to get a range:

    LRANGE playlist 0 3

to get the length of the list:

    LLEN playlist

To get an element by index

    LINDEX playlist 3

### Can we move a list to another?

the answer is yes, we can use the `MOVE` command to move a list **atomically** to another.

## Sets

SET is unordered collection

    SADD online-users 1002

To check an item if it is a memeber:

    SISMEMBER online-users 1001

To get all members(not in production)

    SMEMBERS online-users

To get length(cardinality) of a set:

    SCARD online-users

Use `SSCAN` to iteratively read members

     SSCAN online-users 0  match 100*

To remove an element from list.

     SREM online-users 1001

to pop randomly a subset of elements

     SPOP online-users 2

### Set intersction/diffrence

to get intersection/diff  between two sets. note that intersection return the items present in first set and not in other sets.

    SINTER odd prime

    SDIFF odd prime

