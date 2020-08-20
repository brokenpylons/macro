# macro

This is a script for when you get stuck into a loop of manually calling the same few commands over and over again and are too lazy to open the editor and make a script. The idea is similar to vim macros. You can record the commands to a register and then replay them.

[![asciicast](https://asciinema.org/a/221835.svg)](https://asciinema.org/a/221835)

## Installation

Install by cloning the repository and running:

```
sudo cp macro /usr/local/bin

# Or

sudo wget -qcO /usr/local/bin/macro https://raw.githubusercontent.com/brokenpylons/macro/master/macro
```

## Commands

| Command                               | Description                                                            |
| ------------------------------------- | ---------------------------------------------------------------------- |
|```macro record```                     | Record the macro (exit with ```C-d```)                                 |
|```macro``` or ```source macro```      | Replay the recorded macro in new or current environment                |
|```macro view```                       | Print the recorded commands to the terminal                            |
|```macro edit```                       | Edit the commands using ```$EDITOR```                                  |
|```macro save <file>```                | Save the macro to a file named ```<file>```                            |
|```source <(macro keep)```             | Keep the history of the current session when recording                 |
|```macro help```                       | Print the usage                                                        |
|```REGISTER=<register> source macro``` | Use the register ```<register>``` (default one is called ```default```)|

Each command can be called by using just the first letter (e.g. ```macro r``` instead of ```macro record```).

By sourcing ```macro keep``` the script is overriden by a function that also saves the history of the current session to a file, which is then loaded in the new shell when recording. That means you can use the up arrow to get previously called commands. To always enable this option you need to put this command to ```.bashrc```.

The script stores the registers and the history in the ```~/.local/share/macro``` directory.

## Aliases

The intended way to use multiple registers is to create an alias for each of them. You can do that by calling:
```
# Run macro in new bash env, then switch back to current bash env
alias <name>='REGISTER=<register> macro '

# Run macro in current bash env
alias <name>='REGISTER=<register> source macro '
```

For example, you can use the following configuration:
```
for x in {a..z}
do
    eval "alias q$x='REGISTER=$x source macro '"
done
```
This adds commands of the form ```q<register>``` (e.g. ```qq``` for register q). For recording you call ```qq r``` and then replay the macro using ```qq```.

To make the aliases persistent add them to ```.bashrc```.

## Contributing
If you find bugs or have any suggestions please open an issue. Pull requests are also welcome.

## License
This repository is placed under the GPL v3.0. See LICENSE for more details.
