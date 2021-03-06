# Bash Terminal Tips

**[Table of Contents]**

- [Trunc Script](#trunc-script)

## Trunc Script

I am a big fan of the terminal, and it’s my preferred work environment for many reasons.

I use the Cloud Foundry CLI `cf` frequently in my work on the SAP Cloud Platform but the output options are limited, and sometimes hard to read. One example is the output from `cf apps` or `cf services` (there are short versions of these two commands, `cf a` and `cf s` respectively).

This screenshot shows some typical output from the `cf s` command:

![](https://blogs.sap.com/wp-content/uploads/2020/04/Screenshot-2020-04-07-at-09.05.18.png)

There’s a lot of information and it wraps onto new lines. Most of the time my focus is on the names of the service instances, and perhaps the service & plan combination they represent – the information towards the end of the line is less important to me. But it’s still being output and making the entire results difficult to read.

With the use of two venerable shell commands, we can fix that.

`[tput](https://en.wikipedia.org/wiki/Tput)` will give us information on the current terminal capabilities. Running `tput cols` returns the number of columns in the current terminal.

[`cut`](<https://en.wikipedia.org/wiki/Cut_(Unix)>) will slice and dice data in many ways; I use it to pick out various fields from output lines, but it can also pick out ranges of characters too.

A combination of these two commands, also making use of the [command substitution](http://www.tldp.org/LDP/abs/html/commandsub.html) technique with `$(...)` (this is the newer & better version of using `` `...` ``backticks) gives us the ability to truncate the output so that it’s a lot more readable:

![](https://blogs.sap.com/wp-content/uploads/2020/04/Screenshot-2020-04-07-at-09.06.22.png)

Here’s a breakdown of the command:

`cf s | cut -c -$(tput cols)`

Read it like this:

1.  Run the `cf s` command
2.  Pipe the STDOUT of that into the STDIN of the `cut` command
3.  To the `cut` command execution, supply a value for the `-c` option which selects specific characters
4.  Which specific characters? Well, the range (x-y) that goes from 1 (implicit) to whatever the command `tput cols` outputs.
5.  In the case of my terminal shown in the screenshots, `tput cols` tells me there are 101 columns, so the effective value for the range given to `-c` is 1-101.

We can make this useful combination into a handy function by defining a shell function, like this:

`trunc () { cut -c -$(tput cols); }`

Now we can use `trunc` like this:

`cf s | trunc`

which gives us the same thing. Lovely!

![](https://blogs.sap.com/wp-content/uploads/2020/04/Screenshot-2020-04-07-at-09.07.14.png)
