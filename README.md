<p align="center">
<img src="https://i.imgur.com/UXuRdG1.png" height="40%" width="60%" alt="Disk Sanitization Steps"/><br />
</p>

<h1>DNS: DNS Manager Experimentation on the Cloud (Azure)</h1>
This demonstration will help strengthen knowledge of concepts surrounding DNS servers.  In this demonstration, I'll be using two virtual machines, Client-1 & DC-1, which are two virtual machines created in previous projects on this GitHub.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- PowerShell
- DNS Manager

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
  
<h2>High-Level DNS Management Steps</h2>

- Logging into DC-1 & Client 1
- Alias Record Exercise
- Local DNS Cache Exercise
- CNAME Record Exercise


<h2>Group Policy & Account Management Steps</h2>

<p>
1) Begin by logging into both <strong>DC-1</strong> & <strong>Client-1</strong> as administrators.  Then, navigate to <strong>PowerShell in Client-1</strong>.<br />
  <br />
<img src="https://i.imgur.com/1vLWOF5.png" height="40%" width="60%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />

<p>
2) Type: <strong> "ping mainframe"</strong> in the command prompt. Notice how the ping was unsuccessful because we have not set up <strong>"mainframe"</strong> in the DNS Manager to route to an IP address. We will do this in the following steps and try again.<br />
  <br />
<img src="https://i.imgur.com/lGUCvfB.png" height="80%" width="100%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />
<br />

<p>
3) Next, type: <strong>ipconfig /displaydns > test.txt</strong>. Then type: <strong>notepad test.txt</strong>. <br />
  <br />
<img src="https://i.imgur.com/mIJloYR.png" height="80%" width="100%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />


<p>
4) If entered correctly, the following window (DNS Cache) should display. The <strong>DNS cache</strong> contains all recently resolved domain names and their corresponding IP addresses. If we search for <Strong>"mainframe"</Strong>, we will find that there is no DNS record in the cache to pull from.<br />
  <br />
<img src="https://i.imgur.com/fBbdD1N.png" height="80%" width="100%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />



<p>
5) The DNS cache is different from a computer's host file.  In this example, we will map an alias to an IP addres using the local <strong> host file</strong>. For example, try to ping "zebra", notice how the ping is unsuccessful.<br />
  <br />
<img src="https://i.imgur.com/Iuut4V8.png" height="80%" width="100%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />

<p>
6) To modify the <strong>host file</strong> navigate to: <strong>Open > Windows > System32 > drivers > etc > [open] hosts</strong>.<br />
  <br />
<img src="https://i.imgur.com/CbuyEBR.png" height="60%" width="80%" alt="Disk Sanitization Steps"/> <br />  
<img src="https://i.imgur.com/KUvtYxF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />

<p>
7) Enter a desired IP address and name it. For this example, we will map <strong>"zebra"</strong> to the loopback IP address <strong>127.0.0.1</strong>. <br />
  <br />
<img src="https://i.imgur.com/KfTAfCm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />

<p>
8) Now, when navigating back to PowerShell and pinging "zebra" the connection should be successful.<br />
  <br />
<img src="https://i.imgur.com/jDPfW8q.png" height="80%" width="100%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />
<br />



<p>
9) However, using the hosts file may serve a purpose occasionally; it's best to use a <strong>DNS server</strong> to store domain names and IP addresses.  Otherwise, we'd have to manually input the IP address into the host file every time it changes, a highly inefficient approach. In the next example, we will use DNS manager to map <strong>"mainframe"</strong>, an <strong>alias</strong>, to <strong>dc-1's</strong> private IP address. As you can see, in PowerShell <strong>"mainframe"</strong> still has not been mapped to an IP address, so we will add it to our <strong>DNS manager</strong>.<br />
  <br />
  <br />
<img src="https://i.imgur.com/H2fKLkj.png" height="80%" width="100%" alt="Disk Sanitization Steps"/> <br />
<img src="https://i.imgur.com/KzfFHW4.png" height="80%" width="100%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />


<p>
10) Begin by logging into <strong>dc-1</strong> and navigating to <strong>"DNS"</strong> and running it as an administrator. <br />
  <br />
<img src="https://i.imgur.com/njmnuwZ.png" height="80%" width="60%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />

<p>
11) Once in DNS Manager, navigate to <strong>dc-1 > Forward Lookup Zones > mydomain.com (created in previous tutorials on this github) > [Right Click] > [Select] New Host (A or AAAA)</strong>. <br />
  <br />
<img src="https://i.imgur.com/dv7bbZg.png" height="80%" width="100%" alt="Disk Sanitization Steps"/> <br />
 
</p>
<br />
<br />
<br />
<br />


<p>
12) Name the Host <strong>"mainframe"</strong> and map it to dc-1's local IP address (10.0.0.4 in this case).<br />
  <br />
<img src="https://i.imgur.com/efsWCSr.png" height="80%" width="100%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />

<p>
13) After <strong>"mainframe"</strong> is setup as a Host in <strong>DNS Manager</strong>, make sure the information in the panel is correct before moving on. <br />
  <br />
<img src="https://i.imgur.com/a0SX9DJ.png" height="80%" width="100%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />
<br />

<p>
14) Next, ping <strong>"mainframe"</strong>, the result should be something like this. Notice how <strong>mainframe is mapped to 10.0.0.4</strong>. <br />
  <br />
<img src="https://i.imgur.com/JdzsWYx.png" height="80%" width="100%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />



<p>
15) Now we are going to change the IP address mapped to "mainframe" in dc-1 in the DNS Manager panel. Select "mainframe" and change the IP address to 8.8.8.8.</strong><br />
  <br />
<img src="https://i.imgur.com/f2lVAMG.png" height="80%" width="100%" alt="Disk Sanitization Steps"/> <br />
<img src="https://i.imgur.com/6vxWO8i.png" height="80%" width="60%" alt="Disk Sanitization Steps"/><br />  
</p>
<br />
<br />
<br />
<br />

<p>
16) If you ping "mainframe" again, notice how the IP address listed is still mapping to 10.0.0.4.  The reason this is happening is because the IP address is saved in the DNS cache alongside other recent connections, we are going to clear the DNS cache so the IP address can be updated.<br />
  <br />
<img src="https://i.imgur.com/t4JiBjY.png" height="80%" width="100%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />
<br />

<p>
17) To see for ourselves, navigate again to PowerShell and type "ipconfig /displaydns > dns.txt" and "notepad dns.txt".
  <br />
<img src="https://i.imgur.com/D4ug1wB.png" height="80%" width="100%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />


<p>
18) Once the DNS cache is opened, we see here that "mainframe" is still associated with 10.0.0.4.  This configuration supercedes the DNS server's configuration, so until the cache is cleared the IP address will remain incorrectly mapped to 10.0.0.4.<br />
  <br />
<img src="https://i.imgur.com/fHrNwui.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />




<p>
19) If we navigate back to <strong>PowerShell</strong> in <strong>dc-1</strong>, and enter <strong>"ipconfig /flushdns"</strong> the DNS cache will clear and look to the DNS server for domain verification.<br />
  <br />
<img src="https://i.imgur.com/R2K1ZsR.png" height="80%" width="100%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />


<p>
20) To test this theory, ping <strong>"mainframe"</strong> yet again and witness the alteration in the IP address, which now should be returning <strong>8.8.8.8</strong>.<br />
  <br />
<img src="https://i.imgur.com/t9YFbDG.png" height="80%" width="100%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />

<p>
21) Now, we are going to setup a <strong>CNAME record</strong> in DNS Manager that points to www.google.com and observe the difference between this and the Alias we just completed. Navigate to <strong>dc-1 > Forward Lookup Zones > mydomain.com (created in previous tutorials on this github) > [Right Click] > [Select] New Alias(CNAME)</strong>.  <br />
  <br />
<img src="https://i.imgur.com/wjIgsuH.png" height="80%" width="100%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />

<p>
22) Create an Alias named <strong>"search"</strong> and for fully qualified domain name(FQDN) enter <strong>"www.google.com"</strong>.<br />
  <br />
<img src="https://i.imgur.com/rx2Wvj6.png" height="80%" width="60%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />

<p>
23) Now, navigate to PowerShell in dc-1, ping <strong>"search"</strong> and <strong>"www.google.com"</strong> should map to that request, also it will return google's public IP address. <br />
  <br />
<img src="https://i.imgur.com/XpckAdJ.png" height="80%" width="100%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />

<p>
24) Additionally, you can perform <strong>"/nslookup search"</strong> and <strong>"www.google.com"</strong> should return.<br />
  <br />
<img src="https://i.imgur.com/BNh666T.png" height="80%" width="100%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />


