# One Interface per Class

Java programmers in particular complain that mocks force them to write one interface per class. No, but I understand why they feel that way.

Overview:

* interfaces and mocks go together, because we didn't always have cglib
* don't mock everything: values, entities, services and "When it's safe to introduce test doubles"
* so what's the problem? Why does an interface have to have multiple implementers?
* fine: the mocks *are* the other implementers. Even if you don't want take advantage of the flexibility in your production code, you need it to check your code carefully and thoroughly.

So just do it already and relax.

