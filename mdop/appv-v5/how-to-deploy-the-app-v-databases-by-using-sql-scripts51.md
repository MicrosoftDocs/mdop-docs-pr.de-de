---
title: So stellen Sie die App-V-Datenbanken mithilfe von SQL-Skripts bereit
description: So stellen Sie die App-V-Datenbanken mithilfe von SQL-Skripts bereit
author: dansimp
ms.assetid: 1183b1bc-d4d7-4914-a049-06e82bf2d96d
ms.reviewer: ''
manager: dansimp
ms.author: dansimp
ms.pagetype: mdop, appcompat, virtualization
ms.mktglfcycl: deploy
ms.sitesec: library
ms.prod: w10
ms.date: 06/16/2016
ms.openlocfilehash: 4695d105c1aa6732efb6b8ed05169cf29e7f972b
ms.sourcegitcommit: 354664bc527d93f80687cd2eba70d1eea024c7c3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/26/2020
ms.locfileid: "10805477"
---
# So stellen Sie die App-V-Datenbanken mithilfe von SQL-Skripts bereit

Verwenden Sie die folgenden Anweisungen, um SQL-Skripts anstelle des Windows Installers zu verwenden:

- Installieren der App-V 5,1-Datenbanken
- Aktualisieren der App-V-Datenbanken auf eine neuere Version

> [!NOTE]
> Wenn Sie die APP-v 5,0 SP3-Datenbank bereits bereitgestellt haben, müssen die SQL-Skripts nicht auf App-v 5,1 aktualisiert werden.

## Installieren der App-V-Datenbanken mithilfe von SQL-Skripts

1. Bevor Sie die Datenbankskripts installieren, überprüfen und belassen Sie eine Kopie der App-V-Lizenzbestimmungen. Durch Ausführen der Datenbankskripts erklären Sie sich mit den Lizenzbedingungen einverstanden. Wenn Sie diese nicht akzeptieren, sollten Sie diese Software nicht verwenden.
1. Kopieren Sie die **appv\_server\_setup.exe** aus dem App-V-Veröffentlichungsmedium an einen temporären Speicherort.
1. Führen Sie an einer Eingabeaufforderung **appv\_server\_setup.exe** aus, und geben Sie einen temporären Speicherort zum Extrahieren der Datenbankskripts an.

    Beispiel: appv\_server\_setup.exe/Layout c:\\ &lt; _temporären Standort Pfad_&gt;

1. Navigieren Sie zu dem temporären Speicherort, den Sie erstellt haben, öffnen Sie den extrahierten **DatabaseScripts** -Ordner, und überprüfen Sie die entsprechende Readme.txt Datei, um Anweisungen zu erhalten:

    | Datenbank | Speicherort der Readme.txt zu verwendenden Datei |
    |--|--|
    | Verwaltungsdatenbank | ManagementDatabase-Unterordner |
    | Berichtsdatenbank | ReportingDatabase-Unterordner |

> [!CAUTION]
> Die readme.txt-Datei im ManagementDatabase-Unterordner ist veraltet. Die Informationen in den aktualisierten Readme-Dateien unten sind die aktuellsten und sollten die Readme-Informationen ersetzen, die in den **DatabaseScripts** -Ordnern zur Verfügung gestellt werden.

> [!IMPORTANT]
> Das InsertVersionInfo. SQL-Skript ist für Versionen der APP-v-Verwaltungsdatenbank später als App-v 5,0 SP3 nicht erforderlich.

Das Skript "Permissions. SQL" sollte gemäß **Schritt 2** im [KB-Artikel 3031340](https://support.microsoft.com/kb/3031340)aktualisiert werden. **Schritt 1** ist für Versionen von App-v später als App-v 5,0 SP3 nicht erforderlich.

## Aktualisierte Informationen zur Verwaltungsdatenbank-Readme-Datei

```plaintext
******************************************************************
Before you install and use the Application Virtualization Database Scripts you must:
1.Review the Microsoft Application Virtualization Server 5.0 license terms.
2.Print and retain a copy of the license terms for your records.
By running the Microsoft Application Virtualization Database Scripts you agree to such license terms.  If you do not accept them, do not use the software.
******************************************************************


Steps to install "AppVManagement" schema in SQL SERVER.


## PREREQUISITES:

 1. Review the installation package.  The following files MUST exist:

    SQL files
    ---------
    Database.sql
    CreateTables.sql
    CreateStoredProcs.sql
    UpdateTables.sql
    Permissions.sql

 2. Ensure the target SQL Server instance and SQL Server Agent service are running.

 3. If you are not running the scripts directly on the server, ensure the
    necessary SQL Server client software is installed and available from
    the specified location.  Specifically, the "osql" command must
##     be supported for these scripts to run.



## PREPARATION:

 1. Review the database.sql file and modify as necessary.  Although the
    defaults are likely sufficient, it is suggested that the following
    settings be reviewed:

    DATABASE - ensure name is satisfactory - default is "AppVManagement".

 2. Review the Permissions.sql file and provide all the necessary account information
    for setting up read and write access on the database. Note: Default settings
##     in the file will not work.



## INSTALLATION:

 1. Run the database.sql against the "master" database.  Your user
    credential must have the ability to create databases.
    This script will create the database.

 2. Run the following scripts against the "AppVManagement" database using the
    same account as above in order.

    CreateTables.sql
    CreateStoredProcs.sql
    UpdateTables.sql
##     Permissions.sql

```

## Aktualisierte Informationen zur Berichtsdatenbank-Readme-Datei

```plaintext
******************************************************************
Before you install and use the Application Virtualization Database Scripts you must:
1.Review the Microsoft Application Virtualization Server 5.0 license terms.
2.Print and retain a copy of the license terms for your records.
By running the Microsoft Application Virtualization Database Scripts you agree to such license terms.  If you do not accept them, do not use the software.
******************************************************************

Steps to install "AppVReporting" schema in SQL SERVER.


## PREREQUISITES:

 1. Review the installation package.  The following files MUST exist:

    SQL files
    ---------
    Database.sql
    UpgradeDatabase.sql
    CreateTables.sql
    CreateReportingStoredProcs.sql
    CreateStoredProcs.sql
    CreateViews.sql
    InsertVersionInfo.sql
    Permissions.sql
    ScheduleReportingJob.sql

 2. Ensure the target SQL Server instance and SQL Server Agent service are running.

 3. If you are not running the scripts directly on the server, ensure the 
    necessary SQL Server client software is installed and executable from
    the location you have chosen.  Specifically, the "osql" command must
##     be supported for these scripts to run.



## PREPARATION:

 1. Review the database.sql file and modify as necessary.  Although the
    defaults are likely sufficient, it is suggested that the following
    settings be reviewed:

    DATABASE - ensure name is satisfactory - default is "AppVReporting".

 2. Review the Permissions.sql file and provide all the necessary account information
    for setting up read and write access on the database. Note: Default settings
    in the file will not work.

 3. Review the ScheduleReportingJob.sql file and make sure that the stored proc schedule
    time is acceptable. The default stored proc schedule time is at 12.01 AM (line 84). 
    If this time is not suitable, you can change this to a more suitable time. The time is
##     in the format HHMMSS.



## INSTALLATION:

 1. Run the database.sql against the "master" database.  Your user
    credential must have the ability to create databases.
    This script will create the database.

 2. If upgrading the database, run UpgradeDatabase.sql This will upgrade database schema.

 2. Run the following scripts against the "AppVReporting" database using the
    same account as above in order.

    CreateTables.sql
    CreateReportingStoredProcs.sql
    CreateStoredProcs.sql
    CreateViews.sql
    InsertVersionInfo.sql
    Permissions.sql
##     ScheduleReportingJob.sql

```

**Sie haben ein App-V-Problem?** Verwenden Sie das [App-V TechNet-Forum](https://social.technet.microsoft.com/Forums/home?forum=mdopappv).

## Verwandte Themen

[Bereitstellen des App-V 5.1-Servers](deploying-the-app-v-51-server.md)

[So stellen Sie den App-V 5.1-Server bereit](how-to-deploy-the-app-v-51-server.md)
