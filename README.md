<h1>Group Policy Object (GPO) implementations</h1>
<p>GPO stands for Group Policy Object. It includes rules, settings, and policies for an organization. Group Policies control what users can and cannot do on a computer. For example, a Group Policy can make sure passwords are complex enough and prevent access to certain folders. In this Project, I will be focusing on four concepts; Disabling or Preventing Shutdown Option for users in a certain OU, Disabling Command Line Interface (CMD) for users in another OU, Changing the default password policy and Automating software installation.  </p>
<h3>*Disabling or Preventing Shutdown Option for the users in Toronto OU</h3>
<p>We are going to following three steps to achieve this policy</p>
<p>* Create</p>
<p>* Apply</p>
<p>* Link to OU</p>
<p>1. To create this policy, go to server manager-dashboard >Tools> Group policy Management</p>
<p align="center"><img src="https://i.imgur.com/lWgeVSe.png" height="50%" width="50%" alt="image"/>

<p>2. On the Group Policy Management Console, expand Forest, expand domains, expand domain name, right-click on Group Policy Objects and click on New.</p>
<p align="center"><img src="https://i.imgur.com/omMBd8n.png" height="50%" width="50%" alt="image"/>

<p>3. On the New GPO screen, type in a descriptive name for the policy(no space) then click OK</p>
<p align="center"><img src="https://i.imgur.com/MqpBeX5.png" height="50%" width="50%" alt="image"/>

<p>4. Back on the Group Policy Management screen, expand Group Policy Objects, right-click on the new policy created and click on Edit </p>
<p align="center"><img src="https://i.imgur.com/lXuGE4W.png" height="50%" width="50%" alt="image"/>

<p>5. Go to this path to edit this policy; User Configuration >Policies > Administrative Templates > Start Menu and Taskbar > Remove and Prevent Access to the shutdown, sleep and restart command.</p>
<p align="center"><img src="https://i.imgur.com/ODoh6oJ.png" height="50%" width="50%" alt="image"/>

<p>6. Double click on the “Remove and Prevent Access to the shutdown, sleep and restart command”, click on Enabled, Apply and then OK</p>
<p align="center"><img src="https://i.imgur.com/HjqBZpJ.png" height="50%" width="50%" alt="image"/>

<p>7. To link this policy to an OU, back on the Group Policy Management screen, right-click on the OU and click on Link an existing GPO</p>
<p align="center"><img src="https://i.imgur.com/Ng0gue3.png" height="50%" width="50%" alt="image"/>

<p>8. On the Select GPO screen, click on the GPO you want to link and click OK</p>
<p align="center"><img src="https://i.imgur.com/y7xoDUu.png" height="50%" width="50%" alt="image"/>

<p>9. On the Group Policy Screen, expand or click on the OU and the GPO linked can be seen</p>
<p align="center"><img src="https://i.imgur.com/gpQ3YIX.png" height="50%" width="50%" alt="image"/>

<p>10. Logging in to one of the user account in Ottawa OU, you can see there is no options of shutting down or restart again</p>
<p align="center"><img src="https://i.imgur.com/Wa5iOFW.png" height="50%" width="50%" alt="image"/>

<br>
<br>

<h3>*Disabling Command Line Interface (CMD) for the users in Ottawa OU</h3>
<p>1. Still On the Group Policy Management Console, expand Forest, expand domains, expand domain name, right-click on Group Policy Objects and click on New.</p>
<p align="center"><img src="https://i.imgur.com/Q6ySMha.png" height="50%" width="50%" alt="image"/>

<p>2. On the New GPO screen, type in a descriptive name for the policy(no space) then click OK</p>
<p align="center"><img src="https://i.imgur.com/S6kQSTi.png" height="50%" width="50%" alt="image"/>

<p>3. Back on the Group Policy Management screen, expand Group Policy Objects, right-click on the new policy created and click on Edit </p>
<p align="center"><img src="https://i.imgur.com/NeEcZEJ.png" height="50%" width="50%" alt="image"/>

<p>4. To edit this policy, go to this path; User Configuration > Policies > Administrative Templates > System > Prevent access to the command prompt.</p>
<p align="center"><img src="https://i.imgur.com/wwUo9D7.png" height="50%" width="50%" alt="image"/>

<p>5. Double click on System and click on Prevent access to the command prompt from the list.</p>
<p align="center"><img src="https://i.imgur.com/TLQopUo.png" height="50%" width="50%" alt="image"/>

<p>6. On the “Prevent access to the command prompt” screen, click on Enabled, then Apply and OK</p>
<p align="center"><img src="https://i.imgur.com/QDb5sbZ.png" height="50%" width="50%" alt="image"/>

<p>7. To link this policy to an OU, back on the Group Policy Management screen, right-click on the OU and click on Link an existing GPO</p>
<p align="center"><img src="https://i.imgur.com/z0nAVam.png" height="50%" width="50%" alt="image"/>

<p>8. On the Select GPO screen, click on the GPO you want to link and click OK </p>
<p align="center"><img src="https://i.imgur.com/54Zmem5.png" height="50%" width="50%" alt="image"/>

<p>9. On the Group Policy Screen, expand or click on the OU and the GPO linked can be seen</p>
<p align="center"><img src="https://i.imgur.com/dpQxn9w.png" height="50%" width="50%" alt="image"/>

<p>10. Launching the Command Line Interface in one of the users in Ottawa OU, one can see the message that it has been disabled by the administrator</p>
<p align="center"><img src="https://i.imgur.com/Oda4CeE.png" height="50%" width="50%" alt="image"/>

<br>

<h3>*Changing the default password policy [for the whole organization]</h3>
<p>1. Still On the Group Policy Management Console, expand Forest, expand domains, expand domain name, right-click on Group Policy Objects and click on New.</p>
<p align="center"><img src="https://i.imgur.com/Q6ySMha.png" height="50%" width="50%" alt="image"/>

<p>2. On the New GPO screen, type in a descriptive name for the policy(no space) then click OK</p>
<p align="center"><img src="https://i.imgur.com/ooT3sWR.png" height="50%" width="50%" alt="image"/>

<p>3. Back on the Group Policy Management screen,  expand Group Policy Objects, right-click on the new policy created and click on Edit </p>
<p align="center"><img src="https://i.imgur.com/MbPHNhe.png" height="50%" width="50%" alt="image"/>

<p>4. Go to this Path; Computer Configuration > Policies > Windows Settings > Security settings > Account Policies > Password Policies and make the changes you require</p>
<p align="center"><img src="https://i.imgur.com/W9OgEkJ.png" height="50%" width="50%" alt="image"/>

<p>5. To Link this newly created policy, right-click on your domain (because it applies to the whole organization), click Link an existing GPO.</p>
<p align="center"><img src="https://i.imgur.com/cahkQiN.png" height="50%" width="50%" alt="image"/>

<p>6. From the Select GPO screen, click on the policy you want to link and click OK.</p>
<p align="center"><img src="https://i.imgur.com/YxMENep.png" height="50%" width="50%" alt="image"/>

<p>7. Back on the Group Policy Management screen, under the domain name, you can see the policy linked under it</p>
<p align="center"><img src="https://i.imgur.com/43VKvdF.png" height="50%" width="50%" alt="image"/>

<p>8. To confirm this policy is implemented, I logged in a domain account account and provided a password which didn’t follow the policy requirement</p>
<p align="center"><img src="https://i.imgur.com/cuDz3Sh.png" height="50%" width="50%" alt="image"/>

<br>

<h3>*Automating software installation</h3>
<p>1. To automate software Installation for all OU in the domain, first I needed to do was to download the Microsoft Software Installer(MSI) Package, so for Mozilla firefox, I went to “https://www.mozilla.org/en-CA/firefox/enterprise/” click on Download</p>
<p align="center"><img src="https://i.imgur.com/AgePtyy.png" height="50%" width="50%" alt="image"/>

<p>2. Next, I created a folder in the C drive of the server named ‘MSI package’. This folder needs to shared and to do this, right-click on the folder and go to properties.</p>
<p align="center"><img src="https://i.imgur.com/6hUsrUU.png" height="50%" width="50%" alt="image"/>

<p>3. On the properties’ page, go to the sharing tab and click on share</p>
<p align="center"><img src="https://i.imgur.com/9SlcFmg.png" height="50%" width="50%" alt="image"/>

<p>4. On the network access’ page, click on the dropdown, select everyone and click Add</p>
<p align="center"><img src="https://i.imgur.com/O3cqtE2.png" height="50%" width="50%" alt="image"/>

<p>5. Still on the network access page, make sure the permission level for “everyone” is Read/Write, then click Share</p>
<p align="center"><img src="https://i.imgur.com/6jtSdOA.png" height="50%" width="50%" alt="image"/>

<p>6. After that, you will get a message that your folder is shared, click Done</p>
<p align="center"><img src="https://i.imgur.com/I5VlcEA.png" height="50%" width="50%" alt="image"/>

<p>7. Back on the MSI Package properties, just click Close</p>
<p align="center"><img src="https://i.imgur.com/Ek3eNuR.png" height="50%" width="50%" alt="image"/>

<p>8. After sharing the folder, I then copied the MSI file from my local computer and paste it in the MSI Package folder created on the server machine</p>
<p align="center"><img src="https://i.imgur.com/Sm3FbZa.png" height="50%" width="50%" alt="image"/>

<p>9. I created a new group policy by right-clicking on the Group Policy Object in Group Policy Management and clicking on New. Gave it a descriptive name</p>
<p align="center"><img src="https://i.imgur.com/taa3D0X.png" height="50%" width="50%" alt="image"/>
<p align="center"><img src="https://i.imgur.com/c1K3b3C.png" height="50%" width="50%" alt="image"/>

<p>10. Now before we link this GPO we need to edit it first. To do this, right-click on the new GPO created and go to edit </p>
<p align="center"><img src="https://i.imgur.com/M4eS9Ce.png" height="50%" width="50%" alt="image"/>

<p>11. On the Group Policy Management Editor, go to this path Computer Configuration>Policies>Sofware Settings>Software Installation>New>Package</p>
<p align="center"><img src="https://i.imgur.com/bZ4HRNe.png" height="50%" width="50%" alt="image"/>

<p>12. Now in the file explorer input the location where the Msi package is saved:<b> \\ADDS-Server\MSI-Package</b>, then select the file in the folder and click Open</p>
<p align="center"><img src="https://i.imgur.com/VfEy7tV.png" height="50%" width="50%" alt="image"/>

<p>13. On the deploy software page, make sure assigned is selected, then click OK</p>
<p align="center"><img src="https://i.imgur.com/mFFYO8g.png" height="50%" width="50%" alt="image"/>

<p>14. Back on the Group Policy Management Editor, you can see the package you just deployed while the software installation tab is selected</p>
<p align="center"><img src="https://i.imgur.com/8nnqVrb.png" height="50%" width="50%" alt="image"/>

<p>15. To link this GPO to the whole organization, right click on the domain name and go to Link an existing GPO</p>
<p align="center"><img src="https://i.imgur.com/Nh7VzSs.png" height="50%" width="50%" alt="image"/>

<p>16. On the Select GPO page, select the intended GPO and click OK</p>
<p align="center"><img src="https://i.imgur.com/QjHKfgW.png" height="50%" width="50%" alt="image"/>

<p>17. Back on the Group Policy Management page, under the domain name's list of GPO, you can see the policy linked under it</p>
<p align="center"><img src="https://i.imgur.com/Ysm7cYp.png" height="50%" width="50%" alt="image"/>

<p>18. To confirm, I logged in to one of the client’s computer and the firefox deployed for the whole organization is there</p>
<p align="center"><img src="https://i.imgur.com/oAa6dtq.png" height="50%" width="50%" alt="image"/>

<br>




