# Comprehensions

> Comprehensions are considered as most "Pythonic" way of constructing needed data on-the-fly.


* List comprehension
* Dictionary comprehension
* Set comprehensions
* Generator expression\*

## List comprehension

> Bread and butter of day-to-day Python programming


```python
[x for x in range(0, 10)]
```




<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]</code></pre>




```python
[x for x in range(0,10) if x%2 == 0]
```




<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>[0, 2, 4, 6, 8]</code></pre>




```python
[(x, y) for x in range(0,10) if x%2 == 0 for y in range(x) if y%2 != 0]
```




<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>[(2, 1),
     (4, 1),
     (4, 3),
     (6, 1),
     (6, 3),
     (6, 5),
     (8, 1),
     (8, 3),
     (8, 5),
     (8, 7)]</code></pre>



## Dictionary comprehension

> Useful to create a dictionary with the same (default) value or predefined by some logic


```python
{x: str(x) for x in range(5)}
```




<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>{0: '0', 1: '1', 2: '2', 3: '3', 4: '4'}</code></pre>




```python
{x: y for x in range(3) for y in range(3)}
```




<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>{0: 2, 1: 2, 2: 2}</code></pre>



## Set comprehension

> Not so widely used but still can be quite helpful. For example if you read lines from the file you can collect unqiue ones.


```python
list_with_duplicated = [1, 1, 2, 3, 2, 1, 4, 2]
print({x for x in list_with_duplicated})
print(set(list_with_duplicated)) # recommended way

print({x for x in list_with_duplicated if x % 2}) # more logical usage
```

<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code>{1, 2, 3, 4}
    {1, 2, 3, 4}
    {1, 3}</code></pre>


## Generator expression

> "Kind of" comprehension but instead of returning sequence as other do, generator expression returns generator object.


```python
(x * x for x in range(10))
```




<pre class="notranslate" style="display:block; white-space: pre-wrap; padding:16px; background-color: #000;color: #e2e2e2;font-family: Hack, Consolas, Menlo, Mono, monospace;border-left: .25em solid #bc0000;"><code><generator object <genexpr> at 0x0000023DF7253678></code></pre>




```python
for x in (x * x for x in range(10)):
    print(x, end=" ")
```

    0 1 4 9 16 25 36 49 64 81