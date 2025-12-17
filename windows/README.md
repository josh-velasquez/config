# Windows Terminal Setup



## PowerShell (Version > 7)
* PowerShell > 7
* Oh My Posh theme
* PSReadLine autocomplete & predictions

### Step 1
Install Oh-My-Posh


### Step 2
Edit Windows Terminal profile JSON:
```
{
    "guid": "{c1e2f3a4-5678-4b9c-8d2e-123456789abc}",
    "name": "PowerShell 7",
    "commandline": "pwsh.exe",
    "startingDirectory": "%USERPROFILE%\\Desktop\\github",
    "font": { "face": "Cascadia Code" },
    "colorScheme": "Frost",
    "useAcrylic": true,
    "opacity": 70,
    "cursorColor": "#000000"
}
```

### Step 3
Create PowerShell profile (Run in the terminal)

```
New-Item -Path $PROFILE -ItemType File -Force
notepad $PROFILE
```

### Step 4
Paste profile template
```

# --- PSReadLine Setup ---
Import-Module PSReadLine -RequiredVersion 2.3.6

# Enable predictions (PowerShell 7.2+ supports plugins)
Set-PSReadLineOption -PredictionSource HistoryAndPlugin
Set-PSReadLineOption -PredictionViewStyle InlineView

# Key bindings:
# Tab = normal completion
# RightArrow = accept inline suggestion
Remove-PSReadLineKeyHandler -Key Tab
Set-PSReadLineKeyHandler -Key Tab -Function MenuComplete
Set-PSReadLineKeyHandler -Key RightArrow -Function AcceptSuggestion

# Optional: custom color for predictions
Set-PSReadLineOption -Colors @{ InlinePrediction = '#00BFA5' }

## --- Oh My Posh Theme ---
# Use theme name (MSIX installs auto-download themes)
oh-my-posh init pwsh --config "nu4a" | Invoke-Expression

```