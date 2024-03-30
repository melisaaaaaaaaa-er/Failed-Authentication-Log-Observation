# Failed Authentication Log Observation

<h2>Purpose</h2>

- Create an attack VM to simulate an adversary to generate failed authentication logs on our honeynet VMs.
- Observe the authentication logs on the honeynet VMs.

#
<img src="https://raw.githubusercontent.com/melisaaaaaaaaa-er/Failed-Authentication-Log-Observation-Images/main/1.png"/>

Create a VM named “attack-vm” on Azure.

Give the VM a different resource group, location, and virtual network/vnet from those of windows-vm and linux-vm.

#
<img src="https://raw.githubusercontent.com/melisaaaaaaaaa-er/Failed-Authentication-Log-Observation-Images/main/2.png"/>

<img src="https://raw.githubusercontent.com/melisaaaaaaaaa-er/Failed-Authentication-Log-Observation-Images/main/3.png"/>

<img src="https://raw.githubusercontent.com/melisaaaaaaaaa-er/Failed-Authentication-Log-Observation-Images/main/4.png"/>

Login to attack-vm through RDP.

Once you’re in, attempt to RDP into windows-vm from within attack-vm using false credentials. This is to create failed authentication logs on windows-vm. Do this a few times.

#
<img src="https://raw.githubusercontent.com/melisaaaaaaaaa-er/Failed-Authentication-Log-Observation-Images/main/5.png"/>

<img src="https://raw.githubusercontent.com/melisaaaaaaaaa-er/Failed-Authentication-Log-Observation-Images/main/6.png"/>

Install SSMS on attack-vm and again attempt to log on with faulty credentials to the SQL server on windows-vm to generate failed authentication logs. Do this a few times.

#
<img src="https://raw.githubusercontent.com/melisaaaaaaaaa-er/Failed-Authentication-Log-Observation-Images/main/7.png"/>

Still on attack-vm, open PowerShell and attempt to SSH into linux-vm using false credentials.

#
<img src="https://raw.githubusercontent.com/melisaaaaaaaaa-er/Failed-Authentication-Log-Observation-Images/main/8.png"/>

<img src="https://raw.githubusercontent.com/melisaaaaaaaaa-er/Failed-Authentication-Log-Observation-Images/main/9.png"/>

<img src="https://raw.githubusercontent.com/melisaaaaaaaaa-er/Failed-Authentication-Log-Observation-Images/main/10.png"/>

RDP into windows-vm and open the Event Viewer.

Navigate to “Security” under “Windows Logs”. Here we can see the failed authentication logs generated previously (with the Event ID 4625) when trying to log into windows-vm.

#
<img src="https://raw.githubusercontent.com/melisaaaaaaaaa-er/Failed-Authentication-Log-Observation-Images/main/11.png"/>

<img src="https://raw.githubusercontent.com/melisaaaaaaaaa-er/Failed-Authentication-Log-Observation-Images/main/12.png"/>

If you chose to leave the VMs on from the previous labs, attempts will have been made to gain unauthorized access to the machines from the Internet, generating many logs that can be seen here.

#
<img src="https://raw.githubusercontent.com/melisaaaaaaaaa-er/Failed-Authentication-Log-Observation-Images/main/13.png"/>

<img src="https://raw.githubusercontent.com/melisaaaaaaaaa-er/Failed-Authentication-Log-Observation-Images/main/14.png"/>

Navigate to the “Application” pane to view the failed authentication logs for the SQL server (Event ID 18456).

#
<img src="https://raw.githubusercontent.com/melisaaaaaaaaa-er/Failed-Authentication-Log-Observation-Images/main/15.png"/>

SSH into the linux-vm through the Control Panel and nagivate to the /var/log directory. You will see the authentication logs file “auth.log”.

<img src="https://raw.githubusercontent.com/melisaaaaaaaaa-er/Failed-Authentication-Log-Observation-Images/main/16.png"/>

<img src="https://raw.githubusercontent.com/melisaaaaaaaaa-er/Failed-Authentication-Log-Observation-Images/main/17.png"/>

Use the command “cat auth.log | grep password” to filter for the machine authentication logs.

We can see both our own authentication attempts and those coming from the Internet.
