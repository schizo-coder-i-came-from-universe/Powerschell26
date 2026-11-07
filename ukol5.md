**1**

Vlastnosti tridy zjistime pomoci skriptu
```poweshell
Get-CimClass -ClassName Win32_Printer
```
Pripadne pro vypsani vsech vlastnosti
```powershell
(Get-CimClass -ClassName Win32_Printer).CimClassProperties
```
Zobrazeni tiskaren a jejich umisteni
```powershell
Get-CimInstance -ClassName Win32_Printer | Select-Object Name, Location
```
Ukazalo se ze FAX nemam v seznamu, proto zmenim umisteni "Microsoft Print to PDF" misto toho:
```powershell
 Get-CimInstance Win32_Printer -Filter "Name='Microsoft Print to PDF'" | Set-CimInstance -Property @{Location="U stareho vlka"}
```
Po overeni pomoci predchoziho kroku je Microsoft Print to PDF nyni U stareho vlka

**2**

Soucasny nazev disku C zjistim pomoci prikazu
```poweshell
Get-CimInstance -ClassName Win32_LogicalDisk -Filter "DeviceID='C:'" | Select-Object DeviceID, VolumeName
```
Muj disk C se nijak nejmenuje, nastavim tedy jmeno na SYSTEM
```powershell
Get-CimInstance -ClassName Win32_LogicalDisk -Filter "DeviceID='C:'" | Set-CimInstance -Property @{VolumeName="System"}
```
Nyni se disk C jmenuje SYSTEM

**3**

Ucty ke kterym se nikdy nikdo neprihlasil zjistim pomoci 
```powershell
Get-CimInstance Win32_NetworkLoginProfile |
    Where-Object { $_.NumberOfLogons -eq 0 } |
    Select-Object Name, NumberOfLogons, LastLogon
```
V mem pripade zadny takovy ucet neexistuje

Pro uzamcene ucty pak pouziji
```powershell
Get-CimInstance Win32_UserAccount |
    Where-Object { $_.Lockout -eq $true } |
    Select-Object Name, Lockout
```
To mi vrati zamecnika a dalsi ucty, ktere jsem uzamkl protoze jsem zapomnel heslo.

Pomoci powershellu muzeme zjistit ucty ke kterym se nikdo neprihlasil:
```powershell
Get-LocalUser |
    Where-Object { $null -eq $_.LastLogon } |
    Select-Object Name, LastLogon
```
Vrati vsak neco jineho, vrati defaultni lokalni ucty jako guest, ktere CIM nejspis nebere v potaz. Nelze pouzit Win32_UserAccount, protoze nema vlastnost LastLogon ani NumberOfLOgons.
Win32_NetworkLoginProfile ale pracuje jen s ucty, ke kterym ma dostupne prihlasovaci udaje. Nejlepsi je tedy pritupy kombinovat.

*Vypsat uzamcene ucty pomoci PS neni mozne bez CIM*
