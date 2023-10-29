<p align="center">
<img src="https://github.com/landonbmartin/DNS/assets/148168629/cd122fa4-6b8f-45bb-a340-a15d189cc1cd" height=20% width=20%/>
</p>

<h1 align = "center">Understanding & Building Intuition for DNS (Domain Name System)</h1>
DNS is the naming system that translates user-friendly domain names into numerical IP addresses, allowing computers to locate and communicate with each other on the internet. This lab demonstrates the use of DNS and how to configure it. When properly configured and installed, we'll perform a few exercises with the Domain Controller and Client Microsoft Azure Virtual Machines to understand DNS better. To see how DNS works, this lab follows up from the <a href = "https://github.com/landonbmartin/configure-ad">installation and configuration of Active Directory</a>.


<br />

<h2>Environments and Technologies Used</h2>
<ul>
  <li>Microsoft Azure (Virtual Machines/Compute)</li>
  <li>Active Directory Domain Services</li>
  <li>Microsoft Remote Desktop</li>
  <li>Command Prompt</li>
</ul>

<br />

<h2>Operating Systems Used</h2>
<ul>
  <li>Windows Server 2022</li>
  <li>Windows 10 Pro (22H2)</li>
</ul>

<br />

<h2>DNS Exercises</h2>

<h3>A-Record</h3>

<p>
  <ul>
    <li>The "A" in A-Record stands for <i>address</i> and this is the most fundamental type of DNS record: pointing to the name of the IP address of a given domain</li>
    <li>Connect and log in to your Domain Controller and Client Virtual Machines as admins (mydomain.com\jane_admin)</li>
    <li>In the Client VM, open the Command Prompt and attempt to ping "mainframe" by entering the command <b>ping mainframe</b>. The request will fail.</li>
    <br>
    <img width="700" alt="ping mainframe" src="https://github.com/landonbmartin/DNS/assets/148168629/ffccf601-4cd5-42b3-80d0-c0d2a3ee5dd3">
    </br>
    <li>The same result will also apply if we try <i>nslookup</i> the mainframe (command line <b>nslookup mainframe</b>) because we do not have a DNS record</li>
    <li>To create a DNS A-Record, go to the Domain Controller VM and open the <b>DNS Manager</b> in the Server Manager Board. Go to the domain you created within the <b>Forward Lookup Zones</b> tab (mydomain.com)</li>
    <li>Right click on the page and create a <b>New Host (A or AAAA)</b>. Name the host <b>mainframe</b> and the IP address should be the same IP as the Domain Controller so that ping can resolve (the IP address I will be using is 10.0.0.4). Once the information is entered, click <b>Add Host</b> and refresh the DNS server so that the record can be updated.</li>
    <br>
    <img width="700" alt="A-Record mainframe" src="https://github.com/landonbmartin/DNS/assets/148168629/54e81cfc-d270-4fcc-b582-4058c3dbdf27">
    </br>
    <li>Go back to the Client VM and attempt to ping "mainframe" again. The ping will receive a reply successfully</li>
    <br>
    <img width="700" alt="ping mainframe successful" src="https://github.com/landonbmartin/DNS/assets/148168629/4a7b4892-2a1e-4494-9358-a6024302142f">
    </br>
  </ul>
</p>

<br />

<h3>Local DNS Cache</h3>

<p>
  <ul>
    <li>This exercise will showcase a DNS cache by creating a local DNS</li>
    <li>In the Domain Controller VM, go to the <b>DNS Manager</b> and locate the mainframe host created and edit the IP address to 8.8.8.8</li>
    <br>
    <img width="700" alt="Change mainframe IP" src="https://github.com/landonbmartin/DNS/assets/148168629/c484af63-0493-4aa0-96bb-30677e3e236b">
    </br>
    <li>Go back to the Client VM and ping "mainframe" again. You will notice it pings the mainframe's old IP address and not 8.8.8.8. This is because the cache needs to be updated, or flushed</li>
    <br>
    <img width="700" alt="Ping 8 8 8 8" src="https://github.com/landonbmartin/DNS/assets/148168629/427fa4fc-10f7-47f5-823c-8b73c388b933">
    </br>
    <li>In the Client VM, run Command Prompt <i>as Administrator</i> and enter the command <b>ipconfig /flushdns</b>. This command is a very helpful command for flushing the DNS for testing pings in IT. The cache in the example image below is now empty</li>
    <br>
    <img width="700" alt="ipconfig flushdns" src="https://github.com/landonbmartin/DNS/assets/148168629/2a122bd6-29a0-4e50-90b5-5627dcf77bd6">
    </br>
    <li>Now attempt to ping "mainframe" again, and now the new record will appear as 8.8.8.8</li>
    <br>
    <img width="700" alt="Successful flushdns" src="https://github.com/landonbmartin/DNS/assets/148168629/96118281-4927-4ad4-9393-fd8827778d4d">
    </br>
  </ul>
</p>


