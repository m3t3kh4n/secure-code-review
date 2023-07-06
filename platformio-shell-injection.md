

Process Method:

```python
def process(self, contents):
    out_file = re.sub(r"[\"\'\;]+", "", self._main_ino) + ".cpp"
    assert self._gcc_preprocess(contents, out_file)
    contents = self.read_safe_contents(out_file)
    contents = self._join_multiline_strings(contents)
    self.write_safe_contents(out_file, self.append_prototypes(contents))
    return out_file
```

```python
out_file = re.sub(r"[\"\'\;]+", "", self._main_ino) + ".cpp"
```

This is the recommended fix:

Old one:

```python
out_file = self._main_ino + ".cpp"
```
This line appends the extension ".cpp" to the original value stored in `self._main_ino` (`.ino` filename) .


New one:

```python
out_file = re.sub(r"[\"\'\;]+", "", self._main_ino, flags=re.I) + ".cpp"
```
The `re.sub()` function removes any matches of regular expression pattern `r"[\"\'\;]+"` (one or more occurrences of double quotes, single quotes, or semicolons) in the `self._main_ino` string. The resulting value, after removing the matched characters, is then concatenated with the string ".cpp" and assigned to the `out_file` variable.


