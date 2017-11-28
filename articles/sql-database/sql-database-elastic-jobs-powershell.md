---
title: "Creación y administración de trabajos elásticos mediante PowerShell | Microsoft Docs"
description: PowerShell usada para administrar grupos de Base de datos SQL de Azure
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
ms.openlocfilehash: b4c97e8f51581f9a3f7c5a8d8e82562255fe7b48
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="dce76-103">Creación y administración de trabajos elásticos de SQL Database mediante PowerShell (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="dce76-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="dce76-104">Las API de PowerShell para **Trabajos de base de datos elástica** permtein definir el grupo de bases de datos en las que se ejecutarán los scripts.</span><span class="sxs-lookup"><span data-stu-id="dce76-104">The PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="dce76-105">Este artículo muestra cómo crear y administrar **trabajos de base de datos elástica** mediante cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dce76-105">This article shows how to create and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="dce76-106">Consulte [Información general sobre trabajos elásticos](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dce76-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="dce76-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dce76-107">Prerequisites</span></span>
* <span data-ttu-id="dce76-108">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="dce76-108">An Azure subscription.</span></span> <span data-ttu-id="dce76-109">Para obtener una prueba gratuita, vea [Prueba gratuita de un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dce76-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="dce76-110">Un conjunto de bases de datos creadas con las herramientas de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="dce76-110">A set of databases created with the Elastic Database tools.</span></span> <span data-ttu-id="dce76-111">Consulte [Introducción a las herramientas de base de datos elástica](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dce76-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="dce76-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dce76-112">Azure PowerShell.</span></span> <span data-ttu-id="dce76-113">Para obtener información detallada, vea [Instalación y configuración de Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dce76-113">For detailed information, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
* <span data-ttu-id="dce76-114">**Trabajos de base de datos elástica** : consulte [Installing Trabajos de base de datos elástica](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="dce76-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="dce76-115">Selección de su suscripción a Azure</span><span class="sxs-lookup"><span data-stu-id="dce76-115">Select your Azure subscription</span></span>
<span data-ttu-id="dce76-116">Para seleccionar la suscripción, necesitará el identificador de la suscripción (**-SubscriptionId**) o el nombre de la suscripción (**-SubscriptionName**).</span><span class="sxs-lookup"><span data-stu-id="dce76-116">To select the subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="dce76-117">Si dispone de varias suscripciones, puede ejecutar el cmdlet **Get-AzureRmSubscription** y copiar la información de la suscripción que quiera del conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="dce76-117">If you have multiple subscriptions you can run the **Get-AzureRmSubscription** cmdlet and copy the desired subscription information from the result set.</span></span> <span data-ttu-id="dce76-118">Cuando tenga la información de la suscripción, ejecute el siguiente cmdlet para establecer esta suscripción como predeterminada, es decir, el destino para crear y administrar trabajos:</span><span class="sxs-lookup"><span data-stu-id="dce76-118">Once you have your subscription information, run the following commandlet to set this subscription as the default, namely the target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="dce76-119">Se recomienda el uso de [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) para desarrollar y ejecutar scripts de PowerShell en Trabajos de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="dce76-119">The [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage to develop and execute PowerShell scripts against the Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="dce76-120">Objetos de Trabajos de base de datos elástica</span><span class="sxs-lookup"><span data-stu-id="dce76-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="dce76-121">En la tabla siguiente se enumeran todos los tipos de objetos de **Trabajos de base de datos elástica** con su descripción y las API de PowerShell relevantes.</span><span class="sxs-lookup"><span data-stu-id="dce76-121">The following table lists out all the object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="dce76-122">Tipo de objeto</span><span class="sxs-lookup"><span data-stu-id="dce76-122">Object Type</span></span></th>
    <th><span data-ttu-id="dce76-123">Description</span><span class="sxs-lookup"><span data-stu-id="dce76-123">Description</span></span></th>
    <th><span data-ttu-id="dce76-124">API de PowerShell relacionadas</span><span class="sxs-lookup"><span data-stu-id="dce76-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="dce76-125">Credential:</span><span class="sxs-lookup"><span data-stu-id="dce76-125">Credential</span></span></td>
    <td><span data-ttu-id="dce76-126">Nombre de usuario y contraseña que se usará al conectarse a bases de datos para la ejecución de scripts o la aplicación de archivos DACPAC.</span><span class="sxs-lookup"><span data-stu-id="dce76-126">Username and password to use when connecting to databases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="dce76-127">La contraseña se cifra antes de enviarla y almacenarla en la base de datos de Trabajos de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="dce76-127">The password is encrypted before sending to and storing in the Elastic Database Jobs database.</span></span>  <span data-ttu-id="dce76-128">El servicio Trabajos de base de datos elástica descifra la contraseña a través de la credencial que se creó y cargó desde el script de instalación.</span><span class="sxs-lookup"><span data-stu-id="dce76-128">The password is decrypted by the Elastic Database Jobs service via the credential created and uploaded from the installation script.</span></span></td>
    <td><p><span data-ttu-id="dce76-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="dce76-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="dce76-130">New-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="dce76-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="dce76-131">Set-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="dce76-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="dce76-132">Script</span><span class="sxs-lookup"><span data-stu-id="dce76-132">Script</span></span></td>
    <td><span data-ttu-id="dce76-133">Script de T-SQL que se va a usar para la ejecución transversal en las bases de datos</span><span class="sxs-lookup"><span data-stu-id="dce76-133">Transact-SQL script to be used for execution across databases.</span></span>  <span data-ttu-id="dce76-134">El script tiene que crearse para que sea idempotente, puesto que el servicio volverá a intentar la ejecución del script tras errores.</span><span class="sxs-lookup"><span data-stu-id="dce76-134">The script should be authored to be idempotent since the service will retry execution of the script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="dce76-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="dce76-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="dce76-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="dce76-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="dce76-137">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="dce76-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="dce76-138">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="dce76-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="dce76-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="dce76-139">DACPAC</span></span></td>
    <td><span data-ttu-id="dce76-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Paquete de aplicación de capa de datos </a> que se va a aplicar transversalmente a las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="dce76-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package to be applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="dce76-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="dce76-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="dce76-142">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="dce76-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="dce76-143">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="dce76-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="dce76-144">Destino de la base de datos</span><span class="sxs-lookup"><span data-stu-id="dce76-144">Database Target</span></span></td>
    <td><span data-ttu-id="dce76-145">Nombre del servidor y la base de datos que apuntan a una Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="dce76-145">Database and server name pointing to an Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="dce76-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="dce76-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="dce76-147">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="dce76-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="dce76-148">Destino de mapa de particiones</span><span class="sxs-lookup"><span data-stu-id="dce76-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="dce76-149">Combinación de un destino de base de datos y una credencial que se usará para determinar la información almacenada en un mapa de particiones de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="dce76-149">Combination of a database target and a credential to be used to determine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="dce76-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="dce76-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="dce76-151">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="dce76-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="dce76-152">Set-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="dce76-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="dce76-153">Destino de colección personalizada</span><span class="sxs-lookup"><span data-stu-id="dce76-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="dce76-154">Grupo de bases de datos que se define para usar colectivamente en la ejecución.</span><span class="sxs-lookup"><span data-stu-id="dce76-154">Defined group of databases to collectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="dce76-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="dce76-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="dce76-156">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="dce76-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="dce76-157">Destino secundario de colección personalizada</span><span class="sxs-lookup"><span data-stu-id="dce76-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="dce76-158">Destino de base de datos al que se hace referencia en una colección personalizada.</span><span class="sxs-lookup"><span data-stu-id="dce76-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="dce76-159">Add-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="dce76-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="dce76-160">Remove-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="dce76-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="dce76-161">Trabajo</span><span class="sxs-lookup"><span data-stu-id="dce76-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="dce76-162">Definición de parámetros para un trabajo que puede usarse para desencadenar la ejecución o para cumplir una programación.</span><span class="sxs-lookup"><span data-stu-id="dce76-162">Definition of parameters for a job that can be used to trigger execution or to fulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="dce76-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="dce76-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="dce76-164">New-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="dce76-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="dce76-165">Set-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="dce76-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="dce76-166">Ejecución de trabajos</span><span class="sxs-lookup"><span data-stu-id="dce76-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="dce76-167">Contenedor de las tareas necesarias para cumplir la ejecución de un script o para aplicar un DACPAC a un destino con las credenciales para las conexiones de base de datos, donde los errores se controlan según una directiva de ejecución.</span><span class="sxs-lookup"><span data-stu-id="dce76-167">Container of tasks necessary to fulfill either executing a script or applying a DACPAC to a target using credentials for database connections with failures handled in accordance to an execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="dce76-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="dce76-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="dce76-169">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="dce76-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="dce76-170">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="dce76-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="dce76-171">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="dce76-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="dce76-172">Ejecución de tareas de trabajo</span><span class="sxs-lookup"><span data-stu-id="dce76-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="dce76-173">Unidad funcional para completar un trabajo.</span><span class="sxs-lookup"><span data-stu-id="dce76-173">Single unit of work to fulfill a job.</span></span></p>
    <p><span data-ttu-id="dce76-174">Si una tarea de trabajo no se puede ejecutar correctamente, se registrará el mensaje de excepción resultante y se creará una nueva tarea de trabajo coincidente que se ejecutará según la directiva de ejecución especificada.</span><span class="sxs-lookup"><span data-stu-id="dce76-174">If a job task is not able to successfully execute, the resulting exception message will be logged and a new matching job task will be created and executed in accordance to the specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="dce76-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="dce76-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="dce76-176">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="dce76-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="dce76-177">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="dce76-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="dce76-178">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="dce76-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="dce76-179">Directiva de ejecución de trabajos</span><span class="sxs-lookup"><span data-stu-id="dce76-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="dce76-180">Controla los tiempos de espera, los límites de reintentos y los intervalos entre reintentos de la ejecución de trabajos.</span><span class="sxs-lookup"><span data-stu-id="dce76-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="dce76-181">Trabajos de base de datos elástica incluye una directiva de ejecución de trabajos predeterminada que, básicamente, producirá un número infinito de reintentos de errores de tareas de trabajo con retroceso exponencial de intervalos entre reintentos.</span><span class="sxs-lookup"><span data-stu-id="dce76-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="dce76-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="dce76-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="dce76-183">New-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="dce76-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="dce76-184">Set-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="dce76-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="dce76-185">Schedule</span><span class="sxs-lookup"><span data-stu-id="dce76-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="dce76-186">Especificación de tareas de duración definida para que la ejecución se produzca en un intervalo recurrente o en un momento dado.</span><span class="sxs-lookup"><span data-stu-id="dce76-186">Time based specification for execution to take place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="dce76-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="dce76-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="dce76-188">New-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="dce76-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="dce76-189">Set-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="dce76-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="dce76-190">Desencadenadores de trabajo</span><span class="sxs-lookup"><span data-stu-id="dce76-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="dce76-191">Asignación entre un trabajo y una programación que desencadena la ejecución del trabajo según la programación.</span><span class="sxs-lookup"><span data-stu-id="dce76-191">A mapping between a job and a schedule to trigger job execution according to the schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="dce76-192">New-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="dce76-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="dce76-193">Remove-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="dce76-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="dce76-194">Tipos de grupo de trabajos de base de datos elástica admitidos</span><span class="sxs-lookup"><span data-stu-id="dce76-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="dce76-195">El trabajo ejecuta scripts de Transact-SQL (T-SQL) o la aplicación de archivos DACPAC en un grupo de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="dce76-195">The job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="dce76-196">Cuando se envía un trabajo para que se ejecute en un grupo de bases de datos, Trabajos de base de datos elástica se “expande” en trabajos secundarios, y cada uno realiza la ejecución solicitada en una sola base de datos del grupo.</span><span class="sxs-lookup"><span data-stu-id="dce76-196">When a job is submitted to be executed across a group of databases, the job “expands” the into child jobs where each performs the requested execution against a single database in the group.</span></span> 

<span data-ttu-id="dce76-197">Hay dos tipos de grupos que puede crear:</span><span class="sxs-lookup"><span data-stu-id="dce76-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="dce76-198">[Mapa de particiones](sql-database-elastic-scale-shard-map-management.md) : cuando se envía un trabajo con destino a un mapa de particiones, el trabajo consulta primero el mapa de particiones para determinar su conjunto actual de particiones y luego crea trabajos secundarios para cada partición del mapa de particiones.</span><span class="sxs-lookup"><span data-stu-id="dce76-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted to target a shard map, the job queries the shard map to determine its current set of shards, and then creates child jobs for each shard in the shard map.</span></span>
* <span data-ttu-id="dce76-199">Grupo Colección personalizada: conjunto personalizado de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="dce76-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="dce76-200">Cuando un trabajo está destinado a una colección personalizada, crea trabajos secundarios para cada base de datos de la colección personalizada.</span><span class="sxs-lookup"><span data-stu-id="dce76-200">When a job targets a custom collection, it creates child jobs for each database currently in the custom collection.</span></span>

## <a name="to-set-the-elastic-database-jobs-connection"></a><span data-ttu-id="dce76-201">Para establecer la conexión de Trabajos de base de datos elástica</span><span class="sxs-lookup"><span data-stu-id="dce76-201">To set the Elastic Database jobs connection</span></span>
<span data-ttu-id="dce76-202">Se debe establecer una conexión con la *base de datos de control* de trabajos antes de usar las API de trabajos.</span><span class="sxs-lookup"><span data-stu-id="dce76-202">A connection needs to be set to the jobs *control database* prior to using the jobs APIs.</span></span> <span data-ttu-id="dce76-203">Al ejecutar este cmdlet se desencadena una ventana de credenciales emergente que solicita el nombre de usuario y la contraseña creados al instalar Trabajos de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="dce76-203">Running this cmdlet triggers a credential window to pop up requesting the user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="dce76-204">En todos los ejemplos que se ofrecen en este tema se da por hecho que este primer paso ya se realizó.</span><span class="sxs-lookup"><span data-stu-id="dce76-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="dce76-205">Apertura de una conexión a Trabajos de base de datos elástica:</span><span class="sxs-lookup"><span data-stu-id="dce76-205">Open a connection to the Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-the-elastic-database-jobs"></a><span data-ttu-id="dce76-206">Credenciales cifradas en el servicio Trabajos de base de datos elástica</span><span class="sxs-lookup"><span data-stu-id="dce76-206">Encrypted credentials within the Elastic Database jobs</span></span>
<span data-ttu-id="dce76-207">Las credenciales de la base de datos se pueden insertar en la *base de datos de control* de trabajos con su contraseña cifrada.</span><span class="sxs-lookup"><span data-stu-id="dce76-207">Database credentials can be inserted into the jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="dce76-208">Es preciso almacenar las credenciales para que los trabajos se puedan ejecutar después (mediante programaciones de trabajos).</span><span class="sxs-lookup"><span data-stu-id="dce76-208">It is necessary to store credentials to enable jobs to be executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="dce76-209">El cifrado funciona a través de un certificado creado como parte del script de instalación.</span><span class="sxs-lookup"><span data-stu-id="dce76-209">Encryption works through a certificate created as part of the installation script.</span></span> <span data-ttu-id="dce76-210">El script de instalación crea y carga el certificado en el servicio en la nube de Azure para descifrar las contraseñas almacenadas que están cifradas.</span><span class="sxs-lookup"><span data-stu-id="dce76-210">The installation script creates and uploads the certificate into the Azure Cloud Service for decryption of the stored encrypted passwords.</span></span> <span data-ttu-id="dce76-211">Más adelante, el servicio en la nube de Azure almacena la clave pública en la *base de datos de control* de trabajos, lo que permite que la API de PowerShell o la interfaz del Portal de Azure clásico cifren una contraseña proporcionada sin que el certificado tenga que estar instalado localmente.</span><span class="sxs-lookup"><span data-stu-id="dce76-211">The Azure Cloud Service later stores the public key within the jobs *control database* which enables the PowerShell API or Azure Classic Portal interface to encrypt a provided password without requiring the certificate to be locally installed.</span></span>

<span data-ttu-id="dce76-212">Las contraseñas de credenciales se cifran y se protegen de los usuarios mediante el acceso de solo lectura a los objetos de Trabajos de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="dce76-212">The credential passwords are encrypted and secure from users with read-only access to Elastic Database jobs objects.</span></span> <span data-ttu-id="dce76-213">Pero es posible que usuarios malintencionados con acceso de lectura y escritura a los objetos de Trabajos de base de datos elástica extraigan una contraseña.</span><span class="sxs-lookup"><span data-stu-id="dce76-213">But it is possible for a malicious user with read-write access to Elastic Database Jobs objects to extract a password.</span></span> <span data-ttu-id="dce76-214">Las credenciales están diseñadas para su reutilización entre ejecuciones de trabajos.</span><span class="sxs-lookup"><span data-stu-id="dce76-214">Credentials are designed to be reused across job executions.</span></span> <span data-ttu-id="dce76-215">Las credenciales se pasan a las bases de datos de destino al establecer conexiones.</span><span class="sxs-lookup"><span data-stu-id="dce76-215">Credentials are passed to target databases when establishing connections.</span></span> <span data-ttu-id="dce76-216">Como actualmente no hay ninguna restricción en las bases de datos de destino que se usan por cada credencial, un usuario malintencionado podría agregar como destino una base de datos que esté bajo el control del usuario malintencionado.</span><span class="sxs-lookup"><span data-stu-id="dce76-216">There are currently no restrictions on the target databases used for each credential, malicious user could add a database target for a database under the malicious user's control.</span></span> <span data-ttu-id="dce76-217">Posteriormente, el usuario podría iniciar un trabajo destinado a esta base de datos para obtener la contraseña de la credencial.</span><span class="sxs-lookup"><span data-stu-id="dce76-217">The user could subsequently start a job targeting this database to gain the credential's password.</span></span>

<span data-ttu-id="dce76-218">Los procedimientos recomendados de seguridad para Trabajos de base de datos elástica son:</span><span class="sxs-lookup"><span data-stu-id="dce76-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="dce76-219">Limitar el uso de las API a las personas de confianza.</span><span class="sxs-lookup"><span data-stu-id="dce76-219">Limit usage of the APIs to trusted individuals.</span></span>
* <span data-ttu-id="dce76-220">Las credenciales deben tener los privilegios mínimos necesarios para realizar la tarea de trabajo.</span><span class="sxs-lookup"><span data-stu-id="dce76-220">Credentials should have the least privileges necessary to perform the job task.</span></span>  <span data-ttu-id="dce76-221">Puede ver más información en este artículo de MSDN sobre SQL Server, [Autorización y permisos](https://msdn.microsoft.com/library/bb669084.aspx) .</span><span class="sxs-lookup"><span data-stu-id="dce76-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="to-create-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="dce76-222">Para crear una credencial cifrada para la ejecución de trabajos en bases de datos</span><span class="sxs-lookup"><span data-stu-id="dce76-222">To create an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="dce76-223">Para crear una nueva credencial cifrada, el cmdlet [**Get-Credential**](https://technet.microsoft.com/library/hh849815.aspx) pedirá un nombre de usuario y una contraseña que pueda pasarse al cmdlet [**New-AzureSqlJobCredential**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span><span class="sxs-lookup"><span data-stu-id="dce76-223">To create a new encrypted credential, the [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed to the [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="to-update-credentials"></a><span data-ttu-id="dce76-224">Para actualizar las credenciales</span><span class="sxs-lookup"><span data-stu-id="dce76-224">To update credentials</span></span>
<span data-ttu-id="dce76-225">Cuando las contraseñas cambian, use el [**cmdlet Set-AzureSqlJobCredential**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) y establezca el parámetro **CredentialName**.</span><span class="sxs-lookup"><span data-stu-id="dce76-225">When passwords change, use the [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) and set the **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="to-define-an-elastic-database-shard-map-target"></a><span data-ttu-id="dce76-226">Para definir un mapa de particiones de base de datos elástica de destino</span><span class="sxs-lookup"><span data-stu-id="dce76-226">To define an Elastic Database shard map target</span></span>
<span data-ttu-id="dce76-227">Para ejecutar un trabajo en todas las bases de datos de un conjunto de particiones (creado con la [biblioteca cliente de Base de datos elástica](sql-database-elastic-database-client-library.md)), use un mapa de particiones como base de datos de destino.</span><span class="sxs-lookup"><span data-stu-id="dce76-227">To execute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as the database target.</span></span> <span data-ttu-id="dce76-228">Este ejemplo requiere crear una aplicación con particiones con la biblioteca cliente de Base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="dce76-228">This example requires a sharded application created using the Elastic Database client library.</span></span> <span data-ttu-id="dce76-229">Consulte [Introducción a las herramientas de Base de datos elástica](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dce76-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="dce76-230">Se debe establecer la base de datos de administrador del mapa de particiones como base de datos de destino y luego especificar ese mapa de particiones como destino.</span><span class="sxs-lookup"><span data-stu-id="dce76-230">The shard map manager database must be set as a database target and then the specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="dce76-231">Crear un script T-SQL para su ejecución transversal en las bases de datos</span><span class="sxs-lookup"><span data-stu-id="dce76-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="dce76-232">Al crear scripts de T-SQL para su ejecución, es muy recomendable hacerlo de forma que sean [idempotentes](https://en.wikipedia.org/wiki/Idempotence) y resistentes a los errores.</span><span class="sxs-lookup"><span data-stu-id="dce76-232">When creating T-SQL scripts for execution, it is highly recommended to build them to be [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="dce76-233">Trabajos de base de datos elástica volverá a intentar la ejecución de un script cada vez que la ejecución encuentra un error, independientemente de la clasificación del error.</span><span class="sxs-lookup"><span data-stu-id="dce76-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of the classification of the failure.</span></span>

<span data-ttu-id="dce76-234">Use el [**cmdlet New-AzureSqlJobContent**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) para crear y guardar un script de ejecución y establezca los parámetros **-ContentName** y **-CommandText**.</span><span class="sxs-lookup"><span data-stu-id="dce76-234">Use the [**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) to create and save a script for execution and set the **-ContentName** and **-CommandText** parameters.</span></span>

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

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="dce76-235">Creación de un script desde un archivo</span><span class="sxs-lookup"><span data-stu-id="dce76-235">Create a new script from a file</span></span>
<span data-ttu-id="dce76-236">Si el script de T-SQL se define dentro de un archivo, use esto para importar el script:</span><span class="sxs-lookup"><span data-stu-id="dce76-236">If the T-SQL script is defined within a file, use this to import the script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path to SQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="to-update-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="dce76-237">Para actualizar un script de T-SQL para su ejecución en distintas bases de datos</span><span class="sxs-lookup"><span data-stu-id="dce76-237">To update a T-SQL script for execution across databases</span></span>
<span data-ttu-id="dce76-238">El siguiente script de PowerShell actualiza el texto de los comandos T-SQL en un script existente.</span><span class="sxs-lookup"><span data-stu-id="dce76-238">This PowerShell script updates the T-SQL command text for an existing script.</span></span>

<span data-ttu-id="dce76-239">Establecimiento de las siguientes variables para que reflejen la definición que se quiera del script que se va a establecer:</span><span class="sxs-lookup"><span data-stu-id="dce76-239">Set the following variables to reflect the desired script definition to be set:</span></span>

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column to TestTable"
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

### <a name="to-update-the-definition-to-an-existing-script"></a><span data-ttu-id="dce76-240">Para actualizar la definición de un script existente</span><span class="sxs-lookup"><span data-stu-id="dce76-240">To update the definition to an existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="to-create-a-job-to-execute-a-script-across-a-shard-map"></a><span data-ttu-id="dce76-241">Para crear un trabajo que ejecute un script en un mapa de particiones</span><span class="sxs-lookup"><span data-stu-id="dce76-241">To create a job to execute a script across a shard map</span></span>
<span data-ttu-id="dce76-242">El siguiente script de PowerShell inicia un trabajo para la ejecución de un script en cada partición de un mapa de particiones de escala elástica.</span><span class="sxs-lookup"><span data-stu-id="dce76-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="dce76-243">Establecimiento de las siguientes variables para que reflejen el script y el destino que se quiera:</span><span class="sxs-lookup"><span data-stu-id="dce76-243">Set the following variables to reflect the desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="to-execute-a-job"></a><span data-ttu-id="dce76-244">Para ejecutar un trabajo</span><span class="sxs-lookup"><span data-stu-id="dce76-244">To execute a job</span></span>
<span data-ttu-id="dce76-245">Este script de PowerShell ejecuta un trabajo existente:</span><span class="sxs-lookup"><span data-stu-id="dce76-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="dce76-246">Actualice la variable siguiente para que refleje el nombre del trabajo que se quiera ejecutar:</span><span class="sxs-lookup"><span data-stu-id="dce76-246">Update the following variable to reflect the desired job name to have executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="to-retrieve-the-state-of-a-single-job-execution"></a><span data-ttu-id="dce76-247">Para recuperar el estado de ejecución de un único trabajo</span><span class="sxs-lookup"><span data-stu-id="dce76-247">To retrieve the state of a single job execution</span></span>
<span data-ttu-id="dce76-248">Use el cmdlet [**Get-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) y establezca el parámetro **JobExecutionId** para ver el estado de una ejecución de trabajos.</span><span class="sxs-lookup"><span data-stu-id="dce76-248">Use the [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) and set the **JobExecutionId** parameter to view the state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="dce76-249">Use el mismo cmdlet **Get-AzureSqlJobExecution** con el parámetro **IncludeChildren** para ver el estado de ejecuciones de trabajos secundarios, es decir, el estado específico de cada ejecución en cada base de datos destino del trabajo.</span><span class="sxs-lookup"><span data-stu-id="dce76-249">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="to-view-the-state-across-multiple-job-executions"></a><span data-ttu-id="dce76-250">Para ver el estado de varias ejecuciones de trabajos</span><span class="sxs-lookup"><span data-stu-id="dce76-250">To view the state across multiple job executions</span></span>
<span data-ttu-id="dce76-251">El [**cmdlet Get-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/new-azuresqljob) tiene varios parámetros opcionales que sirven para mostrar varias ejecuciones del trabajo, filtradas por los parámetros indicados.</span><span class="sxs-lookup"><span data-stu-id="dce76-251">The [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span></span> <span data-ttu-id="dce76-252">Aquí mostramos algunas de las posibles formas de usar Get-AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="dce76-252">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="dce76-253">Recuperar todas las ejecuciones de trabajos activos de nivel superior:</span><span class="sxs-lookup"><span data-stu-id="dce76-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="dce76-254">Recuperar todas las ejecuciones de trabajos de nivel superior, incluidas las ejecuciones de trabajos inactivos:</span><span class="sxs-lookup"><span data-stu-id="dce76-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="dce76-255">Recuperar todas las ejecuciones de trabajos secundarios de un identificador de ejecución de trabajos proporcionado, incluidas las ejecuciones de trabajos inactivos:</span><span class="sxs-lookup"><span data-stu-id="dce76-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="dce76-256">Recuperar todas las ejecuciones de trabajos creadas con una combinación de programación y trabajo, incluidos los trabajos inactivos:</span><span class="sxs-lookup"><span data-stu-id="dce76-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="dce76-257">Recuperar todos los trabajos que se destinan a un mapa de particiones especificado, incluidos los trabajos inactivos:</span><span class="sxs-lookup"><span data-stu-id="dce76-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="dce76-258">Recuperar todos los trabajos que se destinan a una colección personalizada especificada, incluidos los trabajos inactivos:</span><span class="sxs-lookup"><span data-stu-id="dce76-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="dce76-259">Recuperar la lista de ejecuciones de tareas de trabajos dentro de la ejecución de un trabajo específico:</span><span class="sxs-lookup"><span data-stu-id="dce76-259">Retrieve the list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="dce76-260">Recuperar los detalles de ejecución de tareas de trabajo:</span><span class="sxs-lookup"><span data-stu-id="dce76-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="dce76-261">Puede usar este script de PowerShell para ver los detalles de una ejecución de tareas de trabajo, lo que resulta especialmente útil al depurar errores de ejecución.</span><span class="sxs-lookup"><span data-stu-id="dce76-261">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="to-retrieve-failures-within-job-task-executions"></a><span data-ttu-id="dce76-262">Para recuperar errores dentro de las ejecuciones de tareas de trabajo</span><span class="sxs-lookup"><span data-stu-id="dce76-262">To retrieve failures within job task executions</span></span>
<span data-ttu-id="dce76-263">El objeto **JobTaskExecution** incluye una propiedad para el ciclo de vida de la tarea y una propiedad de mensaje.</span><span class="sxs-lookup"><span data-stu-id="dce76-263">The **JobTaskExecution object** includes a property for the lifecycle of the task along with a message property.</span></span> <span data-ttu-id="dce76-264">Si no se realiza correctamente la ejecución de tareas de un trabajo, la propiedad de ciclo de vida se establecerá en *Failed* y la propiedad de mensaje se establecerá en el mensaje de excepción resultante y la pila.</span><span class="sxs-lookup"><span data-stu-id="dce76-264">If a job task execution failed, the lifecycle property will be set to *Failed* and the message property will be set to the resulting exception message and its stack.</span></span> <span data-ttu-id="dce76-265">Si un trabajo no se realiza correctamente, es importante ver los detalles de las tareas de trabajo que no se realizaron correctamente en un trabajo determinado.</span><span class="sxs-lookup"><span data-stu-id="dce76-265">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="to-wait-for-a-job-execution-to-complete"></a><span data-ttu-id="dce76-266">Para esperar a que se complete la ejecución de un trabajo</span><span class="sxs-lookup"><span data-stu-id="dce76-266">To wait for a job execution to complete</span></span>
<span data-ttu-id="dce76-267">Este script de PowerShell sirve para esperar a que una tarea de trabajo se complete:</span><span class="sxs-lookup"><span data-stu-id="dce76-267">The following PowerShell script can be used to wait for a job task to complete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="dce76-268">Crear una directiva de ejecución personalizada</span><span class="sxs-lookup"><span data-stu-id="dce76-268">Create a custom execution policy</span></span>
<span data-ttu-id="dce76-269">Trabajos de base de datos elástica admite la creación de directivas de ejecución personalizadas que se pueden aplicar al iniciar trabajos.</span><span class="sxs-lookup"><span data-stu-id="dce76-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="dce76-270">Actualmente, las directivas de ejecución permiten definir:</span><span class="sxs-lookup"><span data-stu-id="dce76-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="dce76-271">Nombre: identificador de la directiva de ejecución.</span><span class="sxs-lookup"><span data-stu-id="dce76-271">Name: Identifier for the execution policy.</span></span>
* <span data-ttu-id="dce76-272">Tiempo de espera del trabajo: tiempo total antes de que Trabajos de base de datos elástica cancele un trabajo.</span><span class="sxs-lookup"><span data-stu-id="dce76-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="dce76-273">Intervalo de reintento inicial: intervalo de espera antes del primer reintento.</span><span class="sxs-lookup"><span data-stu-id="dce76-273">Initial Retry Interval: Interval to wait before first retry.</span></span>
* <span data-ttu-id="dce76-274">Intervalo máximo de reintento: límite de intervalos de reintento que se usan.</span><span class="sxs-lookup"><span data-stu-id="dce76-274">Maximum Retry Interval: Cap of retry intervals to use.</span></span>
* <span data-ttu-id="dce76-275">Coeficiente de retroceso de intervalo de reintento: coeficiente que se usa para calcular el siguiente intervalo entre reintentos.</span><span class="sxs-lookup"><span data-stu-id="dce76-275">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span></span>  <span data-ttu-id="dce76-276">Se usa la siguiente fórmula: (intervalo de reintento inicial) * Math.pow ((coeficiente de retroceso de intervalo), (número de intentos de) - 2).</span><span class="sxs-lookup"><span data-stu-id="dce76-276">The following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="dce76-277">Número máximo de intentos: número máximo de reintentos para llevar a cabo un trabajo.</span><span class="sxs-lookup"><span data-stu-id="dce76-277">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span></span>

<span data-ttu-id="dce76-278">La directiva de ejecución predeterminada usa los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="dce76-278">The default execution policy uses the following values:</span></span>

* <span data-ttu-id="dce76-279">Nombre: directiva de ejecución predeterminada</span><span class="sxs-lookup"><span data-stu-id="dce76-279">Name: Default execution policy</span></span>
* <span data-ttu-id="dce76-280">Tiempo de espera del trabajo: 1 semana</span><span class="sxs-lookup"><span data-stu-id="dce76-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="dce76-281">Intervalo de reintento inicial: 100 milisegundos</span><span class="sxs-lookup"><span data-stu-id="dce76-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="dce76-282">Intervalo máximo de reintento: 30 minutos</span><span class="sxs-lookup"><span data-stu-id="dce76-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="dce76-283">Coeficiente de intervalo de reintento: 2</span><span class="sxs-lookup"><span data-stu-id="dce76-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="dce76-284">Número máximo de intentos: 2.147.483.647</span><span class="sxs-lookup"><span data-stu-id="dce76-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="dce76-285">Crear la directiva de ejecución que quiera:</span><span class="sxs-lookup"><span data-stu-id="dce76-285">Create the desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="dce76-286">Actualización de una directiva de ejecución personalizada</span><span class="sxs-lookup"><span data-stu-id="dce76-286">Update a custom execution policy</span></span>
<span data-ttu-id="dce76-287">Actualizar la directiva de ejecución que se quiere actualizar:</span><span class="sxs-lookup"><span data-stu-id="dce76-287">Update the desired execution policy to update:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="dce76-288">Cancelación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="dce76-288">Cancel a job</span></span>
<span data-ttu-id="dce76-289">Trabajos de base de datos elástica admite solicitudes de cancelación de trabajos.</span><span class="sxs-lookup"><span data-stu-id="dce76-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="dce76-290">Si Trabajos de base de datos elástica detecta una solicitud de cancelación para un trabajo que está ejecutándose en ese momento, intentará detener el trabajo.</span><span class="sxs-lookup"><span data-stu-id="dce76-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span></span>

<span data-ttu-id="dce76-291">Trabajos de base de datos elástica puede realizar una cancelación de dos formas distintas:</span><span class="sxs-lookup"><span data-stu-id="dce76-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="dce76-292">Cancelar las tareas actualmente en ejecución: si se detecta una cancelación mientras se ejecuta una tarea, se intentará cancelar el aspecto de la tarea que se está ejecutando actualmente.</span><span class="sxs-lookup"><span data-stu-id="dce76-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span></span>  <span data-ttu-id="dce76-293">Por ejemplo: si hay una consulta de larga ejecución en curso en el momento en que se intenta realizar una cancelación, se intentará cancelar la consulta.</span><span class="sxs-lookup"><span data-stu-id="dce76-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span></span>
2. <span data-ttu-id="dce76-294">Cancelación de reintentos de tareas: si el subproceso de control detecta una cancelación antes de iniciar una tarea para su ejecución, evitará iniciar la tarea y declarará cancelada la solicitud.</span><span class="sxs-lookup"><span data-stu-id="dce76-294">Canceling task retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span></span>

<span data-ttu-id="dce76-295">Si se solicita una cancelación de trabajo para un trabajo primario, se respetará la solicitud de cancelación para el trabajo primario y todos los trabajos secundarios.</span><span class="sxs-lookup"><span data-stu-id="dce76-295">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span></span>

<span data-ttu-id="dce76-296">Para enviar una solicitud de cancelación, use el [**cmdlet Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) y establezca el parámetro **JobExecutionId**.</span><span class="sxs-lookup"><span data-stu-id="dce76-296">To submit a cancellation request, use the [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) and set the **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="to-delete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="dce76-297">Para eliminar un trabajo y el historial de trabajos de forma asincrónica</span><span class="sxs-lookup"><span data-stu-id="dce76-297">To delete a job and job history asynchronously</span></span>
<span data-ttu-id="dce76-298">Trabajos de base de datos elástica admite la eliminación asincrónica de trabajos.</span><span class="sxs-lookup"><span data-stu-id="dce76-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="dce76-299">Un trabajo se puede marcar para su eliminación y el sistema eliminará el trabajo y su historial de trabajos una vez completadas todas las ejecuciones de trabajos para ese trabajo.</span><span class="sxs-lookup"><span data-stu-id="dce76-299">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span></span> <span data-ttu-id="dce76-300">El sistema no cancelará automáticamente las ejecuciones de trabajos activos.</span><span class="sxs-lookup"><span data-stu-id="dce76-300">The system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="dce76-301">Invoque a [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) para cancelar las ejecuciones de trabajos activas.</span><span class="sxs-lookup"><span data-stu-id="dce76-301">Invoke [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) to cancel active job executions.</span></span>

<span data-ttu-id="dce76-302">Para desencadenar la eliminación del trabajo, use el [**cmdlet Remove-AzureSqlJob**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) y establezca el parámetro **JobName**.</span><span class="sxs-lookup"><span data-stu-id="dce76-302">To trigger job deletion, use the [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) and set the **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="to-create-a-custom-database-target"></a><span data-ttu-id="dce76-303">Para crear una base de datos de destino personalizada</span><span class="sxs-lookup"><span data-stu-id="dce76-303">To create a custom database target</span></span>
<span data-ttu-id="dce76-304">Puede definir bases de datos de destino personalizadas para la ejecución directa o para su inclusión en un grupo personalizado de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="dce76-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="dce76-305">Por ejemplo, como los **grupos elásticos** todavía no se admiten directamente mediante las API de PowerShell, puede crear una base de datos personalizada como destino y una colección de bases de datos personalizada como destino que englobe todas las bases de datos del grupo.</span><span class="sxs-lookup"><span data-stu-id="dce76-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all the databases in the pool.</span></span>

<span data-ttu-id="dce76-306">Establecimiento de las siguientes variables para que reflejen la información de base de datos que se quiera:</span><span class="sxs-lookup"><span data-stu-id="dce76-306">Set the following variables to reflect the desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="to-create-a-custom-database-collection-target"></a><span data-ttu-id="dce76-307">Para crear una colección de bases de datos de destino personalizada</span><span class="sxs-lookup"><span data-stu-id="dce76-307">To create a custom database collection target</span></span>
<span data-ttu-id="dce76-308">Use el cmdlet [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) para definir una colección de bases de datos personalizada de destino para permitir la ejecución en varias bases de datos definidas como destino.</span><span class="sxs-lookup"><span data-stu-id="dce76-308">Use the [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet to define a custom database collection target to enable execution across multiple defined database targets.</span></span> <span data-ttu-id="dce76-309">Después de crear un grupo de bases de datos, las bases de datos se pueden asociar con la colección personalizada de destino.</span><span class="sxs-lookup"><span data-stu-id="dce76-309">After creating a database group, databases can be associated with the custom collection target.</span></span>

<span data-ttu-id="dce76-310">Establecimiento de las siguientes variables para que reflejen la configuración de destino de la colección personalizada que se quiera:</span><span class="sxs-lookup"><span data-stu-id="dce76-310">Set the following variables to reflect the desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="to-add-databases-to-a-custom-database-collection-target"></a><span data-ttu-id="dce76-311">Para agregar bases de datos a una colección de bases de datos personalizada de destino</span><span class="sxs-lookup"><span data-stu-id="dce76-311">To add databases to a custom database collection target</span></span>
<span data-ttu-id="dce76-312">Para agregar una base de datos a una colección personalizada específica, use el cmdlet [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget).</span><span class="sxs-lookup"><span data-stu-id="dce76-312">To add a database to a specific custom collection use the [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-the-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="dce76-313">Revisión de las bases de datos incluidas en un destino de colección de bases de datos personalizada</span><span class="sxs-lookup"><span data-stu-id="dce76-313">Review the databases within a custom database collection target</span></span>
<span data-ttu-id="dce76-314">Use el cmdlet [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) para recuperar las bases de datos secundarias en un destino de la colección de bases de datos personalizada.</span><span class="sxs-lookup"><span data-stu-id="dce76-314">Use the [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet to retrieve the child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-to-execute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="dce76-315">Creación de un trabajo para ejecutar un script transversalmente en un destino de colección de bases de datos personalizada</span><span class="sxs-lookup"><span data-stu-id="dce76-315">Create a job to execute a script across a custom database collection target</span></span>
<span data-ttu-id="dce76-316">Use el cmdlet [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) para crear un trabajo en un grupo de bases de datos definido por un destino de la colección de base de datos personalizada.</span><span class="sxs-lookup"><span data-stu-id="dce76-316">Use the [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet to create a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="dce76-317">Trabajos de base de datos elástica expande el trabajo en varios trabajos secundarios, cada uno correspondiente a una base de datos asociada al destino de la colección de bases de datos personalizada y garantiza que el script se ejecuta en cada una de las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="dce76-317">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span></span> <span data-ttu-id="dce76-318">De nuevo, es importante que los scripts sean idempotentes para que sean resistentes a los reintentos.</span><span class="sxs-lookup"><span data-stu-id="dce76-318">Again, it is important that scripts are idempotent to be resilient to retries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="dce76-319">Recopilación de datos de una base de datos a otra</span><span class="sxs-lookup"><span data-stu-id="dce76-319">Data collection across databases</span></span>
<span data-ttu-id="dce76-320">Puede usar un trabajo para ejecutar una consulta en un grupo de bases de datos y enviar los resultados a una tabla específica.</span><span class="sxs-lookup"><span data-stu-id="dce76-320">You can use a job to execute a query across a group of databases and send the results to a specific table.</span></span> <span data-ttu-id="dce76-321">La tabla se puede consultar a posteriori para ver los resultados de la consulta de cada base de datos.</span><span class="sxs-lookup"><span data-stu-id="dce76-321">The table can be queried after the fact to see the query’s results from each database.</span></span> <span data-ttu-id="dce76-322">Esto ofrece un mecanismo asincrónico para ejecutar una consulta en numerosas bases de datos.</span><span class="sxs-lookup"><span data-stu-id="dce76-322">This provides an asynchronous method to execute a query across many databases.</span></span> <span data-ttu-id="dce76-323">Los intentos incorrectos se controlan automáticamente mediante reintentos.</span><span class="sxs-lookup"><span data-stu-id="dce76-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="dce76-324">La tabla de destino especificada se creará automáticamente si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="dce76-324">The specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="dce76-325">La nueva tabla coincide con el esquema del conjunto de resultados devuelto.</span><span class="sxs-lookup"><span data-stu-id="dce76-325">The new table matches the schema of the returned result set.</span></span> <span data-ttu-id="dce76-326">Si un script devuelve varios conjuntos de resultados, Trabajos de base de datos elástica solo enviará el primero a la tabla de destino.</span><span class="sxs-lookup"><span data-stu-id="dce76-326">If a script returns multiple result sets, Elastic Database jobs will only send the first to the destination table.</span></span>

<span data-ttu-id="dce76-327">El siguiente script de PowerShell ejecuta un script y recopila los resultados en una tabla especificada.</span><span class="sxs-lookup"><span data-stu-id="dce76-327">The following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="dce76-328">Este script presupone que se creó un script T-SQL que genera un único conjunto de resultados y que se creó una colección de bases de datos personalizada de destino.</span><span class="sxs-lookup"><span data-stu-id="dce76-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="dce76-329">Este script usa el cmdlet [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget).</span><span class="sxs-lookup"><span data-stu-id="dce76-329">This script uses the [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span></span> <span data-ttu-id="dce76-330">Establezca los parámetros del script, las credenciales y el destino de ejecución:</span><span class="sxs-lookup"><span data-stu-id="dce76-330">Set the parameters for script, credentials, and execution target:</span></span>

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

### <a name="to-create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="dce76-331">Para crear e iniciar un trabajo en escenarios de recolección de datos</span><span class="sxs-lookup"><span data-stu-id="dce76-331">To create and start a job for data collection scenarios</span></span>
<span data-ttu-id="dce76-332">Este script usa el cmdlet [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution).</span><span class="sxs-lookup"><span data-stu-id="dce76-332">This script uses the [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span></span>

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

## <a name="to-schedule-a-job-execution-trigger"></a><span data-ttu-id="dce76-333">Para programar un desencadenador de ejecución de trabajos</span><span class="sxs-lookup"><span data-stu-id="dce76-333">To schedule a job execution trigger</span></span>
<span data-ttu-id="dce76-334">El siguiente script de PowerShell se usa para crear una programación periódica.</span><span class="sxs-lookup"><span data-stu-id="dce76-334">The following PowerShell script can be used to create a recurring schedule.</span></span> <span data-ttu-id="dce76-335">Este script usa un intervalo de minutos, pero [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) también admite los parámetros -DayInterval, -HourInterval, -MonthInterval y -WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="dce76-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="dce76-336">Se pueden crear programaciones que se ejecutan una sola vez pasando -OneTime.</span><span class="sxs-lookup"><span data-stu-id="dce76-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="dce76-337">Creación de una programación:</span><span class="sxs-lookup"><span data-stu-id="dce76-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="to-trigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="dce76-338">Para desencadenar un trabajo para que se ejecute a la hora programada</span><span class="sxs-lookup"><span data-stu-id="dce76-338">To trigger a job executed on a time schedule</span></span>
<span data-ttu-id="dce76-339">Se puede definir un desencadenador de trabajo para que un trabajo se ejecute según una programación de tiempo.</span><span class="sxs-lookup"><span data-stu-id="dce76-339">A job trigger can be defined to have a job executed according to a time schedule.</span></span> <span data-ttu-id="dce76-340">El siguiente script de PowerShell sirve para crear un desencadenador de trabajo.</span><span class="sxs-lookup"><span data-stu-id="dce76-340">The following PowerShell script can be used to create a job trigger.</span></span>

<span data-ttu-id="dce76-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) y establezca las siguientes variables para que se correspondan con el trabajo y la programación deseados:</span><span class="sxs-lookup"><span data-stu-id="dce76-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) and set the following variables to correspond to the desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="to-remove-a-scheduled-association-to-stop-job-from-executing-on-schedule"></a><span data-ttu-id="dce76-342">Para quitar una asociación programada y detener la ejecución de un trabajo a la hora programada</span><span class="sxs-lookup"><span data-stu-id="dce76-342">To remove a scheduled association to stop job from executing on schedule</span></span>
<span data-ttu-id="dce76-343">Para suspender la ejecución de un trabajo recurrente a través de un desencadenador de trabajo, se puede quitar el desencadenador de trabajo.</span><span class="sxs-lookup"><span data-stu-id="dce76-343">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span></span> <span data-ttu-id="dce76-344">Quite un desencadenador de trabajo para detener un trabajo que se ejecute según una programación con el [**cmdlet Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span><span class="sxs-lookup"><span data-stu-id="dce76-344">Remove a job trigger to stop a job from being executed according to a schedule using the [**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-to-a-time-schedule"></a><span data-ttu-id="dce76-345">Recuperación de desencadenadores de trabajo enlazados a una programación de tiempo</span><span class="sxs-lookup"><span data-stu-id="dce76-345">Retrieve job triggers bound to a time schedule</span></span>
<span data-ttu-id="dce76-346">El siguiente script de PowerShell sirve para obtener y mostrar los desencadenadores de trabajo registrados para una programación de tiempo determinada.</span><span class="sxs-lookup"><span data-stu-id="dce76-346">The following PowerShell script can be used to obtain and display the job triggers registered to a particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="to-retrieve-job-triggers-bound-to-a-job"></a><span data-ttu-id="dce76-347">Para recuperar los desencadenadores enlazados a un trabajo</span><span class="sxs-lookup"><span data-stu-id="dce76-347">To retrieve job triggers bound to a job</span></span>
<span data-ttu-id="dce76-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) para obtener y mostrar las programaciones que contienen un trabajo registrado.</span><span class="sxs-lookup"><span data-stu-id="dce76-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) to obtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="to-create-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="dce76-349">Para crear una aplicación de capa de datos (DACPAC) para su ejecución en bases de datos</span><span class="sxs-lookup"><span data-stu-id="dce76-349">To create a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="dce76-350">Para crear una DACPAC, consulte [Aplicaciones de capa de datos](https://msdn.microsoft.com/library/ee210546.aspx).</span><span class="sxs-lookup"><span data-stu-id="dce76-350">To create a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="dce76-351">Para implementar una DACPAC, use el [cmdlet New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span><span class="sxs-lookup"><span data-stu-id="dce76-351">To deploy a DACPAC, use the [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span></span> <span data-ttu-id="dce76-352">La DACPAC debe ser accesible para el servicio.</span><span class="sxs-lookup"><span data-stu-id="dce76-352">The DACPAC must be accessible to the service.</span></span> <span data-ttu-id="dce76-353">Se recomienda cargar una DACPAC creada en Almacenamiento de Azure y crear una [firma de acceso compartido](../storage/common/storage-dotnet-shared-access-signature-part-1.md) para la DACPAC.</span><span class="sxs-lookup"><span data-stu-id="dce76-353">It is recommended to upload a created DACPAC to Azure Storage and create a [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for the DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="to-update-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="dce76-354">Para actualizar una aplicación de capa de datos (DACPAC) para su ejecución en bases de datos</span><span class="sxs-lookup"><span data-stu-id="dce76-354">To update a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="dce76-355">Las DACPAC existentes que se registren en Trabajos de base de datos elástica pueden actualizarse para que señalen a nuevos URI.</span><span class="sxs-lookup"><span data-stu-id="dce76-355">Existing DACPACs registered within Elastic Database Jobs can be updated to point to new URIs.</span></span> <span data-ttu-id="dce76-356">Use el cmdlet [**Set-AzureSqlJobContentDefinition**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) para actualizar el URI de una DACPAC registrada:</span><span class="sxs-lookup"><span data-stu-id="dce76-356">Use the [**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) to update the DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="to-create-a-job-to-apply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="dce76-357">Para crear un trabajo para aplicar una aplicación de capa de datos (DACPAC) en bases de datos</span><span class="sxs-lookup"><span data-stu-id="dce76-357">To create a job to apply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="dce76-358">Una vez creada una DACPAC en Trabajos de base de datos elástica, puede crearse un trabajo que aplique transversalmente la DACPAC en un grupo de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="dce76-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created to apply the DACPAC across a group of databases.</span></span> <span data-ttu-id="dce76-359">El siguiente script de PowerShell sirve para crear un trabajo DACPAC transversalmente en una colección personalizada de bases de datos:</span><span class="sxs-lookup"><span data-stu-id="dce76-359">The following PowerShell script can be used to create a DACPAC job across a custom collection of databases:</span></span>

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
