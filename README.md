# learn-redis
Learning Redis


## Keys

Setting a key in redis is fairly simple

    SET key value [TTL]

To read the key

    GET key

We can use `XX`(exists) `NX`(not exist) when using `SET` command example

    SET name Samy NX

This tells redis to set the name value to Samy only if the key `name` does not exist.

To check if key exists we  use

    exists key

There are two ways to get all keys

    keys

this will block, and gets all keys

    SCAN slot(offet) MATCH customer:1* [count batch_size]
    SCAN 0 MATCH customer:1* [count 100]

EACH time it return next offset, until no more keys it returns 0.
