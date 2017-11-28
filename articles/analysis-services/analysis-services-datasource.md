---
title: "Orígenes de datos admitidos en Azure Analysis Services | Microsoft Docs"
description: "Describe los orígenes de datos admitidos para los modelos de datos en Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 6ec63319-ff9b-4b01-a1cd-274481dc8995
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 8bd6c3b5a923ce2f3cd0f60af82e59c5cc27cbb4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="data-sources-supported-in-azure-analysis-services"></a><span data-ttu-id="0f8d1-103">Orígenes de datos admitidos en Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="0f8d1-103">Data sources supported in Azure Analysis Services</span></span>
<span data-ttu-id="0f8d1-104">Los servidores de Azure Analysis Services admiten la conexión a orígenes de datos en la nube y de forma local en su organización.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-104">Azure Analysis Services servers support connecting to data sources in the cloud and on-premises in your organization.</span></span> <span data-ttu-id="0f8d1-105">Con el tiempo se van agregando más orígenes de datos compatibles,</span><span class="sxs-lookup"><span data-stu-id="0f8d1-105">Additional supported data sources are being added all the time.</span></span> <span data-ttu-id="0f8d1-106">por lo que se recomienda consultarlos con asiduidad.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-106">Check back often.</span></span> 

<span data-ttu-id="0f8d1-107">Actualmente se admiten los siguientes orígenes de datos:</span><span class="sxs-lookup"><span data-stu-id="0f8d1-107">The following data sources are currently supported:</span></span>

| <span data-ttu-id="0f8d1-108">Nube</span><span class="sxs-lookup"><span data-stu-id="0f8d1-108">Cloud</span></span>  |
|---|
| <span data-ttu-id="0f8d1-109">Azure Blob Storage*</span><span class="sxs-lookup"><span data-stu-id="0f8d1-109">Azure Blob Storage*</span></span>  |
| <span data-ttu-id="0f8d1-110">Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="0f8d1-110">Azure SQL Database</span></span>  |
| <span data-ttu-id="0f8d1-111">Almacenamiento de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="0f8d1-111">Azure Data Warehouse</span></span> |


| <span data-ttu-id="0f8d1-112">Local</span><span class="sxs-lookup"><span data-stu-id="0f8d1-112">On-premises</span></span>  |   |   |   |
|---|---|---|---|
| <span data-ttu-id="0f8d1-113">Base de datos de Access</span><span class="sxs-lookup"><span data-stu-id="0f8d1-113">Access Database</span></span>  | <span data-ttu-id="0f8d1-114">Carpeta*</span><span class="sxs-lookup"><span data-stu-id="0f8d1-114">Folder*</span></span> | <span data-ttu-id="0f8d1-115">Base de datos de Oracle</span><span class="sxs-lookup"><span data-stu-id="0f8d1-115">Oracle Database</span></span>  | <span data-ttu-id="0f8d1-116">Base de datos de Teradata</span><span class="sxs-lookup"><span data-stu-id="0f8d1-116">Teradata Database</span></span> |
| <span data-ttu-id="0f8d1-117">Active Directory*</span><span class="sxs-lookup"><span data-stu-id="0f8d1-117">Active Directory*</span></span>  | <span data-ttu-id="0f8d1-118">Documento JSON*</span><span class="sxs-lookup"><span data-stu-id="0f8d1-118">JSON document*</span></span>  | <span data-ttu-id="0f8d1-119">Base de datos de Postgre SQL*</span><span class="sxs-lookup"><span data-stu-id="0f8d1-119">Postgre SQL Database*</span></span>  |<span data-ttu-id="0f8d1-120">Tabla XML*</span><span class="sxs-lookup"><span data-stu-id="0f8d1-120">XML table*</span></span> |
| <span data-ttu-id="0f8d1-121">Analysis Services</span><span class="sxs-lookup"><span data-stu-id="0f8d1-121">Analysis Services</span></span>  | <span data-ttu-id="0f8d1-122">Líneas de archivo binario*</span><span class="sxs-lookup"><span data-stu-id="0f8d1-122">Lines from binary*</span></span>  | <span data-ttu-id="0f8d1-123">SAP HANA*</span><span class="sxs-lookup"><span data-stu-id="0f8d1-123">SAP HANA*</span></span>  |
| <span data-ttu-id="0f8d1-124">Analytics Platform System</span><span class="sxs-lookup"><span data-stu-id="0f8d1-124">Analytics Platform System</span></span>  | <span data-ttu-id="0f8d1-125">Base de datos MySQL</span><span class="sxs-lookup"><span data-stu-id="0f8d1-125">MySQL Database</span></span>  | <span data-ttu-id="0f8d1-126">SAP Business Warehouse*</span><span class="sxs-lookup"><span data-stu-id="0f8d1-126">SAP Business Warehouse*</span></span>  | |
| <span data-ttu-id="0f8d1-127">Dynamics CRM*</span><span class="sxs-lookup"><span data-stu-id="0f8d1-127">Dynamics CRM*</span></span>  | <span data-ttu-id="0f8d1-128">Fuente OData*</span><span class="sxs-lookup"><span data-stu-id="0f8d1-128">OData Feed*</span></span>  | <span data-ttu-id="0f8d1-129">SharePoint*</span><span class="sxs-lookup"><span data-stu-id="0f8d1-129">SharePoint*</span></span>  |
| <span data-ttu-id="0f8d1-130">Libro de Excel</span><span class="sxs-lookup"><span data-stu-id="0f8d1-130">Excel workbook</span></span>  | <span data-ttu-id="0f8d1-131">Consulta ODBC</span><span class="sxs-lookup"><span data-stu-id="0f8d1-131">ODBC query</span></span>  | <span data-ttu-id="0f8d1-132">SQL Database</span><span class="sxs-lookup"><span data-stu-id="0f8d1-132">SQL Database</span></span>  |
| <span data-ttu-id="0f8d1-133">Exchange*</span><span class="sxs-lookup"><span data-stu-id="0f8d1-133">Exchange*</span></span>  | <span data-ttu-id="0f8d1-134">OLE DB</span><span class="sxs-lookup"><span data-stu-id="0f8d1-134">OLE DB</span></span>  | <span data-ttu-id="0f8d1-135">Base de datos de Sybase</span><span class="sxs-lookup"><span data-stu-id="0f8d1-135">Sybase Database</span></span>  |

<span data-ttu-id="0f8d1-136">\* Solo modelos tabulares 1400.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-136">\* Tabular 1400 models only.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0f8d1-137">Para establecer conexión con orígenes de datos locales se debe instalar una [puerta de enlace de datos locales](analysis-services-gateway.md) en un equipo de su entorno.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-137">Connecting to on-premises data sources require an [On-premises data gateway](analysis-services-gateway.md) installed on a computer in your environment.</span></span>

## <a name="data-providers"></a><span data-ttu-id="0f8d1-138">Proveedores de datos</span><span class="sxs-lookup"><span data-stu-id="0f8d1-138">Data providers</span></span>

<span data-ttu-id="0f8d1-139">Los modelos de datos de Azure Analysis Services pueden requerir distintos proveedores de datos al conectarse a algunos orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-139">Data models in Azure Analysis Services may require different data providers when connecting to certain data sources.</span></span> <span data-ttu-id="0f8d1-140">En algunos casos, los modelos tabulares se conectan a orígenes de datos mediante proveedores nativos como SQL Server Native Client (SQLNCLI11) pueden devolver un error.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-140">In some cases, tabular models connecting to data sources using native providers such as SQL Server Native Client (SQLNCLI11) may return an error.</span></span>

<span data-ttu-id="0f8d1-141">Para los modelos de datos que se conectan a un origen de datos en la nube, como Azure SQL Database, si usa proveedores nativos que no sean SQLOLEDB, puede ver el mensaje de error: **"El proveedor 'SQLNCLI11.1' no está registrado"**.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-141">For data models that connect to a cloud data source such as Azure SQL Database, if you use native providers other than SQLOLEDB, you may see error message: **“The provider 'SQLNCLI11.1' is not registered.”**</span></span> <span data-ttu-id="0f8d1-142">O bien, si tiene un modelo DirectQuery conectarse a orígenes de datos locales, si utiliza los proveedores nativos, puede ver el mensaje de error: **"Error al crear el conjunto de filas OLE DB. Sintaxis incorrecta cerca de 'LIMIT'”**.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-142">Or, if you have a DirectQuery model connecting to on-premises data sources, if you use native providers you may see error message: **“Error creating OLE DB row set. Incorrect syntax near 'LIMIT'”**.</span></span>

<span data-ttu-id="0f8d1-143">Los siguientes proveedores de orígenes de datos se admiten en los modelos de datos en memoria o DirectQuery cuando se conectan a orígenes de datos locales o en la nube:</span><span class="sxs-lookup"><span data-stu-id="0f8d1-143">The following datasource providers are supported for in-memory or DirectQuery data models when connecting to data sources in the cloud or on-premises:</span></span>

### <a name="cloud"></a><span data-ttu-id="0f8d1-144">Nube</span><span class="sxs-lookup"><span data-stu-id="0f8d1-144">Cloud</span></span>
| <span data-ttu-id="0f8d1-145">**Origen de datos**</span><span class="sxs-lookup"><span data-stu-id="0f8d1-145">**Datasource**</span></span> | <span data-ttu-id="0f8d1-146">**En memoria**</span><span class="sxs-lookup"><span data-stu-id="0f8d1-146">**In-memory**</span></span> | <span data-ttu-id="0f8d1-147">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="0f8d1-147">**DirectQuery**</span></span> |
|  --- | --- | --- |
| <span data-ttu-id="0f8d1-148">Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="0f8d1-148">Azure SQL Data Warehouse</span></span> |<span data-ttu-id="0f8d1-149">Proveedor de datos .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="0f8d1-149">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="0f8d1-150">Proveedor de datos .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="0f8d1-150">.NET Framework Data Provider for SQL Server</span></span> |
| <span data-ttu-id="0f8d1-151">Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="0f8d1-151">Azure SQL Database</span></span> |<span data-ttu-id="0f8d1-152">Proveedor de datos .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="0f8d1-152">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="0f8d1-153">Proveedor de datos .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="0f8d1-153">.NET Framework Data Provider for SQL Server</span></span> | |

### <a name="on-premises-via-gateway"></a><span data-ttu-id="0f8d1-154">Local (mediante una puerta de enlace)</span><span class="sxs-lookup"><span data-stu-id="0f8d1-154">On-premises (via Gateway)</span></span>
|<span data-ttu-id="0f8d1-155">**Origen de datos**</span><span class="sxs-lookup"><span data-stu-id="0f8d1-155">**Datasource**</span></span> | <span data-ttu-id="0f8d1-156">**En memoria**</span><span class="sxs-lookup"><span data-stu-id="0f8d1-156">**In-memory**</span></span> | <span data-ttu-id="0f8d1-157">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="0f8d1-157">**DirectQuery**</span></span> |
|  --- | --- | --- |
| <span data-ttu-id="0f8d1-158">SQL Server</span><span class="sxs-lookup"><span data-stu-id="0f8d1-158">SQL Server</span></span> |<span data-ttu-id="0f8d1-159">SQL Server Native Client 11.0</span><span class="sxs-lookup"><span data-stu-id="0f8d1-159">SQL Server Native Client 11.0</span></span> |<span data-ttu-id="0f8d1-160">Proveedor de datos .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="0f8d1-160">.NET Framework Data Provider for SQL Server</span></span> |
| <span data-ttu-id="0f8d1-161">SQL Server</span><span class="sxs-lookup"><span data-stu-id="0f8d1-161">SQL Server</span></span> |<span data-ttu-id="0f8d1-162">Proveedor OLE DB de Microsoft para SQL Server</span><span class="sxs-lookup"><span data-stu-id="0f8d1-162">Microsoft OLE DB Provider for SQL Server</span></span> |<span data-ttu-id="0f8d1-163">Proveedor de datos .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="0f8d1-163">.NET Framework Data Provider for SQL Server</span></span> | |
| <span data-ttu-id="0f8d1-164">SQL Server</span><span class="sxs-lookup"><span data-stu-id="0f8d1-164">SQL Server</span></span> |<span data-ttu-id="0f8d1-165">Proveedor de datos .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="0f8d1-165">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="0f8d1-166">Proveedor de datos .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="0f8d1-166">.NET Framework Data Provider for SQL Server</span></span> | |
| <span data-ttu-id="0f8d1-167">Oracle</span><span class="sxs-lookup"><span data-stu-id="0f8d1-167">Oracle</span></span> |<span data-ttu-id="0f8d1-168">Proveedor OLE DB de Microsoft para Oracle</span><span class="sxs-lookup"><span data-stu-id="0f8d1-168">Microsoft OLE DB Provider for Oracle</span></span> |<span data-ttu-id="0f8d1-169">Proveedor de datos de Oracle para .NET</span><span class="sxs-lookup"><span data-stu-id="0f8d1-169">Oracle Data Provider for .NET</span></span> | |
| <span data-ttu-id="0f8d1-170">Oracle</span><span class="sxs-lookup"><span data-stu-id="0f8d1-170">Oracle</span></span> |<span data-ttu-id="0f8d1-171">Proveedor de datos de Oracle para .NET</span><span class="sxs-lookup"><span data-stu-id="0f8d1-171">Oracle Data Provider for .NET</span></span> |<span data-ttu-id="0f8d1-172">Proveedor de datos de Oracle para .NET</span><span class="sxs-lookup"><span data-stu-id="0f8d1-172">Oracle Data Provider for .NET</span></span> | |
| <span data-ttu-id="0f8d1-173">Teradata</span><span class="sxs-lookup"><span data-stu-id="0f8d1-173">Teradata</span></span> |<span data-ttu-id="0f8d1-174">Proveedor OLE DB para Teradata</span><span class="sxs-lookup"><span data-stu-id="0f8d1-174">OLE DB Provider for Teradata</span></span> |<span data-ttu-id="0f8d1-175">Proveedor de datos de Teradata para .NET</span><span class="sxs-lookup"><span data-stu-id="0f8d1-175">Teradata Data Provider for .NET</span></span> | |
| <span data-ttu-id="0f8d1-176">Teradata</span><span class="sxs-lookup"><span data-stu-id="0f8d1-176">Teradata</span></span> |<span data-ttu-id="0f8d1-177">Proveedor de datos de Teradata para .NET</span><span class="sxs-lookup"><span data-stu-id="0f8d1-177">Teradata Data Provider for .NET</span></span> |<span data-ttu-id="0f8d1-178">Proveedor de datos de Teradata para .NET</span><span class="sxs-lookup"><span data-stu-id="0f8d1-178">Teradata Data Provider for .NET</span></span> | |
| <span data-ttu-id="0f8d1-179">Analytics Platform System</span><span class="sxs-lookup"><span data-stu-id="0f8d1-179">Analytics Platform System</span></span> |<span data-ttu-id="0f8d1-180">Proveedor de datos .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="0f8d1-180">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="0f8d1-181">Proveedor de datos .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="0f8d1-181">.NET Framework Data Provider for SQL Server</span></span> | |

> [!NOTE]
> <span data-ttu-id="0f8d1-182">Asegúrese de que estén instalados proveedores de 64 bits cuando se use la puerta de enlace local.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-182">Ensure 64-bit providers are installed when using On-premises gateway.</span></span>
> 
> 

<span data-ttu-id="0f8d1-183">Cuando se migra un modelo tabular de SQL Server Analysis Services local a Azure Analysis Services, puede ser necesario cambiar el proveedor.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-183">When migrating an on-premises SQL Server Analysis Services tabular model to Azure Analysis Services, it may be necessary to change the provider.</span></span>

<span data-ttu-id="0f8d1-184">**Para especificar un proveedor de origen de datos**</span><span class="sxs-lookup"><span data-stu-id="0f8d1-184">**To specify a datasource provider**</span></span>

1. <span data-ttu-id="0f8d1-185">En SSDT > **Tabular Model Explorer**(Explorador de modelos tabulares) > **Orígenes de datos**, haga clic en una conexión de origen de datos y en **Editar origen de datos**.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-185">In SSDT > **Tabular Model Explorer** > **Data Sources**, right-click a data source connection, and then click **Edit Data Source**.</span></span>
2. <span data-ttu-id="0f8d1-186">En **Editar conexión**, haga clic en **Avanzadas** para abrir la ventana de propiedades avanzadas.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-186">In **Edit Connection**, click **Advanced** to open the Advance properties window.</span></span>
3. <span data-ttu-id="0f8d1-187">En **Establecer propiedades avanzadas** > **Proveedores**, seleccione el proveedor adecuado.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-187">In **Set Advanced Properties** > **Providers**, then select the appropriate provider.</span></span>

## <a name="impersonation"></a><span data-ttu-id="0f8d1-188">Suplantación</span><span class="sxs-lookup"><span data-stu-id="0f8d1-188">Impersonation</span></span>
<span data-ttu-id="0f8d1-189">En algunos casos, puede ser necesario especificar otra cuenta de suplantación.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-189">In some cases, it may be necessary to specify a different impersonation account.</span></span> <span data-ttu-id="0f8d1-190">La cuenta de suplantación se puede especificar en SSDT o SSMS.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-190">Impersonation account can be specified in SSDT or SSMS.</span></span>

<span data-ttu-id="0f8d1-191">Para orígenes de datos locales:</span><span class="sxs-lookup"><span data-stu-id="0f8d1-191">For on-premises data sources:</span></span>

* <span data-ttu-id="0f8d1-192">Si se utiliza la autenticación de SQL, la suplantación debe ser la Cuenta de servicio.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-192">If using SQL authentication, impersonation should be Service Account.</span></span>
* <span data-ttu-id="0f8d1-193">Si se utiliza la autenticación de Windows, establezca la contraseña y el usuario de Windows.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-193">If using Windows authentication, set Windows user/password.</span></span> <span data-ttu-id="0f8d1-194">Para SQL Server, se admite la autenticación de Windows con una cuenta de suplantación específica solo para los modelos de datos en memoria.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-194">For SQL Server, Windows authentication with a specific impersonation account is supported only for in-memory data models.</span></span>

<span data-ttu-id="0f8d1-195">Para orígenes de datos en la nube:</span><span class="sxs-lookup"><span data-stu-id="0f8d1-195">For cloud data sources:</span></span>

* <span data-ttu-id="0f8d1-196">Si se utiliza la autenticación de SQL, la suplantación debe ser la Cuenta de servicio.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-196">If using SQL authentication, impersonation should be Service Account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f8d1-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0f8d1-197">Next steps</span></span>
<span data-ttu-id="0f8d1-198">Si tiene orígenes de datos locales, asegúrese de instalar la [puerta de enlace local](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="0f8d1-198">If you have on-premises data sources, be sure to install the [On-premises gateway](analysis-services-gateway.md).</span></span>   
<span data-ttu-id="0f8d1-199">Para aprender más acerca de la administración del servidor en SSDT o SSMS, consulte el artículo sobre la[administración del servidor](analysis-services-manage.md).</span><span class="sxs-lookup"><span data-stu-id="0f8d1-199">To learn more about managing your server in SSDT or SSMS, see [Manage your server](analysis-services-manage.md).</span></span>

