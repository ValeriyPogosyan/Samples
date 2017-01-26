# BioConnect
The solution contains two projects:

- BioConnectService
- BioClient

BioConnectService is a regular windows service which contains TCP/IP listener for local host at port 5555.
To install the service:

- build the solution 
- open the VS command prompt in admin mode and navigate to the bin folder of the project (debug or release) with
  BioConnectService.exe and run
     installutil.exe BioConnectService.exe -- to install the service
     installutil.exe /u BioConnectService.exe -- to uninstall the service

To test the service open several command prompts and run the BioClient.exe from the bin folder (debug/release):

The output should look like the following 
C:\Test\COPY>BioClient.exe
Sent: HELLO
Received: HI

 Press Enter to continue...
 

Sent: COUNT
Received: 8

 Press Enter to continue...
 
Sent: CONNECTIONS
Received: 9

 Press Enter to continue...
 

Sent: TERMINATE
Received: BYE

If running several clients simultanously the COUNT and CONNECTIONS will show the corresponding numbers.

Description of the solution.
TCPServer is the Server class. When "StartServer" method is called  this Server object tries to connect to a IP Address specified on a port configured. Then the server start listening for client socket requests. As soon as a request comes in from any client then a Client Socket Listening thread will be started. That thread is responsible for client communication.

