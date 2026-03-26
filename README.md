# 3a.CREATION FOR ECHO CLIENT AND ECHO SERVER USING TCP SOCKETS
# AIM
To write a python program for creating Echo Client and Echo Server using TCP
Sockets Links.
## ALGORITHM:
1. Import the necessary modules in python
2. Create a socket connection to using the socket module.
3. Send message to the client and receive the message from the client using the Socket module in
 server .
4. Send and receive the message using the send function in socket.
## PROGRAM
server.py
```
import socket
import threading

def handle_client(conn, addr):
    print(f"Connected to {addr}")
    
    while True:
        try:
            data = conn.recv(1024).decode()
            
            if not data:
                break
            
            print(f"Received from {addr}: {data}")
            conn.send(f"Echo: {data}".encode())
        
        except:
            break
    
    print(f"Connection closed with {addr}")
    conn.close()


server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

host = "127.0.0.1"
port = 12345

server.bind((host, port))
server.listen(5)

print("Server is running and waiting for connections...")

while True:
    conn, addr = server.accept()
    
    client_thread = threading.Thread(target=handle_client, args=(conn, addr))
    client_thread.start()
```
client.py
```
import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

host = "127.0.0.1"
port = 12345

client.connect((host, port))

print("Connected to server. Type 'exit' to quit.")

while True:
    message = input("Enter message: ")
    
    if message.lower() == "exit":
        client.send("Client disconnected".encode())
        break
    
    client.send(message.encode())
    
    response = client.recv(1024).decode()
    print("Server says:", response)

client.close()
```

## OUPUT
<img width="835" height="229" alt="image" src="https://github.com/user-attachments/assets/930ecd8d-6ced-49ce-a544-2d50272f7064" />

## RESULT
Thus, the python program for creating Echo Client and Echo Server using TCP Sockets Links 
was successfully created and executed.
