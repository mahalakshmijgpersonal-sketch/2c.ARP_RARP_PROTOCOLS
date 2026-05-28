# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
Server.py 

```
mport socket

# Create socket
s = socket.socket()

# Connect to server
s.connect(('localhost', 8000))

while True:
    
    # Get IP address
    ip = input("Enter logical Address : ")

    # Send IP to server
    s.send(ip.encode())

    # Receive MAC address
    print("MAC Address :", s.recv(1024).decode())

```

Client.py

```
import socket

# Create socket
s = socket.socket()

# Bind host and port
s.bind(('localhost', 8000))

# Listen for client
s.listen(5)

print("Waiting for connection...")

# Accept client connection
c, addr = s.accept()

print("Connected with :", addr)

# IP and MAC address dictionary
address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True:
    
    # Receive IP address
    ip = c.recv(1024).decode()

    try:
        # Send MAC address
        c.send(address[ip].encode())

    except KeyError:
        # If IP not found
        c.send("Not Found".encode())

```
## OUPUT - ARP


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/70b9e150-c464-4068-9538-f0d9d7d3fd43" />

## PROGRAM - RARP

Server.py

```
import socket

s = socket.socket()

s.connect(('localhost', 9000))

while True:
    ip = input("Enter MAC Address : ")

    s.send(ip.encode())

    print("Logical Address", s.recv(1024)
```
Client.py

```
import socket

s = socket.socket()
s.bind(('localhost', 9000))
s.listen(5)

c, addr = s.accept()

address = {
    "6A:08:AA:C2": "192.168.1.100",
    "8A:BC:E3:FA": "192.168.1.99"
}

while True:
    ip = c.recv(1024).decode()

    try:
        c.send(address[ip].encode())

    except KeyError:
        c.send("Not Found".encode())

```


## OUPUT -RARP

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/073db837-a6fc-4f85-a99e-ec9692e92f89" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
