<h1>Container Types</h1>

Various container types are supported to defined collections of objects.

## Lists

The `List` annotation can be used to define a homogeneous collection of any other type.

```python
from typing import List, Optional
```

| Type Annotation | Python Value | YAML Content |
| --- | --- | --- |
| `foobar: List[int]` | `foobar = []` | `foobar:`<br>&nbsp;&nbsp;&nbsp;&nbsp;`-` |
| `foobar: List[int]` | `foobar = [1.23]` | `foobar:`<br>&nbsp;&nbsp;&nbsp;&nbsp;`- 1` |
| `foobar: List[int]` | `foobar = None` | `foobar:`<br>&nbsp;&nbsp;&nbsp;&nbsp;`-` |
| `foobar: Optional[List[int]]` | `foobar = None` | `foobar: ` |

More examples can be found in this [Jupyter Notebook](https://github.com/jacebrowning/datafiles/blob/develop/notebooks/patched_containers.ipynb).

## Dictionaries

The `Dict` annotation can be used to define a loose mapping of multiple types.

```python
from typing import Dict, Optional
```

| Type Annotation | Python Value | YAML Content |
| --- | --- | --- |
| `foobar: Dict[str, int]` | `foobar = {}` | `foobar: {}` |
| `foobar: Dict[str, int]` | `foobar = {'a': 42}` | `foobar:`<br>&nbsp;&nbsp;&nbsp;&nbsp;`a: 42` |
| `foobar: Dict[str, int]` | `foobar = None` | `foobar: {}` |
| `foobar: Optional[Dict[str, int]]` | `foobar = None` | `foobar: ` |

_Schema enforcement is not available with the `Dict` annotation._

## Dataclasses

Other dataclasses can serve as the annotation for an attribute to create nested structure:

```
#!python hl_lines="14"
from dataclasses import dataclass

from datafiles import datafile


@dataclass
class Nested:
    qux: str


@datafile("sample.yml")
class Sample:
    foo: int
    bar: Nested
```

which can be constructed like so:

```python
sample = Sample(42, Nested("Hello, world!"))
```

to save this `sample.yml` file:

```yaml
foo: 42
bar:
  qux: Hello, world!
```

More examples can be found in this [Jupyter Notebook](https://github.com/jacebrowning/datafiles/blob/develop/notebooks/nested_dataclass.ipynb).
