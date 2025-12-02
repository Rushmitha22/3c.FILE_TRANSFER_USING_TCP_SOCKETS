# EXPERIMENT 3C : CREATION FOR FILE TRANSFER USING TCP SOCKETS :
## NAME : RUSHMITHA R 
## REGISTRATION NUMBER : 212224040281
## AIM:
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM :
### SERVER :
```
import socket

HOST = "0.0.0.0"
PORT = 8080
BUFFER_SIZE = 1024

server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server_socket.bind((HOST, PORT))

server_socket.listen(1)
print("Server waiting for client...")

conn, addr = server_socket.accept()
print("Connected to:", addr)


with open("send.txt", "rb") as file:
    data = file.read()
    conn.sendall(data)

print("File sent successfully!")

conn.close()
server_socket.close()

```

### CLIENT :
```
import socket

SERVER_IP = "127.0.0.1"
PORT = 8080
BUFFER_SIZE = 1024


client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)


client_socket.connect((SERVER_IP, PORT))
print("Connected to server.")


with open("received.txt", "wb") as file:
    while True:
        data = client_socket.recv(BUFFER_SIZE)
        if not data:
            break
        file.write(data)

print("File received successfully!")

client_socket.close()

```


## OUTPUT :

### SERVER :
<img width="667" height="196" alt="3c server" src="https://github.com/user-attachments/assets/b4552f81-8912-4de9-81eb-caa366da519d" />

### CLIENT :
<img width="607" height="220" alt="3c client" src="https://github.com/user-attachments/assets/ebfeed7f-3ab8-495e-a147-7edbaf7b4688" />


## RESULT:
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
