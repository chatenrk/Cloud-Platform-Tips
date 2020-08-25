# SAP Cloud Platform Tips and Tricks

**[Table of Contents]**

- [Quick Access Commands](#quick-access-commands)
  - [CF CLI Related](#cf-cli-related)
  - [HANA CLI Related](#hana-cli-related)
  - [Github Related](#github-related)
- [SQL Commands](#sql-commands)
  - [Create User](#create-user)
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

  **where**

  - SERVICE refers to service marketplace service
  - PLAN is the plan relating to service above
  - SERVICE_INSTANCE is the instance name which would get created on SAP cloud platform

  **Example**
  `cf create-service hana hana-shared test-hana-service`

- Create Service Key

  `cf create-service-key SERVICE_INSTANCE SERVICE_KEY [-c PARAMETERS_AS_JSON]`

  **where**

  - SERVICE_INSTANCE is the name of service instance which was created above
  - SERVICE_KEY is the name of the service key

  **Example**
  `cf create-service-key test-hana-service default`

- Create User Provided Service
  `cf create-user-provided-service SERVICE_INSTANCE [-p CREDENTIALS] [-l SYSLOG_DRAIN_URL] [-r ROUTE_SERVICE_URL] [ -t TAGS]`

  **where**

  - SERVICE_INSTANCE is the name of service instance which needs to be created
  - CREDENTIALS is a JSON object, sample JSON as below

  ```shell
  {\"user\":\"CUPS_SFLIGHT\",\"password\":\"<Password>\",\"driver\":\"com.sap.db.jdbc.Driver\",\"tags\":[\"hana\"] , \"schema\" : \"SFLIGHT\" }"
  ```

### HANA CLI Related

- HANA CLI Help

  `hana-cli help`

- HANA CLI Connect

  `hana-cli connect`

- Open database explorer

  `hana-cli opendbx`

- Check status of Hana Database

  `hana-cli status`

- Connect ServiceKey and service and prepare default-env.json

  `hana-cli serviceKey [instance] [key]`

  **where**

  - instance is the name of the hana service instance created in cloud platform(via CLI or directly)
  - key is the service created for the above service

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

## SQL Commands

### Create user

Create a user via SQL command. This is especially helpful when technical users are needed to be created, and grnats need to be done for a User provided service to work and provide cross-schema access

```shell
CREATE USER CUPS_SFLIGHT PASSWORD "<Password>" SET PARAMETER CLIENT = '001' SET USERGROUP DEFAULT;
ALTER USER CUPS_SFLIGHT DISABLE PASSWORD LIFETIME;
GRANT SELECT ON SCHEMA SFLIGHT TO CUPS_SFLIGHT WITH GRANT OPTION;
GRANT SELECT METADATA ON SCHEMA SFLIGHT to CUPS_SFLIGHT WITH GRANT OPTION;
```

### Grant Role

Grant schema roles to users created

```shell
CREATE ROLE SFLIGHT_CONTAINER_ACCESS;
GRANT SELECT, SELECT METADATA ON SCHEMA SFLIGHT TO SFLIGHT_CONTAINER_ACCESS WITH GRANT OPTION;
GRANT SFLIGHT_CONTAINER_ACCESS TO CUPS_SFLIGHT WITH ADMIN OPTION;

```

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
