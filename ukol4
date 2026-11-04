**Kontrolujeme palindromy**
```powershell
while ($true) {
    $text = Read-Host "Zadejte text (exit pro ukonceni)"

    if ($text -eq "exit") {
        break
    }

    $upraveny = $text.ToLower().Normalize([System.Text.NormalizationForm]::FormD)
    $upraveny = $upraveny -replace '\p{Mn}', ''
    $upraveny = $upraveny -replace '[^a-z0-9]', ''

    if ($upraveny.Length -eq 0) {
        Write-Host "Zadejte platny text." -ForegroundColor Yellow
        continue
    }

    $znaky = $upraveny.ToCharArray()
    [array]::Reverse($znaky)
    $obraceny = -join $znaky

    if ($upraveny -eq $obraceny) {
        Write-Host "Text JE palindrom." -ForegroundColor Green
    }
    else {
        Write-Host "Text NENI palindrom." -ForegroundColor Red
    }
}
```
