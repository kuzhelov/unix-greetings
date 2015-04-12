# unix-greetings

## pgrep

Pgrep is a tool for searching for a specific process by its name (however, this is not the only possible parameter). 

Nevertheless, it is quite important to understand the fact that by default pgrep uses only first 15 letters of process name for finding a matching (according to [this](http://askubuntu.com/questions/157075/why-does-ps-aux-grep-x-give-better-results-than-pgrep-x)). In order to utilize a full command's name the `f` option should be used: 

**prep -f `process-pattern`**

## sed

Stream Editor. This is a noninteractive text editor primary usage area of which is to filter input data and provide the output. The formula described above could be easily pushed into pipes.

### Working princile

* each line of input is copied into a `pattern space` - internal buffer where editing operations are performed
* all sed commands are applied to the `pattern space` buffer in order of declaration
* all previous steps are applied to other lines if correspondent options are specified

Additional notes:

* if a command in a processing sequence changes content of the `pattern space` buffer, all the subsequent commands are applied to the modified content
* the original input file always stay unchanged due to the fact that sed operates on the copies of its lines

### Substitute replacement command

**.. | sed 'option' s/`pattern`/`replacement`/`flags`;`other-chained-actions`**

**Options**

* `-E` - ***not UNIX standardized, applicable to Mac*** - interpret regular expressions in extended (modern) form

**Pattern**

Is a regular expression in its basic or extended form (depending on related option being specified). Can include grouping expressions in the following form (extended): `fwd=(group-expression-here)`

**Replacement**

Represents string on which text fragment that match `pattern` will be replaced. Can include references to group matches in the following form: `/1 is the match of the first group. /2 is the match of the second`

**Flags**

Multiple flags can be combined - `.. | sed s/one/two/gp`.

* **g** - apply substitution to all strings of the input (stands for `global`)
* **p** - send modified version of `pattern space` to the output stream (stands for `print`). Effectively results in a double output of the strings that were modified - double output of their modified version.

**Other chained actions**

* **d** - delete the modified line of the `pattern space` - i.e., this line will not be sent to the output stream. This action will not prevent sending copied version of modified lines to the output stream (for example, those that were produced by the `p` flag)

** Usage examples **

`.. | sed s/one/two/gp;d` - will output only the lines where replacement `one` on `two` has taken place. Other lines will be skipped.

