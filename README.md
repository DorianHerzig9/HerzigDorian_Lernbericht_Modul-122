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
```powershell
while ($true) {
    $computerName = $env:COMPUTERNAME
    $performanceData = Get-WmiObject -Class Win32_PerfFormattedData_PerfOS_Processor -ComputerName $computerName
    $cpuUsage = $performanceData.PercentProcessorTime
    $memoryData = Get-WmiObject -Class Win32_OperatingSystem -ComputerName $computerName
    $availableMemory = $memoryData.FreePhysicalMemory / 1MB
    $totalMemory = $memoryData.TotalVisibleMemorySize / 1MB

    $cpuUsageFormatted = "{0:N2}%" -f $cpuUsage
    $availableMemoryFormatted = "{0:N2} MB" -f $availableMemory
    $totalMemoryFormatted = "{0:N2} MB" -f $totalMemory

    Write-Host "PC-Leistungsübersicht für $computerName"
    Write-Host "---------------------------------------"
    Write-Host "CPU-Auslastung       : $cpuUsageFormatted"
    Write-Host "Verfügbarer Arbeitsspeicher : $availableMemoryFormatted"
    Write-Host "Gesamter Arbeitsspeicher    : $totalMemoryFormatted"
    Write-Host "---------------------------------------"

    Start-Sleep -Seconds 1
}
```

3. Screenshot der PowerShell-Ausgabe:
![Ausgabee]("C:\Users\A_119591\OneDrive - Kantonsschule Baden\Bilder\Screenshots\Screenshot 2023-07-02 213644.png")

## Verifikation

Die textliche Beschreibung zeigt, dass ich gelernt habe, mit PowerShell Systeminformationen abzurufen und zu formatieren, um eine PC-Leistungsübersicht zu erstellen. Der Code-Fetzen demonstriert die Implementierung des Projekts. Der Screenshot zeigt die tatsächliche Ausgabe der PowerShell-Befehle.

# Reflektion zum Arbeitsprozess

👍 Etwas, was gut lief: Ich fand es gut, wie ich mithilfe von PowerShell die erforderlichen Informationen abrufen und formatieren konnte.

👎 Etwas, was nicht gut lief: Bei der Umsetzung des Projekts hatte ich Schwierigkeiten, die richtigen WMI-Klassen für die benötigten Informationen zu finden.

**VBV**: Als Verbesserungsvorschlag könnte ich vorschlagen, dass ich in Zukunft mehr Zeit investiere, um mich eingehender mit den verfügbaren WMI-Klassen und deren Eigenschaften vertraut zu machen, um die Aufgabe effizienter und reibungsloser zu erledigen.
