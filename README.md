# XenonStack-Assignment1
# Problem Statement And Solution:

 Scenario: There is a customer who came to you with a problem to have a custom linux
command for his operations. Our task is to understand the problem and create a linux
command via bash script as per the instructions.

* Command name - internsctl
* Command version - v0.1.0
# Section A
1. I want a manual page of command so that I can see the full documentation of the command.
For example if you execute the command
man ls
as output we get the doc and usage guidelines. Similarly if I execute man internsctl I want
to see the manual of my command.
2. Each linux command has an option --help which helps the end user to understand the use
cases via examples. Similarly if I execute internsctl --help it should provide me the
necessary help

3. I want to see version of my command by executing
internsctl --version
---
* <b>Solution:</b>

<b>step-1:</b> Code Provided in SecA file

<b>step-2:</b> chmod +x internsctl

<b>step-3:</b> internsctl --help

<b>step-4:</b> internsctl --version

---

# Section B
I want to execute the following command for -
* Part1 | Level Easy
I want to get cpu information of my server through the following command:

$ internsctl cpu getinfo
Expected Output -
I want similar output as we get from lscpu command

I want to get memory information of my server through the following command:
$ internsctl memory getinfo
Expected Output
I want similar output as we get from free command

---
* <b>Solution:</b>

<b>step-1:</b> Code provided in SecB_part1 add it to previous code

<b>step-3:</b> chmod +x internsctl.sh

<b>step-4:</b> internsctl cpu getinfo & 
                internsctl memory getinfo

---

* Part2 | Level Intermediate
I want to create a new user on my server through the following command:
$ internsctl user create <username>
Note - above command should create user who can login to linux system and access his home
directory

I want to list all the regular users present on my server through the following command:
$ internsctl user list

If want to list all the users with sudo permissions on my server through the following command:
$ internsctl user list --sudo-only

---

* <b>Solution:</b>

<b>step-1:</b> 


<b>step-2:</b> 
function create_user() {
    if [ -z "$2" ]; then
        echo "Error: Missing username. Usage: internsctl user create <username>"
        exit 1
    fi
sudo useradd -m "$2"
echo "User '$2' created successfully."
}

function list_users() {
    cut -d: -f1 /etc/passwd
}


function list_sudo_users() {
    getent group sudo | cut -d: -f4 | tr ',' '\n'
}

<b>step-3:</b>  
case "$1" in
user)
        if [ "$2" == "create" ]; then
            create_user "$@"
        elif [ "$2" == "list" ]; then
            if [ "$3" == "--sudo-only" ]; then
                list_sudo_users
            else
                list_users
            fi
        else
            echo "Invalid subcommand for 'user'. Use 'internsctl user create <username>' or 'internsctl user list [--sudo-only]'."
            exit 1
        fi
        ;;
    *)
        echo "Invalid option. Use 'internsctl --help' for usage guidelines."
        exit 1
        ;;
esac

<b>step-4:</b> chmod +x internsctl.sh

<b>step-5:</b> 
1. internsctl user create testuser
2. internsctl user list
3. internsctl user list --sudo-only

---

* Part3 | Advanced Level
By executing below command I want to get some information about a file
$ internsctl file getinfo <file-name>
Expected Output [make sure to have the output in following format only]
xenonstack@xsd-034:~$ internsctl file getinfo hello.txt
File: hello.txt
Access: -rw-r--r--
Size(B): 5448
Owner: xenonstack

Modify: 2024-01-03 17:34:44.616123431 +0530

In case I want only specific information then I must have a provision to use options
$ internsctl file getinfo [options] <file-name>
--size, -s to print size
--permissions, -p print file permissions
--owner, o print file owner
--last-modified, m
