# Group Policy Administration and Windows Endpoint Configuration

**Windows Server 2019 | Active Directory | Group Policy | Windows 10 | MSI Deployment**

## Project Overview

I designed, configured, scoped, and tested four Group Policy Objects (GPOs) in a Windows Active Directory lab. The policies controlled selected user-interface features, restricted access to Command Prompt, enforced a domain password policy, and deployed Mozilla Firefox to Windows client computers from a shared MSI package.

This project demonstrates how Group Policy can be used to apply consistent user and computer settings across an Active Directory environment while reducing the need to configure endpoints individually.

## Simulated Business Scenario

An organization needs a centralized method for applying security settings, user restrictions, and standard software across domain-joined computers. Configuring each workstation manually would be slow, inconsistent, and difficult to audit.

To address this, I created separate GPOs for each requirement, linked them to the appropriate domain or organizational-unit scope, updated policy on the client, and validated the resulting user or computer behavior.

## Project Objectives

- Create clearly named GPOs in the Group Policy Management Console (GPMC).
- Configure separate user and computer policies.
- Link each GPO to the correct Active Directory scope.
- Remove selected power commands from the Windows user interface.
- Restrict interactive access to Command Prompt for a designated user OU.
- Configure a domain-wide password policy.
- Deploy an MSI package to domain-joined computers through a secure network share.
- Validate policy application from a Windows client.
- Use `gpresult` and Group Policy Results to support troubleshooting.

## Lab Environment

| Component | Technology | Purpose |
| --- | --- | --- |
| Domain controller | Windows Server 2019 | Hosts AD DS, GPMC, and the lab domain |
| Client workstation | Windows 10 | Receives and validates user and computer policies |
| Policy management | Group Policy Management Console | Creates, configures, links, and reviews GPOs |
| Software package | Mozilla Firefox Enterprise MSI | Demonstrates centralized computer-based deployment |
| Distribution point | SMB network share | Provides domain computers with access to the MSI package |


## Skills Demonstrated

- Group Policy creation, configuration, and linking
- User Configuration and Computer Configuration policies
- Administrative Template configuration
- Domain password-policy administration
- MSI software assignment through Group Policy
- Policy confirmation with `gpresult` 
- Group Policy troubleshooting and documentation

## Implementation Summary

### 1. Removed Power Commands from the Windows Interface

I created a user-based GPO and enabled:

`User Configuration > Policies > Administrative Templates > Start Menu and Taskbar > Remove and prevent access to the Shut Down, Restart, Sleep, and Hibernate commands`

I linked the GPO to the designated user OU and validated that the affected user's Windows power menu no longer displayed those commands.

<p align="center">
  <img src="https://i.imgur.com/61iVckY.png" width="750" alt="Enabling the policy that removes Windows power commands">
</p>

<p align="center">
  <img src="https://i.imgur.com/Mkf6pny.png" width="750" alt="Windows power menu after the Group Policy setting was applied">
</p>



### 2. Restricted Interactive Command Prompt Access

I created a second user-based GPO and enabled:

`User Configuration > Policies > Administrative Templates > System > Prevent access to the command prompt`

After linking the policy to the intended user OU, I tested it from a client session and confirmed that Command Prompt displayed a restriction message.

<p align="center">
  <img src="https://i.imgur.com/nUnLMPY.png" width="750" alt="Enabling the policy that restricts Command Prompt access">
</p>

<p align="center">
  <img src="htt" width="750" alt="Command Prompt displaying an administrator restriction message">
</p>



### 3. Configured the Domain Password Policy

I configured password requirements under:

`Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy`


<p align="center">
  <img src="https://i.imgur.com/XriSH8o.png" width="750" alt="Configuring the Active Directory domain password policy">
</p>

<p align="center">
  <img src="https://i.imgur.com/Ka9arN8.png" width="750" alt="Windows rejecting a password that does not meet the domain policy">
</p>



### 4. Deployed Firefox with Group Policy

I downloaded the Firefox Enterprise MSI, placed it in a dedicated SMB distribution share, and assigned the package under:

`Computer Configuration > Policies > Software Settings > Software Installation`

<p align="center">
  <img src="https://i.imgur.com/L7hAlnj.png" width="750" alt="Selecting the Firefox MSI through its UNC network path">
</p>

<p align="center">
  <img src="https://i.imgur.com/vtvJ8tJ.png" width="750" alt="Firefox listed as an assigned Group Policy software package">
</p>

<p align="center">
  <img src="https://i.imgur.com/hguhxKb.png" width="750" alt="Firefox installed on the Windows client through Group Policy">
</p>


## Policy Validation

I validated the policies through visible client behavior and the following administrative checks:

```powershell
gpupdate /force
gpresult /r

```

- `gpupdate /force` requests an immediate user and computer policy refresh.
- `gpresult /r` displays a summary of the policies applied to the current user and computer.


For additional evidence, GPMC's **Group Policy Results Wizard** can show the winning GPO for each applied setting.

## Troubleshooting Reference

| Symptom | Likely cause | Verification or resolution |
| --- | --- | --- |
| A user policy does not apply | The user object is outside the linked OU, security filtering excludes the user, or another GPO has precedence | Generate a `gpresult /h` report and review the applied and denied GPOs |
| A computer policy does not apply | The GPO is linked to a user OU instead of the computer's OU | Verify the computer object's location and review the GPO link scope |
| The MSI package does not install | The computer cannot read the share, the package was selected by local path, or a restart has not occurred | Test the UNC path, review share and NTFS permissions, and restart the client |
| The expected password policy is not effective | The account policy is linked below the domain root or loses precedence | Review domain-root links and confirm the effective settings with `net accounts /domain` |
| Command Prompt remains available | The wrong user is being tested or the user policy has not refreshed | Run `gpupdate /force`, sign out, sign back in, and verify with `gpresult` |
| Group Policy processing reports errors | DNS, SYSVOL access, network connectivity, or replication is unavailable | Verify domain DNS, test access to `\\<domain-name>\SYSVOL`, and review the GroupPolicy Operational event log |

## Security and Administration Practices

- Use descriptive GPO names that identify the target and purpose. GPO names can contain spaces.
- Keep separate GPOs for logically separate settings to simplify testing and troubleshooting.
- Test new policies in a controlled OU before applying them broadly.
- Apply least privilege to GPO delegation, software shares, and package-management accounts.
- Give deployment targets read access to software packages, not write access.
- Use trusted, approved MSI packages and record their version and cryptographic hash.
- Review inheritance, link order, enforcement, security filtering, and WMI filters before troubleshooting.
- Back up GPOs and document changes before modifying production policy.
- Use Group Policy Results or `gpresult` to prove what was actually applied instead of relying only on the GPO link.

## Key Takeaways

This project reinforced that creating a GPO is only one part of Group Policy administration. A policy must be configured in the correct user or computer section, linked to the appropriate scope, processed by the intended client, and validated through Resultant Set of Policy data or observable behavior.

It also demonstrated the importance of secure scoping and distribution. Broad domain links and writable software shares may work in a lab, but production deployments should begin with a test OU, use least-privilege permissions, and expand only after successful validation.

<details>
<summary><strong>View the Power-Command Policy Walkthrough</strong></summary>

1. Open **Server Manager > Tools > Group Policy Management**.

   <p align="center"><img src="https://i.imgur.com/Rjkflqv.png" width="750" alt="Opening Group Policy Management from Server Manager"></p>

2. Expand the forest and domain, right-click **Group Policy Objects**, and select **New**.

   <p align="center"><img src="https://i.imgur.com/g5CWiWe.png" width="750" alt="Creating a new Group Policy Object"></p>

3. Give the GPO a clear, descriptive name. Spaces are allowed.

   <p align="center"><img src="https://i.imgur.com/mspuDv0.png" width="750" alt="Naming a new Group Policy Object"></p>

4. Right-click the new GPO and select **Edit**.

   <p align="center"><img src="https://i.imgur.com/QhEBU9j.png" width="750" alt="Editing a new Group Policy Object"></p>

5. Navigate to **User Configuration > Policies > Administrative Templates > Start Menu and Taskbar** and open the power-command policy.

   <p align="center"><img src="https://i.imgur.com/O2MWyMX.png" width="750" alt="Locating the Windows power-command policy setting"></p>

6. Select **Enabled**, apply the setting, and close the editor.

   <p align="center"><img src="https://i.imgur.com/borBqRq.png" width="750" alt="Enabling the power-command restriction policy"></p>

7. Right-click the intended user OU and select **Link an Existing GPO**.

   <p align="center"><img src="https://i.imgur.com/jMn0uyk.png" width="750" alt="Linking a Group Policy Object to a user OU"></p>

8. Select the new GPO and confirm the link.

   <p align="center"><img src="https://i.imgur.com/ylkgEYE.png" width="750" alt="Selecting the power-command GPO to link"></p>

9. Verify the GPO link beneath the intended OU.

   <p align="center"><img src="https://i.imgur.com/xu6BU98.png" width="750" alt="Verifying the linked Group Policy Object"></p>

10. Sign in as a user in the targeted OU and validate the Windows power menu.

    <p align="center"><img src="https://i.imgur.com/5RrtUgJ.png" width="750" alt="Validating the restricted Windows power menu"></p>

</details>

<details>
<summary><strong>View the Command Prompt Policy Walkthrough</strong></summary>

1. Create a separate GPO and open it in Group Policy Management Editor.

   <p align="center"><img src="https://i.imgur.com/jMn0uyk.png" width="750" alt="Opening the Command Prompt restriction GPO for editing"></p>

2. Navigate to **User Configuration > Policies > Administrative Templates > System**.

   <p align="center"><img src="https://i.imgur.com/x5E7UFz.png" width="750" alt="Opening System Administrative Templates"></p>

3. Open **Prevent access to the command prompt**.

   <p align="center"><img src="https://i.imgur.com/6i0C8z7.png" width="750" alt="Selecting the Command Prompt restriction policy"></p>

4. Select **Enabled**, review the script-processing option, and apply the setting.

   <p align="center"><img src="https://i.imgur.com/sEJREEh.png" width="750" alt="Enabling the Command Prompt restriction"></p>

5. Link the GPO to the intended user OU.

   <p align="center"><img src="https://i.imgur.com/JF9ZADB.png" width="750" alt="Linking the Command Prompt policy to a user OU"></p>

6. Confirm that the GPO appears beneath the targeted OU.

   <p align="center"><img src="https://i.imgur.com/ALvG4nd.png" width="750" alt="Verifying the Command Prompt GPO link"></p>

7. Sign in as an affected user and launch Command Prompt to validate the restriction.

   <p align="center"><img src="https://i.imgur.com/QyIJcpq.png" width="750" alt="Validating restricted Command Prompt access"></p>

</details>

<details>
<summary><strong>View the Domain Password Policy Walkthrough</strong></summary>

1. Create and edit a GPO intended for the domain account policy.

   <p align="center"><img src="https://i.imgur.com/ooT3sWR.png" width="750" alt="Naming the domain password policy GPO"></p>

2. Navigate to **Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy** and configure the required settings.

   <p align="center"><img src="https://i.imgur.com/W9OgEkJ.png" width="750" alt="Configuring domain password requirements"></p>

3. Link the GPO at the domain root so it can define the domain account policy.

   <p align="center"><img src="https://i.imgur.com/cahkQiN.png" width="750" alt="Linking the password policy at the domain root"></p>

4. Select the password-policy GPO and confirm the link.

   <p align="center"><img src="https://i.imgur.com/YxMENep.png" width="750" alt="Selecting the password-policy GPO"></p>

5. Verify that the policy appears beneath the domain.

   <p align="center"><img src="https://i.imgur.com/43VKvdF.png" width="750" alt="Verifying the domain-level password-policy link"></p>

6. Test the policy by attempting to set a noncompliant password and confirm that Windows rejects it.

   <p align="center"><img src="https://i.imgur.com/cuDz3Sh.png" width="750" alt="Validating enforcement of the domain password policy"></p>

</details>

<details>
<summary><strong>View the Firefox MSI Deployment Walkthrough</strong></summary>

1. Download the Firefox Enterprise MSI from Mozilla's enterprise download page.

   <p align="center"><img src="https://i.imgur.com/AgePtyy.png" width="750" alt="Downloading the Firefox Enterprise MSI package"></p>

2. Create a dedicated package folder on the server and share it as a software distribution point.

   <p align="center"><img src="https://i.imgur.com/6hUsrUU.png" width="750" alt="Creating the MSI package distribution folder"></p>

3. Configure share and NTFS permissions so deployment administrators can manage packages and target computer accounts have read access.

4. Copy the approved MSI file into the distribution folder.

   <p align="center"><img src="https://i.imgur.com/Sm3FbZa.png" width="750" alt="Copying the Firefox MSI into the software distribution folder"></p>

5. Create a dedicated computer-based software-deployment GPO.

   <p align="center"><img src="https://i.imgur.com/taa3D0X.png" width="750" alt="Creating a software-deployment Group Policy Object"></p>

   <p align="center"><img src="https://i.imgur.com/c1K3b3C.png" width="750" alt="Naming the Firefox deployment GPO"></p>

6. Edit the new GPO.

   <p align="center"><img src="https://i.imgur.com/M4eS9Ce.png" width="750" alt="Opening the Firefox deployment GPO for editing"></p>

7. Navigate to **Computer Configuration > Policies > Software Settings > Software Installation**, then select **New > Package**.

   <p align="center"><img src="https://i.imgur.com/bZ4HRNe.png" width="750" alt="Creating a new Group Policy software package"></p>

8. Enter the complete UNC path to the MSI package and open the file.

   <p align="center"><img src="https://i.imgur.com/VfEy7tV.png" width="750" alt="Opening the MSI package through its UNC path"></p>

9. Select **Assigned** as the deployment method.

   <p align="center"><img src="https://i.imgur.com/mFFYO8g.png" width="750" alt="Assigning the MSI package to computers"></p>

10. Confirm that the package appears in the Software Installation policy.

    <p align="center"><img src="https://i.imgur.com/8nnqVrb.png" width="750" alt="Verifying the assigned Firefox MSI package"></p>

11. Link the GPO to the intended computer scope. A test computer OU is recommended before broad deployment.

    <p align="center"><img src="https://i.imgur.com/Nh7VzSs.png" width="750" alt="Linking the Firefox deployment GPO"></p>

12. Select the deployment GPO and confirm the link.

    <p align="center"><img src="https://i.imgur.com/QjHKfgW.png" width="750" alt="Selecting the Firefox deployment GPO"></p>

13. Verify the link in GPMC.

    <p align="center"><img src="https://i.imgur.com/Ysm7cYp.png" width="750" alt="Verifying the linked software-deployment policy"></p>

14. Restart the targeted client and confirm that Firefox is installed.

    <p align="center"><img src="https://i.imgur.com/oAa6dtq.png" width="750" alt="Validating the Firefox installation on the Windows client"></p>


</details>


## Related Projects

- [Active Directory Domain Services Deployment and Windows Client Integration](https://github.com/AdeniyiAdesakin/Install-Active-Directory-Domain-Services-and-Join-Client-s-Computer-to-Active-Directory)
- [Active Directory Identity Administration](https://github.com/AdeniyiAdesakin/Active-Directory-Implementation)
- [Bulk Active Directory User Provisioning with PowerShell](https://github.com/AdeniyiAdesakin/Import-bulk-Users-from-a-CSV-Spreadsheet-with-PowerShell-)
