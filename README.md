# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
**SERVER**
```
import socket

# Create server socket
server = socket.socket()

# Bind address and port
server.bind(('localhost', 8000))

# Listen for connection
server.listen(1)

print("Server waiting for connection...")

# Accept client connection
client, addr = server.accept()

print("Connected to:", addr)

# Input total messages
total = int(input("Enter number of packets: "))

# Create packet list
packets = ["Msg" + str(i) for i in range(total)]

# Window size
window = int(input("Enter window size: "))

start = 0

while start < len(packets):

    # Current window packets
    data = packets[start:start + window]

    print("Sending:", data)

    # Send data
    client.send(str(data).encode())

    # Receive ACK
    ack = client.recv(1024).decode()

    print("Client:", ack)

    # Move window
    start += window

print("Transmission completed")

client.close()
server.close()
```
**CLIENT**
```
import socket

# Create client socket
client = socket.socket()

# Connect to server
client.connect(('localhost', 8000))

print("Connected to server")

while True:

    # Receive packet data
    data = client.recv(1024).decode()

    if not data:
        break

    print("Received:", data)

    # Send acknowledgement
    client.send("ACK Received".encode())

client.close()

```
## CODE
**SERVER**
<img width="1920" height="1080" alt="Screenshot 2026-05-14 111101" src="https://github.com/user-attachments/assets/526613d2-c461-4967-8ace-82788f989064" />

**CLIENT**
<img width="1920" height="1080" alt="Screenshot 2026-05-14 111114" src="https://github.com/user-attachments/assets/aa145681-7235-46e2-9052-a5732a4e9538" />

## OUPUT
<img width="1920" height="1080" alt="Screenshot 2026-05-14 111030" src="https://github.com/user-attachments/assets/a841ea79-9e1b-468c-afc5-0563058ce2d0" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
