# Local Folder Sync GDrive using UIPath

## Description

The project is composed of two flows:
- **Main** flow that handles the user interaction part
- **GoogleDriveSyncFlow** flow that handles the files and folders detection and overall file configuration.

### Main - the user interaction flow

The first flow - **Main** - handles the user interactions with the automatization. These interactions consists in asking the user for the time frequency of the file and folders sync and due to time management should ask the user to login with it's Google Account (but at the moment this feature is not available).

### GoogleDriveSyncFlow - the files and folder hadling flow

The second flow - **GoogleDriveSyncFlow** - is more complex due to the way Google Workspace and system file management are working, so because of that we will take each major step of the automatization independently and exaplain it.

After the user has logged with the Google Account through the UIPath Studio application the automatization will create a local folder at the `C:\LocalFolderSync` and a test file named `welcome.txt` inside the folder (the folder is created only if there is not yet another folder with this name already). 

The automatization continues with the creation of the folder (the folder has the same name) on the Google Drive. If the folder already exists we will take the id of that found folder instead of creating a new one, if there is no folder yet created, we create one.

These are the initial conditions that needs to be satisfied in order for the automation to continue. We then initialize a new list of files that will be later used as a verification method to see which files are deleted.

We iterate through each sub-folder of the main folder to create our folder structure in Google Drive. This step is important because we want to match the folder structure from local folder with the one on the remote. After each folder search we upload the files in that specific folder to the corresponding folder on remote.

Then we repeat the process of files uploading for the main folder only then, to make sure that the files that are not asociated to a folder are going to be uploaded too.

After uploading all the files and folders from the local to remote we then use the previous created list (its element represent the name of the files and folders uploaded to remote) to verify if any file or folder was deleted from local, but still exists on remote. If that is the case, we identify the specific file/folder by the id and delete it from remote too.

These proceses are going to repeat after X time inputed by the user in the user interaction part of the automatization.

## Improvements

The automatization is far from being perfect. The main key focus aspects that the automatization are error handling situation and a way of asking the user to login using their account.

## Team members

This is a project made for the Robotic Process Automation course of the West University of Timișoara and the members that participated in the development of the project are:
- Poenaru Iulian
- Raț Ioan-Paul
- Benteu Alexandru
