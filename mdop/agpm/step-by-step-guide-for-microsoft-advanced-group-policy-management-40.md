---
title: Schrittweise Anleitung für Microsoft Advanced Group Policy Management 4.0
description: Schrittweise Anleitung für Microsoft Advanced Group Policy Management 4.0
author: dansimp
ms.assetid: dc6f9b16-b1d4-48f3-88bb-f29301f0131c
ms.reviewer: ''
manager: dansimp
ms.author: dansimp
ms.pagetype: mdop
ms.mktglfcycl: manage
ms.sitesec: library
ms.prod: w10
ms.date: 08/30/2016
ms.openlocfilehash: 819d536451095d23080115799016aa0ac5242dee
ms.sourcegitcommit: 354664bc527d93f80687cd2eba70d1eea024c7c3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/26/2020
ms.locfileid: "10808211"
---
# Schrittweise Anleitung für Microsoft Advanced Group Policy Management 4.0


Diese schrittweise Anleitung zeigt erweiterte Techniken für die Gruppenrichtlinienverwaltung, die die Gruppenrichtlinien-Verwaltungskonsole (Group Policy Management Console, GPMC) und Microsoft Advanced Group Policy Management (AGPM) verwenden. AGPM vergrößert die Funktionen der GPMC und bietet Folgendes:

-   Standard Rollen für das Delegieren von Berechtigungen zum Verwalten von Gruppenrichtlinienobjekten (GPOs) an mehrere Gruppenrichtlinienadministratoren sowie die Möglichkeit, den Zugriff auf GPOs in der Produktionsumgebung zu delegieren.

-   Ein Archiv, damit Gruppenrichtlinienadministratoren GPOs offline erstellen und ändern können, bevor die GPOs in einer Produktionsumgebung bereitgestellt werden.

-   Die Möglichkeit, auf eine frühere Version eines GPO im Archiv zurückzusetzen und die Anzahl der im Archiv gespeicherten Versionen zu begrenzen.

-   Möglichkeit zum ein-und Auschecken von GPOs, um sicherzustellen, dass Gruppenrichtlinienadministratoren die Arbeit des anderen nicht versehentlich überschreiben.

-   Die Möglichkeit, nach GPOs mit bestimmten Attributen zu suchen und die Liste der angezeigten GPOs zu filtern.

## Übersicht über AGPM-Szenarien


In diesem Szenario verwenden Sie für jede Rolle in AGPM ein separates Benutzerkonto, um zu veranschaulichen, wie Gruppenrichtlinien in einer Umgebung verwaltet werden können, die mehrere Gruppenrichtlinienadministratoren mit unterschiedlichen Berechtigungsstufen aufweist. Insbesondere führen Sie die folgenden Aufgaben aus:

-   Wenn Sie ein Konto verwenden, das Mitglied der Gruppe der Domänenadministratoren ist, installieren Sie AGPM Server, und weisen Sie die Rolle AGPM-Administrator einem Konto oder einer Gruppe zu.

-   Installieren Sie AGPM-Client mithilfe von Konten, denen Sie AGPM-Rollen zuweisen.

-   Verwenden Sie ein Konto mit der Rolle AGPM-Administrator, konfigurieren Sie AGPM, und delegieren Sie den Zugriff auf GPOs, indem Sie anderen Konten Rollen zuweisen.

-   Fordern Sie von einem Konto mit der Rolle "Editor" an, dass ein neues Gruppenrichtlinienobjekt erstellt wird, das Sie dann mit einem Konto genehmigen, das über die Rolle "genehmigende Person" verfügt. Verwenden Sie das Editor-Konto, um das Gruppenrichtlinienobjekt aus dem Archiv zu überprüfen, das Gruppenrichtlinienobjekt zu bearbeiten, das Gruppenrichtlinienobjekt in das Archiv zu überprüfen und die Bereitstellung anzufordern.

-   Überprüfen Sie das Gruppenrichtlinienobjekt, und stellen Sie es in Ihrer Produktionsumgebung bereit, indem Sie ein Konto verwenden, das die Rolle genehmigende Person aufweist.

-   Erstellen Sie mithilfe eines Kontos mit der Rolle "Editor" eine GPO-Vorlage, und verwenden Sie Sie als Ausgangspunkt zum Erstellen eines neuen Gruppenrichtlinienobjekts.

-   Wenn Sie ein Konto verwenden, das über die Rolle genehmigende Person verfügt, löschen Sie ein GPO, und stellen Sie es wieder her.

![Entwicklungsprozess für Gruppenrichtlinienobjekte](images/ab77a1f3-f430-4e7d-be58-ee8f9bd1140e.gif)

## Anforderungen


Computer, auf denen Sie AGPM installieren möchten, müssen die folgenden Anforderungen erfüllen, und Sie müssen Konten erstellen, die in diesem Szenario verwendet werden können.

**Hinweis**  Wenn Sie AGPM 2,5 installiert haben und ein Upgrade von Windows Server® 2003 auf Windows Server2008R2 oder Windows Server2008 durchführen oder ein Upgrade von Windows Vista ohne installierte Service Packs auf Windows7 oder Windows Vista® mit Service Pack1 (SP1) durchführen, müssen Sie das Betriebssystem aktualisieren, bevor Sie auf AGPM 4.0 aktualisieren können.

Wenn Sie AGPM 3,0 installiert haben, müssen Sie das Betriebssystem nicht aktualisieren, bevor Sie auf AGPM 4,0 aktualisieren.

 

In einer gemischten Umgebung, die sowohl neuere als auch ältere Betriebssysteme umfasst, gibt es einige Funktionseinschränkungen, wie in der folgenden Tabelle angegeben.

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Betriebssystem, auf dem AGPM Server 4,0 ausgeführt wird</th>
<th align="left">Betriebssystem, auf dem AGPM-Client 4,0 ausgeführt wird</th>
<th align="left">Status der Unterstützung von AGPM 4,0</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows Server2008R2 oder Windows7</p></td>
<td align="left"><p>Windows Server2008R2 oder Windows7</p></td>
<td align="left"><p>Unterstützt</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows Server2008R2 oder Windows7</p></td>
<td align="left"><p>Windows Server2008 oder Windows Vista mit SP1</p></td>
<td align="left"><p>Unterstützt, aber Richtlinieneinstellungen oder Einstellungselemente, die nur in Windows Server2008R2 oder Windows7 vorhanden sind, können nicht bearbeitet werden</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Server2008 oder Windows Vista mit SP1</p></td>
<td align="left"><p>Windows Server2008R2 oder Windows7</p></td>
<td align="left"><p>Nicht unterstützt</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows Server2008 oder Windows Vista mit SP1</p></td>
<td align="left"><p>Windows Server2008 oder Windows Vista mit SP1</p></td>
<td align="left"><p>Unterstützt, aber Richtlinieneinstellungen oder Einstellungselemente, die nur in Windows Server2008R2 oder Windows7 vorhanden sind, können nicht gemeldet oder bearbeitet werden</p></td>
</tr>
</tbody>
</table>

 

### AGPM-Server Anforderungen

Für AGPM Server 4.0 sind Windows-Server2008R2, Windows Server2008, Windows7 und die GPMC von Remote Server-Verwaltungs Tools (Remote Server Administration Tools) oder Windows Vista mit SP1 und die GPMC von Remote Server-Verwaltungskonsole erforderlich. Sowohl 32-Bit-als auch 64-Bit-Versionen werden unterstützt.

Bevor Sie AGPM Server installieren, müssen Sie Mitglied der Gruppe der Domänenadministratoren sein, und die folgenden Windows-Features müssen vorhanden sein, sofern nicht anders angegeben:

-   GPMC

    -   Windows Server2008R2 oder Windows Server2008: Wenn die GPMC nicht vorhanden ist, wird Sie von AGPM automatisch installiert.

    -   Windows7: Sie müssen die GPMC vor der Installation von AGPM über die Remoteverwaltungskonsole installieren. Weitere Informationen finden Sie unter [Remote Server-Verwaltungs Tools für Windows 7](https://go.microsoft.com/fwlink/?LinkID=131280) ( https://go.microsoft.com/fwlink/?LinkID=131280) .

    -   Windows Vista mit SP1: Sie müssen die GPMC vor der Installation von AGPM über die Remoteverwaltungskonsole installieren. Weitere Informationen finden Sie unter [Remote Server-Verwaltungs Tools für Windows Vista mit Service Pack 1](https://go.microsoft.com/fwlink/?LinkID=116179) ( https://go.microsoft.com/fwlink/?LinkID=116179) .

-   .NET Framework 3,5 oder höhere Versionen

    -   Windows Server2008R2 oder Windows7: Wenn die .NET Framework-Version 3,5 oder höher nicht vorhanden ist, wird .NET Framework 3,5 automatisch von AGPM installiert.

    -   Windows Server2008 oder Windows Vista mit SP1: Sie müssen .NET Framework 3,5 oder eine neuere Version installieren, bevor Sie AGPM installieren.

Die folgenden Windows-Features sind für AGPM Server erforderlich und werden automatisch installiert, wenn Sie nicht vorhanden sind:

-   WCF-Aktivierung; Nicht-HTTP-Aktivierung

-   Windows-Prozessaktivierungsdienst

    -   Prozessmodell

    -   .NET-Umgebung

    -   Konfigurations-APIs

### AGPM-Client Anforderungen

AGPM Client 4.0 erfordert Windows-Server2008R2, Windows Server2008, Windows7 und die GPMC von der Remote-Verwaltungskonsole oder Windows Vista mit SP1 und die GPMC von Remote-Verwaltungskonsole installiert. Sowohl 32-Bit-als auch 64-Bit-Versionen werden unterstützt. AGPM-Client kann auf einem Computer installiert werden, auf dem AGPM Server ausgeführt wird.

Die folgenden Windows-Features sind für AGPM-Client erforderlich und werden, sofern nicht anders angegeben, automatisch installiert, wenn Sie nicht vorhanden sind:

-   GPMC

    -   Windows Server2008R2 oder Windows Server2008: Wenn die GPMC nicht vorhanden ist, wird Sie von AGPM automatisch installiert.

    -   Windows7: Sie müssen die GPMC vor der Installation von AGPM über die Remoteverwaltungskonsole installieren. Weitere Informationen finden Sie unter [Remote Server-Verwaltungs Tools für Windows 7](https://go.microsoft.com/fwlink/?LinkID=131280) ( https://go.microsoft.com/fwlink/?LinkID=131280) .

    -   Windows Vista mit SP1: Sie müssen die GPMC vor der Installation von AGPM über die Remoteverwaltungskonsole installieren. Weitere Informationen finden Sie unter [Remote Server-Verwaltungs Tools für Windows Vista mit Service Pack 1](https://go.microsoft.com/fwlink/?LinkID=116179) ( https://go.microsoft.com/fwlink/?LinkID=116179) .

-   .NET Framework 3,0 oder höhere Version

    -   Windows Server2008R2 oder Windows7: Wenn die .NET Framework-Version 3,0 oder höher nicht vorhanden ist, wird .NET Framework 3,5 automatisch von AGPM installiert.

    -   Windows Server2008 oder Windows Vista mit SP1: Wenn die .NET Framework-Version 3,0 oder höher nicht vorhanden ist, wird .NET Framework 3,0 automatisch von AGPM installiert.

### Voraussetzungen für Szenarien

Bevor Sie mit diesem Szenario beginnen, erstellen Sie vier Benutzerkonten. Während des Szenarios weisen Sie jedem dieser Konten eine der folgenden AGPM-Rollen zu: AGPM-Administrator (Vollzugriff), genehmigende Person, Editor und Bearbeiter. Diese Konten müssen in der Lage sein, e-Mail-Nachrichten zu senden und zu empfangen. Weisen Sie den Konten mit den Rollen des AGPM-Administrators, genehmigenden und (optional)-Editors die Berechtigung **Link-GPOs** zu.

**Hinweis** 
 Die Berechtigung " **GPOs verknüpfen** " wird standardmäßig Mitgliedern von Domänenadministratoren und Unternehmensadministratoren zugewiesen. Klicken Sie auf den Knoten für die Domäne, und klicken Sie dann auf die Registerkarte **Delegierung** , wählen Sie **GPOs verknüpfen**aus, klicken Sie auf **Hinzufügen**, und wählen Sie dann Benutzer oder Gruppen aus, denen Sie **die Berechtigung zuweisen** möchten, um anderen Benutzern oder Gruppen (wie Konten, die die Rollen "AGPM-Administrator" oder "Genehmiger" aufweisen) Berechtigungen zuzuweisen.

 

## Schritte zum Installieren und Konfigurieren von AGPM


Sie müssen die folgenden Schritte ausführen, um AGPM zu installieren und zu konfigurieren.

[Schritt 1: Installieren des AGPM-Servers](#bkmk-config1)

[Schritt 2: Installieren des AGPM-Clients](#bkmk-config2)

[Schritt 3: Konfigurieren einer AGPM-Server Verbindung](#bkmk-config3)

[Schritt 4: Konfigurieren einer e-Mail-Benachrichtigung](#bkmk-config4)

[Schritt 5: Delegieren des Zugriffs](#bkmk-config5)

### <a href="" id="bkmk-config1"></a>Schritt 1: Installieren des AGPM-Servers

In diesem Schritt installieren Sie AGPM Server auf dem Mitglieds Server oder Domänencontroller, auf dem der AGPM-Dienst ausgeführt wird, und konfigurieren das Archiv. Alle AGPM-Vorgänge werden über diesen Windows-Dienst verwaltet und mit den Anmeldeinformationen des Diensts ausgeführt. Das von einem AGPM-Server verwaltete Archiv kann auf diesem Server oder auf einem anderen Server in derselben Gesamtstruktur gehostet werden.

**So installieren Sie AGPM Server auf dem Computer, der den AGPM-Dienst hosten soll**

1.  Melden Sie sich mit einem Konto an, das Mitglied der Gruppe der Domänenadministratoren ist.

2.  Starten Sie die Microsoft Desktop Optimization Pack-CD, und folgen Sie den Anweisungen auf dem Bildschirm, um **Advanced Group Policy Management-Server**auszuwählen.

3.  Klicken Sie im Dialogfeld **Willkommen** auf **weiter**.

4.  Akzeptieren Sie im Dialogfeld **Microsoft-Software-Lizenzbestimmungen** die Begriffe, und klicken Sie dann auf **weiter**.

5.  Wählen Sie im Dialogfeld **Anwendungspfad** einen Speicherort aus, an dem AGPM Server installiert werden soll. Auf dem Computer, auf dem AGPM Server installiert ist, wird der AGPM-Dienst gehostet und das Archiv verwaltet. Klicken Sie auf **Weiter**.

6.  Wählen Sie im Dialogfeld **Archivpfad** einen Speicherort für das Archiv in Bezug auf den AGPM-Server aus. Der Archivpfad kann auf einen Ordner auf dem AGPM-Server oder anderswo verweisen. Sie sollten jedoch einen Speicherort mit genügend Speicherplatz auswählen, um alle GPOs und Verlaufsdaten zu speichern, die von diesem AGPM-Server verwaltet werden. Klicken Sie auf **Weiter**.

7.  Wählen Sie im Dialogfeld **AGPM-Dienstkonto** ein Dienstkonto aus, unter dem der AGPM-Dienst ausgeführt wird, und klicken Sie dann auf **weiter**.

    Dieses Konto muss ein Mitglied der Gruppe der Domänenadministratoren oder, bei einer Konfiguration mit geringsten Berechtigungen, die folgenden Gruppen in jeder vom AGPM-Server verwalteten Domäne sein:

    -   Besitzer von Gruppenrichtlinien Erstellern

    -   Sicherungs-Operatoren

    Darüber hinaus erfordert dieses Konto die Berechtigung "Vollzugriff" für die folgenden Ordner:

    -   Der Ordner "AGPM-Archiv", für den diese Berechtigung automatisch während der Installation von AGPM Server erteilt wird, wenn Sie auf einem lokalen Laufwerk installiert ist.

    -   Der temporäre Ordner des lokalen Systems, in der Regel%windir%\\temp.

8.  Wählen Sie im Dialogfeld **Besitzer des Archivs** ein Konto oder eine Gruppe aus, dem Sie die Rolle AGPM-Administrator (Vollzugriff) zuweisen. AGPM-Administratoren können AGPM-Rollen und-Berechtigungen anderen Gruppenrichtlinienadministratoren zuweisen, damit Sie später die Rolle des AGPM-Administrators zusätzlichen Gruppenrichtlinienadministratoren zuweisen können. Wählen Sie in diesem Szenario das Konto aus, das in der Rolle des AGPM-Administrators dienen soll. Klicken Sie auf **Weiter**.

9.  Geben Sie im Dialogfeld **Portkonfiguration** einen Port ein, den der AGPM-Dienst abhören soll. Deaktivieren Sie das Kontrollkästchen **Portausnahme für Firewall hinzufügen** , es sei denn, Sie konfigurieren Portausnahmen manuell oder verwenden Regeln, um Portausnahmen zu konfigurieren. Klicken Sie auf **Weiter**.

10. Wählen Sie im Dialogfeld **Sprachen** eine oder mehrere Anzeigesprachen aus, die für AGPM Server installiert werden sollen.

11. Klicken Sie auf **Installieren**, und klicken Sie dann auf **Fertig stellen** , um den Setup-Assistenten zu beenden.

    **Vorsicht**  Ändern Sie die Einstellungen für den AGPM-Dienst nicht über **Administrative Tools** und **Dienste** im Betriebssystem. Dadurch kann der Start des AGPM-Diensts verhindert werden. Informationen zum Ändern der Einstellungen für den Dienst finden Sie unter Hilfe zur erweiterten Gruppenrichtlinienverwaltung.

     

### <a href="" id="bkmk-config2"></a>Schritt 2: Installieren des AGPM-Clients

Jeder Gruppenrichtlinienadministrator – jeder, der GPOs erstellt, bearbeitet, bereitstellt, überprüft oder löscht, muss AGPM-Client auf Computern installiert haben, die Sie zum Verwalten von GPOs verwenden. Der Knoten Änderungs Steuerelement, mit dem Sie viele der GPO-Verwaltungsaufgaben ausführen, wird nur dann in der Gruppenrichtlinien-Verwaltungskonsole angezeigt, wenn Sie den AGPM-Client installieren. In diesem Szenario installieren Sie AGPM-Client auf mindestens einem Computer. Sie müssen den AGPM-Client nicht auf den Computern von Endbenutzern installieren, die keine Gruppenrichtlinienverwaltung durchführen.

**So installieren Sie den AGPM-Client auf dem Computer eines Gruppenrichtlinienadministrators**

1.  Starten Sie die Microsoft Desktop Optimization Pack-CD, und folgen Sie den Anweisungen auf dem Bildschirm, um **Erweiterte Gruppenrichtlinienverwaltung-Client**auszuwählen.

2.  Klicken Sie im Dialogfeld **Willkommen** auf **weiter**.

3.  Akzeptieren Sie im Dialogfeld **Microsoft-Software-Lizenzbestimmungen** die Begriffe, und klicken Sie dann auf **weiter**.

4.  Wählen Sie im Dialogfeld **Anwendungspfad** einen Speicherort aus, an dem AGPM-Client installiert werden soll. Klicken Sie auf **Weiter**.

5.  Geben Sie im Dialogfeld **AGPM-Server** den DNS-Namen oder die IP-Adresse für den AGPM-Server und den Port ein, mit dem Sie eine Verbindung herstellen möchten. Der Standardport für den AGPM-Dienst ist 4600. Deaktivieren Sie das Kontrollkästchen **Microsoft Management Console über das Firewall zulassen** , es sei denn, Sie konfigurieren Portausnahmen manuell oder verwenden Regeln, um Portausnahmen zu konfigurieren. Klicken Sie auf **Weiter**.

6.  Wählen Sie im Dialogfeld **Sprachen** eine oder mehrere Anzeigesprachen aus, die für AGPM-Client installiert werden sollen.

7.  Klicken Sie auf **Installieren**, und klicken Sie dann auf **Fertig stellen** , um den Setup-Assistenten zu beenden.

### <a href="" id="bkmk-config3"></a>Schritt 3: Konfigurieren einer AGPM-Server Verbindung

AGPM speichert alle Versionen der einzelnen gesteuerten Gruppenrichtlinienobjekte (GPO), also jedes GPO, für das AGPM Änderungs Steuerelemente bereitstellt, in einem zentralen Archiv. Dadurch können Gruppenrichtlinienadministratoren Gruppenrichtlinienobjekte offline anzeigen und ändern, ohne die bereitgestellte Version jedes GPO unmittelbar zu beeinflussen.

In diesem Schritt konfigurieren Sie eine AGPM-Serververbindung und stellen sicher, dass alle Gruppenrichtlinienadministratoren eine Verbindung mit dem gleichen AGPM-Server herstellen. (Informationen zum Konfigurieren mehrerer AGPM-Server finden Sie unter Hilfe zur erweiterten Gruppenrichtlinienverwaltung.)

**So konfigurieren Sie eine AGPM-Server Verbindung für alle Gruppenrichtlinienadministratoren**

1.  Melden Sie sich auf einem Computer, auf dem Sie AGPM-Client installiert haben, mit dem Benutzerkonto an, das Sie als Archiv Besitzer ausgewählt haben. Dieser Benutzer hat die Rolle des AGPM-Administrators (Vollzugriff).

2.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Gruppenrichtlinienverwaltung** , um die GPMC zu öffnen.

3.  Bearbeiten Sie ein Gruppenrichtlinienobjekt, das auf alle Gruppenrichtlinienadministratoren angewendet wird.

4.  Doppelklicken Sie im Fenster **Gruppenrichtlinien-Verwaltungs-Editor** auf **Benutzerkonfiguration**, **Richtlinien**, **Administrative Vorlagen**, **Windows-Komponenten**und **AGPM**.

5.  Doppelklicken Sie im Detailbereich auf **AGPM: standardmäßiger AGPM-Server (alle Domänen) angeben**.

6.  Wählen Sie im **Eigenschaften** Fenster die Option **aktiviert** aus, und geben Sie den DNS-Namen oder die IP-Adresse und den Port (beispielsweise **Server.contoso.com:4600**) für den Server ein, der das Archiv hostet. Standardmäßig verwendet der AGPM-Dienst Port 4600.

7.  Klicken Sie auf **OK**, und schließen Sie dann das Fenster **Gruppenrichtlinien-Verwaltungs-Editor** . Wenn die Gruppenrichtlinie aktualisiert wird, wird die AGPM-Server Verbindung für jeden Gruppenrichtlinienadministrator konfiguriert.

### <a href="" id="bkmk-config4"></a>Schritt 4: Konfigurieren einer e-Mail-Benachrichtigung

Als AGPM-Administrator (Vollzugriff) legen Sie die e-Mail-Adressen von Genehmigern und AGPM-Administratoren fest, denen eine e-Mail-Nachricht mit einer Anforderung gesendet wird, wenn ein Editor versucht, ein GPO zu erstellen, bereitzustellen oder zu löschen. Darüber hinaus ermitteln Sie den Alias, aus dem diese Nachrichten gesendet werden.

**So konfigurieren Sie die e-Mail-Benachrichtigung für AGPM**

1.  Navigieren Sie im **Gruppenrichtlinien-Verwaltungs-Editor** zum Ordner **Change Control** . 

2.  Klicken Sie im Detailbereich auf die Registerkarte **Domänendelegierung** .

3.  Geben Sie im Feld **von e-Mail-Adresse** den e-Mail-Alias für AGPM ein, aus dem Benachrichtigungen gesendet werden sollen.

4.  Geben Sie im Feld **an e-Mail-Adresse** die e-Mail-Adresse für das Benutzerkonto ein, dem Sie die genehmigende Rolle zuweisen möchten.

5.  Geben Sie im Feld **SMTP-Server** einen gültigen SMTP-e-Mail-Server ein.

6.  Geben Sie in den Feldern **Benutzername** und **Kennwort** die Anmeldeinformationen eines Benutzers ein, der auf den SMTP-Dienst zugreifen kann. Klicken Sie auf **Übernehmen**.

### <a href="" id="bkmk-config5"></a>Schritt 5: Delegieren des Zugriffs

Als AGPM-Administrator (Vollzugriff) delegieren Sie den Zugriff auf Gruppenrichtlinienobjekte auf Domänenebene, wobei dem Konto jedes Gruppenrichtlinienadministrators Rollen zugewiesen werden.

**Hinweis**  Sie können den Zugriff auch auf der GPO-Ebene anstelle der Domänenebene delegieren. Weitere Informationen finden Sie unter Hilfe zur erweiterten Gruppenrichtlinienverwaltung.

 

**Wichtig**  Sie sollten die Mitgliedschaft in der Gruppe der Gruppenrichtlinien Ersteller-Besitzer einschränken, damit Sie nicht dazu verwendet werden kann, die AGPM-Verwaltung des Zugriffs auf GPOs zu umgehen. (Klicken Sie in der **Gruppenrichtlinien-Verwaltungskonsole**auf **Gruppenrichtlinienobjekte** in der Gesamtstruktur und Domäne, in der Sie GPOs verwalten möchten, klicken Sie auf **Delegierung**, und konfigurieren Sie dann die Einstellungen, um die Anforderungen Ihrer Organisation zu erfüllen.)

 

**So delegieren Sie den Zugriff auf alle GPOs in einer Domäne**

1.  Klicken Sie auf der Registerkarte **Domänendelegierung** auf die Schaltfläche **Hinzufügen** , wählen Sie das Benutzerkonto des Gruppenrichtlinienadministrators aus, das als genehmigende Person fungieren soll, und klicken Sie dann auf **OK**.

2.  Wählen Sie im Dialogfeld **Gruppe oder Benutzer hinzufügen** die Rolle **genehmigende Person** aus, um diese Rolle dem Konto zuzuweisen, und klicken Sie dann auf **OK**. (Diese Rolle umfasst die Rolle Prüfer.)

3.  Klicken Sie auf die Schaltfläche **Hinzufügen** , wählen Sie das Benutzerkonto des Gruppenrichtlinienadministrators aus, das als Editor fungieren soll, und klicken Sie dann auf **OK**.

4.  Wählen Sie im Dialogfeld **Gruppe oder Benutzer hinzufügen** die **Editor** Rolle aus, um diese Rolle dem Konto zuzuweisen, und klicken Sie dann auf **OK**. (Diese Rolle umfasst die Rolle Prüfer.)

5.  Klicken Sie auf die Schaltfläche **Hinzufügen** , wählen Sie das Benutzerkonto des Gruppenrichtlinienadministrators aus, das als Bearbeiter fungieren soll, und klicken Sie dann auf **OK**.

6.  Wählen Sie im Dialogfeld **Gruppe oder Benutzer hinzufügen** die Rolle **Prüfer** aus, um dem Konto nur diese Rolle zuzuweisen.

## Schritte zum Verwalten von GPOs


Sie müssen die folgenden Schritte ausführen, um GPOs mithilfe von AGPM zu erstellen, zu bearbeiten, zu überprüfen und bereitzustellen. Darüber hinaus erstellen Sie eine Vorlage, löschen ein GPO und Wiederherstellen eines gelöschten Gruppenrichtlinienobjekts.

[Schritt 1: Erstellen eines Gruppenrichtlinienobjekts](#bkmk-manage1)

[Schritt 2: Bearbeiten eines Gruppenrichtlinienobjekts](#bkmk-manage2)

[Schritt 3: überprüfen und Bereitstellen eines Gruppenrichtlinienobjekts](#bkmk-manage3)

[Schritt 4: Verwenden einer Vorlage zum Erstellen eines Gruppenrichtlinienobjekts](#bkmk-manage4)

[Schritt 5: Löschen und Wiederherstellen eines Gruppenrichtlinienobjekts](#bkmk-manage5)

### <a href="" id="bkmk-manage1"></a>Schritt 1: Erstellen eines Gruppenrichtlinienobjekts

In einer Umgebung mit mehreren Gruppenrichtlinienadministratoren können Personen mit der Rolle des Editors anfordern, dass neue GPOs erstellt werden. Diese Anforderung muss jedoch von einer Person mit der Rolle Genehmiger genehmigt werden.

In diesem Schritt verwenden Sie ein Konto mit der Rolle "Bearbeiter", um die Erstellung eines neuen Gruppenrichtlinienobjekts anzufordern. Wenn Sie ein Konto mit der Rolle genehmigende Person verwenden, genehmigen Sie diese Anforderung zum Erstellen des Gruppenrichtlinienobjekts.

**So fordern Sie die Erstellung und Verwaltung eines neuen Gruppenrichtlinienobjekts über AGPM an**

1.  Melden Sie sich auf einem Computer, auf dem Sie AGPM-Client installiert haben, mit einem Benutzerkonto an, dem die Rolle des Editors in AGPM zugewiesen ist.

2.  Klicken Sie in der Struktur der **Gruppenrichtlinien-Verwaltungskonsole** in der Gesamtstruktur und Domäne, in der Sie GPOs verwalten möchten, auf **Steuerelement ändern** .

3.  Klicken Sie mit der rechten Maustaste auf den Knoten **Change Control** , und klicken Sie dann auf **Neues gesteuertes Gruppenrichtlinienobjekt**.

4.  Im Dialogfeld " **Neues gesteuertes GPO** ":

    1.  Wenn Sie eine Kopie der Anfrage erhalten möchten, geben Sie Ihre e-Mail-Adresse in das Feld **CC** ein.

    2.  Geben Sie **eigenes** als Namen für das neue Gruppenrichtlinienobjekt ein.

    3.  Geben Sie einen Kommentar für das neue Gruppenrichtlinienobjekt ein.

    4.  Klicken Sie auf **Live erstellen** , damit das neue Gruppenrichtlinienobjekt unmittelbar nach der Genehmigung in der Produktionsumgebung bereitgestellt wird. Klicken Sie auf **Übermitteln**.

5.  Wenn im Fenster " **AGPM-Status** " angezeigt wird, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. Das neue Gruppenrichtlinienobjekt wird auf der Registerkarte **Ausstehend** angezeigt.

**So genehmigen Sie die ausstehende Anforderung zum Erstellen eines Gruppenrichtlinienobjekts**

1.  Melden Sie sich auf einem Computer, auf dem Sie AGPM-Client installiert haben, mit einem Benutzerkonto an, das die Rolle der genehmigenden Person in AGPM hat.

2.  Öffnen Sie den e-Mail-Posteingang für das Konto, und beachten Sie, dass Sie eine e-Mail-Nachricht vom AGPM-Alias mit der Anforderung des Editors zum Erstellen eines Gruppenrichtlinienobjekts erhalten haben.

3.  Klicken Sie in der Struktur der **Gruppenrichtlinien-Verwaltungskonsole** in der Gesamtstruktur und Domäne, in der Sie GPOs verwalten möchten, auf **Steuerelement ändern** .

4.  Klicken Sie auf der Registerkarte **Inhalt** auf die Registerkarte **Ausstehend** , um die ausstehenden GPOs anzuzeigen.

5.  Klicken Sie mit der rechten Maustaste auf **eigenes**, und klicken Sie dann auf **genehmigen**.

6.  Klicken Sie auf **Ja** , um die Genehmigung zu bestätigen und das Gruppenrichtlinienobjekt auf die Registerkarte **gesteuert** zu verschieben.

### <a href="" id="bkmk-manage2"></a>Schritt 2: Bearbeiten eines Gruppenrichtlinienobjekts

Sie können GPOs verwenden, um Computer-oder Benutzereinstellungen zu konfigurieren und für viele Computer oder Benutzer bereitzustellen. In diesem Schritt verwenden Sie ein Konto mit der Rolle "Bearbeiter", um ein GPO aus dem Archiv auszuchecken, das Gruppenrichtlinienobjekt offline zu bearbeiten, das bearbeitete GPO in das Archiv zu überprüfen und die Bereitstellung des Gruppenrichtlinienobjekts in der Produktionsumgebung anzufordern. In diesem Szenario konfigurieren Sie eine Einstellung im Gruppenrichtlinienobjekt so, dass das Kennwort mindestens acht Zeichen lang sein muss.

**So überprüfen Sie das Gruppenrichtlinienobjekt aus dem Archiv zur Bearbeitung**

1.  Melden Sie sich auf einem Computer, auf dem Sie AGPM-Client installiert haben, mit einem Benutzerkonto an, das die Rolle des Editors in AGPM hat.

2.  Klicken Sie in der Struktur der **Gruppenrichtlinien-Verwaltungskonsole** in der Gesamtstruktur und Domäne, in der Sie GPOs verwalten möchten, auf **Steuerelement ändern** .

3.  Klicken Sie im Detailbereich auf der Registerkarte **Inhalt** auf die Registerkarte **gesteuert** , um die gesteuerten GPOs anzuzeigen.

4.  Klicken Sie mit der rechten Maustaste auf **eigenes**, und klicken Sie dann auf **Auschecken**.

5.  Geben Sie einen Kommentar ein, der im Verlauf des Gruppenrichtlinienobjekts angezeigt werden soll, während es ausgecheckt ist, und klicken Sie dann auf **OK**.

6.  Wenn im Fenster " **AGPM-Status** " angezeigt wird, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. Auf der Registerkarte **gesteuert** wird der Status des Gruppenrichtlinienobjekts als **ausgecheckt**identifiziert.

**So bearbeiten Sie das Gruppenrichtlinienobjekt offline und konfigurieren die minimale Kennwortlänge**

1.  Klicken Sie auf der Registerkarte **gesteuert** mit der rechten Maustaste auf **eigenes**, und klicken Sie dann auf **Bearbeiten** , um das Fenster **Gruppenrichtlinien-Verwaltungs-Editor** zu öffnen und eine Offlinekopie des Gruppenrichtlinienobjekts zu ändern. Konfigurieren Sie in diesem Szenario die minimale Kennwortlänge:

    1.  Doppelklicken Sie unter **Computer Konfiguration**auf **Richtlinien**, **Windows-Einstellungen**, **Sicherheitseinstellungen**, **Kontorichtlinien**und **Kennwortrichtlinien**.

    2.  Doppelklicken Sie im Detailbereich auf **minimale Kennwortlänge**.

    3.  Aktivieren Sie im Eigenschaftenfenster das Kontrollkästchen **diese Richtlinieneinstellung definieren** , legen Sie die Anzahl der Zeichen auf **8**fest, und klicken Sie dann auf **OK**.

2.  Schließen Sie das Fenster **Gruppenrichtlinien-Verwaltungs-Editor** .

**So überprüfen Sie das Gruppenrichtlinienobjekt in das Archiv**

1.  Klicken Sie auf der Registerkarte **gesteuert** mit der rechten Maustaste auf **eigenes** , und klicken Sie dann auf **Einchecken**.

2.  Geben Sie einen Kommentar ein, und klicken Sie dann auf **OK**.

3.  Wenn im Fenster " **AGPM-Status** " angezeigt wird, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. Auf der Registerkarte **gesteuert** wird der Status des Gruppenrichtlinienobjekts als **eingecheckt**gekennzeichnet.

**So fordern Sie die Bereitstellung des Gruppenrichtlinienobjekts in der Produktionsumgebung an**

1.  Klicken Sie auf der Registerkarte **gesteuert** mit der rechten Maustaste auf **eigenes** , und klicken Sie dann auf **Bereitstellen**.

2.  Da es sich bei diesem Konto nicht um eine genehmigende Person oder einen AGPM-Administrator handelt, müssen Sie eine Anforderung für die Bereitstellung einreichen. Wenn Sie eine Kopie der Anfrage erhalten möchten, geben Sie Ihre e-Mail-Adresse in das Feld **CC** ein. Geben Sie einen Kommentar ein, der im Verlauf des Gruppenrichtlinienobjekts angezeigt werden soll, und klicken Sie dann auf **Absenden**.

3.  Wenn im Fenster " **AGPM-Status** " angezeigt wird, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. **Eigenes** wird in der Liste der GPOs auf der Registerkarte **Ausstehend** angezeigt.

### <a href="" id="bkmk-manage3"></a>Schritt 3: überprüfen und Bereitstellen eines Gruppenrichtlinienobjekts

In diesem Schritt fungieren Sie als genehmigende Person, erstellen Berichte und analysieren die Einstellungen und Änderungen an den Einstellungen im Gruppenrichtlinienobjekt, um festzustellen, ob Sie diese genehmigen sollten. Nachdem Sie das Gruppenrichtlinienobjekt ausgewertet haben, müssen Sie es in der Produktionsumgebung bereitstellen und das Gruppenrichtlinienobjekt mit einer Domäne oder einer Organisationseinheit verknüpfen. Das Gruppenrichtlinienobjekt wird wirksam, wenn Gruppenrichtlinien für Computer in dieser Domäne oder OU aktualisiert werden.

**So überprüfen Sie die Einstellungen im Gruppenrichtlinienobjekt**

1. Melden Sie sich auf einem Computer, auf dem Sie AGPM-Client installiert haben, mit einem Benutzerkonto an, dem die Rolle der genehmigenden Person in AGPM zugewiesen ist. Jeder Gruppenrichtlinienadministrator mit der Rolle Prüfer, die in allen anderen Rollen enthalten ist, kann die Einstellungen in einem Gruppenrichtlinienobjekt überprüfen.

2. Öffnen Sie den e-Mail-Posteingang für das Konto, und beachten Sie, dass Sie eine e-Mail-Nachricht vom AGPM-Alias mit der Anforderung eines Editors zum Bereitstellen eines Gruppenrichtlinienobjekts erhalten haben.

3. Klicken Sie in der Struktur der **Gruppenrichtlinien-Verwaltungskonsole** in der Gesamtstruktur und Domäne, in der Sie GPOs verwalten möchten, auf **Steuerelement ändern** .

4. Klicken Sie im Detailbereich auf der Registerkarte **Inhalt** auf die Registerkarte **Ausstehend** .

5. Doppelklicken Sie auf **eigenes** , um dessen Verlauf anzuzeigen.

6. Überprüfen Sie die Einstellungen in der neuesten Version von eigenes:

   1.  Klicken Sie im **Verlaufs** Fenster mit der rechten Maustaste auf die GPO-Version mit dem letzten Zeitstempel, klicken Sie auf **Einstellungen**, und klicken Sie dann auf **HTML-Bericht** , um eine Zusammenfassung der Einstellungen des Gruppenrichtlinienobjekts anzuzeigen.

   2.  Klicken Sie im Webbrowser auf **Alle anzeigen** , um alle Einstellungen im Gruppenrichtlinienobjekt anzuzeigen. Schließen Sie den Browser.

7. Vergleichen Sie die neueste Version von eigenes mit der ersten Version, die in das Archiv eingecheckt wurde:

   1. Klicken Sie im Fenster " **Verlauf** " auf die GPO-Version mit dem letzten Zeitstempel. Drücken Sie STRG, und klicken Sie dann auf die älteste GPO-Version, für die die **Computer Version** nicht * * \ \ * * * ist.

   2. Klicken Sie auf die Schaltfläche **Unterschiede** . Der Abschnitt **Kontorichtlinien/Kennwortrichtlinie** ist grün hervorgehoben und wird mit **\ [+ \]** vorangestellt. Dies zeigt an, dass die Einstellung nur in der letzten Version des Gruppenrichtlinienobjekts konfiguriert ist.

   3. Klicken Sie auf **Kontorichtlinien/Kennwortrichtlinien**. Die Einstellung **minimale Kennwortlänge** ist auch in grün hervorgehoben und mit **\ [+ \]** gekennzeichnet, was darauf hinweist, dass Sie nur in der letzten Version des Gruppenrichtlinienobjekts konfiguriert ist.

   4. Schließen Sie den Webbrowser.

**So stellen Sie das Gruppenrichtlinienobjekt in der Produktionsumgebung bereit**

1.  Klicken Sie auf der Registerkarte **Ausstehend** mit der rechten Maustaste auf **eigenes** , und klicken Sie dann auf **genehmigen**.

2.  Geben Sie einen Kommentar ein, der in das Protokoll des Gruppenrichtlinienobjekts aufgenommen werden soll.

3.  Klicken Sie auf **Ja**. Wenn im Fenster " **AGPM-Status** " angezeigt wird, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. Das Gruppenrichtlinienobjekt wird in der Produktionsumgebung bereitgestellt.

**So verknüpfen Sie das Gruppenrichtlinienobjekt mit einer Domäne oder Organisationseinheit**

1.  Klicken Sie in der GPMC mit der rechten Maustaste entweder auf die Domäne oder auf eine Organisationseinheit, auf die Sie das konfigurierte Gruppenrichtlinienobjekt anwenden möchten, und klicken Sie dann auf **vorhandenes Gruppenrichtlinienobjekt verknüpfen**.

2.  Klicken Sie im Dialogfeld **GPO auswählen** auf **eigenes**, und klicken Sie dann auf **OK**.

### <a href="" id="bkmk-manage4"></a>Schritt 4: Verwenden einer Vorlage zum Erstellen eines Gruppenrichtlinienobjekts

In diesem Schritt verwenden Sie ein Konto, das über die Rolle des Editors verfügt, um eine Vorlage zu erstellen und zu verwenden. Bei dieser Vorlage handelt es sich um eine statische Version eines GPO, die als Ausgangspunkt zum Erstellen neuer GPOs verwendet werden kann. Obwohl Sie eine Vorlage nicht bearbeiten können, können Sie ein neues Gruppenrichtlinienobjekt basierend auf einer Vorlage erstellen. Vorlagen sind hilfreich für das schnelle Erstellen mehrerer GPOs, in denen viele der gleichen Richtlinieneinstellungen enthalten sind.

**So erstellen Sie eine Vorlage auf der Grundlage eines vorhandenen Gruppenrichtlinienobjekts**

1.  Melden Sie sich auf einem Computer, auf dem Sie AGPM-Client installiert haben, mit einem Benutzerkonto an, dem die Rolle des Editors in AGPM zugewiesen ist.

2.  Klicken Sie in der Struktur der **Gruppenrichtlinien-Verwaltungskonsole** in der Gesamtstruktur und Domäne, in der Sie GPOs verwalten möchten, auf **Steuerelement ändern** .

3.  Klicken Sie im Detailbereich auf der Registerkarte **Inhalt** auf die Registerkarte **gesteuert** .

4.  Klicken Sie mit der rechten Maustaste auf **eigenes**, und klicken Sie dann auf **als Vorlage speichern** , um eine Vorlage zu erstellen, die alle Einstellungen umfasst, die derzeit in eigenes enthalten sind.

5.  Geben Sie **MyTemplate** als Namen für die Vorlage und einen Kommentar ein, und klicken Sie dann auf **OK**.

6.  Wenn im Fenster " **AGPM-Status** " angezeigt wird, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. Die neue Vorlage wird auf der Registerkarte **Vorlagen** angezeigt.

**So fordern Sie die Erstellung und Verwaltung eines neuen Gruppenrichtlinienobjekts über AGPM an**

1.  Klicken Sie auf die Registerkarte **gesteuert** .

2.  Klicken Sie mit der rechten Maustaste auf den Knoten **Change Control** , und klicken Sie dann auf **Neues gesteuertes Gruppenrichtlinienobjekt**.

3.  Im Dialogfeld " **Neues gesteuertes GPO** ":

    1.  Wenn Sie eine Kopie der Anfrage erhalten möchten, geben Sie Ihre e-Mail-Adresse in das Feld **CC** ein.

    2.  Geben Sie **Gruppenrichtlinienverwaltungs** als Namen für das neue Gruppenrichtlinienobjekt ein.

    3.  Geben Sie einen Kommentar für das neue Gruppenrichtlinienobjekt ein.

    4.  Klicken Sie auf **Live erstellen** , damit das neue Gruppenrichtlinienobjekt unmittelbar nach der Genehmigung in der Produktionsumgebung bereitgestellt wird.

    5.  Wählen Sie für **aus GPO-Vorlage**die Option meine **Vorlage**aus. Klicken Sie auf **Übermitteln**.

4.  Wenn im Fenster " **AGPM-Status** " angezeigt wird, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. Das neue Gruppenrichtlinienobjekt wird auf der Registerkarte **Ausstehend** angezeigt.

Verwenden Sie ein Konto, dem die Rolle der genehmigenden Person zugewiesen ist, um die ausstehende Anforderung zum Erstellen des Gruppenrichtlinienobjekts zu genehmigen, wie in [Schritt 1: Erstellen eines Gruppenrichtlinienobjekts](#bkmk-manage1). MyTemplate enthält alle Einstellungen, die Sie in eigenes konfiguriert haben. Da Gruppenrichtlinienverwaltungs mit MyTemplate erstellt wurde, enthält es zunächst alle Einstellungen, die eigenes zum Zeitpunkt der Erstellung von MyTemplate enthielt. Sie können dies bestätigen, indem Sie einen Differenz Bericht generieren, um Gruppenrichtlinienverwaltungs mit MyTemplate zu vergleichen.

**So überprüfen Sie das Gruppenrichtlinienobjekt aus dem Archiv zur Bearbeitung**

1.  Melden Sie sich auf einem Computer, auf dem Sie AGPM-Client installiert haben, mit einem Benutzerkonto an, dem die Rolle des Editors in AGPM zugewiesen ist.

2.  Klicken Sie mit der rechten Maustaste auf **Gruppenrichtlinienverwaltungs**, und klicken Sie dann auf **Auschecken**.

3.  Geben Sie einen Kommentar ein, der im Verlauf des Gruppenrichtlinienobjekts angezeigt werden soll, während es ausgecheckt ist, und klicken Sie dann auf **OK**.

4.  Wenn im Fenster " **AGPM-Status** " angezeigt wird, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. Auf der Registerkarte **gesteuert** wird der Status des Gruppenrichtlinienobjekts als **ausgecheckt**identifiziert.

**So bearbeiten Sie das Gruppenrichtlinienobjekt offline und konfigurieren die Kontosperrungsdauer**

1.  Klicken Sie auf der Registerkarte **gesteuert** mit der rechten Maustaste auf **Gruppenrichtlinienverwaltungs**, und klicken Sie dann auf **Bearbeiten** , um das Fenster **Gruppenrichtlinien-Verwaltungs-Editor** zu öffnen und eine Offlinekopie des Gruppenrichtlinienobjekts zu ändern. Konfigurieren Sie in diesem Szenario die minimale Kennwortlänge:

    1.  Doppelklicken Sie unter **Computer Konfiguration**auf **Richtlinien**, **Windows-Einstellungen**, **Sicherheitseinstellungen**, **Kontorichtlinien**und **Kontosperrungsrichtlinien**.

    2.  Doppelklicken Sie im Detailbereich auf **Kontosperrungsdauer**.

    3.  Aktivieren Sie im Fenster Eigenschaften die Option **diese Richtlinieneinstellung definieren**, legen Sie die Dauer auf **30** Minuten fest, und klicken Sie dann auf **OK**.

2.  Schließen Sie das Fenster **Gruppenrichtlinien-Verwaltungs-Editor** .

Überprüfen Sie Gruppenrichtlinienverwaltungs in die Archivierungs-und Anforderungs Bereitstellung wie bei eigenes in [Schritt 2: Bearbeiten eines Gruppenrichtlinienobjekts](#bkmk-manage2). Sie können Gruppenrichtlinienverwaltungs mit eigenes oder mit MyTemplate vergleichen, indem Sie Differenz Berichte verwenden. Jedes Konto, das die Rolle Prüfer enthält (AGPM-Administrator \ [Vollzugriff \], genehmigende Person, Bearbeiter oder Bearbeiter) kann Berichte generieren.

**So vergleichen Sie ein GPO mit einem anderen Gruppenrichtlinienobjekt und einer Vorlage**

1.  So vergleichen Sie eigenes und Gruppenrichtlinienverwaltungs:

    1.  Klicken Sie auf der Registerkarte **gesteuert** auf **eigenes**. Drücken Sie STRG, und klicken Sie dann auf **Gruppenrichtlinienverwaltungs**.

    2.  Klicken Sie mit der rechten Maustaste auf **Gruppenrichtlinienverwaltungs**, zeigen Sie auf **Unterschiede**, und klicken Sie dann auf **HTML-Bericht**.

2.  So vergleichen Sie Gruppenrichtlinienverwaltungs und MyTemplate:

    1.  Klicken Sie auf der Registerkarte **gesteuert** auf **Gruppenrichtlinienverwaltungs**.

    2.  Klicken Sie mit der rechten Maustaste auf **Gruppenrichtlinienverwaltungs**, zeigen Sie auf **Unterschiede**, und klicken Sie dann auf **Vorlage**.

    3.  Wählen Sie **MyTemplate** und **HTML-Bericht**aus, und klicken Sie dann auf **OK**.

### <a href="" id="bkmk-manage5"></a>Schritt 5: Löschen und Wiederherstellen eines Gruppenrichtlinienobjekts

In diesem Schritt fungieren Sie als genehmigende Person, um ein GPO zu löschen.

**So löschen Sie ein Gruppenrichtlinienobjekt**

1.  Melden Sie sich auf einem Computer, auf dem Sie AGPM-Client installiert haben, mit einem Benutzerkonto an, dem die Rolle der genehmigenden Person zugewiesen ist.

2.  Klicken Sie in der Struktur der **Gruppenrichtlinien-Verwaltungskonsole** in der Gesamtstruktur und Domäne, in der Sie GPOs verwalten möchten, auf **Steuerelement ändern** .

3.  Klicken Sie auf der Registerkarte **Inhalt** auf die Registerkarte **gesteuert** , um die gesteuerten GPOs anzuzeigen.

4.  Klicken Sie mit der rechten Maustaste auf **eigenes**, und klicken Sie dann auf **Löschen**. Klicken Sie auf **Gruppenrichtlinienobjekt aus Archiv und Produktion löschen** , um sowohl die Version im Archiv als auch die bereitgestellte Version des Gruppenrichtlinienobjekts in der Produktionsumgebung zu löschen.

5.  Geben Sie einen Kommentar ein, der im Überwachungspfad für das Gruppenrichtlinienobjekt angezeigt werden soll, und klicken Sie dann auf **OK**.

6.  Wenn im Fenster " **AGPM-Status** " angezeigt wird, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. Das Gruppenrichtlinienobjekt wird von der Registerkarte " **gesteuert** " entfernt und auf der Registerkarte " **Papierkorb** " angezeigt, wo es wiederhergestellt oder gelöscht werden kann.

Gelegentlich können Sie feststellen, dass Sie nach dem Löschen eines Gruppenrichtlinienobjekts nach wie vor benötigt werden. In diesem Schritt fungieren Sie als genehmigende Person zum Wiederherstellen eines gelöschten Gruppenrichtlinienobjekts.

**So stellen Sie ein gelöschtes Gruppenrichtlinienobjekt wieder her**

1.  Klicken Sie auf der Registerkarte **Inhalt** auf die Registerkarte **Papierkorb** , um gelöschte GPOs anzuzeigen.

2.  Klicken Sie mit der rechten Maustaste auf **eigenes**, und klicken Sie dann auf **Wiederherstellen**.

3.  Geben Sie einen Kommentar ein, der im Verlauf des Gruppenrichtlinienobjekts angezeigt werden soll, und klicken Sie dann auf **OK**.

4.  Wenn im Fenster " **AGPM-Status** " angezeigt wird, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. Das Gruppenrichtlinienobjekt wird von der Registerkarte " **Papierkorb** " entfernt und auf der Registerkarte " **gesteuert** " angezeigt.

    **Hinweis**  Wenn Sie ein GPO im Archiv wiederherstellen, wird es nicht automatisch in der Produktionsumgebung bereitgestellt. Wenn Sie das Gruppenrichtlinienobjekt an die Produktionsumgebung zurückgeben möchten, stellen Sie das Gruppenrichtlinienobjekt wie in [Schritt 3: überprüfen und Bereitstellen eines Gruppenrichtlinien](#bkmk-manage3)Objekts bereit.

     

Nachdem Sie ein GPO bearbeitet und bereitgestellt haben, stellen Sie möglicherweise fest, dass die letzten Änderungen am Gruppenrichtlinienobjekt ein Problem verursachen. In diesem Schritt fungieren Sie als genehmigende Person, um einen Rollback zu einer früheren Version des Gruppenrichtlinienobjekts durchführen zu können. Sie können einen Rollback zu einer beliebigen Version im Verlauf des Gruppenrichtlinienobjekts ausführen. Sie können Kommentare und Beschriftungen verwenden, um bekannte gute Versionen zu identifizieren und wenn bestimmte Änderungen vorgenommen wurden.

**So führen Sie einen Rollback zu einer früheren Version eines GPO durch**

1.  Klicken Sie auf der Registerkarte **Inhalt** auf die Registerkarte **gesteuert** , um die gesteuerten GPOs anzuzeigen.

2.  Doppelklicken Sie auf **eigenes** , um dessen Verlauf anzuzeigen.

3.  Klicken Sie mit der rechten Maustaste auf die bereit **zustellende**Version, klicken Sie auf bereitstellen, und klicken Sie dann auf **Ja**.

4.  Wenn das **Status** Fenster angibt, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. Klicken Sie im Fenster **Verlauf** auf **Schließen**.

    **Hinweis**  Um zu überprüfen, ob die Version, die erneut bereitgestellt wurde, die beabsichtigte Version ist, untersuchen Sie einen Unterschiedsbericht für die beiden Versionen. Wählen Sie im Fenster **Verlauf** für das Gruppenrichtlinienobjekt die beiden Versionen aus, klicken Sie mit der rechten Maustaste darauf, zeigen Sie auf **Differenz**, und klicken Sie dann auf **HTML-Bericht** oder **XML-Bericht**.

     

 

 





