⚙️ # Concurrent FTP Server: Multi-Client File Transfer System

📌 # Project Overview

This project is an industrial-grade Concurrent FTP Server implemented in C on Linux. It facilitates simultaneous file downloads for multiple clients using socket programming and process-level isolation. The server is designed to demonstrate high-concurrency handling and reliable data transmission through a custom communication protocol.

🛠 # Tech Stack & Environment

Language: C (C11 standard)

Platform: Linux (Ubuntu/Debian recommended)

Networking: TCP/IP Socket Programming

Concurrency: Multi-process (fork-based)

System Calls: socket, bind, listen, accept, fork, stat, read, write

📦 Dependencies & Requirements

This project relies strictly on the Linux Kernel API and standard libraries. Ensure the following are installed:

GCC Compiler: sudo apt-get install build-essential

Linux Environment: Required for POSIX-compliant system calls (sys/socket.h, unistd.h, etc.).

Network Access: Permissions to bind to local ports (ports > 1024 recommended).

🧠 Core Logic

The application implements a Concurrent Child-per-Client architecture:

Passive Open: The Server initializes a socket, binds it to a port, and enters a listen state.

Concurrency via fork(): Upon a successful accept(), the parent process spawns a child process. This ensures the server remains non-blocking and can handle new connections while the child manages the file transfer.

Protocol-Driven Transfer:

Handshake: Client sends a filename request.

Header: Server calculates file size using stat() and sends an OK <size> header.

Chunking: The file is streamed in 1KB - 4KB chunks to optimize buffer usage and prevent memory exhaustion.

Resource Cleanup: The server implements signal handling or wait() logic to prevent the accumulation of "zombie" processes.

🚀 Execution Steps

1. Clone and Navigate

git clone [https://github.com/your-username/concurrent-ftp-server.git](https://github.com/your-username/concurrent-ftp-server.git)
cd concurrent-ftp-server


2. Compilation

Compile both the server and client components using gcc:

# Compile Server
gcc server.c -o server

# Compile Client
gcc client.c -o client


3. Running the Server

Start the server by specifying a port number:

./server 9090


4. Running the Client

In a new terminal, request a file from the server:

# Usage: ./client <Server_IP> <Port> <Filename>
./client 127.0.0.1 9090 Demo.txt


📂 Project Structure

server.c: Main server logic (Socket init, Forking, File Transmission).

client.c: Client implementation (Handshake, Buffer writing).

Demo.txt: Sample file for testing transfers.

👤 Author

Sakshi Bhapkar Final-Year Information Technology Engineering Student
