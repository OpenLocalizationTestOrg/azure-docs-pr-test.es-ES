---
title: "trabajos de base de datos elástica aaaInstalling | Documentos de Microsoft"
description: "Guiará a través de la instalación de función de trabajo elástico Hola."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0349f66a4428f81d00d43681d7f2177f273ec032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="installing-elastic-database-jobs-overview"></a><span data-ttu-id="58ecd-103">Información general sobre la instalación de Trabajos de base de datos elástica</span><span class="sxs-lookup"><span data-stu-id="58ecd-103">Installing Elastic Database jobs overview</span></span>
<span data-ttu-id="58ecd-104">[**Trabajos de base de datos elásticos** ](sql-database-elastic-jobs-overview.md) puede instalarse a través de PowerShell o a través de hello Portal.You clásico de Azure puede obtener acceso a toocreate y administrar los trabajos mediante Hola API de PowerShell solo si instalar paquetes de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="58ecd-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through hello Azure Classic Portal.You can gain access toocreate and manage jobs using hello PowerShell API only if you install hello PowerShell package.</span></span> <span data-ttu-id="58ecd-105">Además, Hola PowerShell APIs proporcionan una funcionalidad significativamente mayor que el portal de hello en este momento.</span><span class="sxs-lookup"><span data-stu-id="58ecd-105">Additionally, hello PowerShell APIs provide significantly more functionality than hello portal at this point in time.</span></span>

<span data-ttu-id="58ecd-106">Si ya ha instalado **trabajos de base de datos elástica** a través de hello Portal desde una existente **grupo elástico**, última versión preliminar Powershell Hola incluye secuencias de comandos tooupgrade la instalación existente.</span><span class="sxs-lookup"><span data-stu-id="58ecd-106">If you have already installed **Elastic Database jobs** through hello Portal from an existing **elastic pool**, hello latest Powershell preview includes scripts tooupgrade your existing installation.</span></span> <span data-ttu-id="58ecd-107">Es altamente recomendado tooupgrade su toohello de instalación más reciente **trabajos de base de datos elástica** componentes en orden tootake aprovechar las nuevas funcionalidades expuestas a través de Hola PowerShell APIs.</span><span class="sxs-lookup"><span data-stu-id="58ecd-107">It is highly recommended tooupgrade your installation toohello latest **Elastic Database jobs** components in order tootake advantage of new functionality exposed via hello PowerShell APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58ecd-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="58ecd-108">Prerequisites</span></span>
* <span data-ttu-id="58ecd-109">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="58ecd-109">An Azure subscription.</span></span> <span data-ttu-id="58ecd-110">Para obtener una versión de evaluación gratuita, consulte [Versión de evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="58ecd-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="58ecd-111">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="58ecd-111">Azure PowerShell.</span></span> <span data-ttu-id="58ecd-112">Instalar la versión más reciente hello mediante hello [instalador de plataforma Web](http://go.microsoft.com/fwlink/p/?linkid=320376).</span><span class="sxs-lookup"><span data-stu-id="58ecd-112">Install hello latest version using hello [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span></span> <span data-ttu-id="58ecd-113">Para obtener información detallada, vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="58ecd-113">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="58ecd-114">[Utilidad de línea de comandos de NuGet](https://nuget.org/nuget.exe) es tooinstall usado Hola bases de datos elásticas trabajos paquete.</span><span class="sxs-lookup"><span data-stu-id="58ecd-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used tooinstall hello Elastic Database jobs package.</span></span> <span data-ttu-id="58ecd-115">Para obtener más información, consulte http://docs.nuget.org/docs/start-here/installing-nuget.</span><span class="sxs-lookup"><span data-stu-id="58ecd-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span></span>

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a><span data-ttu-id="58ecd-116">Descargue e importe el paquete de PowerShell de trabajos de bases de datos elásticas Hola</span><span class="sxs-lookup"><span data-stu-id="58ecd-116">Download and import hello Elastic Database jobs PowerShell package</span></span>
1. <span data-ttu-id="58ecd-117">Inicia la ventana de comandos de PowerShell de Microsoft Azure y ve directorio toohello donde descargó la utilidad de línea de comandos del NuGet (nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="58ecd-117">Launch Microsoft Azure PowerShell command window and navigate toohello directory where you downloaded NuGet Command-line Utility (nuget.exe).</span></span>
2. <span data-ttu-id="58ecd-118">Descargue e importe **trabajos de base de datos elástica** paquete en el directorio actual de hello con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="58ecd-118">Download and import **Elastic Database jobs** package into hello current directory with hello following command:</span></span>
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    <span data-ttu-id="58ecd-119">Hola **trabajos de base de datos elástica** archivos se colocan en el directorio local de hello en una carpeta denominada **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** donde *x.x.xxxx.x* refleja el número de versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="58ecd-119">hello **Elastic Database jobs** files are placed in hello local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects hello version number.</span></span> <span data-ttu-id="58ecd-120">cmdlets de PowerShell de Hello (incluidos los archivos .dll de cliente necesario) se encuentran en hello **tools\ElasticDatabaseJobs** subdirectorio hello tooinstall de secuencias de comandos de PowerShell, actualizar y desinstalar también residen en hello  **herramientas** subdirectorio.</span><span class="sxs-lookup"><span data-stu-id="58ecd-120">hello PowerShell cmdlets (including required client .dlls) are located in hello **tools\ElasticDatabaseJobs** sub-directory and hello PowerShell scripts tooinstall, upgrade and uninstall also reside in hello **tools** sub-directory.</span></span>
3. <span data-ttu-id="58ecd-121">Desplácese subdirectorio herramientas toohello bajo la carpeta de hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x escribiendo cd de herramientas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="58ecd-121">Navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. <span data-ttu-id="58ecd-122">Ejecute el directorio de hello.\InstallElasticDatabaseJobsCmdlets.ps1 scripts toocopy hello ElasticDatabaseJobs en $home\Documents\WindowsPowerShell\Modules.</span><span class="sxs-lookup"><span data-stu-id="58ecd-122">Execute hello .\InstallElasticDatabaseJobsCmdlets.ps1 script toocopy hello ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="58ecd-123">Esto también importará automáticamente módulo Hola para su uso, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="58ecd-123">This will also automatically import hello module for use, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="58ecd-124">Instalar componentes de trabajos de bases de datos elásticas hello mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="58ecd-124">Install hello Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="58ecd-125">Inicia una ventana de comandos de PowerShell de Microsoft Azure y ve toohello \tools subdirectorio bajo la carpeta de Hola Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x: escriba cd \tools</span><span class="sxs-lookup"><span data-stu-id="58ecd-125">Launch a Microsoft Azure PowerShell command window and navigate toohello \tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. <span data-ttu-id="58ecd-126">Ejecutar script de PowerShell de hello.\InstallElasticDatabaseJobs.ps1 y suministrar valores de sus variables solicitados.</span><span class="sxs-lookup"><span data-stu-id="58ecd-126">Execute hello .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span></span> <span data-ttu-id="58ecd-127">Esta secuencia de comandos creará los componentes de hello descritos en [bases de datos elásticas trabajos componentes y precios](sql-database-elastic-jobs-overview.md#components-and-pricing) además de configurar Hola servicio de nube de Azure tooappropriately usan componentes dependientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="58ecd-127">This script will create hello components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring hello Azure Cloud Service tooappropriately use hello dependent components.</span></span>

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

<span data-ttu-id="58ecd-128">Al ejecutar este comando, se abrirá una ventana para especificar el **nombre de usuario** y la **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="58ecd-128">When you run this command a window opens asking for a **user name** and **password**.</span></span> <span data-ttu-id="58ecd-129">No trata sus credenciales de Azure, escriba el nombre de usuario de Hola y la contraseña que se desea toocreate para el nuevo servidor de hello las credenciales de administrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="58ecd-129">This is not your Azure credentials, enter hello user name and password that will be hello administrator credentials you want toocreate for hello new server.</span></span>

<span data-ttu-id="58ecd-130">parámetros de Hello proporcionados en esta invocación de ejemplo pueden modificarse para la configuración deseada.</span><span class="sxs-lookup"><span data-stu-id="58ecd-130">hello parameters provided on this sample invocation can be modified for your desired settings.</span></span> <span data-ttu-id="58ecd-131">siguiente Hola proporciona más información sobre el comportamiento de Hola de cada parámetro:</span><span class="sxs-lookup"><span data-stu-id="58ecd-131">hello following provides more information on hello behavior of each parameter:</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="58ecd-132">Parámetro</span><span class="sxs-lookup"><span data-stu-id="58ecd-132">Parameter</span></span></th>
    <th><span data-ttu-id="58ecd-133">Description</span><span class="sxs-lookup"><span data-stu-id="58ecd-133">Description</span></span></th>
  </tr>

<tr>
    <td><span data-ttu-id="58ecd-134">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="58ecd-134">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="58ecd-135">Proporciona el nombre del grupo de recursos de Azure de hello creado hello toocontain que acaba de crear componentes de Azure.</span><span class="sxs-lookup"><span data-stu-id="58ecd-135">Provides hello Azure resource group name created toocontain hello newly created Azure components.</span></span> <span data-ttu-id="58ecd-136">Este parámetro tiene como valor predeterminado demasiado "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="58ecd-136">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="58ecd-137">No es recomendable toochange este valor.</span><span class="sxs-lookup"><span data-stu-id="58ecd-137">It is not recommended toochange this value.</span></span></td>
    </tr>

</tr>

    <tr>
    <td><span data-ttu-id="58ecd-138">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="58ecd-138">ResourceGroupLocation</span></span></td>
    <td><span data-ttu-id="58ecd-139">Proporciona hello toobe de ubicación de Azure permiten Hola que acaba de crear componentes de Azure.</span><span class="sxs-lookup"><span data-stu-id="58ecd-139">Provides hello Azure location toobe used for hello newly created Azure components.</span></span> <span data-ttu-id="58ecd-140">Este parámetro tiene como valor predeterminado toohello ubicación Central US.</span><span class="sxs-lookup"><span data-stu-id="58ecd-140">This parameter defaults toohello Central US location.</span></span></td>
</tr>

<tr>
    <td><span data-ttu-id="58ecd-141">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="58ecd-141">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="58ecd-142">Proporciona el número de Hola de tooinstall de los trabajadores de servicio.</span><span class="sxs-lookup"><span data-stu-id="58ecd-142">Provides hello number of service workers tooinstall.</span></span> <span data-ttu-id="58ecd-143">Este parámetro tiene como valor predeterminado too1.</span><span class="sxs-lookup"><span data-stu-id="58ecd-143">This parameter defaults too1.</span></span> <span data-ttu-id="58ecd-144">Un número mayor de los trabajadores puede ser usado tooscale out Hola servicio y tooprovide alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="58ecd-144">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span> <span data-ttu-id="58ecd-145">Se recomienda toouse "2" para las implementaciones que necesitan una alta disponibilidad del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="58ecd-145">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
    </tr>

</tr>
    <tr>
    <td><span data-ttu-id="58ecd-146">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="58ecd-146">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="58ecd-147">Proporciona el tamaño VM de hello para el uso dentro de hello servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="58ecd-147">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="58ecd-148">Este parámetro tiene como valor predeterminado tooA0.</span><span class="sxs-lookup"><span data-stu-id="58ecd-148">This parameter defaults tooA0.</span></span> <span data-ttu-id="58ecd-149">Se aceptan valores de parámetros de A0/A1 y A2/A3 que hacer al trabajo de hello rol toouse un tamaño ExtraSmall/pequeño/mediano/grande, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="58ecd-149">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="58ecd-150">Para obtener más información sobre los tamaños de rol de trabajo, consulte [Componentes y precios de trabajos de base de datos elástica](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="58ecd-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="58ecd-151">SqlServerDatabaseSlo</span><span class="sxs-lookup"><span data-stu-id="58ecd-151">SqlServerDatabaseSlo</span></span></td>
    <td><span data-ttu-id="58ecd-152">Proporciona el objetivo de nivel de servicio de Hola para un servidor Standard edition.</span><span class="sxs-lookup"><span data-stu-id="58ecd-152">Provides hello service level objective for a Standard edition.</span></span> <span data-ttu-id="58ecd-153">Este parámetro tiene como valor predeterminado tooS0.</span><span class="sxs-lookup"><span data-stu-id="58ecd-153">This parameter defaults tooS0.</span></span> <span data-ttu-id="58ecd-154">Se aceptan valores de parámetro de S0, S1, S2 y S3 que hacer Hola base de datos de SQL Azure toouse Hola respectivo SLO.</span><span class="sxs-lookup"><span data-stu-id="58ecd-154">Parameter values of S0/S1/S2/S3 are accepted which cause hello Azure SQL Database toouse hello respective SLO.</span></span> <span data-ttu-id="58ecd-155">Para obtener más información sobre SLO de SQL Database, consulte [Componentes y precios de trabajos de base de datos elástica](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="58ecd-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="58ecd-156">SqlServerAdministratorUserName</span><span class="sxs-lookup"><span data-stu-id="58ecd-156">SqlServerAdministratorUserName</span></span></td>
    <td><span data-ttu-id="58ecd-157">Proporciona el nombre de usuario de administrador de Hola para hello que acaba de crear el servidor de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="58ecd-157">Provides hello admin user name for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="58ecd-158">Cuando no se especifica, abrirá a una ventana de credenciales de PowerShell tooprompt credenciales Hola.</span><span class="sxs-lookup"><span data-stu-id="58ecd-158">When not specified, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="58ecd-159">SqlServerAdministratorPassword</span><span class="sxs-lookup"><span data-stu-id="58ecd-159">SqlServerAdministratorPassword</span></span></td>
    <td><span data-ttu-id="58ecd-160">Proporciona la contraseña de administrador de Hola para hello que acaba de crear el servidor de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="58ecd-160">Provides hello admin password for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="58ecd-161">Cuando no se proporciona una ventana de credenciales PowerShell abrirá tooprompt credenciales Hola.</span><span class="sxs-lookup"><span data-stu-id="58ecd-161">When not provided, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>
</table>

<span data-ttu-id="58ecd-162">Para los sistemas que tienen como destino con un número grande de trabajos que se ejecutan en paralelo en un gran número de bases de datos, se recomienda como parámetros de toospecify: ServiceWorkerCount - 2 - ServiceVmSize A2 - SqlServerDatabaseSlo S2.</span><span class="sxs-lookup"><span data-stu-id="58ecd-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended toospecify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a><span data-ttu-id="58ecd-163">Actualización de una instalación existente de componentes de Trabajos de base de datos elástica mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="58ecd-163">Update an existing Elastic Database jobs components installation using PowerShell</span></span>
<span data-ttu-id="58ecd-164">**trabajos de base de datos elástica** se pueden actualizar en una instalación existente para escalado y alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="58ecd-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span></span> <span data-ttu-id="58ecd-165">Este proceso permite futuras actualizaciones de código de servicio sin necesidad de toodrop y volver a crear la base de datos de control de Hola.</span><span class="sxs-lookup"><span data-stu-id="58ecd-165">This process allows for future upgrades of service code without having toodrop and recreate hello control database.</span></span> <span data-ttu-id="58ecd-166">Este proceso también puede usarse en hello misma versión toomodify Hola servicio VM tamaño u Hola servidor worker del recuento.</span><span class="sxs-lookup"><span data-stu-id="58ecd-166">This process can also be used within hello same version toomodify hello service VM size or hello server worker count.</span></span>

<span data-ttu-id="58ecd-167">tamaño de máquina virtual de hello tooupdate de una instalación, Hola ejecución siguiente secuencia de comandos con parámetros actualiza los valores de toohello de su elección.</span><span class="sxs-lookup"><span data-stu-id="58ecd-167">tooupdate hello VM size of an installation, run hello following script with parameters updated toohello values of your choice.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th><span data-ttu-id="58ecd-168">Parámetro</span><span class="sxs-lookup"><span data-stu-id="58ecd-168">Parameter</span></span></th>
  <th><span data-ttu-id="58ecd-169">Description</span><span class="sxs-lookup"><span data-stu-id="58ecd-169">Description</span></span></th>
</tr>

  <tr>
    <td><span data-ttu-id="58ecd-170">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="58ecd-170">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="58ecd-171">Identifica el nombre del grupo de recursos de Azure de hello utilizado al instalar componentes de trabajo de base de datos elástica de hello inicialmente.</span><span class="sxs-lookup"><span data-stu-id="58ecd-171">Identifies hello Azure resource group name used when hello Elastic Database job components were initially installed.</span></span> <span data-ttu-id="58ecd-172">Este parámetro tiene como valor predeterminado demasiado "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="58ecd-172">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="58ecd-173">Ya que no es recomendable toochange este valor, que no debería haber toospecify este parámetro.</span><span class="sxs-lookup"><span data-stu-id="58ecd-173">Since it is not recommended toochange this value, you shouldn't have toospecify this parameter.</span></span></td>
    </tr>
</tr>

</tr>

  <tr>
    <td><span data-ttu-id="58ecd-174">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="58ecd-174">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="58ecd-175">Proporciona el número de Hola de tooinstall de los trabajadores de servicio.</span><span class="sxs-lookup"><span data-stu-id="58ecd-175">Provides hello number of service workers tooinstall.</span></span>  <span data-ttu-id="58ecd-176">Este parámetro tiene como valor predeterminado too1.</span><span class="sxs-lookup"><span data-stu-id="58ecd-176">This parameter defaults too1.</span></span>  <span data-ttu-id="58ecd-177">Un número mayor de los trabajadores puede ser usado tooscale out Hola servicio y tooprovide alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="58ecd-177">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span>  <span data-ttu-id="58ecd-178">Se recomienda toouse "2" para las implementaciones que necesitan una alta disponibilidad del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="58ecd-178">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
</tr>

</tr>

    <tr>
    <td><span data-ttu-id="58ecd-179">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="58ecd-179">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="58ecd-180">Proporciona el tamaño VM de hello para el uso dentro de hello servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="58ecd-180">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="58ecd-181">Este parámetro tiene como valor predeterminado tooA0.</span><span class="sxs-lookup"><span data-stu-id="58ecd-181">This parameter defaults tooA0.</span></span> <span data-ttu-id="58ecd-182">Se aceptan valores de parámetros de A0/A1 y A2/A3 que hacer al trabajo de hello rol toouse un tamaño ExtraSmall/pequeño/mediano/grande, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="58ecd-182">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="58ecd-183">Para obtener más información sobre los tamaños de rol de trabajo, consulte [Componentes y precios de trabajos de base de datos elástica](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="58ecd-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a><span data-ttu-id="58ecd-184">Instalar componentes de trabajos de bases de datos elásticas hello mediante Hola Portal</span><span class="sxs-lookup"><span data-stu-id="58ecd-184">Install hello Elastic Database jobs components using hello Portal</span></span>
<span data-ttu-id="58ecd-185">Una vez que tenga [crea un grupo elástico](sql-database-elastic-pool-manage-portal.md), puede instalar **trabajos de base de datos elástica** ejecución tooenable de componentes de las tareas administrativas en cada base de datos en el grupo elástico Hola.</span><span class="sxs-lookup"><span data-stu-id="58ecd-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components tooenable execution of administrative tasks against each database in hello elastic pool.</span></span> <span data-ttu-id="58ecd-186">A diferencia de cuando utilizando Hola **trabajos de base de datos elástica** PowerShell APIs, interfaz del portal de hello está restringido actualmente tooonly ejecutar en un grupo existente.</span><span class="sxs-lookup"><span data-stu-id="58ecd-186">Unlike when using hello **Elastic Database jobs** PowerShell APIs, hello portal interface is currently restricted tooonly executing against an existing pool.</span></span>

<span data-ttu-id="58ecd-187">**Estimado toocomplete de tiempo:** 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="58ecd-187">**Estimated time toocomplete:** 10 minutes.</span></span>

1. <span data-ttu-id="58ecd-188">Desde la vista de panel de Hola de grupo elástico de Hola a través de hello [Portal de Azure](https://portal.azure.com/#) , haga clic en **crear trabajo**.</span><span class="sxs-lookup"><span data-stu-id="58ecd-188">From hello dashboard view of hello elastic pool via hello [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span></span>
2. <span data-ttu-id="58ecd-189">Si va a crear un trabajo para hello primera vez, debe instalar **trabajos de base de datos elástica** haciendo clic en **términos de vista previa**.</span><span class="sxs-lookup"><span data-stu-id="58ecd-189">If you are creating a job for hello first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span></span>
3. <span data-ttu-id="58ecd-190">Aceptar términos Hola haciendo clic en Hola casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="58ecd-190">Accept hello terms by clicking hello checkbox.</span></span>
4. <span data-ttu-id="58ecd-191">En la vista de Hola "instalar servicios", haga clic en **CREDENCIALES de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="58ecd-191">In hello "Install services" view, click **JOB CREDENTIALS**.</span></span>
   
    ![Instalar servicios de Hola][1]
5. <span data-ttu-id="58ecd-193">Escriba un nombre de usuario y una contraseña de administración de la base de datos. Como parte de la instalación de hello, se crea un nuevo servidor de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="58ecd-193">Type a user name and password for a database admin. As part of hello installation, a new Azure SQL Database server is created.</span></span> <span data-ttu-id="58ecd-194">Dentro de este nuevo servidor, una nueva base de datos, conocida como base de datos de control de hello, se crea y utiliza los metadatos de hello toocontain para los trabajos de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="58ecd-194">Within this new server, a new database, known as hello control database, is created and used toocontain hello meta data for Elastic Database jobs.</span></span> <span data-ttu-id="58ecd-195">nombre de usuario de Hello y una contraseña creados aquí se usan a fin de hello del inicio de sesión de base de datos de control de toohello.</span><span class="sxs-lookup"><span data-stu-id="58ecd-195">hello user name and password created here are used for hello purpose of logging in toohello control database.</span></span> <span data-ttu-id="58ecd-196">Se usa una credencial independiente para la ejecución de secuencias de comandos en bases de datos de hello en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="58ecd-196">A separate credential is used for script execution against hello databases within hello pool.</span></span>
   
    ![Creación del nombre de usuario y la contraseña][2]
6. <span data-ttu-id="58ecd-198">Haga clic en el botón Aceptar Hola.</span><span class="sxs-lookup"><span data-stu-id="58ecd-198">Click hello OK button.</span></span> <span data-ttu-id="58ecd-199">componentes de Hola se crean automáticamente en unos minutos en una nueva [grupo de recursos](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="58ecd-199">hello components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="58ecd-200">nuevo grupo de recursos Hola está anclado toohello iniciar panel, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="58ecd-200">hello new resource group is pinned toohello start board, as shown below.</span></span> <span data-ttu-id="58ecd-201">Todos los trabajos de base de datos una vez creados, elástica (servicio en la nube, base de datos SQL, Bus de servicio y almacenamiento) se crean en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="58ecd-201">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in hello group.</span></span>
   
    ![Grupo de recursos en el panel de inicio][3]
7. <span data-ttu-id="58ecd-203">Si intenta toocreate o administrar un trabajo mientras se está instalando los trabajos de base de datos elástica, al proporcionar **credenciales** , verá el siguiente mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="58ecd-203">If you attempt toocreate or manage a job while elastic database jobs is installing, when providing **Credentials** you will see hello following message.</span></span>
   
    ![Implementación en curso][4]

<span data-ttu-id="58ecd-205">Si se requiere la desinstalación, elimine el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="58ecd-205">If uninstallation is required, delete hello resource group.</span></span> <span data-ttu-id="58ecd-206">Vea [cómo toouninstall Hola bases de datos elásticas trabajo componentes](sql-database-elastic-jobs-uninstall.md).</span><span class="sxs-lookup"><span data-stu-id="58ecd-206">See [How toouninstall hello Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="58ecd-207">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="58ecd-207">Next steps</span></span>
<span data-ttu-id="58ecd-208">Asegúrese de una credencial con los derechos apropiados de hello para la ejecución del script se crea en cada base de datos del grupo de hello, para más información, vea [proteger la base de datos de SQL](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="58ecd-208">Ensure a credential with hello appropriate rights for script execution is created on each database in hello group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="58ecd-209">Vea [crear y administrar los trabajos de una base de datos elástica](sql-database-elastic-jobs-create-and-manage.md) tooget iniciado.</span><span class="sxs-lookup"><span data-stu-id="58ecd-209">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) tooget started.</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
