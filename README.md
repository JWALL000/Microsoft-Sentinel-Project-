## Project Overview 
Welcome to my project. In this project I successfully configured a honeypot and exposed it to the internet to capture the attention of attackers - I also used microsoft
sentinel as a SIEM and the azure log analytics tool to capture event logs from my windows VM and finally I created an attack map to map out the geolocation of the attackers IP 
addresses to I could gain insight to where the attacks were coming from. In the steps below I will explain how I did this. Thanks for reading! 

![Microsoft Sentinel Project1](https://github.com/JWALL000/Microsoft-Sentinel-Project-/blob/main/Sentinel%20Project%20for%20GitHub/Step%201%20-%20Welcome%20to%20my%20project%20-%20setting%20up%20sentinel.PNG)

## Steps 

# Step 1
I started this project by adding a virtual network, following the instructions and setting the desired resource group. 
![Microsoft Sentinel Project2](https://github.com/JWALL000/Microsoft-Sentinel-Project-/blob/main/Sentinel%20Project%20for%20GitHub/Step%202%20-%20Creating%20a%20Virtual%20Network.PNG)


# Step 2 
I then started to set up my virtual machine - this would be the honeypot that we exposed to the internet to gain the interest of attackers. 
![Microsoft Sentinel Project3](https://github.com/JWALL000/Microsoft-Sentinel-Project-/blob/main/Sentinel%20Project%20for%20GitHub/Step%203%20-%20Setting%20up%20a%20VM.PNG)
![Microsoft Sentinel Project4](https://github.com/JWALL000/Microsoft-Sentinel-Project-/blob/main/Sentinel%20Project%20for%20GitHub/Step%204%20-%20VM%20up%20and%20running.PNG)


# Step 3 
It was now time to change some firewall settings. As you will notice - Microsfot Windows 11 comes standard with basic firewall rules for porjection against unwanted inbound 
traffic. In this step I disable the firewall rules to allow attackers to ping and try to gain access to the machine. 
![Microsoft Sentinel Project5](https://github.com/JWALL000/Microsoft-Sentinel-Project-/blob/main/Sentinel%20Project%20for%20GitHub/Step5%20-%20Connecting%20via%20remote%20desktop.PNG)
![Microsoft Sentinel Project6](https://github.com/JWALL000/Microsoft-Sentinel-Project-/blob/main/Sentinel%20Project%20for%20GitHub/Step%206%20-%20Turning%20off%20firewall%20rules.PNG)

# Step 4 
I then tested to see if I could ping the virtual machine from my host pc. As you can see below we could successfully ping the VM. 
![Microsoft Sentinel Project6](https://github.com/JWALL000/Microsoft-Sentinel-Project-/blob/main/Sentinel%20Project%20for%20GitHub/Step%207%20-%20Pinging%20VM.PNG)


# Step 5 
After the VM had been exposed to the internet for a short amount of time - It was time to see if any logon attempts had been made on our machine. I used Windows Event Viewer 
to do this and as you can see we have new logons at 4:46:43 PM with the event ID of 4625.
![Microsoft Sentinel Project7](https://github.com/JWALL000/Microsoft-Sentinel-Project-/blob/main/Sentinel%20Project%20for%20GitHub/Step%208%20-%20Windows%20Event%20logs.PNG)

# Step 6 
In this next step - we get Log.AnalyticsOMS configuured and set up. This would allow us to view out Windows event logs in our instance of Microspft Sentinel. 
![Microsoft Sentinel Project8](https://github.com/JWALL000/Microsoft-Sentinel-Project-/blob/main/Sentinel%20Project%20for%20GitHub/Step%2010%20-%20Setting%20up%20log%20repository.PNG)

# Step 7 
Next I installed Windows secutity events as a data collector in sentinel. Allow us to view security events in Sentinel from our VM.
![Microsoft Sentinel Project9](https://github.com/JWALL000/Microsoft-Sentinel-Project-/blob/main/Sentinel%20Project%20for%20GitHub/Step%2011%20-%20Installing%20Windows%20Security%20Events%20into%20Sentinel.PNG)


# Step 9 
I then had the task of configuring data collection rules. If this step was missed or if a mistake was made then our data collectors would not work in Sentinel. 
![Microsoft Sentinel Project10](https://github.com/JWALL000/Microsoft-Sentinel-Project-/blob/main/Sentinel%20Project%20for%20GitHub/Step%2012%20-%20Creating%20data%20connection%20rule.PNG)

# Step 10 
Now it was time to wait. After about half an hour later we started to see our logs in our Log analytic workspace - so our VM was connected successfully to Azure environment. 
I also used this time to search thorugh our logs usings KQL. This made finding security events much easier. 
![Microsoft Sentinel Project11](https://github.com/JWALL000/Microsoft-Sentinel-Project-/blob/main/Sentinel%20Project%20for%20GitHub/Step%2013%20-%20Using%20KQL%20to%20search%20through%20security%20events.PNG)


# Step 11 
In this step I set up a watchlist of potentially malicious locations. I did this using a geo location map which I uploaded to Azure. The map contained well known malicious IP 
addresses from around the World. 
![Microsoft Sentinel Project12](https://github.com/JWALL000/Microsoft-Sentinel-Project-/blob/main/Sentinel%20Project%20for%20GitHub/Step%2014%20-%20Setting%20up%20watchlist%20with%20Geolocation.PNG)

# Step 12 
Next it was time to set up an attack map - this would show us on a map of globe where our security events were coming from. I had updated this map to refresh after every 5 minutes 
to get it as close to real time as possible. I started this step by opening a new workbook in sentinel. 
![Microsoft Sentinel Project13](https://github.com/JWALL000/Microsoft-Sentinel-Project-/blob/main/Sentinel%20Project%20for%20GitHub/Step%2015%20-%20Using%20the%20two%20file%20templates%20to%20poplulate%20the%20Geolocations%20in%20our%20watchlist.PNG)

# Step 13 
Now it was time to upload some .json code into the workbook. This code would build out our attack map and included all known IPs of every region - this makes it possible to 
indenitfy what countries and regions the attackers are from. 

![Microsoft Sentinel Project15](https://github.com/JWALL000/Microsoft-Sentinel-Project-/blob/main/Sentinel%20Project%20for%20GitHub/Step%2017%20-%20New%20workbook%20edited.PNG)

# Step 14 
After that it was time to wait and see how well our map would work. After some time I started seeing IP addresses orginate from Romania trying to sign in to our PC. This was the first time 
seeing the map work and I was very impressed. 
![Microsoft Sentinel Project16](https://github.com/JWALL000/Microsoft-Sentinel-Project-/blob/main/Sentinel%20Project%20for%20GitHub/Step%2019%20-%20Created%20attack%20map.PNG)

I then played around with the settings in our attack map and could configure settings to our personal prefences. 
![Microsoft Sentinel Project17](https://github.com/JWALL000/Microsoft-Sentinel-Project-/blob/main/Sentinel%20Project%20for%20GitHub/Step%2020%20-%20Looking%20at%20settings%20in%20attack%20map.PNG)


## Conclusion
I highly enjoyed this lab as it gave me great insight into how fast threat actors work in real life when they try to exploit a potential vulneratbility. And using sentinel 
as our SIEM gave me some valuable experience with Sentinel and how the Azure environment works at a basic level and lastly, I enjoyed  using the attack map to see where 
our attackers IPs were orginating from. 

Thanks for viewing my project - Hopefully this was as interesting to you as it was to me. 

Joseph Wall 



