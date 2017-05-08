# delegation v.1.1
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

print(B(A()).foo())  # ('B.foo()', 'B')
print(B(A()).bar())  # ('A.bar()', 'A')
print(B(A()).xyz())  # ('A.xyz()', 'A')

print(C(A(), B(A())).foo())  # [('A.foo()', 'A'), ('B.foo()', 'B')]
print(C(A(), B(A())).bar())  # [('A.bar()', 'A'), ('A.bar()', 'A')]
print(C(A(), B(A())).xyz())  # ('C.xyz()', 'C')
```


## License
BSD
