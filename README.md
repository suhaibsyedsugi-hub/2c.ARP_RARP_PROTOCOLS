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
```
server.py:

import socket

# Create a socket object
s = socket.socket() 
s.bind(('localhost', 8000)) 
s.listen(5) 
print("ARP Server is running and waiting for client request...")

c, addr = s.accept()

# IP to MAC mapping dictionary
address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True: 
    try:
        # Receive IP address from client
        ip = c.recv(1024).decode()
        if not ip:
            break
            
        # Look up MAC address and send it back
        if ip in address:
            c.send(address[ip].encode())
        else:
            c.send("Not Found".encode())
    except Exception as e:
        print("Connection closed or Error:", e)
        break

c.close()

client .py:

import socket

s = socket.socket() 
s.connect(('localhost', 8000)) 

while True:
    ip = input("Enter logical Address (IP): ")
    if ip.lower() == 'exit':
        break
        
    s.send(ip.encode())
    mac_address = s.recv(1024).decode()
    print("MAC Address:", mac_address)

s.close()



```


## OUPUT - ARP
<img width="655" height="87" alt="image" src="https://github.com/user-attachments/assets/cbd4968c-4ea3-4dfd-8a78-adb8cc32934f" />

<img width="660" height="173" alt="image" src="https://github.com/user-attachments/assets/1049cb49-6a21-43f1-ad44-64187ae05f67" />

## PROGRAM - RARP
```
server.py:

import socket

# Create a socket object
s = socket.socket()
s.bind(('localhost', 9000)) 
s.listen(5) 
print("RARP Server is running and waiting for client request...")

c, addr = s.accept()

# MAC to IP mapping dictionary
address = {
    "6A:08:AA:C2": "192.168.1.100",
    "8A:BC:E3:FA": "192.168.1.99"
}

while True: 
    try:
        # Receive MAC address from client
        mac = c.recv(1024).decode()
        if not mac:
            break
            
        # Look up IP address and send it back
        if mac in address:
            c.send(address[mac].encode())
        else:
            c.send("Not Found".encode())
    except Exception as e:
        print("Connection closed or Error:", e)
        break

c.close()


client.py:

import socket 

s = socket.socket() 
s.connect(('localhost', 9000)) 

while True:
    mac = input("Enter MAC Address: ")
    if mac.lower() == 'exit':
        break
        
    s.send(mac.encode())
    logical_address = s.recv(1024).decode()
    print("Logical Address (IP):", logical_address)

s.close()


```
## OUPUT -RARP

<img width="653" height="84" alt="image" src="https://github.com/user-attachments/assets/15316cab-0237-49fc-8394-cb938f8076ed" />

<img width="651" height="120" alt="image" src="https://github.com/user-attachments/assets/d845ef9d-317b-44fb-a7c3-774ed7f0e1e7" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
