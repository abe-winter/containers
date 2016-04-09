## containers

This is a python library for typed containers -- it makes it safer & easier to work with lists & dicts of items of the same type.

### example

```python
import containers

@containers.container_class
class C:
    def __init__(self, x):
        self.x = x
    
    @containers.container_method(list)
    def sum(container):
        return sum(item.x for item in container)

    @containers.container_key
    def key(self):
        return self.x

c_list = C.container(list)
c_list.append(C(1))
c_list.append(C(2))

# items of incompatible type are rejected
with pytest.raises(TypeError):
    c_list.append(3)

# container_method methods are available on the list
assert c_list.sum() == 3

# automatic dictionary keys
c_dict = C.container(dict)
c_dict.add_value(C('k'))
assert c_dict['k'].x == 'k'
assert C('k').key() == 'k'
```

### compatibility

Tested on 2.7 and 3.4.

### installation

```
pip install containers
```
