## Introspection

<span title="This is important" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">ℹ️</span>

* Checking id of object: `id()`
    * Check that objects have same id: `is`
* Checking the type of object/variable:
    * ```type()``` - returns a type of object
    * ```isinstance(x, typeA)``` - returns True/False depends if object ```x``` of type ```typeA```

* ```dir()``` - return a list of valid attributes for argument (or list of names in current local scope if no argument)
* `sys.getsizeof()` - get the size (in bytes) of the memory allocated byt the object
* module `inspect` - low-level API for contents of a class, source code of a method, argument list for a function, detailed traceback
* module `dis` - decompiling Python byte-code showing code execution trace
* 3rd-party module `rich` has handly `inspect` method for inspecting any kind of Python object

Example of introspection of int object:


```python
a = 42
print(dir(a))
```

<pre class="notranslate" style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>['__abs__', '__add__', '__and__', '__bool__', '__ceil__', '__class__', '__delattr__', '__dir__', '__divmod__', '__doc__', '__eq__', '__float__', '__floor__', '__floordiv__', '__format__', '__ge__', '__getattribute__', '__getnewargs__', '__gt__', '__hash__', '__index__', '__init__', '__init_subclass__', '__int__', '__invert__', '__le__', '__lshift__', '__lt__', '__mod__', '__mul__', '__ne__', '__neg__', '__new__', '__or__', '__pos__', '__pow__', '__radd__', '__rand__', '__rdivmod__', '__reduce__', '__reduce_ex__', '__repr__', '__rfloordiv__', '__rlshift__', '__rmod__', '__rmul__', '__ror__', '__round__', '__rpow__', '__rrshift__', '__rshift__', '__rsub__', '__rtruediv__', '__rxor__', '__setattr__', '__sizeof__', '__str__', '__sub__', '__subclasshook__', '__truediv__', '__trunc__', '__xor__', 'bit_length', 'conjugate', 'denominator', 'from_bytes', 'imag', 'numerator', 'real', 'to_bytes']</code></pre>


We see a lot of methods available in object which gives us a hint what is the kind of object it is and what we can do with it.

Introspection of an instance of some class:


```python
class A(object):      # Creating simple class
    attr1 = 5         # with one attribute: "attr1"
some_obj = A()
print(some_obj.attr1) # Checking the value of custom attribute
print(dir(some_obj))  # This will show all inherited methods and attribute we created: "attr1"
```

<pre class="notranslate" style="background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>5
    ['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'attr1']</code></pre>


In this case we can see many inherited methods (from parent class called "object") and also attributes and methods defined by us (in this example it is just one attribute "attr1")

## Getting the size of an object

> `sys.getsizeof()` - get the size (in bytes) of the memory allocated byt the object.


```python
import sys

sys.getsizeof(100500)
```


<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">28</span>
</pre>



## Introspection with `rich`

<span title="Advanced topic" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">🔥</span>

There is a nice library `rich` used for displaying various content to terminal. It is can be used as additional inspection tool in Python (or `ipython`/`Jupyter` also):



```python
from rich import inspect

i = 100500

inspect(i)
```


<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080">╭────── </span><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">&lt;</span><span style="color: #ff00ff; text-decoration-color: #ff00ff; font-weight: bold">class</span><span style="color: #000000; text-decoration-color: #000000"> </span><span style="color: #008000; text-decoration-color: #008000">'int'</span><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">&gt;</span><span style="color: #000080; text-decoration-color: #000080"> ───────╮</span>
<span style="color: #000080; text-decoration-color: #000080">│</span> <span style="color: #800080; text-decoration-color: #800080; font-weight: bold">int</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">([</span><span style="color: #008080; text-decoration-color: #008080">x</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">])</span><span style="color: #008080; text-decoration-color: #008080"> -&gt; integer</span>        <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span> <span style="color: #800080; text-decoration-color: #800080; font-weight: bold">int</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080">x, </span><span style="color: #808000; text-decoration-color: #808000">base</span><span style="color: #008080; text-decoration-color: #008080">=</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">10</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">)</span><span style="color: #008080; text-decoration-color: #008080"> -&gt; integer</span> <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                            <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span> <span style="color: #008000; text-decoration-color: #008000">╭────────────────────────╮</span> <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span> <span style="color: #008000; text-decoration-color: #008000">│</span> <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">100500</span>                 <span style="color: #008000; text-decoration-color: #008000">│</span> <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span> <span style="color: #008000; text-decoration-color: #008000">╰────────────────────────╯</span> <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                            <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span> <span style="color: #808000; text-decoration-color: #808000; font-style: italic">denominator</span> = <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">1</span>            <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>        <span style="color: #808000; text-decoration-color: #808000; font-style: italic">imag</span> = <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">0</span>            <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>   <span style="color: #808000; text-decoration-color: #808000; font-style: italic">numerator</span> = <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">100500</span>       <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>        <span style="color: #808000; text-decoration-color: #808000; font-style: italic">real</span> = <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">100500</span>       <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">╰────────────────────────────╯</span>
</pre>



<span title="Advanced topic" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">🔥</span>

And with methods overview:


```python
inspect(i, methods=True)
```


<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080">╭────────────────────────────────────── </span><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">&lt;</span><span style="color: #ff00ff; text-decoration-color: #ff00ff; font-weight: bold">class</span><span style="color: #000000; text-decoration-color: #000000"> </span><span style="color: #008000; text-decoration-color: #008000">'int'</span><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">&gt;</span><span style="color: #000080; text-decoration-color: #000080"> ──────────────────────────────────────╮</span>
<span style="color: #000080; text-decoration-color: #000080">│</span> <span style="color: #800080; text-decoration-color: #800080; font-weight: bold">int</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">([</span><span style="color: #008080; text-decoration-color: #008080">x</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">])</span><span style="color: #008080; text-decoration-color: #008080"> -&gt; integer</span>                                                                       <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span> <span style="color: #800080; text-decoration-color: #800080; font-weight: bold">int</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">(</span><span style="color: #008080; text-decoration-color: #008080">x, </span><span style="color: #808000; text-decoration-color: #808000">base</span><span style="color: #008080; text-decoration-color: #008080">=</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">10</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">)</span><span style="color: #008080; text-decoration-color: #008080"> -&gt; integer</span>                                                                <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                                                                                           <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span> <span style="color: #008000; text-decoration-color: #008000">╭───────────────────────────────────────────────────────────────────────────────────────╮</span> <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span> <span style="color: #008000; text-decoration-color: #008000">│</span> <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">100500</span>                                                                                <span style="color: #008000; text-decoration-color: #008000">│</span> <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span> <span style="color: #008000; text-decoration-color: #008000">╰───────────────────────────────────────────────────────────────────────────────────────╯</span> <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                                                                                           <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>      <span style="color: #808000; text-decoration-color: #808000; font-style: italic">denominator</span> = <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">1</span>                                                                      <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>             <span style="color: #808000; text-decoration-color: #808000; font-style: italic">imag</span> = <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">0</span>                                                                      <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>        <span style="color: #808000; text-decoration-color: #808000; font-style: italic">numerator</span> = <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">100500</span>                                                                 <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>             <span style="color: #808000; text-decoration-color: #808000; font-style: italic">real</span> = <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">100500</span>                                                                 <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span> <span style="color: #808000; text-decoration-color: #808000; font-style: italic">as_integer_ratio</span> = <span style="color: #00ffff; text-decoration-color: #00ffff; font-style: italic">def </span><span style="color: #800000; text-decoration-color: #800000; font-weight: bold">as_integer_ratio</span><span style="font-weight: bold">()</span>: <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">Return integer ratio.</span>                          <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>       <span style="color: #808000; text-decoration-color: #808000; font-style: italic">bit_length</span> = <span style="color: #00ffff; text-decoration-color: #00ffff; font-style: italic">def </span><span style="color: #800000; text-decoration-color: #800000; font-weight: bold">bit_length</span><span style="font-weight: bold">()</span>: <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">Number of bits necessary to represent self in </span>       <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                    <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">binary.</span>                                                                <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>        <span style="color: #808000; text-decoration-color: #808000; font-style: italic">conjugate</span> = <span style="color: #00ffff; text-decoration-color: #00ffff; font-style: italic">def </span><span style="color: #800000; text-decoration-color: #800000; font-weight: bold">conjugate</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">...</span><span style="font-weight: bold">)</span> <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">Returns self, the complex conjugate of any int.</span>     <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>       <span style="color: #808000; text-decoration-color: #808000; font-style: italic">from_bytes</span> = <span style="color: #00ffff; text-decoration-color: #00ffff; font-style: italic">def </span><span style="color: #800000; text-decoration-color: #800000; font-weight: bold">from_bytes</span><span style="font-weight: bold">(</span>bytes, byteorder, *, <span style="color: #808000; text-decoration-color: #808000">signed</span>=<span style="color: #ff0000; text-decoration-color: #ff0000; font-style: italic">False</span><span style="font-weight: bold">)</span>: <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">Return the integer </span> <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                    <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">represented by the given array of bytes.</span>                               <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>         <span style="color: #808000; text-decoration-color: #808000; font-style: italic">to_bytes</span> = <span style="color: #00ffff; text-decoration-color: #00ffff; font-style: italic">def </span><span style="color: #800000; text-decoration-color: #800000; font-weight: bold">to_bytes</span><span style="font-weight: bold">(</span>length, byteorder, *, <span style="color: #808000; text-decoration-color: #808000">signed</span>=<span style="color: #ff0000; text-decoration-color: #ff0000; font-style: italic">False</span><span style="font-weight: bold">)</span>: <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">Return an array of </span>  <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                    <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">bytes representing an integer.</span>                                         <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">╰───────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>



<span title="Advanced topic" style="position: absolute; top: 25px; right: 30px; font-size: 250%; color:red">🔥</span>

An example of `list` inspection:


```python
inspect([1, 2, 3], methods=True)
```


<pre style="white-space:pre;overflow-x:auto;line-height:normal;font-family:Menlo,'DejaVu Sans Mono',consolas,'Courier New',monospace"><span style="color: #000080; text-decoration-color: #000080">╭───────────────────────────────────── </span><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">&lt;</span><span style="color: #ff00ff; text-decoration-color: #ff00ff; font-weight: bold">class</span><span style="color: #000000; text-decoration-color: #000000"> </span><span style="color: #008000; text-decoration-color: #008000">'list'</span><span style="color: #000080; text-decoration-color: #000080; font-weight: bold">&gt;</span><span style="color: #000080; text-decoration-color: #000080"> ──────────────────────────────────────╮</span>
<span style="color: #000080; text-decoration-color: #000080">│</span> <span style="color: #008080; text-decoration-color: #008080">Built-in mutable sequence.</span>                                                                <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                                                                                           <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span> <span style="color: #008000; text-decoration-color: #008000">╭───────────────────────────────────────────────────────────────────────────────────────╮</span> <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span> <span style="color: #008000; text-decoration-color: #008000">│</span> <span style="font-weight: bold">[</span><span style="color: #008080; text-decoration-color: #008080; font-weight: bold">1</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">2</span>, <span style="color: #008080; text-decoration-color: #008080; font-weight: bold">3</span><span style="font-weight: bold">]</span>                                                                             <span style="color: #008000; text-decoration-color: #008000">│</span> <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span> <span style="color: #008000; text-decoration-color: #008000">╰───────────────────────────────────────────────────────────────────────────────────────╯</span> <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>                                                                                           <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>  <span style="color: #808000; text-decoration-color: #808000; font-style: italic">append</span> = <span style="color: #00ffff; text-decoration-color: #00ffff; font-style: italic">def </span><span style="color: #800000; text-decoration-color: #800000; font-weight: bold">append</span><span style="font-weight: bold">(</span>object, <span style="color: #800080; text-decoration-color: #800080">/</span><span style="font-weight: bold">)</span>: <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">Append object to the end of the list.</span>                    <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>   <span style="color: #808000; text-decoration-color: #808000; font-style: italic">clear</span> = <span style="color: #00ffff; text-decoration-color: #00ffff; font-style: italic">def </span><span style="color: #800000; text-decoration-color: #800000; font-weight: bold">clear</span><span style="font-weight: bold">()</span>: <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">Remove all items from list.</span>                                        <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>    <span style="color: #808000; text-decoration-color: #808000; font-style: italic">copy</span> = <span style="color: #00ffff; text-decoration-color: #00ffff; font-style: italic">def </span><span style="color: #800000; text-decoration-color: #800000; font-weight: bold">copy</span><span style="font-weight: bold">()</span>: <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">Return a shallow copy of the list.</span>                                  <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>   <span style="color: #808000; text-decoration-color: #808000; font-style: italic">count</span> = <span style="color: #00ffff; text-decoration-color: #00ffff; font-style: italic">def </span><span style="color: #800000; text-decoration-color: #800000; font-weight: bold">count</span><span style="font-weight: bold">(</span>value, <span style="color: #800080; text-decoration-color: #800080">/</span><span style="font-weight: bold">)</span>: <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">Return number of occurrences of value.</span>                     <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>  <span style="color: #808000; text-decoration-color: #808000; font-style: italic">extend</span> = <span style="color: #00ffff; text-decoration-color: #00ffff; font-style: italic">def </span><span style="color: #800000; text-decoration-color: #800000; font-weight: bold">extend</span><span style="font-weight: bold">(</span>iterable, <span style="color: #800080; text-decoration-color: #800080">/</span><span style="font-weight: bold">)</span>: <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">Extend list by appending elements from the iterable.</span>   <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>   <span style="color: #808000; text-decoration-color: #808000; font-style: italic">index</span> = <span style="color: #00ffff; text-decoration-color: #00ffff; font-style: italic">def </span><span style="color: #800000; text-decoration-color: #800000; font-weight: bold">index</span><span style="font-weight: bold">(</span>value, <span style="color: #808000; text-decoration-color: #808000">start</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">0</span>, <span style="color: #808000; text-decoration-color: #808000">stop</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">9223372036854775807</span>, <span style="color: #800080; text-decoration-color: #800080">/</span><span style="font-weight: bold">)</span>: <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">Return first index of </span>  <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>           <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">value.</span>                                                                          <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>  <span style="color: #808000; text-decoration-color: #808000; font-style: italic">insert</span> = <span style="color: #00ffff; text-decoration-color: #00ffff; font-style: italic">def </span><span style="color: #800000; text-decoration-color: #800000; font-weight: bold">insert</span><span style="font-weight: bold">(</span>index, object, <span style="color: #800080; text-decoration-color: #800080">/</span><span style="font-weight: bold">)</span>: <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">Insert object before index.</span>                       <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>     <span style="color: #808000; text-decoration-color: #808000; font-style: italic">pop</span> = <span style="color: #00ffff; text-decoration-color: #00ffff; font-style: italic">def </span><span style="color: #800000; text-decoration-color: #800000; font-weight: bold">pop</span><span style="font-weight: bold">(</span><span style="color: #808000; text-decoration-color: #808000">index</span>=<span style="color: #008080; text-decoration-color: #008080; font-weight: bold">-1</span>, <span style="color: #800080; text-decoration-color: #800080">/</span><span style="font-weight: bold">)</span>: <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">Remove and return item at index </span><span style="color: #7f7f7f; text-decoration-color: #7f7f7f; font-weight: bold">(</span><span style="color: #7f7f7f; text-decoration-color: #7f7f7f">default last</span><span style="color: #7f7f7f; text-decoration-color: #7f7f7f; font-weight: bold">)</span><span style="color: #7f7f7f; text-decoration-color: #7f7f7f">.</span>           <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>  <span style="color: #808000; text-decoration-color: #808000; font-style: italic">remove</span> = <span style="color: #00ffff; text-decoration-color: #00ffff; font-style: italic">def </span><span style="color: #800000; text-decoration-color: #800000; font-weight: bold">remove</span><span style="font-weight: bold">(</span>value, <span style="color: #800080; text-decoration-color: #800080">/</span><span style="font-weight: bold">)</span>: <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">Remove first occurrence of value.</span>                         <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span> <span style="color: #808000; text-decoration-color: #808000; font-style: italic">reverse</span> = <span style="color: #00ffff; text-decoration-color: #00ffff; font-style: italic">def </span><span style="color: #800000; text-decoration-color: #800000; font-weight: bold">reverse</span><span style="font-weight: bold">()</span>: <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">Reverse *IN PLACE*.</span>                                              <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>    <span style="color: #808000; text-decoration-color: #808000; font-style: italic">sort</span> = <span style="color: #00ffff; text-decoration-color: #00ffff; font-style: italic">def </span><span style="color: #800000; text-decoration-color: #800000; font-weight: bold">sort</span><span style="font-weight: bold">(</span>*, <span style="color: #808000; text-decoration-color: #808000">key</span>=<span style="color: #800080; text-decoration-color: #800080; font-style: italic">None</span>, <span style="color: #808000; text-decoration-color: #808000">reverse</span>=<span style="color: #ff0000; text-decoration-color: #ff0000; font-style: italic">False</span><span style="font-weight: bold">)</span>: <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">Sort the list in ascending order and </span>     <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">│</span>           <span style="color: #7f7f7f; text-decoration-color: #7f7f7f">return </span><span style="color: #bf7fbf; text-decoration-color: #bf7fbf; font-style: italic">None</span><span style="color: #7f7f7f; text-decoration-color: #7f7f7f">.</span>                                                                    <span style="color: #000080; text-decoration-color: #000080">│</span>
<span style="color: #000080; text-decoration-color: #000080">╰───────────────────────────────────────────────────────────────────────────────────────────╯</span>
</pre>