[System.Enum]::GetValues([System.ConsoleColor]) | ForEach-Object {
    $color = $_

    Write-Host ("{0,-15}" -f $color) -NoNewline -ForegroundColor Gray
    Write-Host ("{0,-15}" -f $color) -NoNewline -ForegroundColor $color
    Write-Host ("{0,-15}" -f $color) -ForegroundColor Gray -BackgroundColor $color
}
