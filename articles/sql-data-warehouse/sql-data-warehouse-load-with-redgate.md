---
title: almacenamiento de datos de Azure de aaaUse Redgate tooload datos tooyour | Documentos de Microsoft
description: "Obtenga información acerca de cómo Studio del toouse Redgate de plataforma de datos para escenarios de almacenamiento de datos."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a><span data-ttu-id="32264-103">Carga de datos con Redgate's Data Platform Studio</span><span class="sxs-lookup"><span data-stu-id="32264-103">Load data with Redgate Data Platform Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="32264-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="32264-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)
> * [<span data-ttu-id="32264-105">Factoría de datos</span><span class="sxs-lookup"><span data-stu-id="32264-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [<span data-ttu-id="32264-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="32264-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)
> * [<span data-ttu-id="32264-107">BCP</span><span class="sxs-lookup"><span data-stu-id="32264-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="32264-108">Este tutorial muestra cómo toouse [datos plataforma Studio del Redgate](http://www.red-gate.com/products/azure-development/data-platform-studio/) datos de toomove (DP) desde un tooAzure de SQL Server local almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="32264-108">This tutorial shows you how toouse [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) toomove data from an on-premises SQL Server tooAzure SQL Data Warehouse.</span></span> <span data-ttu-id="32264-109">Studio de la plataforma de datos aplica correcciones de compatibilidad más adecuadas de Hola y optimizaciones, por lo que tiene más rápido Hola tooget de manera que se inició con almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="32264-109">Data Platform Studio applies hello most appropriate compatibility fixes and optimizations, so it's hello quickest way tooget started with SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="32264-110">[Redgate](http://www.red-gate.com) es un experimentado asociado de Microsoft que ofrece diversas herramientas de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="32264-110">[Redgate](http://www.red-gate.com) is a long-time Microsoft partner that delivers various SQL Server tools.</span></span> <span data-ttu-id="32264-111">Esta característica de Data Platform Studio está disponible gratuitamente para uso comercial y no comercial.</span><span class="sxs-lookup"><span data-stu-id="32264-111">This feature in Data Platform Studio has been made available freely for both commercial and non-commercial use.</span></span>
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="32264-112">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="32264-112">Before you begin</span></span>
### <a name="create-or-identify-resources"></a><span data-ttu-id="32264-113">Creación o identificación de recursos</span><span class="sxs-lookup"><span data-stu-id="32264-113">Create or identify resources</span></span>
<span data-ttu-id="32264-114">Antes de iniciar este tutorial, necesita toohave:</span><span class="sxs-lookup"><span data-stu-id="32264-114">Before starting this tutorial, you need toohave:</span></span>

* <span data-ttu-id="32264-115">**base de datos de SQL Server local**: Hola datos que desea tooimport tooSQL almacenamiento de datos necesita toocome desde un servidor local de SQL (versión 2008R2 o superior).</span><span class="sxs-lookup"><span data-stu-id="32264-115">**on-premises SQL Server Database**: hello data you want tooimport tooSQL Data Warehouse needs toocome from an on-premises SQL Server (version 2008R2 or above).</span></span> <span data-ttu-id="32264-116">Data Platform Studio no puede importar datos directamente desde Azure SQL Database ni desde archivos de texto.</span><span class="sxs-lookup"><span data-stu-id="32264-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span></span>
* <span data-ttu-id="32264-117">**Cuenta de almacenamiento de Azure**: datos de hello en el almacenamiento de blobs de Azure cree etapas en Studio de la plataforma de datos antes de cargarlos en el almacén de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="32264-117">**Azure Storage Account**: Data Platform Studio stages hello data in Azure Blob Storage before loading it into SQL Data Warehouse.</span></span> <span data-ttu-id="32264-118">cuenta de almacenamiento de Hello debe utilizar modelo de implementación de "Administrador de recursos" hello (valor predeterminado de Hola) en lugar del modelo de implementación "Clásico" Hola.</span><span class="sxs-lookup"><span data-stu-id="32264-118">hello storage account must be using hello “Resource Manager” deployment model (hello default) rather than hello “Classic” deployment model.</span></span> <span data-ttu-id="32264-119">Si no tienes una cuenta de almacenamiento, obtenga información acerca de cómo tooCreate una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="32264-119">If you don't have a storage account, learn how tooCreate a storage account.</span></span> 
* <span data-ttu-id="32264-120">**Almacenamiento de datos SQL**: este tutorial mueve datos Hola de tooSQL de SQL Server local almacenamiento de datos, por lo que necesita toohave un almacenamiento de datos en línea.</span><span class="sxs-lookup"><span data-stu-id="32264-120">**SQL Data Warehouse**: This tutorial moves hello data from on-premises SQL Server tooSQL Data Warehouse, so you need toohave a data warehouse online.</span></span> <span data-ttu-id="32264-121">Si no dispone de un almacén de datos, obtenga información acerca de cómo tooCreate un almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="32264-121">If you do not already have a data warehouse, learn how tooCreate an Azure SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="32264-122">El rendimiento mejora si la cuenta de almacenamiento de Hola y Hola data warehouse se crean en hello misma región.</span><span class="sxs-lookup"><span data-stu-id="32264-122">Performance is improved if hello storage account and hello data warehouse are created in hello same region.</span></span>
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a><span data-ttu-id="32264-123">Paso 1: Iniciar sesión en tooData Studio plataforma con su cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="32264-123">Step 1: Sign in tooData Platform Studio with your Azure account</span></span>
<span data-ttu-id="32264-124">Abra el explorador web y navegue toohello [Studio de la plataforma de datos](https://www.dataplatformstudio.com/) sitio Web.</span><span class="sxs-lookup"><span data-stu-id="32264-124">Open your web browser and navigate toohello [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span></span> <span data-ttu-id="32264-125">Inicio de sesión con Hola misma cuenta de Azure que le toocreate usado Hola almacenamiento cuenta de almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="32264-125">Sign in with hello same Azure account that you used toocreate hello storage account and data warehouse.</span></span> <span data-ttu-id="32264-126">Si su dirección de correo electrónico está asociado con un trabajo o a la cuenta del centro educativo y una cuenta de Microsoft, ser cuenta de hello toochoose seguro de que tiene acceso a los recursos de tooyour.</span><span class="sxs-lookup"><span data-stu-id="32264-126">If your email address is associated with both a work or school account and a Microsoft account, be sure toochoose hello account that has access tooyour resources.</span></span>

> [!NOTE]
> <span data-ttu-id="32264-127">Si se trata de la primera vez que usa Studio de la plataforma de datos, son más frecuentes toogrant Hola aplicación permiso toomanage los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="32264-127">If this is your first time using Data Platform Studio, you are asked toogrant hello application permission toomanage your Azure resources.</span></span>
> 
> 

## <a name="step-2-start-hello-import-wizard"></a><span data-ttu-id="32264-128">Paso 2: Iniciar el Asistente para la importación de Hola</span><span class="sxs-lookup"><span data-stu-id="32264-128">Step 2: Start hello Import Wizard</span></span>
<span data-ttu-id="32264-129">Desde la pantalla principal de DP de bienvenida, seleccione a hello tooAzure almacenamiento de datos SQL vínculo toostart Hola importación Asistente para la importación.</span><span class="sxs-lookup"><span data-stu-id="32264-129">From hello DPS main screen, select hello Import tooAzure SQL Data Warehouse link toostart hello import wizard.</span></span>

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a><span data-ttu-id="32264-130">Paso 3: Instalar la puerta de enlace de datos plataforma Studio Hola</span><span class="sxs-lookup"><span data-stu-id="32264-130">Step 3: Install hello Data Platform Studio Gateway</span></span>
<span data-ttu-id="32264-131">tooconnect tooyour en SQL Server base de datos local, deberá tooinstall Hola DP puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="32264-131">tooconnect tooyour on-premises SQL Server database, you need tooinstall hello DPS Gateway.</span></span> <span data-ttu-id="32264-132">puerta de enlace de Hello es un agente de cliente que proporciona acceso tooyour entorno local extrae datos de Hola y lo carga en la cuenta de almacenamiento de tooyour.</span><span class="sxs-lookup"><span data-stu-id="32264-132">hello gateway is a client agent that provides access tooyour on-premises environment, extracts hello data, and uploads it tooyour storage account.</span></span> <span data-ttu-id="32264-133">Los datos nunca pasan a través de los servidores de Redgate.</span><span class="sxs-lookup"><span data-stu-id="32264-133">Your data never passes through Redgate’s servers.</span></span> <span data-ttu-id="32264-134">Hola tooinstall puerta de enlace:</span><span class="sxs-lookup"><span data-stu-id="32264-134">tooinstall hello Gateway:</span></span>

1. <span data-ttu-id="32264-135">Haga clic en hello **crear puerta de enlace** vínculo</span><span class="sxs-lookup"><span data-stu-id="32264-135">Click hello **Create Gateway** link</span></span>
2. <span data-ttu-id="32264-136">Descarga e instalación Hola puerta de enlace con Hola el instalador proporcionado</span><span class="sxs-lookup"><span data-stu-id="32264-136">Download and install hello Gateway using hello provided installer</span></span>

![][2]

> [!NOTE]
> <span data-ttu-id="32264-137">Hola puerta de enlace puede instalarse en cualquier equipo con la base de datos de SQL Server de origen de toohello de red acceso.</span><span class="sxs-lookup"><span data-stu-id="32264-137">hello Gateway can be installed on any machine with network access toohello source SQL Server database.</span></span> <span data-ttu-id="32264-138">Tiene acceso a la base de datos de SQL Server de hello mediante la autenticación de Windows con credenciales de saludo del usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="32264-138">It accesses hello SQL Server database using Windows authentication with hello credentials of hello current user.</span></span>
> 
> 

<span data-ttu-id="32264-139">Una vez instalado, Hola tooConnected de cambios de estado de puerta de enlace y puede seleccionar siguiente.</span><span class="sxs-lookup"><span data-stu-id="32264-139">Once installed, hello Gateway status changes tooConnected and you can select Next.</span></span>

## <a name="step-4-identify-hello-source-database"></a><span data-ttu-id="32264-140">Paso 4: Identificar la base de datos de origen de Hola</span><span class="sxs-lookup"><span data-stu-id="32264-140">Step 4: Identify hello source database</span></span>
<span data-ttu-id="32264-141">Hola *escriba el nombre del servidor* cuadro de texto, escriba Hola nombre de hello servidor que hospeda la base de datos y seleccione **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="32264-141">In hello *Enter Server Name* textbox, enter hello name of hello server that hosts your database and select **Next**.</span></span> <span data-ttu-id="32264-142">A continuación, desde el menú desplegable de hello, seleccione base de datos de hello de que desea tooimport datos.</span><span class="sxs-lookup"><span data-stu-id="32264-142">Then, from hello drop-down menu, select hello database you want tooimport data from.</span></span>

![][3]

<span data-ttu-id="32264-143">DP inspecciona la base de datos seleccionada de Hola para tablas tooimport.</span><span class="sxs-lookup"><span data-stu-id="32264-143">DPS inspects hello selected database for tables tooimport.</span></span> <span data-ttu-id="32264-144">De forma predeterminada, DP importa todas las tablas de hello en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="32264-144">By default, DPS imports all hello tables in hello database.</span></span> <span data-ttu-id="32264-145">Puede seleccionar o anular la selección de tablas expandiendo Hola todas las tablas de vínculo.</span><span class="sxs-lookup"><span data-stu-id="32264-145">You can select or deselect tables by expanding hello All Tables link.</span></span> <span data-ttu-id="32264-146">Seleccione toomove siguiente de botón Hola al día.</span><span class="sxs-lookup"><span data-stu-id="32264-146">Select hello Next button toomove forward.</span></span>

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a><span data-ttu-id="32264-147">Paso 5: Elija un almacenamiento cuenta toostage Hola de datos</span><span class="sxs-lookup"><span data-stu-id="32264-147">Step 5: Choose a storage account toostage hello data</span></span>
<span data-ttu-id="32264-148">DP le solicitará una ubicación toostage Hola de datos.</span><span class="sxs-lookup"><span data-stu-id="32264-148">DPS prompts you for a location toostage hello data.</span></span> <span data-ttu-id="32264-149">Elija una cuenta de almacenamiento existente de la suscripción y seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="32264-149">Choose an existing storage account from your subscription and select **Next**.</span></span>

> [!NOTE]
> <span data-ttu-id="32264-150">DP creará un nuevo contenedor de blob en hello elegido cuenta de almacenamiento y utilizar una carpeta distinta para cada importación.</span><span class="sxs-lookup"><span data-stu-id="32264-150">DPS will create a new blob container in hello chosen storage account and use a distinct folder for each import.</span></span>
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a><span data-ttu-id="32264-151">Paso 6: Selección del almacenamiento de datos</span><span class="sxs-lookup"><span data-stu-id="32264-151">Step 6: Select a data warehouse</span></span>
<span data-ttu-id="32264-152">A continuación, seleccione en línea [almacenamiento de datos de SQL Azure](http://aka.ms/sqldw) tooimport datos de hello en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="32264-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database tooimport hello data into.</span></span> <span data-ttu-id="32264-153">Una vez que haya seleccionado la base de datos, necesita tooenter Hola credenciales tooconnect toohello la base de datos y seleccione **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="32264-153">Once you've selected your database, you need tooenter hello credentials tooconnect toohello database and select **Next**.</span></span>

![][5]

> [!NOTE]
> <span data-ttu-id="32264-154">DP combina tablas de datos de origen de hello en almacenamiento de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="32264-154">DPS merges hello source data tables into hello data warehouse.</span></span> <span data-ttu-id="32264-155">DP le advierte si el nombre de tabla Hola requiere toooverwrite tablas existentes en almacenamiento de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="32264-155">DPS warns you if hello table name requires it toooverwrite existing tables in hello data warehouse.</span></span> <span data-ttu-id="32264-156">Opcionalmente, puede eliminar los objetos existentes en almacenamiento de datos de hello haciendo clic en eliminar todos los objetos existentes antes de la importación.</span><span class="sxs-lookup"><span data-stu-id="32264-156">You may optionally delete any existing objects in hello data warehouse by ticking Delete all existing objects before import.</span></span>
> 
> 

## <a name="step-7-import-hello-data"></a><span data-ttu-id="32264-157">Paso 7: Importar datos de Hola</span><span class="sxs-lookup"><span data-stu-id="32264-157">Step 7: Import hello data</span></span>
<span data-ttu-id="32264-158">DP confirma que desea incluir los datos de hello tooimport.</span><span class="sxs-lookup"><span data-stu-id="32264-158">DPS confirms that you would like tooimport hello data.</span></span> <span data-ttu-id="32264-159">Simplemente haga clic en la importación de datos de hello inicio importación botón toobegin Hola.</span><span class="sxs-lookup"><span data-stu-id="32264-159">Simply click hello Start import button toobegin hello data import.</span></span>

![][6]

<span data-ttu-id="32264-160">DP muestra una visualización que muestra el progreso de Hola de extracción y carga de datos Hola Hola local SQL Server y Hola del progreso de la importación de hello en almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="32264-160">DPS displays a visualization that shows hello progress of extracting and uploading hello data from hello on-premises SQL Server and hello progress of hello import into SQL Data Warehouse.</span></span>

![][7]

<span data-ttu-id="32264-161">Una vez completada la importación de hello, DP muestra un resumen de importación de datos de Hola y Hola de correcciones de compatibilidad que se han realizado un informe de cambios.</span><span class="sxs-lookup"><span data-stu-id="32264-161">Once hello import is complete, DPS displays a summary of hello data import and a change report of hello compatibility fixes that have been performed.</span></span>

![][8]

## <a name="next-steps"></a><span data-ttu-id="32264-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="32264-162">Next steps</span></span>
<span data-ttu-id="32264-163">tooexplore sus datos en almacenamiento de datos de SQL, iniciar, consulte:</span><span class="sxs-lookup"><span data-stu-id="32264-163">tooexplore your data within SQL Data Warehouse, start by viewing:</span></span>

* <span data-ttu-id="32264-164">[Consultas en Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span><span class="sxs-lookup"><span data-stu-id="32264-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span></span>
* <span data-ttu-id="32264-165">[Visualización de datos con Power BI][Visualize data with Power BI]</span><span class="sxs-lookup"><span data-stu-id="32264-165">[Visualize data with Power BI][Visualize data with Power BI]</span></span>

<span data-ttu-id="32264-166">toolearn más información acerca datos plataforma Studio del Redgate:</span><span class="sxs-lookup"><span data-stu-id="32264-166">toolearn more about Redgate’s Data Platform Studio:</span></span>

* [<span data-ttu-id="32264-167">Visite la página principal de DP de Hola</span><span class="sxs-lookup"><span data-stu-id="32264-167">Visit hello DPS homepage</span></span>](http://www.dataplatformstudio.com/)
* [<span data-ttu-id="32264-168">Vea una demostración de DPS en Channel9</span><span class="sxs-lookup"><span data-stu-id="32264-168">Watch a demo of DPS on Channel9</span></span>](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

<span data-ttu-id="32264-169">Para obtener información general de otras maneras toomigrate y carga los datos en el almacén de datos de SQL consulte:</span><span class="sxs-lookup"><span data-stu-id="32264-169">For an overview of other ways toomigrate and load your data in SQL Data Warehouse see:</span></span>

* <span data-ttu-id="32264-170">[Migrar el almacenamiento de datos de solución tooSQL][Migrate your solution tooSQL Data Warehouse]</span><span class="sxs-lookup"><span data-stu-id="32264-170">[Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse]</span></span>
* [<span data-ttu-id="32264-171">Carga de datos en Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="32264-171">Load data into Azure SQL Data Warehouse</span></span>](sql-data-warehouse-overview-load.md)

<span data-ttu-id="32264-172">Para más sugerencias de desarrollo, vea hello [Introducción al desarrollo de almacenamiento de datos de SQL](sql-data-warehouse-overview-develop.md).</span><span class="sxs-lookup"><span data-stu-id="32264-172">For more development tips, see hello [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
