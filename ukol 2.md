vypise barvy podle zadani

```powershell
[System.Enum]::GetValues([System.ConsoleColor]) | ForEach-Object {
    $color = $_

    Write-Host ("{0,-15}" -f $color) -NoNewline -ForegroundColor Gray
    Write-Host ("{0,-15}" -f $color) -NoNewline -ForegroundColor $color
    Write-Host ("{0,-15}" -f $color) -ForegroundColor Gray -BackgroundColor $color
}
```
druha verze co je delsi ale mela by fungovat vzdy
```poweshell
$colors = [System.Enum]::GetValues([System.ConsoleColor])

# ANSI codes for the 16 console colors
$fg = @(30, 34, 32, 36, 31, 35, 33, 37,
        90, 94, 92, 96, 91, 95, 93, 97)

$bg = @(40, 44, 42, 46, 41, 45, 43, 47,
        100, 104, 102, 106, 101, 105, 103, 107)

$esc = [char]27

foreach ($color in $colors) {
    $i = [int]$color
    $name = $color.ToString()

    $width = $Host.UI.RawUI.WindowSize.Width

    if ($width -ge 47) {
        $line = "{0,-15}" -f $name
        $line += "$esc[$($fg[$i])m" + ("{0,-15}" -f $name)
        $line += "$esc[0m"
        $line += "$esc[$($bg[$i])m" + ("{0,-15}" -f $name)
        $line += "$esc[0m"
    }
    elseif ($width -ge 32) {
        $line = "{0,-15}" -f $name
        $line += "$esc[$($fg[$i])m$name$esc[0m"
    }
    else {
        $line = "$esc[$($fg[$i])m$name$esc[0m"
    }

    Write-Host $line
}
```
