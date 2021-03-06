---
title: So installieren Sie den Berichtsserver auf einem eigenständigen Computer und verbinden ihn mit der Datenbank
description: So installieren Sie den Berichtsserver auf einem eigenständigen Computer und verbinden ihn mit der Datenbank
author: dansimp
ms.assetid: 11f07750-4045-4c8d-a583-7d70c9e9aa7b
ms.reviewer: ''
manager: dansimp
ms.author: dansimp
ms.pagetype: mdop, appcompat, virtualization
ms.mktglfcycl: deploy
ms.sitesec: library
ms.prod: w10
ms.date: 06/16/2016
ms.openlocfilehash: 67866714ff6ae60097d9b368fd0eaf361b08eec6
ms.sourcegitcommit: 354664bc527d93f80687cd2eba70d1eea024c7c3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/26/2020
ms.locfileid: "10805378"
---
# So installieren Sie den Berichtsserver auf einem eigenständigen Computer und verbinden ihn mit der Datenbank

Gehen Sie wie folgt vor, um den Berichtsserver auf einem eigenständigen Computer zu installieren und mit der Datenbank zu verbinden.

**Wichtig** Bevor Sie die folgenden Schritte ausführen, sollten Sie die [App-V 5,1-Berichterstellung](about-app-v-51-reporting.md)lesen und verstehen.

## So installieren Sie den Berichtsserver auf einem eigenständigen Computer und verbinden ihn mit der Datenbank

1. Kopieren Sie die App-V 5,1 Server-Installationsdateien auf den Computer, auf dem Sie Sie installieren möchten. Um die App-V 5,1 Server-Installation zu starten, klicken Sie mit der rechten Maustaste, und führen Sie **appv\_server\_setup.exe** als Administrator aus. Klicken Sie auf **Installieren**.

2. Überprüfen und akzeptieren Sie auf der Seite **Erste Schritte** die Lizenzbestimmungen, und klicken Sie auf **weiter**.

3. Aktivieren Sie auf der Seite **Microsoft Update verwenden, um die Sicherheit Ihres Computers zu gewährleisten und auf dem neuesten Stand zu bleiben** , um Microsoft Updates zu aktivieren, die Option **Microsoft Update verwenden, wenn ich auf Updates Suche (empfohlen).** Wenn Sie Microsoft-Updates deaktivieren möchten, wählen Sie **Ich möchte Microsoft Update nicht verwenden**aus. Klicken Sie auf **Weiter**.

4. Aktivieren Sie auf der Seite **Featureauswahl** das Kontrollkästchen **Berichts Server** , und klicken Sie auf **weiter**.

5. Übernehmen Sie auf der Seite **Installationsspeicherort** den Standardspeicherort, und klicken Sie auf **weiter**.

6. Wählen Sie auf der Seite **vorhandene Berichtsdatenbank konfigurieren** die Option **SQL-Remoteserver verwenden**aus, und geben Sie den Computernamen des Computers ein, auf dem Microsoft SQL Server ausgeführt wird, beispielsweise **Sie SQLSERVERMACHINE**.

    > [!NOTE]
    > Wenn Microsoft SQL Server auf demselben Server bereitgestellt wird, wählen Sie **lokalen SQL Server verwenden**aus.

    Wählen Sie für die SQL Server-Instanz **die Option Standardinstanz verwenden**aus. Wenn Sie eine benutzerdefinierte Microsoft SQL Server-Instanz verwenden, müssen Sie **eine benutzerdefinierte Instanz verwenden** auswählen und dann den Namen der Instanz eingeben.

    Geben Sie den **SQL Server-Datenbanknamen** an, den dieser Berichtsserver verwenden soll, beispielsweise **AppvReporting**.

7. Klicken Sie auf der Seite **Konfigurieren der Berichts Server Konfiguration** .

   - Geben Sie den Website Namen an, den Sie für den Berichterstellungsdienst verwenden möchten. Lassen Sie den Standardwert unverändert, wenn Sie keinen benutzerdefinierten Namen haben.

   - Geben Sie für die **Portbindung**eine eindeutige Portnummer an, die von App-V 5,1, beispielsweise **55555**, verwendet wird. Sie sollten auch sicherstellen, dass der angegebene Port nicht von einer anderen Website verwendet wird.

8. Klicken Sie auf **Installieren**.

**Sie haben ein App-V-Problem?** Verwenden Sie das [App-V TechNet-Forum](https://social.technet.microsoft.com/Forums/home?forum=mdopappv).

## Verwandte Themen

[Informationen zur App-V 5.1-Berichterstellung](about-app-v-51-reporting.md)

[Bereitstellen von App-V 5.1](deploying-app-v-51.md)

[So aktivieren Sie die Berichterstellung auf dem App-V 5.1-Client mithilfe von PowerShell](how-to-enable-reporting-on-the-app-v-51-client-by-using-powershell.md)
