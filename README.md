# Short description of the solution
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

After installing the service run from the command prompt "services.msc" and find the service named "BioConnect Test Service (Valeriy Pogosyan)". Right click then select Start.

To test the service open several command prompts as clients and run in every one the BioClient.exe from the bin folder (debug/release):

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

The multhithreaded approach used in the solution allows to use TCP/IP sockets inside of the windows service - other approaches are prone to block the windows service preventing it's normal installation and usage.

Event log records the events like start and stop. To open events log press CTRL+ALT+S from within of the VS and navigate to BioLog folder. BioSource folder will have event log enties.


What else to do:

- Create a standalone setup program that others can use to install your Windows service
- To use ServiceController class to build another application to control the service programmatically
- Try different packages like TopShelf to compare solutions and performances.

