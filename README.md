# ring-buffer

A persistent collection with semantics roughly equivalent to a ring buffer: acts like a queue, but
has a predetermined maximum capacity; items added after that capacity is exceeded implicitly eject
items from the front of the queue to make room.

Implements all the relevant Clojure interfaces, but none of the java interop interfaces; pull
requests welcome.

Possible optimization: keep a reference to unused items until some new item overwrites it. This is
easier and faster, but if you have a queue with very large objects (or a very large, mostly-empty
queue), you may see memory leaks. The performance gain is probably not worth it, but I suppose
that's a tradeoff some may not be willing to make.

## Usage

```clojure
ring-buffer.core> (into (ring-buffer 3) '(a b))
(a b)
ring-buffer.core> (into (ring-buffer 3) '(a b c d e))
(c d e)
ring-buffer.core> (pop (into (ring-buffer 3) '(a b c d e)))
(d e)
ring-buffer.core> (peek (into (ring-buffer 3) '(a b c d e)))
c
```

## License

Copyright © 2012 Alan Malloy

Distributed under the Eclipse Public License, the same as Clojure.
