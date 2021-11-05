# Network Analysis #

## Time Thieves ##

At least two users on the network have been wasting time on YouTube. Usually, IT wouldn't pay much mind to this behavior, but it seems these people have created their own web server on the corporate network. So far, Security knows the following about these time thieves:

    * They have set up an Active Directory network.
    * They are constantly watching videos on YouTube.
    * Their IP addresses are somewhere in the range 10.6.12.0/24.

You must inspect your traffic capture to answer the following questions:

1.	What is the domain name of the users' custom site?

    **frank-n-ted.com**

    ip.addr==10.6.12.1

    ![Photo7](Photos/7.png)

2. What is the IP address of the Domain Controller (DC) of the AD network?

        10.6.12.12 (Frank-n-Ted-DC.frank-n-ted.com)

        ip.addr == 10.6.12.0/24
![Photo8](Photos/8.png)

3. What is the name of the malware downloaded to the 10.6.12.203 machine? Once you have found the file, export it to your Kali machine's desktop.

Command: ip.addr == 10.6.12.203 && http.request.method == GET

Downloaded file name is **june11.dll**

![](Photos/9.png)

	Export file: File – Export Objects – HTTP…

4.	Upload the file to VirusTotal.com. What kind of malware is this classified as?

        It’s Trojan malware.
![](Photos/10.png)
![](Photos/11.png)

## Vulnerable Windows Machines ##

The Security team received reports of an infected Windows host on the network. They know the following:

    - Machines in the network live in the range 172.16.4.0/24.
    - The domain mind-hammer.net is associated with the infected computer.
    - The DC for this network lives at 172.16.4.4 and is named Mind-Hammer-DC.
    - The network has standard gateway and broadcast addresses.

Inspect your traffic to answer the following questions:

1.	Find the following information about the infected Windows machine:

    - Host name: Rotterdam -PC
    - IP address: 172.16.4.205
    - MAC address: 00:59:07:b0:63:a4

Command: ip.src == 172.16.4.4 && kerberos.CNameString

![](Photos/12.png)
![](Photos/13.png)

2.	What is the username of the Windows user whose computer is infected?

    Filter: ip.src == 172.16.4.205 && kerberos.CNameString

    Username is matthijs.devries

![](Photos/14.png)

3.	What are the IP addresses used in the actual infection traffic?

We filtered Conversational statistic, and then filtered this by highest number of packages between IPs.

    Statistic – Conversations – IPv4 (tab) – Packets (high to low)

    The IP addresses: 185.243.115.84 and 172.16.4.205. 
![](Photos/15.png)

4.	As a bonus, retrieve the desktop background of the Windows host.

We extracted the file using following path and sorted then for the size (from the highest to the lowest):

    Export file: File – Export Objects – HTTP…

File has Recycle Bin image and Start button (didn’t fit on my screen), which means it was a screenshot from a desktop.

    **empty.gif%3fss&ss2img**

![](Photos/16.png)

# Illegal Downloads #

IT was informed that some users are torrenting on the network. The Security team does not forbid the use of torrents for legitimate purposes, such as downloading operating systems. However, they have a strict policy against copyright infringement.
IT shared the following about the torrent activity:

    - The machines using torrents live in the range 10.0.0.0/24 and are clients of an AD domain.
    - The DC of this domain lives at 10.0.0.2 and is named DogOfTheYear-DC.
    - The DC is associated with the domain dogoftheyear.net.

Your task is to isolate torrent traffic and answer the following questions:

1.	Find the following information about the machine with IP address 10.0.0.201:

    * MAC address 00:16:17:18:66:c8
    * Windows username: elmer.blanko
    * OS version: Windows 10, BLANCO-DESKTOP

Filter: ip.src==10.0.0.201&& Kerberos.CNameString

![](Photos/17.png)
![](Photos/18.png)
![](Photos/19.png)

2.	Which torrent file did the user download?

The torrent file is Betty_Boop_Rythm_on_the_eservation.avi.torrent.

Filter: ip.addr==10.0.0.201 && http.request.method==GET 
And also write a String filter: torrent.

![](Photos/20.png)







