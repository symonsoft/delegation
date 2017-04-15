# delegation v.1.0
Python delegate pattern library

## About
Simple implementation of the delegate pattern.

## Installation
```sh
$ pip install delegation
```

## Examples
Here's a basic example:
```python
from delegation import SingleDelegated, MultiDelegated


class A(object):
    def foo(self):
        return 'A.foo()', self.__class__.__name__

    def bar(self):
        return 'A.bar()', self.__class__.__name__

    def xyz(self):
        return 'A.xyz()', self.__class__.__name__


class B(SingleDelegated):
    def foo(self):
        return 'B.foo()', self.__class__.__name__


class C(MultiDelegated):
    def xyz(self):
        return 'C.xyz()', self.__class__.__name__

print B(A()).foo()
print B(A()).bar()
print B(A()).xyz()

print C(A(), B(A())).foo()
print C(A(), B(A())).bar()
print C(A(), B(A())).xyz()

```
Output:
```
('B.foo()', 'B')
('A.bar()', 'A')
('A.xyz()', 'A')
[('A.foo()', 'A'), ('B.foo()', 'B')]
[('A.bar()', 'A'), ('A.bar()', 'A')]
('C.xyz()', 'C')
```

## License
BSD
