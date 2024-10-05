# Custom Commands

Custom commands are an abstraction of CLI commands. The developer abstracts command operations into blocks,
which can be used by himself and the users to build command-chains. These custom chains represent custom commands.

A command chain is made up of blocks from different categories. Each of these blocks belong to a different categories
and serve different purposes.

User defined command chains are loaded at runtime, and executed if needed.

## Command Blocks

Command blocks can be classified by their different categories. Laid out below are the four core block categories;

<tabs>
    <tab title="Parameter Block">
     Parameter blocks signify an argument to be passed to the program. These can have defined types.
    </tab>
    <tab title="Condition Block">
         Purpose: A block that modifies or conditions the chain, based on external factors, logic, or transformations.
        Example: A block that checks for the day of the week or modifies input data before it reaches the function block.
        The developer can define blocks that hold can certain value, and have those depend on external factors.
        For example: A variable block "home", that can hold different locations depending on tghe day of the week, which
        is checked at runtime.
    </tab>
    <tab title="Function Block">
        A function block is a block defined by the developer that takes some number of arguments, and outputs the
        result to a Termination block.
    </tab>
    <tab title="Termination Block">
        Termination blocks are placed at the end of a chain and determine what is to be done with the output of a
        function block. These can be set up to print to the console, write to a file, or even email.
    </tab>
</tabs>

# Command Chain Examples

A 'connection' command that is fed 2 arguments, and is told to print it in simple form to the terminal.
<procedure title="[ARG] - [ARG] - [CONNECTION] - [CONSOLE]" id="some_procedure" collapsible="true">
    <step>Ask 2 arguments from the user</step>
    <step>Pass the two arguments to the 'connection' function</step>
    <step>Pass the output to a termination block "console", which will probably output it to the console.</step>
</procedure>


A timetable command that which takes 1 argument, which it will
output nicely to the terminal"
<procedure title="[PARAM] - [TIMETABLE] - [PRINT-FANCY]" id="example_2" collapsible="true">
    <step>Take 1 argument from the user.</step>
    <step>Pass the argument to the 'timetable' function</step>
    <step>Pass the output to a termination block "print-fancy", which will probably print it out 'fancy'.</step>
</procedure>


A sum function
<procedure title="[SUM] - [PARAM...] - [STDOUT]" id="example_3" collapsible="true">
    <step>The user is required to use the name "sum" for the function.</step>
    <step>Take a variable amount of integers from the user.</step>
    <step>Give the arguments to the 'sum' function block.</step>
    <step>Print to stdout</step>
</procedure>


``` 
> myapp sum 3 4 5 ...
```


---

> These blocks are defined by the developer itself, and it is up to them to implement the different outputs 
> to the possible operators. This is best done with interfaces.


# Block Definition Example

Here I will describe how one of these blocks might look like. Take for example a param block.

```
[PARAM]

Block name: "Station"
Type: String
Restrictions: 
```

This would create a developer defined Param Block "Station". The developer itself can use this block to craft his 
own commands.

If the developer enables the user to create custom commands (which Isomer encourages), they can also use this block.
The following example shows the result of a chain builder:

``` 
[STATION] - [CONDITION:value] - [CONNECTION] - [CONSOLE]

The user has created a command that defines one "constant" station 
"Zingem", and only has to supply one more. The condition here is 
defined by the developer and can be for example, a different station 
for each day of the week.

This command will be of the form

myapp arg

The user has chosen to output the result of CONNECTION to the
terminal.
```


> This is an abstract and high-level overview of the structure. The technical implementation is not relevant to the
> idea and function.


# Chain Builders

A program should enable users to build their own chains, given developer defined blocks. Isomer ships with a 
very rudimentary chain builder that allows users to combine blocks that are defined in the source code. However,
a custom solution fitting the function and feel of the program may be better suited.

## Glossary

Block
: An Isomer object that represents a piece of a custom command chain.

Verifier
: Internal algorithm that checks soundness of a chain.