# 4.Execution_of_NetworkCommands
## AIM :Use of Network commands in Real Time environment
## Software : Command Prompt And Network Protocol Analyzer
## Procedure: To do this EXPERIMENT- follows these steps:
<BR>
In this EXPERIMENT- students have to understand basic networking commands e.g cpdump, netstat, ifconfig, nslookup ,traceroute and also Capture ping and traceroute PDUs using a network protocol analyzer 
<BR>
All commands related to Network configuration which includes how to switch to privilege mode
<BR>
and normal mode and how to configure router interface and how to save this configuration to
<BR>
flash memory or permanent memory.
<BR>
This commands includes
<BR>
• Configuring the Router commands
<BR>
• General Commands to configure network
<BR>
• Privileged Mode commands of a router 
<BR>
• Router Processes & Statistics
<BR>
• IP Commands
<BR>
• Other IP Commands e.g. show ip route etc.
<BR>

## PROGRAM
# CLIENT.PY
```
import socket

s = socket.socket()
s.connect(('localhost', 10000))

while True:
    ip = input("Enter the website you want to ping (or type 'exit' to quit): ")
    s.send(ip.encode('utf-8'))
    if ip.lower() == 'exit':
        break
    print(s.recv(4096).decode('utf-8'))

s.close()
```
# SERVER.PY
```
import socket
import subprocess

s = socket.socket()
s.bind(('localhost', 10000))
s.listen(5)

print("Server listening on port 10000...")

c, addr = s.accept()
print(f"Connection from {addr}")

while True:
    try:
        hostname = c.recv(1024).decode('utf-8')

        if not hostname or hostname.lower() == 'exit':
            print("Client disconnected.")
            break

        result = subprocess.run(
            ["ping", hostname],
            capture_output=True,
            text=True
        )

        output = result.stdout

        c.send(output.encode('utf-8'))

    except Exception as e:
        c.send(f"Ping failed: {e}".encode('utf-8'))

c.close()
s.close()
```
## Output
<img width="1389" height="424" alt="Screenshot 2026-05-24 135237" src="https://github.com/user-attachments/assets/d799abaa-e24f-4955-84cd-2ad30a3bc108" />

## Result

  Thus Execution of Network commands Performed 
