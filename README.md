# Office 365 Starter Project for Windows Store App #

[日本 (日本語)](https://github.com/OfficeDev/O365-Windows-Start/blob/master/loc/README-ja.md) (Japanese)


**Table of Contents**

- [Overview](#overview)
- [Change History](#changehistory)
- [Prerequisites and Configuration](#prerequisites)
- [Build](#build)
- [Project Files of Interest](#project)
- [Known Issues](#knownissues)
- [Troubleshooting](#troubleshooting)
- [Additional resources](#additional-resources)
- [Questions and comments](#questions-and-comments)
- [License](https://github.com/OfficeDev/Office-365-APIs-Starter-Project-for-Windows/blob/master/LICENSE.txt)

<a name="overview"></a>

## Overview ##

The Office 365 Starter Project sample uses the Office 365 API Tools client libraries to illustrate basic operations against the Files, Calendar and Contacts service endpoints in Office 365.
The sample also demonstrates how to authenticate against multiple Office 365 services in a single app experience, and retrieve user information from the Users and Groups service.
We'll be adding examples of how to use more APIs such as Email when we update this project, so make sure to check back.

Below are the operations that you can perform with this sample:

Calendar  
  - Get calendar events  
  - Create events  
  - Update events  
  - Delete events  

Contacts  
  - Get contacts  
  - Create contacts  
  - Update contacts  
  - Delete contacts  
  - Change contact photo  

My Files  
  - Get files and folders  
  - Create text files  
  - Delete files or folders  
  - Read text file contents (OneDrive)  
  - Update text file contents  
  - Download files  
  - Upload files  

Users and Groups  
  - Get display name  
  - Get job title  
  - Get profile picture  
  - Get user ID  
  - Check signed in/out state  
	
Mail  
  - Get mail (with paged results)  
  - Send mail  
  - Delete mail  

<a name="changehistory"></a>
## Change History ##
January 26, 2015:

- Added mail capabilities.


December 17, 2014:

- Simplified authentication flow and client creation in AuthenticationHelper.cs file.

- Added cache for the information from the discovery service so that the app doesn't query the service more than once.

- Added support for corporate intranets and company accounts. The `UseCorporateNetwork` property of the `AuthenticationContext` object is now set to true. The project also now includes declarations for the Enterprise Authentication, Private Networks, and Shared User Certificates capabilities. See [App capability declarations (Windows Runtime apps)](http://aka.ms/vaha2s) for more information.

<a name="prerequisites"></a>

## Prerequisites and Configuration ##

This sample requires the following:  

  - Windows 8.1.  
  - Visual Studio 2013 with Update 4.  
  - [Office 365 API Tools version 1.4.50428.2](http://aka.ms/k0534n).  
  - An [Office 365 developer site](http://aka.ms/ro9c62).  
  - To use the Files part of this project, OneDrive for Business must be setup on your tenant, which happens the first time you sign-on to OneDrive for Business via the web browser.

**Note:** This sample will work if you are using Visual Studio 2015 with Update 1. After you configure the sample, though, you'll need to edit this key/value pair in your App.xaml file: 

`<x:String x:Key="ida:ClientId">your client id</x:String>`.

The code in the sample looks for the `ClientID` key, so the key/value pair should look like this:

`<x:String x:Key="ida:ClientID">your client id</x:String>`.

###Configure the sample

Follow these steps to configure the sample.

   1. Open the O365-APIs-Start-Windows.sln file using Visual Studio 2013.
   2. Build the solution. The NuGet Package Restore feature will load the assemblies listed in the packages.config file. You should do this before adding connected services in the following steps so that you don't get older versions of some assemblies.
   3. Register and configure the app to consume Office 365 services (detailed below).


###Register app to consume Office 365 APIs

You can do this via the Office 365 API Tools for Visual Studio (which automates the registration process). Be sure to download and install the Office 365 API tools from the Visual Studio Gallery.

   1. In the Solution Explorer window, choose Office365Starter project -> Add -> Connected Service.
   2. A Services Manager dialog box will appear. Choose Office 365 and Register your app.
   3. On the sign-in dialog box, enter the username and password for your Office 365 tenant. We recommend that you use your Office 365 Developer Site. Often, this user name will follow the pattern <your-name>@<tenant-name>.onmicrosoft.com. If you do not have a developer site, you can get a free Developer Site as part of your MSDN Benefits or sign up for a free trial. Be aware that the user must be an Tenant Admin user—but for tenants created as part of an Office 365 Developer Site, this is likely to be the case already. Also developer accounts are usually limited to one sign-in.
   4. After you're signed in, you will see a list of all the services. Initially, no permissions will be selected, as the app is not registered to consume any services yet. 
   5. To register for the services used in this sample, choose the following permissions:  
   	- (Calendar) – Read and write to your calendars.  
	- (Contacts) - Read and write to your contacts. 
	- (My Files) – Read and write your files.
	- (Users and Groups) – Sign you in and read your profile.  
	- (Users and Groups) – Access your organization's directory.
	- (Mail) - Read and write to your mail.
	- (Mail) - Send mail as you.
  
   6. Click OK in the Services Manager dialog box.

**Note:** If you see any errors while installing packages during step 6, for example, *Unable to find "Microsoft.Azure.ActiveDirectory.GraphClient"*, make sure the local path where you placed the solution is not too long/deep. Moving the solution closer to the root of your drive resolves this issue. We'll also work on shortening the folder names in a future update.      

<a name="build"></a>
## Build ##

After you've loaded the solution in Visual Studio, press F5 to build and debug.
Run the solution and sign in with your organizational account to Office 365.

<a name="project"></a>
## Project Files of Interest ##

**Helper Classes**  
   - CalendarOperations.cs  
   - FileOperations.cs  
   - UserOperations.cs  
   - AuthenticationHelper.cs  
   - ContactOperations.cs  

**View Models**  
   - CalendarViewModel.cs  
   - EventViewModel.cs  
   - UserViewModel.cs  
   - ContactsViewModel.cs  
   - FilesViewModel.cs  
   - FileSystemItemViewModel.cs  
   - ContactItemViewModel.cs  

<a name="knownissues"></a>
## Known issues ##



- None at the moment, but do let us know if you find any. We're listening. 

<a name="troubleshooting"></a>
## Troubleshooting ##



- You receive an "insufficient privileges" exception when you connect to Office 365 as a normal user, i.e., someone that does not have elevated privileges and is not a global administrator. Make sure you have set the *Access your organization's directory* permission when you add the connected services.




- You receive errors during package installation, for example, *Unable to find "Microsoft.Azure.ActiveDirectory.GraphClient"*. Make sure the local path where you placed the solution is not too long/deep. Moving the solution closer to the root of your drive resolves this issue. We'll also work on shortening the folder names in a future update.  



- You may run into an authentication error after deploying and running if apps do not have the ability to access account information in the [Windows Privacy Settings](http://aka.ms/gqqx6p) menu. Set **Let my apps access my name, picture, and other account info** to **On**. This setting can be reset by a Windows Update. 

- You run the Windows App Certification Kit against the installed app, and the app fails the supported APIs test. This likely happened because the Visual Studio tools installed older versions of some assemblies. Check the entries for Microsoft.Azure.ActiveDirectory.GraphClient and the Microsoft.OData assemblies in your project's packages.config file. Make sure that the version numbers for those assemblies match the version numbers in [this repo's version of packages.config](https://github.com/OfficeDev/O365-Windows-Start/blob/master/Office365StarterProject/packages.config). When you rebuild and reinstall the solution with the updated assemblies, the app should pass the supported APIs test.

## Additional resources ##
* [Office 365 APIs platform overview](http://msdn.microsoft.com/office/office365/howto/platform-development-overview)
* [File REST API reference](https://msdn.microsoft.com/office/office365/api/files-rest-operations)
* [Outlook Calendar REST API reference](http://msdn.microsoft.com/office/office365/api/calendar-rest-operations)
* [Outlook Mail REST API reference](https://msdn.microsoft.com/office/office365/api/mail-rest-operations)
* [Microsoft Office 365 API Tools](https://visualstudiogallery.msdn.microsoft.com/a15b85e6-69a7-4fdf-adda-a38066bb5155)
* [Office Dev Center](http://dev.office.com/)
* [Office 365 APIs starter projects and code samples](http://msdn.microsoft.com/office/office365/howto/starter-projects-and-code-samples)
* [Connecting to Office 365 in Windows Store, Phone, and universal apps](https://github.com/OfficeDev/O365-Win-Connect)
* [Office 365 Code Snippets for Windows](https://github.com/OfficeDev/O365-Win-Snippets)
* [Office 365 Profile sample for Windows](https://github.com/OfficeDev/O365-Win-Profile)
* [Office 365 REST API Explorer for Sites](https://github.com/OfficeDev/Office-365-REST-API-Explorer)


## Questions and comments

We'd love to get your feedback on the O365 Windows Starter project. You can send your questions and suggestions to us in the [Issues](https://github.com/OfficeDev/O365-Windows-Start/issues) section of this repository.

Questions about Office 365 development in general should be posted to [Stack Overflow](http://stackoverflow.com/questions/tagged/Office365+API). Make sure that your questions or comments are tagged with [Office365] and [API].


## Copyright ##

Copyright (c) Microsoft. All rights reserved.



This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information, see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
