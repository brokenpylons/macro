# macro
This is a script for people that get stuck into a loop of manually calling the same few commands over and over again and are too lazy to open the editor and make a script. The idea is similar to vim macros. You can record the commands to a register and then replay them.

## Installation

Install by cloning the repository and running:

```
sudo cp macro /usr/local/bin
```

## Commands

| Command                        | Description                                                            |
| -----------------------------  | ---------------------------------------------------------------------- |
|```macro record```              | Record the macro                                                       |
|```macro```                     | Replay the recorded macro                                              |
|```macro view```                | Print the recorded commands to the terminal                            |
|```macro edit```                | Edit the commands using ```$EDITOR```                                  |
|```macro save <file>```         | Save the macro to a file named ```<file>```                            |
|```source <(macro keep)```      | Keep the history of the current session when recording                 |
|```macro help```                | Print the usage                                                        |
|```REGISTER=<register> macro``` | Use the register ```<register>``` (default one is called ```default```)|

Each command can be called by using just the first letter (e.g. ```macro r``` instead of ```macro record```).

By soucing ```macro keep``` the script is overriden by a function that also saves the current history to a file, which is then loaded in the new shell when recording. That means you can use the up arrow to get previously called commands. I suggest you call this in your ```.bashrc```.

The script stores the registers and the history in the ```~/.local/share/macro``` directory.

## Aliases

The recommended way to use multiple registers is to create an alias for each of them. You can do that by calling:
```
alias <name>='REGISTER=<register> macro '
```

For example, I use the following configuration:
```
for x in {a..z}
do
    eval "alias q$x='REGISTER=$x macro '"
done
```
This adds commands of the form ```q<register>``` (e.g. ```qq``` for register q). For recording I call ```qq r``` and then replay the macro using ```qq```.

To make the aliases persistent add them to ```.bashrc```.

## License
This repository is placed under the GPL v3.0. See LICENSE for more details.
