# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM:
## SERVER
'''

import socket

server = socket.socket()

server.connect(('localhost', 9000))

print("Connected to sender\n")

while True:
    message = server.recv(1024).decode()

    if not message:
        break

    print("Frames received:", message)

    ack_msg = "ACK received successfully"

    server.send(ack_msg.encode())

server.close()

'''

## CLIENT
'''

import socket
import time

client = socket.socket()
client.bind(('localhost', 9000))

client.listen(1)
print("Waiting for receiver connection...")

conn, addr = client.accept()
print("Connected with:", addr)

frames = int(input("Enter total number of frames: "))
window = int(input("Enter window size: "))

data = list(range(1, frames + 1))

start = 0

while start < frames:
    end = min(start + window, frames)

    current_frames = data[start:end]

    print("\nSending frames:", current_frames)

    conn.send(str(current_frames).encode())

    ack = conn.recv(1024).decode()

    print("Receiver:", ack)

    time.sleep(1)

    start += window

print("\nAll frames sent successfully")

conn.close()
client.close()

'''
## OUPUT:

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
