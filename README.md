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