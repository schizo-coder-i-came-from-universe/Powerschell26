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

**Nasledne pocitame znaky slova a tak**
```powershell
while ($true) {
    $text = Read-Host "Zadejte text (exit pro ukonceni)"

    if ($text -eq "exit") {
        break
    }

    # Pocet znaku vcetne mezer
    $sMezerami = $text.Length

    # Pocet znaku bez mezer
    $bezMezer = ($text -replace '\s', '').Length

    # Pocet samohlasek vcetne diakritiky
    $samohlasky = ([regex]::Matches($text, '[aeiouyáéěíóúůýAEIOUYÁÉĚÍÓÚŮÝ]')).Count

    # Pocet slov
    $slova = @($text -split '\s+' | Where-Object { $_ -ne '' }).Count

    # Vypis vysledku
    Write-Host ""
    Write-Host "Pocet znaku s mezerami: $sMezerami" -ForegroundColor Cyan
    Write-Host "Pocet znaku bez mezer: $bezMezer" -ForegroundColor Cyan
    Write-Host "Pocet samohlasek:      $samohlasky" -ForegroundColor Green
    Write-Host "Pocet slov:            $slova" -ForegroundColor Yellow
    Write-Host ""
}
```
