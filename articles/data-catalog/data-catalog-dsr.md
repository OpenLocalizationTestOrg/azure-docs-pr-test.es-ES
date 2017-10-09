---
title: "aaaSupported orígenes de datos en el catálogo de datos de Azure | Documentos de Microsoft"
description: "En este artículo se enumera las especificaciones de hello admitido orígenes de datos."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: jstevens
editor: 
tags: 
ms.assetid: fd4345ca-2ed8-4c5e-9c4b-f954be2fc9f9
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 4bfcabf31bf9fd781c939a5026abc42a5407df32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="supported-data-sources-in-azure-data-catalog"></a><span data-ttu-id="ca3d7-103">Orígenes de datos compatibles en Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="ca3d7-103">Supported data sources in Azure Data Catalog</span></span>

<span data-ttu-id="ca3d7-104">Puede publicar metadatos mediante una API pública o un clic-herramienta de registro de una vez, o bien especificando información directamente toohello catálogo de datos de Azure portal web.</span><span class="sxs-lookup"><span data-stu-id="ca3d7-104">You can publish metadata by using a public API or a click-once registration tool, or by manually entering information directly toohello Azure Data Catalog web portal.</span></span> <span data-ttu-id="ca3d7-105">Hello siguiente tabla resumen todos los orígenes de datos que son compatibles con el catálogo de hello hoy y Hola funcionalidades de publicación para cada uno.</span><span class="sxs-lookup"><span data-stu-id="ca3d7-105">hello following table summarizes all data sources that are supported by hello catalog today, and hello publishing capabilities for each.</span></span> <span data-ttu-id="ca3d7-106">También se presentan Hola herramientas de datos externos que puede iniciar cada origen de datos de nuestra experiencia portal "open-in".</span><span class="sxs-lookup"><span data-stu-id="ca3d7-106">Also listed are hello external data tools that each data source can launch from our portal "open-in" experience.</span></span> <span data-ttu-id="ca3d7-107">Hola segunda tabla contiene una especificación más técnica de cada propiedad de conexión de origen de datos.</span><span class="sxs-lookup"><span data-stu-id="ca3d7-107">hello second table contains a more technical specification of each data-source connection property.</span></span>


## <a name="list-of-supported-data-sources"></a><span data-ttu-id="ca3d7-108">Lista de orígenes de datos que se admiten</span><span class="sxs-lookup"><span data-stu-id="ca3d7-108">List of supported data sources</span></span>

<table>
    <tr>
       <td><span data-ttu-id="ca3d7-109"><b>Objeto de origen de datos</b></span><span class="sxs-lookup"><span data-stu-id="ca3d7-109"><b>Data source object</b></span></span></td>
       <td><span data-ttu-id="ca3d7-110"><b>API</b></span><span class="sxs-lookup"><span data-stu-id="ca3d7-110"><b>API</b></span></span></td>
       <td><span data-ttu-id="ca3d7-111"><b>Entrada manual</b></span><span class="sxs-lookup"><span data-stu-id="ca3d7-111"><b>Manual entry</b></span></span></td>
       <td><span data-ttu-id="ca3d7-112"><b>Herramienta de registro</b></span><span class="sxs-lookup"><span data-stu-id="ca3d7-112"><b>Registration tool</b></span></span></td>
       <td><span data-ttu-id="ca3d7-113"><b>Herramientas abiertas</b></span><span class="sxs-lookup"><span data-stu-id="ca3d7-113"><b>Open-in tools</b></span></span></td>
       <td><span data-ttu-id="ca3d7-114"><b>Notas</b></span><span class="sxs-lookup"><span data-stu-id="ca3d7-114"><b>Notes</b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-115">Directorio de Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ca3d7-115">Azure Data Lake Store directory</span></span></td>
      <td><span data-ttu-id="ca3d7-116">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-116">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-117">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-117">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-118">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-118">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-119">Archivo de Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ca3d7-119">Azure Data Lake Store file</span></span></td>
      <td><span data-ttu-id="ca3d7-120">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-120">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-121">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-121">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-122">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-122">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-123">Almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="ca3d7-123">Azure Blob storage</span></span></td>
      <td><span data-ttu-id="ca3d7-124">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-124">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-125">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-125">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-126">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-126">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-127"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-127"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-128">Directorio de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="ca3d7-128">Azure Storage directory</span></span></td>
      <td><span data-ttu-id="ca3d7-129">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-129">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-130">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-130">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-131">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-131">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-132"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-132"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-133">Tabla de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="ca3d7-133">Azure Storage table</span></span></td>
      <td><span data-ttu-id="ca3d7-134">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-134">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-135">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-135">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-136">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-136">✓</span></span></td>
      <td>
        <font size="2"></font>
      </td>
      <td>
        <font size="2"></font>
      </td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-137">Directorio de HDFS</span><span class="sxs-lookup"><span data-stu-id="ca3d7-137">HDFS directory</span></span></td>
      <td><span data-ttu-id="ca3d7-138">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-138">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-139">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-139">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-140">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-140">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-141">Archivo de HDFS</span><span class="sxs-lookup"><span data-stu-id="ca3d7-141">HDFS file</span></span></td>
      <td><span data-ttu-id="ca3d7-142">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-142">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-143">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-143">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-144">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-144">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-145">Tabla de Hive</span><span class="sxs-lookup"><span data-stu-id="ca3d7-145">Hive table</span></span></td>
      <td><span data-ttu-id="ca3d7-146">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-146">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-147">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-147">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-148">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-148">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-149"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-149"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-150">Vista de Hive</span><span class="sxs-lookup"><span data-stu-id="ca3d7-150">Hive view</span></span></td>
      <td><span data-ttu-id="ca3d7-151">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-151">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-152">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-152">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-153">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-153">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-154"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-154"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-155">Tabla de MySQL</span><span class="sxs-lookup"><span data-stu-id="ca3d7-155">MySQL table</span></span></td>
      <td><span data-ttu-id="ca3d7-156">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-156">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-157">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-157">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-158">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-158">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-159"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-159"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-160">Vista de MySQL</span><span class="sxs-lookup"><span data-stu-id="ca3d7-160">MySQL view</span></span></td>
      <td><span data-ttu-id="ca3d7-161">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-161">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-162">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-162">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-163">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-163">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-164"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-164"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-165">Tabla de Oracle Database</span><span class="sxs-lookup"><span data-stu-id="ca3d7-165">Oracle Database table</span></span></td>
      <td><span data-ttu-id="ca3d7-166">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-166">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-167">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-167">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-168">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-168">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-169"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-169"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-170">Vista de Oracle Database</span><span class="sxs-lookup"><span data-stu-id="ca3d7-170">Oracle Database view</span></span></td>
      <td><span data-ttu-id="ca3d7-171">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-171">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-172">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-172">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-173">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-173">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-174"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-174"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-175">Otro (recurso genérico)</span><span class="sxs-lookup"><span data-stu-id="ca3d7-175">Other (generic asset)</span></span></td>
      <td><span data-ttu-id="ca3d7-176">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-176">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-177">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-177">✓</span></span></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-178">Tabla de Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ca3d7-178">Azure SQL Data Warehouse table</span></span></td>
      <td><span data-ttu-id="ca3d7-179">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-179">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-180">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-180">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-181">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-181">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-182"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-182"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-183">Vista de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ca3d7-183">SQL Data Warehouse view</span></span></td>
      <td><span data-ttu-id="ca3d7-184">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-184">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-185">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-185">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-186">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-186">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-187"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-187"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-188">Dimensión de SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-188">SQL Server Analysis Services dimension</span></span></td>
      <td><span data-ttu-id="ca3d7-189">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-189">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-190">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-190">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-191">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-191">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-192"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-192"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-193">KPI de SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-193">SQL Server Analysis Services KPI</span></span></td>
      <td><span data-ttu-id="ca3d7-194">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-194">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-195">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-195">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-196">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-196">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-197"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-197"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-198">Medida de SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-198">SQL Server Analysis Services measure</span></span></td>
      <td><span data-ttu-id="ca3d7-199">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-199">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-200">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-200">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-201">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-201">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-202"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-202"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-203">Tabla de SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-203">SQL Server Analysis Services table</span></span></td>
      <td><span data-ttu-id="ca3d7-204">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-204">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-205">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-205">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-206">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-206">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-207"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-207"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-208">Informe de SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-208">SQL Server Reporting Services report</span></span></td>
      <td><span data-ttu-id="ca3d7-209">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-209">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-210">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-210">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-211">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-211">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-212"><font size=2>Browser</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-212"><font size=2>Browser</font></span></span></td>
      <td><span data-ttu-id="ca3d7-213"><font size=2>Solo servidores de modo nativo. No se admite el modo de SharePoint.</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-213"><font size=2>Native mode servers only. SharePoint mode is not supported.</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-214">Tabla de SQL Server</span><span class="sxs-lookup"><span data-stu-id="ca3d7-214">SQL Server table</span></span></td>
      <td><span data-ttu-id="ca3d7-215">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-215">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-216">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-216">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-217">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-217">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-218"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-218"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-219">Vista de SQL Server</span><span class="sxs-lookup"><span data-stu-id="ca3d7-219">SQL Server view</span></span></td>
      <td><span data-ttu-id="ca3d7-220">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-220">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-221">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-221">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-222">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-222">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-223"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-223"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-224">Tabla de Teradata</span><span class="sxs-lookup"><span data-stu-id="ca3d7-224">Teradata table</span></span></td>
      <td><span data-ttu-id="ca3d7-225">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-225">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-226">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-226">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-227">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-227">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-228"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-228"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-229">Vista de Teradata</span><span class="sxs-lookup"><span data-stu-id="ca3d7-229">Teradata view</span></span></td>
      <td><span data-ttu-id="ca3d7-230">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-230">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-231">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-231">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-232">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-232">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-233"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-233"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-234">Vista de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="ca3d7-234">SAP HANA view</span></span></td>
      <td><span data-ttu-id="ca3d7-235">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-235">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-236">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-236">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-237">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-237">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-238"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-238"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-239">Tabla de DB2</span><span class="sxs-lookup"><span data-stu-id="ca3d7-239">DB2 table</span></span></td>
      <td><span data-ttu-id="ca3d7-240">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-240">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-241">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-241">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-242">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-242">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-243">Vista de DB2</span><span class="sxs-lookup"><span data-stu-id="ca3d7-243">DB2 view</span></span></td>
      <td><span data-ttu-id="ca3d7-244">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-244">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-245">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-245">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-246">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-246">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-247">Archivo de sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-247">File system file</span></span></td>
      <td><span data-ttu-id="ca3d7-248">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-248">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-249">Directorio FTP</span><span class="sxs-lookup"><span data-stu-id="ca3d7-249">FTP directory</span></span></td>
      <td><span data-ttu-id="ca3d7-250">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-250">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-251">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-251">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-252">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-252">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-253">Archivo FTP</span><span class="sxs-lookup"><span data-stu-id="ca3d7-253">FTP file</span></span></td>
      <td><span data-ttu-id="ca3d7-254">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-254">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-255">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-255">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-256">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-256">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-257">Informe HTTP</span><span class="sxs-lookup"><span data-stu-id="ca3d7-257">HTTP report</span></span></td>
      <td><span data-ttu-id="ca3d7-258">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-258">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-259">Punto de conexión HTTP</span><span class="sxs-lookup"><span data-stu-id="ca3d7-259">HTTP endpoint</span></span></td>
      <td><span data-ttu-id="ca3d7-260">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-260">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-261">Archivo HTTP</span><span class="sxs-lookup"><span data-stu-id="ca3d7-261">HTTP file</span></span></td>
      <td><span data-ttu-id="ca3d7-262">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-262">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-263">Conjunto de entidades de OData</span><span class="sxs-lookup"><span data-stu-id="ca3d7-263">OData entity set</span></span></td>
      <td><span data-ttu-id="ca3d7-264">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-264">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-265">Función de OData</span><span class="sxs-lookup"><span data-stu-id="ca3d7-265">OData function</span></span></td>
      <td><span data-ttu-id="ca3d7-266">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-266">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-267">Tabla de PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ca3d7-267">PostgreSQL table</span></span></td>
      <td><span data-ttu-id="ca3d7-268">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-268">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-269">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-269">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-270">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-270">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-271">Vista de PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ca3d7-271">PostgreSQL view</span></span></td>
      <td><span data-ttu-id="ca3d7-272">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-272">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-273">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-273">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-274">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-274">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-275">Vista de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="ca3d7-275">SAP HANA view</span></span></td>
      <td><span data-ttu-id="ca3d7-276">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-276">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td> <span data-ttu-id="ca3d7-277">Objeto de Salesforce</span><span class="sxs-lookup"><span data-stu-id="ca3d7-277">Salesforce object</span></span></td>
      <td><span data-ttu-id="ca3d7-278">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-278">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-279">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-279">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-280">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-280">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-281">Lista de SharePoint</span><span class="sxs-lookup"><span data-stu-id="ca3d7-281">SharePoint list</span></span> </td>
      <td><span data-ttu-id="ca3d7-282">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-282">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-283">Colección de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ca3d7-283">Azure Cosmos DB collection</span></span></td>
      <td><span data-ttu-id="ca3d7-284">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-284">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-285">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-285">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-286">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-286">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-287">Tabla ODBC genérica</span><span class="sxs-lookup"><span data-stu-id="ca3d7-287">Generic ODBC table</span></span></td>
      <td><span data-ttu-id="ca3d7-288">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-288">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-289">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-289">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-290">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-290">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-291">Vista de ODBC genérica</span><span class="sxs-lookup"><span data-stu-id="ca3d7-291">Generic ODBC view</span></span></td>
      <td><span data-ttu-id="ca3d7-292">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-292">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-293">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-293">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-294">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-294">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-295">Tabla de Cassandra</span><span class="sxs-lookup"><span data-stu-id="ca3d7-295">Cassandra table</span></span></td>
      <td><span data-ttu-id="ca3d7-296">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-296">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-297">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-297">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-298">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-298">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="ca3d7-299"><font size=2>Publicar como un recurso ODBC genérico</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-299"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-300">Vista de Cassandra</span><span class="sxs-lookup"><span data-stu-id="ca3d7-300">Cassandra view</span></span></td>
      <td><span data-ttu-id="ca3d7-301">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-301">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-302">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-302">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-303">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-303">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="ca3d7-304"><font size=2>Publicar como un recurso ODBC genérico</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-304"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-305">Tabla de Sybase</span><span class="sxs-lookup"><span data-stu-id="ca3d7-305">Sybase table</span></span></td>
      <td><span data-ttu-id="ca3d7-306">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-306">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-307">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-307">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-308">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-308">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-309">Vista de Sybase</span><span class="sxs-lookup"><span data-stu-id="ca3d7-309">Sybase view</span></span></td>
      <td><span data-ttu-id="ca3d7-310">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-310">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-311">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-311">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-312">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-312">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-313">Tabla de MongoDB</span><span class="sxs-lookup"><span data-stu-id="ca3d7-313">MongoDB table</span></span></td>
      <td><span data-ttu-id="ca3d7-314">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-314">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-315">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-315">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-316">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-316">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="ca3d7-317"><font size=2>Publicar como un recurso ODBC genérico</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-317"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-318">Vista de MongoDB</span><span class="sxs-lookup"><span data-stu-id="ca3d7-318">MongoDB view</span></span></td>
      <td><span data-ttu-id="ca3d7-319">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-319">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-320">✓ </span><span class="sxs-lookup"><span data-stu-id="ca3d7-320">✓</span></span></td>
      <td><span data-ttu-id="ca3d7-321">✓</span><span class="sxs-lookup"><span data-stu-id="ca3d7-321">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="ca3d7-322"><font size=2>Publicar como un recurso ODBC genérico</font></span><span class="sxs-lookup"><span data-stu-id="ca3d7-322"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
</table>

<span data-ttu-id="ca3d7-323">Si necesita compatibilidad con fuentes adicionales, envíe un toohello de solicitud de característica [foro del catálogo de datos de Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="ca3d7-323">If you need support for additional sources, submit a feature request toohello [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span></span>


## <a name="data-source-reference-specification"></a><span data-ttu-id="ca3d7-324">Especificación de referencia de origen de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-324">Data-source reference specification</span></span>
> [!NOTE]
> <span data-ttu-id="ca3d7-325">Hola **estructura DSL** columna de hello en la tabla siguiente muestra únicamente Hola propiedades de conexión para la bolsa de propiedades de "dirección" que se usan el catálogo de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ca3d7-325">hello **DSL structure** column in hello following table lists only hello connection properties for "address" property bag that are used by Azure Data Catalog.</span></span> <span data-ttu-id="ca3d7-326">Es decir, la bolsa de propiedades de "dirección" puede contener otras propiedades de conexión de origen de datos de Hola que continúa el catálogo de datos, pero no la usa.</span><span class="sxs-lookup"><span data-stu-id="ca3d7-326">That is, "address" property bag can contain other connection properties of hello data source which Azure Data Catalog persists, but does not use.</span></span>

<table>
    <tr>
       <td><span data-ttu-id="ca3d7-327"><b>Tipo de origen</b></span><span class="sxs-lookup"><span data-stu-id="ca3d7-327"><b>Source type</b></span></span></td>
       <td><span data-ttu-id="ca3d7-328"><b>Tipo de recurso</b></span><span class="sxs-lookup"><span data-stu-id="ca3d7-328"><b>Asset type</b></span></span></td>
       <td><span data-ttu-id="ca3d7-329"><b>Tipos de objeto</b></span><span class="sxs-lookup"><span data-stu-id="ca3d7-329"><b>Object types</b></span></span></td>
       <td><span data-ttu-id="ca3d7-330"><b>Estructura de DSL<b></span><span class="sxs-lookup"><span data-stu-id="ca3d7-330"><b>DSL structure<b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-331">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="ca3d7-331">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="ca3d7-332">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-332">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-333">Data Lake</span><span class="sxs-lookup"><span data-stu-id="ca3d7-333">Data Lake</span></span></td>
      <td><span data-ttu-id="ca3d7-334">
        <font size=2> Protocolo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="ca3d7-334">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="ca3d7-335">Autenticación: {básica, oauth}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-335">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="ca3d7-336">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-336">Address:</span></span> <br><span data-ttu-id="ca3d7-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-338">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="ca3d7-338">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="ca3d7-339">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-339">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-340">Directorio, archivo</span><span class="sxs-lookup"><span data-stu-id="ca3d7-340">Directory, file</span></span></td>
      <td><span data-ttu-id="ca3d7-341">
        <font size=2> Protocolo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="ca3d7-341">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="ca3d7-342">Autenticación: {básica, oauth}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-342">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="ca3d7-343">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-343">Address:</span></span> <br><span data-ttu-id="ca3d7-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-345">Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ca3d7-345">Azure Storage</span></span></td>
      <td><span data-ttu-id="ca3d7-346">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-346">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-347">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-347">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-348">
        <font size=2> Protocolo: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="ca3d7-348">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="ca3d7-349">Autenticación: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-349">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="ca3d7-350">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-350">Address:</span></span> <br><span data-ttu-id="ca3d7-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; dominio</span><span class="sxs-lookup"><span data-stu-id="ca3d7-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="ca3d7-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cuenta</span><span class="sxs-lookup"><span data-stu-id="ca3d7-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="ca3d7-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; contenedor</font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-354">Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ca3d7-354">Azure Storage</span></span></td>
      <td><span data-ttu-id="ca3d7-355">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-355">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-356">Blob, directorio</span><span class="sxs-lookup"><span data-stu-id="ca3d7-356">Blob, directory</span></span></td>
      <td><span data-ttu-id="ca3d7-357">
        <font size=2> Protocolo: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="ca3d7-357">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="ca3d7-358">Autenticación: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-358">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="ca3d7-359">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-359">Address:</span></span> <br><span data-ttu-id="ca3d7-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; dominio</span><span class="sxs-lookup"><span data-stu-id="ca3d7-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="ca3d7-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cuenta</span><span class="sxs-lookup"><span data-stu-id="ca3d7-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="ca3d7-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container</span></span> <br><span data-ttu-id="ca3d7-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; nombre </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-364">Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ca3d7-364">Azure Storage</span></span></td>
      <td><span data-ttu-id="ca3d7-365">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-365">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-366">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-366">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-367">
        <font size=2> Protocolo: azure-tables</span><span class="sxs-lookup"><span data-stu-id="ca3d7-367">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="ca3d7-368">Autenticación: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-368">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="ca3d7-369">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-369">Address:</span></span> <br><span data-ttu-id="ca3d7-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; dominio</span><span class="sxs-lookup"><span data-stu-id="ca3d7-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="ca3d7-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cuenta</font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-372">Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ca3d7-372">Azure Storage</span></span></td>
      <td><span data-ttu-id="ca3d7-373">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-373">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-374">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-374">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-375">
        <font size=2> Protocolo: azure-tables</span><span class="sxs-lookup"><span data-stu-id="ca3d7-375">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="ca3d7-376">Autenticación: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-376">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="ca3d7-377">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-377">Address:</span></span> <br><span data-ttu-id="ca3d7-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; dominio</span><span class="sxs-lookup"><span data-stu-id="ca3d7-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="ca3d7-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cuenta</span><span class="sxs-lookup"><span data-stu-id="ca3d7-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="ca3d7-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; nombre </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-381">Cosmos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-381">Cosmos</span></span></td>
      <td><span data-ttu-id="ca3d7-382">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-382">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-383">Clúster virtual</span><span class="sxs-lookup"><span data-stu-id="ca3d7-383">Virtual cluster</span></span></td>
      <td><span data-ttu-id="ca3d7-384">
        <font size=2> Protocolo: cosmos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-384">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="ca3d7-385">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-385">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ca3d7-386">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-386">Address:</span></span> <br><span data-ttu-id="ca3d7-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-388">Cosmos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-388">Cosmos</span></span></td>
      <td><span data-ttu-id="ca3d7-389">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-389">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-390">Transmisión, conjunto de transmisiones, vista</span><span class="sxs-lookup"><span data-stu-id="ca3d7-390">Stream, stream set, view</span></span></td>
      <td><span data-ttu-id="ca3d7-391">
        <font size=2> Protocolo: cosmos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-391">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="ca3d7-392">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-392">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ca3d7-393">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-393">Address:</span></span> <br><span data-ttu-id="ca3d7-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-395">Datazen</span><span class="sxs-lookup"><span data-stu-id="ca3d7-395">Datazen</span></span></td>
      <td><span data-ttu-id="ca3d7-396">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-396">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-397">Sitio</span><span class="sxs-lookup"><span data-stu-id="ca3d7-397">Site</span></span></td>
      <td><span data-ttu-id="ca3d7-398">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="ca3d7-398">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="ca3d7-399">Autenticación: {no, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-399">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="ca3d7-400">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-400">Address:</span></span> <br><span data-ttu-id="ca3d7-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-402">Datazen</span><span class="sxs-lookup"><span data-stu-id="ca3d7-402">Datazen</span></span></td>
      <td><span data-ttu-id="ca3d7-403">Informe</span><span class="sxs-lookup"><span data-stu-id="ca3d7-403">Report</span></span></td>
      <td><span data-ttu-id="ca3d7-404">Informe, panel</span><span class="sxs-lookup"><span data-stu-id="ca3d7-404">Report, dashboard</span></span></td>
      <td><span data-ttu-id="ca3d7-405">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="ca3d7-405">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="ca3d7-406">Autenticación: {no, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-406">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="ca3d7-407">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-407">Address:</span></span> <br><span data-ttu-id="ca3d7-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-409">DB2</span><span class="sxs-lookup"><span data-stu-id="ca3d7-409">DB2</span></span></td>
      <td><span data-ttu-id="ca3d7-410">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-410">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-411">Base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-411">Database</span></span></td>
      <td><span data-ttu-id="ca3d7-412">
        <font size=2> Protocolo: db2</span><span class="sxs-lookup"><span data-stu-id="ca3d7-412">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="ca3d7-413">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-413">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ca3d7-414">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-414">Address:</span></span> <br><span data-ttu-id="ca3d7-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-417">DB2</span><span class="sxs-lookup"><span data-stu-id="ca3d7-417">DB2</span></span></td>
      <td><span data-ttu-id="ca3d7-418">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-418">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-419">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="ca3d7-419">Table, view</span></span></td>
      <td><span data-ttu-id="ca3d7-420">
        <font size=2> Protocolo: db2</span><span class="sxs-lookup"><span data-stu-id="ca3d7-420">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="ca3d7-421">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-421">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ca3d7-422">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-422">Address:</span></span> <br><span data-ttu-id="ca3d7-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="ca3d7-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="ca3d7-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-427">Sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-427">File system</span></span></td>
      <td><span data-ttu-id="ca3d7-428">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-428">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-429">Archivo</span><span class="sxs-lookup"><span data-stu-id="ca3d7-429">File</span></span></td>
      <td><span data-ttu-id="ca3d7-430">
        <font size=2> Protocolo: archivo</span><span class="sxs-lookup"><span data-stu-id="ca3d7-430">
        <font size=2> Protocol: file</span></span> <br><span data-ttu-id="ca3d7-431">Autenticación: {no, básica, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-431">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="ca3d7-432">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-432">Address:</span></span> <br><span data-ttu-id="ca3d7-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ruta de acceso </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-434">FTP</span><span class="sxs-lookup"><span data-stu-id="ca3d7-434">FTP</span></span></td>
      <td><span data-ttu-id="ca3d7-435">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-435">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-436">Directorio, archivo</span><span class="sxs-lookup"><span data-stu-id="ca3d7-436">Directory, file</span></span></td>
      <td><span data-ttu-id="ca3d7-437">
        <font size=2> Protocolo: ftp</span><span class="sxs-lookup"><span data-stu-id="ca3d7-437">
        <font size=2> Protocol: ftp</span></span> <br><span data-ttu-id="ca3d7-438">Autenticación: {no, básica, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-438">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="ca3d7-439">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-439">Address:</span></span> <br><span data-ttu-id="ca3d7-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-441">sistema de archivos distribuido de Hadoop</span><span class="sxs-lookup"><span data-stu-id="ca3d7-441">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="ca3d7-442">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-442">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-443">Clúster</span><span class="sxs-lookup"><span data-stu-id="ca3d7-443">Cluster</span></span></td>
      <td><span data-ttu-id="ca3d7-444">
        <font size=2> Protocolo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="ca3d7-444">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="ca3d7-445">Autenticación: {básica, oauth}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-445">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="ca3d7-446">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-446">Address:</span></span> <br><span data-ttu-id="ca3d7-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-448">sistema de archivos distribuido de Hadoop</span><span class="sxs-lookup"><span data-stu-id="ca3d7-448">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="ca3d7-449">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-449">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-450">Directorio, archivo</span><span class="sxs-lookup"><span data-stu-id="ca3d7-450">Directory, file</span></span></td>
      <td><span data-ttu-id="ca3d7-451">
        <font size=2> Protocolo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="ca3d7-451">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="ca3d7-452">Autenticación: {básica, oauth}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-452">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="ca3d7-453">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-453">Address:</span></span> <br><span data-ttu-id="ca3d7-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-455">Hive</span><span class="sxs-lookup"><span data-stu-id="ca3d7-455">Hive</span></span></td>
      <td><span data-ttu-id="ca3d7-456">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-456">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-457">Base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-457">Database</span></span></td>
      <td><span data-ttu-id="ca3d7-458">
        <font size=2> Protocolo: hive</span><span class="sxs-lookup"><span data-stu-id="ca3d7-458">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="ca3d7-459">Autenticación: {hdinsight, básica, nombre de usuario, no}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-459">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="ca3d7-460">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-460">Address:</span></span> <br><span data-ttu-id="ca3d7-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-463">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-463">connectionProperties:</span></span> <br><span data-ttu-id="ca3d7-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-465">Hive</span><span class="sxs-lookup"><span data-stu-id="ca3d7-465">Hive</span></span></td>
      <td><span data-ttu-id="ca3d7-466">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-466">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-467">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="ca3d7-467">Table, view</span></span></td>
      <td><span data-ttu-id="ca3d7-468">
        <font size=2> Protocolo: hive</span><span class="sxs-lookup"><span data-stu-id="ca3d7-468">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="ca3d7-469">Autenticación: {hdinsight, básica, nombre de usuario, no}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-469">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="ca3d7-470">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-470">Address:</span></span> <br><span data-ttu-id="ca3d7-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="ca3d7-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="ca3d7-474">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-474">connectionProperties:</span></span> <br><span data-ttu-id="ca3d7-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-476">http</span><span class="sxs-lookup"><span data-stu-id="ca3d7-476">HTTP</span></span></td>
      <td><span data-ttu-id="ca3d7-477">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-477">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-478">Sitio</span><span class="sxs-lookup"><span data-stu-id="ca3d7-478">Site</span></span></td>
      <td><span data-ttu-id="ca3d7-479">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="ca3d7-479">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="ca3d7-480">Autenticación: {no, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-480">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="ca3d7-481">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-481">Address:</span></span> <br><span data-ttu-id="ca3d7-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-483">http</span><span class="sxs-lookup"><span data-stu-id="ca3d7-483">HTTP</span></span></td>
      <td><span data-ttu-id="ca3d7-484">Informe</span><span class="sxs-lookup"><span data-stu-id="ca3d7-484">Report</span></span></td>
      <td><span data-ttu-id="ca3d7-485">Informe, panel</span><span class="sxs-lookup"><span data-stu-id="ca3d7-485">Report, dashboard</span></span></td>
      <td><span data-ttu-id="ca3d7-486">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="ca3d7-486">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="ca3d7-487">Autenticación: {no, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-487">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="ca3d7-488">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-488">Address:</span></span> <br><span data-ttu-id="ca3d7-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-490">http</span><span class="sxs-lookup"><span data-stu-id="ca3d7-490">HTTP</span></span></td>
      <td><span data-ttu-id="ca3d7-491">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-491">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-492">Punto de conexión, archivo</span><span class="sxs-lookup"><span data-stu-id="ca3d7-492">Endpoint, file</span></span></td>
      <td><span data-ttu-id="ca3d7-493">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="ca3d7-493">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="ca3d7-494">Autenticación: {no, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-494">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="ca3d7-495">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-495">Address:</span></span> <br><span data-ttu-id="ca3d7-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-497">MySQL</span><span class="sxs-lookup"><span data-stu-id="ca3d7-497">MySQL</span></span></td>
      <td><span data-ttu-id="ca3d7-498">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-498">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-499">Base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-499">Database</span></span></td>
      <td><span data-ttu-id="ca3d7-500">
        <font size=2> Protocolo: mysql</span><span class="sxs-lookup"><span data-stu-id="ca3d7-500">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="ca3d7-501">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-501">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ca3d7-502">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-502">Address:</span></span> <br><span data-ttu-id="ca3d7-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-505">MySQL</span><span class="sxs-lookup"><span data-stu-id="ca3d7-505">MySQL</span></span></td>
      <td><span data-ttu-id="ca3d7-506">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-506">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-507">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="ca3d7-507">Table, view</span></span></td>
      <td><span data-ttu-id="ca3d7-508">
        <font size=2> Protocolo: mysql</span><span class="sxs-lookup"><span data-stu-id="ca3d7-508">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="ca3d7-509">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-509">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ca3d7-510">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-510">Address:</span></span> <br><span data-ttu-id="ca3d7-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-514">OData</span><span class="sxs-lookup"><span data-stu-id="ca3d7-514">OData</span></span></td>
      <td><span data-ttu-id="ca3d7-515">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-515">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-516">Contenedor de entidades</span><span class="sxs-lookup"><span data-stu-id="ca3d7-516">Entity container</span></span></td>
      <td><span data-ttu-id="ca3d7-517">
        <font size=2> Protocolo: odata</span><span class="sxs-lookup"><span data-stu-id="ca3d7-517">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="ca3d7-518">Autenticación: {no, básica, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-518">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="ca3d7-519">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-519">Address:</span></span> <br><span data-ttu-id="ca3d7-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-521">OData</span><span class="sxs-lookup"><span data-stu-id="ca3d7-521">OData</span></span></td>
      <td><span data-ttu-id="ca3d7-522">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-522">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-523">Conjunto de entidades, función</span><span class="sxs-lookup"><span data-stu-id="ca3d7-523">Entity set, function</span></span></td>
      <td><span data-ttu-id="ca3d7-524">
        <font size=2> Protocolo: odata</span><span class="sxs-lookup"><span data-stu-id="ca3d7-524">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="ca3d7-525">Autenticación: {no, básica, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-525">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="ca3d7-526">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-526">Address:</span></span> <br><span data-ttu-id="ca3d7-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="ca3d7-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="ca3d7-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; recurso </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-529">Base de datos de Oracle</span><span class="sxs-lookup"><span data-stu-id="ca3d7-529">Oracle Database</span></span></td>
      <td><span data-ttu-id="ca3d7-530">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-530">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-531">Base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-531">Database</span></span></td>
      <td><span data-ttu-id="ca3d7-532">
        <font size=2> Protocolo: oracle</span><span class="sxs-lookup"><span data-stu-id="ca3d7-532">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="ca3d7-533">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-533">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ca3d7-534">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-534">Address:</span></span> <br><span data-ttu-id="ca3d7-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-537">Base de datos de Oracle</span><span class="sxs-lookup"><span data-stu-id="ca3d7-537">Oracle Database</span></span></td>
      <td><span data-ttu-id="ca3d7-538">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-538">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-539">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="ca3d7-539">Table, view</span></span></td>
      <td><span data-ttu-id="ca3d7-540">
        <font size=2> Protocolo: oracle</span><span class="sxs-lookup"><span data-stu-id="ca3d7-540">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="ca3d7-541">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-541">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ca3d7-542">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-542">Address:</span></span> <br><span data-ttu-id="ca3d7-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="ca3d7-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ca3d7-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-547">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ca3d7-547">PostgreSQL</span></span></td>
      <td><span data-ttu-id="ca3d7-548">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-548">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-549">Base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-549">Database</span></span></td>
      <td><span data-ttu-id="ca3d7-550">
        <font size=2> Protocolo: postgresql</span><span class="sxs-lookup"><span data-stu-id="ca3d7-550">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="ca3d7-551">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-551">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ca3d7-552">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-552">Address:</span></span> <br><span data-ttu-id="ca3d7-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-555">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ca3d7-555">PostgreSQL</span></span></td>
      <td><span data-ttu-id="ca3d7-556">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-556">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-557">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="ca3d7-557">Table, view</span></span></td>
      <td><span data-ttu-id="ca3d7-558">
        <font size=2> Protocolo: postgresql</span><span class="sxs-lookup"><span data-stu-id="ca3d7-558">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="ca3d7-559">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-559">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ca3d7-560">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-560">Address:</span></span> <br><span data-ttu-id="ca3d7-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="ca3d7-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ca3d7-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-565">Power BI</span><span class="sxs-lookup"><span data-stu-id="ca3d7-565">Power BI</span></span></td>
      <td><span data-ttu-id="ca3d7-566">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-566">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-567">Sitio</span><span class="sxs-lookup"><span data-stu-id="ca3d7-567">Site</span></span></td>
      <td><span data-ttu-id="ca3d7-568">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="ca3d7-568">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="ca3d7-569">Autenticación: {no, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-569">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="ca3d7-570">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-570">Address:</span></span> <br><span data-ttu-id="ca3d7-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-572">Power BI</span><span class="sxs-lookup"><span data-stu-id="ca3d7-572">Power BI</span></span></td>
      <td><span data-ttu-id="ca3d7-573">Informe</span><span class="sxs-lookup"><span data-stu-id="ca3d7-573">Report</span></span></td>
      <td><span data-ttu-id="ca3d7-574">Informe, panel</span><span class="sxs-lookup"><span data-stu-id="ca3d7-574">Report, dashboard</span></span></td>
      <td><span data-ttu-id="ca3d7-575">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="ca3d7-575">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="ca3d7-576">Autenticación: {no, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-576">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="ca3d7-577">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-577">Address:</span></span> <br><span data-ttu-id="ca3d7-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-579">Power Query</span><span class="sxs-lookup"><span data-stu-id="ca3d7-579">Power Query</span></span></td>
      <td><span data-ttu-id="ca3d7-580">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-580">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-581">Mashup de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-581">Data mashup</span></span></td>
      <td><span data-ttu-id="ca3d7-582">
        <font size=2>Protocolo: power-query</span><span class="sxs-lookup"><span data-stu-id="ca3d7-582">
        <font size=2> Protocol: power-query</span></span> <br><span data-ttu-id="ca3d7-583">Autenticación: {oauth}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-583">Authentication: {oauth}</span></span> <br><span data-ttu-id="ca3d7-584">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-584">Address:</span></span> <br><span data-ttu-id="ca3d7-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-586">Salesforce</span><span class="sxs-lookup"><span data-stu-id="ca3d7-586">Salesforce</span></span></td>
      <td><span data-ttu-id="ca3d7-587">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-587">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-588">Objeto</span><span class="sxs-lookup"><span data-stu-id="ca3d7-588">Object</span></span></td>
      <td><span data-ttu-id="ca3d7-589">
        <font size=2> Protocolo: salesforce-com</span><span class="sxs-lookup"><span data-stu-id="ca3d7-589">
        <font size=2> Protocol: salesforce-com</span></span> <br><span data-ttu-id="ca3d7-590">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-590">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ca3d7-591">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-591">Address:</span></span> <br><span data-ttu-id="ca3d7-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span><span class="sxs-lookup"><span data-stu-id="ca3d7-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span></span> <br><span data-ttu-id="ca3d7-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span><span class="sxs-lookup"><span data-stu-id="ca3d7-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span></span> <br><span data-ttu-id="ca3d7-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-595">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="ca3d7-595">SAP HANA</span></span></td>
      <td><span data-ttu-id="ca3d7-596">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-596">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-597">Server</span><span class="sxs-lookup"><span data-stu-id="ca3d7-597">Server</span></span></td>
      <td><span data-ttu-id="ca3d7-598">
        <font size=2> Protocolo: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="ca3d7-598">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="ca3d7-599">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-599">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ca3d7-600">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-600">Address:</span></span> <br><span data-ttu-id="ca3d7-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-602">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="ca3d7-602">SAP HANA</span></span></td>
      <td><span data-ttu-id="ca3d7-603">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-603">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-604">Ver</span><span class="sxs-lookup"><span data-stu-id="ca3d7-604">View</span></span></td>
      <td><span data-ttu-id="ca3d7-605">
        <font size=2> Protocolo: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="ca3d7-605">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="ca3d7-606">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-606">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ca3d7-607">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-607">Address:</span></span> <br><span data-ttu-id="ca3d7-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="ca3d7-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ca3d7-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-611">SharePoint</span><span class="sxs-lookup"><span data-stu-id="ca3d7-611">SharePoint</span></span></td>
      <td><span data-ttu-id="ca3d7-612">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-612">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-613">Enumerar</span><span class="sxs-lookup"><span data-stu-id="ca3d7-613">List</span></span></td>
      <td><span data-ttu-id="ca3d7-614">
        <font size=2> Protocolo: sharepoint-list</span><span class="sxs-lookup"><span data-stu-id="ca3d7-614">
        <font size=2> Protocol: sharepoint-list</span></span> <br><span data-ttu-id="ca3d7-615">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-615">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ca3d7-616">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-616">Address:</span></span> <br><span data-ttu-id="ca3d7-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-618">Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="ca3d7-618">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="ca3d7-619">Comando</span><span class="sxs-lookup"><span data-stu-id="ca3d7-619">Command</span></span></td>
      <td><span data-ttu-id="ca3d7-620">Procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="ca3d7-620">Stored procedure</span></span></td>
      <td><span data-ttu-id="ca3d7-621">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="ca3d7-621">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="ca3d7-622">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-622">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ca3d7-623">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-623">Address:</span></span> <br><span data-ttu-id="ca3d7-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="ca3d7-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ca3d7-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-628">Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="ca3d7-628">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="ca3d7-629">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="ca3d7-629">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="ca3d7-630">Función con valores de tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-630">Table-valued function</span></span></td>
      <td><span data-ttu-id="ca3d7-631">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="ca3d7-631">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="ca3d7-632">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-632">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ca3d7-633">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-633">Address:</span></span> <br><span data-ttu-id="ca3d7-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="ca3d7-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ca3d7-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-638">Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="ca3d7-638">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="ca3d7-639">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-639">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-640">Base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-640">Database</span></span></td>
      <td><span data-ttu-id="ca3d7-641">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="ca3d7-641">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="ca3d7-642">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-642">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ca3d7-643">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-643">Address:</span></span> <br><span data-ttu-id="ca3d7-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-646">Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="ca3d7-646">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="ca3d7-647">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-647">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-648">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="ca3d7-648">Table, view</span></span></td>
      <td><span data-ttu-id="ca3d7-649">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="ca3d7-649">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="ca3d7-650">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-650">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ca3d7-651">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-651">Address:</span></span> <br><span data-ttu-id="ca3d7-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="ca3d7-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ca3d7-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-656">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ca3d7-656">SQL Server</span></span></td>
      <td><span data-ttu-id="ca3d7-657">Comando</span><span class="sxs-lookup"><span data-stu-id="ca3d7-657">Command</span></span></td>
      <td><span data-ttu-id="ca3d7-658">Procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="ca3d7-658">Stored procedure</span></span></td>
      <td><span data-ttu-id="ca3d7-659">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="ca3d7-659">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="ca3d7-660">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-660">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ca3d7-661">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-661">Address:</span></span> <br><span data-ttu-id="ca3d7-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="ca3d7-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ca3d7-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-666">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ca3d7-666">SQL Server</span></span></td>
      <td><span data-ttu-id="ca3d7-667">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="ca3d7-667">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="ca3d7-668">Función con valores de tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-668">Table-valued function</span></span></td>
      <td><span data-ttu-id="ca3d7-669">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="ca3d7-669">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="ca3d7-670">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-670">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ca3d7-671">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-671">Address:</span></span> <br><span data-ttu-id="ca3d7-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="ca3d7-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ca3d7-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-676">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ca3d7-676">SQL Server</span></span></td>
      <td><span data-ttu-id="ca3d7-677">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-677">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-678">Base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-678">Database</span></span></td>
      <td><span data-ttu-id="ca3d7-679">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="ca3d7-679">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="ca3d7-680">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-680">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ca3d7-681">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-681">Address:</span></span> <br><span data-ttu-id="ca3d7-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-684">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ca3d7-684">SQL Server</span></span></td>
      <td><span data-ttu-id="ca3d7-685">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-685">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-686">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="ca3d7-686">Table, view</span></span></td>
      <td><span data-ttu-id="ca3d7-687">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="ca3d7-687">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="ca3d7-688">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-688">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ca3d7-689">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-689">Address:</span></span> <br><span data-ttu-id="ca3d7-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="ca3d7-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ca3d7-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-694">SQL Server Analysis Services multidimensional</span><span class="sxs-lookup"><span data-stu-id="ca3d7-694">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="ca3d7-695">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-695">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-696">Modelo</span><span class="sxs-lookup"><span data-stu-id="ca3d7-696">Model</span></span></td>
      <td><span data-ttu-id="ca3d7-697">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-697">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="ca3d7-698">Autenticación: {windows, básica, anónima, no}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-698">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="ca3d7-699">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-699">Address:</span></span> <br><span data-ttu-id="ca3d7-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-703">SQL Server Analysis Services multidimensional</span><span class="sxs-lookup"><span data-stu-id="ca3d7-703">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="ca3d7-704">KPI</span><span class="sxs-lookup"><span data-stu-id="ca3d7-704">KPI</span></span></td>
      <td><span data-ttu-id="ca3d7-705">KPI</span><span class="sxs-lookup"><span data-stu-id="ca3d7-705">KPI</span></span></td>
      <td><span data-ttu-id="ca3d7-706">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-706">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="ca3d7-707">Autenticación: {windows, básica, anónima, no}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-707">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="ca3d7-708">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-708">Address:</span></span> <br><span data-ttu-id="ca3d7-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="ca3d7-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="ca3d7-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="ca3d7-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="ca3d7-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-714">SQL Server Analysis Services multidimensional</span><span class="sxs-lookup"><span data-stu-id="ca3d7-714">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="ca3d7-715">Measure</span><span class="sxs-lookup"><span data-stu-id="ca3d7-715">Measure</span></span></td>
      <td><span data-ttu-id="ca3d7-716">Measure</span><span class="sxs-lookup"><span data-stu-id="ca3d7-716">Measure</span></span></td>
      <td><span data-ttu-id="ca3d7-717">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-717">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="ca3d7-718">Autenticación: {windows, básica, anónima, no}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-718">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="ca3d7-719">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-719">Address:</span></span> <br><span data-ttu-id="ca3d7-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="ca3d7-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="ca3d7-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="ca3d7-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="ca3d7-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-725">SQL Server Analysis Services multidimensional</span><span class="sxs-lookup"><span data-stu-id="ca3d7-725">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="ca3d7-726">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-726">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-727">Dimension Data</span><span class="sxs-lookup"><span data-stu-id="ca3d7-727">Dimension</span></span></td>
      <td><span data-ttu-id="ca3d7-728">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-728">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="ca3d7-729">Autenticación: {windows, básica, anónima, no}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-729">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="ca3d7-730">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-730">Address:</span></span> <br><span data-ttu-id="ca3d7-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="ca3d7-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="ca3d7-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="ca3d7-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="ca3d7-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-736">Tabular de SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-736">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="ca3d7-737">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-737">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-738">Modelo</span><span class="sxs-lookup"><span data-stu-id="ca3d7-738">Model</span></span></td>
      <td><span data-ttu-id="ca3d7-739">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-739">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="ca3d7-740">Autenticación: {windows, básica, anónima, no}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-740">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="ca3d7-741">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-741">Address:</span></span> <br><span data-ttu-id="ca3d7-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-745">Tabular de SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-745">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="ca3d7-746">KPI</span><span class="sxs-lookup"><span data-stu-id="ca3d7-746">KPI</span></span></td>
      <td><span data-ttu-id="ca3d7-747">KPI</span><span class="sxs-lookup"><span data-stu-id="ca3d7-747">KPI</span></span></td>
      <td><span data-ttu-id="ca3d7-748">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-748">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="ca3d7-749">Autenticación: {windows, básica, anónima, no}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-749">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="ca3d7-750">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-750">Address:</span></span> <br><span data-ttu-id="ca3d7-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="ca3d7-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="ca3d7-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="ca3d7-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="ca3d7-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-756">Tabular de SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-756">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="ca3d7-757">Measure</span><span class="sxs-lookup"><span data-stu-id="ca3d7-757">Measure</span></span></td>
      <td><span data-ttu-id="ca3d7-758">Measure</span><span class="sxs-lookup"><span data-stu-id="ca3d7-758">Measure</span></span></td>
      <td><span data-ttu-id="ca3d7-759">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-759">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="ca3d7-760">Autenticación: {windows, básica, anónima, no}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-760">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="ca3d7-761">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-761">Address:</span></span> <br><span data-ttu-id="ca3d7-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="ca3d7-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="ca3d7-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="ca3d7-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="ca3d7-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-767">Tabular de SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-767">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="ca3d7-768">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-768">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-769">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-769">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-770">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-770">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="ca3d7-771">Autenticación: {windows, básica, anónima, no}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-771">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="ca3d7-772">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-772">Address:</span></span> <br><span data-ttu-id="ca3d7-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="ca3d7-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="ca3d7-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="ca3d7-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="ca3d7-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-778">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-778">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="ca3d7-779">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-779">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-780">Server</span><span class="sxs-lookup"><span data-stu-id="ca3d7-780">Server</span></span></td>
      <td><span data-ttu-id="ca3d7-781">
        <font size=2> Protocolo: reporting-services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-781">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="ca3d7-782">Autenticación: {windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-782">Authentication: {windows}</span></span> <br><span data-ttu-id="ca3d7-783">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-783">Address:</span></span> <br><span data-ttu-id="ca3d7-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-786">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-786">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="ca3d7-787">Informe</span><span class="sxs-lookup"><span data-stu-id="ca3d7-787">Report</span></span></td>
      <td><span data-ttu-id="ca3d7-788">Informe</span><span class="sxs-lookup"><span data-stu-id="ca3d7-788">Report</span></span></td>
      <td><span data-ttu-id="ca3d7-789">
        <font size=2> Protocolo: reporting-services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-789">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="ca3d7-790">Autenticación: {windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-790">Authentication: {windows}</span></span> <br><span data-ttu-id="ca3d7-791">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-791">Address:</span></span> <br><span data-ttu-id="ca3d7-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="ca3d7-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span></span> <br><span data-ttu-id="ca3d7-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-795">Teradata</span><span class="sxs-lookup"><span data-stu-id="ca3d7-795">Teradata</span></span></td>
      <td><span data-ttu-id="ca3d7-796">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-796">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-797">Base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-797">Database</span></span></td>
      <td><span data-ttu-id="ca3d7-798">
        <font size=2> Protocolo: teradata</span><span class="sxs-lookup"><span data-stu-id="ca3d7-798">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="ca3d7-799">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-799">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ca3d7-800">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-800">Address:</span></span> <br><span data-ttu-id="ca3d7-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-803">Teradata</span><span class="sxs-lookup"><span data-stu-id="ca3d7-803">Teradata</span></span></td>
      <td><span data-ttu-id="ca3d7-804">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-804">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-805">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="ca3d7-805">Table, view</span></span></td>
      <td><span data-ttu-id="ca3d7-806">
        <font size=2> Protocolo: teradata</span><span class="sxs-lookup"><span data-stu-id="ca3d7-806">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="ca3d7-807">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-807">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ca3d7-808">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-808">Address:</span></span> <br><span data-ttu-id="ca3d7-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-812">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-812">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="ca3d7-813">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-813">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-814">Modelo</span><span class="sxs-lookup"><span data-stu-id="ca3d7-814">Model</span></span></td>
      <td><span data-ttu-id="ca3d7-815">
        <font size="2"> Protocolo: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="ca3d7-815">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="ca3d7-816">Autenticación: {windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-816">Authentication: {windows}</span></span> <br><span data-ttu-id="ca3d7-817">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-817">Address:</span></span> <br><span data-ttu-id="ca3d7-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="ca3d7-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="ca3d7-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="ca3d7-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="ca3d7-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; versión </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-821">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="ca3d7-821">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="ca3d7-822">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-822">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-823">Entidad</span><span class="sxs-lookup"><span data-stu-id="ca3d7-823">Entity</span></span></td>
      <td><span data-ttu-id="ca3d7-824">
        <font size="2"> Protocolo: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="ca3d7-824">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="ca3d7-825">Autenticación: {windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-825">Authentication: {windows}</span></span> <br><span data-ttu-id="ca3d7-826">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-826">Address:</span></span> <br><span data-ttu-id="ca3d7-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="ca3d7-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="ca3d7-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="ca3d7-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="ca3d7-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; versión</span><span class="sxs-lookup"><span data-stu-id="ca3d7-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span></span> <br><span data-ttu-id="ca3d7-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entidad </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-831">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ca3d7-831">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="ca3d7-832">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-832">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-833">Base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-833">Database</span></span></td>
      <td><span data-ttu-id="ca3d7-834">
        <font size=2> Protocolo: document-db</span><span class="sxs-lookup"><span data-stu-id="ca3d7-834">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="ca3d7-835">Autenticación: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-835">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="ca3d7-836">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-836">Address:</span></span> <br><span data-ttu-id="ca3d7-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="ca3d7-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="ca3d7-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-839">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ca3d7-839">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="ca3d7-840">Colección</span><span class="sxs-lookup"><span data-stu-id="ca3d7-840">Collection</span></span></td>
      <td><span data-ttu-id="ca3d7-841">Colección</span><span class="sxs-lookup"><span data-stu-id="ca3d7-841">Collection</span></span></td>
      <td><span data-ttu-id="ca3d7-842">
        <font size=2> Protocolo: document-db</span><span class="sxs-lookup"><span data-stu-id="ca3d7-842">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="ca3d7-843">Autenticación: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-843">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="ca3d7-844">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-844">Address:</span></span> <br><span data-ttu-id="ca3d7-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="ca3d7-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="ca3d7-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; colección </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-848">ODBC genérico</span><span class="sxs-lookup"><span data-stu-id="ca3d7-848">Generic ODBC</span></span></td>
      <td><span data-ttu-id="ca3d7-849">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-849">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-850">Base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-850">Database</span></span></td>
      <td><span data-ttu-id="ca3d7-851">
        <font size=2> Protocolo: odbc</span><span class="sxs-lookup"><span data-stu-id="ca3d7-851">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="ca3d7-852">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-852">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ca3d7-853">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-853">Address:</span></span> <br><span data-ttu-id="ca3d7-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; opciones</span><span class="sxs-lookup"><span data-stu-id="ca3d7-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="ca3d7-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-856">ODBC genérico</span><span class="sxs-lookup"><span data-stu-id="ca3d7-856">Generic ODBC</span></span></td>
      <td><span data-ttu-id="ca3d7-857">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-857">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-858">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="ca3d7-858">Table, View</span></span></td>
      <td><span data-ttu-id="ca3d7-859">
        <font size=2> Protocolo: odbc</span><span class="sxs-lookup"><span data-stu-id="ca3d7-859">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="ca3d7-860">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-860">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ca3d7-861">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-861">Address:</span></span> <br><span data-ttu-id="ca3d7-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; opciones</span><span class="sxs-lookup"><span data-stu-id="ca3d7-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="ca3d7-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="ca3d7-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="ca3d7-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-866">Sybase</span><span class="sxs-lookup"><span data-stu-id="ca3d7-866">Sybase</span></span></td>
      <td><span data-ttu-id="ca3d7-867">Contenedor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-867">Container</span></span></td>
      <td><span data-ttu-id="ca3d7-868">Base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-868">Database</span></span></td>
      <td><span data-ttu-id="ca3d7-869">
        <font size=2> protocolo: sybase</span><span class="sxs-lookup"><span data-stu-id="ca3d7-869">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="ca3d7-870">autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-870">authentication: {basic, windows}</span></span> <br><span data-ttu-id="ca3d7-871">dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-871">address:</span></span> <br><span data-ttu-id="ca3d7-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-874">Sybase</span><span class="sxs-lookup"><span data-stu-id="ca3d7-874">Sybase</span></span></td>
      <td><span data-ttu-id="ca3d7-875">Tabla</span><span class="sxs-lookup"><span data-stu-id="ca3d7-875">Table</span></span></td>
      <td><span data-ttu-id="ca3d7-876">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="ca3d7-876">Table, View</span></span></td>
      <td><span data-ttu-id="ca3d7-877">
        <font size=2> protocolo: sybase</span><span class="sxs-lookup"><span data-stu-id="ca3d7-877">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="ca3d7-878">autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="ca3d7-878">authentication: {basic, windows}</span></span> <br><span data-ttu-id="ca3d7-879">dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-879">address:</span></span> <br><span data-ttu-id="ca3d7-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="ca3d7-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ca3d7-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="ca3d7-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ca3d7-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="ca3d7-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ca3d7-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ca3d7-884">Sí (ninguno de hello anterior)</span><span class="sxs-lookup"><span data-stu-id="ca3d7-884">Other (none of hello above)</span></span></td>
      <td>\*</td>
      <td>\*</td>
      <td><span data-ttu-id="ca3d7-885">
        <font size=2> Protocolo: generic-asset</span><span class="sxs-lookup"><span data-stu-id="ca3d7-885">
        <font size=2> Protocol: generic-asset</span></span> <br><span data-ttu-id="ca3d7-886">Dirección:</span><span class="sxs-lookup"><span data-stu-id="ca3d7-886">Address:</span></span> <br><span data-ttu-id="ca3d7-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span><span class="sxs-lookup"><span data-stu-id="ca3d7-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span></span></td>
    </tr>
</table>
