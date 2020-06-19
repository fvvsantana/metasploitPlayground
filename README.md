# Metasploit Playground

## Description

This project was created for a Security Engineering course in my bachelor program. The professor asked us to demonstrate a security attack using [Metasploit](https://www.metasploit.com/), but we ended up creating an environment that allows the execution of several different attacks.

The environment consists of a machine with Metasploit installed (attacker) and another machine with Metasploitable 2 installed (victim). In [this guide](https://metasploit.help.rapid7.com/docs/metasploitable-2-exploitability-guide) you can see examples of attacks that are possible to perform against the Metasploitable machine.

Docker was used to create the environment. For the attacker, the image used was [metasploitframework/metasploit-framework](https://hub.docker.com/r/metasploitframework/metasploit-framework). For the victim, the image used was [tleemcjr/metasploitable2](https://hub.docker.com/r/tleemcjr/metasploitable2).

# Pre-requisites
* [Docker Engine](https://docs.docker.com/get-docker/)

## Setting up environment

The environment will basically be set up opening the machine of the attacker in a terminal and the machine of the victim in another terminal.

Starting at the root of the project, enter the attacker's folder:
```
    cd attacker
```

This terminal will be the attacker's terminal. Now build the attacker's image:
```
    docker build -t "attacker" .
```

Open a new terminal window to be the victim's terminal. From the root of the project, enter the victim's directory and build its image:
```
cd victim
docker build -t "victim" .
```

In the terminal of the victim, when the download have finished, start the victim's container:
```
docker run -it --volume=/tmp/victim/:/data victim:latest
```
Note that a volume will be mounted in the path "/tmp/victim/" of your computer. This volume is useful in case you want to capture the traffic of data using tcpdump in the victim's terminal. You can save the capture in the "/data/" directory of the victim.

In the attacker's terminal, wait until the image is downloaded and then start the attacker's container:
```
docker run -it attacker:latest
```

You're all set.

## Usage

You can open the msfconsole in the attacker's terminal using the command:
```
./msfconsole -r docker/msfconsole.rc -y config/database.yml
```
This command starts msfconsole with some settings. It sets the LHOST attribute to the attacker's IP address. Also it starts a database to allow searches to be performed faster, among other settings.

After discovering the victim's IP address, you can use nmap inside the msfconsole to scan the possible vulnerable services of the victim to be exploited:
```
nmap -T4 -A -v victim_s_ip_address
```

Choose a service to exploit and have fun!

In case you missed it, [this guide](https://metasploit.help.rapid7.com/docs/metasploitable-2-exploitability-guide) has some examples of exploits to use.

In case you understand Portuguese, there is a [report](relatorio.pdf) with a didactic explanation of a simple attack using this environment.

## Tech stack
* Docker
* Metasploit
* Metasploitable 2

# Acknowledgments
Thanks to [Bruno](https://github.com/billionai) for collaborating in the writing of the report and in the presentation.
