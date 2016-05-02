## Automating Scripts with Cron

Documentation for managing automation shell scripts.

To run a script from the command line use:

```bash
$ bash script-name.sh
```

##Job Schedule Setup

Use `cron` tasks to setup routine jobs.  Can [use a website](http://www.cronmaker.com/) to help configure when jobs run.

To list your cron tasks:
```bash
$ crontab -l
```

To create a new `cron` task:
```bash
$ crontab -e
```

Edit the file `crontab` file so it looks like the following format:
```bash
$ when-to-run
```

For Example, to run a script every day at 6pm, your crontab file should look like:
```bash
0 0 18 1/1 * ? * ~/Script/my-script.sh
```



