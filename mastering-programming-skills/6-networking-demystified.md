# Networking
- Networking is the term used for everything that involves machines communicating with each other
    - The devices may be physically close or distant
- Since everything in linux is a file, connecting to a different machine is also done via file descripters.

## Pieces of a Network:

- Major Pieces: User Computer and Servers(Big Computers)
- To connect these two, we have other pieces in between them: routers, Domain Name Server etc

## Packet Tranfer Route

- Suppose A sends a message to B, this message travels the following path:

- A's computer -> CAT cable -> CPE box at A's home -> optical fibre-> multiplexer near A's house ->optical fibre-> A's ISP's data centre -> connection-> B's ISP data centre-> multiplexer near B's house-> B's home router - > B's computer through WiFi.



### ping command

- This command helps to send a packet to any server
    - If we are unable to send that means the server is private
- `ping www.google.com` shows response sent by Google as we ping it.
- We can observe that the response mentions an IP Address i.e Google's IP Address
- The mapping of Domain name and IP Adress is somehow done by the ping command

## Understanding IP and MAC Addresses

- `ifconfig` command shows us information related to these addresses
- Each machine has a physical card called NIC Card
    - Each NIC card has a unique id
    - This unique ID is the MAC Address of the machine
- IP Address is not tied to a machine but rather the network, it is provided by the ISP
    - Each router has a pool of IP Addresses and all devices connected to it are given one of these
    - The IP Address might change each time we connect to the network but we can set it to remain static for a particular MAC Address

### Public and Private IP Address

- Public IP Addresses can be accessed by everyone and are unique globally.
- Private IP Addresses cannot be accessed by everyone.
    - They are unique only within a router pool.
