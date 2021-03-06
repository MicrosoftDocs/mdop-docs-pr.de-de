---
title: Schrittweise Anleitung für Microsoft Advanced Group Policy Management 2.5
description: Schrittweise Anleitung für Microsoft Advanced Group Policy Management 2.5
author: dansimp
ms.assetid: 454298c9-0fab-497a-9808-c0246a4c8db5
ms.reviewer: ''
manager: dansimp
ms.author: dansimp
ms.pagetype: mdop
ms.mktglfcycl: manage
ms.sitesec: library
ms.prod: w10
ms.date: 08/30/2016
ms.openlocfilehash: 67925e417e4fb1f5398dfd030f366936f1d36909
ms.sourcegitcommit: 354664bc527d93f80687cd2eba70d1eea024c7c3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/26/2020
ms.locfileid: "10808208"
---
# Schrittweise Anleitung für Microsoft Advanced Group Policy Management 2.5


Diese Schritt-für-Schritt-Anleitung zeigt erweiterte Techniken für die Gruppenrichtlinienverwaltung mithilfe der Gruppenrichtlinien-Verwaltungskonsole (Group Policy Management Console, GPMC) und Microsoft Advanced Group Policy Management (AGPM). AGPM vergrößert die Funktionen der GPMC und bietet Folgendes:

-   Standard Rollen für das Delegieren von Berechtigungen zum Verwalten von Gruppenrichtlinienobjekten (GPOs) an mehrere Gruppenrichtlinienadministratoren.

-   Ein Archiv, damit Gruppenrichtlinienadministratoren GPOs offline erstellen und ändern können, bevor Sie in einer Produktionsumgebung bereitgestellt werden.

-   Die Möglichkeit, einen Rollback zu einer beliebigen vorherigen Version eines GPO durchführen zu können.

-   Möglichkeit zum ein-und Auschecken von GPOs, um sicherzustellen, dass Gruppenrichtlinienadministratoren die Arbeit des anderen nicht versehentlich überschreiben.

## Übersicht über AGPM-Szenarien


In diesem Szenario verwenden Sie für jede Rolle in AGPM ein separates Benutzerkonto, um zu veranschaulichen, wie Gruppenrichtlinien in einer Umgebung mit mehreren Gruppenrichtlinienadministratoren verwaltet werden können, die unterschiedliche Berechtigungsstufen aufweisen. Insbesondere führen Sie die folgenden Aufgaben aus:

-   Wenn Sie ein Konto verwenden, das Mitglied der Gruppe der Domänenadministratoren ist, installieren Sie AGPM Server, und weisen Sie die Rolle AGPM-Administrator einem Konto oder einer Gruppe zu.

-   Installieren Sie AGPM-Client mithilfe von Konten, denen Sie AGPM-Rollen zuweisen.

-   Wenn Sie ein Konto mit der Rolle AGPM-Administrator verwenden, konfigurieren Sie AGPM, und delegieren Sie den Zugriff auf GPOs, indem Sie anderen Konten Rollen zuweisen.

-   Wenn Sie ein Konto mit der Rolle des Editors verwenden, fordern Sie die Erstellung eines Gruppenrichtlinienobjekts an, das Sie dann mit einem Konto mit der Rolle genehmigende Person genehmigen. Überprüfen Sie mit dem Editor-Konto das Gruppenrichtlinienobjekt aus dem Archiv, bearbeiten Sie das Gruppenrichtlinienobjekt, überprüfen Sie das Gruppenrichtlinienobjekt in das Archiv, und fordern Sie die Bereitstellung an.

-   Überprüfen Sie das Gruppenrichtlinienobjekt, und stellen Sie es in Ihrer Produktionsumgebung bereit, indem Sie ein Konto mit der Rolle genehmigende Person verwenden.

-   Erstellen Sie mithilfe eines Kontos mit der Rolle "Editor" eine GPO-Vorlage, und verwenden Sie Sie als Ausgangspunkt zum Erstellen eines neuen Gruppenrichtlinienobjekts.

-   Wenn Sie ein Konto mit der Rolle genehmigende Person verwenden, löschen Sie ein GPO, und stellen Sie es wieder her.

![Entwicklungsprozess für Gruppenrichtlinienobjekte](images/ab77a1f3-f430-4e7d-be58-ee8f9bd1140e.gif)

## Anforderungen


Computer, auf denen Sie AGPM installieren möchten, müssen die folgenden Anforderungen erfüllen, und Sie müssen Konten erstellen, die in diesem Szenario verwendet werden können.

### AGPM-Server Anforderungen

AGPM Server 2.5 erfordert Windows Vista® (32-Bit-Version) ohne installierte Service Packs oder Windows Server® 2003 (32-Bit-Version) sowie die GPMC. Darüber hinaus müssen Sie ein Mitglied der Gruppe der Domänenadministratoren sein, um AGPM Server installieren zu können.

Sie sollten AGPM Server auf einem Mitglieds Server oder Domänencontroller mit der neuesten Version der GPMC installieren, die für Sie verfügbar ist und von AGPM unterstützt wird. AGPM verwendet die GPMC zum Sichern und Wiederherstellen von GPOs, und neuere Versionen der GPMC bieten zusätzliche Richtlinieneinstellungen, die in früheren Versionen nicht verfügbar sind. Wenn die Version der GPMC auf dem AGPM-Server älter als die Version auf den Computern ist, die von Administratoren zum Verwalten von Gruppenrichtlinien verwendet werden, kann der AGPM-Server diese Richtlinieneinstellungen nicht speichern, die in der älteren Version der GPMC nicht verfügbar sind.

Insbesondere können Sie die meisten Richtlinieneinstellungen weiterhin verwalten, wenn auf dem AGPM-Server Windows Server2003 ausgeführt wird und die Version der GPMC, die Sie begleitet hat, und die Computer der Gruppenrichtlinienadministratoren Windows Vista und die Version der GPMC, die Sie begleitet hat, ausgeführt werden. Richtlinieneinstellungen aus der GPMC in Windows Vista, die nicht in der GPMC in Windows Server 2003 verfügbar sind, beispielsweise in Bezug auf Ordnerumleitung, Drahtlosnetzwerke (IEEE 802,11) und bereitgestellte Drucker, können vom AGPM-Server nicht gespeichert werden, obwohl Administratoren Sie mithilfe von AGPM auf ihren Computern konfigurieren können.

Wenn Sie AGPM Server auf einem Computer mit einer älteren Version von GPMC installieren müssen, als die Gruppenrichtlinienadministratoren ausgeführt werden, finden Sie Informationen dazu, welche Richtlinieneinstellungen für welche Betriebssysteme verfügbar sind. Informationen zum Herunterladen der Gruppenrichtlinien Einstellungsreferenz finden Sie unter <https://go.microsoft.com/fwlink/?LinkID=106147> .

**Hinweis**  Archive können nicht von einem AGPM-Server oder einem GPOVault-Server mit Windows Server2003 zu einem AGPM-Server migriert werden, auf dem Windows Vista ausgeführt wird.

Wenn GPOVault Server auf dem Computer installiert ist, auf dem Sie AGPM Server installieren möchten, empfiehlt es sich für Windows Server2003, GPOVault Server vor Beginn der Installation nicht zu deinstallieren. Die Installation von AGPM Server wird GPOVault Server deinstallieren und Ihre vorhandenen GPOVault-Archivdaten automatisch in ein AGPM-Archiv übertragen.

 

### AGPM-Client Anforderungen

AGPM Client 2.5 erfordert Windows Vista (32-Bit-Version) ohne installierte Service Packs oder Windows Server2003 (32-Bit-Version) sowie die GPMC. AGPM-Client kann auf einem Computer mit AGPM Server installiert werden.

### Voraussetzungen für Szenarien

Bevor Sie mit diesem Szenario beginnen, erstellen Sie vier Benutzerkonten. Während des Szenarios weisen Sie jedem dieser Konten eine der folgenden AGPM-Rollen zu: AGPM-Administrator (Vollzugriff), genehmigende Person, Editor und Bearbeiter. Diese Konten müssen in der Lage sein, e-Mail-Nachrichten zu senden und zu empfangen. Weisen Sie den Konten mit den Rollen des AGPM-Administrators, genehmigenden und (optional)-Editors die Berechtigung " **Link-GPOs** " zu.

**Hinweis** 
 Die Berechtigung " **GPOs verknüpfen** " wird standardmäßig Mitgliedern von Domänenadministratoren und Unternehmensadministratoren zugewiesen. Klicken Sie auf den Knoten für die Domäne, und klicken Sie dann auf die Registerkarte **Delegierung** , wählen Sie **GPOs verknüpfen**aus, klicken Sie auf **Hinzufügen**, und wählen Sie dann Benutzer oder Gruppen aus, denen die Berechtigung zugewiesen werden soll, wenn Sie zusätzlichen Benutzern oder Gruppen die Berechtigung zum **Verknüpfen von GPOs** zuweisen möchten (beispielsweise Konten mit den Rollen AGPM-Administrator oder genehmigende Person).

 

In diesem Szenario führen Sie Aktionen mit unterschiedlichen Konten aus. Sie können sich entweder mit jedem Konto wie angegeben anmelden, oder Sie können den Befehl **Ausführen als** verwenden, um die GPMC mit dem angegebenen Konto zu starten.

**Hinweis**  Wenn Sie den Befehl **Ausführen als** in der GPMC unter Windows Server2003 verwenden möchten, klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, klicken Sie mit der rechten Maustaste auf **Gruppenrichtlinienverwaltung**, und klicken Sie dann auf **Ausführen als**. Klicken Sie auf **den folgenden Benutzer** , und geben Sie die Anmeldeinformationen für ein Konto ein.

Wenn Sie den Befehl **Ausführen als** in der GPMC unter Windows Vista verwenden möchten, klicken Sie auf die Schaltfläche **Start** , zeigen Sie auf **Ausführen**, und geben Sie **runas/User:** <em> DomainName\\UserName </em> **"MMC%windir%\\system32\\gpmc.msc"** ein, und klicken Sie auf **OK**. Geben Sie das Kennwort für das Konto ein, wenn Sie dazu aufgefordert werden.

 

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

4.  Akzeptieren Sie im Dialogfeld **Microsoft-Software-Lizenzbestimmungen** die Begriffe, und klicken Sie auf **weiter**.

5.  Wählen Sie im Dialogfeld **Anwendungspfad** einen Speicherort aus, an dem AGPM Server installiert werden soll. Auf dem Computer, auf dem AGPM Server installiert ist, wird der AGPM-Dienst gehostet und das Archiv verwaltet. Klicken Sie auf **Weiter**.

6.  Wählen Sie im Dialogfeld **Archivpfad** einen Speicherort für das Archiv relativ zum AGPM-Server aus. Der Archivpfad kann auf einen Ordner auf dem AGPM-Server oder an anderer Stelle verweisen, Sie sollten jedoch einen Speicherort mit genügend Speicherplatz zum Speichern aller GPOs und Verlaufsdaten auswählen, die von diesem AGPM-Server verwaltet werden. Klicken Sie auf **Weiter**.

7.  Wählen Sie im Dialogfeld **AGPM-Dienstkonto** ein Dienstkonto aus, unter dem der AGPM-Dienst ausgeführt wird, und klicken Sie dann auf **weiter**.

8.  Wählen Sie im Dialogfeld **Besitzer des Archivs** ein Konto oder eine Gruppe aus, dem Sie zunächst die Rolle AGPM-Administrator (Vollzugriff) zuweisen möchten. Dieser AGPM-Administrator kann anderen Gruppenrichtlinienadministratoren AGPM-Rollen und-Berechtigungen zuweisen (einschließlich der Rolle des AGPM-Administrators). Wählen Sie in diesem Szenario das Konto aus, das in der Rolle des AGPM-Administrators dienen soll. Klicken Sie auf **Weiter**.

9.  Klicken Sie auf **Installieren**, und klicken Sie dann auf **Fertig stellen** , um den Setup-Assistenten zu beenden.

    **Vorsicht**  Ändern Sie die Einstellungen für den AGPM-Dienst nicht über **Administrative Tools** und **Dienste** im Betriebssystem. Dadurch kann der Start des AGPM-Diensts verhindert werden. Informationen zum Ändern der Einstellungen für den Dienst finden Sie unter Hilfe zur erweiterten Gruppenrichtlinienverwaltung.

     

### <a href="" id="bkmk-config2"></a>Schritt 2: Installieren des AGPM-Clients

Jeder Gruppenrichtlinienadministrator – jeder, der GPOs erstellt, bearbeitet, bereitstellt, überprüft oder löscht, muss AGPM-Client auf Computern installiert haben, die Sie zum Verwalten von GPOs verwenden. In diesem Szenario installieren Sie AGPM-Client auf mindestens einem Computer. Sie müssen den AGPM-Client nicht auf den Computern von Endbenutzern installieren, die keine Gruppenrichtlinienverwaltung durchführen.

**So installieren Sie den AGPM-Client auf dem Computer eines Gruppenrichtlinienadministrators**

1.  Starten Sie die Microsoft Desktop Optimization Pack-CD, und folgen Sie den Anweisungen auf dem Bildschirm, um **Erweiterte Gruppenrichtlinienverwaltung-Client**auszuwählen.

2.  Klicken Sie im Dialogfeld **Willkommen** auf **weiter**.

3.  Akzeptieren Sie im Dialogfeld **Microsoft-Software-Lizenzbestimmungen** die Begriffe, und klicken Sie auf **weiter**.

4.  Wählen Sie im Dialogfeld **Anwendungspfad** einen Speicherort aus, an dem AGPM-Client installiert werden soll. Klicken Sie auf **Weiter**.

5.  Geben Sie im Dialogfeld **AGPM-Server** den vollqualifizierten Computernamen und den Port für den AGPM-Server ein, mit dem die Verbindung hergestellt werden soll. Der Standardport für den AGPM-Dienst ist 4600. Klicken Sie auf **Weiter**.

6.  Klicken Sie auf **Installieren**, und klicken Sie dann auf **Fertig stellen** , um den Setup-Assistenten zu beenden.

### <a href="" id="bkmk-config3"></a>Schritt 3: Konfigurieren einer AGPM-Server Verbindung

AGPM speichert alle Versionen der einzelnen gesteuerten Gruppenrichtlinienobjekte (GPO) – ein GPO, für das AGPM das Änderungs Steuerelement bereitstellt – in einem zentralen Archiv, sodass Gruppenrichtlinienadministratoren GPOs offline anzeigen und ändern können, ohne dass sich dies unmittelbar auf die bereitgestellte Version jedes GPO auswirkt.

In diesem Schritt konfigurieren Sie eine AGPM-Serververbindung und stellen sicher, dass alle Gruppenrichtlinienadministratoren eine Verbindung mit dem gleichen AGPM-Server herstellen. (Informationen zum Konfigurieren mehrerer AGPM-Server finden Sie unter Hilfe zur erweiterten Gruppenrichtlinienverwaltung.)

**So konfigurieren Sie eine AGPM-Server Verbindung für alle Gruppenrichtlinienadministratoren**

1.  Melden Sie sich auf einem Computer, auf dem Sie AGPM-Client installiert haben, mit dem Benutzerkonto an, das Sie als Archiv Besitzer ausgewählt haben. Dieser Benutzer hat die Rolle des AGPM-Administrators (Vollzugriff).

2.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie auf **Gruppenrichtlinienverwaltung** , um die **Gruppenrichtlinien-Verwaltungskonsole (Group Policy Management Console, GPMC)** zu öffnen.

3.  Bearbeiten Sie in der **Gruppenrichtlinien-Verwaltungskonsolen** Struktur ein GPO, das auf alle Gruppenrichtlinienadministratoren angewendet wird.

4.  Klicken Sie im **Gruppenrichtlinienobjekt-Editor** -Fenster auf **Benutzerkonfiguration**, **Administrative Vorlagen**und **Windows-Komponenten**.

5.  Wenn **AGPM** nicht unter Windows- **Komponenten**aufgeführt ist:

    1.  Klicken Sie mit der rechten Maustaste auf **Administrative Vorlagen** , und wählen Sie **Vorlagen hinzufügen/entfernen**aus.

    2.  Klicken Sie auf **Hinzufügen**, wählen Sie **AGPM. ADMX** oder **AGPM. adm**aus, klicken Sie auf **Öffnen**und dann auf **Schließen**.

6.  Doppelklicken Sie unter **Windows-Komponenten**auf **AGPM**.

7.  Doppelklicken Sie im Detailbereich auf **AGPM-Server (alle Domänen)**.

8.  Wählen Sie im **Eigenschaftenfenster AGPM-Server (alle Domänen)** die Option **aktiviert** aus, und geben Sie den vollqualifizierten Computernamen und-Port (beispielsweise Server.contoso.com:4600) für den Server ein, der das Archiv hostet. Der vom AGPM-Dienst verwendete Port ist Port 4600.

9.  Klicken Sie auf **OK**, und schließen Sie dann das **Gruppenrichtlinienobjekt-Editor-** Fenster. Wenn die Gruppenrichtlinie aktualisiert wird, wird die AGPM-Server Verbindung für jeden Gruppenrichtlinienadministrator konfiguriert.

### <a href="" id="bkmk-config4"></a>Schritt 4: Konfigurieren einer e-Mail-Benachrichtigung

Als AGPM-Administrator (Vollzugriff) legen Sie die e-Mail-Adressen von Genehmigern und AGPM-Administratoren fest, denen eine e-Mail-Nachricht mit einer Anforderung gesendet wird, wenn ein Editor versucht, ein GPO zu erstellen, bereitzustellen oder zu löschen. Darüber hinaus ermitteln Sie den Alias, aus dem diese Nachrichten gesendet werden.

**So konfigurieren Sie die e-Mail-Benachrichtigung für AGPM**

1.  Klicken Sie in der Struktur der **Gruppenrichtlinien-Verwaltungskonsole** in der Gesamtstruktur und Domäne, in der Sie GPOs verwalten möchten, auf **Steuerelement ändern** .

2.  Klicken Sie im Detailbereich auf die Registerkarte **Domänendelegierung** .

3.  Geben Sie im Feld **von** den e-Mail-Alias für AGPM ein, aus dem Benachrichtigungen gesendet werden sollen.

4.  Geben Sie im Feld **an** die e-Mail-Adresse für das Benutzerkonto ein, dem Sie die genehmigende Rolle zuweisen möchten.

5.  Geben Sie im Feld **SMTP-Server** einen gültigen SMTP-e-Mail-Server ein.

6.  Geben Sie in den Feldern **Benutzername** und **Kennwort** die Anmeldeinformationen eines Benutzers mit Zugriff auf den SMTP-Dienst ein.

7.  Klicken Sie auf **Übernehmen**.

### <a href="" id="bkmk-config5"></a>Schritt 5: Delegieren des Zugriffs

Als AGPM-Administrator (Vollzugriff) delegieren Sie den Zugriff auf Gruppenrichtlinienobjekte auf Domänenebene, wobei dem Konto jedes Gruppenrichtlinienadministrators Rollen zugewiesen werden.

**Hinweis**  Sie können den Zugriff auch auf der GPO-Ebene und nicht auf der Domänenebene delegieren. Ausführliche Informationen finden Sie unter Hilfe zur erweiterten Gruppenrichtlinienverwaltung.

 

**Wichtig**  Sie sollten die Mitgliedschaft in der Gruppe der Gruppenrichtlinien Ersteller-Besitzer einschränken, damit Sie nicht dazu verwendet werden kann, die AGPM-Verwaltung des Zugriffs auf GPOs zu umgehen. (Klicken Sie in der **Gruppenrichtlinien-Verwaltungskonsole**auf **Gruppenrichtlinienobjekte** in der Gesamtstruktur und Domäne, in der Sie GPOs verwalten möchten, klicken Sie auf **Delegierung**, und konfigurieren Sie dann die Einstellungen, um die Anforderungen Ihrer Organisation zu erfüllen.)

 

**So delegieren Sie den Zugriff auf alle GPOs in einer Domäne**

1.  Klicken Sie in der Struktur der **Gruppenrichtlinien-Verwaltungskonsole** in der Gesamtstruktur und Domäne, in der Sie GPOs verwalten möchten, auf **Steuerelement ändern** .

2.  Klicken Sie auf der Registerkarte **Domänendelegierung** auf die Schaltfläche **erweitert** .

3.  Im Dialogfeld " **Berechtigungen** ":

    1.  Klicken Sie auf das Benutzerkonto eines Gruppenrichtlinienadministrators, und aktivieren Sie dann das Kontrollkästchen **Genehmiger** , um diese Rolle dem Konto zuzuweisen. Deaktivieren Sie das Kontrollkästchen **Editor** . (Diese Rolle umfasst die Rolle Prüfer.)

    2.  Klicken Sie auf das Benutzerkonto eines anderen Gruppenrichtlinienadministrators, und aktivieren Sie dann das Kontrollkästchen **Editor** , um diese Rolle dem Konto zuzuweisen. (Diese Rolle umfasst die Rolle Prüfer.)

    3.  Klicken Sie auf ein drittes Konto, und aktivieren Sie dann **das Kontrollkästchen Prüfer,** um dem Konto dieses Gruppenrichtlinienadministrators nur die Rolle Prüfer zuzuweisen. Deaktivieren Sie das Kontrollkästchen **Editor** .

    4.  Klicken Sie auf die Schaltfläche **erweitert** .

4.  Im Dialogfeld " **Erweiterte Sicherheitseinstellungen** ":

    1.  Wählen Sie einen Gruppenrichtlinienadministrator aus, und klicken Sie dann auf **Bearbeiten**.

    2.  Wählen Sie für **anwenden auf**die Option **dieses Objekt und verschachtelte Objekte**aus, und klicken Sie dann im Dialogfeld **Berechtigungs** **Eintrag** auf **OK** .

    3.  Wiederholen Sie diesen Vorgang für jeden Gruppenrichtlinienadministrator.

5.  Klicken Sie im Dialogfeld **Erweiterte Sicherheitseinstellungen** auf **OK**.

6.  Klicken Sie im Dialogfeld **Berechtigungen** auf **OK**.

## Schritte zum Verwalten von GPOs


Sie müssen die folgenden Schritte ausführen, um GPOs mithilfe von AGPM zu erstellen, zu bearbeiten, zu überprüfen und bereitzustellen. Darüber hinaus erstellen Sie eine Vorlage, löschen ein GPO und Wiederherstellen eines gelöschten Gruppenrichtlinienobjekts.

[Schritt 1: Erstellen eines Gruppenrichtlinienobjekts](#bkmk-manage1)

[Schritt 2: Bearbeiten eines Gruppenrichtlinienobjekts](#bkmk-manage2)

[Schritt 3: überprüfen und Bereitstellen eines Gruppenrichtlinienobjekts](#bkmk-manage3)

[Schritt 4: Verwenden einer Vorlage zum Erstellen eines Gruppenrichtlinienobjekts](#bkmk-manage4)

[Schritt 5: Löschen und Wiederherstellen eines Gruppenrichtlinienobjekts](#bkmk-manage5)

### <a href="" id="bkmk-manage1"></a>Schritt 1: Erstellen eines Gruppenrichtlinienobjekts

In einer Umgebung mit mehreren Gruppenrichtlinienadministratoren können Personen, die die Rolle des Editors besitzen, die Erstellung neuer GPOs anfordern, doch eine solche Anforderung muss von einer Person mit der Rolle Genehmiger genehmigt werden, da sich die Erstellung eines neuen Gruppenrichtlinienobjekts auf die Produktionsumgebung auswirkt.

In diesem Schritt verwenden Sie ein Konto mit der Rolle "Editor", um die Erstellung eines neuen Gruppenrichtlinienobjekts anzufordern. Wenn Sie ein Konto mit der Rolle Genehmiger verwenden, genehmigen Sie diese Anforderung und schließen die Erstellung eines Gruppenrichtlinienobjekts ab.

**So fordern Sie die Erstellung eines über AGPM verwalteten neuen Gruppenrichtlinienobjekts an**

1.  Melden Sie sich auf einem Computer, auf dem Sie AGPM-Client installiert haben, mit einem Benutzerkonto an, dem die Rolle des Editors in AGPM zugewiesen wurde.

2.  Klicken Sie in der Struktur der **Gruppenrichtlinien-Verwaltungskonsole** in der Gesamtstruktur und Domäne, in der Sie GPOs verwalten möchten, auf **Steuerelement ändern** .

3.  Klicken Sie mit der rechten Maustaste auf den Knoten **Change Control** , und klicken Sie dann auf **Neues gesteuertes Gruppenrichtlinienobjekt**.

4.  Im Dialogfeld " **Neues gesteuertes GPO** ":

    1.  Wenn Sie eine Kopie der Anfrage erhalten möchten, geben Sie Ihre e-Mail-Adresse in das Feld **CC** ein.

    2.  Geben Sie **eigenes** als Namen für das neue Gruppenrichtlinienobjekt ein.

    3.  Geben Sie einen Kommentar für das neue Gruppenrichtlinienobjekt ein.

    4.  Klicken Sie auf **Live erstellen** , damit das neue Gruppenrichtlinienobjekt unmittelbar nach der Genehmigung in der Produktionsumgebung bereitgestellt wird.

    5.  Klicken Sie auf **Übermitteln**.

5.  Wenn im Fenster " **AGPM-Status** " angezeigt wird, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. Das neue Gruppenrichtlinienobjekt wird auf der Registerkarte **Ausstehend** angezeigt.

**So genehmigen Sie die ausstehende Anforderung zum Erstellen eines Gruppenrichtlinienobjekts**

1.  Melden Sie sich auf einem Computer, auf dem Sie AGPM-Client installiert haben, mit einem Benutzerkonto an, dem die Rolle der genehmigenden Person in AGPM zugewiesen wurde.

2.  Öffnen Sie den e-Mail-Posteingang für das Konto, und beachten Sie, dass Sie eine e-Mail-Nachricht vom AGPM-Alias mit der Anforderung des Editors zum Erstellen eines Gruppenrichtlinienobjekts erhalten haben.

3.  Klicken Sie in der Struktur der **Gruppenrichtlinien-Verwaltungskonsole** in der Gesamtstruktur und Domäne, in der Sie GPOs verwalten möchten, auf **Steuerelement ändern** .

4.  Klicken Sie auf der Registerkarte **Inhalt** auf die Registerkarte **Ausstehend** , um die ausstehenden GPOs anzuzeigen.

5.  Klicken Sie mit der rechten Maustaste auf **eigenes**, und klicken Sie dann auf **genehmigen**.

6.  Klicken Sie auf **Ja** , um die Genehmigung für die Erstellung des Gruppenrichtlinienobjekts zu bestätigen. Das Gruppenrichtlinienobjekt wird auf die Registerkarte **gesteuert** verschoben.

### <a href="" id="bkmk-manage2"></a>Schritt 2: Bearbeiten eines Gruppenrichtlinienobjekts

Sie können GPOs verwenden, um Computer-oder Benutzereinstellungen zu konfigurieren und für viele Computer oder Benutzer bereitzustellen. In diesem Schritt verwenden Sie ein Konto mit der Rolle "Editor", um ein GPO aus dem Archiv auszuchecken, das Gruppenrichtlinienobjekt offline zu bearbeiten, das bearbeitete GPO in das Archiv zu überprüfen und die Bereitstellung des Gruppenrichtlinienobjekts in der Produktionsumgebung anzufordern. In diesem Szenario konfigurieren Sie eine Einstellung im Gruppenrichtlinienobjekt, um zu erzwingen, dass das Kennwort mindestens acht Zeichen lang sein muss.

**So überprüfen Sie das Gruppenrichtlinienobjekt aus dem Archiv zur Bearbeitung**

1.  Melden Sie sich auf einem Computer, auf dem Sie AGPM-Client installiert haben, mit einem Benutzerkonto an, dem die Rolle des Editors in AGPM zugewiesen wurde.

2.  Klicken Sie in der Struktur der **Gruppenrichtlinien-Verwaltungskonsole** in der Gesamtstruktur und Domäne, in der Sie GPOs verwalten möchten, auf **Steuerelement ändern** .

3.  Klicken Sie im Detailbereich auf der Registerkarte **Inhalt** auf die Registerkarte **gesteuert** , um die gesteuerten GPOs anzuzeigen.

4.  Klicken Sie mit der rechten Maustaste auf **eigenes**, und klicken Sie dann auf **Auschecken**.

5.  Geben Sie einen Kommentar ein, der im **Verlauf** des Gruppenrichtlinienobjekts angezeigt werden soll, während es ausgecheckt ist, und klicken Sie dann auf **OK**.

6.  Wenn im Fenster " **AGPM-Status** " angezeigt wird, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. Auf der Registerkarte **gesteuert** wird der Status des Gruppenrichtlinienobjekts als **ausgecheckt**identifiziert.

**So bearbeiten Sie das Gruppenrichtlinienobjekt offline und konfigurieren die minimale Kennwortlänge**

1.  Klicken Sie auf der Registerkarte **gesteuert** mit der rechten Maustaste auf **eigenes**, und klicken Sie dann auf **Bearbeiten** , um das Fenster **Gruppenrichtlinienobjekt-Editor** zu öffnen und Änderungen an einer Offlinekopie des Gruppenrichtlinienobjekts vorzunehmen. Konfigurieren Sie in diesem Szenario die minimale Kennwortlänge:

    1.  Doppelklicken Sie unter **Computer Konfiguration**auf **Windows-Einstellungen**, doppelklicken Sie auf **Sicherheitseinstellungen**, doppelklicken Sie auf **Kontorichtlinien**, und doppelklicken Sie auf **Kennwortrichtlinien**.

    2.  Doppelklicken Sie im Detailbereich auf **minimale Kennwortlänge**.

    3.  Aktivieren Sie im Eigenschaftenfenster das Kontrollkästchen **diese Richtlinieneinstellung definieren** , legen Sie die Anzahl der Zeichen auf **8**fest, und klicken Sie dann auf **OK**.

2.  Schließen Sie das Fenster des **Gruppenrichtlinienobjekt-Editors** .

**So überprüfen Sie das Gruppenrichtlinienobjekt in das Archiv**

1.  Klicken Sie auf der Registerkarte **gesteuert** mit der rechten Maustaste auf **eigenes** , und klicken Sie dann auf **Einchecken**.

2.  Geben Sie einen Kommentar ein, und klicken Sie dann auf **OK**.

3.  Wenn im Fenster " **AGPM-Status** " angezeigt wird, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. Auf der Registerkarte **gesteuert** wird der Status des Gruppenrichtlinienobjekts als **eingecheckt**gekennzeichnet.

**So fordern Sie die Bereitstellung des Gruppenrichtlinienobjekts in der Produktionsumgebung an**

1.  Klicken Sie auf der Registerkarte **gesteuert** mit der rechten Maustaste auf **eigenes** , und klicken Sie dann auf **Bereitstellen**.

2.  Da es sich bei diesem Konto nicht um eine genehmigende Person oder einen AGPM-Administrator handelt, müssen Sie eine Anforderung für die Bereitstellung einreichen. Wenn Sie eine Kopie der Anfrage erhalten möchten, geben Sie Ihre e-Mail-Adresse in das Feld **CC** ein. Geben Sie einen Kommentar ein, der im **Verlauf** des Gruppenrichtlinienobjekts angezeigt werden soll, und klicken Sie dann auf **Absenden**.

3.  Wenn im Fenster " **AGPM-Status** " angezeigt wird, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. **Eigenes** wird in der Liste der GPOs auf der Registerkarte **Ausstehend** angezeigt.

### <a href="" id="bkmk-manage3"></a>Schritt 3: überprüfen und Bereitstellen eines Gruppenrichtlinienobjekts

In diesem Schritt fungieren Sie als genehmigende Person, erstellen Berichte und analysieren die Einstellungen und Änderungen an den Einstellungen im Gruppenrichtlinienobjekt, um festzustellen, ob Sie diese genehmigen sollten. Nachdem Sie das Gruppenrichtlinienobjekt ausgewertet haben, stellen Sie es in der Produktionsumgebung bereit, und verknüpfen Sie es mit einer Domäne oder einer Organisationseinheit, damit es wirksam wird, wenn die Gruppenrichtlinie für Computer in dieser Domäne oder OU aktualisiert wird.

**So überprüfen Sie die Einstellungen im Gruppenrichtlinienobjekt**

1.  Melden Sie sich auf einem Computer, auf dem Sie AGPM-Client installiert haben, mit einem Benutzerkonto an, dem die Rolle der genehmigenden Person in AGPM zugewiesen wurde. (Jeder Gruppenrichtlinienadministrator mit der Rolle Prüfer, der in allen anderen Rollen enthalten ist, kann die Einstellungen in einem Gruppenrichtlinienobjekt überprüfen.)

2.  Öffnen Sie den e-Mail-Posteingang für das Konto, und beachten Sie, dass Sie eine e-Mail-Nachricht vom AGPM-Alias mit der Anforderung eines Editors zum Bereitstellen eines Gruppenrichtlinienobjekts erhalten haben.

3.  Klicken Sie in der Struktur der **Gruppenrichtlinien-Verwaltungskonsole** in der Gesamtstruktur und Domäne, in der Sie GPOs verwalten möchten, auf **Steuerelement ändern** .

4.  Klicken Sie im Detailbereich auf der Registerkarte **Inhalt** auf die Registerkarte **Ausstehend** .

5.  Doppelklicken Sie auf **eigenes** , um dessen Verlauf anzuzeigen.

6.  Überprüfen Sie die Einstellungen in der neuesten Version von eigenes:

    1.  Klicken Sie im **Verlaufs** Fenster mit der rechten Maustaste auf die GPO-Version mit dem neuesten Zeitstempel, klicken Sie auf **Einstellungen**, und klicken Sie dann auf **HTML-Bericht** , um eine Zusammenfassung der GPO-Einstellungen anzuzeigen.

    2.  Klicken Sie im Webbrowser auf **Alle anzeigen** , um alle Einstellungen im Gruppenrichtlinienobjekt anzuzeigen.

    3.  Schließen Sie den Browser.

7.  Vergleichen Sie die neueste Version von eigenes mit der ersten Version, die in das Archiv eingecheckt wurde:

    1.  Klicken Sie im Fenster " **Verlauf** " auf die GPO-Version mit dem aktuellsten Zeitstempel. Drücken Sie **STRG** , und klicken Sie auf die älteste GPO-Version mit dem Status **eingecheckt**.

    2.  Klicken Sie auf die Schaltfläche **Unterschiede** . Der Abschnitt **Kontorichtlinien/Kennwortrichtlinie** ist grün hervorgehoben und wird mit **\ [+ \]** vorangestellt, was darauf hinweist, dass diese Einstellung nur in der letzten Version des Gruppenrichtlinienobjekts konfiguriert ist.

    3.  Klicken Sie auf **Kontorichtlinien/Kennwortrichtlinien**. Die Einstellung **minimale Kennwortlänge** ist auch in grün hervorgehoben und mit **\ [+ \]** gekennzeichnet, was darauf hinweist, dass Sie nur in der letzten Version des Gruppenrichtlinienobjekts konfiguriert ist.

    4.  Schließen Sie den Webbrowser.

**So stellen Sie das Gruppenrichtlinienobjekt in der Produktionsumgebung bereit**

1.  Klicken Sie auf der Registerkarte **Ausstehend** mit der rechten Maustaste auf **eigenes** , und klicken Sie dann auf **genehmigen**.

2.  Geben Sie einen Kommentar ein, der in das Protokoll des Gruppenrichtlinienobjekts aufgenommen werden soll.

3.  Klicken Sie auf **Ja**. Wenn im Fenster " **AGPM-Status** " angezeigt wird, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. Das Gruppenrichtlinienobjekt wird in der Produktionsumgebung bereitgestellt.

**So verknüpfen Sie das Gruppenrichtlinienobjekt mit einer Domäne oder Organisationseinheit**

1.  Klicken Sie in der GPMC mit der rechten Maustaste auf die Domäne oder auf eine Organisationseinheit, auf die das von Ihnen konfigurierte Gruppenrichtlinienobjekt angewendet werden soll, und klicken Sie dann auf **vorhandenes Gruppenrichtlinienobjekt verknüpfen**.

2.  Klicken Sie im Dialogfeld **GPO auswählen** auf **eigenes**, und klicken Sie dann auf **OK**.

### <a href="" id="bkmk-manage4"></a>Schritt 4: Verwenden einer Vorlage zum Erstellen eines Gruppenrichtlinienobjekts

In diesem Schritt verwenden Sie ein Konto mit der Rolle "Editor", um eine Vorlage zu erstellen – eine nicht bearbeitbare, statische Version eines GPO, die als Ausgangspunkt zum Erstellen neuer GPOs verwendet werden soll, und dann basierend auf dieser Vorlage ein neues Gruppenrichtlinienobjekt erstellen. Vorlagen sind hilfreich für das schnelle Erstellen mehrerer GPOs, in denen viele der gleichen Einstellungen enthalten sind.

**So erstellen Sie eine Vorlage auf der Grundlage eines vorhandenen Gruppenrichtlinienobjekts**

1.  Melden Sie sich auf einem Computer, auf dem Sie AGPM-Client installiert haben, mit einem Benutzerkonto an, dem die Rolle des Editors in AGPM zugewiesen wurde.

2.  Klicken Sie in der Struktur der **Gruppenrichtlinien-Verwaltungskonsole** in der Gesamtstruktur und Domäne, in der Sie GPOs verwalten möchten, auf **Steuerelement ändern** .

3.  Klicken Sie im Detailbereich auf der Registerkarte **Inhalt** auf die Registerkarte **gesteuert** .

4.  Klicken Sie mit der rechten Maustaste auf **eigenes**, und klicken Sie dann auf **als Vorlage speichern** , um eine Vorlage zu erstellen, die alle Einstellungen umfasst, die derzeit in eigenes enthalten sind.

5.  Geben Sie **MyTemplate** als Namen für die Vorlage und einen Kommentar ein, und klicken Sie dann auf **OK**.

6.  Wenn im Fenster " **AGPM-Status** " angezeigt wird, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. Die neue Vorlage wird auf der Registerkarte **Vorlagen** angezeigt.

**So fordern Sie die Erstellung eines über AGPM verwalteten neuen Gruppenrichtlinienobjekts an**

1.  Klicken Sie auf die Registerkarte **gesteuert** .

2.  Klicken Sie mit der rechten Maustaste auf den Knoten **Change Control** , und klicken Sie dann auf **Neues gesteuertes Gruppenrichtlinienobjekt**.

3.  Im Dialogfeld " **Neues gesteuertes GPO** ":

    1.  Wenn Sie eine Kopie der Anfrage erhalten möchten, geben Sie Ihre e-Mail-Adresse in das Feld **CC** ein.

    2.  Geben Sie **Gruppenrichtlinienverwaltungs** als Namen für das neue Gruppenrichtlinienobjekt ein.

    3.  Geben Sie einen Kommentar für das neue Gruppenrichtlinienobjekt ein.

    4.  Klicken Sie auf **Live erstellen**, damit das neue Gruppenrichtlinienobjekt unmittelbar nach der Genehmigung in der Produktionsumgebung bereitgestellt wird.

    5.  Wählen Sie für **aus GPO-Vorlage**die Option meine **Vorlage**aus.

    6.  Klicken Sie auf **Übermitteln**.

4.  Wenn im Fenster " **AGPM-Status** " angezeigt wird, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. Das neue Gruppenrichtlinienobjekt wird auf der Registerkarte **Ausstehend** angezeigt.

Verwenden Sie ein Konto, dem die Rolle der genehmigenden Person zugewiesen wurde, um die ausstehende Anforderung zum Erstellen des Gruppenrichtlinienobjekts zu genehmigen, wie in [Schritt 1: Erstellen eines Gruppenrichtlinienobjekts](#bkmk-manage1). MyTemplate enthält alle Einstellungen, die Sie in eigenes konfiguriert haben. Da Gruppenrichtlinienverwaltungs mit MyTemplate erstellt wurde, enthält es zunächst alle Einstellungen, die eigenes zum Zeitpunkt der Erstellung von MyTemplate enthielt. Sie können dies bestätigen, indem Sie einen Differenz Bericht generieren, um Gruppenrichtlinienverwaltungs mit MyTemplate zu vergleichen.

**So überprüfen Sie das Gruppenrichtlinienobjekt aus dem Archiv zur Bearbeitung**

1.  Melden Sie sich auf einem Computer, auf dem Sie AGPM-Client installiert haben, mit einem Benutzerkonto an, dem die Rolle des Editors in AGPM zugewiesen wurde.

2.  Klicken Sie mit der rechten Maustaste auf **Gruppenrichtlinienverwaltungs**, und klicken Sie dann auf **Auschecken**.

3.  Geben Sie einen Kommentar ein, der im Verlauf des Gruppenrichtlinienobjekts angezeigt werden soll, während es ausgecheckt ist, und klicken Sie dann auf **OK**.

4.  Wenn im Fenster " **AGPM-Status** " angezeigt wird, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. Auf der Registerkarte **gesteuert** wird der Status des Gruppenrichtlinienobjekts als **ausgecheckt**identifiziert.

**So bearbeiten Sie das Gruppenrichtlinienobjekt offline und konfigurieren die Kontosperrungsdauer**

1.  Klicken Sie auf der Registerkarte **gesteuert** mit der rechten Maustaste auf **Gruppenrichtlinienverwaltungs**, und klicken Sie dann auf **Bearbeiten** , um das Fenster **Gruppenrichtlinienobjekt-Editor** zu öffnen und Änderungen an einer Offlinekopie des Gruppenrichtlinienobjekts vorzunehmen. Konfigurieren Sie in diesem Szenario die minimale Kennwortlänge:

    1.  Doppelklicken Sie unter **Computer Konfiguration**auf **Windows-Einstellungen**, doppelklicken Sie auf **Sicherheitseinstellungen**, doppelklicken Sie auf **Kontorichtlinien**, und doppelklicken Sie auf **Kontosperrungsrichtlinien**.

    2.  Doppelklicken Sie im Detailbereich auf **Kontosperrungsdauer**.

    3.  Aktivieren Sie im Fenster Eigenschaften die Option **diese Richtlinieneinstellung definieren**, legen Sie die Dauer auf **30** Minuten fest, und klicken Sie dann auf **OK**.

2.  Schließen Sie das Fenster des **Gruppenrichtlinienobjekt-Editors** .

Überprüfen Sie Gruppenrichtlinienverwaltungs in die Archivierungs-und Anforderungs Bereitstellung wie bei eigenes in [Schritt 2: Bearbeiten eines Gruppenrichtlinienobjekts](#bkmk-manage2). Sie können Gruppenrichtlinienverwaltungs mit eigenes oder mit MyTemplate mithilfe von Unterschiedsberichten vergleichen. Jedes Konto, das die Rolle Prüfer enthält (AGPM-Administrator \ [Vollzugriff \], genehmigende Person, Bearbeiter oder Bearbeiter) kann Berichte generieren.

**So vergleichen Sie ein GPO mit einem anderen Gruppenrichtlinienobjekt und einer Vorlage**

1.  So vergleichen Sie eigenes und Gruppenrichtlinienverwaltungs:

    1.  Klicken Sie auf der Registerkarte **gesteuert** auf **eigenes**. Drücken Sie **STRG** , und klicken Sie dann auf **Gruppenrichtlinienverwaltungs**.

    2.  Klicken Sie mit der rechten Maustaste auf **Gruppenrichtlinienverwaltungs**, zeigen Sie auf **Unterschiede**, und klicken Sie auf **HTML-Bericht**.

2.  So vergleichen Sie Gruppenrichtlinienverwaltungs und MyTemplate:

    1.  Klicken Sie auf der Registerkarte **gesteuert** auf **Gruppenrichtlinienverwaltungs**.

    2.  Klicken Sie mit der rechten Maustaste auf **Gruppenrichtlinienverwaltungs**, zeigen Sie auf **Unterschiede**, und klicken Sie auf **Vorlage**.

    3.  Wählen Sie **MyTemplate** und **HTML-Bericht**aus, und klicken Sie dann auf **OK**.

### <a href="" id="bkmk-manage5"></a>Schritt 5: Löschen und Wiederherstellen eines Gruppenrichtlinienobjekts

In diesem Schritt fungieren Sie als genehmigende Person, um ein GPO zu löschen.

**So löschen Sie ein Gruppenrichtlinienobjekt**

1.  Melden Sie sich auf einem Computer, auf dem Sie AGPM-Client installiert haben, mit einem Benutzerkonto an, dem die Rolle der genehmigenden Person zugewiesen wurde.

2.  Klicken Sie in der Struktur der **Gruppenrichtlinien-Verwaltungskonsole** in der Gesamtstruktur und Domäne, in der Sie GPOs verwalten möchten, auf **Steuerelement ändern** .

3.  Klicken Sie auf der Registerkarte **Inhalt** auf die Registerkarte **gesteuert** , um die gesteuerten GPOs anzuzeigen.

4.  Klicken Sie mit der rechten Maustaste auf **eigenes**, und klicken Sie dann auf **Löschen**. Klicken Sie auf **Gruppenrichtlinienobjekt aus Archiv und Produktion löschen** , um sowohl die Version im Archiv als auch die bereitgestellte Version des Gruppenrichtlinienobjekts in der Produktionsumgebung zu löschen.

5.  Geben Sie einen Kommentar ein, der im Überwachungspfad für das Gruppenrichtlinienobjekt angezeigt werden soll, und klicken Sie dann auf **OK**.

6.  Wenn im Fenster " **AGPM-Status** " angezeigt wird, dass der Gesamtfortschritt abgeschlossen ist, klicken Sie auf **Schließen**. Das Gruppenrichtlinienobjekt wird von der Registerkarte " **gesteuert** " entfernt und auf der Registerkarte " **Papierkorb** " angezeigt, wo es wiederhergestellt oder gelöscht werden kann.

Gelegentlich können Sie nach dem Löschen eines GPO feststellen, dass es noch benötigt wird. In diesem Schritt fungieren Sie als genehmigende Person zum Wiederherstellen eines gelöschten Gruppenrichtlinienobjekts.

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

     

 

 





