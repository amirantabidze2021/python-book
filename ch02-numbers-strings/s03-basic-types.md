## Basic types

<span title="This is important" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">ℹ️</span>

| Type        | Short description                        | Mutable | Example            |
|-------------|------------------------------------------|---------|---------------------------
| `NoneType`  | "Empty" value                            |<span style="color:blue">No</span>|  `None`               |
| `bool`      | Boolean value  (`True` or `False`)       |<span style="color:blue">No</span>|  `True`               | 
| `int`       | Integer numbers                          |<span style="color:blue">No</span>|  `42`                 |
| `float`     | Floating point number                    |<span style="color:blue">No</span>|  `23.43`              |
| `str`       | Textual data - sequense of characters    |<span style="color:blue">No</span>|  `"Hello!"`           |
| `list`      | Mutable sequense of any kind of objects  |<span style="color:green">Yes</span>|  `[1, 2, 3]`          |
| `tuple`     | Immutable sequense of objects            |<span style="color:blue">No</span>|  `(1, 2, 3)`          |
| `set`       | Mutable collection of unique objects     |<span style="color:green">Yes</span>|  `{1, 2, 3}`          |
| `frozenset`| Immutable collection of unique objects    |<span style="color:blue">No</span>|  `frozenset({1, 2, 3})`
| `dict`      | The collection of key-value pairs        |<span style="color:green">Yes</span>|  `{"name": "Johnny", "second_name": "Walker" }`

Main categories:
* Mutable or Immutable
    * Is object allowing it's change after creation?
* Hashable
    * Can this object be used as the key for the dictionary (has defined `__hash__()` and `__eq__()` methods)?
* Container, sequence, iterable
    * Has this object contained elements like other objects (has methods like `__iter__` or `__getitem__()`)?
* Callable
    * Can be invoked/run like a function or class (has method `__call__()` defined)? 

Additional types:
* `function` 
* `code object`
* `module`
* `iterator`
* `generator`
* `slice object`

And much more (because everything in Python is a object and thus - everything is of some specific type).

### Sizes of the object of basic types:

<span title="Advanced topic" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">🔥</span>


```python
import sys, rich

table = rich.table.Table(rich.table.Column(header="Object", style="blue"), 
                         "Type", 
                         rich.table.Column(header="Size", style="cyan", justify="right"),
                         title="Basic types memory usage", show_lines=True)
objects = [ None, True, 42, 3.1415, "Hello", [1, 2, 3], ("a", "b", "c"),
            {1, 2, 3}, frozenset({1, 2, 3}), {"x": 1, "y": 2} ]

for obj in objects:
    table.add_row(*map(str, (obj, type(obj), sys.getsizeof(obj))))
rich.console.Console().print(table)
```


<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-style: italic">              Basic types memory usage               </span>
┏━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━┳━━━━━━┓
┃<span style="font-weight: bold"> Object               </span>┃<span style="font-weight: bold"> Type                </span>┃<span style="font-weight: bold"> Size </span>┃
┡━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━╇━━━━━━┩
│<span style="color: #000080; text-decoration-color: #000080"> None                 </span>│ &lt;class 'NoneType'&gt;  │<span style="color: #008080; text-decoration-color: #008080">   16 </span>│
├──────────────────────┼─────────────────────┼──────┤
│<span style="color: #000080; text-decoration-color: #000080"> True                 </span>│ &lt;class 'bool'&gt;      │<span style="color: #008080; text-decoration-color: #008080">   28 </span>│
├──────────────────────┼─────────────────────┼──────┤
│<span style="color: #000080; text-decoration-color: #000080"> 42                   </span>│ &lt;class 'int'&gt;       │<span style="color: #008080; text-decoration-color: #008080">   28 </span>│
├──────────────────────┼─────────────────────┼──────┤
│<span style="color: #000080; text-decoration-color: #000080"> 3.1415               </span>│ &lt;class 'float'&gt;     │<span style="color: #008080; text-decoration-color: #008080">   24 </span>│
├──────────────────────┼─────────────────────┼──────┤
│<span style="color: #000080; text-decoration-color: #000080"> Hello                </span>│ &lt;class 'str'&gt;       │<span style="color: #008080; text-decoration-color: #008080">   54 </span>│
├──────────────────────┼─────────────────────┼──────┤
│<span style="color: #000080; text-decoration-color: #000080"> [1, 2, 3]            </span>│ &lt;class 'list'&gt;      │<span style="color: #008080; text-decoration-color: #008080">   80 </span>│
├──────────────────────┼─────────────────────┼──────┤
│<span style="color: #000080; text-decoration-color: #000080"> ('a', 'b', 'c')      </span>│ &lt;class 'tuple'&gt;     │<span style="color: #008080; text-decoration-color: #008080">   64 </span>│
├──────────────────────┼─────────────────────┼──────┤
│<span style="color: #000080; text-decoration-color: #000080"> {1, 2, 3}            </span>│ &lt;class 'set'&gt;       │<span style="color: #008080; text-decoration-color: #008080">  216 </span>│
├──────────────────────┼─────────────────────┼──────┤
│<span style="color: #000080; text-decoration-color: #000080"> frozenset({1, 2, 3}) </span>│ &lt;class 'frozenset'&gt; │<span style="color: #008080; text-decoration-color: #008080">  216 </span>│
├──────────────────────┼─────────────────────┼──────┤
│<span style="color: #000080; text-decoration-color: #000080"> {'x': 1, 'y': 2}     </span>│ &lt;class 'dict'&gt;      │<span style="color: #008080; text-decoration-color: #008080">  232 </span>│
└──────────────────────┴─────────────────────┴──────┘
</pre>



<span title="Advanced topic" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">🔥</span>

Memory requirement to store elements of `int` type in a different collections.

For _1 million_ of elements:

| Type | Bytes per element |
|------|-----------
| Tuple |8
| List  |9
| Set   | 33
| Dictionary | 42

Memory size may not be the only criteria to select data type. Rather, time required to perform operation on data type can be critical criteria.


```python
import sys, rich
n = 1000000

tests = {
    "list": [*range(n)],
    "tuple": tuple(range(n)),
    "set": set(range(n)),
    "dict": dict.fromkeys(range(n))
}

table = rich.table.Table("Type", 
                         rich.table.Column(header="Total size", style="cyan", justify="right"), 
                         rich.table.Column(header="Size per element", style="red", justify="right"),
    title=f"Collections memory requirement ({n} elements)", show_lines=True
)
for type_, collection in tests.items():
#     print(f"Size of <{type_}> ({n} items): {sys.getsizeof(collection)}, {sys.getsizeof(collection) / n} per element")
    table.add_row(str(type_), str(sys.getsizeof(collection)), str(sys.getsizeof(collection) / n))
rich.console.Console().print(table)
```


<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="font-style: italic"> Collections memory requirement (1000000 </span>
<span style="font-style: italic">                elements)                </span>
┏━━━━━━━┳━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━┓
┃<span style="font-weight: bold"> Type  </span>┃<span style="font-weight: bold"> Total size </span>┃<span style="font-weight: bold"> Size per element </span>┃
┡━━━━━━━╇━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━┩
│ list  │<span style="color: #008080; text-decoration-color: #008080">    8000056 </span>│<span style="color: #800000; text-decoration-color: #800000">         8.000056 </span>│
├───────┼────────────┼──────────────────┤
│ tuple │<span style="color: #008080; text-decoration-color: #008080">    8000040 </span>│<span style="color: #800000; text-decoration-color: #800000">          8.00004 </span>│
├───────┼────────────┼──────────────────┤
│ set   │<span style="color: #008080; text-decoration-color: #008080">   33554648 </span>│<span style="color: #800000; text-decoration-color: #800000">        33.554648 </span>│
├───────┼────────────┼──────────────────┤
│ dict  │<span style="color: #008080; text-decoration-color: #008080">   41943136 </span>│<span style="color: #800000; text-decoration-color: #800000">        41.943136 </span>│
└───────┴────────────┴──────────────────┘
</pre>