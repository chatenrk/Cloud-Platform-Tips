# SAP Cloud Platform Tips and Tricks

**[Table of Contents]**

- [Quick Access Commands](#quick-access-commands)
  - [CF CLI Related](#cf-cli-related)
  - [Github Related](#github-related)
- [CF-CLI Tips](#cf-cli-tips)
- [Bash Terminal Tips](#bash-terminal-tips)
  - [Trunc Script](#trunc-script)

## Quick Access Commands

### CF CLI Related

- Help for CF CLI

  `cf --help (or) cf -h`

- Login to cloud foundry

  `cf login (or) cf l`

- List all services

  `cf services (or) cf s`

- Create service

  `cf create-service SERVICE PLAN SERVICE_INSTANCE [-b BROKER] [-c PARAMETERS_AS_JSON] [-t TAGS]`

  **For example**
  `cf create-service hana hana-shared test-hana-service`

  **where**

  - hana refers to service marketplace service
  - hana-shared is the plan relating to service above
  - test-hana-service is the instance name which would get created on SAP cloud platform

- Create Service Key
  `cf create-service-key SERVICE_INSTANCE SERVICE_KEY [-c PARAMETERS_AS_JSON]`

  **For example**
  `cf create-service-key test-hana-service default`
  **where**

  - SERVICE_INSTANCE is the name of service instance which was created above
  - SERVICE_KEY is the name of the service key

### HANA CLI Related

### Github Related

- Initialise a local git repository

  `git init`

- Add all modified entries into the git repository

  `git add .`

- Commit changes

  `git commit -m "Commit Message"`

- Add remote github repository

  `git remote add origin <<insert github repository name here>>`

- Push changes to remote repository

  `git push -u origin master`

## CF-CLI Tips

## Bash Terminal Tips

### Trunc Script

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
