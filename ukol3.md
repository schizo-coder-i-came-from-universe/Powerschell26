1. Vytvoreni aliasu
```poweshell
Set-Alias np notepad.exe
Set-Alias ct control.exe
```
2. Zaloha do JSON
```poweshell
Get-Alias np, ct | Select-Object Name, Definition |
    ConvertTo-Json | Set-Content aliases.json
```
3. Zaloha do XML
```poweshell
Get-Alias np, ct | Export-Clixml aliases.xml
```
4. Smazani aliasu
```poweshell
Remove-Item Alias:np, Alias:ct
```
5. Obnova z JSON
```poweshell
Get-Content aliases.json | ConvertFrom-Json | ForEach-Object {
    Set-Alias -Name $_.Name -Value $_.Definition
}
```
Kontrola
```poweshell
Get-Alias np, ct
```
6. Opetovne smazani
```poweshell
Remove-Item Alias:np, Alias:ct
```
7. Obnova z XML
```poweshell
Import-Clixml aliases.xml | ForEach-Object {
    Set-Alias -Name $_.Name -Value $_.Definition
}
```
Zaverecna kontrola
```poweshell
Get-Alias np, ct
```
