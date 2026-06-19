
## Verify you are using PowerShell 7 and not PowerShell 5


NerdFonts and OhMyPosh work only if you use PowerShell 7.

To verify it, run on your PowerShell

```powershell
$PSVersionTable.PSVersion
```

It should show you something like
![[Pasted image 20260618174556.png]]

If not, run

```powershell
winget install --id Microsoft.PowerShell --source winget
```


Note: always use "PowerShell" (v7), and not "Windows PowerShell" (v5)
![[Pasted image 20260618174656.png]]

## Choose a Nerd Font from the official website

1. Visit [https://www.nerdfonts.com/font-downloads](https://www.nerdfonts.com/font-downloads)
2. Download a font you like (e.g. **JetBrainsMono**, **FiraCode**, **CascadiaCode**)
3. Extract the `.zip` file
4. Right-click the `.ttf` files and choose **Install for all users**

### Install TerminalIcons for ls command

In a PowerShell 7, admin mode, run:

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned -Force
Install-Module PowerShellGet -Force -AllowPrerelease
Import-Module PowerShellGet -Force
Install-PSResource -Name Terminal-Icons -TrustRepository -Force
Import-Module Terminal-Icons
```

So that, when you run 
```powershell
ls
```

it will show icons like these:

![[Pasted image 20260619093715.png]]

## Ensure you have a PowerShell profile

Open a PowerShell 7, and type

```powershell
$PROFILE
```

It should show you a path to a `.ps1`, like

```
C:\Users\BelloneDavide\<PATH>\Documents\PowerShell\Microsoft.PowerShell_profile.ps1
```

## Add TerminalIcons to you PowerShell profile

Open the profile (eg, with notepad:)

```powershell
notepad $PROFILE
```

And import the TerminalIcons module

```powershell
Import-Module Terminal-Icons
```


## Install OhMyPosh

In PowerShell, run

```powershell
winget install JanDeDobbeleer.OhMyPosh --source winget
```

## Choose the Theme

From the [Themes page](https://ohmyposh.dev/docs/themes), choose one.

![[Pasted image 20260619095215.png]]

Each theme links to a JSON definition. 

![[Pasted image 20260619095230.png]]

Open it and store it into your computer:

![[Pasted image 20260619095242.png]]
## Add the theme in the PowerShell profile

Run the `oh-my-posh init` command in the `$PROFILE` file, adding the link to the json file on your computer.

```powershell
oh-my-posh init pwsh --config "C:\Users\BelloneDavide\themesemodipt-extend.omp.json" | Invoke-Expression
```

## Set PowerShell 7 with Nerd Fonts as main Terminal 

In the Settings of Windows Terminal, choose the PowerShell (with black icon). 
Under Appearance, open the Font Face list, and select the one downloaded from NerdFonts.

![[Pasted image 20260619095546.png]]

## Final Result
You will have the icons from NerdFonts, the GIT info 

![[Pasted image 20260619095733.png]]

## Sources

- [How to Install Nerd Fonts and Icons in PowerShell 7 on Windows 11](https://ardalis.com/install-nerd-fonts-terminal-icons-pwsh-7-win-11/)
- [NerdFonts](https://www.nerdfonts.com/font-downloads)
- [OhMyPoshTheme](https://ohmyposh.dev/docs/themes#the-unnamed)