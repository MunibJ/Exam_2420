# Exam_2420
# Created by: Munib Javed

## Description
Final exam for my `2420 class`
<br>
<br>
<br>
# Question 1: 
`How could you update most of the software on your Ubuntu OS?`

## Answer: sudo apt-get update
<br>
<br>
<br>

# Question 2: Fix the code with Vim and opy the code below into a new vim buffer

```
if [ $# -eq 1 ] ; then
  eco "Usage: $0 temperature[F|V|K]
        where the suffix:
        F    indicates input is in Fahrenheit (default)
        V    indicates input is in Celsius
        K    indicates input is in Kelvin"
   exit 1
fi

unit="$(eco $1|sed -e 's/[-[numbs]]*//g' | tr '[:lower:]' '[:upper:]' )"
temp="$(eco $1|sed -e 's/[^-[:digit:]]*//g')"
```

## Answer: 
For the `ECO`, I changed it to `ECHO` using the `:s` command.
<br>
For the `V` to `C` change, I used the `:s` command again.
I manually made the other changes such as in the unit and temp variables using `insert mode`.

The final code is:
![alt text](/Exam_2420/images/question2vimfile.png)

<br>
<br>
<br>

# Question 3: Using the man page for journalctl write a journalctl command that does the following:
`- print logs for the current boot`

`- logs should have a priority of warning or more important`

`- output in a nice pretty json.`

## Answer:
To find the manpage for journalctl, I used the `man` command.
<br>
Command: `man journalctl`
<br>
Picture: 
![alt text](/Exam_2420/images/question3manjournal.png)

<br>
I found some information about json files on the manpage.
<br>

I will be using the `json-pretty` option to print the logs in a nice pretty json.
<br>

Picture:
![alt text](/Exam_2420/images/question3json.png)

<br>

I will be using the `--priority` option to print logs with a priority of warning or more important. I found it in the manpage by scrolling down till I saw the options.

Picture:
![alt text](/Exam_2420/images/question3priority.png)

<br>

I will be using the `--boot` option to print logs for the current boot. I found this online and it worked.

The command is `journalctl --priority=warning --boot --json-pretty`

<br>


# Question 4: create a new regular user adduser or useradd with a home directory. You just need more than one regular user on the system to test your script.

## Answer:

I used the `adduser` command to create a new user and made 3 test users

Picture:
![alt text](/Exam_2420/images/question4adduser.png)

<br>

I then added passwords to the users using the `passwd` command.
<br>

Picture:
![alt text](/Exam_2420/images/question4apsswd.png)

<br>

I then created my bash script using the `vim` command and called it question4.sh and made it executable using the `chmod` command.I then made. I then made the bash script for the question.
<br>

The bash script I made is:
![alt text](/Exam_2420/images/question4bash.png)

<br>

And the output is:
![alt text](/Exam_2420/images/question4output.png)

<br>

I placed the script inside of a folder called `scripts` in my `/home/vagrant` directory.
<br>

Picture:

![alt text](/Exam_2420/images/question4dir.png)


<br>
<br>

# Question 5: Write a service file that runs your script from part 4

## Answer: 

I created a service file using the `vim` command and called it question4.service and made it executable using the `chmod` command. I placed the service file in the `/etc/systemd/system` directory.

Picture:
![alt text](/Exam_2420/images/question5service.png)

<br>

The service file I made is simple: 

```
[Unit]
Description=Find regular users and currently logged in users along with the shell script for the users and output a list

[Service]
Type=oneshot
ExecStart=/home/vagrant/script/question4.sh

[Install]
WantedBy=multi-user.target
```
<br>

I then moved the question4.service file over to my `/etc/systemd/system` directory. 
<br>

I then ran the `systemctl` command to enable the service and start the service. Following that, I ran the command `systemctl start` to start the service and `systemctl status` to check the status of the service.

Picture:
![alt text](/Exam_2420/images/question4servicefile.png)
<br>

This shows that the script ran once and completed and the service is now inactive.


# Question 6: Create a timer to run your script using Monotonic Timer, runs 1 minute after boot and again every day while unit is active

<br>

## Answer: 

I created a timer file using the `vim` command and called it `question4.timer` and made it executable using the `chmod` command.

The timer service file I made is simple: 

```
[Unit]
Description=Timer for running the find users service

[Timer]
OnBootSec=60
Unit=question4.service

[Install]
WantedBy=timers.target
```

I then moved the question4.timer file over to my `/etc/systemd/system` directory. 

Following that I ran the `systemctl` command to enable the timer and start the timer. 

Following that, I ran the command `systemctl start` to start the timer and `systemctl status` to check the status of the timer.

Picture:

![alt text](/Exam_2420/images/question6timer.png)



