---
title: Versionshinweise für DaRT 8.1
description: Versionshinweise für DaRT 8.1
author: dansimp
ms.assetid: 44303107-60f4-485c-848a-7e0529f142d4
ms.reviewer: ''
manager: dansimp
ms.author: dansimp
ms.pagetype: mdop
ms.mktglfcycl: support
ms.sitesec: library
ms.prod: w10
ms.date: 06/16/2016
ms.openlocfilehash: 0d0ba817ddd5bbdefcf7fed833f4c47e7b9d9ce0
ms.sourcegitcommit: 354664bc527d93f80687cd2eba70d1eea024c7c3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/26/2020
ms.locfileid: "10810750"
---
# Versionshinweise für DaRT 8.1


**Drücken Sie STRG + F, um diese Versionshinweise zu durchsuchen.**

Lesen Sie diese Versionshinweise gründlich, bevor Sie Microsoft Diagnostics and Recovery Toolset (Dart) 8,1 installieren.

Diese Versionshinweise enthalten Informationen, die erforderlich sind, um die Diagnose-und Wiederherstellungs-Toolset 8,1 erfolgreich zu installieren. Die Anmerkungen zu dieser Version enthalten auch Informationen, die in der Produktdokumentation nicht zur Verfügung stehen. Wenn es einen Unterschied zwischen diesen Versionshinweisen und anderer Dart-Dokumentation gibt, sollte die neueste Änderung als autorisierend angesehen werden. Diese Versionshinweise ersetzen die Inhalte, die in diesem Produkt enthalten sind.

## Bekannte Probleme mit Dart 8,1


### Disk Commander kann einen beschädigten Master-Boot-Eintrag in einer physikalischen Partition in Windows 8,1 nicht reparieren

In Windows 8,1 kann der "Master Boot Record (MBR) wiederherstellen" oder die Kopfzeile der GUID-Partitionstabelle (GPT)-Option in Disk Commander keinen beschädigten Master-Boot-Eintrag in einer physikalischen Partition reparieren, und der Clientcomputer kann daher nicht gestartet werden.

**Problemumgehung:** Starten Sie die **Systemstartreparatur**, klicken Sie auf **Problembehandlung**, klicken Sie auf **Erweiterte Optionen**, und klicken Sie dann auf **Reparieren**.

### Mehrere Instanzen des Datenträger Abwischens, die auf dasselbe Laufwerk ausgerichtet sind, führen dazu, dass alle Instanzen, mit Ausnahme der letzten, einen Fehler melden.

Wenn Sie mehrere Instanzen der Datenträger Zurücksetzung starten und dann versuchen, dasselbe Laufwerk mithilfe von zwei separaten Datenträger Zurücksetzungs Instanzen zu wischen, melden alle Instanzen mit Ausnahme des letzten einen Fehler beim wischen des Laufwerks.

**Problemumgehung:** Keine.

### Bei der Datenträger Zurücksetzung werden möglicherweise nicht alle Daten auf Solid-State-Laufwerken mit Flash Speicher gelöscht

Wenn Sie Daten auf einem Solid-State-Laufwerk (SSD) mit Flash-Speicher löschen, werden alle Daten möglicherweise nicht gelöscht. Dieses Problem tritt auf, weil die SSD-Firmware den physikalischen Standort von Schreibvorgängen steuert, während die Datenträgerbereinigung ausgeführt wird.

**Problemumgehung:** Keine.

### System Wiederherstellung schlägt fehl, wenn Sie den Schlosser-Assistenten oder den Registrierungs-Editor ausführen

Wenn Sie den Schlosser-Assistenten, den Registrierungs-Editor und möglicherweise andere Tools ausführen, schlägt die System Wiederherstellung fehl.

**Problemumgehung:** Schließen Sie Dart, und starten Sie es erneut, und starten Sie dann die System Wiederherstellung.

### Der System Datei-Checker-Scan (SFC) kann nicht ausgeführt werden, nachdem Sie den Schlosser-Assistenten oder die Computer Verwaltung gestartet und geschlossen haben.

Wenn Sie den Schlosser-Assistenten oder die Tools in der Computer Verwaltung starten und dann schließen, kann die System Dateiprüfung nicht ausgeführt werden.

**Problemumgehung:** Schließen Sie Dart, und starten Sie es erneut, und starten Sie dann die System Dateiprüfung.

### <a href="" id="-------------dart-installer-does-not-fail-when-the-windows-assessment-and-deployment-kit-is-not-installed"></a> Dart-Installationsprogramm schlägt nicht fehl, wenn das Windows Assessment-und Deployment Kit nicht installiert ist

Wenn Sie Dart 8,1 über die Befehlszeile zum Ausführen des Windows Installers (MSI) installieren und das Windows Assessment and Deployment Kit (WindowsADK) nicht installiert wurde, sollte die Dart-Installation fehlschlagen. Derzeit installiert das Dart 8,1-Installationsprogramm alle Komponenten mit Ausnahme des DART-Wiederherstellungs Bilds.

**Problemumgehung:** Keine.

### Windows Defender kann nicht gestartet werden, nachdem der Schlosser-Assistent, der Registrierungs-Editor, Crash Analyzer und die Computer Verwaltung gestartet wurden.

Windows Defender wird nicht gestartet, wenn Sie Schlosser-Assistent, Registrierungs-Editor, Crash Analyzer und Computer Verwaltung bereits begonnen haben.

**Problemumgehung:** Schließen Sie Dart, und starten Sie es erneut, und starten Sie dann Windows Defender.

### Windows Defender kann langsam gestartet werden

Windows Defender benötigt manchmal einige Minuten, um zu starten. Auf der Statusleiste wird der aktuelle Ladestatus angezeigt.

**Problemumgehung:** Keine.

## Verwandte Themen


[Informationen zu DaRT 8.1](about-dart-81.md)

 

 





