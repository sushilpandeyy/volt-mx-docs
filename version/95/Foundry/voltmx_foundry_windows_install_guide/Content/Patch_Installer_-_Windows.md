                         

You are here: Installing Hotfix Archives for Volt MX Foundry - Windows

Installing Hotfix Archives for Volt MX Foundry - Windows
=======================================================


The Volt MX Foundry Patch Installer can be used to apply patches (software updates) to Volt MX Foundry components for a specific GA release.

<b>For example:</b>

To apply a `9.2.1.x` patch to a version earlier than `9.2.1 GA`, you need to upgrade to  9.2.1 GA  by using the installer, and then apply the `9.2.1.x` patch.

The Patch Installer uses hotfix archives and applies the software updates to an existing Volt MX Foundry Installation. A hotfix archive (which is a `.zip` file) can have artifacts for one or more components. While installing hotfix archives, all components in the archive are installed to your existing Volt MX Foundry installation.

### Prerequisites

* Ensure that you have a previous version of Volt MX Foundry GA installed on your system at an accessible network location.

> **_IMPORTANT:_** If you are required to install hotfix archives to a set of components for a specific release, you must have the supported Volt MX Foundry GA version (for example, Volt MX Foundry 9.2.1) with required components installed on your system.<br>
<b>For example</b>, if you are required to install hotfix archive for Console version V 9.2.1, you must have Foundry 9.2.1 GA with Console installed on your system.</br>


* Ensure that  `Volt MX Foundry PatchInstaller.exe`  file has execute permission


<b>To download Volt MX Foundry Patch Installer and hotfixes, follow these steps:</b>

1. You can obtain a user name and password from your sales
   representative or partner.

2. Navigate to the Volt MX Foundry section.

3. From the Volt MX Foundry Patch Installer, select the specific 
   release from the Version drop-down list and then click on the specific release related files you want to download based on your platform (Windows or Linux).For example, if you want to download `Volt MX Foundry Patch Installer 9.0 GA`, select the `9.0 GA `version from the drop-down list, and then click the Installer_Windows link.

4. For the required hotfix components, select the specific release 
   from the Version drop-down list and then click Download. The following is a sample screen.

<b>To install Volt MX Foundry patch using the installer, follow these steps:</b>

1. Unzip the `Volt MX Foundry-9.x.x.GA.zip` file, and navigate to
   the Volt MX <b>Foundry_Patch_Installer_Windowsfolder</b>.

2. Double-click `Volt MX Foundry PatchInstaller-9.x.x.GA.exe` to
   launch the installer.<br>
   The <b>InstallAnywhere</b> dialog appears and displays the progress of the launching the installer.


      ![](Resources/Images/voltmx_Foundry_Patch_Installer.png)  


      A dialog with the Volt MX Foundry logo appears.


      ![](Resources/Images/voltmx-logo.png)  



<ol start="3">
  <li>Next, the <b>Introduction</b> window appears asking for following
   details: Enter the details to proceed with the upgrade:</li>
</ol>

   *    Please provide the location of the patch file: Provide the
        patch file location of the Volt MX Foundry component that you wish to install to current version. For example, middleware.zip.
        For information about creating a patch file, refer to [Creating a patch file for Foundry components](#creating-a-patch-file-for-foundry-components).
   *    Please provide the location of existing installation . The
        default install location appears in this field.
        Provide the location of existing olt MX Foundry installation that you wish to upgrade with the selected patch version.


   ![](Resources/Images/voltmx_introduction.png)  



<ol start="4">
  <li>Click <b>Next</b>. <b>The Pre-Installation Summary</b> window appears.</li>
</ol>


   ![](Resources/Images/voltmx_preinstalled_summary.png) 


   The installer takes backup of the current install folder. The backup folder will have a suffix of `_{Patch_File_Name}`. For example, if the hotfix name is KPNS.XXX, then the suffix of the backup folder will be `_KPNS.XXX`.

   > **_IMPORTANT:_** The Installer does not support automatic backups of database and other artifacts. The Installer does not support rollback in case of a failure during the upgrade.<br>
   -  You must take backup of your database and other artifacts
      before upgrading.<br>
   -  After the upgrade, republish your Volt MX Foundry
      applications.</br>

<ol start="5">
  <li>Click <b>Install</b>. The <b>Installing Volt MX Foundry</b> window appears and the <b>installation starts</b>.</li>
</ol>

   Once the installation completes, the Installation window appears with the confirmation message.


![](Resources/Images/voltmx_introduction1.png) 


   The installation of Volt MX Foundry is finished. In case of any errors during the installation, refer to the installation log for details. Installation log is located at below location: For example, `C:\VoltMXFoundry900\`

<ol start="6">
<li>Click <b>Done</b> to complete the installation. After the installation
   is completed, the installer creates logs in the install folder.</li>
</ol>

   For troubleshooting tips to resolve problems that you may encounter during installation, refer to the following:

   [FAQs and Troubleshooting](https://opensource.hcltechsw.com/volt-mx-docs/95/docs/documentation/Foundry/voltmx_foundry_windows_install_guide/Content/Troubleshooting.html)


   The <b> < Install Location > </b> directory contains the log files logging each invocation of the installer. To make problem identification easier, provide these log files to Volt MX when reporting an issue.

## Creating a patch file for Foundry components

To create a patch file for Foundry components, you need to create a zip file with the relevant files. The contents for the zip must be downloaded from the link to the build artifacts.

  