---
title: "Orígenes de datos compatibles en Azure Data Catalog | Microsoft Docs"
description: "En este artículo se enumeran las especificaciones de los orígenes de datos compatibles actualmente."
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
ms.openlocfilehash: d6867c73bc6ea3c238cceef8a68466d451f3365c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="supported-data-sources-in-azure-data-catalog"></a><span data-ttu-id="cb719-103">Orígenes de datos compatibles en Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="cb719-103">Supported data sources in Azure Data Catalog</span></span>

<span data-ttu-id="cb719-104">Pueden publicarse metadatos mediante una API pública o una herramienta de registro con un solo clic, o mediante la especificación manual de información directamente en el portal web de Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="cb719-104">You can publish metadata by using a public API or a click-once registration tool, or by manually entering information directly to the Azure Data Catalog web portal.</span></span> <span data-ttu-id="cb719-105">En la siguiente tabla se resumen todos los orígenes que admite el catálogo actualmente y las funcionalidades de publicación de cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="cb719-105">The following table summarizes all data sources that are supported by the catalog today, and the publishing capabilities for each.</span></span> <span data-ttu-id="cb719-106">También se enumeran las herramientas de datos externas que cada origen puede iniciar desde nuestra experiencia "abierta" del portal.</span><span class="sxs-lookup"><span data-stu-id="cb719-106">Also listed are the external data tools that each data source can launch from our portal "open-in" experience.</span></span> <span data-ttu-id="cb719-107">La segunda tabla contiene una especificación más técnica de las propiedades de conexión de cada propiedad de la conexión del origen de datos.</span><span class="sxs-lookup"><span data-stu-id="cb719-107">The second table contains a more technical specification of each data-source connection property.</span></span>


## <a name="list-of-supported-data-sources"></a><span data-ttu-id="cb719-108">Lista de orígenes de datos que se admiten</span><span class="sxs-lookup"><span data-stu-id="cb719-108">List of supported data sources</span></span>

<table>
    <tr>
       <td><span data-ttu-id="cb719-109"><b>Objeto de origen de datos</b></span><span class="sxs-lookup"><span data-stu-id="cb719-109"><b>Data source object</b></span></span></td>
       <td><span data-ttu-id="cb719-110"><b>API</b></span><span class="sxs-lookup"><span data-stu-id="cb719-110"><b>API</b></span></span></td>
       <td><span data-ttu-id="cb719-111"><b>Entrada manual</b></span><span class="sxs-lookup"><span data-stu-id="cb719-111"><b>Manual entry</b></span></span></td>
       <td><span data-ttu-id="cb719-112"><b>Herramienta de registro</b></span><span class="sxs-lookup"><span data-stu-id="cb719-112"><b>Registration tool</b></span></span></td>
       <td><span data-ttu-id="cb719-113"><b>Herramientas abiertas</b></span><span class="sxs-lookup"><span data-stu-id="cb719-113"><b>Open-in tools</b></span></span></td>
       <td><span data-ttu-id="cb719-114"><b>Notas</b></span><span class="sxs-lookup"><span data-stu-id="cb719-114"><b>Notes</b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-115">Directorio de Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="cb719-115">Azure Data Lake Store directory</span></span></td>
      <td><span data-ttu-id="cb719-116">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-116">✓</span></span></td>
      <td><span data-ttu-id="cb719-117">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-117">✓</span></span></td>
      <td><span data-ttu-id="cb719-118">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-118">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-119">Archivo de Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="cb719-119">Azure Data Lake Store file</span></span></td>
      <td><span data-ttu-id="cb719-120">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-120">✓</span></span></td>
      <td><span data-ttu-id="cb719-121">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-121">✓</span></span></td>
      <td><span data-ttu-id="cb719-122">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-122">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-123">Almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="cb719-123">Azure Blob storage</span></span></td>
      <td><span data-ttu-id="cb719-124">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-124">✓</span></span></td>
      <td><span data-ttu-id="cb719-125">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-125">✓</span></span></td>
      <td><span data-ttu-id="cb719-126">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-126">✓</span></span></td>
      <td><span data-ttu-id="cb719-127"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="cb719-127"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-128">Directorio de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="cb719-128">Azure Storage directory</span></span></td>
      <td><span data-ttu-id="cb719-129">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-129">✓</span></span></td>
      <td><span data-ttu-id="cb719-130">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-130">✓</span></span></td>
      <td><span data-ttu-id="cb719-131">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-131">✓</span></span></td>
      <td><span data-ttu-id="cb719-132"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="cb719-132"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-133">Tabla de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="cb719-133">Azure Storage table</span></span></td>
      <td><span data-ttu-id="cb719-134">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-134">✓</span></span></td>
      <td><span data-ttu-id="cb719-135">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-135">✓</span></span></td>
      <td><span data-ttu-id="cb719-136">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-136">✓</span></span></td>
      <td>
        <font size="2"></font>
      </td>
      <td>
        <font size="2"></font>
      </td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-137">Directorio de HDFS</span><span class="sxs-lookup"><span data-stu-id="cb719-137">HDFS directory</span></span></td>
      <td><span data-ttu-id="cb719-138">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-138">✓</span></span></td>
      <td><span data-ttu-id="cb719-139">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-139">✓</span></span></td>
      <td><span data-ttu-id="cb719-140">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-140">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-141">Archivo de HDFS</span><span class="sxs-lookup"><span data-stu-id="cb719-141">HDFS file</span></span></td>
      <td><span data-ttu-id="cb719-142">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-142">✓</span></span></td>
      <td><span data-ttu-id="cb719-143">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-143">✓</span></span></td>
      <td><span data-ttu-id="cb719-144">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-144">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-145">Tabla de Hive</span><span class="sxs-lookup"><span data-stu-id="cb719-145">Hive table</span></span></td>
      <td><span data-ttu-id="cb719-146">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-146">✓</span></span></td>
      <td><span data-ttu-id="cb719-147">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-147">✓</span></span></td>
      <td><span data-ttu-id="cb719-148">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-148">✓</span></span></td>
      <td><span data-ttu-id="cb719-149"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="cb719-149"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-150">Vista de Hive</span><span class="sxs-lookup"><span data-stu-id="cb719-150">Hive view</span></span></td>
      <td><span data-ttu-id="cb719-151">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-151">✓</span></span></td>
      <td><span data-ttu-id="cb719-152">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-152">✓</span></span></td>
      <td><span data-ttu-id="cb719-153">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-153">✓</span></span></td>
      <td><span data-ttu-id="cb719-154"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="cb719-154"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-155">Tabla de MySQL</span><span class="sxs-lookup"><span data-stu-id="cb719-155">MySQL table</span></span></td>
      <td><span data-ttu-id="cb719-156">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-156">✓</span></span></td>
      <td><span data-ttu-id="cb719-157">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-157">✓</span></span></td>
      <td><span data-ttu-id="cb719-158">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-158">✓</span></span></td>
      <td><span data-ttu-id="cb719-159"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="cb719-159"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-160">Vista de MySQL</span><span class="sxs-lookup"><span data-stu-id="cb719-160">MySQL view</span></span></td>
      <td><span data-ttu-id="cb719-161">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-161">✓</span></span></td>
      <td><span data-ttu-id="cb719-162">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-162">✓</span></span></td>
      <td><span data-ttu-id="cb719-163">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-163">✓</span></span></td>
      <td><span data-ttu-id="cb719-164"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="cb719-164"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-165">Tabla de Oracle Database</span><span class="sxs-lookup"><span data-stu-id="cb719-165">Oracle Database table</span></span></td>
      <td><span data-ttu-id="cb719-166">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-166">✓</span></span></td>
      <td><span data-ttu-id="cb719-167">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-167">✓</span></span></td>
      <td><span data-ttu-id="cb719-168">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-168">✓</span></span></td>
      <td><span data-ttu-id="cb719-169"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="cb719-169"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-170">Vista de Oracle Database</span><span class="sxs-lookup"><span data-stu-id="cb719-170">Oracle Database view</span></span></td>
      <td><span data-ttu-id="cb719-171">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-171">✓</span></span></td>
      <td><span data-ttu-id="cb719-172">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-172">✓</span></span></td>
      <td><span data-ttu-id="cb719-173">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-173">✓</span></span></td>
      <td><span data-ttu-id="cb719-174"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="cb719-174"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-175">Otro (recurso genérico)</span><span class="sxs-lookup"><span data-stu-id="cb719-175">Other (generic asset)</span></span></td>
      <td><span data-ttu-id="cb719-176">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-176">✓</span></span></td>
      <td><span data-ttu-id="cb719-177">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-177">✓</span></span></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-178">Tabla de Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="cb719-178">Azure SQL Data Warehouse table</span></span></td>
      <td><span data-ttu-id="cb719-179">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-179">✓</span></span></td>
      <td><span data-ttu-id="cb719-180">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-180">✓</span></span></td>
      <td><span data-ttu-id="cb719-181">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-181">✓</span></span></td>
      <td><span data-ttu-id="cb719-182"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="cb719-182"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-183">Vista de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="cb719-183">SQL Data Warehouse view</span></span></td>
      <td><span data-ttu-id="cb719-184">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-184">✓</span></span></td>
      <td><span data-ttu-id="cb719-185">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-185">✓</span></span></td>
      <td><span data-ttu-id="cb719-186">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-186">✓</span></span></td>
      <td><span data-ttu-id="cb719-187"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="cb719-187"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-188">Dimensión de SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="cb719-188">SQL Server Analysis Services dimension</span></span></td>
      <td><span data-ttu-id="cb719-189">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-189">✓</span></span></td>
      <td><span data-ttu-id="cb719-190">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-190">✓</span></span></td>
      <td><span data-ttu-id="cb719-191">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-191">✓</span></span></td>
      <td><span data-ttu-id="cb719-192"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="cb719-192"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-193">KPI de SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="cb719-193">SQL Server Analysis Services KPI</span></span></td>
      <td><span data-ttu-id="cb719-194">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-194">✓</span></span></td>
      <td><span data-ttu-id="cb719-195">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-195">✓</span></span></td>
      <td><span data-ttu-id="cb719-196">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-196">✓</span></span></td>
      <td><span data-ttu-id="cb719-197"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="cb719-197"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-198">Medida de SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="cb719-198">SQL Server Analysis Services measure</span></span></td>
      <td><span data-ttu-id="cb719-199">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-199">✓</span></span></td>
      <td><span data-ttu-id="cb719-200">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-200">✓</span></span></td>
      <td><span data-ttu-id="cb719-201">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-201">✓</span></span></td>
      <td><span data-ttu-id="cb719-202"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="cb719-202"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-203">Tabla de SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="cb719-203">SQL Server Analysis Services table</span></span></td>
      <td><span data-ttu-id="cb719-204">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-204">✓</span></span></td>
      <td><span data-ttu-id="cb719-205">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-205">✓</span></span></td>
      <td><span data-ttu-id="cb719-206">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-206">✓</span></span></td>
      <td><span data-ttu-id="cb719-207"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="cb719-207"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-208">Informe de SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="cb719-208">SQL Server Reporting Services report</span></span></td>
      <td><span data-ttu-id="cb719-209">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-209">✓</span></span></td>
      <td><span data-ttu-id="cb719-210">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-210">✓</span></span></td>
      <td><span data-ttu-id="cb719-211">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-211">✓</span></span></td>
      <td><span data-ttu-id="cb719-212"><font size=2>Browser</font></span><span class="sxs-lookup"><span data-stu-id="cb719-212"><font size=2>Browser</font></span></span></td>
      <td><span data-ttu-id="cb719-213"><font size=2>Solo servidores de modo nativo. No se admite el modo de SharePoint.</font></span><span class="sxs-lookup"><span data-stu-id="cb719-213"><font size=2>Native mode servers only. SharePoint mode is not supported.</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-214">Tabla de SQL Server</span><span class="sxs-lookup"><span data-stu-id="cb719-214">SQL Server table</span></span></td>
      <td><span data-ttu-id="cb719-215">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-215">✓</span></span></td>
      <td><span data-ttu-id="cb719-216">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-216">✓</span></span></td>
      <td><span data-ttu-id="cb719-217">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-217">✓</span></span></td>
      <td><span data-ttu-id="cb719-218"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="cb719-218"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-219">Vista de SQL Server</span><span class="sxs-lookup"><span data-stu-id="cb719-219">SQL Server view</span></span></td>
      <td><span data-ttu-id="cb719-220">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-220">✓</span></span></td>
      <td><span data-ttu-id="cb719-221">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-221">✓</span></span></td>
      <td><span data-ttu-id="cb719-222">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-222">✓</span></span></td>
      <td><span data-ttu-id="cb719-223"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="cb719-223"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-224">Tabla de Teradata</span><span class="sxs-lookup"><span data-stu-id="cb719-224">Teradata table</span></span></td>
      <td><span data-ttu-id="cb719-225">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-225">✓</span></span></td>
      <td><span data-ttu-id="cb719-226">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-226">✓</span></span></td>
      <td><span data-ttu-id="cb719-227">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-227">✓</span></span></td>
      <td><span data-ttu-id="cb719-228"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="cb719-228"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-229">Vista de Teradata</span><span class="sxs-lookup"><span data-stu-id="cb719-229">Teradata view</span></span></td>
      <td><span data-ttu-id="cb719-230">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-230">✓</span></span></td>
      <td><span data-ttu-id="cb719-231">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-231">✓</span></span></td>
      <td><span data-ttu-id="cb719-232">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-232">✓</span></span></td>
      <td><span data-ttu-id="cb719-233"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="cb719-233"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-234">Vista de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cb719-234">SAP HANA view</span></span></td>
      <td><span data-ttu-id="cb719-235">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-235">✓</span></span></td>
      <td><span data-ttu-id="cb719-236">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-236">✓</span></span></td>
      <td><span data-ttu-id="cb719-237">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-237">✓</span></span></td>
      <td><span data-ttu-id="cb719-238"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="cb719-238"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-239">Tabla de DB2</span><span class="sxs-lookup"><span data-stu-id="cb719-239">DB2 table</span></span></td>
      <td><span data-ttu-id="cb719-240">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-240">✓</span></span></td>
      <td><span data-ttu-id="cb719-241">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-241">✓</span></span></td>
      <td><span data-ttu-id="cb719-242">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-242">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-243">Vista de DB2</span><span class="sxs-lookup"><span data-stu-id="cb719-243">DB2 view</span></span></td>
      <td><span data-ttu-id="cb719-244">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-244">✓</span></span></td>
      <td><span data-ttu-id="cb719-245">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-245">✓</span></span></td>
      <td><span data-ttu-id="cb719-246">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-246">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-247">Archivo de sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="cb719-247">File system file</span></span></td>
      <td><span data-ttu-id="cb719-248">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-248">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-249">Directorio FTP</span><span class="sxs-lookup"><span data-stu-id="cb719-249">FTP directory</span></span></td>
      <td><span data-ttu-id="cb719-250">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-250">✓</span></span></td>
      <td><span data-ttu-id="cb719-251">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-251">✓</span></span></td>
      <td><span data-ttu-id="cb719-252">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-252">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-253">Archivo FTP</span><span class="sxs-lookup"><span data-stu-id="cb719-253">FTP file</span></span></td>
      <td><span data-ttu-id="cb719-254">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-254">✓</span></span></td>
      <td><span data-ttu-id="cb719-255">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-255">✓</span></span></td>
      <td><span data-ttu-id="cb719-256">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-256">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-257">Informe HTTP</span><span class="sxs-lookup"><span data-stu-id="cb719-257">HTTP report</span></span></td>
      <td><span data-ttu-id="cb719-258">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-258">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-259">Punto de conexión HTTP</span><span class="sxs-lookup"><span data-stu-id="cb719-259">HTTP endpoint</span></span></td>
      <td><span data-ttu-id="cb719-260">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-260">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-261">Archivo HTTP</span><span class="sxs-lookup"><span data-stu-id="cb719-261">HTTP file</span></span></td>
      <td><span data-ttu-id="cb719-262">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-262">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-263">Conjunto de entidades de OData</span><span class="sxs-lookup"><span data-stu-id="cb719-263">OData entity set</span></span></td>
      <td><span data-ttu-id="cb719-264">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-264">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-265">Función de OData</span><span class="sxs-lookup"><span data-stu-id="cb719-265">OData function</span></span></td>
      <td><span data-ttu-id="cb719-266">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-266">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-267">Tabla de PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="cb719-267">PostgreSQL table</span></span></td>
      <td><span data-ttu-id="cb719-268">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-268">✓</span></span></td>
      <td><span data-ttu-id="cb719-269">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-269">✓</span></span></td>
      <td><span data-ttu-id="cb719-270">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-270">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-271">Vista de PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="cb719-271">PostgreSQL view</span></span></td>
      <td><span data-ttu-id="cb719-272">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-272">✓</span></span></td>
      <td><span data-ttu-id="cb719-273">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-273">✓</span></span></td>
      <td><span data-ttu-id="cb719-274">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-274">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-275">Vista de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cb719-275">SAP HANA view</span></span></td>
      <td><span data-ttu-id="cb719-276">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-276">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td> <span data-ttu-id="cb719-277">Objeto de Salesforce</span><span class="sxs-lookup"><span data-stu-id="cb719-277">Salesforce object</span></span></td>
      <td><span data-ttu-id="cb719-278">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-278">✓</span></span></td>
      <td><span data-ttu-id="cb719-279">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-279">✓</span></span></td>
      <td><span data-ttu-id="cb719-280">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-280">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-281">Lista de SharePoint</span><span class="sxs-lookup"><span data-stu-id="cb719-281">SharePoint list</span></span> </td>
      <td><span data-ttu-id="cb719-282">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-282">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-283">Colección de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cb719-283">Azure Cosmos DB collection</span></span></td>
      <td><span data-ttu-id="cb719-284">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-284">✓</span></span></td>
      <td><span data-ttu-id="cb719-285">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-285">✓</span></span></td>
      <td><span data-ttu-id="cb719-286">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-286">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-287">Tabla ODBC genérica</span><span class="sxs-lookup"><span data-stu-id="cb719-287">Generic ODBC table</span></span></td>
      <td><span data-ttu-id="cb719-288">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-288">✓</span></span></td>
      <td><span data-ttu-id="cb719-289">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-289">✓</span></span></td>
      <td><span data-ttu-id="cb719-290">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-290">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-291">Vista de ODBC genérica</span><span class="sxs-lookup"><span data-stu-id="cb719-291">Generic ODBC view</span></span></td>
      <td><span data-ttu-id="cb719-292">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-292">✓</span></span></td>
      <td><span data-ttu-id="cb719-293">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-293">✓</span></span></td>
      <td><span data-ttu-id="cb719-294">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-294">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-295">Tabla de Cassandra</span><span class="sxs-lookup"><span data-stu-id="cb719-295">Cassandra table</span></span></td>
      <td><span data-ttu-id="cb719-296">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-296">✓</span></span></td>
      <td><span data-ttu-id="cb719-297">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-297">✓</span></span></td>
      <td><span data-ttu-id="cb719-298">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-298">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="cb719-299"><font size=2>Publicar como un recurso ODBC genérico</font></span><span class="sxs-lookup"><span data-stu-id="cb719-299"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-300">Vista de Cassandra</span><span class="sxs-lookup"><span data-stu-id="cb719-300">Cassandra view</span></span></td>
      <td><span data-ttu-id="cb719-301">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-301">✓</span></span></td>
      <td><span data-ttu-id="cb719-302">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-302">✓</span></span></td>
      <td><span data-ttu-id="cb719-303">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-303">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="cb719-304"><font size=2>Publicar como un recurso ODBC genérico</font></span><span class="sxs-lookup"><span data-stu-id="cb719-304"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-305">Tabla de Sybase</span><span class="sxs-lookup"><span data-stu-id="cb719-305">Sybase table</span></span></td>
      <td><span data-ttu-id="cb719-306">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-306">✓</span></span></td>
      <td><span data-ttu-id="cb719-307">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-307">✓</span></span></td>
      <td><span data-ttu-id="cb719-308">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-308">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-309">Vista de Sybase</span><span class="sxs-lookup"><span data-stu-id="cb719-309">Sybase view</span></span></td>
      <td><span data-ttu-id="cb719-310">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-310">✓</span></span></td>
      <td><span data-ttu-id="cb719-311">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-311">✓</span></span></td>
      <td><span data-ttu-id="cb719-312">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-312">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-313">Tabla de MongoDB</span><span class="sxs-lookup"><span data-stu-id="cb719-313">MongoDB table</span></span></td>
      <td><span data-ttu-id="cb719-314">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-314">✓</span></span></td>
      <td><span data-ttu-id="cb719-315">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-315">✓</span></span></td>
      <td><span data-ttu-id="cb719-316">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-316">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="cb719-317"><font size=2>Publicar como un recurso ODBC genérico</font></span><span class="sxs-lookup"><span data-stu-id="cb719-317"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-318">Vista de MongoDB</span><span class="sxs-lookup"><span data-stu-id="cb719-318">MongoDB view</span></span></td>
      <td><span data-ttu-id="cb719-319">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-319">✓</span></span></td>
      <td><span data-ttu-id="cb719-320">✓ </span><span class="sxs-lookup"><span data-stu-id="cb719-320">✓</span></span></td>
      <td><span data-ttu-id="cb719-321">✓</span><span class="sxs-lookup"><span data-stu-id="cb719-321">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="cb719-322"><font size=2>Publicar como un recurso ODBC genérico</font></span><span class="sxs-lookup"><span data-stu-id="cb719-322"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
</table>

<span data-ttu-id="cb719-323">Si necesita compatibilidad con más fuentes, envíe una solicitud de característica al [foro de Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="cb719-323">If you need support for additional sources, submit a feature request to the [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span></span>


## <a name="data-source-reference-specification"></a><span data-ttu-id="cb719-324">Especificación de referencia de origen de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-324">Data-source reference specification</span></span>
> [!NOTE]
> <span data-ttu-id="cb719-325">La columna **Estructura de DSL** de la tabla siguiente solo enumera las propiedades de conexión del contenedor de propiedades "dirección" que usa Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="cb719-325">The **DSL structure** column in the following table lists only the connection properties for "address" property bag that are used by Azure Data Catalog.</span></span> <span data-ttu-id="cb719-326">Es decir, el contenedor de propiedades "dirección" puede contener otras propiedades de conexión del origen de datos que Azure Data Catalog conserva, pero no utiliza.</span><span class="sxs-lookup"><span data-stu-id="cb719-326">That is, "address" property bag can contain other connection properties of the data source which Azure Data Catalog persists, but does not use.</span></span>

<table>
    <tr>
       <td><span data-ttu-id="cb719-327"><b>Tipo de origen</b></span><span class="sxs-lookup"><span data-stu-id="cb719-327"><b>Source type</b></span></span></td>
       <td><span data-ttu-id="cb719-328"><b>Tipo de recurso</b></span><span class="sxs-lookup"><span data-stu-id="cb719-328"><b>Asset type</b></span></span></td>
       <td><span data-ttu-id="cb719-329"><b>Tipos de objeto</b></span><span class="sxs-lookup"><span data-stu-id="cb719-329"><b>Object types</b></span></span></td>
       <td><span data-ttu-id="cb719-330"><b>Estructura de DSL<b></span><span class="sxs-lookup"><span data-stu-id="cb719-330"><b>DSL structure<b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-331">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="cb719-331">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="cb719-332">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-332">Container</span></span></td>
      <td><span data-ttu-id="cb719-333">Data Lake</span><span class="sxs-lookup"><span data-stu-id="cb719-333">Data Lake</span></span></td>
      <td><span data-ttu-id="cb719-334">
        <font size=2> Protocolo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="cb719-334">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="cb719-335">Autenticación: {básica, oauth}</span><span class="sxs-lookup"><span data-stu-id="cb719-335">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="cb719-336">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-336">Address:</span></span> <br><span data-ttu-id="cb719-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-338">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="cb719-338">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="cb719-339">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-339">Table</span></span></td>
      <td><span data-ttu-id="cb719-340">Directorio, archivo</span><span class="sxs-lookup"><span data-stu-id="cb719-340">Directory, file</span></span></td>
      <td><span data-ttu-id="cb719-341">
        <font size=2> Protocolo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="cb719-341">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="cb719-342">Autenticación: {básica, oauth}</span><span class="sxs-lookup"><span data-stu-id="cb719-342">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="cb719-343">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-343">Address:</span></span> <br><span data-ttu-id="cb719-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-345">Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="cb719-345">Azure Storage</span></span></td>
      <td><span data-ttu-id="cb719-346">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-346">Container</span></span></td>
      <td><span data-ttu-id="cb719-347">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-347">Container</span></span></td>
      <td><span data-ttu-id="cb719-348">
        <font size=2> Protocolo: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="cb719-348">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="cb719-349">Autenticación: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="cb719-349">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="cb719-350">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-350">Address:</span></span> <br><span data-ttu-id="cb719-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; dominio</span><span class="sxs-lookup"><span data-stu-id="cb719-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="cb719-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cuenta</span><span class="sxs-lookup"><span data-stu-id="cb719-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="cb719-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; contenedor</font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-354">Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="cb719-354">Azure Storage</span></span></td>
      <td><span data-ttu-id="cb719-355">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-355">Table</span></span></td>
      <td><span data-ttu-id="cb719-356">Blob, directorio</span><span class="sxs-lookup"><span data-stu-id="cb719-356">Blob, directory</span></span></td>
      <td><span data-ttu-id="cb719-357">
        <font size=2> Protocolo: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="cb719-357">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="cb719-358">Autenticación: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="cb719-358">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="cb719-359">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-359">Address:</span></span> <br><span data-ttu-id="cb719-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; dominio</span><span class="sxs-lookup"><span data-stu-id="cb719-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="cb719-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cuenta</span><span class="sxs-lookup"><span data-stu-id="cb719-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="cb719-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container</span></span> <br><span data-ttu-id="cb719-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; nombre </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-364">Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="cb719-364">Azure Storage</span></span></td>
      <td><span data-ttu-id="cb719-365">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-365">Container</span></span></td>
      <td><span data-ttu-id="cb719-366">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-366">Container</span></span></td>
      <td><span data-ttu-id="cb719-367">
        <font size=2> Protocolo: azure-tables</span><span class="sxs-lookup"><span data-stu-id="cb719-367">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="cb719-368">Autenticación: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="cb719-368">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="cb719-369">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-369">Address:</span></span> <br><span data-ttu-id="cb719-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; dominio</span><span class="sxs-lookup"><span data-stu-id="cb719-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="cb719-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cuenta</font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-372">Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="cb719-372">Azure Storage</span></span></td>
      <td><span data-ttu-id="cb719-373">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-373">Table</span></span></td>
      <td><span data-ttu-id="cb719-374">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-374">Table</span></span></td>
      <td><span data-ttu-id="cb719-375">
        <font size=2> Protocolo: azure-tables</span><span class="sxs-lookup"><span data-stu-id="cb719-375">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="cb719-376">Autenticación: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="cb719-376">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="cb719-377">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-377">Address:</span></span> <br><span data-ttu-id="cb719-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; dominio</span><span class="sxs-lookup"><span data-stu-id="cb719-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="cb719-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cuenta</span><span class="sxs-lookup"><span data-stu-id="cb719-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="cb719-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; nombre </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-381">Cosmos</span><span class="sxs-lookup"><span data-stu-id="cb719-381">Cosmos</span></span></td>
      <td><span data-ttu-id="cb719-382">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-382">Container</span></span></td>
      <td><span data-ttu-id="cb719-383">Clúster virtual</span><span class="sxs-lookup"><span data-stu-id="cb719-383">Virtual cluster</span></span></td>
      <td><span data-ttu-id="cb719-384">
        <font size=2> Protocolo: cosmos</span><span class="sxs-lookup"><span data-stu-id="cb719-384">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="cb719-385">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-385">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="cb719-386">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-386">Address:</span></span> <br><span data-ttu-id="cb719-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-388">Cosmos</span><span class="sxs-lookup"><span data-stu-id="cb719-388">Cosmos</span></span></td>
      <td><span data-ttu-id="cb719-389">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-389">Table</span></span></td>
      <td><span data-ttu-id="cb719-390">Transmisión, conjunto de transmisiones, vista</span><span class="sxs-lookup"><span data-stu-id="cb719-390">Stream, stream set, view</span></span></td>
      <td><span data-ttu-id="cb719-391">
        <font size=2> Protocolo: cosmos</span><span class="sxs-lookup"><span data-stu-id="cb719-391">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="cb719-392">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-392">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="cb719-393">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-393">Address:</span></span> <br><span data-ttu-id="cb719-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-395">Datazen</span><span class="sxs-lookup"><span data-stu-id="cb719-395">Datazen</span></span></td>
      <td><span data-ttu-id="cb719-396">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-396">Container</span></span></td>
      <td><span data-ttu-id="cb719-397">Sitio</span><span class="sxs-lookup"><span data-stu-id="cb719-397">Site</span></span></td>
      <td><span data-ttu-id="cb719-398">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="cb719-398">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="cb719-399">Autenticación: {no, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="cb719-399">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="cb719-400">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-400">Address:</span></span> <br><span data-ttu-id="cb719-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-402">Datazen</span><span class="sxs-lookup"><span data-stu-id="cb719-402">Datazen</span></span></td>
      <td><span data-ttu-id="cb719-403">Informe</span><span class="sxs-lookup"><span data-stu-id="cb719-403">Report</span></span></td>
      <td><span data-ttu-id="cb719-404">Informe, panel</span><span class="sxs-lookup"><span data-stu-id="cb719-404">Report, dashboard</span></span></td>
      <td><span data-ttu-id="cb719-405">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="cb719-405">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="cb719-406">Autenticación: {no, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="cb719-406">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="cb719-407">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-407">Address:</span></span> <br><span data-ttu-id="cb719-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-409">DB2</span><span class="sxs-lookup"><span data-stu-id="cb719-409">DB2</span></span></td>
      <td><span data-ttu-id="cb719-410">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-410">Container</span></span></td>
      <td><span data-ttu-id="cb719-411">Base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-411">Database</span></span></td>
      <td><span data-ttu-id="cb719-412">
        <font size=2> Protocolo: db2</span><span class="sxs-lookup"><span data-stu-id="cb719-412">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="cb719-413">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-413">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="cb719-414">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-414">Address:</span></span> <br><span data-ttu-id="cb719-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-417">DB2</span><span class="sxs-lookup"><span data-stu-id="cb719-417">DB2</span></span></td>
      <td><span data-ttu-id="cb719-418">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-418">Table</span></span></td>
      <td><span data-ttu-id="cb719-419">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="cb719-419">Table, view</span></span></td>
      <td><span data-ttu-id="cb719-420">
        <font size=2> Protocolo: db2</span><span class="sxs-lookup"><span data-stu-id="cb719-420">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="cb719-421">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-421">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="cb719-422">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-422">Address:</span></span> <br><span data-ttu-id="cb719-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="cb719-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="cb719-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-427">Sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="cb719-427">File system</span></span></td>
      <td><span data-ttu-id="cb719-428">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-428">Table</span></span></td>
      <td><span data-ttu-id="cb719-429">Archivo</span><span class="sxs-lookup"><span data-stu-id="cb719-429">File</span></span></td>
      <td><span data-ttu-id="cb719-430">
        <font size=2> Protocolo: archivo</span><span class="sxs-lookup"><span data-stu-id="cb719-430">
        <font size=2> Protocol: file</span></span> <br><span data-ttu-id="cb719-431">Autenticación: {no, básica, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-431">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="cb719-432">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-432">Address:</span></span> <br><span data-ttu-id="cb719-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ruta de acceso </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-434">FTP</span><span class="sxs-lookup"><span data-stu-id="cb719-434">FTP</span></span></td>
      <td><span data-ttu-id="cb719-435">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-435">Table</span></span></td>
      <td><span data-ttu-id="cb719-436">Directorio, archivo</span><span class="sxs-lookup"><span data-stu-id="cb719-436">Directory, file</span></span></td>
      <td><span data-ttu-id="cb719-437">
        <font size=2> Protocolo: ftp</span><span class="sxs-lookup"><span data-stu-id="cb719-437">
        <font size=2> Protocol: ftp</span></span> <br><span data-ttu-id="cb719-438">Autenticación: {no, básica, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-438">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="cb719-439">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-439">Address:</span></span> <br><span data-ttu-id="cb719-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-441">sistema de archivos distribuido de Hadoop</span><span class="sxs-lookup"><span data-stu-id="cb719-441">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="cb719-442">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-442">Container</span></span></td>
      <td><span data-ttu-id="cb719-443">Clúster</span><span class="sxs-lookup"><span data-stu-id="cb719-443">Cluster</span></span></td>
      <td><span data-ttu-id="cb719-444">
        <font size=2> Protocolo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="cb719-444">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="cb719-445">Autenticación: {básica, oauth}</span><span class="sxs-lookup"><span data-stu-id="cb719-445">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="cb719-446">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-446">Address:</span></span> <br><span data-ttu-id="cb719-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-448">sistema de archivos distribuido de Hadoop</span><span class="sxs-lookup"><span data-stu-id="cb719-448">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="cb719-449">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-449">Table</span></span></td>
      <td><span data-ttu-id="cb719-450">Directorio, archivo</span><span class="sxs-lookup"><span data-stu-id="cb719-450">Directory, file</span></span></td>
      <td><span data-ttu-id="cb719-451">
        <font size=2> Protocolo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="cb719-451">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="cb719-452">Autenticación: {básica, oauth}</span><span class="sxs-lookup"><span data-stu-id="cb719-452">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="cb719-453">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-453">Address:</span></span> <br><span data-ttu-id="cb719-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-455">Hive</span><span class="sxs-lookup"><span data-stu-id="cb719-455">Hive</span></span></td>
      <td><span data-ttu-id="cb719-456">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-456">Container</span></span></td>
      <td><span data-ttu-id="cb719-457">Base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-457">Database</span></span></td>
      <td><span data-ttu-id="cb719-458">
        <font size=2> Protocolo: hive</span><span class="sxs-lookup"><span data-stu-id="cb719-458">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="cb719-459">Autenticación: {hdinsight, básica, nombre de usuario, no}</span><span class="sxs-lookup"><span data-stu-id="cb719-459">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="cb719-460">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-460">Address:</span></span> <br><span data-ttu-id="cb719-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-463">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="cb719-463">connectionProperties:</span></span> <br><span data-ttu-id="cb719-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-465">Hive</span><span class="sxs-lookup"><span data-stu-id="cb719-465">Hive</span></span></td>
      <td><span data-ttu-id="cb719-466">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-466">Table</span></span></td>
      <td><span data-ttu-id="cb719-467">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="cb719-467">Table, view</span></span></td>
      <td><span data-ttu-id="cb719-468">
        <font size=2> Protocolo: hive</span><span class="sxs-lookup"><span data-stu-id="cb719-468">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="cb719-469">Autenticación: {hdinsight, básica, nombre de usuario, no}</span><span class="sxs-lookup"><span data-stu-id="cb719-469">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="cb719-470">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-470">Address:</span></span> <br><span data-ttu-id="cb719-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="cb719-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="cb719-474">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="cb719-474">connectionProperties:</span></span> <br><span data-ttu-id="cb719-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-476">http</span><span class="sxs-lookup"><span data-stu-id="cb719-476">HTTP</span></span></td>
      <td><span data-ttu-id="cb719-477">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-477">Container</span></span></td>
      <td><span data-ttu-id="cb719-478">Sitio</span><span class="sxs-lookup"><span data-stu-id="cb719-478">Site</span></span></td>
      <td><span data-ttu-id="cb719-479">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="cb719-479">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="cb719-480">Autenticación: {no, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="cb719-480">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="cb719-481">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-481">Address:</span></span> <br><span data-ttu-id="cb719-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-483">http</span><span class="sxs-lookup"><span data-stu-id="cb719-483">HTTP</span></span></td>
      <td><span data-ttu-id="cb719-484">Informe</span><span class="sxs-lookup"><span data-stu-id="cb719-484">Report</span></span></td>
      <td><span data-ttu-id="cb719-485">Informe, panel</span><span class="sxs-lookup"><span data-stu-id="cb719-485">Report, dashboard</span></span></td>
      <td><span data-ttu-id="cb719-486">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="cb719-486">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="cb719-487">Autenticación: {no, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="cb719-487">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="cb719-488">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-488">Address:</span></span> <br><span data-ttu-id="cb719-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-490">http</span><span class="sxs-lookup"><span data-stu-id="cb719-490">HTTP</span></span></td>
      <td><span data-ttu-id="cb719-491">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-491">Table</span></span></td>
      <td><span data-ttu-id="cb719-492">Punto de conexión, archivo</span><span class="sxs-lookup"><span data-stu-id="cb719-492">Endpoint, file</span></span></td>
      <td><span data-ttu-id="cb719-493">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="cb719-493">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="cb719-494">Autenticación: {no, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="cb719-494">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="cb719-495">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-495">Address:</span></span> <br><span data-ttu-id="cb719-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-497">MySQL</span><span class="sxs-lookup"><span data-stu-id="cb719-497">MySQL</span></span></td>
      <td><span data-ttu-id="cb719-498">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-498">Container</span></span></td>
      <td><span data-ttu-id="cb719-499">Base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-499">Database</span></span></td>
      <td><span data-ttu-id="cb719-500">
        <font size=2> Protocolo: mysql</span><span class="sxs-lookup"><span data-stu-id="cb719-500">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="cb719-501">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-501">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="cb719-502">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-502">Address:</span></span> <br><span data-ttu-id="cb719-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-505">MySQL</span><span class="sxs-lookup"><span data-stu-id="cb719-505">MySQL</span></span></td>
      <td><span data-ttu-id="cb719-506">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-506">Table</span></span></td>
      <td><span data-ttu-id="cb719-507">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="cb719-507">Table, view</span></span></td>
      <td><span data-ttu-id="cb719-508">
        <font size=2> Protocolo: mysql</span><span class="sxs-lookup"><span data-stu-id="cb719-508">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="cb719-509">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-509">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="cb719-510">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-510">Address:</span></span> <br><span data-ttu-id="cb719-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-514">OData</span><span class="sxs-lookup"><span data-stu-id="cb719-514">OData</span></span></td>
      <td><span data-ttu-id="cb719-515">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-515">Container</span></span></td>
      <td><span data-ttu-id="cb719-516">Contenedor de entidades</span><span class="sxs-lookup"><span data-stu-id="cb719-516">Entity container</span></span></td>
      <td><span data-ttu-id="cb719-517">
        <font size=2> Protocolo: odata</span><span class="sxs-lookup"><span data-stu-id="cb719-517">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="cb719-518">Autenticación: {no, básica, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-518">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="cb719-519">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-519">Address:</span></span> <br><span data-ttu-id="cb719-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-521">OData</span><span class="sxs-lookup"><span data-stu-id="cb719-521">OData</span></span></td>
      <td><span data-ttu-id="cb719-522">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-522">Table</span></span></td>
      <td><span data-ttu-id="cb719-523">Conjunto de entidades, función</span><span class="sxs-lookup"><span data-stu-id="cb719-523">Entity set, function</span></span></td>
      <td><span data-ttu-id="cb719-524">
        <font size=2> Protocolo: odata</span><span class="sxs-lookup"><span data-stu-id="cb719-524">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="cb719-525">Autenticación: {no, básica, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-525">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="cb719-526">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-526">Address:</span></span> <br><span data-ttu-id="cb719-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="cb719-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="cb719-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; recurso </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-529">Base de datos de Oracle</span><span class="sxs-lookup"><span data-stu-id="cb719-529">Oracle Database</span></span></td>
      <td><span data-ttu-id="cb719-530">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-530">Container</span></span></td>
      <td><span data-ttu-id="cb719-531">Base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-531">Database</span></span></td>
      <td><span data-ttu-id="cb719-532">
        <font size=2> Protocolo: oracle</span><span class="sxs-lookup"><span data-stu-id="cb719-532">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="cb719-533">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-533">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="cb719-534">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-534">Address:</span></span> <br><span data-ttu-id="cb719-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-537">Base de datos de Oracle</span><span class="sxs-lookup"><span data-stu-id="cb719-537">Oracle Database</span></span></td>
      <td><span data-ttu-id="cb719-538">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-538">Table</span></span></td>
      <td><span data-ttu-id="cb719-539">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="cb719-539">Table, view</span></span></td>
      <td><span data-ttu-id="cb719-540">
        <font size=2> Protocolo: oracle</span><span class="sxs-lookup"><span data-stu-id="cb719-540">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="cb719-541">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-541">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="cb719-542">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-542">Address:</span></span> <br><span data-ttu-id="cb719-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="cb719-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="cb719-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-547">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="cb719-547">PostgreSQL</span></span></td>
      <td><span data-ttu-id="cb719-548">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-548">Container</span></span></td>
      <td><span data-ttu-id="cb719-549">Base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-549">Database</span></span></td>
      <td><span data-ttu-id="cb719-550">
        <font size=2> Protocolo: postgresql</span><span class="sxs-lookup"><span data-stu-id="cb719-550">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="cb719-551">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-551">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="cb719-552">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-552">Address:</span></span> <br><span data-ttu-id="cb719-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-555">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="cb719-555">PostgreSQL</span></span></td>
      <td><span data-ttu-id="cb719-556">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-556">Table</span></span></td>
      <td><span data-ttu-id="cb719-557">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="cb719-557">Table, view</span></span></td>
      <td><span data-ttu-id="cb719-558">
        <font size=2> Protocolo: postgresql</span><span class="sxs-lookup"><span data-stu-id="cb719-558">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="cb719-559">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-559">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="cb719-560">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-560">Address:</span></span> <br><span data-ttu-id="cb719-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="cb719-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="cb719-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-565">Power BI</span><span class="sxs-lookup"><span data-stu-id="cb719-565">Power BI</span></span></td>
      <td><span data-ttu-id="cb719-566">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-566">Container</span></span></td>
      <td><span data-ttu-id="cb719-567">Sitio</span><span class="sxs-lookup"><span data-stu-id="cb719-567">Site</span></span></td>
      <td><span data-ttu-id="cb719-568">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="cb719-568">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="cb719-569">Autenticación: {no, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="cb719-569">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="cb719-570">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-570">Address:</span></span> <br><span data-ttu-id="cb719-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-572">Power BI</span><span class="sxs-lookup"><span data-stu-id="cb719-572">Power BI</span></span></td>
      <td><span data-ttu-id="cb719-573">Informe</span><span class="sxs-lookup"><span data-stu-id="cb719-573">Report</span></span></td>
      <td><span data-ttu-id="cb719-574">Informe, panel</span><span class="sxs-lookup"><span data-stu-id="cb719-574">Report, dashboard</span></span></td>
      <td><span data-ttu-id="cb719-575">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="cb719-575">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="cb719-576">Autenticación: {no, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="cb719-576">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="cb719-577">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-577">Address:</span></span> <br><span data-ttu-id="cb719-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-579">Power Query</span><span class="sxs-lookup"><span data-stu-id="cb719-579">Power Query</span></span></td>
      <td><span data-ttu-id="cb719-580">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-580">Table</span></span></td>
      <td><span data-ttu-id="cb719-581">Mashup de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-581">Data mashup</span></span></td>
      <td><span data-ttu-id="cb719-582">
        <font size=2>Protocolo: power-query</span><span class="sxs-lookup"><span data-stu-id="cb719-582">
        <font size=2> Protocol: power-query</span></span> <br><span data-ttu-id="cb719-583">Autenticación: {oauth}</span><span class="sxs-lookup"><span data-stu-id="cb719-583">Authentication: {oauth}</span></span> <br><span data-ttu-id="cb719-584">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-584">Address:</span></span> <br><span data-ttu-id="cb719-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-586">Salesforce</span><span class="sxs-lookup"><span data-stu-id="cb719-586">Salesforce</span></span></td>
      <td><span data-ttu-id="cb719-587">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-587">Table</span></span></td>
      <td><span data-ttu-id="cb719-588">Objeto</span><span class="sxs-lookup"><span data-stu-id="cb719-588">Object</span></span></td>
      <td><span data-ttu-id="cb719-589">
        <font size=2> Protocolo: salesforce-com</span><span class="sxs-lookup"><span data-stu-id="cb719-589">
        <font size=2> Protocol: salesforce-com</span></span> <br><span data-ttu-id="cb719-590">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-590">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="cb719-591">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-591">Address:</span></span> <br><span data-ttu-id="cb719-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span><span class="sxs-lookup"><span data-stu-id="cb719-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span></span> <br><span data-ttu-id="cb719-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span><span class="sxs-lookup"><span data-stu-id="cb719-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span></span> <br><span data-ttu-id="cb719-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-595">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cb719-595">SAP HANA</span></span></td>
      <td><span data-ttu-id="cb719-596">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-596">Container</span></span></td>
      <td><span data-ttu-id="cb719-597">Server</span><span class="sxs-lookup"><span data-stu-id="cb719-597">Server</span></span></td>
      <td><span data-ttu-id="cb719-598">
        <font size=2> Protocolo: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="cb719-598">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="cb719-599">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-599">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="cb719-600">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-600">Address:</span></span> <br><span data-ttu-id="cb719-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-602">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cb719-602">SAP HANA</span></span></td>
      <td><span data-ttu-id="cb719-603">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-603">Table</span></span></td>
      <td><span data-ttu-id="cb719-604">Ver</span><span class="sxs-lookup"><span data-stu-id="cb719-604">View</span></span></td>
      <td><span data-ttu-id="cb719-605">
        <font size=2> Protocolo: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="cb719-605">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="cb719-606">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-606">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="cb719-607">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-607">Address:</span></span> <br><span data-ttu-id="cb719-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="cb719-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="cb719-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-611">SharePoint</span><span class="sxs-lookup"><span data-stu-id="cb719-611">SharePoint</span></span></td>
      <td><span data-ttu-id="cb719-612">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-612">Table</span></span></td>
      <td><span data-ttu-id="cb719-613">Enumerar</span><span class="sxs-lookup"><span data-stu-id="cb719-613">List</span></span></td>
      <td><span data-ttu-id="cb719-614">
        <font size=2> Protocolo: sharepoint-list</span><span class="sxs-lookup"><span data-stu-id="cb719-614">
        <font size=2> Protocol: sharepoint-list</span></span> <br><span data-ttu-id="cb719-615">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-615">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="cb719-616">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-616">Address:</span></span> <br><span data-ttu-id="cb719-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-618">Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="cb719-618">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="cb719-619">Comando</span><span class="sxs-lookup"><span data-stu-id="cb719-619">Command</span></span></td>
      <td><span data-ttu-id="cb719-620">Procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="cb719-620">Stored procedure</span></span></td>
      <td><span data-ttu-id="cb719-621">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="cb719-621">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="cb719-622">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-622">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="cb719-623">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-623">Address:</span></span> <br><span data-ttu-id="cb719-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="cb719-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="cb719-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-628">Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="cb719-628">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="cb719-629">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="cb719-629">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="cb719-630">Función con valores de tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-630">Table-valued function</span></span></td>
      <td><span data-ttu-id="cb719-631">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="cb719-631">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="cb719-632">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-632">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="cb719-633">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-633">Address:</span></span> <br><span data-ttu-id="cb719-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="cb719-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="cb719-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-638">Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="cb719-638">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="cb719-639">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-639">Container</span></span></td>
      <td><span data-ttu-id="cb719-640">Base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-640">Database</span></span></td>
      <td><span data-ttu-id="cb719-641">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="cb719-641">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="cb719-642">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-642">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="cb719-643">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-643">Address:</span></span> <br><span data-ttu-id="cb719-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-646">Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="cb719-646">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="cb719-647">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-647">Table</span></span></td>
      <td><span data-ttu-id="cb719-648">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="cb719-648">Table, view</span></span></td>
      <td><span data-ttu-id="cb719-649">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="cb719-649">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="cb719-650">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-650">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="cb719-651">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-651">Address:</span></span> <br><span data-ttu-id="cb719-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="cb719-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="cb719-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-656">SQL Server</span><span class="sxs-lookup"><span data-stu-id="cb719-656">SQL Server</span></span></td>
      <td><span data-ttu-id="cb719-657">Comando</span><span class="sxs-lookup"><span data-stu-id="cb719-657">Command</span></span></td>
      <td><span data-ttu-id="cb719-658">Procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="cb719-658">Stored procedure</span></span></td>
      <td><span data-ttu-id="cb719-659">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="cb719-659">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="cb719-660">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-660">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="cb719-661">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-661">Address:</span></span> <br><span data-ttu-id="cb719-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="cb719-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="cb719-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-666">SQL Server</span><span class="sxs-lookup"><span data-stu-id="cb719-666">SQL Server</span></span></td>
      <td><span data-ttu-id="cb719-667">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="cb719-667">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="cb719-668">Función con valores de tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-668">Table-valued function</span></span></td>
      <td><span data-ttu-id="cb719-669">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="cb719-669">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="cb719-670">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-670">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="cb719-671">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-671">Address:</span></span> <br><span data-ttu-id="cb719-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="cb719-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="cb719-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-676">SQL Server</span><span class="sxs-lookup"><span data-stu-id="cb719-676">SQL Server</span></span></td>
      <td><span data-ttu-id="cb719-677">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-677">Container</span></span></td>
      <td><span data-ttu-id="cb719-678">Base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-678">Database</span></span></td>
      <td><span data-ttu-id="cb719-679">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="cb719-679">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="cb719-680">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-680">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="cb719-681">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-681">Address:</span></span> <br><span data-ttu-id="cb719-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-684">SQL Server</span><span class="sxs-lookup"><span data-stu-id="cb719-684">SQL Server</span></span></td>
      <td><span data-ttu-id="cb719-685">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-685">Table</span></span></td>
      <td><span data-ttu-id="cb719-686">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="cb719-686">Table, view</span></span></td>
      <td><span data-ttu-id="cb719-687">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="cb719-687">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="cb719-688">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-688">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="cb719-689">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-689">Address:</span></span> <br><span data-ttu-id="cb719-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="cb719-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="cb719-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-694">SQL Server Analysis Services multidimensional</span><span class="sxs-lookup"><span data-stu-id="cb719-694">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="cb719-695">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-695">Container</span></span></td>
      <td><span data-ttu-id="cb719-696">Modelo</span><span class="sxs-lookup"><span data-stu-id="cb719-696">Model</span></span></td>
      <td><span data-ttu-id="cb719-697">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="cb719-697">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="cb719-698">Autenticación: {windows, básica, anónima, no}</span><span class="sxs-lookup"><span data-stu-id="cb719-698">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="cb719-699">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-699">Address:</span></span> <br><span data-ttu-id="cb719-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-703">SQL Server Analysis Services multidimensional</span><span class="sxs-lookup"><span data-stu-id="cb719-703">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="cb719-704">KPI</span><span class="sxs-lookup"><span data-stu-id="cb719-704">KPI</span></span></td>
      <td><span data-ttu-id="cb719-705">KPI</span><span class="sxs-lookup"><span data-stu-id="cb719-705">KPI</span></span></td>
      <td><span data-ttu-id="cb719-706">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="cb719-706">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="cb719-707">Autenticación: {windows, básica, anónima, no}</span><span class="sxs-lookup"><span data-stu-id="cb719-707">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="cb719-708">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-708">Address:</span></span> <br><span data-ttu-id="cb719-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="cb719-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="cb719-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="cb719-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="cb719-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-714">SQL Server Analysis Services multidimensional</span><span class="sxs-lookup"><span data-stu-id="cb719-714">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="cb719-715">Measure</span><span class="sxs-lookup"><span data-stu-id="cb719-715">Measure</span></span></td>
      <td><span data-ttu-id="cb719-716">Measure</span><span class="sxs-lookup"><span data-stu-id="cb719-716">Measure</span></span></td>
      <td><span data-ttu-id="cb719-717">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="cb719-717">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="cb719-718">Autenticación: {windows, básica, anónima, no}</span><span class="sxs-lookup"><span data-stu-id="cb719-718">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="cb719-719">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-719">Address:</span></span> <br><span data-ttu-id="cb719-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="cb719-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="cb719-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="cb719-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="cb719-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-725">SQL Server Analysis Services multidimensional</span><span class="sxs-lookup"><span data-stu-id="cb719-725">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="cb719-726">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-726">Table</span></span></td>
      <td><span data-ttu-id="cb719-727">Dimension Data</span><span class="sxs-lookup"><span data-stu-id="cb719-727">Dimension</span></span></td>
      <td><span data-ttu-id="cb719-728">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="cb719-728">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="cb719-729">Autenticación: {windows, básica, anónima, no}</span><span class="sxs-lookup"><span data-stu-id="cb719-729">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="cb719-730">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-730">Address:</span></span> <br><span data-ttu-id="cb719-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="cb719-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="cb719-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="cb719-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="cb719-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-736">Tabular de SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="cb719-736">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="cb719-737">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-737">Container</span></span></td>
      <td><span data-ttu-id="cb719-738">Modelo</span><span class="sxs-lookup"><span data-stu-id="cb719-738">Model</span></span></td>
      <td><span data-ttu-id="cb719-739">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="cb719-739">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="cb719-740">Autenticación: {windows, básica, anónima, no}</span><span class="sxs-lookup"><span data-stu-id="cb719-740">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="cb719-741">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-741">Address:</span></span> <br><span data-ttu-id="cb719-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-745">Tabular de SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="cb719-745">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="cb719-746">KPI</span><span class="sxs-lookup"><span data-stu-id="cb719-746">KPI</span></span></td>
      <td><span data-ttu-id="cb719-747">KPI</span><span class="sxs-lookup"><span data-stu-id="cb719-747">KPI</span></span></td>
      <td><span data-ttu-id="cb719-748">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="cb719-748">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="cb719-749">Autenticación: {windows, básica, anónima, no}</span><span class="sxs-lookup"><span data-stu-id="cb719-749">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="cb719-750">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-750">Address:</span></span> <br><span data-ttu-id="cb719-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="cb719-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="cb719-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="cb719-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="cb719-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-756">Tabular de SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="cb719-756">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="cb719-757">Measure</span><span class="sxs-lookup"><span data-stu-id="cb719-757">Measure</span></span></td>
      <td><span data-ttu-id="cb719-758">Measure</span><span class="sxs-lookup"><span data-stu-id="cb719-758">Measure</span></span></td>
      <td><span data-ttu-id="cb719-759">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="cb719-759">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="cb719-760">Autenticación: {windows, básica, anónima, no}</span><span class="sxs-lookup"><span data-stu-id="cb719-760">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="cb719-761">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-761">Address:</span></span> <br><span data-ttu-id="cb719-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="cb719-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="cb719-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="cb719-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="cb719-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-767">Tabular de SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="cb719-767">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="cb719-768">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-768">Table</span></span></td>
      <td><span data-ttu-id="cb719-769">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-769">Table</span></span></td>
      <td><span data-ttu-id="cb719-770">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="cb719-770">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="cb719-771">Autenticación: {windows, básica, anónima, no}</span><span class="sxs-lookup"><span data-stu-id="cb719-771">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="cb719-772">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-772">Address:</span></span> <br><span data-ttu-id="cb719-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="cb719-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="cb719-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="cb719-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="cb719-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-778">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="cb719-778">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="cb719-779">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-779">Container</span></span></td>
      <td><span data-ttu-id="cb719-780">Server</span><span class="sxs-lookup"><span data-stu-id="cb719-780">Server</span></span></td>
      <td><span data-ttu-id="cb719-781">
        <font size=2> Protocolo: reporting-services</span><span class="sxs-lookup"><span data-stu-id="cb719-781">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="cb719-782">Autenticación: {windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-782">Authentication: {windows}</span></span> <br><span data-ttu-id="cb719-783">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-783">Address:</span></span> <br><span data-ttu-id="cb719-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-786">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="cb719-786">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="cb719-787">Informe</span><span class="sxs-lookup"><span data-stu-id="cb719-787">Report</span></span></td>
      <td><span data-ttu-id="cb719-788">Informe</span><span class="sxs-lookup"><span data-stu-id="cb719-788">Report</span></span></td>
      <td><span data-ttu-id="cb719-789">
        <font size=2> Protocolo: reporting-services</span><span class="sxs-lookup"><span data-stu-id="cb719-789">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="cb719-790">Autenticación: {windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-790">Authentication: {windows}</span></span> <br><span data-ttu-id="cb719-791">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-791">Address:</span></span> <br><span data-ttu-id="cb719-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="cb719-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span></span> <br><span data-ttu-id="cb719-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-795">Teradata</span><span class="sxs-lookup"><span data-stu-id="cb719-795">Teradata</span></span></td>
      <td><span data-ttu-id="cb719-796">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-796">Container</span></span></td>
      <td><span data-ttu-id="cb719-797">Base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-797">Database</span></span></td>
      <td><span data-ttu-id="cb719-798">
        <font size=2> Protocolo: teradata</span><span class="sxs-lookup"><span data-stu-id="cb719-798">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="cb719-799">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-799">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="cb719-800">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-800">Address:</span></span> <br><span data-ttu-id="cb719-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-803">Teradata</span><span class="sxs-lookup"><span data-stu-id="cb719-803">Teradata</span></span></td>
      <td><span data-ttu-id="cb719-804">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-804">Table</span></span></td>
      <td><span data-ttu-id="cb719-805">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="cb719-805">Table, view</span></span></td>
      <td><span data-ttu-id="cb719-806">
        <font size=2> Protocolo: teradata</span><span class="sxs-lookup"><span data-stu-id="cb719-806">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="cb719-807">Autenticación: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-807">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="cb719-808">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-808">Address:</span></span> <br><span data-ttu-id="cb719-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-812">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="cb719-812">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="cb719-813">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-813">Container</span></span></td>
      <td><span data-ttu-id="cb719-814">Modelo</span><span class="sxs-lookup"><span data-stu-id="cb719-814">Model</span></span></td>
      <td><span data-ttu-id="cb719-815">
        <font size="2"> Protocolo: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="cb719-815">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="cb719-816">Autenticación: {windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-816">Authentication: {windows}</span></span> <br><span data-ttu-id="cb719-817">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-817">Address:</span></span> <br><span data-ttu-id="cb719-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="cb719-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="cb719-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="cb719-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="cb719-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; versión </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-821">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="cb719-821">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="cb719-822">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-822">Table</span></span></td>
      <td><span data-ttu-id="cb719-823">Entidad</span><span class="sxs-lookup"><span data-stu-id="cb719-823">Entity</span></span></td>
      <td><span data-ttu-id="cb719-824">
        <font size="2"> Protocolo: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="cb719-824">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="cb719-825">Autenticación: {windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-825">Authentication: {windows}</span></span> <br><span data-ttu-id="cb719-826">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-826">Address:</span></span> <br><span data-ttu-id="cb719-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="cb719-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="cb719-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="cb719-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="cb719-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; versión</span><span class="sxs-lookup"><span data-stu-id="cb719-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span></span> <br><span data-ttu-id="cb719-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entidad </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-831">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cb719-831">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="cb719-832">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-832">Container</span></span></td>
      <td><span data-ttu-id="cb719-833">Base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-833">Database</span></span></td>
      <td><span data-ttu-id="cb719-834">
        <font size=2> Protocolo: document-db</span><span class="sxs-lookup"><span data-stu-id="cb719-834">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="cb719-835">Autenticación: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="cb719-835">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="cb719-836">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-836">Address:</span></span> <br><span data-ttu-id="cb719-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="cb719-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="cb719-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-839">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cb719-839">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="cb719-840">Colección</span><span class="sxs-lookup"><span data-stu-id="cb719-840">Collection</span></span></td>
      <td><span data-ttu-id="cb719-841">Colección</span><span class="sxs-lookup"><span data-stu-id="cb719-841">Collection</span></span></td>
      <td><span data-ttu-id="cb719-842">
        <font size=2> Protocolo: document-db</span><span class="sxs-lookup"><span data-stu-id="cb719-842">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="cb719-843">Autenticación: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="cb719-843">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="cb719-844">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-844">Address:</span></span> <br><span data-ttu-id="cb719-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="cb719-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="cb719-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; colección </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-848">ODBC genérico</span><span class="sxs-lookup"><span data-stu-id="cb719-848">Generic ODBC</span></span></td>
      <td><span data-ttu-id="cb719-849">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-849">Container</span></span></td>
      <td><span data-ttu-id="cb719-850">Base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-850">Database</span></span></td>
      <td><span data-ttu-id="cb719-851">
        <font size=2> Protocolo: odbc</span><span class="sxs-lookup"><span data-stu-id="cb719-851">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="cb719-852">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-852">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="cb719-853">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-853">Address:</span></span> <br><span data-ttu-id="cb719-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; opciones</span><span class="sxs-lookup"><span data-stu-id="cb719-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="cb719-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-856">ODBC genérico</span><span class="sxs-lookup"><span data-stu-id="cb719-856">Generic ODBC</span></span></td>
      <td><span data-ttu-id="cb719-857">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-857">Table</span></span></td>
      <td><span data-ttu-id="cb719-858">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="cb719-858">Table, View</span></span></td>
      <td><span data-ttu-id="cb719-859">
        <font size=2> Protocolo: odbc</span><span class="sxs-lookup"><span data-stu-id="cb719-859">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="cb719-860">Autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-860">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="cb719-861">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-861">Address:</span></span> <br><span data-ttu-id="cb719-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; opciones</span><span class="sxs-lookup"><span data-stu-id="cb719-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="cb719-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="cb719-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="cb719-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-866">Sybase</span><span class="sxs-lookup"><span data-stu-id="cb719-866">Sybase</span></span></td>
      <td><span data-ttu-id="cb719-867">Contenedor</span><span class="sxs-lookup"><span data-stu-id="cb719-867">Container</span></span></td>
      <td><span data-ttu-id="cb719-868">Base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-868">Database</span></span></td>
      <td><span data-ttu-id="cb719-869">
        <font size=2> protocolo: sybase</span><span class="sxs-lookup"><span data-stu-id="cb719-869">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="cb719-870">autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-870">authentication: {basic, windows}</span></span> <br><span data-ttu-id="cb719-871">dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-871">address:</span></span> <br><span data-ttu-id="cb719-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-874">Sybase</span><span class="sxs-lookup"><span data-stu-id="cb719-874">Sybase</span></span></td>
      <td><span data-ttu-id="cb719-875">Tabla</span><span class="sxs-lookup"><span data-stu-id="cb719-875">Table</span></span></td>
      <td><span data-ttu-id="cb719-876">Tabla, vista</span><span class="sxs-lookup"><span data-stu-id="cb719-876">Table, View</span></span></td>
      <td><span data-ttu-id="cb719-877">
        <font size=2> protocolo: sybase</span><span class="sxs-lookup"><span data-stu-id="cb719-877">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="cb719-878">autenticación: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="cb719-878">authentication: {basic, windows}</span></span> <br><span data-ttu-id="cb719-879">dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-879">address:</span></span> <br><span data-ttu-id="cb719-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="cb719-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="cb719-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; base de datos</span><span class="sxs-lookup"><span data-stu-id="cb719-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="cb719-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="cb719-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="cb719-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="cb719-884">Otro (ninguno de los anteriores)</span><span class="sxs-lookup"><span data-stu-id="cb719-884">Other (none of the above)</span></span></td>
      <td>\*</td>
      <td>\*</td>
      <td><span data-ttu-id="cb719-885">
        <font size=2> Protocolo: generic-asset</span><span class="sxs-lookup"><span data-stu-id="cb719-885">
        <font size=2> Protocol: generic-asset</span></span> <br><span data-ttu-id="cb719-886">Dirección:</span><span class="sxs-lookup"><span data-stu-id="cb719-886">Address:</span></span> <br><span data-ttu-id="cb719-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span><span class="sxs-lookup"><span data-stu-id="cb719-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span></span></td>
    </tr>
</table>
