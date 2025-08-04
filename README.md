
# Peer-to-Peer File Sharing System

Run instructions

This document explains how to set up, configure, and run the P2P File Sharing System implemented in C++. The project is compatible with **Linux** and **macOS**. For **Windows** users, instructions are provided to set up a Linux virtual machine.

---

## 1. Prerequisites and Dependencies

- **Operating System:** Linux (Ubuntu recommended) or macOS  
- **C++ Compiler:** g++ (GCC) or clang++  
- **Libraries:** `pthread`, `sys/socket`, `fstream`, standard C++ STL  
- **Git:** For cloning the repository

### For macOS:
Ensure Xcode Command Line Tools are installed:
```bash
xcode-select --install
```

### For Linux:
Install build essentials:
```bash
sudo apt update
sudo apt install build-essential git
```

---

## 2. Cloning the Project

Clone the project repository from GitHub:
```bash
git clone <your-github-repo-link>
cd <repo-directory>
```

---

## 3. Building the Project

Compile the tracker and node programs:
```bash
g++ -std=c++17 -pthread tracker.cpp -o tracker
g++ -std=c++17 -pthread node.cpp -o node
```

---

## 4. Running the Project (Local/Network)

### A. Start the Tracker (must be started first):
```bash
./tracker
```
- By default, the tracker listens on `127.0.0.1:12345` (see `config.h`).

### B. Start a Node:
```bash
./node <node_id>
```
- Each node requires a unique integer `node_id` (e.g., 1, 2, 3, ...).

### C. File Management:
- Each node has a directory: `node_files/node<node_id>/`
- To share a file, place it in your node's directory.

### D. Registering and Sharing Files:
In the node terminal, use:
```bash
send <filename>      # Register and share a file with the tracker
search <filename>    # Find which nodes have a file
download <filename>  # Download a file from other nodes
exit                 # Gracefully leave the network
```

### E. Tracker IP Configuration:
- **Localhost:** Use `127.0.0.1` for tracker IP.  
- **LAN (WiFi/Hotspot):** On the tracker machine, run `ip a` to find its IP address.  
  On all nodes, update the tracker IP in `config.h`:
```cpp
TRACKER_IP = "<tracker-device-ip>";
```
Rebuild the project after changing the IP.

---

## 5. Special Notes & Troubleshooting

- **Ports:** Ensure no firewall blocks UDP ports used by the tracker and nodes.  
- **Multiple Nodes:** You can run multiple nodes on the same machine by using different `node_id` values and separate terminals.  
- **Logs:** Logs are stored in the `logs/` directory for both tracker and nodes.  
- **File Directory:** All files to be shared or downloaded are managed in `node_files/node<node_id>/`.

---

## 6. Example Workflow

1. Start the tracker:
```bash
./tracker
```

2. Start two nodes in separate terminals:
```bash
./node 1
./node 2
```

3. Place `example.txt` in `node_files/node1/`

4. In node 1 terminal:
```bash
send example.txt
```

5. In node 2 terminal:
```bash
search example.txt
download example.txt
```

---
