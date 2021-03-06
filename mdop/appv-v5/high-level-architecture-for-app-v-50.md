---
title: High-Level-Architektur für App-V 5.0
description: High-Level-Architektur für App-V 5.0
author: dansimp
ms.assetid: fdf8b841-918f-4672-b352-0f2b9519581b
ms.reviewer: ''
manager: dansimp
ms.author: dansimp
ms.pagetype: mdop, appcompat, virtualization
ms.mktglfcycl: deploy
ms.sitesec: library
ms.prod: w10
ms.date: 06/16/2016
ms.openlocfilehash: 0ec105ffcc3213e488615603484b2de6bafce4d3
ms.sourcegitcommit: 354664bc527d93f80687cd2eba70d1eea024c7c3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/26/2020
ms.locfileid: "10805816"
---
# High-Level-Architektur für App-V 5.0


Verwenden Sie die folgenden Informationen, um Ihnen zu helfen, die Microsoft Application Virtualization (App-V) 5,0-Bereitstellung zu vereinfachen.

## Übersicht über die Architektur


Eine typische App-V 5,0-Implementierung besteht aus den folgenden Elementen.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Element</th>
<th align="left">Weitere Informationen</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>App-V 5,0-Verwaltungs Server</p></td>
<td align="left"><p>Der APP-v 5,0-Verwaltungsserver bietet allgemeine Verwaltungsfunktionen für die APP-v 5,0-Infrastruktur. Darüber hinaus können Sie mehr als eine Instanz des Verwaltungsservers in Ihrer Umgebung installieren, die die folgenden Vorteile bietet:</p>
<ul>
<li><p>Fehlertoleranz und höhere Verfügbarkeit – die Installation und Konfiguration des App-V 5,0-Verwaltungsservers auf zwei separaten Computern kann in Situationen helfen, in denen einer der Server nicht verfügbar oder offline ist.</p>
<p>Sie können auch die Verfügbarkeit von App-V 5,0 erhöhen, indem Sie den Verwaltungsserver auf mehreren Computern installieren. In diesem Szenario sollte auch ein Netzwerklastenausgleich berücksichtigt werden, damit Server Anforderungen ausgeglichen sind.</p></li>
<li><p>Skalierbarkeit – Sie können bei Bedarf zusätzliche Verwaltungsserver hinzufügen, um eine hohe Auslastung zu unterstützen, beispielsweise können Sie mehrere Server hinter einem Load Balancer installieren.</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>App-V 5,0-Veröffentlichungs Server</p></td>
<td align="left"><p>Der App-V 5,0-Publishing Server bietet Funktionen für das Hosten und Streaming virtueller Anwendungen. Der Veröffentlichungsserver erfordert keine Datenbankverbindung und unterstützt die folgenden Protokolle:</p>
<ul>
<li><p>HTTP und HTTPS</p></li>
</ul>
<p>Sie können auch die Verfügbarkeit von App-V 5,0 verbessern, indem Sie den Veröffentlichungsserver auf mehreren Computern installieren. Darüber hinaus sollte ein Netzwerklastenausgleich berücksichtigt werden, damit Server Anforderungen ausgeglichen sind.</p></td>
</tr>
<tr class="odd">
<td align="left"><p>App-V 5,0-Berichts Server</p></td>
<td align="left"><p>Der APP-v 5,0-Berichtsserver ermöglicht autorisierten Benutzern, vorhandene App-v 5,0-Berichte und Ad-hoc-Berichte auszuführen und anzuzeigen, die Ihnen beim Verwalten der APP-v 5,0-Infrastruktur behilflich sein können. Der Berichtsserver erfordert eine Verbindung mit der App-V 5,0-Berichtsdatenbank. Sie können auch die Verfügbarkeit von App-V 5,0 verbessern, indem Sie den Berichtsserver auf mehreren Computern installieren. Darüber hinaus sollte ein Netzwerklastenausgleich berücksichtigt werden, damit Server Anforderungen ausgeglichen sind.</p></td>
</tr>
<tr class="even">
<td align="left"><p>App-V 5,0-Client</p></td>
<td align="left"><p>Mit dem App-v 5,0-Client können Pakete, die mit App-v 5,0 erstellt wurden, auf Zielcomputern ausgeführt werden.</p></td>
</tr>
</tbody>
</table>

 

**Hinweis**  Wenn Sie App-v 5,0 mit ESD (Electronic Software Distribution) verwenden, müssen Sie den App-v 5,0-Verwaltungsserver nicht verwenden, Sie können jedoch weiterhin die Bericht Erstellungs-und Streamingfunktionen von App-v 5,0 nutzen.

 






## Verwandte Themen


[Erste Schritte mit App-V 5.0](getting-started-with-app-v-50--rtm.md)

 

 





