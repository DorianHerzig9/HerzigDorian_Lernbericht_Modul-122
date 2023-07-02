# Lern-Bericht

## Einleitung

In diesem Projekt ging es darum, eine PC-Leistungsübersicht mit PowerShell zu erstellen.

## Was habe ich gelernt?

Ich habe gelernt, wie man mit PowerShell Systeminformationen abruft und formatiert, um eine Leistungsübersicht des PCs zu erstellen.

## Beschreibung

Um zu zeigen, was ich gelernt habe, verwende ich die folgenden Medien:

1. Textliche Beschreibung:
```plaintext
Mit PowerShell wurden Informationen zur CPU-Auslastung und zum verfügbaren sowie gesamten Arbeitsspeicher abgerufen.
Die Informationen wurden formatiert und anschließend auf der Konsole ausgegeben.
```

2. Code-Fetzen:
```PowerShell
while ($true) {
    $computerName = $env:COMPUTERNAME

    # CPU-Auslastung
    $cpuData = Get-WmiObject -Class Win32_PerfFormattedData_PerfOS_Processor -ComputerName $computerName
    $cpuUsage = $cpuData.PercentProcessorTime
    $cpuUsageFormatted = "{0:N2}%" -f $cpuUsage

    # Verfügbarer Arbeitsspeicher
    $memoryData = Get-WmiObject -Class Win32_OperatingSystem -ComputerName $computerName
    $availableMemory = $memoryData.FreePhysicalMemory / 1MB
    $totalMemory = $memoryData.TotalVisibleMemorySize / 1MB
    $availableMemoryFormatted = "{0:N2} MB" -f $availableMemory
    $totalMemoryFormatted = "{0:N2} MB" -f $totalMemory

    # Festplattenspeicher
    $diskData = Get-WmiObject -Class Win32_LogicalDisk -ComputerName $computerName
    $diskUsage = $diskData | ForEach-Object { $_.DeviceID + ": " + "{0:N2} GB" -f ($_.Size / 1GB) }
    $diskUsageFormatted = $diskUsage -join ", "

    # Netzwerknutzung
    $networkData = Get-WmiObject -Class Win32_PerfFormattedData_Tcpip_NetworkInterface -ComputerName $computerName
    $networkUsage = $networkData | ForEach-Object { $_.Name + ": " + "{0:N2} bytes/sec" -f $_.BytesTotalPerSec }
    $networkUsageFormatted = $networkUsage -join ", "

    # Systemzeit
    $systemTime = Get-Date

    # Ausgabe der PC-Werte
    Write-Host "PC-Leistungsübersicht für $computerName"
    Write-Host "---------------------------------------"
    Write-Host "CPU-Auslastung                : $cpuUsageFormatted"
    Write-Host "Verfügbarer Arbeitsspeicher   : $availableMemoryFormatted"
    Write-Host "Gesamter Arbeitsspeicher      : $totalMemoryFormatted"
    Write-Host "Festplattenspeicher           : $diskUsageFormatted"
    Write-Host "Netzwerknutzung               : $networkUsageFormatted"
    Write-Host "Systemzeit                    : $systemTime"
    Write-Host "---------------------------------------"

    Start-Sleep -Seconds 1
}
```

3. Screenshot der PowerShell-Ausgabe:
<img width="625" alt="Screenshot 2023-07-02 213644" src="https://github.com/DorianHerzig9/HerzigDorian_Lernbericht_Modul-122/assets/110893245/a4d85428-7db3-4f36-8d4b-b512a157f940">


## Verifikation

Die textliche Beschreibung zeigt, dass ich gelernt habe, mit PowerShell Systeminformationen abzurufen und zu formatieren, um eine PC-Leistungsübersicht zu erstellen. Der Code-Fetzen demonstriert die Implementierung des Projekts. Der Screenshot zeigt die tatsächliche Ausgabe der PowerShell-Befehle.

# Reflektion zum Arbeitsprozess

👍 Etwas, was gut lief: Ich fand es gut, wie ich mithilfe von PowerShell die erforderlichen Informationen abrufen und formatieren konnte.

👎 Etwas, was nicht gut lief: Bei der Umsetzung des Projekts hatte ich Schwierigkeiten, die richtigen WMI-Klassen für die benötigten Informationen zu finden.

**VBV**: Als Verbesserungsvorschlag könnte ich vorschlagen, dass ich in Zukunft mehr Zeit investiere, um mich eingehender mit den verfügbaren WMI-Klassen und deren Eigenschaften vertraut zu machen, um die Aufgabe effizienter und reibungsloser zu erledigen.
