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

c_list = C.container(list)
c_list.append(C(1))
c_list.append(C(2))
with pytest.raises(TypeError):
    c_list.append(3)
assert c_list.sum() == 3
```

### compatibility

Tested on 2.7 and 3.4.

### installation

```
pip install containers
```
