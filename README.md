
**Socket Programming Example**

**Secret Flag:** 92146d257b83fc17e749fd35670b47bcc4254d0e409768b3c07db6eb83c547fa

**Description:**

This Python script demonstrates basic socket programming using TCP. It establishes a connection to a server, sends a message containing an identifier, processes mathematical expressions received from the server, evaluates these expressions, and sends the results back. The script also handles responses indicating success or failure.

**Code Explanation:**

- **Import the Socket Library:**

  ```python
  import socket
  ```

  This library provides the necessary functions for creating and managing sockets.

- **Define Hostname and Port:**

  ```python
  server_hostname = 'sample_server.py'
  default_server_port = 5211
  ```

  Specify the server's hostname and port number for connection.

- **Create a Socket Object:**

  ```python
  client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
  ```

  Create a socket using IPv4 and TCP protocol.

- **Connect to the Server:**

  ```python
  client_socket.connect((server_hostname, default_server_port))
  ```

  Establish a connection to the server using the specified hostname and port.

- **Send Data to the Server:**

  ```python
  message_from_client = "EECE7374 INTR 002665287"
  client_socket.send(message_from_client.encode())
  ```

  Send a message to the server, encoded as bytes.

- **Receive Data from the Server:**

  ```python
  message_to_client = client_socket.recv(4096)
  response = message_to_client.decode("utf-8")
  ```

  Receive and decode the response from the server.

- **Process Server Responses:**

  ```python
  while ((response.split())[1] == "EXPR"):
      print(response)
      a = str((response.split())[2])
      b = str((response.split())[3])
      c = str((response.split())[4])
      d = a + b + c
      answer = str(eval(d))
      message_from_client = "EECE7374 RSLT" + " " + answer
      print(message_from_client)
      client_socket.send(message_from_client.encode())
      message_to_client = client_socket.recv(4096)
      response = message_to_client.decode("utf-8")
  ```

  Evaluate mathematical expressions and send results back to the server.

- **Handle Final Responses:**

  ```python
  print(response)
  client_socket.close()
  ```

  Print the final server response and close the connection.

**How to Use:**

1. **Update Server Details:**
   - Modify `server_hostname` and `default_server_port` with the correct server details.

2. **Run the Script:**
   - Execute the script to start communication with the server and process responses.
   ```bash
   python socket_client.py
   ```

