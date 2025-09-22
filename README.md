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
import os

HOST = '127.0.0.1'
PORT = 65432

def send_file(filename, conn):
    if os.path.isfile(filename):
        file_size = os.path.getsize(filename)
        conn.sendall(f"EXISTS {file_size}".encode('utf-8'))

        client_response = conn.recv(1024).decode('utf-8')
        if client_response == 'READY':
            with open(filename, 'rb') as f:
                chunk = f.read(1024)
                while chunk:
                    conn.sendall(chunk)
                    chunk = f.read(1024)
            print(f"File '{filename}' sent successfully.")
    else:
        conn.sendall(b'NOT_EXISTS')

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as server_socket:
    server_socket.bind((HOST, PORT))
    server_socket.listen()
    print(f"File server is listening on {HOST}:{PORT}")

    while True:
        conn, addr = server_socket.accept()
        with conn:
            print(f"Connected by {addr}")
            filename = conn.recv(1024).decode('utf-8')
            print(f"Client requested file: {filename}")
            send_file(filename, conn)
```

### CLIENT :
```
import socket
import os

HOST = '127.0.0.1'
PORT = 65432

filename = input("Enter the filename you want to download: ")

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.connect((HOST, PORT))
    s.sendall(filename.encode('utf-8'))

    response = s.recv(1024).decode('utf-8')
    if response.startswith("EXISTS"):
        _, size = response.split()
        file_size = int(size)
        print(f"File '{filename}' exists on server, size: {file_size} bytes.")

        s.sendall(b'READY')
        received_size = 0
        with open('received_' + filename, 'wb') as f:
            while received_size < file_size:
                data = s.recv(1024)
                if not data:
                    break
                f.write(data)
                received_size += len(data)
                print(f"Received {received_size} of {file_size} bytes")

        print(f"File '{filename}' received and saved as 'received_{filename}'")
    else:
        print("File does not exist on server.")

```


## OUTPUT :

### SERVER :
<img width="667" height="196" alt="3c server" src="https://github.com/user-attachments/assets/b4552f81-8912-4de9-81eb-caa366da519d" />

### CLIENT :
<img width="607" height="220" alt="3c client" src="https://github.com/user-attachments/assets/ebfeed7f-3ab8-495e-a147-7edbaf7b4688" />


## RESULT:
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
