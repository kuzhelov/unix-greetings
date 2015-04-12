# unix-greetings

## pgrep

Pgrep is a tool for searching for a specific process by its name (however, this is not the only possible parameter). 

Nevertheless, it is quite important to understand the fact that by default pgrep uses only first 15 letters of process name for finding a matching (according to [this](http://askubuntu.com/questions/157075/why-does-ps-aux-grep-x-give-better-results-than-pgrep-x)). In order to utilize a full command's name the `f` option should be used: 

**prep -f `process-pattern`**
