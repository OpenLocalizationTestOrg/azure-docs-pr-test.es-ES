---
title: "aaaCreate y administrar los trabajos elásticos mediante PowerShell | Documentos de Microsoft"
description: Usar PowerShell toomanage grupos de base de datos de SQL Azure
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="2123c-103">Creación y administración de trabajos elásticos de SQL Database mediante PowerShell (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="2123c-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="2123c-104">Hola PowerShell APIs de **trabajos de base de datos elástica** (en versión preliminar), le permiten definir un grupo de bases de datos con el que se ejecutarán las secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="2123c-104">hello PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="2123c-105">Este artículo se muestra cómo toocreate y administrar **trabajos de base de datos elástica** mediante cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2123c-105">This article shows how toocreate and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="2123c-106">Consulte [Información general sobre trabajos elásticos](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2123c-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2123c-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2123c-107">Prerequisites</span></span>
* <span data-ttu-id="2123c-108">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="2123c-108">An Azure subscription.</span></span> <span data-ttu-id="2123c-109">Para obtener una prueba gratuita, vea [Prueba gratuita de un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2123c-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2123c-110">Un conjunto de bases de datos creadas con herramientas de base de datos elástica Hola.</span><span class="sxs-lookup"><span data-stu-id="2123c-110">A set of databases created with hello Elastic Database tools.</span></span> <span data-ttu-id="2123c-111">Consulte [Introducción a las herramientas de base de datos elástica](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2123c-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="2123c-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2123c-112">Azure PowerShell.</span></span> <span data-ttu-id="2123c-113">Para obtener información detallada, vea [cómo tooinstall y configurar Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2123c-113">For detailed information, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
* <span data-ttu-id="2123c-114">**Trabajos de base de datos elástica** : consulte [Installing Trabajos de base de datos elástica](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="2123c-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="2123c-115">Selección de su suscripción a Azure</span><span class="sxs-lookup"><span data-stu-id="2123c-115">Select your Azure subscription</span></span>
<span data-ttu-id="2123c-116">suscripción de hello tooselect necesita su Id. de suscripción (**- SubscriptionId**) o el nombre de la suscripción (**- SubscriptionName**).</span><span class="sxs-lookup"><span data-stu-id="2123c-116">tooselect hello subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="2123c-117">Si tiene varias suscripciones se puede ejecutar hello **AzureRmSubscription Get** información de suscripción del conjunto de resultados de hello deseada de Hola de cmdlet y copia.</span><span class="sxs-lookup"><span data-stu-id="2123c-117">If you have multiple subscriptions you can run hello **Get-AzureRmSubscription** cmdlet and copy hello desired subscription information from hello result set.</span></span> <span data-ttu-id="2123c-118">Una vez que tenga información de su suscripción, ejecutar Hola después commandlet tooset esta suscripción como valor predeterminado de hello, es decir Hola destino para crear y administrar trabajos:</span><span class="sxs-lookup"><span data-stu-id="2123c-118">Once you have your subscription information, run hello following commandlet tooset this subscription as hello default, namely hello target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="2123c-119">Hola [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) se recomienda para uso toodevelop y ejecutar los scripts de PowerShell frente a los trabajos de base de datos elástica Hola.</span><span class="sxs-lookup"><span data-stu-id="2123c-119">hello [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage toodevelop and execute PowerShell scripts against hello Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="2123c-120">Objetos de Trabajos de base de datos elástica</span><span class="sxs-lookup"><span data-stu-id="2123c-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="2123c-121">Hola siguiente tabla se enumeran todos los tipos de objeto de Hola de **trabajos de base de datos elástica** junto con su descripción y relevante APIs PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2123c-121">hello following table lists out all hello object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="2123c-122">Tipo de objeto</span><span class="sxs-lookup"><span data-stu-id="2123c-122">Object Type</span></span></th>
    <th><span data-ttu-id="2123c-123">Description</span><span class="sxs-lookup"><span data-stu-id="2123c-123">Description</span></span></th>
    <th><span data-ttu-id="2123c-124">API de PowerShell relacionadas</span><span class="sxs-lookup"><span data-stu-id="2123c-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="2123c-125">Credential:</span><span class="sxs-lookup"><span data-stu-id="2123c-125">Credential</span></span></td>
    <td><span data-ttu-id="2123c-126">Toouse de nombre de usuario y contraseña al conectar toodatabases para la ejecución de secuencias de comandos o aplicación de dacpac.</span><span class="sxs-lookup"><span data-stu-id="2123c-126">Username and password toouse when connecting toodatabases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="2123c-127">Hola contraseña se cifra antes de enviar tooand almacenar en la base de datos de hello trabajos elástico de base de datos.</span><span class="sxs-lookup"><span data-stu-id="2123c-127">hello password is encrypted before sending tooand storing in hello Elastic Database Jobs database.</span></span>  <span data-ttu-id="2123c-128">servicio de trabajos elástico de base de datos a través de la credencial de hello creado y cargado desde un script de instalación de Hola Hola descifra Hola contraseña.</span><span class="sxs-lookup"><span data-stu-id="2123c-128">hello password is decrypted by hello Elastic Database Jobs service via hello credential created and uploaded from hello installation script.</span></span></td>
    <td><p><span data-ttu-id="2123c-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="2123c-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="2123c-130">New-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="2123c-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="2123c-131">Set-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="2123c-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="2123c-132">Script</span><span class="sxs-lookup"><span data-stu-id="2123c-132">Script</span></span></td>
    <td><span data-ttu-id="2123c-133">Script de Transact-SQL toobe utilizado para la ejecución a través de las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="2123c-133">Transact-SQL script toobe used for execution across databases.</span></span>  <span data-ttu-id="2123c-134">script de Hola debe ser idempotente toobe creados desde servicio Hola volverá a intentar la ejecución del script de Hola tras errores.</span><span class="sxs-lookup"><span data-stu-id="2123c-134">hello script should be authored toobe idempotent since hello service will retry execution of hello script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="2123c-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="2123c-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="2123c-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="2123c-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="2123c-137">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="2123c-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="2123c-138">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="2123c-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="2123c-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="2123c-139">DACPAC</span></span></td>
    <td><span data-ttu-id="2123c-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Aplicación de capa de datos </a> toobe aplicada entre bases de datos del paquete.</span><span class="sxs-lookup"><span data-stu-id="2123c-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package toobe applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="2123c-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="2123c-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="2123c-142">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="2123c-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="2123c-143">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="2123c-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="2123c-144">Destino de la base de datos</span><span class="sxs-lookup"><span data-stu-id="2123c-144">Database Target</span></span></td>
    <td><span data-ttu-id="2123c-145">Base de datos y servidor nombre señalador tooan base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="2123c-145">Database and server name pointing tooan Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="2123c-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="2123c-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="2123c-147">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="2123c-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="2123c-148">Destino de mapa de particiones</span><span class="sxs-lookup"><span data-stu-id="2123c-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="2123c-149">Combinación de un destino de la base de datos y una credencial toobe utiliza toodetermine la información almacenada dentro de un mapa de particiones de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="2123c-149">Combination of a database target and a credential toobe used toodetermine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="2123c-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="2123c-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="2123c-151">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="2123c-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="2123c-152">Set-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="2123c-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="2123c-153">Destino de colección personalizada</span><span class="sxs-lookup"><span data-stu-id="2123c-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="2123c-154">Usar grupo definido de toocollectively de las bases de datos para la ejecución.</span><span class="sxs-lookup"><span data-stu-id="2123c-154">Defined group of databases toocollectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="2123c-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="2123c-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="2123c-156">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="2123c-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="2123c-157">Destino secundario de colección personalizada</span><span class="sxs-lookup"><span data-stu-id="2123c-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="2123c-158">Destino de base de datos al que se hace referencia en una colección personalizada.</span><span class="sxs-lookup"><span data-stu-id="2123c-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="2123c-159">Add-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="2123c-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="2123c-160">Remove-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="2123c-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="2123c-161">Trabajo</span><span class="sxs-lookup"><span data-stu-id="2123c-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="2123c-162">Definición de parámetros para un trabajo que pueden ser utilizados tootrigger ejecución o toofulfill una programación.</span><span class="sxs-lookup"><span data-stu-id="2123c-162">Definition of parameters for a job that can be used tootrigger execution or toofulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="2123c-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="2123c-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="2123c-164">New-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="2123c-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="2123c-165">Set-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="2123c-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="2123c-166">Ejecución de trabajos</span><span class="sxs-lookup"><span data-stu-id="2123c-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="2123c-167">Contenedor de tareas de toofulfill es necesario ejecutar una secuencia de comandos o aplicar un destino de tooa DACPAC con credenciales para las conexiones de base de datos con errores se controla en la directiva de ejecución de acuerdo tooan.</span><span class="sxs-lookup"><span data-stu-id="2123c-167">Container of tasks necessary toofulfill either executing a script or applying a DACPAC tooa target using credentials for database connections with failures handled in accordance tooan execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="2123c-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="2123c-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="2123c-169">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="2123c-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="2123c-170">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="2123c-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="2123c-171">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="2123c-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="2123c-172">Ejecución de tareas de trabajo</span><span class="sxs-lookup"><span data-stu-id="2123c-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="2123c-173">Unidad única de trabajo toofulfill un trabajo.</span><span class="sxs-lookup"><span data-stu-id="2123c-173">Single unit of work toofulfill a job.</span></span></p>
    <p><span data-ttu-id="2123c-174">Si una tarea de trabajo no es capaz de toosuccessfully ejecutar, se registrará el mensaje de excepción resultante de Hola y se creará una nueva tarea de trabajo coincidente y ejecutan en toohello según lo especificado directiva de ejecución.</span><span class="sxs-lookup"><span data-stu-id="2123c-174">If a job task is not able toosuccessfully execute, hello resulting exception message will be logged and a new matching job task will be created and executed in accordance toohello specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="2123c-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="2123c-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="2123c-176">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="2123c-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="2123c-177">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="2123c-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="2123c-178">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="2123c-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="2123c-179">Directiva de ejecución de trabajos</span><span class="sxs-lookup"><span data-stu-id="2123c-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="2123c-180">Controla los tiempos de espera, los límites de reintentos y los intervalos entre reintentos de la ejecución de trabajos.</span><span class="sxs-lookup"><span data-stu-id="2123c-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="2123c-181">Trabajos de base de datos elástica incluye una directiva de ejecución de trabajos predeterminada que, básicamente, producirá un número infinito de reintentos de errores de tareas de trabajo con retroceso exponencial de intervalos entre reintentos.</span><span class="sxs-lookup"><span data-stu-id="2123c-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="2123c-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="2123c-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="2123c-183">New-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="2123c-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="2123c-184">Set-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="2123c-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="2123c-185">Schedule</span><span class="sxs-lookup"><span data-stu-id="2123c-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="2123c-186">Tiempo según la especificación de contexto de ejecución tootake en un intervalo de repetición o de una sola vez.</span><span class="sxs-lookup"><span data-stu-id="2123c-186">Time based specification for execution tootake place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="2123c-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="2123c-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="2123c-188">New-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="2123c-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="2123c-189">Set-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="2123c-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="2123c-190">Desencadenadores de trabajo</span><span class="sxs-lookup"><span data-stu-id="2123c-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="2123c-191">Una asignación entre un trabajo y programación tootrigger ejecución de un trabajo según la programación de toohello.</span><span class="sxs-lookup"><span data-stu-id="2123c-191">A mapping between a job and a schedule tootrigger job execution according toohello schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="2123c-192">New-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="2123c-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="2123c-193">Remove-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="2123c-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="2123c-194">Tipos de grupo de trabajos de base de datos elástica admitidos</span><span class="sxs-lookup"><span data-stu-id="2123c-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="2123c-195">trabajo de Hello ejecuta scripts Transact-SQL (T-SQL) o una aplicación de DACPACs a través de un grupo de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="2123c-195">hello job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="2123c-196">Un trabajo una vez enviado toobe ejecutado a través de un grupo de bases de datos, trabajo Hola "expande" hello en los trabajos secundarios donde cada uno realiza Hola solicitó la ejecución en una base de datos en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2123c-196">When a job is submitted toobe executed across a group of databases, hello job “expands” hello into child jobs where each performs hello requested execution against a single database in hello group.</span></span> 

<span data-ttu-id="2123c-197">Hay dos tipos de grupos que puede crear:</span><span class="sxs-lookup"><span data-stu-id="2123c-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="2123c-198">[Mapa de particiones](sql-database-elastic-scale-shard-map-management.md) grupo: cuando un trabajo está tootarget enviado un mapa de particiones, Hola consulta toodetermine de mapa de particiones de hello su conjunto actual de particiones y, a continuación, crea secundarios trabajos para cada partición en el mapa de particiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="2123c-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted tootarget a shard map, hello job queries hello shard map toodetermine its current set of shards, and then creates child jobs for each shard in hello shard map.</span></span>
* <span data-ttu-id="2123c-199">Grupo Colección personalizada: conjunto personalizado de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="2123c-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="2123c-200">Cuando un trabajo está destinado a una colección personalizada, crea a secundarios trabajos para cada base de datos actualmente en la colección personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="2123c-200">When a job targets a custom collection, it creates child jobs for each database currently in hello custom collection.</span></span>

## <a name="tooset-hello-elastic-database-jobs-connection"></a><span data-ttu-id="2123c-201">Hola tooset conexión de base de datos elástica trabajos</span><span class="sxs-lookup"><span data-stu-id="2123c-201">tooset hello Elastic Database jobs connection</span></span>
<span data-ttu-id="2123c-202">Una conexión debe establecer toohello trabajos de toobe *base de datos de control* toousing anterior Hola trabajos API.</span><span class="sxs-lookup"><span data-stu-id="2123c-202">A connection needs toobe set toohello jobs *control database* prior toousing hello jobs APIs.</span></span> <span data-ttu-id="2123c-203">Si ejecuta este cmdlet, desencadena una toopop de ventana de credencial de solicitar el nombre de usuario de Hola y la contraseña que creó durante la instalación de los trabajos de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="2123c-203">Running this cmdlet triggers a credential window toopop up requesting hello user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="2123c-204">En todos los ejemplos que se ofrecen en este tema se da por hecho que este primer paso ya se realizó.</span><span class="sxs-lookup"><span data-stu-id="2123c-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="2123c-205">Abrir otra conexión toohello elástico de base de datos de trabajos:</span><span class="sxs-lookup"><span data-stu-id="2123c-205">Open a connection toohello Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a><span data-ttu-id="2123c-206">Credenciales cifradas dentro de los trabajos de base de datos elástica Hola</span><span class="sxs-lookup"><span data-stu-id="2123c-206">Encrypted credentials within hello Elastic Database jobs</span></span>
<span data-ttu-id="2123c-207">Las credenciales de la base de datos se pueden insertar en los trabajos de hello *base de datos de control* con su contraseña cifrada.</span><span class="sxs-lookup"><span data-stu-id="2123c-207">Database credentials can be inserted into hello jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="2123c-208">Es necesario toostore credenciales tooenable trabajos toobe ejecutado en un momento posterior, (uso de las programaciones de trabajo).</span><span class="sxs-lookup"><span data-stu-id="2123c-208">It is necessary toostore credentials tooenable jobs toobe executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="2123c-209">Cifrado funciona a través de un certificado creado como parte del script de instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2123c-209">Encryption works through a certificate created as part of hello installation script.</span></span> <span data-ttu-id="2123c-210">crea el script de instalación de Hola y certificado de Hola de cargas en hello servicio de nube de Azure para el descifrado de hello almacena contraseñas cifradas.</span><span class="sxs-lookup"><span data-stu-id="2123c-210">hello installation script creates and uploads hello certificate into hello Azure Cloud Service for decryption of hello stored encrypted passwords.</span></span> <span data-ttu-id="2123c-211">Hola servicio de nube de Azure más adelante guarda la clave pública de hello en los trabajos de hello *base de datos de control* que permite Hola API de PowerShell o el Portal de Azure clásico interfaz tooencrypt una contraseña proporcionada sin necesidad de certificado de Hola toobe instalado localmente.</span><span class="sxs-lookup"><span data-stu-id="2123c-211">hello Azure Cloud Service later stores hello public key within hello jobs *control database* which enables hello PowerShell API or Azure Classic Portal interface tooencrypt a provided password without requiring hello certificate toobe locally installed.</span></span>

<span data-ttu-id="2123c-212">las contraseñas de credencial de Hello son cifrada y segura de los usuarios con objetos de trabajos de base de datos de tooElastic de acceso de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="2123c-212">hello credential passwords are encrypted and secure from users with read-only access tooElastic Database jobs objects.</span></span> <span data-ttu-id="2123c-213">Pero es posible que un usuario malintencionado con acceso de lectura y escritura tooElastic trabajos de base de datos objetos tooextract una contraseña.</span><span class="sxs-lookup"><span data-stu-id="2123c-213">But it is possible for a malicious user with read-write access tooElastic Database Jobs objects tooextract a password.</span></span> <span data-ttu-id="2123c-214">Las credenciales son toobe diseñada reutilizar en las ejecuciones del trabajo.</span><span class="sxs-lookup"><span data-stu-id="2123c-214">Credentials are designed toobe reused across job executions.</span></span> <span data-ttu-id="2123c-215">Las credenciales se pasan las bases de datos de tootarget al establecer conexiones.</span><span class="sxs-lookup"><span data-stu-id="2123c-215">Credentials are passed tootarget databases when establishing connections.</span></span> <span data-ttu-id="2123c-216">Actualmente no hay ninguna restricción en bases de datos de destino de hello utilizadas para cada credencial, un usuario malintencionado podría agregar un destino de la base de datos para una base de datos bajo el control del usuario malintencionado Hola.</span><span class="sxs-lookup"><span data-stu-id="2123c-216">There are currently no restrictions on hello target databases used for each credential, malicious user could add a database target for a database under hello malicious user's control.</span></span> <span data-ttu-id="2123c-217">usuario de Hello posteriormente pudo iniciar un trabajo que se dirige a la contraseña del esta base de datos toogain Hola credencial.</span><span class="sxs-lookup"><span data-stu-id="2123c-217">hello user could subsequently start a job targeting this database toogain hello credential's password.</span></span>

<span data-ttu-id="2123c-218">Los procedimientos recomendados de seguridad para Trabajos de base de datos elástica son:</span><span class="sxs-lookup"><span data-stu-id="2123c-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="2123c-219">Limitar el uso de las personas de hello API tootrusted.</span><span class="sxs-lookup"><span data-stu-id="2123c-219">Limit usage of hello APIs tootrusted individuals.</span></span>
* <span data-ttu-id="2123c-220">Las credenciales deben tener Hola tarea de mínimos privilegios necesarios tooperform hello trabajo.</span><span class="sxs-lookup"><span data-stu-id="2123c-220">Credentials should have hello least privileges necessary tooperform hello job task.</span></span>  <span data-ttu-id="2123c-221">Puede ver más información en este artículo de MSDN sobre SQL Server, [Autorización y permisos](https://msdn.microsoft.com/library/bb669084.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2123c-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="2123c-222">toocreate una credencial para la ejecución de trabajos entre bases de datos cifrada</span><span class="sxs-lookup"><span data-stu-id="2123c-222">toocreate an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="2123c-223">toocreate un nuevo cifrado de credenciales, hello [ **cmdlet Get-Credential** ](https://technet.microsoft.com/library/hh849815.aspx) pide un nombre de usuario y una contraseña que se pueden pasar toohello [ **AzureSqlJobCredential de nuevo cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span><span class="sxs-lookup"><span data-stu-id="2123c-223">toocreate a new encrypted credential, hello [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed toohello [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a><span data-ttu-id="2123c-224">credenciales de tooupdate</span><span class="sxs-lookup"><span data-stu-id="2123c-224">tooupdate credentials</span></span>
<span data-ttu-id="2123c-225">Cuando cambien las contraseñas, usar hello [ **cmdlet Set-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) conjunto hello y **CredentialName** parámetro.</span><span class="sxs-lookup"><span data-stu-id="2123c-225">When passwords change, use hello [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) and set hello **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a><span data-ttu-id="2123c-226">toodefine un destino de asignación de particiones de bases de datos elásticas</span><span class="sxs-lookup"><span data-stu-id="2123c-226">toodefine an Elastic Database shard map target</span></span>
<span data-ttu-id="2123c-227">tooexecute un trabajo en todas las bases de datos en un conjunto de particiones (creado con [biblioteca de cliente de base de datos elástica](sql-database-elastic-database-client-library.md)), utiliza un mapa de particiones como destino de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2123c-227">tooexecute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as hello database target.</span></span> <span data-ttu-id="2123c-228">Este ejemplo requiere una aplicación particionada creada mediante la biblioteca de cliente de base de datos elástica Hola.</span><span class="sxs-lookup"><span data-stu-id="2123c-228">This example requires a sharded application created using hello Elastic Database client library.</span></span> <span data-ttu-id="2123c-229">Consulte [Introducción a las herramientas de Base de datos elástica](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2123c-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="2123c-230">base de datos de administrador de asignación de Hello particiones se debe establecer como destino de la base de datos y, a continuación, mapa de particiones específicas de hello debe especificarse como un destino.</span><span class="sxs-lookup"><span data-stu-id="2123c-230">hello shard map manager database must be set as a database target and then hello specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="2123c-231">Crear un script T-SQL para su ejecución transversal en las bases de datos</span><span class="sxs-lookup"><span data-stu-id="2123c-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="2123c-232">Al crear scripts de T-SQL para su ejecución, se recomienda encarecidamente toobuild les toobe [idempotente](https://en.wikipedia.org/wiki/Idempotence) y resistentes a los errores.</span><span class="sxs-lookup"><span data-stu-id="2123c-232">When creating T-SQL scripts for execution, it is highly recommended toobuild them toobe [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="2123c-233">Trabajos de base de datos elásticos volverá a intentar la ejecución de una secuencia de comandos cada vez que la ejecución encuentra un error, independientemente de clasificación de Hola de error de Hola.</span><span class="sxs-lookup"><span data-stu-id="2123c-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of hello classification of hello failure.</span></span>

<span data-ttu-id="2123c-234">Hola de uso [ **cmdlet New-AzureSqlJobContent** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate guardar un script para su ejecución y establezca hello **- ContentName** y **- CommandText**parámetros.</span><span class="sxs-lookup"><span data-stu-id="2123c-234">Use hello [**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate and save a script for execution and set hello **-ContentName** and **-CommandText** parameters.</span></span>

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="2123c-235">Creación de un script desde un archivo</span><span class="sxs-lookup"><span data-stu-id="2123c-235">Create a new script from a file</span></span>
<span data-ttu-id="2123c-236">Si Hola script T-SQL se define dentro de un archivo, use este script de Hola tooimport:</span><span class="sxs-lookup"><span data-stu-id="2123c-236">If hello T-SQL script is defined within a file, use this tooimport hello script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="2123c-237">secuencia de comandos de tooupdate un instrucción T-SQL para su ejecución en bases de datos</span><span class="sxs-lookup"><span data-stu-id="2123c-237">tooupdate a T-SQL script for execution across databases</span></span>
<span data-ttu-id="2123c-238">Estas actualizaciones de secuencia de comandos de PowerShell Hola texto de comando de T-SQL para un script existente.</span><span class="sxs-lookup"><span data-stu-id="2123c-238">This PowerShell script updates hello T-SQL command text for an existing script.</span></span>

<span data-ttu-id="2123c-239">Conjunto Hola siguiendo definición toobe conjunto de variables tooreflect Hola deseado script:</span><span class="sxs-lookup"><span data-stu-id="2123c-239">Set hello following variables tooreflect hello desired script definition toobe set:</span></span>

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a><span data-ttu-id="2123c-240">tooupdate Hola definición tooan secuencia de comandos existente</span><span class="sxs-lookup"><span data-stu-id="2123c-240">tooupdate hello definition tooan existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a><span data-ttu-id="2123c-241">toocreate un tooexecute de trabajo una secuencia de comandos a través de un mapa de particiones</span><span class="sxs-lookup"><span data-stu-id="2123c-241">toocreate a job tooexecute a script across a shard map</span></span>
<span data-ttu-id="2123c-242">El siguiente script de PowerShell inicia un trabajo para la ejecución de un script en cada partición de un mapa de particiones de escala elástica.</span><span class="sxs-lookup"><span data-stu-id="2123c-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="2123c-243">Hola conjunto después Hola de variables tooreflect había deseado script y destino:</span><span class="sxs-lookup"><span data-stu-id="2123c-243">Set hello following variables tooreflect hello desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a><span data-ttu-id="2123c-244">tooexecute un trabajo</span><span class="sxs-lookup"><span data-stu-id="2123c-244">tooexecute a job</span></span>
<span data-ttu-id="2123c-245">Este script de PowerShell ejecuta un trabajo existente:</span><span class="sxs-lookup"><span data-stu-id="2123c-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="2123c-246">Hola de actualización después de la variable tooreflect Hola deseado toohave de nombre de trabajo ejecuta:</span><span class="sxs-lookup"><span data-stu-id="2123c-246">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="2123c-247">estado de hello tooretrieve una única ejecución de trabajo</span><span class="sxs-lookup"><span data-stu-id="2123c-247">tooretrieve hello state of a single job execution</span></span>
<span data-ttu-id="2123c-248">Hola de uso [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) conjunto hello y **JobExecutionId** estado de hello tooview los parámetros de ejecución del trabajo.</span><span class="sxs-lookup"><span data-stu-id="2123c-248">Use hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) and set hello **JobExecutionId** parameter tooview hello state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="2123c-249">Use Hola mismo **Get AzureSqlJobExecution** cmdlet con hello **IncludeChildren** estado de hello tooview los parámetros de las ejecuciones de trabajo secundarios, es decir Hola estado específico para cada ejecución del trabajo en todas base de datos de destino de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2123c-249">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a><span data-ttu-id="2123c-250">estado de hello tooview a través de varias ejecuciones del trabajo</span><span class="sxs-lookup"><span data-stu-id="2123c-250">tooview hello state across multiple job executions</span></span>
<span data-ttu-id="2123c-251">Hola [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) tiene varios parámetros opcionales que pueden ser utilizado toodisplay múltiples ejecuciones del trabajo, filtradas mediante parámetros de hello proporcionado.</span><span class="sxs-lookup"><span data-stu-id="2123c-251">hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="2123c-252">siguiente Hello muestra algunas de hello formas toouse AzureSqlJobExecution Get:</span><span class="sxs-lookup"><span data-stu-id="2123c-252">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="2123c-253">Recuperar todas las ejecuciones de trabajos activos de nivel superior:</span><span class="sxs-lookup"><span data-stu-id="2123c-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="2123c-254">Recuperar todas las ejecuciones de trabajos de nivel superior, incluidas las ejecuciones de trabajos inactivos:</span><span class="sxs-lookup"><span data-stu-id="2123c-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="2123c-255">Recuperar todas las ejecuciones de trabajos secundarios de un identificador de ejecución de trabajos proporcionado, incluidas las ejecuciones de trabajos inactivos:</span><span class="sxs-lookup"><span data-stu-id="2123c-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="2123c-256">Recuperar todas las ejecuciones de trabajos creadas con una combinación de programación y trabajo, incluidos los trabajos inactivos:</span><span class="sxs-lookup"><span data-stu-id="2123c-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="2123c-257">Recuperar todos los trabajos que se destinan a un mapa de particiones especificado, incluidos los trabajos inactivos:</span><span class="sxs-lookup"><span data-stu-id="2123c-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="2123c-258">Recuperar todos los trabajos que se destinan a una colección personalizada especificada, incluidos los trabajos inactivos:</span><span class="sxs-lookup"><span data-stu-id="2123c-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="2123c-259">Recuperar la lista de Hola de ejecuciones de la tarea de trabajo dentro de la ejecución de un trabajo específico:</span><span class="sxs-lookup"><span data-stu-id="2123c-259">Retrieve hello list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="2123c-260">Recuperar los detalles de ejecución de tareas de trabajo:</span><span class="sxs-lookup"><span data-stu-id="2123c-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="2123c-261">Hola siguiente script de PowerShell puede ser utilizados tooview Hola detalles de una ejecución de la tarea de trabajo, que es especialmente útil al depurar errores de ejecución.</span><span class="sxs-lookup"><span data-stu-id="2123c-261">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a><span data-ttu-id="2123c-262">errores de tooretrieve dentro de las ejecuciones de tareas de trabajo</span><span class="sxs-lookup"><span data-stu-id="2123c-262">tooretrieve failures within job task executions</span></span>
<span data-ttu-id="2123c-263">Hola **JobTaskExecution objeto** incluye una propiedad para el ciclo de vida de Hola de tarea hello junto con una propiedad de mensaje.</span><span class="sxs-lookup"><span data-stu-id="2123c-263">hello **JobTaskExecution object** includes a property for hello lifecycle of hello task along with a message property.</span></span> <span data-ttu-id="2123c-264">Si se produce un error en una ejecución de la tarea de trabajo, propiedad de ciclo de vida de Hola se establecerá demasiado*error* y se establecerá la propiedad de mensaje de Hola toohello mensaje de excepción resultante y la pila.</span><span class="sxs-lookup"><span data-stu-id="2123c-264">If a job task execution failed, hello lifecycle property will be set too*Failed* and hello message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="2123c-265">Si un trabajo no es correcta, es importante tooview detalles de Hola de tareas de trabajo que no se realizó correctamente para un trabajo determinado.</span><span class="sxs-lookup"><span data-stu-id="2123c-265">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a><span data-ttu-id="2123c-266">toowait para un toocomplete de ejecución de trabajo</span><span class="sxs-lookup"><span data-stu-id="2123c-266">toowait for a job execution toocomplete</span></span>
<span data-ttu-id="2123c-267">Hola siguiente script de PowerShell puede ser usado toowait para un toocomplete de tareas de trabajo:</span><span class="sxs-lookup"><span data-stu-id="2123c-267">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="2123c-268">Crear una directiva de ejecución personalizada</span><span class="sxs-lookup"><span data-stu-id="2123c-268">Create a custom execution policy</span></span>
<span data-ttu-id="2123c-269">Trabajos de base de datos elástica admite la creación de directivas de ejecución personalizadas que se pueden aplicar al iniciar trabajos.</span><span class="sxs-lookup"><span data-stu-id="2123c-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="2123c-270">Actualmente, las directivas de ejecución permiten definir:</span><span class="sxs-lookup"><span data-stu-id="2123c-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="2123c-271">Nombre: Identificador de directiva de ejecución de Hola.</span><span class="sxs-lookup"><span data-stu-id="2123c-271">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="2123c-272">Tiempo de espera del trabajo: tiempo total antes de que Trabajos de base de datos elástica cancele un trabajo.</span><span class="sxs-lookup"><span data-stu-id="2123c-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="2123c-273">Intervalo de reintento inicial: Intervalo toowait antes del primer reintento.</span><span class="sxs-lookup"><span data-stu-id="2123c-273">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="2123c-274">Intervalo de reintento máximo: Límite de toouse de intervalos de reintento.</span><span class="sxs-lookup"><span data-stu-id="2123c-274">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="2123c-275">Coeficiente de retroceso de intervalo de reintento: Coeficiente utiliza el siguiente intervalo de saludo de toocalculate entre los reintentos.</span><span class="sxs-lookup"><span data-stu-id="2123c-275">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="2123c-276">Hello se utiliza siguiente fórmula: (intervalo de reintentos inicial) * Math.pow ((coeficiente de retroceso de intervalo), (número de intentos de) - 2).</span><span class="sxs-lookup"><span data-stu-id="2123c-276">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="2123c-277">Número máximo de intentos: número máximo de Hola de tooperform de intentos de reintento de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="2123c-277">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="2123c-278">Directiva de ejecución de Hello predeterminada utiliza Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="2123c-278">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="2123c-279">Nombre: directiva de ejecución predeterminada</span><span class="sxs-lookup"><span data-stu-id="2123c-279">Name: Default execution policy</span></span>
* <span data-ttu-id="2123c-280">Tiempo de espera del trabajo: 1 semana</span><span class="sxs-lookup"><span data-stu-id="2123c-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="2123c-281">Intervalo de reintento inicial: 100 milisegundos</span><span class="sxs-lookup"><span data-stu-id="2123c-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="2123c-282">Intervalo máximo de reintento: 30 minutos</span><span class="sxs-lookup"><span data-stu-id="2123c-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="2123c-283">Coeficiente de intervalo de reintento: 2</span><span class="sxs-lookup"><span data-stu-id="2123c-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="2123c-284">Número máximo de intentos: 2.147.483.647</span><span class="sxs-lookup"><span data-stu-id="2123c-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="2123c-285">Crear directiva de ejecución de hello deseado:</span><span class="sxs-lookup"><span data-stu-id="2123c-285">Create hello desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="2123c-286">Actualización de una directiva de ejecución personalizada</span><span class="sxs-lookup"><span data-stu-id="2123c-286">Update a custom execution policy</span></span>
<span data-ttu-id="2123c-287">Tooupdate de directiva de ejecución de actualización Hola deseado:</span><span class="sxs-lookup"><span data-stu-id="2123c-287">Update hello desired execution policy tooupdate:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="2123c-288">Cancelación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="2123c-288">Cancel a job</span></span>
<span data-ttu-id="2123c-289">Trabajos de base de datos elástica admite solicitudes de cancelación de trabajos.</span><span class="sxs-lookup"><span data-stu-id="2123c-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="2123c-290">Si los trabajos de base de datos elástica detecta una solicitud de cancelación de un trabajo que se está ejecutando actualmente, tratará de trabajo de hello toostop.</span><span class="sxs-lookup"><span data-stu-id="2123c-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="2123c-291">Trabajos de base de datos elástica puede realizar una cancelación de dos formas distintas:</span><span class="sxs-lookup"><span data-stu-id="2123c-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="2123c-292">Cancelar están ejecutando tareas actualmente: si se detecta una cancelación mientras una tarea se está ejecutando actualmente, se intentará una cancelación dentro de hello ejecutando el aspecto de la tarea hello.</span><span class="sxs-lookup"><span data-stu-id="2123c-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="2123c-293">Por ejemplo: si hay una consulta de ejecución prolongada que se están llevando a cabo cuando se intenta realizar una cancelación, habrá una consulta de hello toocancel intento.</span><span class="sxs-lookup"><span data-stu-id="2123c-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="2123c-294">Cancelación de reintentos: si se detecta una cancelación por subproceso de control de hello antes de que se inicia una tarea para su ejecución, el subproceso de control de Hola se evitar iniciar tarea hello y declarar solicitud hello como cancelada.</span><span class="sxs-lookup"><span data-stu-id="2123c-294">Canceling task retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="2123c-295">Si se solicita una cancelación de trabajo para un trabajo primario, se respetará la solicitud de cancelación de Hola de trabajo primario de Hola y para todos los trabajos secundarios.</span><span class="sxs-lookup"><span data-stu-id="2123c-295">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="2123c-296">toosubmit una solicitud de cancelación, utilice hello [ **cmdlet Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) conjunto hello y **JobExecutionId** parámetro.</span><span class="sxs-lookup"><span data-stu-id="2123c-296">toosubmit a cancellation request, use hello [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) and set hello **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="2123c-297">toodelete un trabajo y el historial de trabajos de forma asincrónica</span><span class="sxs-lookup"><span data-stu-id="2123c-297">toodelete a job and job history asynchronously</span></span>
<span data-ttu-id="2123c-298">Trabajos de base de datos elástica admite la eliminación asincrónica de trabajos.</span><span class="sxs-lookup"><span data-stu-id="2123c-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="2123c-299">Un trabajo se puede marcar para su eliminación y sistema de hello eliminará trabajo hello y su historial de trabajo una vez han completado todas las ejecuciones del trabajo para el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2123c-299">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="2123c-300">sistema de Hello no cancelará automáticamente las ejecuciones del trabajo activo.</span><span class="sxs-lookup"><span data-stu-id="2123c-300">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="2123c-301">Invocar [ **Stop AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel ejecuciones de trabajo activo.</span><span class="sxs-lookup"><span data-stu-id="2123c-301">Invoke [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel active job executions.</span></span>

<span data-ttu-id="2123c-302">eliminación de trabajo tootrigger, use hello [ **cmdlet Remove-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) conjunto hello y **JobName** parámetro.</span><span class="sxs-lookup"><span data-stu-id="2123c-302">tootrigger job deletion, use hello [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) and set hello **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a><span data-ttu-id="2123c-303">toocreate un destino de la base de datos personalizada</span><span class="sxs-lookup"><span data-stu-id="2123c-303">toocreate a custom database target</span></span>
<span data-ttu-id="2123c-304">Puede definir bases de datos de destino personalizadas para la ejecución directa o para su inclusión en un grupo personalizado de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="2123c-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="2123c-305">Por ejemplo, porque **grupos elásticos** están aún no admiten directamente mediante PowerShell APIs, puede crear un destino de la base de datos personalizada y el destino de la colección de base de datos personalizada que abarca todas las bases de datos de hello en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2123c-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="2123c-306">Establecer Hola siguiendo la información de base de datos de las variables tooreflect Hola deseado:</span><span class="sxs-lookup"><span data-stu-id="2123c-306">Set hello following variables tooreflect hello desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a><span data-ttu-id="2123c-307">toocreate un destino de recopilación de la base de datos personalizada</span><span class="sxs-lookup"><span data-stu-id="2123c-307">toocreate a custom database collection target</span></span>
<span data-ttu-id="2123c-308">Hola de uso [ **New-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) toodefine cmdlet una ejecución de tooenable del destino de colección personalizada de la base de datos a través de varios destinos de la base de datos definido.</span><span class="sxs-lookup"><span data-stu-id="2123c-308">Use hello [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine a custom database collection target tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="2123c-309">Después de crear un grupo de base de datos, se pueden asociadas con el destino de colección personalizada hello las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="2123c-309">After creating a database group, databases can be associated with hello custom collection target.</span></span>

<span data-ttu-id="2123c-310">Establecer Hola siguiente configuración de destino de colección personalizada deseada de variables tooreflect hello:</span><span class="sxs-lookup"><span data-stu-id="2123c-310">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="2123c-311">destino de colección de base de datos personalizada tooa de tooadd las bases de datos</span><span class="sxs-lookup"><span data-stu-id="2123c-311">tooadd databases tooa custom database collection target</span></span>
<span data-ttu-id="2123c-312">tooadd una recopilación personalizada específica de tooa de base de datos use hello [ **agregar AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2123c-312">tooadd a database tooa specific custom collection use hello [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="2123c-313">Revise las bases de datos de hello dentro de un destino de colección de la base de datos personalizada</span><span class="sxs-lookup"><span data-stu-id="2123c-313">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="2123c-314">Hola de uso [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) bases de datos de cmdlet tooretrieve Hola secundarios dentro de un destino de colección de la base de datos personalizada.</span><span class="sxs-lookup"><span data-stu-id="2123c-314">Use hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve hello child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="2123c-315">Crear una secuencia de comandos de un tooexecute de trabajo a través de un destino de recopilación de la base de datos personalizada</span><span class="sxs-lookup"><span data-stu-id="2123c-315">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="2123c-316">Hola de uso [ **New-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) toocreate cmdlet un trabajo para un grupo de bases de datos definidas por un destino de recopilación de la base de datos personalizada.</span><span class="sxs-lookup"><span data-stu-id="2123c-316">Use hello [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="2123c-317">Trabajos de base de datos elásticos expandirán trabajo hello en varios puestos de secundarios cada base de datos correspondiente de tooa asociados con el destino de colección de base de datos personalizada hello y asegúrese de que se ejecuta el script de Hola en cada base de datos.</span><span class="sxs-lookup"><span data-stu-id="2123c-317">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="2123c-318">Una vez más, es importante que los scripts son idempotentes toobe resistente tooretries.</span><span class="sxs-lookup"><span data-stu-id="2123c-318">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="2123c-319">Recopilación de datos de una base de datos a otra</span><span class="sxs-lookup"><span data-stu-id="2123c-319">Data collection across databases</span></span>
<span data-ttu-id="2123c-320">Puede usar un tooexecute una consulta de trabajo a través de un grupo de bases de datos y tabla específica de hello resultados tooa de envío.</span><span class="sxs-lookup"><span data-stu-id="2123c-320">You can use a job tooexecute a query across a group of databases and send hello results tooa specific table.</span></span> <span data-ttu-id="2123c-321">tabla de Hello puede consultarse después Hola hechos toosee Hola resultados de la consulta de cada base de datos.</span><span class="sxs-lookup"><span data-stu-id="2123c-321">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="2123c-322">Esto proporciona un método asincrónico tooexecute una consulta entre varias bases de datos.</span><span class="sxs-lookup"><span data-stu-id="2123c-322">This provides an asynchronous method tooexecute a query across many databases.</span></span> <span data-ttu-id="2123c-323">Los intentos incorrectos se controlan automáticamente mediante reintentos.</span><span class="sxs-lookup"><span data-stu-id="2123c-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="2123c-324">tabla de destino especificado de Hola se creará automáticamente si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="2123c-324">hello specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="2123c-325">nueva tabla de Hello coincide con esquema Hola de hello devolvió un conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="2123c-325">hello new table matches hello schema of hello returned result set.</span></span> <span data-ttu-id="2123c-326">Si una secuencia de comandos devuelve varios conjuntos de resultados, trabajos de base de datos elástica sólo enviará la primera tabla de destino toohello Hola.</span><span class="sxs-lookup"><span data-stu-id="2123c-326">If a script returns multiple result sets, Elastic Database jobs will only send hello first toohello destination table.</span></span>

<span data-ttu-id="2123c-327">Hola siguiente script de PowerShell ejecuta una secuencia de comandos y recopila los resultados en una tabla especificada.</span><span class="sxs-lookup"><span data-stu-id="2123c-327">hello following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="2123c-328">Este script presupone que se creó un script T-SQL que genera un único conjunto de resultados y que se creó una colección de bases de datos personalizada de destino.</span><span class="sxs-lookup"><span data-stu-id="2123c-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="2123c-329">Este script utiliza hello [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2123c-329">This script uses hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span></span> <span data-ttu-id="2123c-330">Establecer los parámetros de hello para la secuencia de comandos, las credenciales y de destino de ejecución:</span><span class="sxs-lookup"><span data-stu-id="2123c-330">Set hello parameters for script, credentials, and execution target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="2123c-331">toocreate e iniciar un trabajo para escenarios de recopilación de datos</span><span class="sxs-lookup"><span data-stu-id="2123c-331">toocreate and start a job for data collection scenarios</span></span>
<span data-ttu-id="2123c-332">Este script utiliza hello [ **inicio AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2123c-332">This script uses hello [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span></span>

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a><span data-ttu-id="2123c-333">tooschedule un desencadenador de ejecución de trabajo</span><span class="sxs-lookup"><span data-stu-id="2123c-333">tooschedule a job execution trigger</span></span>
<span data-ttu-id="2123c-334">Hola siguiente script de PowerShell puede ser utilizado toocreate una programación periódica.</span><span class="sxs-lookup"><span data-stu-id="2123c-334">hello following PowerShell script can be used toocreate a recurring schedule.</span></span> <span data-ttu-id="2123c-335">Este script usa un intervalo de minutos, pero [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) también admite los parámetros -DayInterval, -HourInterval, -MonthInterval y -WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="2123c-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="2123c-336">Se pueden crear programaciones que se ejecutan una sola vez pasando -OneTime.</span><span class="sxs-lookup"><span data-stu-id="2123c-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="2123c-337">Creación de una programación:</span><span class="sxs-lookup"><span data-stu-id="2123c-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="2123c-338">tootrigger un trabajo que se ejecuta según una programación de tiempo</span><span class="sxs-lookup"><span data-stu-id="2123c-338">tootrigger a job executed on a time schedule</span></span>
<span data-ttu-id="2123c-339">Un desencadenador de trabajo puede ser toohave definido una programación de tiempo de trabajo ejecuta correspondiente tooa.</span><span class="sxs-lookup"><span data-stu-id="2123c-339">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="2123c-340">Hola siguiente script de PowerShell pueden toocreate usa un desencadenador de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2123c-340">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="2123c-341">Use [AzureSqlJobTrigger New](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) y conjunto Hola siguiendo las variables toocorrespond toohello deseado trabajo y una programación:</span><span class="sxs-lookup"><span data-stu-id="2123c-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) and set hello following variables toocorrespond toohello desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="2123c-342">tooremove un trabajo de toostop asociación programada de ejecutarse en programación</span><span class="sxs-lookup"><span data-stu-id="2123c-342">tooremove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="2123c-343">se puede quitar toodiscontinue recurrente de ejecución del trabajo a través de un desencadenador de trabajo, el desencadenador de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2123c-343">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span> <span data-ttu-id="2123c-344">Quitar un toostop de desencadenador de trabajo un trabajo del que se está ejecutando correspondiente programación tooa con hello [ **cmdlet Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span><span class="sxs-lookup"><span data-stu-id="2123c-344">Remove a job trigger toostop a job from being executed according tooa schedule using hello [**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a><span data-ttu-id="2123c-345">Recuperar la programación de tiempo de trabajo desencadenadores tooa enlazado</span><span class="sxs-lookup"><span data-stu-id="2123c-345">Retrieve job triggers bound tooa time schedule</span></span>
<span data-ttu-id="2123c-346">Hola siguiente script de PowerShell puede tooobtain usado y mostrar programación de tiempo determinado de hello trabajo desencadenadores tooa registrados.</span><span class="sxs-lookup"><span data-stu-id="2123c-346">hello following PowerShell script can be used tooobtain and display hello job triggers registered tooa particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a><span data-ttu-id="2123c-347">desencadenadores de trabajo tooretrieve enlazados tooa trabajo</span><span class="sxs-lookup"><span data-stu-id="2123c-347">tooretrieve job triggers bound tooa job</span></span>
<span data-ttu-id="2123c-348">Use [AzureSqlJobTrigger Get](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain y mostrar programaciones que contiene un trabajo registrado.</span><span class="sxs-lookup"><span data-stu-id="2123c-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="2123c-349">toocreate una aplicación de capa de datos (DACPAC) para la ejecución a través de las bases de datos</span><span class="sxs-lookup"><span data-stu-id="2123c-349">toocreate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="2123c-350">vea toocreate un DACPAC [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span><span class="sxs-lookup"><span data-stu-id="2123c-350">toocreate a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="2123c-351">toodeploy un DACPAC, usar hello [cmdlet New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span><span class="sxs-lookup"><span data-stu-id="2123c-351">toodeploy a DACPAC, use hello [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span></span> <span data-ttu-id="2123c-352">Hola DACPAC debe ser accesible toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="2123c-352">hello DACPAC must be accessible toohello service.</span></span> <span data-ttu-id="2123c-353">Es recomendable tooupload una tooAzure DACPAC creado almacenamiento y crear un [firma de acceso compartido](../storage/common/storage-dotnet-shared-access-signature-part-1.md) para hello DACPAC.</span><span class="sxs-lookup"><span data-stu-id="2123c-353">It is recommended tooupload a created DACPAC tooAzure Storage and create a [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for hello DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="2123c-354">tooupdate una aplicación de capa de datos (DACPAC) para la ejecución a través de las bases de datos</span><span class="sxs-lookup"><span data-stu-id="2123c-354">tooupdate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="2123c-355">Dacpac existente registrado en un período trabajos elástico de base de datos puede ser actualizada toopoint toonew URI.</span><span class="sxs-lookup"><span data-stu-id="2123c-355">Existing DACPACs registered within Elastic Database Jobs can be updated toopoint toonew URIs.</span></span> <span data-ttu-id="2123c-356">Hola de uso [ **cmdlet Set-AzureSqlJobContentDefinition** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI en una existente registrado DACPAC:</span><span class="sxs-lookup"><span data-stu-id="2123c-356">Use hello [**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="2123c-357">toocreate una tooapply una aplicación de capa de datos (DACPAC) a través de las bases de datos de trabajo</span><span class="sxs-lookup"><span data-stu-id="2123c-357">toocreate a job tooapply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="2123c-358">Una vez creado un DACPAC en trabajos elástico de base de datos, un trabajo puede crearse tooapply hello DACPAC a través de un grupo de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="2123c-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created tooapply hello DACPAC across a group of databases.</span></span> <span data-ttu-id="2123c-359">Hola siguiente script de PowerShell pueden toocreate usa un trabajo DACPAC a través de una colección personalizada de las bases de datos:</span><span class="sxs-lookup"><span data-stu-id="2123c-359">hello following PowerShell script can be used toocreate a DACPAC job across a custom collection of databases:</span></span>

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
