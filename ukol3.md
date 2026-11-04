1. Vytvoreni aliasu
Set-Alias np notepad.exe
Set-Alias ct control.exe

2. Zaloha do JSON
Get-Alias np, ct | Select-Object Name, Definition |
    ConvertTo-Json | Set-Content aliases.json

3. Zaloha do XML
Get-Alias np, ct | Export-Clixml aliases.xml

4. Smazani aliasu
Remove-Item Alias:np, Alias:ct

5. Obnova z JSON
Get-Content aliases.json | ConvertFrom-Json | ForEach-Object {
    Set-Alias -Name $_.Name -Value $_.Definition
}

Kontrola
Get-Alias np, ct

6. Opetovne smazani
Remove-Item Alias:np, Alias:ct

7. Obnova z XML
Import-Clixml aliases.xml | ForEach-Object {
    Set-Alias -Name $_.Name -Value $_.Definition
}

Zaverecna kontrola
Get-Alias np, ct
