---
published: true
---

Anytime I do something I want to find a way to automate it. This past Christmas I got a new PC and went through the processes of setting up my apps and settings needed for development work. Below is a guide on how to do this quickly.

### Install Chocolatey
<https://chocolatey.org/install#individual>
_Chocolatey has the largest online registry of Windows packages. Chocolatey packages encapsulate everything required to manage a particular piece of software into one deployment artifact by wrapping installers, executables, zips, and/or scripts into a compiled package file._ - Chocolatey Website

I use Choco to install all my apps I need in a scripted way.

### Find Packages To Install
<https://chocolatey.org/packages>
For me this took some time to compile the list that I wanted but you can use the ones I have as a starting point and customize from there.

### Run Choco Install
-	NOTE: must run PowerShell as administrator
-	NOTE: must run 'Set-ExecutionPolicy Unrestricted' before executing this script

#### My Chco Install powershell script
```
chocolatey feature enable -n allowGlobalConfirmation

choco install visualstudio2019professional --package-parameters "--allWorkloads --includeRecommended --includeOptional --passive --locale en-US"
choco install resharper
choco install vscode

choco install nodejs-lts
choco install git
choco install github
choco install poshgit

choco install sql-server-express
choco install sql-server-management-studio
choco install sqlsearch
choco install oracle-sql-developer

choco install microsoft-teams
choco install postman
choco install prefix
choco install linqpad4
choco install cmder
choco install 7zip
choco install notepadplusplus
choco install SublimeText3
choco install googlechrome

choco install spotify
choco install obs-studio
```
