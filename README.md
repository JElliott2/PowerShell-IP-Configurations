# PowerShell IP Configurations
 Using PowerShell to configure IP settings after IP conflicts
# **Windows IP Tools**
There are a variety of tools and methods to configure and manage IP settings. I will focus on PowerShell and some ways you can get different IP information from it. These will help to fix issues around IP conflict and other IP addressing issues.

The first command you will get accustomed to is `Get-NetIPAddress` The information gained will look like this. 


![PowerShell window showing how to find IP information.](screen1.png)

If you are interested in only your IPv4 address you can use *-AddressFamily* and state IPv4.

`Get-NetIPAddress -AddressFamily IPv4`

![](screen2.png)


Once you have learned the IP address and the name of the interface, you can set that interface with a new IP. To do so, use the *-InterfaceAlias* of the network adapter as below.

`Get-NetIPAddress -AdressFamily IPv4 -InterfaceAlias 'Ethernet 2'`

`New-NetIPAddress -InterfaceAlias 'Ethernet 2' -IPv4Address '**NEW IP**' -PrefixLength 24 (this is for the subnet mask) -DefaultGateway '**Enter your default gateway here**'`

These tools would allow you to fix issues with conflicting IPs and to manually set an IP address if DHCP is proving problematic. To verify that the new IP address has been set, re-enter the *Get-NetIPAddress* command in PowerShell. You could also use the cmd line to ping your own IP address at 127.0.0.1 or a standard DNS server like google (8.8.8.8) to verify TCP/IP is working correctly.

`ping 127.0.0.1`

`ping 8.8.8.8`

If problems persist and you cannot get the IP address settings working correctly, you may need to reset your IP settings. To do so within PowerShell, you can use the cmd line inputs: *ipconfig /release* which releases the currently assigned IP and *ipconfig /renew* which will assign a new IP using DHCP. Note that if you have a preferred IP it will be set to the preferred address.

You can also verify your current IP address using the settings in Windows.

![How to find the setting to verify IP](Animation.gif)
