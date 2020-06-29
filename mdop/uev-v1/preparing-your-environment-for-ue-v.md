---
title: Vorbereiten der Umgebung für UE-V
description: Vorbereiten der Umgebung für UE-V
author: dansimp
ms.assetid: c93d3b33-e032-451a-9e1b-8534e1625396
ms.reviewer: ''
manager: dansimp
ms.author: dansimp
ms.pagetype: mdop, virtualization
ms.mktglfcycl: deploy
ms.sitesec: library
ms.prod: w10
ms.date: 06/16/2016
ms.openlocfilehash: 8f806f3c326bad5204a7f1ee69e11b61177e3cce
ms.sourcegitcommit: 354664bc527d93f80687cd2eba70d1eea024c7c3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/26/2020
ms.locfileid: "10810681"
---
# <span data-ttu-id="ae2f5-103">Vorbereiten der Umgebung für UE-V</span><span class="sxs-lookup"><span data-stu-id="ae2f5-103">Preparing Your Environment for UE-V</span></span>


<span data-ttu-id="ae2f5-104">Microsoft User Experience Virtualization (UE-V) durchstreift die Einstellungen zwischen Computern durch die Verwendung eines Einstellungsspeicher Orts.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-104">Microsoft User Experience Virtualization (UE-V) roams settings between computers by the use of a settings storage location.</span></span> <span data-ttu-id="ae2f5-105">Der Speicherort der Einstellungen ist eine Dateifreigabe und sollte während der Bereitstellung des UE-V-Agents konfiguriert werden.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-105">The settings storage location is a file share and should be configured during the UE-V Agent deployment.</span></span> <span data-ttu-id="ae2f5-106">Sie muss entweder als Speicherort für Einstellungen oder als Active Directory-Basisverzeichnis definiert werden.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-106">It must be defined either as a settings storage location or as an Active Directory home directory.</span></span> <span data-ttu-id="ae2f5-107">Darüber hinaus sollte der Administrator einen Zeitserver konfigurieren, um eine konsistente Synchronisierung zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-107">In addition, the administrator should configure a time server to support consistent synchronization.</span></span> <span data-ttu-id="ae2f5-108">Wenn Sie Ihre Umgebung für UE-V vorbereiten möchten, sollten Sie Folgendes berücksichtigen:</span><span class="sxs-lookup"><span data-stu-id="ae2f5-108">To prepare your environment for UE-V, you should consider the following:</span></span>

-   <span data-ttu-id="ae2f5-109">[Speicher für UE-V-Einstellungen](#bkmk-uevsettingsstorage):</span><span class="sxs-lookup"><span data-stu-id="ae2f5-109">[UE-V Settings Storage](#bkmk-uevsettingsstorage):</span></span>

    -   [<span data-ttu-id="ae2f5-110">Definieren eines Speicherorts für Einstellungen</span><span class="sxs-lookup"><span data-stu-id="ae2f5-110">Defining a Settings Storage Location</span></span>](#bkmk-definingsettingsstoragelocation)

    -   [<span data-ttu-id="ae2f5-111">Verwenden des Active Directory-Basisverzeichnisses mit UE-V</span><span class="sxs-lookup"><span data-stu-id="ae2f5-111">Using Active Directory Home Directory with UE-V</span></span>](#bkmk-usingactivedirectoryhomedirectory)

-   [<span data-ttu-id="ae2f5-112">Synchronisieren von Computer Uhren für die Synchronisierung von UE-V-Einstellungen</span><span class="sxs-lookup"><span data-stu-id="ae2f5-112">Synchronize Computer Clocks for UE-V Settings Synchronization</span></span>](#bkmk-synchronizecomputerclocks)

-   [<span data-ttu-id="ae2f5-113">Leistungs-und Kapazitätsplanung</span><span class="sxs-lookup"><span data-stu-id="ae2f5-113">Performance and Capacity Planning</span></span>](#bkmk-performancecapacityplanning)

<span data-ttu-id="ae2f5-114">Weitere Informationen zu den Anforderungen an das Betriebssystem und den Computer finden Sie unter [unterstützte Konfigurationen für UE-V 1,0](supported-configurations-for-ue-v-10.md).</span><span class="sxs-lookup"><span data-stu-id="ae2f5-114">For more information about operating system and computer requirements, see [Supported Configurations for UE-V 1.0](supported-configurations-for-ue-v-10.md).</span></span>

## <a href="" id="bkmk-uevsettingsstorage"></a><span data-ttu-id="ae2f5-115">Speicher für UE-V-Einstellungen</span><span class="sxs-lookup"><span data-stu-id="ae2f5-115">UE-V settings storage</span></span>


<span data-ttu-id="ae2f5-116">Sie können den Speicher der Benutzeroberflächen-Virtualisierungs-Einstellungen in einer von zwei Konfigurationen definieren: einem Einstellungs Speicherort oder einem Active Directory-Basisverzeichnis.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-116">You can define the User Experience Virtualization settings storage in one of two configurations: a settings storage location or an Active Directory home directory.</span></span>

### <a href="" id="bkmk-definingsettingsstoragelocation"></a><span data-ttu-id="ae2f5-117">Definieren eines Speicherorts für Einstellungen</span><span class="sxs-lookup"><span data-stu-id="ae2f5-117">Define a settings storage location</span></span>

<span data-ttu-id="ae2f5-118">Der Speicherort der UE-v-Einstellungen ist eine standardmäßige Netzwerkfreigabe, auf die UE-v-Benutzer zugreifen können.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-118">The UE-V settings storage location is a standard network share that is accessible by UE-V users.</span></span> <span data-ttu-id="ae2f5-119">Vor dem Definieren des Speicherorts für Einstellungen müssen Sie ein Stammverzeichnis erstellen.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-119">Before you define the settings storage location, you must create a root directory.</span></span> <span data-ttu-id="ae2f5-120">Benutzer, die Einstellungen für die Freigabe speichern, müssen über Lese-/Schreibzugriff für den Speicherort verfügen.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-120">Users who will store settings on the share must have read/write permissions to the storage location.</span></span> <span data-ttu-id="ae2f5-121">Der UE-V-Agent erstellt benutzerspezifische Ordner unter diesem Stammverzeichnis.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-121">The UE-V Agent will create user-specific folders under this root directory.</span></span> <span data-ttu-id="ae2f5-122">Der Speicherort des Einstellungs Speichers wird durch Festlegen der **SettingsStoragePath** -Konfigurationsoption definiert.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-122">The settings storage location is defined by setting the **SettingsStoragePath** configuration option.</span></span> <span data-ttu-id="ae2f5-123">Diese Option kann wie folgt konfiguriert werden:</span><span class="sxs-lookup"><span data-stu-id="ae2f5-123">This option can be configured in the following ways:</span></span>

-   <span data-ttu-id="ae2f5-124">Während der Installation des UE-V-Agents über einen Befehlszeilenparameter oder in einem Batchskript.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-124">During the installation of the UE-V agent through a command-line parameter or in a batch script.</span></span>

-   <span data-ttu-id="ae2f5-125">Verwenden von Gruppenrichtlinien</span><span class="sxs-lookup"><span data-stu-id="ae2f5-125">Using Group Policy.</span></span>

-   <span data-ttu-id="ae2f5-126">Nach der Installation mithilfe von PowerShell oder WMI.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-126">After installation, by using PowerShell or WMI.</span></span>

<span data-ttu-id="ae2f5-127">Der Pfad muss sich im UNC-Pfad (Universal Naming Convention) des Servers und der Freigabe befinden.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-127">The path must be in a universal naming convention (UNC) path of the server and share.</span></span> <span data-ttu-id="ae2f5-128">Beispiel: **\\\\server\\settingsshare\\**.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-128">For example, **\\\\server\\settingsshare\\**.</span></span> <span data-ttu-id="ae2f5-129">Diese Konfigurationsoption unterstützt die Verwendung von Variablen, um bestimmte Roaming-Szenarien zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-129">This configuration option supports the use of variables to enable specific roaming scenarios.</span></span>

<span data-ttu-id="ae2f5-130">Sie können die `%username%` Variable mit dem UNC-Pfad des Servers und der Freigabe verwenden.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-130">You can use the `%username%` variable with the UNC path of the server and share.</span></span> <span data-ttu-id="ae2f5-131">Dadurch werden die gleichen Einstellungen für alle Computer oder Sitzungen bereitgestellt, bei denen sich ein Benutzer anmeldet.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-131">This will provide the same settings experience on all computers or sessions that a user logs into.</span></span> <span data-ttu-id="ae2f5-132">Bedenken Sie diese Konfiguration für die folgenden Szenarien:</span><span class="sxs-lookup"><span data-stu-id="ae2f5-132">Consider this configuration for the following scenarios:</span></span>

1.  <span data-ttu-id="ae2f5-133">Benutzer im Unternehmen verfügen über mehrere, ähnlich konfigurierte physische Computer, und die Einstellungen jedes Benutzers sollten auf allen Computern gleich sein.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-133">Users in the enterprise have multiple, similarly configured physical computers and each user’s settings should be the same across all computers.</span></span>

2.  <span data-ttu-id="ae2f5-134">Benutzer im Unternehmen verwenden VPN-Pools (Virtual Desktop Infrastructure), in denen die Einstellungen für die VDI-Sitzungen jedes Benutzers beibehalten werden sollen.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-134">Users in the enterprise use virtual desktop infrastructure (VDI) pools where settings should be retained across each user’s VDI sessions.</span></span>

3.  <span data-ttu-id="ae2f5-135">Benutzer im Unternehmen verfügen über einen physikalischen Computer und verwenden zusätzlich eine VDI.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-135">Users in the enterprise have one physical computer and additionally use a VDI.</span></span> <span data-ttu-id="ae2f5-136">Die Einstellungen der einzelnen Benutzer sollten unabhängig davon sein, ob Sie den physikalischen Computer oder die VDI-Sitzung verwenden.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-136">Each user’s settings experience should be the same whether using the physical computer or VDI session.</span></span>

4.  <span data-ttu-id="ae2f5-137">Mehrere Enterprise-Computer werden von mehreren Benutzern verwendet.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-137">Multiple enterprise computers are used by multiple users.</span></span> <span data-ttu-id="ae2f5-138">Die Einstellungen des jeweiligen Benutzers sollten auf allen Computern gleich sein.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-138">Each user’s settings experience should be the same across all computers.</span></span>

<span data-ttu-id="ae2f5-139">Sie können die **%username%\\%Computername%** -Variablen mit dem UNC-Pfad des Servers und der Freigabe verwenden.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-139">You can use the **%username%\\%computername%** variables with the UNC path of the server and share.</span></span> <span data-ttu-id="ae2f5-140">Dadurch bleibt die Einstellungen für die einzelnen Computer erhalten.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-140">This will preserve the settings experience for each computer.</span></span> <span data-ttu-id="ae2f5-141">Bedenken Sie diese Konfiguration für die folgenden Szenarien:</span><span class="sxs-lookup"><span data-stu-id="ae2f5-141">Consider this configuration for the following scenarios:</span></span>

1.  <span data-ttu-id="ae2f5-142">Benutzer im Unternehmen verfügen über mehrere physische Computer, und Sie möchten die Einstellungen für die einzelnen Computer beibehalten.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-142">Users in the enterprise have multiple physical computers and you want to preserve the settings experience for each computer.</span></span>

2.  <span data-ttu-id="ae2f5-143">Die Enterprise-Computer werden von mehreren Benutzern verwendet.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-143">The enterprise computers are used by multiple users.</span></span> <span data-ttu-id="ae2f5-144">Die Einstellungen sollten für jeden Computer beibehalten werden, in dem sich der Benutzer anmeldet.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-144">The settings experience should be preserved for each computer that the user logs into.</span></span>

<span data-ttu-id="ae2f5-145">Der UE-v-Agent erstellt dynamisch den benutzerspezifischen Einstellungsspeicher Pfad basierend auf einer UE-v- `SettingsStoragePath` Konfigurationseinstellung und den definierten Variablen.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-145">The UE-V agent dynamically creates the user-specific settings storage path based on a UE-V `SettingsStoragePath` configuration setting and the variables that are defined.</span></span>

<span data-ttu-id="ae2f5-146">Der UE-V-Agent erstellt dynamisch einen versteckten Systemordner `SettingsPackages` , der innerhalb jedes benutzerspezifischen Speicherorts benannt ist.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-146">The UE-V agent dynamically creates a hidden system folder named `SettingsPackages` within each user-specific storage location.</span></span> <span data-ttu-id="ae2f5-147">Der UE-v-Agent liest und schreibt Einstellungen an diesen Speicherort, wie Sie von den registrierten UE-v-Einstellungen für Standort Vorlagen definiert werden.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-147">The UE-V agent reads and writes settings to this location as defined by registered UE-V settings location templates.</span></span>

<span data-ttu-id="ae2f5-148">Wenn der Speicherort der Einstellungen für einen Satz verwalteter Computer eines Benutzers identisch ist, werden die entsprechenden UE-V-Einstellungen durch die Regel "letzte Write WINS" bestimmt.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-148">If the settings storage location is the same for a set of managed computers of a user, the applicable UE-V settings are determined by a “Last write wins” rule.</span></span> <span data-ttu-id="ae2f5-149">Der Agent, der auf einem Computer ausgeführt wird, liest und schreibt unabhängig von Agents, die auf anderen Computern ausgeführt werden, an den Speicherort der Einstellungen.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-149">The agent that runs on one computer reads and writes to the settings location independently of agents that run on other computers.</span></span> <span data-ttu-id="ae2f5-150">Die zuletzt geschriebenen Einstellungen und Werte sind die Einstellungen, die angewendet werden, wenn der nächste Agent vom Speicherort für Einstellungen liest.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-150">The last settings and values written are the settings that are applied when the next agent reads from the settings storage location.</span></span> <span data-ttu-id="ae2f5-151">Weitere Informationen finden Sie unter [Bereitstellen des Speicherorts für Einstellungen für UE-V 1,0](deploying-the-settings-storage-location-for-ue-v-10.md).</span><span class="sxs-lookup"><span data-stu-id="ae2f5-151">For more information, see [Deploying the Settings Storage Location for UE-V 1.0](deploying-the-settings-storage-location-for-ue-v-10.md).</span></span>

### <a href="" id="bkmk-usingactivedirectoryhomedirectory"></a><span data-ttu-id="ae2f5-152">Verwenden des Active Directory-Basisverzeichnisses mit UE-V</span><span class="sxs-lookup"><span data-stu-id="ae2f5-152">Use Active Directory home directory with UE-V</span></span>

<span data-ttu-id="ae2f5-153">Wenn für UE-V kein Speicherplatz für Einstellungen konfiguriert ist, wenn der Agent bereitgestellt wird, wird das Active Directory-Basisverzeichnis (AD) des Benutzers zum Speichern von Einstellungen für Standort Pakete verwendet.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-153">If no settings storage location is configured for UE-V when the agent is deployed, then the user’s Active Directory (AD) home directory is used to store settings location packages.</span></span> <span data-ttu-id="ae2f5-154">Der UE-V-Agent erstellt dynamisch den Einstellungsspeicher Ordner unter dem Stammverzeichnis des AD Home-Verzeichnisses jedes Benutzers.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-154">The UE-V agent dynamically creates the settings storage folder below the root of the AD home directory of each user.</span></span> <span data-ttu-id="ae2f5-155">Der Agent verwendet nur das Active Directory-Basisverzeichnis, wenn ein Settings-Speicherort (SettingsStoragePath) nicht anderweitig definiert ist.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-155">The agent only uses the Active Directory home directory if a settings storage location (SettingsStoragePath) is not otherwise defined.</span></span>

## <a href="" id="bkmk-synchronizecomputerclocks"></a><span data-ttu-id="ae2f5-156">Synchronisieren von Computeruhren für die Synchronisierung von UE-V-Einstellungen</span><span class="sxs-lookup"><span data-stu-id="ae2f5-156">Synchronize computer clocks for UE-V settings synchronization</span></span>


<span data-ttu-id="ae2f5-157">Computer, auf denen der UE-V-Agent zum Synchronisieren von Einstellungen ausgeführt wird, müssen einen Zeitserver verwenden.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-157">Computers that run the UE-V agent to synchronize settings must use a time server.</span></span> <span data-ttu-id="ae2f5-158">Zeitstempel werden verwendet, um festzustellen, ob die Einstellungen vom Speicherort der Einstellungen synchronisiert werden müssen.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-158">Time stamps are used to determine if settings need to be synchronized from the settings storage location.</span></span> <span data-ttu-id="ae2f5-159">Wenn die Uhrzeit des Computers falsch ist, können ältere Einstellungen neuere Einstellungen überschreiben, oder die neuen Einstellungen werden möglicherweise nicht am Speicherort des Einstellungs Speichers gespeichert.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-159">If the computer clock is inaccurate, older settings can overwrite newer settings, or the new settings might not be saved to the settings storage location.</span></span> <span data-ttu-id="ae2f5-160">Die Verwendung eines Zeitservers ermöglicht es UE-V, eine konsistente Einstellungen zu gewährleisten.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-160">The use of a time server enables UE-V to maintain a consistent settings experience.</span></span>

## <a href="" id="bkmk-performancecapacityplanning"></a><span data-ttu-id="ae2f5-161">Leistungs-und Kapazitätsplanung</span><span class="sxs-lookup"><span data-stu-id="ae2f5-161">Performance and capacity planning</span></span>


<span data-ttu-id="ae2f5-162">Die Kapazitätsanforderungen für UE-V können mithilfe der standardmäßigen Festplattenkapazität und der Netzwerkstatusüberwachung bestimmt werden.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-162">Capacity requirements for UE-V can be determined by use of standard disk capacity and network health monitoring.</span></span> <span data-ttu-id="ae2f5-163">UE-V verwendet eine SMB-Freigabe (Server Message Block) für die Speicherung von Einstellungspaketen.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-163">UE-V uses a Server Message Block (SMB) share for the storage of settings packages.</span></span> <span data-ttu-id="ae2f5-164">Die Größe der Einstellungs Pakete variiert je nach den Einstellungsinformationen für eine bestimmte Anwendung.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-164">The size of settings packages varies depending on the settings information for a specific application.</span></span> <span data-ttu-id="ae2f5-165">Während die meisten Einstellungs Pakete klein sind, kann die Synchronisierung von potenziell umfangreichen Dateien, wie etwa Desktop Bildern, zu einer schlechten Leistung führen, insbesondere bei langsameren Netzwerken.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-165">While most settings packages are small, the synchronization of potentially large files, such as desktop images, can result in poor performance, particularly on slower networks.</span></span> <span data-ttu-id="ae2f5-166">Um Probleme mit der Netzwerklatenz zu minimieren, sollten Sie die Speicherorte für Einstellungen in denselben lokalen Netzwerken erstellen, in denen sich die Computer der Benutzer befinden.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-166">To minimize problems with network latency, you should create settings storage locations on the same local networks where the users’ computers reside.</span></span>

<span data-ttu-id="ae2f5-167">Standardmäßig wird die UE-V-Synchronisierung nach 2 Sekunden ablaufen, wenn das Netzwerk langsam ist oder das Einstellungspaket groß ist.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-167">By default, the UE-V synchronization will time out after 2 seconds if the network is slow or the settings package is large.</span></span> <span data-ttu-id="ae2f5-168">Sie können das Timeout mit Gruppenrichtlinien konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="ae2f5-168">You can configure the timeout with Group Policy.</span></span> <span data-ttu-id="ae2f5-169">Weitere Informationen zum Festlegen des Timeouts finden Sie unter [Konfigurieren von UE-V mit Gruppenrichtlinienobjekten](configuring-ue-v-with-group-policy-objects.md).</span><span class="sxs-lookup"><span data-stu-id="ae2f5-169">For more information about how to set the timeout, see [Configuring UE-V with Group Policy Objects](configuring-ue-v-with-group-policy-objects.md).</span></span>

## <span data-ttu-id="ae2f5-170">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="ae2f5-170">Related topics</span></span>


[<span data-ttu-id="ae2f5-171">Microsoft-User Experience Virtualization (UE-V) 1.0</span><span class="sxs-lookup"><span data-stu-id="ae2f5-171">Microsoft User Experience Virtualization (UE-V) 1.0</span></span>](index.md)

[<span data-ttu-id="ae2f5-172">Planen für UE-V 1.0</span><span class="sxs-lookup"><span data-stu-id="ae2f5-172">Planning for UE-V 1.0</span></span>](planning-for-ue-v-10.md)

[<span data-ttu-id="ae2f5-173">Unterstützte Konfigurationen für UE-V 1.0</span><span class="sxs-lookup"><span data-stu-id="ae2f5-173">Supported Configurations for UE-V 1.0</span></span>](supported-configurations-for-ue-v-10.md)

 

 




