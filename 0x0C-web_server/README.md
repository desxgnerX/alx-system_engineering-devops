0x0C. Web server

    By Sylvain Kalache

Concepts

For this project, students are expected to look at this concept:

    What is a Child Process?

Background Context

In this project, some of the tasks will be graded on 2 aspects:

    Is your web-01 server configured according to requirements
    Does your answer file contain a Bash script that automatically performs commands to configure an Ubuntu machine to fit requirements (meaning without any human intervention)

For example, if I need to create a file /tmp/test containing the string hello world and modify the configuration of Nginx to listen on port 8080 instead of 80, I can use emacs on my server to create the file and to modify the Nginx configuration file /etc/nginx/sites-enabled/default.

But my answer file would contain:

sylvain@ubuntu cat 88-script_example
#!/usr/bin/env bash
# Configuring a server with specification XYZ
echo hello world > /tmp/test
sed -i 's/80/8080/g' /etc/nginx/sites-enabled/default
sylvain@ubuntu

As you can tell, I am not using emacs to perform the task in my answer file. This exercise is aiming at training you on automating your work. If you can automate tasks that you do manually, you can then automate yourself out of repetitive tasks and focus your energy on something more interesting. For an SRE, that comes very handy when there are hundreds or thousands of servers to manage, the work cannot be only done manually. Note that the checker will execute your script as the root user, you do not need to use the sudo command.

A good Software Engineer is a lazy Software Engineer.

Tips: to test your answer Bash script, feel free to reproduce the checker environment:

    start an ubuntu:16.04 Docker container
    run your script on it
    see how it behaves

Check out the Docker concept page for more info about how to manipulate containers.
Resources

Read or watch:

    How the web works
    Nginx
    How to Configure Nginx
    Child process concept page
    Root and sub domain
    HTTP requests
    HTTP redirection
    Not found HTTP response code
    Logs files on Linux

For reference:

    RFC 7231 (HTTP/1.1)
    RFC 7540 (HTTP/2)

man or help:

    scp
    curl

Learning Objectives

At the end of this project, you are expected to be able to explain to anyone, without the help of Google:
General

    What is the main role of a web server
    What is a child process
    Why web servers usually have a parent process and child processes
    What are the main HTTP requests

DNS

    What DNS stands for
    What is DNS main role

DNS Record Types

    A
    CNAME
    TXT
    MX

Requirements
General

    Allowed editors: vi, vim, emacs
    All your files will be interpreted on Ubuntu 16.04 LTS
    All your files should end with a new line
    A README.md file, at the root of the folder of the project, is mandatory
    All your Bash script files must be executable
    Your Bash script must pass Shellcheck (version 0.3.7) without any error
    The first line of all your Bash scripts should be exactly #!/usr/bin/env bash
    The second line of all your Bash scripts should be a comment explaining what is the script doing
    You can't use systemctl for restarting a process

Quiz questions

Show
Your servers

| Name | Username | IP | State |
| | --- | --- | --- | --- | --- | | 1723-web-01 | ubuntu | 100.26.181.86 | running |
|

|
|
Tasks
0. Transfer a file to your server

mandatory

Write a Bash script that transfers a file from our client to a server:

Requirements:

    Accepts 4 parameters
        The path to the file to be transferred
        The IP of the server we want to transfer the file to
        The username scp connects with
        The path to the SSH private key that scp uses
    Display Usage: 0-transfer_file PATH_TO_FILE IP USERNAME PATH_TO_SSH_KEY if less than 3 parameters passed
    scp must transfer the file to the user home directory ~/
    Strict host key checking must be disabled when using scp

Example:

sylvain@ubuntu$ ./0-transfer_file
Usage: 0-transfer_file PATH_TO_FILE IP USERNAME PATH_TO_SSH_KEY
sylvain@ubuntu$
sylvain@ubuntu$ ssh ubuntu@8.8.8.8 -i /vagrant/sylvain 'ls ~/'
afile
sylvain@ubuntu$
sylvain@ubuntu$ touch some_page.html
sylvain@ubuntu$ ./0-transfer_file some_page.html 8.8.8.8 sylvain /vagrant/private_key
some_page.html                                     100%   12     0.1KB/s   00:00
sylvain@ubuntu$ ssh ubuntu@8.8.8.8 -i /vagrant/private_key 'ls ~/'
afile
some_page.html
sylvain@ubuntu$

In this example, I:

    remotely execute the ls ~/ command via ssh to see what ~/ contains
    create a file named some_page.html
    execute my 0-transfer_file script
    remotely execute the ls ~/ command via ssh to see that the file some_page.html has been successfully transferred

That is one way of publishing your website pages to your server.

Repo:

    GitHub repository: alx-system_engineering-devops
    Directory: 0x0C-web_server
    File: 0-transfer_file
