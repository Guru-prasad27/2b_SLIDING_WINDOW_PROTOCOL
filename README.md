# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
To implement the Sliding Window Protocol for reliable and efficient frame transmission, allowing multiple frames to be sent before acknowledgment to improve throughput.
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
# Server.py
```
import socket 
s = socket.socket() 
s.bind(('localhost', 8000)) 
s.listen(1) 
print("Waiting for connection...") 
conn, addr = s.accept() 
print("Connected to", addr) 
while True: 
    data = conn.recv(1024).decode() 
    if not data: 
        break 
    print("Frames received:", data) 
    ack = "ACK for " + data 
    conn.send(ack.encode()) 
conn.close()
```
# Clint.py
```
import socket 
s = socket.socket() 
s.connect(('localhost', 8000)) 
n = int(input("Enter number of frames: ")) 
w = int(input("Enter window size: ")) 
frames = list(range(1, n+1)) 
i = 0
while i < n: 
    send_frames = frames[i:i+w] 
    msg = " ".join(map(str, send_frames)) 
    print("Sending frames:", msg) 
    s.send(msg.encode()) 
    ack = s.recv(1024).decode() 
    print("Received:", ack) 
    i += w 
s.close()
```
## OUPUT
# Server.py
<img width="390" height="134" alt="Screenshot 2026-05-12 160507" src="https://github.com/user-attachments/assets/3e2e049c-3f29-4d75-9529-eecdf2aef763" />

# Clint.py
<img width="381" height="240" alt="Screenshot 2026-05-12 160554" src="https://github.com/user-attachments/assets/938e35f1-9de4-4d51-a8e1-8380a784405f" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
