
# Oh My Posh Installation Guide for Windows

This guide provides step-by-step instructions for installing and configuring Oh My Posh on a Windows system.

## Prerequisites

- Windows 10/11
- PowerShell
- Administrative privileges

## Installation Steps

### 1. Install Windows Terminal
```powershell
winget install Microsoft.WindowsTerminal
```

### 2. Install Oh My Posh
```powershell
winget install JanDeDobbeleer.OhMyPosh
```

### 3. Install Nerd Font

- Visit [Nerd Fonts website](https://www.nerdfonts.com/)
- Download "CascadiaCode Nerd Font" (recommended)
- Extract the ZIP file
- Right-click on the font files and select "Install" or "Install for all users"

### 4. Configure Windows Terminal

- Open Windows Terminal
- Click dropdown (▼) → **Settings**
- Select **PowerShell** profile from left sidebar
- Under "Appearance":
  - Find "Font face"
  - Select "CaskaydiaCove NF" (or your installed Nerd Font)
- Save settings

### 5. Configure PowerShell Profile

- Open PowerShell profile in notepad:
  ```powershell
  notepad $PROFILE
  ```
- Add these lines to the profile:
  ```powershell
  $env:POSH_THEMES_PATH = "C:\Program Files (x86)\oh-my-posh\themes"
  oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\powerlevel10k_classic.omp.json" | Invoke-Expression
  ```

### 6. Final Steps

- Restart PowerShell/Windows Terminal
- View available themes:
  ```powershell
  Get-PoshThemes
  ```

## Customization

To change themes:

- Run `Get-PoshThemes` to see available themes
- Edit your PowerShell profile
- Update the theme path in the configuration line:
  ```powershell
  oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\THEME_NAME.omp.json" | Invoke-Expression
  ```
- Replace `THEME_NAME` with your chosen theme.

## This will look after installation
![alt text](image.png)



