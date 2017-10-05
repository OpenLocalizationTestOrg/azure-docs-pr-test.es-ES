---
title: "Instalación de trabajos de base de datos elástica | Microsoft Docs"
description: "Pasos de instalación de la característica de trabajo elástico."
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
ms.openlocfilehash: e7a2d6dbcefbb31d76257eaf96ccc235d7a29416
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="installing-elastic-database-jobs-overview"></a><span data-ttu-id="40e10-103">Información general sobre la instalación de Trabajos de base de datos elástica</span><span class="sxs-lookup"><span data-stu-id="40e10-103">Installing Elastic Database jobs overview</span></span>
<span data-ttu-id="40e10-104">Los [**trabajos de base de datos elástica**](sql-database-elastic-jobs-overview.md) se pueden instalar a través de PowerShell o del Portal de Azure clásico. Obtendrá acceso para crear y administrar trabajos con la API de PowerShell solo si instala el paquete de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="40e10-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through the Azure Classic Portal.You can gain access to create and manage jobs using the PowerShell API only if you install the PowerShell package.</span></span> <span data-ttu-id="40e10-105">Además, en este momento, las API de PowerShell proporcionan mucha más funcionalidad que el portal en este momento.</span><span class="sxs-lookup"><span data-stu-id="40e10-105">Additionally, the PowerShell APIs provide significantly more functionality than the portal at this point in time.</span></span>

<span data-ttu-id="40e10-106">Si ya instaló los **trabajos de base de datos elástica** a través del Portal a partir de un **grupo elástico** existente, la última versión preliminar de PowerShell incluye scripts para actualizar la instalación existente.</span><span class="sxs-lookup"><span data-stu-id="40e10-106">If you have already installed **Elastic Database jobs** through the Portal from an existing **elastic pool**, the latest Powershell preview includes scripts to upgrade your existing installation.</span></span> <span data-ttu-id="40e10-107">Es muy recomendable actualizar la instalación a los componentes más recientes de los **trabajos de base de datos elástica** para aprovechar la nueva funcionalidad expuesta a través de las API de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="40e10-107">It is highly recommended to upgrade your installation to the latest **Elastic Database jobs** components in order to take advantage of new functionality exposed via the PowerShell APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40e10-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="40e10-108">Prerequisites</span></span>
* <span data-ttu-id="40e10-109">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="40e10-109">An Azure subscription.</span></span> <span data-ttu-id="40e10-110">Para obtener una versión de evaluación gratuita, consulte [Versión de evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="40e10-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="40e10-111">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="40e10-111">Azure PowerShell.</span></span> <span data-ttu-id="40e10-112">Instale la versión más reciente mediante el [Instalador de plataforma web](http://go.microsoft.com/fwlink/p/?linkid=320376).</span><span class="sxs-lookup"><span data-stu-id="40e10-112">Install the latest version using the [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span></span> <span data-ttu-id="40e10-113">Para obtener información detallada, vea [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="40e10-113">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="40e10-114">[utilidad de línea de comandos NuGet](https://nuget.org/nuget.exe) sirve para instalar el paquete de trabajos de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="40e10-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used to install the Elastic Database jobs package.</span></span> <span data-ttu-id="40e10-115">Para obtener más información, consulte http://docs.nuget.org/docs/start-here/installing-nuget.</span><span class="sxs-lookup"><span data-stu-id="40e10-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span></span>

## <a name="download-and-import-the-elastic-database-jobs-powershell-package"></a><span data-ttu-id="40e10-116">Descarga e importación del paquete de PowerShell de Trabajos de base de datos elástica</span><span class="sxs-lookup"><span data-stu-id="40e10-116">Download and import the Elastic Database jobs PowerShell package</span></span>
1. <span data-ttu-id="40e10-117">Inicie la ventana de comandos de Microsoft Azure PowerShell y navegue al directorio donde descargó la utilidad de línea de comandos NuGet (nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="40e10-117">Launch Microsoft Azure PowerShell command window and navigate to the directory where you downloaded NuGet Command-line Utility (nuget.exe).</span></span>
2. <span data-ttu-id="40e10-118">Descargue e importe el paquete de **trabajos de base de datos elástica** en el directorio actual con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="40e10-118">Download and import **Elastic Database jobs** package into the current directory with the following command:</span></span>
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    <span data-ttu-id="40e10-119">Los archivos de **trabajos de base de datos elástica** se ubican en el directorio local, en una carpeta con el nombre **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x**, donde *x.x.xxxx.x* indica el número de versión.</span><span class="sxs-lookup"><span data-stu-id="40e10-119">The **Elastic Database jobs** files are placed in the local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects the version number.</span></span> <span data-ttu-id="40e10-120">Los cmdlets de PowerShell (incluidos los archivos .DLL de cliente necesarios) se ubican en el subdirectorio **tools\ElasticDatabaseJobs** y los scripts de PowerShell para instalar, actualizar y desinstalar también residen en el subdirectorio **tools**.</span><span class="sxs-lookup"><span data-stu-id="40e10-120">The PowerShell cmdlets (including required client .dlls) are located in the **tools\ElasticDatabaseJobs** sub-directory and the PowerShell scripts to install, upgrade and uninstall also reside in the **tools** sub-directory.</span></span>
3. <span data-ttu-id="40e10-121">Navegue al subdirectorio tools de la carpeta Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x. Para ello, escriba cd tools, como en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="40e10-121">Navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. <span data-ttu-id="40e10-122">Ejecute el script .\InstallElasticDatabaseJobsCmdlets.ps1 para copiar el directorio ElasticDatabaseJobs en $home\Documents\WindowsPowerShell\Modules.</span><span class="sxs-lookup"><span data-stu-id="40e10-122">Execute the .\InstallElasticDatabaseJobsCmdlets.ps1 script to copy the ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="40e10-123">Así también importará automáticamente el módulo para su uso, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="40e10-123">This will also automatically import the module for use, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-the-elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="40e10-124">Instalación de componentes de Trabajos de base de datos elástica mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="40e10-124">Install the Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="40e10-125">Inicie una ventana de comandos de Microsoft Azure PowerShell y navegue hasta el subdirectorio \tools en la carpeta Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x: escriba cd \tools</span><span class="sxs-lookup"><span data-stu-id="40e10-125">Launch a Microsoft Azure PowerShell command window and navigate to the \tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. <span data-ttu-id="40e10-126">Ejecute el script .\InstallElasticDatabaseJobs.ps1 de PowerShell y proporcione valores para las variables que solicite.</span><span class="sxs-lookup"><span data-stu-id="40e10-126">Execute the .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span></span> <span data-ttu-id="40e10-127">Este script creará los componentes descritos en [Componentes y precios de trabajos de base de datos elástica](sql-database-elastic-jobs-overview.md#components-and-pricing) con la configuración del Servicio en la nube de Azure para usar adecuadamente los componentes dependientes.</span><span class="sxs-lookup"><span data-stu-id="40e10-127">This script will create the components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring the Azure Cloud Service to appropriately use the dependent components.</span></span>

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

<span data-ttu-id="40e10-128">Al ejecutar este comando, se abrirá una ventana para especificar el **nombre de usuario** y la **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="40e10-128">When you run this command a window opens asking for a **user name** and **password**.</span></span> <span data-ttu-id="40e10-129">No especifique aquí sus credenciales de Azure, sino el nombre de usuario y contraseña serán las credenciales de administrador que desea crear para el nuevo servidor.</span><span class="sxs-lookup"><span data-stu-id="40e10-129">This is not your Azure credentials, enter the user name and password that will be the administrator credentials you want to create for the new server.</span></span>

<span data-ttu-id="40e10-130">Los parámetros proporcionados en esta invocación de ejemplo pueden modificarse para tener la configuración que quiera.</span><span class="sxs-lookup"><span data-stu-id="40e10-130">The parameters provided on this sample invocation can be modified for your desired settings.</span></span> <span data-ttu-id="40e10-131">La siguiente tabla ofrece más información sobre el comportamiento de cada parámetro:</span><span class="sxs-lookup"><span data-stu-id="40e10-131">The following provides more information on the behavior of each parameter:</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="40e10-132">Parámetro</span><span class="sxs-lookup"><span data-stu-id="40e10-132">Parameter</span></span></th>
    <th><span data-ttu-id="40e10-133">Description</span><span class="sxs-lookup"><span data-stu-id="40e10-133">Description</span></span></th>
  </tr>

<tr>
    <td><span data-ttu-id="40e10-134">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="40e10-134">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="40e10-135">Proporciona el nombre del grupo de recursos de Azure creado para contener los componentes de Azure recién creados.</span><span class="sxs-lookup"><span data-stu-id="40e10-135">Provides the Azure resource group name created to contain the newly created Azure components.</span></span> <span data-ttu-id="40e10-136">El valor predeterminado de este parámetro es "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="40e10-136">This parameter defaults to “__ElasticDatabaseJob”.</span></span> <span data-ttu-id="40e10-137">No se recomienda cambiar este valor.</span><span class="sxs-lookup"><span data-stu-id="40e10-137">It is not recommended to change this value.</span></span></td>
    </tr>

</tr>

    <tr>
    <td><span data-ttu-id="40e10-138">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="40e10-138">ResourceGroupLocation</span></span></td>
    <td><span data-ttu-id="40e10-139">Proporciona la ubicación de Azure que se usará para los componentes de Azure recién creados.</span><span class="sxs-lookup"><span data-stu-id="40e10-139">Provides the Azure location to be used for the newly created Azure components.</span></span> <span data-ttu-id="40e10-140">El valor predeterminado de este parámetro es la ubicación Central EE. UU.</span><span class="sxs-lookup"><span data-stu-id="40e10-140">This parameter defaults to the Central US location.</span></span></td>
</tr>

<tr>
    <td><span data-ttu-id="40e10-141">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="40e10-141">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="40e10-142">Proporciona el número de trabajos del servicio que se va a instalar.</span><span class="sxs-lookup"><span data-stu-id="40e10-142">Provides the number of service workers to install.</span></span> <span data-ttu-id="40e10-143">El valor predeterminado de este parámetro es 1.</span><span class="sxs-lookup"><span data-stu-id="40e10-143">This parameter defaults to 1.</span></span> <span data-ttu-id="40e10-144">Puede usarse un número mayor de trabajos para escalar horizontalmente el servicio y ofrecer alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="40e10-144">A higher number of workers can be used to scale out the service and to provide high availability.</span></span> <span data-ttu-id="40e10-145">Se recomienda usar "2" en las implementaciones que requieren alta disponibilidad del servicio.</span><span class="sxs-lookup"><span data-stu-id="40e10-145">It is recommended to use “2” for deployments that require high availability of the service.</span></span></td>
    </tr>

</tr>
    <tr>
    <td><span data-ttu-id="40e10-146">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="40e10-146">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="40e10-147">Proporciona el tamaño de máquina virtual para su uso dentro del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="40e10-147">Provides the VM size for usage within the Cloud Service.</span></span> <span data-ttu-id="40e10-148">El valor predeterminado de este parámetro es A0.</span><span class="sxs-lookup"><span data-stu-id="40e10-148">This parameter defaults to A0.</span></span> <span data-ttu-id="40e10-149">Se aceptan los valores de parámetros de A0/A1/A2/A3, que hacen que el rol de trabajo use un tamaño ExtraSmall/Small/Medium/Large, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="40e10-149">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="40e10-150">Para obtener más información sobre los tamaños de rol de trabajo, consulte [Componentes y precios de trabajos de base de datos elástica](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="40e10-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="40e10-151">SqlServerDatabaseSlo</span><span class="sxs-lookup"><span data-stu-id="40e10-151">SqlServerDatabaseSlo</span></span></td>
    <td><span data-ttu-id="40e10-152">Proporciona el objetivo de nivel de servicio para un servidor Standard Edition.</span><span class="sxs-lookup"><span data-stu-id="40e10-152">Provides the service level objective for a Standard edition.</span></span> <span data-ttu-id="40e10-153">El valor predeterminado de este parámetro es S0.</span><span class="sxs-lookup"><span data-stu-id="40e10-153">This parameter defaults to S0.</span></span> <span data-ttu-id="40e10-154">Se aceptan valores de parámetro de S0/S1/S2/S3 lo que hace que Base de datos SQL de Azure use el SLO respectivo.</span><span class="sxs-lookup"><span data-stu-id="40e10-154">Parameter values of S0/S1/S2/S3 are accepted which cause the Azure SQL Database to use the respective SLO.</span></span> <span data-ttu-id="40e10-155">Para obtener más información sobre SLO de SQL Database, consulte [Componentes y precios de trabajos de base de datos elástica](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="40e10-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="40e10-156">SqlServerAdministratorUserName</span><span class="sxs-lookup"><span data-stu-id="40e10-156">SqlServerAdministratorUserName</span></span></td>
    <td><span data-ttu-id="40e10-157">Proporciona el nombre de usuario del administrador del servidor de Base de datos SQL de Azure recién creado.</span><span class="sxs-lookup"><span data-stu-id="40e10-157">Provides the admin user name for the newly created Azure SQL Database server.</span></span> <span data-ttu-id="40e10-158">Cuando no se especifica, se abrirá una ventana de credenciales de PowerShell para solicitar las credenciales.</span><span class="sxs-lookup"><span data-stu-id="40e10-158">When not specified, a PowerShell credentials window will open to prompt for the credentials.</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="40e10-159">SqlServerAdministratorPassword</span><span class="sxs-lookup"><span data-stu-id="40e10-159">SqlServerAdministratorPassword</span></span></td>
    <td><span data-ttu-id="40e10-160">Proporciona la contraseña del administrador del servidor de Base de datos SQL de Azure recién creado.</span><span class="sxs-lookup"><span data-stu-id="40e10-160">Provides the admin password for the newly created Azure SQL Database server.</span></span> <span data-ttu-id="40e10-161">Cuando no se proporciona, se abrirá una ventana de credenciales de PowerShell para solicitar las credenciales.</span><span class="sxs-lookup"><span data-stu-id="40e10-161">When not provided, a PowerShell credentials window will open to prompt for the credentials.</span></span></td>
</tr>
</table>

<span data-ttu-id="40e10-162">En sistemas destinados a tener grandes cantidades de trabajos ejecutándose en paralelo en gran cantidad de bases de datos, se recomienda especificar parámetros como, por ejemplo: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span><span class="sxs-lookup"><span data-stu-id="40e10-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended to specify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a><span data-ttu-id="40e10-163">Actualización de una instalación existente de componentes de Trabajos de base de datos elástica mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="40e10-163">Update an existing Elastic Database jobs components installation using PowerShell</span></span>
<span data-ttu-id="40e10-164">**trabajos de base de datos elástica** se pueden actualizar en una instalación existente para escalado y alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="40e10-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span></span> <span data-ttu-id="40e10-165">Este proceso permite actualizaciones futuras del código de servicio sin tener que quitar y volver a crear la base de datos de control.</span><span class="sxs-lookup"><span data-stu-id="40e10-165">This process allows for future upgrades of service code without having to drop and recreate the control database.</span></span> <span data-ttu-id="40e10-166">Este proceso también puede usarse dentro de la misma versión para modificar el tamaño de máquina virtual del servicio o el número de trabajos de servidor.</span><span class="sxs-lookup"><span data-stu-id="40e10-166">This process can also be used within the same version to modify the service VM size or the server worker count.</span></span>

<span data-ttu-id="40e10-167">Para actualizar el tamaño de máquina virtual de una instalación, ejecute el siguiente script con parámetros actualizados con los valores que elija.</span><span class="sxs-lookup"><span data-stu-id="40e10-167">To update the VM size of an installation, run the following script with parameters updated to the values of your choice.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th><span data-ttu-id="40e10-168">Parámetro</span><span class="sxs-lookup"><span data-stu-id="40e10-168">Parameter</span></span></th>
  <th><span data-ttu-id="40e10-169">Description</span><span class="sxs-lookup"><span data-stu-id="40e10-169">Description</span></span></th>
</tr>

  <tr>
    <td><span data-ttu-id="40e10-170">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="40e10-170">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="40e10-171">Identifica el nombre del grupo de recursos de Azure usado al instalar inicialmente componentes de Trabajos de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="40e10-171">Identifies the Azure resource group name used when the Elastic Database job components were initially installed.</span></span> <span data-ttu-id="40e10-172">El valor predeterminado de este parámetro es "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="40e10-172">This parameter defaults to “__ElasticDatabaseJob”.</span></span> <span data-ttu-id="40e10-173">Puesto que no se recomienda cambiar este valor, no debería tener que especificar este parámetro.</span><span class="sxs-lookup"><span data-stu-id="40e10-173">Since it is not recommended to change this value, you shouldn't have to specify this parameter.</span></span></td>
    </tr>
</tr>

</tr>

  <tr>
    <td><span data-ttu-id="40e10-174">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="40e10-174">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="40e10-175">Proporciona el número de trabajos del servicio que se va a instalar.</span><span class="sxs-lookup"><span data-stu-id="40e10-175">Provides the number of service workers to install.</span></span>  <span data-ttu-id="40e10-176">El valor predeterminado de este parámetro es 1.</span><span class="sxs-lookup"><span data-stu-id="40e10-176">This parameter defaults to 1.</span></span>  <span data-ttu-id="40e10-177">Puede usarse un número mayor de trabajos para escalar horizontalmente el servicio y ofrecer alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="40e10-177">A higher number of workers can be used to scale out the service and to provide high availability.</span></span>  <span data-ttu-id="40e10-178">Se recomienda usar "2" en las implementaciones que requieren alta disponibilidad del servicio.</span><span class="sxs-lookup"><span data-stu-id="40e10-178">It is recommended to use “2” for deployments that require high availability of the service.</span></span></td>
</tr>

</tr>

    <tr>
    <td><span data-ttu-id="40e10-179">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="40e10-179">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="40e10-180">Proporciona el tamaño de máquina virtual para su uso dentro del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="40e10-180">Provides the VM size for usage within the Cloud Service.</span></span> <span data-ttu-id="40e10-181">El valor predeterminado de este parámetro es A0.</span><span class="sxs-lookup"><span data-stu-id="40e10-181">This parameter defaults to A0.</span></span> <span data-ttu-id="40e10-182">Se aceptan los valores de parámetros de A0/A1/A2/A3, que hacen que el rol de trabajo use un tamaño ExtraSmall/Small/Medium/Large, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="40e10-182">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="40e10-183">Para obtener más información sobre los tamaños de rol de trabajo, consulte [Componentes y precios de trabajos de base de datos elástica](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="40e10-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</table>

## <a name="install-the-elastic-database-jobs-components-using-the-portal"></a><span data-ttu-id="40e10-184">Instalación de componentes de Trabajos de base de datos elástica mediante el Portal</span><span class="sxs-lookup"><span data-stu-id="40e10-184">Install the Elastic Database jobs components using the Portal</span></span>
<span data-ttu-id="40e10-185">Una vez creado el [grupo elástico](sql-database-elastic-pool-manage-portal.md), puede instalar componentes de los **trabajos de base de datos elástica** para habilitar la ejecución de tareas administrativas en cada base de datos del grupo.</span><span class="sxs-lookup"><span data-stu-id="40e10-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components to enable execution of administrative tasks against each database in the elastic pool.</span></span> <span data-ttu-id="40e10-186">A diferencia de lo que sucede cuando se usan las API de PowerShell de **Trabajos de base de datos elástica** , la interfaz del portal está actualmente restringida exclusivamente a la ejecución en un grupo existente.</span><span class="sxs-lookup"><span data-stu-id="40e10-186">Unlike when using the **Elastic Database jobs** PowerShell APIs, the portal interface is currently restricted to only executing against an existing pool.</span></span>

<span data-ttu-id="40e10-187">**Tiempo estimado para completar el tutorial:** 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="40e10-187">**Estimated time to complete:** 10 minutes.</span></span>

1. <span data-ttu-id="40e10-188">En la vista del panel del grupo elástico a través de [Azure Portal](https://portal.azure.com/#), haga clic en **Crear trabajo**.</span><span class="sxs-lookup"><span data-stu-id="40e10-188">From the dashboard view of the elastic pool via the [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span></span>
2. <span data-ttu-id="40e10-189">Si va a crear un trabajo por primera vez, deberá instalar los **trabajos de base de datos elástica** haciendo clic en **TÉRMINOS DE VISTA PREVIA**.</span><span class="sxs-lookup"><span data-stu-id="40e10-189">If you are creating a job for the first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span></span>
3. <span data-ttu-id="40e10-190">Acepte los términos haciendo clic en la casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="40e10-190">Accept the terms by clicking the checkbox.</span></span>
4. <span data-ttu-id="40e10-191">En la vista "Instalar servicios", haga clic en **CREDENCIALES DEL TRABAJO**.</span><span class="sxs-lookup"><span data-stu-id="40e10-191">In the "Install services" view, click **JOB CREDENTIALS**.</span></span>
   
    ![Instalación de los servicios][1]
5. <span data-ttu-id="40e10-193">Escriba un nombre de usuario y una contraseña de administración de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="40e10-193">Type a user name and password for a database admin.</span></span> <span data-ttu-id="40e10-194">Como parte de la instalación, se creará un nuevo servidor de base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="40e10-194">As part of the installation, a new Azure SQL Database server is created.</span></span> <span data-ttu-id="40e10-195">En este nuevo servidor, se creará una nueva base de datos, conocida como base de datos de control, que sirve para contener los metadatos de Trabajos de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="40e10-195">Within this new server, a new database, known as the control database, is created and used to contain the meta data for Elastic Database jobs.</span></span> <span data-ttu-id="40e10-196">El nombre de usuario y la contraseña que se crean aquí se usan con el fin de iniciar sesión en la base de datos de control.</span><span class="sxs-lookup"><span data-stu-id="40e10-196">The user name and password created here are used for the purpose of logging in to the control database.</span></span> <span data-ttu-id="40e10-197">Se usa una credencial diferente para la ejecución de scripts en las bases de datos del grupo.</span><span class="sxs-lookup"><span data-stu-id="40e10-197">A separate credential is used for script execution against the databases within the pool.</span></span>
   
    ![Creación del nombre de usuario y la contraseña][2]
6. <span data-ttu-id="40e10-199">Haga clic en el botón Aceptar.</span><span class="sxs-lookup"><span data-stu-id="40e10-199">Click the OK button.</span></span> <span data-ttu-id="40e10-200">Los componentes se crean en pocos minutos en un nuevo [grupo de recursos](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="40e10-200">The components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="40e10-201">El nuevo grupo de recursos se ancla al panel de inicio, tal como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="40e10-201">The new resource group is pinned to the start board, as shown below.</span></span> <span data-ttu-id="40e10-202">Una vez creados, los trabajos de bases de datos elásticas (servicio de nube, base de datos SQL, bus de servicio y almacenamiento) se crearán en el grupo.</span><span class="sxs-lookup"><span data-stu-id="40e10-202">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in the group.</span></span>
   
    ![Grupo de recursos en el panel de inicio][3]
7. <span data-ttu-id="40e10-204">Si intenta crear o administrar un trabajo mientras se está instalando trabajos de bases de datos elásticas, se mostrará el mensaje siguiente al proporcionar las **Credenciales** .</span><span class="sxs-lookup"><span data-stu-id="40e10-204">If you attempt to create or manage a job while elastic database jobs is installing, when providing **Credentials** you will see the following message.</span></span>
   
    ![Implementación en curso][4]

<span data-ttu-id="40e10-206">Si se requiere la desinstalación, elimine el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="40e10-206">If uninstallation is required, delete the resource group.</span></span> <span data-ttu-id="40e10-207">Consulte [Desinstalación de componentes de trabajos de base de datos elástica](sql-database-elastic-jobs-uninstall.md).</span><span class="sxs-lookup"><span data-stu-id="40e10-207">See [How to uninstall the Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="40e10-208">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="40e10-208">Next steps</span></span>
<span data-ttu-id="40e10-209">Asegúrese de que se cree una credencial con los derechos adecuados para la ejecución del script en cada base de datos del grupo. Para obtener más información, consulte [Protección de bases de datos SQL](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="40e10-209">Ensure a credential with the appropriate rights for script execution is created on each database in the group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="40e10-210">Consulte [Creación y administración de trabajos de base de datos elástica](sql-database-elastic-jobs-create-and-manage.md).</span><span class="sxs-lookup"><span data-stu-id="40e10-210">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) to get started.</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
