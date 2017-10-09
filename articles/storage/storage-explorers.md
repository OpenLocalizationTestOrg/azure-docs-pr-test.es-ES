---
title: aaaTools para trabajar con el almacenamiento de Azure | Documentos de Microsoft
description: Una lista de herramientas que le permiten tooview/interactuar con los datos de almacenamiento de Azure.
services: storage
documentationcenter: 
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: e4748642-98c4-437e-b0ed-4f9641c2e894
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: dineshmurthy
ms.openlocfilehash: 3308de2153099a05a676ab1d76426bd932e8a96c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-client-tools"></a><span data-ttu-id="46c9e-103">Herramientas de cliente de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="46c9e-103">Azure Storage Client Tools</span></span>
<span data-ttu-id="46c9e-104">Los usuarios de almacenamiento de Azure con frecuencia desean toobe capaz de tooview/interactuar con sus datos mediante una herramienta de cliente de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="46c9e-104">Users of Azure Storage frequently want toobe able tooview/interact with their data using an Azure Storage client tool.</span></span> <span data-ttu-id="46c9e-105">En las tablas de Hola a continuación, se incluyen una serie de herramientas que le permiten toodo esta.</span><span class="sxs-lookup"><span data-stu-id="46c9e-105">In hello tables below, we list a number of tools that allow you toodo this.</span></span> <span data-ttu-id="46c9e-106">Colocamos una "X" en cada bloque si proporciona la capacidad de hello tooeither enumerar y tener acceso a la abstracción de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="46c9e-106">We put an "X" in each block if it provides hello ability tooeither enumerate and/or access hello data abstraction.</span></span> <span data-ttu-id="46c9e-107">tabla de Hello también muestra si herramientas Hola está disponible o no.</span><span class="sxs-lookup"><span data-stu-id="46c9e-107">hello table also shows if hello tools is free or not.</span></span> <span data-ttu-id="46c9e-108">"Prueba" indica que hay una prueba gratuita, pero producto completo de hello no está disponible.</span><span class="sxs-lookup"><span data-stu-id="46c9e-108">"Trial" indicates that there is a free trial, but hello full product is not free.</span></span> <span data-ttu-id="46c9e-109">"S/N" indica que hay disponible una versión gratuita, mientras que la versión disponible para la compra es diferente.</span><span class="sxs-lookup"><span data-stu-id="46c9e-109">"Y/N" indicates that a version is available for free, while a different version is available for purchase.</span></span>

<span data-ttu-id="46c9e-110">Hemos proporcionado únicamente una instantánea de herramientas de cliente de almacenamiento de Azure disponibles Hola.</span><span class="sxs-lookup"><span data-stu-id="46c9e-110">We've only provided a snapshot of hello available Azure Storage client tools.</span></span> <span data-ttu-id="46c9e-111">Estas herramientas pueden continuar tooevolve y crecer en la funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="46c9e-111">These tools may continue tooevolve and grow in functionality.</span></span> <span data-ttu-id="46c9e-112">Si no hay correcciones o actualizaciones, deje un toolet comentario que saber.</span><span class="sxs-lookup"><span data-stu-id="46c9e-112">If there are corrections or updates, please leave a comment toolet us know.</span></span> <span data-ttu-id="46c9e-113">Hello mismo puede decirse si sabe de herramientas que debería aparecer aquí toobe - estaremos encantado tooadd ellos.</span><span class="sxs-lookup"><span data-stu-id="46c9e-113">hello same is true if you know of tools that ought toobe here - we'd be happy tooadd them.</span></span>

<span data-ttu-id="46c9e-114">**Herramientas de cliente de Almacenamiento de Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="46c9e-114">**Microsoft Azure Storage Client Tools**</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="46c9e-115">Herramienta de cliente de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="46c9e-115">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="46c9e-116">Blob en bloques</span><span class="sxs-lookup"><span data-stu-id="46c9e-116">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="46c9e-117">Blob en páginas</span><span class="sxs-lookup"><span data-stu-id="46c9e-117">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="46c9e-118">Append Blob</span><span class="sxs-lookup"><span data-stu-id="46c9e-118">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="46c9e-119">Tablas</span><span class="sxs-lookup"><span data-stu-id="46c9e-119">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="46c9e-120">Colas</span><span class="sxs-lookup"><span data-stu-id="46c9e-120">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="46c9e-121">Archivos</span><span class="sxs-lookup"><span data-stu-id="46c9e-121">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="46c9e-122">Gratuito</span><span class="sxs-lookup"><span data-stu-id="46c9e-122">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="46c9e-123">Plataforma</span><span class="sxs-lookup"><span data-stu-id="46c9e-123">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="46c9e-124">Web</span><span class="sxs-lookup"><span data-stu-id="46c9e-124">Web</span></span></td>
    <td><span data-ttu-id="46c9e-125">Windows</span><span class="sxs-lookup"><span data-stu-id="46c9e-125">Windows</span></span></td>
    <td><span data-ttu-id="46c9e-126">OSX</span><span class="sxs-lookup"><span data-stu-id="46c9e-126">OSX</span></span></td>
    <td><span data-ttu-id="46c9e-127">Linux</span><span class="sxs-lookup"><span data-stu-id="46c9e-127">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="46c9e-128"><a href="https://azure.microsoft.com/features/azure-portal/">Microsoft Azure Portal</a></span><span class="sxs-lookup"><span data-stu-id="46c9e-128"><a href="https://azure.microsoft.com/features/azure-portal/">Microsoft Azure Portal</a></span></span></td>
    <td><span data-ttu-id="46c9e-129">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-129">X</span></span></td>
    <td><span data-ttu-id="46c9e-130">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-130">X</span></span></td>
    <td><span data-ttu-id="46c9e-131">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-131">X</span></span></td>
    <td><span data-ttu-id="46c9e-132">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-132">X</span></span></td>
    <td><span data-ttu-id="46c9e-133">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-133">X</span></span></td>
    <td><span data-ttu-id="46c9e-134">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-134">X</span></span></td>
    <td><span data-ttu-id="46c9e-135">Y</span><span class="sxs-lookup"><span data-stu-id="46c9e-135">Y</span></span></td>
    <td><span data-ttu-id="46c9e-136">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-136">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="46c9e-137"><a href="http://storageexplorer.com/">Explorador de Microsoft Azure Storage</a></span><span class="sxs-lookup"><span data-stu-id="46c9e-137"><a href="http://storageexplorer.com/">Microsoft Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="46c9e-138">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-138">X</span></span></td>
    <td><span data-ttu-id="46c9e-139">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-139">X</span></span></td>
    <td><span data-ttu-id="46c9e-140">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-140">X</span></span></td>
    <td><span data-ttu-id="46c9e-141">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-141">X</span></span></td>
    <td><span data-ttu-id="46c9e-142">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-142">X</span></span></td>
    <td><span data-ttu-id="46c9e-143">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-143">X</span></span></td>
    <td><span data-ttu-id="46c9e-144">Y</span><span class="sxs-lookup"><span data-stu-id="46c9e-144">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="46c9e-145">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-145">X</span></span></td>
    <td><span data-ttu-id="46c9e-146">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-146">X</span></span></td>
    <td><span data-ttu-id="46c9e-147">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-147">X</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="46c9e-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Explorador de servidores de Microsoft Visual Studio</a></span><span class="sxs-lookup"><span data-stu-id="46c9e-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio Server Explorer</a></span></span></td>
    <td><span data-ttu-id="46c9e-149">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-149">X</span></span></td>
    <td><span data-ttu-id="46c9e-150">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-150">X</span></span></td>
    <td><span data-ttu-id="46c9e-151">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-151">X</span></span></td>
    <td><span data-ttu-id="46c9e-152">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-152">X</span></span></td>
    <td><span data-ttu-id="46c9e-153">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-153">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="46c9e-154">Y</span><span class="sxs-lookup"><span data-stu-id="46c9e-154">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="46c9e-155">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-155">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
</table>

<span data-ttu-id="46c9e-156">**Herramientas de cliente de Almacenamiento de Azure de terceros**</span><span class="sxs-lookup"><span data-stu-id="46c9e-156">**Third-Party Azure Storage Client Tools**</span></span>

<span data-ttu-id="46c9e-157">No hemos comprobado la funcionalidad de Hola o reclamado por hello siguientes herramientas de otros fabricantes y su lista de calidad no implica una aprobación por parte de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="46c9e-157">We have not verified hello functionality or quality claimed by hello following third-party tools and their listing does not imply an endorsement by Microsoft.</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="46c9e-158">Herramienta de cliente de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="46c9e-158">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="46c9e-159">Blob en bloques</span><span class="sxs-lookup"><span data-stu-id="46c9e-159">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="46c9e-160">Blob en páginas</span><span class="sxs-lookup"><span data-stu-id="46c9e-160">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="46c9e-161">Append Blob</span><span class="sxs-lookup"><span data-stu-id="46c9e-161">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="46c9e-162">Tablas</span><span class="sxs-lookup"><span data-stu-id="46c9e-162">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="46c9e-163">Colas</span><span class="sxs-lookup"><span data-stu-id="46c9e-163">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="46c9e-164">Archivos</span><span class="sxs-lookup"><span data-stu-id="46c9e-164">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="46c9e-165">Gratuito</span><span class="sxs-lookup"><span data-stu-id="46c9e-165">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="46c9e-166">Plataforma</span><span class="sxs-lookup"><span data-stu-id="46c9e-166">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="46c9e-167">Web</span><span class="sxs-lookup"><span data-stu-id="46c9e-167">Web</span></span></td>
    <td><span data-ttu-id="46c9e-168">Windows</span><span class="sxs-lookup"><span data-stu-id="46c9e-168">Windows</span></span></td>
    <td><span data-ttu-id="46c9e-169">OSX</span><span class="sxs-lookup"><span data-stu-id="46c9e-169">OSX</span></span></td>
    <td><span data-ttu-id="46c9e-170">Linux</span><span class="sxs-lookup"><span data-stu-id="46c9e-170">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="46c9e-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span><span class="sxs-lookup"><span data-stu-id="46c9e-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span></span></td>
    <td><span data-ttu-id="46c9e-172">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-172">X</span></span></td>
    <td><span data-ttu-id="46c9e-173">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-173">X</span></span></td>
    <td><span data-ttu-id="46c9e-174">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-174">X</span></span></td>
    <td><span data-ttu-id="46c9e-175">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-175">X</span></span></td>
    <td><span data-ttu-id="46c9e-176">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-176">X</span></span></td>
    <td><span data-ttu-id="46c9e-177">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-177">X</span></span></td>
    <td><span data-ttu-id="46c9e-178">Versión de prueba</span><span class="sxs-lookup"><span data-stu-id="46c9e-178">Trial</span></span></td>
    <td><span data-ttu-id="46c9e-179">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-179">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="46c9e-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span><span class="sxs-lookup"><span data-stu-id="46c9e-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span></span></td>
    <td><span data-ttu-id="46c9e-181">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-181">X</span></span></td>
    <td><span data-ttu-id="46c9e-182">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-182">X</span></span></td>
    <td><span data-ttu-id="46c9e-183">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-183">X</span></span></td>
    <td><span data-ttu-id="46c9e-184">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-184">X</span></span></td>
    <td><span data-ttu-id="46c9e-185">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-185">X</span></span></td>
    <td><span data-ttu-id="46c9e-186">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-186">X</span></span></td>
    <td><span data-ttu-id="46c9e-187">Versión de prueba</span><span class="sxs-lookup"><span data-stu-id="46c9e-187">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="46c9e-188">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-188">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="46c9e-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Explorer</a></span><span class="sxs-lookup"><span data-stu-id="46c9e-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Explorer</a></span></span></td>
    <td><span data-ttu-id="46c9e-190">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-190">X</span></span></td>
    <td><span data-ttu-id="46c9e-191">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-191">X</span></span></td>
    <td><span data-ttu-id="46c9e-192">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-192">X</span></span></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="46c9e-193">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-193">X</span></span></td>
    <td><span data-ttu-id="46c9e-194">Y</span><span class="sxs-lookup"><span data-stu-id="46c9e-194">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="46c9e-195">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-195">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="46c9e-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Explorador de almacenamiento de Azure</a></span><span class="sxs-lookup"><span data-stu-id="46c9e-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="46c9e-197">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-197">X</span></span></td>
    <td><span data-ttu-id="46c9e-198">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-198">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="46c9e-199">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-199">X</span></span></td>
    <td><span data-ttu-id="46c9e-200">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-200">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="46c9e-201">Y</span><span class="sxs-lookup"><span data-stu-id="46c9e-201">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="46c9e-202">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-202">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="46c9e-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span><span class="sxs-lookup"><span data-stu-id="46c9e-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span></span></td>
    <td><span data-ttu-id="46c9e-204">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-204">X</span></span></td>
    <td><span data-ttu-id="46c9e-205">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-205">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="46c9e-206">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-206">X</span></span></td>
    <td><span data-ttu-id="46c9e-207">S/N</span><span class="sxs-lookup"><span data-stu-id="46c9e-207">Y/N</span></span></td>
    <td></td>
    <td><span data-ttu-id="46c9e-208">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-208">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="46c9e-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span><span class="sxs-lookup"><span data-stu-id="46c9e-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span></span></td>
    <td><span data-ttu-id="46c9e-210">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-210">X</span></span></td>
    <td><span data-ttu-id="46c9e-211">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-211">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="46c9e-212">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-212">X</span></span></td>
    <td><span data-ttu-id="46c9e-213">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-213">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="46c9e-214">Versión de prueba</span><span class="sxs-lookup"><span data-stu-id="46c9e-214">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="46c9e-215">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-215">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="46c9e-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span><span class="sxs-lookup"><span data-stu-id="46c9e-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span></span></td>
    <td><span data-ttu-id="46c9e-217">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-217">X</span></span></td>
    <td><span data-ttu-id="46c9e-218">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-218">X</span></span></td>
    <td><span data-ttu-id="46c9e-219">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-219">X</span></span></td>
    <td><span data-ttu-id="46c9e-220">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-220">X</span></span></td>
    <td><span data-ttu-id="46c9e-221">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-221">X</span></span></td>
    <td><span data-ttu-id="46c9e-222">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-222">X</span></span></td>
    <td><span data-ttu-id="46c9e-223">Y</span><span class="sxs-lookup"><span data-stu-id="46c9e-223">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="46c9e-224">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-224">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="46c9e-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span><span class="sxs-lookup"><span data-stu-id="46c9e-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span></span></td>
    <td><span data-ttu-id="46c9e-226">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-226">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="46c9e-227">Versión de prueba</span><span class="sxs-lookup"><span data-stu-id="46c9e-227">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="46c9e-228">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-228">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="46c9e-229"><a href="http://storageexplorer.codeplex.com/">Azure Web Storage Explorer</a></span><span class="sxs-lookup"><span data-stu-id="46c9e-229"><a href="http://storageexplorer.codeplex.com/">Azure Web Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="46c9e-230">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-230">X</span></span></td>
    <td><span data-ttu-id="46c9e-231">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-231">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="46c9e-232">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-232">X</span></span></td>
    <td><span data-ttu-id="46c9e-233">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-233">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="46c9e-234">Y</span><span class="sxs-lookup"><span data-stu-id="46c9e-234">Y</span></span></td>
    <td><span data-ttu-id="46c9e-235">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-235">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="46c9e-236"><a href="https://zudio.co/">Zudio</a></span><span class="sxs-lookup"><span data-stu-id="46c9e-236"><a href="https://zudio.co/">Zudio</a></span></span></td>
    <td><span data-ttu-id="46c9e-237">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-237">X</span></span></td>
    <td><span data-ttu-id="46c9e-238">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-238">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="46c9e-239">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-239">X</span></span></td>
    <td><span data-ttu-id="46c9e-240">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-240">X</span></span></td>
    <td><span data-ttu-id="46c9e-241">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-241">X</span></span></td>
    <td><span data-ttu-id="46c9e-242">Versión de prueba</span><span class="sxs-lookup"><span data-stu-id="46c9e-242">Trial</span></span></td>
    <td><span data-ttu-id="46c9e-243">X</span><span class="sxs-lookup"><span data-stu-id="46c9e-243">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>
