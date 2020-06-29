---
title: Anzeigen von App-V-Server-Veröffentlichungsmetadaten
description: Anzeigen von App-V-Server-Veröffentlichungsmetadaten
author: dansimp
ms.assetid: 048dd42a-24d4-4cc4-81f6-7a919aadd9b2
ms.reviewer: ''
manager: dansimp
ms.author: dansimp
ms.pagetype: mdop, appcompat, virtualization
ms.mktglfcycl: deploy
ms.sitesec: library
ms.prod: w10
ms.date: 06/16/2016
ms.openlocfilehash: 304aa656de98a0c9d59f0a6166811ead911033ad
ms.sourcegitcommit: 354664bc527d93f80687cd2eba70d1eea024c7c3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/26/2020
ms.locfileid: "10804847"
---
# <span data-ttu-id="cef14-103">Anzeigen von App-V-Server-Veröffentlichungsmetadaten</span><span class="sxs-lookup"><span data-stu-id="cef14-103">Viewing App-V Server Publishing Metadata</span></span>


<span data-ttu-id="cef14-104">Gehen Sie wie folgt vor, um Veröffentlichungsmetadaten anzuzeigen, die Ihnen bei der Behebung von Problemen mit der Veröffentlichung helfen können.</span><span class="sxs-lookup"><span data-stu-id="cef14-104">Use this procedure to view publishing metadata, which can help you resolve publishing-related issues.</span></span> <span data-ttu-id="cef14-105">Sie müssen den App-V-Verwaltungsserver verwenden, um dieses Verfahren verwenden zu können.</span><span class="sxs-lookup"><span data-stu-id="cef14-105">You must be using the App-V Management server to use this procedure.</span></span>

<span data-ttu-id="cef14-106">Dieser Artikel enthält die folgenden Informationen:</span><span class="sxs-lookup"><span data-stu-id="cef14-106">This article contains the following information:</span></span>

-   [<span data-ttu-id="cef14-107">App-V 5,0 SP3-Anforderungen für das Anzeigen von Veröffentlichungsmetadaten</span><span class="sxs-lookup"><span data-stu-id="cef14-107">App-V 5.0 SP3 requirements for viewing publishing metadata</span></span>](#bkmk-50sp3-reqs-pub-meta)

-   [<span data-ttu-id="cef14-108">Syntax für die Anzeige von Veröffentlichungsmetadaten</span><span class="sxs-lookup"><span data-stu-id="cef14-108">Syntax to use for viewing publishing metadata</span></span>](#bkmk-syntax-view-pub-meta)

-   [<span data-ttu-id="cef14-109">Abfrage Werte für Clientbetriebssystem und-Version</span><span class="sxs-lookup"><span data-stu-id="cef14-109">Query values for client operating system and version</span></span>](#bkmk-values-query-pub-meta)

-   [<span data-ttu-id="cef14-110">Definition von Veröffentlichungsmetadaten</span><span class="sxs-lookup"><span data-stu-id="cef14-110">Definition of publishing metadata</span></span>](#bkmk-whatis-pub-metadata)

## <a href="" id="bkmk-50sp3-reqs-pub-meta"></a><span data-ttu-id="cef14-111">App-V 5,0 SP3-Anforderungen für das Anzeigen von Veröffentlichungsmetadaten</span><span class="sxs-lookup"><span data-stu-id="cef14-111">App-V 5.0 SP3 requirements for viewing publishing metadata</span></span>


<span data-ttu-id="cef14-112">In App-v 5,0 SP3 müssen Sie die folgenden Werte in der Adresse angeben, wenn Sie den App-v-Veröffentlichungsserver nach Metadaten Abfragen:</span><span class="sxs-lookup"><span data-stu-id="cef14-112">In App-V 5.0 SP3, you must provide the following values in the address when you query the App-V Publishing server for metadata:</span></span>

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><span data-ttu-id="cef14-113">Wert</span><span class="sxs-lookup"><span data-stu-id="cef14-113">Value</span></span></th>
<th align="left"><span data-ttu-id="cef14-114">Zusätzliche Details</span><span class="sxs-lookup"><span data-stu-id="cef14-114">Additional details</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><span data-ttu-id="cef14-115">ClientVersion</span><span class="sxs-lookup"><span data-stu-id="cef14-115">ClientVersion</span></span></strong></p></td>
<td align="left"><p><span data-ttu-id="cef14-116">Wenn Sie den <strong> Clientversion </strong> -Parameter aus der Abfrage weglassen, schließen die Metadaten die neuen App-V 5,0 SP3-Features aus.</span><span class="sxs-lookup"><span data-stu-id="cef14-116">If you omit the <strong>ClientVersion</strong> parameter from the query, the metadata excludes the new App-V 5.0 SP3 features.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><span data-ttu-id="cef14-117">Kunden</span><span class="sxs-lookup"><span data-stu-id="cef14-117">ClientOS</span></span></strong></p></td>
<td align="left"><p><span data-ttu-id="cef14-118">Sie müssen diesen Wert nur angeben, wenn Sie beim Sequenzieren des Pakets bestimmte Clientbetriebssysteme auswählen.</span><span class="sxs-lookup"><span data-stu-id="cef14-118">You have to provide this value only if you select specific client operating systems when you sequence the package.</span></span> <span data-ttu-id="cef14-119">Wenn Sie die Standardeinstellung (alle Betriebssysteme) auswählen, geben Sie diesen Wert in der Abfrage nicht an.</span><span class="sxs-lookup"><span data-stu-id="cef14-119">If you select the default (all operating systems), do not specify this value in the query.</span></span></p>
<p><span data-ttu-id="cef14-120">Wenn Sie den <strong> Client </strong> -Parameter aus der Abfrage weglassen, werden nur die Pakete, die für die Unterstützung eines beliebigen Betriebssystems sequenziert wurden, in den Metadaten angezeigt.</span><span class="sxs-lookup"><span data-stu-id="cef14-120">If you omit the <strong>ClientOS</strong> parameter from the query, only the packages that were sequenced to support any operating system appear in the metadata.</span></span></p></td>
</tr>
</tbody>
</table>



## <a href="" id="bkmk-syntax-view-pub-meta"></a><span data-ttu-id="cef14-121">Abfragesyntax für das Anzeigen von Veröffentlichungsmetadaten</span><span class="sxs-lookup"><span data-stu-id="cef14-121">Query syntax for viewing publishing metadata</span></span>


<span data-ttu-id="cef14-122">Die folgende Tabelle enthält die Beispiele für Syntax und Abfrage.</span><span class="sxs-lookup"><span data-stu-id="cef14-122">The following table provides the syntax and query examples.</span></span>

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><span data-ttu-id="cef14-123">Version von App-V</span><span class="sxs-lookup"><span data-stu-id="cef14-123">Version of App-V</span></span></th>
<th align="left"><span data-ttu-id="cef14-124">Abfragesyntax</span><span class="sxs-lookup"><span data-stu-id="cef14-124">Query syntax</span></span></th>
<th align="left"><span data-ttu-id="cef14-125">Parameter Beschreibungen</span><span class="sxs-lookup"><span data-stu-id="cef14-125">Parameter descriptions</span></span></th>
<th align="left"><span data-ttu-id="cef14-126">Beispiel</span><span class="sxs-lookup"><span data-stu-id="cef14-126">Example</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span data-ttu-id="cef14-127">App-V 5,0 SP3</span><span class="sxs-lookup"><span data-stu-id="cef14-127">App-V 5.0 SP3</span></span></p></td>
<td align="left"><p><code>http://&lt;PubServer&gt;:&lt;Publishing Port#&gt;/?ClientVersion=&lt;AppvClientVersion&gt;&amp;ClientOS=&lt;OSStringValue&gt;</code></p></td>
<td align="left"><table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><span data-ttu-id="cef14-128">Parameter</span><span class="sxs-lookup"><span data-stu-id="cef14-128">Parameter</span></span></th>
<th align="left"><span data-ttu-id="cef14-129">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="cef14-129">Description</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span data-ttu-id="cef14-130">&lt;"Pubserver&gt;</span><span class="sxs-lookup"><span data-stu-id="cef14-130">&lt;PubServer&gt;</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-131">Der Name des App-V-Veröffentlichungsservers.</span><span class="sxs-lookup"><span data-stu-id="cef14-131">Name of the App-V Publishing server.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><p><span data-ttu-id="cef14-132">&lt;Veröffentlichungs-Port #&gt;</span><span class="sxs-lookup"><span data-stu-id="cef14-132">&lt;Publishing Port#&gt;</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-133">Port zu dem App-V-Veröffentlichungsserver, den Sie bei der Konfiguration des Veröffentlichungsservers festgelegt haben.</span><span class="sxs-lookup"><span data-stu-id="cef14-133">Port to the App-V Publishing server, which you defined when you configured the Publishing server.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span data-ttu-id="cef14-134">Clientversion = &lt; AppvClientVersion&gt;</span><span class="sxs-lookup"><span data-stu-id="cef14-134">ClientVersion=&lt;AppvClientVersion&gt;</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-135">Die Version des App-V-Clients.</span><span class="sxs-lookup"><span data-stu-id="cef14-135">Version of the App-V client.</span></span> <span data-ttu-id="cef14-136">In der folgenden Tabelle finden Sie den richtigen zu verwendenden Wert.</span><span class="sxs-lookup"><span data-stu-id="cef14-136">Refer to the following table for the correct value to use.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><p><span data-ttu-id="cef14-137">Clients = &lt; OSStringValue&gt;</span><span class="sxs-lookup"><span data-stu-id="cef14-137">ClientOS=&lt;OSStringValue&gt;</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-138">Das Betriebssystem des Computers, auf dem der App-V-Client ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="cef14-138">Operating system of the computer that is running the App-V client.</span></span> <span data-ttu-id="cef14-139">In der folgenden Tabelle finden Sie den richtigen zu verwendenden Wert.</span><span class="sxs-lookup"><span data-stu-id="cef14-139">Refer to the following table for the correct value to use.</span></span></p></td>
</tr>
</tbody>
</table>
<p> </p>
<p><span data-ttu-id="cef14-140">Wenn Sie den Namen des Veröffentlichungsservers und die Portnummer (http:// &lt; "pubserver &gt; : &lt; Publishing Port # &gt; ) vom App-V-Client abrufen möchten, sehen Sie sich die URL-Konfiguration des <strong> PowerShell-Cmdlets Get-AppvPublishingServer an </strong> .</span><span class="sxs-lookup"><span data-stu-id="cef14-140">To get the name of the Publishing server and the port number (http://&lt;PubServer&gt;:&lt;Publishing Port#&gt;) from the App-V Client, look at the URL configuration of the <strong>Get-AppvPublishingServer</strong> PowerShell cmdlet.</span></span></p></td>
<td align="left"><p><code><a href="http://pubsvr01:2718/?clientversion=5.0.10066.0&amp;clientos=WindowsClient_6.2_x64" data-raw-source="http://pubsvr01:2718/?clientversion=5.0.10066.0&amp;amp;clientos=WindowsClient_6.2_x64">http://pubsvr01:2718/?clientversion=5.0.10066.0&amp;clientos=WindowsClient_6.2_x64</a></code></p>
<p><span data-ttu-id="cef14-141">Im Beispiel:</span><span class="sxs-lookup"><span data-stu-id="cef14-141">In the example:</span></span></p>
<ul>
<li><p><span data-ttu-id="cef14-142">Ein Windows Server 2012 R2 mit dem Namen "pubsvr01" hostet den Veröffentlichungsdienst.</span><span class="sxs-lookup"><span data-stu-id="cef14-142">A Windows Server 2012 R2 named “pubsvr01” hosts the Publishing service.</span></span></p></li>
<li><p><span data-ttu-id="cef14-143">Der Windows-Client ist Windows 8,1 64-Bit.</span><span class="sxs-lookup"><span data-stu-id="cef14-143">The Windows client is Windows 8.1 64-bit.</span></span></p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><span data-ttu-id="cef14-144">App-v 5,0 über APP-v 5,0 SP2</span><span class="sxs-lookup"><span data-stu-id="cef14-144">App-V 5.0 through App-V 5.0 SP2</span></span></p></td>
<td align="left"><p><code>http://&lt;PubServer&gt;:&lt;Publishing Port#&gt;/ </code></p>
<div class="alert">
<strong><span data-ttu-id="cef14-145">Hinweis:</span><span class="sxs-lookup"><span data-stu-id="cef14-145">Note</span></span></strong><br/><p><strong><span data-ttu-id="cef14-146">Clientversion </strong> und <strong> -Clients </strong> werden nur in App-V 5,0 SP3 unterstützt.</span><span class="sxs-lookup"><span data-stu-id="cef14-146">ClientVersion</strong> and <strong>ClientOS</strong> are supported only in App-V 5.0 SP3.</span></span></p>
</div>
<div>

</div></td>
<td align="left"><p><span data-ttu-id="cef14-147">Lesen Sie die Informationen für App-V 5,0 SP3.</span><span class="sxs-lookup"><span data-stu-id="cef14-147">See the information for App-V 5.0 SP3.</span></span></p></td>
<td align="left"><p><code><a href="http://pubsvr01:2718" data-raw-source="http://pubsvr01:2718">http://pubsvr01:2718</a></code></p>
<p><span data-ttu-id="cef14-148">Im Beispiel hostet ein Windows Server 2012 R2 mit dem Namen "pubsvr01" die Verwaltungs-und Veröffentlichungsdienste.</span><span class="sxs-lookup"><span data-stu-id="cef14-148">In the example, A Windows Server 2012 R2 named “pubsvr01” hosts the Management and Publishing services.</span></span></p></td>
</tr>
</tbody>
</table>



## <a href="" id="bkmk-values-query-pub-meta"></a><span data-ttu-id="cef14-149">Abfrage Werte für Clientbetriebssystem und-Version</span><span class="sxs-lookup"><span data-stu-id="cef14-149">Query values for client operating system and version</span></span>


<span data-ttu-id="cef14-150">Geben Sie in ihrer Veröffentlichungsmetadaten-Abfrage die Zeichenfolgenwerte ein, die dem verwendeten Clientbetriebssystem und der verwendeten Version entsprechen.</span><span class="sxs-lookup"><span data-stu-id="cef14-150">In your publishing metadata query, enter the string values that correspond to the client operating system and version that you’re using.</span></span>

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><span data-ttu-id="cef14-151">Betriebssystem</span><span class="sxs-lookup"><span data-stu-id="cef14-151">Operating system</span></span></th>
<th align="left"><span data-ttu-id="cef14-152">Architektur</span><span class="sxs-lookup"><span data-stu-id="cef14-152">Architecture</span></span></th>
<th align="left"><span data-ttu-id="cef14-153">Zeichenfolgenwert für die Zeichenfolge</span><span class="sxs-lookup"><span data-stu-id="cef14-153">Operating string string value</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span data-ttu-id="cef14-154">Windows8.1</span><span class="sxs-lookup"><span data-stu-id="cef14-154">Windows 8.1</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-155">64Bit</span><span class="sxs-lookup"><span data-stu-id="cef14-155">64-bit</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-156">WindowsClient_6.2_x64</span><span class="sxs-lookup"><span data-stu-id="cef14-156">WindowsClient_6.2_x64</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><p><span data-ttu-id="cef14-157">Windows8.1</span><span class="sxs-lookup"><span data-stu-id="cef14-157">Windows 8.1</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-158">32 Bit</span><span class="sxs-lookup"><span data-stu-id="cef14-158">32-bit</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-159">WindowsClient_6.2_x86</span><span class="sxs-lookup"><span data-stu-id="cef14-159">WindowsClient_6.2_x86</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span data-ttu-id="cef14-160">Windows 8</span><span class="sxs-lookup"><span data-stu-id="cef14-160">Windows 8</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-161">64Bit</span><span class="sxs-lookup"><span data-stu-id="cef14-161">64-bit</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-162">WindowsClient_6.2_x64</span><span class="sxs-lookup"><span data-stu-id="cef14-162">WindowsClient_6.2_x64</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><p><span data-ttu-id="cef14-163">Windows 8</span><span class="sxs-lookup"><span data-stu-id="cef14-163">Windows 8</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-164">32 Bit</span><span class="sxs-lookup"><span data-stu-id="cef14-164">32-bit</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-165">WindowsClient_6.2_x86</span><span class="sxs-lookup"><span data-stu-id="cef14-165">WindowsClient_6.2_x86</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span data-ttu-id="cef14-166">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="cef14-166">Windows Server 2012 R2</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-167">64Bit</span><span class="sxs-lookup"><span data-stu-id="cef14-167">64-bit</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-168">WindowsServer_6.2_x64</span><span class="sxs-lookup"><span data-stu-id="cef14-168">WindowsServer_6.2_x64</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><p><span data-ttu-id="cef14-169">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="cef14-169">Windows Server 2012 R2</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-170">32 Bit</span><span class="sxs-lookup"><span data-stu-id="cef14-170">32-bit</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-171">WindowsServer_6.2_x86</span><span class="sxs-lookup"><span data-stu-id="cef14-171">WindowsServer_6.2_x86</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span data-ttu-id="cef14-172">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="cef14-172">Windows Server 2012</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-173">64Bit</span><span class="sxs-lookup"><span data-stu-id="cef14-173">64-bit</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-174">WindowsServer_6.2_x64</span><span class="sxs-lookup"><span data-stu-id="cef14-174">WindowsServer_6.2_x64</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><p><span data-ttu-id="cef14-175">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="cef14-175">Windows Server 2012</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-176">32 Bit</span><span class="sxs-lookup"><span data-stu-id="cef14-176">32-bit</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-177">WindowsServer_6.2_x86</span><span class="sxs-lookup"><span data-stu-id="cef14-177">WindowsServer_6.2_x86</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span data-ttu-id="cef14-178">Windows7</span><span class="sxs-lookup"><span data-stu-id="cef14-178">Windows 7</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-179">64Bit</span><span class="sxs-lookup"><span data-stu-id="cef14-179">64-bit</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-180">WindowsClient_6.1_x64</span><span class="sxs-lookup"><span data-stu-id="cef14-180">WindowsClient_6.1_x64</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><p><span data-ttu-id="cef14-181">Windows7</span><span class="sxs-lookup"><span data-stu-id="cef14-181">Windows 7</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-182">32 Bit</span><span class="sxs-lookup"><span data-stu-id="cef14-182">32-bit</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-183">WindowsClient_6.1_x86</span><span class="sxs-lookup"><span data-stu-id="cef14-183">WindowsClient_6.1_x86</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span data-ttu-id="cef14-184">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="cef14-184">Windows Server 2008 R2</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-185">64Bit</span><span class="sxs-lookup"><span data-stu-id="cef14-185">64-bit</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-186">WindowsServer_6.1_x64</span><span class="sxs-lookup"><span data-stu-id="cef14-186">WindowsServer_6.1_x64</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><p><span data-ttu-id="cef14-187">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="cef14-187">Windows Server 2008 R2</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-188">32 Bit</span><span class="sxs-lookup"><span data-stu-id="cef14-188">32-bit</span></span></p></td>
<td align="left"><p><span data-ttu-id="cef14-189">WindowsServer_6.1_x86</span><span class="sxs-lookup"><span data-stu-id="cef14-189">WindowsServer_6.1_x86</span></span></p></td>
</tr>
</tbody>
</table>



## <a href="" id="bkmk-whatis-pub-metadata"></a><span data-ttu-id="cef14-190">Definition von Veröffentlichungsmetadaten</span><span class="sxs-lookup"><span data-stu-id="cef14-190">Definition of publishing metadata</span></span>


<span data-ttu-id="cef14-191">Wenn Pakete auf einem Computer veröffentlicht werden, auf dem der App-V-Client ausgeführt wird, werden Metadaten an diesen Computer gesendet, der angibt, welche Pakete und Verbindungsgruppen veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="cef14-191">When packages are published to a computer that is running the App-V client, metadata is sent to that computer indicating which packages and connection groups are being published.</span></span> <span data-ttu-id="cef14-192">Der App-V-Client führt zwei getrennte Anforderungen für die folgenden Aktionen aus:</span><span class="sxs-lookup"><span data-stu-id="cef14-192">The App-V Client makes two separate requests for the following:</span></span>

-   <span data-ttu-id="cef14-193">Pakete und Verbindungsgruppen, die für den Clientcomputer berechtigt sind.</span><span class="sxs-lookup"><span data-stu-id="cef14-193">Packages and connection groups that are entitled to the client computer.</span></span>

-   <span data-ttu-id="cef14-194">Pakete und Verbindungsgruppen, die für den aktuellen Benutzer berechtigt sind.</span><span class="sxs-lookup"><span data-stu-id="cef14-194">Packages and connection groups that are entitled to the current user.</span></span>

<span data-ttu-id="cef14-195">Der Veröffentlichungsserver kommuniziert mit dem Verwaltungsserver, um zu ermitteln, welche Pakete und Verbindungsgruppen für den anfordernden verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="cef14-195">The Publishing server communicates with the Management server to determine which packages and connection groups are available to the requester.</span></span> <span data-ttu-id="cef14-196">Der Veröffentlichungsserver muss beim Verwaltungsserver registriert sein, damit die Metadaten generiert werden.</span><span class="sxs-lookup"><span data-stu-id="cef14-196">The Publishing server must be registered with the Management server in order for the metadata to be generated.</span></span>

<span data-ttu-id="cef14-197">Sie können die Metadaten für jede Anforderung in einem Internet Browser anzeigen, indem Sie eine Abfrage verwenden, die sich im Kontext des jeweiligen Benutzers oder Computers befindet.</span><span class="sxs-lookup"><span data-stu-id="cef14-197">You can view the metadata for each request in an Internet browser by using a query that is in the context of the specific user or computer.</span></span>






## <span data-ttu-id="cef14-198">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="cef14-198">Related topics</span></span>


[<span data-ttu-id="cef14-199">Technische Referenz zu App-V 5.0</span><span class="sxs-lookup"><span data-stu-id="cef14-199">Technical Reference for App-V 5.0</span></span>](technical-reference-for-app-v-50.md)








