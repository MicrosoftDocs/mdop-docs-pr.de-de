---
title: Installieren des App-V 5.1-Clients für den SCS-Modus (Shared Content Store)
description: Installieren des App-V 5.1-Clients für den SCS-Modus (Shared Content Store)
author: dansimp
ms.assetid: 6f3ecb1b-b5b5-4ae0-8de9-b4ffdfd2c216
ms.reviewer: ''
manager: dansimp
ms.author: dansimp
ms.pagetype: mdop, appcompat, virtualization
ms.mktglfcycl: deploy
ms.sitesec: library
ms.prod: w10
ms.date: 08/30/2016
ms.openlocfilehash: a7ce8114a44762180bf9bb0240913dca50c55d31
ms.sourcegitcommit: 354664bc527d93f80687cd2eba70d1eea024c7c3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/26/2020
ms.locfileid: "10805438"
---
# Installieren des App-V 5.1-Clients für den SCS-Modus (Shared Content Store)


Gehen Sie wie folgt vor, um den Microsoft Application Virtualization (app-v) 5,1-Client so zu installieren, dass der APP-v 5,1 Shared Content Store (SCS)-Modus verwendet wird. Stellen Sie sicher, dass alle erforderlichen Voraussetzungen auf dem Computer installiert sind, auf dem Sie die Installation planen. Verwenden Sie den folgenden Link, um die [Voraussetzungen für App-V 5,1](app-v-51-prerequisites.md)anzuzeigen.

**Hinweis**  Bevor Sie diesen Vorgang ausführen, falls erforderlich, deinstallieren Sie eine vorhandene Version des App-V 5,1-Clients.

 

Weitere Informationen zum SCS-Modus finden Sie unter [freigegebenen Inhaltsspeicher in Microsoft App-V 5,0 – Behind the Scenes](https://go.microsoft.com/fwlink/?LinkId=316879) ( https://go.microsoft.com/fwlink/?LinkId=316879) .

**Installieren und Konfigurieren des App-V 5,1-Clients für den SCS-Modus**

1.  Kopieren Sie die App-V 5,1-Clientinstallationsdateien auf den Computer, auf dem Sie installiert werden soll. Öffnen Sie eine Befehlszeile, und geben Sie in dem Verzeichnis, in dem die Installationsdateien gespeichert sind, je nach der Version des zu installierenden Clients eine der folgenden Optionen ein:

    -   So installieren Sie die RDS-Version des App-V 5,1-Clienttyps: **appv\_client\_setup\_rds.exe/SHAREDCONTENTSTOREMODE = 1/q**

    -   So installieren Sie die Standard Version des App-V 5,1-Clienttyps: **appv\_client\_setup.exe/SHAREDCONTENTSTOREMODE = 1/q**

        **Wichtig**  Sie müssen eine unbeaufsichtigte Installation durchführen, oder die Installation schlägt fehl.

         

2.  Nachdem Sie die Installation abgeschlossen haben, können Sie Pakete auf dem Computer bereitstellen, auf dem der Client ausgeführt wird, und alle Paketinhalte werden über das Netzwerk gestreamt.

    Sie **haben einen Vorschlag für App-V**? [Hier](http://appv.uservoice.com/forums/280448-microsoft-application-virtualization)können Sie Vorschläge hinzufügen oder abstimmen. **Sie haben ein App-V-Problem?** Verwenden Sie das [App-V TechNet-Forum](https://social.technet.microsoft.com/Forums/home?forum=mdopappv).

## Verwandte Themen


[Bereitstellen von App-V 5.1-Sequencer und -Client](deploying-the-app-v-51-sequencer-and-client.md)

 

 





