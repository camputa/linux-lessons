# In-Depth `sed` Command

The `sed` command is a stream editor that performs basic text transformations on an input stream (a file or input from a pipeline). With `sed`, you can edit text files, search and replace patterns, and perform complex text manipulations efficiently. It reads input line by line and applies specified operations to each line.

## Basic Usage

At its simplest, `sed` is used to perform basic text replacements. The basic syntax of `sed` looks like this:

```bash
sed 's/pattern/replacement/' filename
```

This command searches for `pattern` and replaces it with `replacement` in `filename`.

## Common Options and Configurations

### Substitute Command (`s`)

The most common `sed` command is the substitute command `s`, which is used for search and replace operations. For example, to replace all occurrences of "old" with "new":

```bash
sed 's/old/new/' filename
```

To replace all occurrences globally on each line, add the `g` flag:

```bash
sed 's/old/new/g' filename
```

### In-place Editing (`-i`)

To edit files in place, use the `-i` option. This option modifies the original file directly:

```bash
sed -i 's/old/new/g' filename
```

### Regular Expressions

`sed` supports regular expressions for advanced pattern matching. For example, to replace any digit with a hash symbol:

```bash
sed 's/[0-9]/#/g' filename
```

### Addressing

You can specify line addresses to limit the scope of operations. For instance, to replace only on the second line:

```bash
sed '2s/old/new/' filename
```

To replace from the second to the fourth line:

```bash
sed '2,4s/old/new/' filename
```

### Multiple Commands

You can apply multiple commands in a single `sed` invocation using the `-e` option or by separating commands with semicolons:

```bash
sed -e 's/old/new/' -e 's/foo/bar/' filename
```

or

```bash
sed 's/old/new/; s/foo/bar/' filename
```

### Deleting Lines

To delete specific lines, use the `d` command. For example, to delete the third line:

```bash
sed '3d' filename
```

To delete lines matching a pattern:

```bash
sed '/pattern/d' filename
```

### Inserting and Appending Text

To insert text before a line, use the `i` command:

```bash
sed '3i\Inserted text' filename
```

To append text after a line, use the `a` command:

```bash
sed '3a\Appended text' filename
```

### Changing Lines

To replace the entire line, use the `c` command:

```bash
sed '3c\New text' filename
```

### Printing Lines

To print specific lines, use the `p` command with the `-n` option to suppress automatic printing:

```bash
sed -n '3p' filename
```

To print lines matching a pattern:

```bash
sed -n '/pattern/p' filename
```

### Saving to a New File

You can redirect the output of `sed` to a new file:

```bash
sed 's/old/new/g' filename > newfile
```

## Advanced Features

### Hold and Pattern Space

`sed` has two buffers: the pattern space (where the current line is held) and the hold space (a temporary buffer). Commands like `h`, `H`, `g`, and `G` manipulate these buffers for advanced text processing.

For example, to swap lines using hold space:

```bash
sed '1{h;d};2{H;g}' filename
```

### Branching and Flow Control

`sed` supports conditional branching with commands like `b` and `t`. These commands allow you to control the flow of operations based on conditions.

For example, to skip the next command if a pattern matches:

```bash
sed '/pattern/b; s/foo/bar/' filename
```

### Advanced Regular Expressions

For more complex patterns, `sed` supports extended regular expressions with the `-E` option:

```bash
sed -E 's/[A-Za-z]+/\U&/g' filename
```

This command converts all words to uppercase.

## Conclusion

The `sed` command is an incredibly powerful tool for text processing and transformation on Linux. By mastering its common options and configurations, you can perform a wide range of tasks, from simple text replacements to complex data manipulations. Embrace the learning process with enthusiasm, and you'll find that `sed` can significantly enhance your productivity on your Ubuntu 20.04 system.

Remember, practice makes perfect. Experiment with different `sed` commands and options to see how they work. Happy learning and happy coding! Enjoy your journey with `sed` and make the most of its capabilities!