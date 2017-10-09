---
title: aaaUsing SQL bases de datos en la pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo puede implementar las bases de datos SQL como un servicio en la pila de Azure y adaptador de proveedor de recursos de SQL Server de hello pasos rápidos toodeploy Hola"
services: azure-stack
documentationCenter: 
author: JeffGoldner
manager: bradleyb
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: JeffGo
ms.openlocfilehash: 01418ce7cd708ca8f9e302d6bcd2a43ad33df93f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-databases-on-microsoft-azure-stack"></a><span data-ttu-id="0b855-103">Uso de bases de datos SQL en Microsoft Azure Stack</span><span class="sxs-lookup"><span data-stu-id="0b855-103">Use SQL databases on Microsoft Azure Stack</span></span>


<span data-ttu-id="0b855-104">Usar Hola SQL Server recursos proveedor adaptador tooexpose bases de datos SQL como un servicio de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="0b855-104">Use hello SQL Server resource provider adapter tooexpose SQL databases as a service of Azure Stack.</span></span> <span data-ttu-id="0b855-105">Después de instalar el proveedor de recursos de Hola y conéctelo a tooone o más instancias de SQL Server, usted y sus usuarios pueden crear bases de datos para aplicaciones nativas de nube y sitios Web que se basa en SQL, cargas de trabajo que se basan en SQL sin tener que tooprovision un virtual máquina (VM) que hospeda SQL Server cada vez.</span><span class="sxs-lookup"><span data-stu-id="0b855-105">After you install hello resource provider and connect it tooone or more SQL Server instances, you and your users can create databases for cloud-native apps, websites that are based on SQL, and workloads that are based on SQL without having tooprovision a virtual machine (VM) that hosts SQL Server each time.</span></span>

<span data-ttu-id="0b855-106">proveedor de recursos de Hello no admite todas las capacidades de administración de base de datos de Hola de [base de datos de SQL Azure](https://azure.microsoft.com/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="0b855-106">hello resource provider does not support all hello database management capabilities of [Azure SQL Database](https://azure.microsoft.com/services/sql-database/).</span></span> <span data-ttu-id="0b855-107">Por ejemplo, no se admiten grupos elástico de base de datos y rendimiento de base de datos de hello capacidad tooscale.</span><span class="sxs-lookup"><span data-stu-id="0b855-107">For example, elastic database pools and hello ability tooscale database performance aren't supported.</span></span> <span data-ttu-id="0b855-108">Hola API no es compatible con la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="0b855-108">hello API is not compatible with SQL DB.</span></span>


## <a name="sql-server-resource-provider-adapter-architecture"></a><span data-ttu-id="0b855-109">Arquitectura del adaptador del proveedor de recursos de SQL Server</span><span class="sxs-lookup"><span data-stu-id="0b855-109">SQL Server Resource Provider Adapter architecture</span></span>
<span data-ttu-id="0b855-110">proveedor de recursos de Hello no se basa en ni ofrece todas las capacidades de administración de base de datos de Hola de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0b855-110">hello resource provider is not based on, nor does it offer all hello database management capabilities of Azure SQL Database.</span></span> <span data-ttu-id="0b855-111">Por ejemplo, grupos de bases de datos elásticas y rendimiento de base de datos de hello capacidad toodial arriba y abajo automáticamente no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="0b855-111">For example, elastic database pools and hello ability toodial database performance up and down automatically aren't available.</span></span> <span data-ttu-id="0b855-112">Sin embargo, Hola recursos proveedor admite similar crear, leer, actualizar y eliminar operaciones (CRUD).</span><span class="sxs-lookup"><span data-stu-id="0b855-112">However, hello resource provider does support similar create, read, update, and delete (CRUD) operations.</span></span>

<span data-ttu-id="0b855-113">proveedor de recursos de Hola se compone de tres componentes:</span><span class="sxs-lookup"><span data-stu-id="0b855-113">hello resource provider is made up of three components:</span></span>

- <span data-ttu-id="0b855-114">**adaptador de proveedor de recursos de Hello SQL VM**, que es una máquina virtual de Windows ejecuta Servicios de proveedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b855-114">**hello SQL resource provider adapter VM**, which is a Windows virtual machine running hello provider services.</span></span>
- <span data-ttu-id="0b855-115">**proveedor de recursos de Hello propio**, que procesa las solicitudes de aprovisionamiento y expone recursos de base de datos.</span><span class="sxs-lookup"><span data-stu-id="0b855-115">**hello resource provider itself**, which processes provisioning requests and exposes database resources.</span></span>
- <span data-ttu-id="0b855-116">**Los servidores que hospedan SQL Server**, que proporcionan capacidad para las bases de datos, conocidos como servidores de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="0b855-116">**Servers that host SQL Server**, which provide capacity for databases, called Hosting Servers.</span></span> 

<span data-ttu-id="0b855-117">Esta versión ya no crea una instancia de SQL.</span><span class="sxs-lookup"><span data-stu-id="0b855-117">This release no longer creates a SQL instance.</span></span> <span data-ttu-id="0b855-118">Debe crear una (o más) o proporcionar acceso a instancias de SQL tooexternal.</span><span class="sxs-lookup"><span data-stu-id="0b855-118">You must create one (or more) and/or provide access tooexternal SQL instances.</span></span> <span data-ttu-id="0b855-119">Hay una serie de opciones tooyou disponibles incluidas las plantillas de hello [Galería de inicio rápido de Azure pila](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) y elementos del Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0b855-119">There are a number of options available tooyou including templates in hello [Azure Stack Quickstart Gallery](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) and Marketplace items.</span></span> 

>[!NOTE]
<span data-ttu-id="0b855-120">Si ha descargado los elementos de Marketplace de SQL, asegúrese de que también descargar Hola extensión de IaaS de SQL o estos no se implementarán.</span><span class="sxs-lookup"><span data-stu-id="0b855-120">If you have downloaded any SQL Marketplace items, make sure you also download hello SQL IaaS Extension or these will not deploy.</span></span>


## <a name="deploy-hello-resource-provider"></a><span data-ttu-id="0b855-121">Implementar el proveedor de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="0b855-121">Deploy hello resource provider</span></span>

1. <span data-ttu-id="0b855-122">Si no lo ha hecho ya, registrar el kit de desarrollo y descargar la imagen de Windows Server 2016 EVAL Hola descargable a través de administración de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0b855-122">If you have not already done so, register your development kit and download hello Windows Server 2016 EVAL image downloadable through Marketplace Management.</span></span> <span data-ttu-id="0b855-123">También puede utilizar una secuencia de comandos toocreate un [imagen de Windows Server 2016](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span><span class="sxs-lookup"><span data-stu-id="0b855-123">You can also use a script toocreate a [Windows Server 2016 image](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span></span> <span data-ttu-id="0b855-124">en tiempo de ejecución de Hello .NET 3.5 ya no es necesario.</span><span class="sxs-lookup"><span data-stu-id="0b855-124">hello .NET 3.5 runtime is no longer required.</span></span>

2. <span data-ttu-id="0b855-125">[Descargar archivo de los archivos binarios de proveedor de recursos SQL de hello](https://aka.ms/azurestacksqlrp) y extraerlo en el host de kit de desarrollo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b855-125">[Download hello SQL resource provider binaries file](https://aka.ms/azurestacksqlrp) and extract it on hello development kit host.</span></span>

3. <span data-ttu-id="0b855-126">Inicie sesión en el host de kit de desarrollo de toohello y extraer Hola directorio temporal del tooa de archivo instalador SQL RP.</span><span class="sxs-lookup"><span data-stu-id="0b855-126">Sign in toohello development kit host and extract hello SQL RP installer file tooa temporary directory.</span></span>

4. <span data-ttu-id="0b855-127">certificado de raíz de Hello Azure pila se recuperan y se crea un certificado autofirmado como parte de este proceso.</span><span class="sxs-lookup"><span data-stu-id="0b855-127">hello Azure Stack root certificate is retrieved and a self-signed certificate is created as part of this process.</span></span> 

    <span data-ttu-id="0b855-128">__Opcional:__ si necesita tooprovide su propietario, preparar certificados hello y copiar el directorio local de tooa si desea toocustomize certificados hello (script de instalación toohello pasado).</span><span class="sxs-lookup"><span data-stu-id="0b855-128">__Optional:__ If you need tooprovide your own, prepare hello certificates and copy tooa local directory if you wish toocustomize hello certificates (passed toohello installation script).</span></span> <span data-ttu-id="0b855-129">Necesita Hola siguientes certificados:</span><span class="sxs-lookup"><span data-stu-id="0b855-129">You need hello following certificates:</span></span>

    <span data-ttu-id="0b855-130">a.</span><span class="sxs-lookup"><span data-stu-id="0b855-130">a.</span></span> <span data-ttu-id="0b855-131">Un certificado comodín para *.dbadapter.\<región\>.\<fqdn externo\>.</span><span class="sxs-lookup"><span data-stu-id="0b855-131">A wildcard certificate for *.dbadapter.\<region\>.\<external fqdn\>.</span></span> <span data-ttu-id="0b855-132">Este certificado debe ser de confianza, como podría ser emitido por una entidad de certificación (es decir, cadena Hola de confianza debe existir sin necesidad de certificados intermedios). (Un certificado de sitio solo puede utilizarse con nombre VM explícito Hola que proporcionar durante la instalación).</span><span class="sxs-lookup"><span data-stu-id="0b855-132">This certificate must be trusted, such as would be issued by a certificate authority (that is, hello chain of trust must exist without requiring intermediate certificates.) (A single site certificate can be used with hello explicit VM name you provide during install.)</span></span>

    <span data-ttu-id="0b855-133">b.</span><span class="sxs-lookup"><span data-stu-id="0b855-133">b.</span></span> <span data-ttu-id="0b855-134">certificado de raíz de Hello utilizado por hello Azure Resource Manager para la instancia de la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="0b855-134">hello root certificate used by hello Azure Resource Manager for your instance of Azure Stack.</span></span> <span data-ttu-id="0b855-135">Si no se encuentra, se recuperará el certificado de raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b855-135">If it is not found, hello root certificate will be retrieved.</span></span>


5. <span data-ttu-id="0b855-136">Abra un **nueva** elevados de PowerShell de la consola y cambie el directorio de toohello donde extrajo los archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b855-136">Open a **new** elevated PowerShell console and change toohello directory where you extracted hello files.</span></span> <span data-ttu-id="0b855-137">Usar un nuevo tooavoid problemas de ventana que pueden surgir de módulos de PowerShell incorrectos ya están cargados en el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b855-137">Use a new window tooavoid problems that may arise from incorrect PowerShell modules already loaded on hello system.</span></span>

6. <span data-ttu-id="0b855-138">Si ha instalado cualquier versión de Hola AzureRm o AzureStack PowerShell módulos que no sean 1.2.9 o 1.2.10, es posible que tooremove solicitada ellos u Hola instalación no continuará.</span><span class="sxs-lookup"><span data-stu-id="0b855-138">If you have installed any versions of hello AzureRm or AzureStack PowerShell modules other than 1.2.9 or 1.2.10, you will be prompted tooremove them or hello install will not proceed.</span></span> <span data-ttu-id="0b855-139">Se incluyen las versiones 1.3 o posterior.</span><span class="sxs-lookup"><span data-stu-id="0b855-139">This includes versions 1.3 or greater.</span></span>

7. <span data-ttu-id="0b855-140">Ejecute hello DeploySqlProvider.ps1 secuencia de comandos con parámetros de hello enumerada a continuación.</span><span class="sxs-lookup"><span data-stu-id="0b855-140">Run hello DeploySqlProvider.ps1 script with hello parameters listed below.</span></span>

<span data-ttu-id="0b855-141">script de Hola realiza estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0b855-141">hello script performs these steps:</span></span>

* <span data-ttu-id="0b855-142">Si es necesario, descargue una versión compatible de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0b855-142">If necessary, download a compatible version of Azure PowerShell.</span></span>
* <span data-ttu-id="0b855-143">Cargar certificados de Hola y otra cuenta de almacenamiento de tooa de artefactos en la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="0b855-143">Upload hello certificates and other artifacts tooa storage account on your Azure Stack.</span></span>
* <span data-ttu-id="0b855-144">Publicar paquetes de la Galería para que pueda implementar bases de datos SQL a través de la Galería de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b855-144">Publish gallery packages so that you can deploy SQL databases through hello gallery.</span></span>
* <span data-ttu-id="0b855-145">Implementar una máquina virtual mediante la imagen de Windows Server 2016 Hola creado en el paso 1 e instalar el proveedor de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b855-145">Deploy a VM using hello Windows Server 2016 image created in step 1 and install hello resource provider.</span></span>
* <span data-ttu-id="0b855-146">Registrar un registro DNS local que se asigna el proveedor de recursos de tooyour máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0b855-146">Register a local DNS record that maps tooyour resource provider VM.</span></span>
* <span data-ttu-id="0b855-147">Registre el proveedor de recursos con hello local Azure Resource Manager (inquilino y administrador).</span><span class="sxs-lookup"><span data-stu-id="0b855-147">Register your resource provider with hello local Azure Resource Manager (Tenant and Admin).</span></span>

> [!NOTE]
> <span data-ttu-id="0b855-148">Si la instalación de hello tiene más de 90 minutos, se puede producir un error y verá un mensaje de error en la pantalla de bienvenida y en el archivo de registro de hello, pero se vuelve a intentar implementación Hola de hello errores paso.</span><span class="sxs-lookup"><span data-stu-id="0b855-148">If hello installation takes more than 90 minutes, it may fail and you see a failure message on hello screen and in hello log file, but hello deployment is retried from hello failing step.</span></span> <span data-ttu-id="0b855-149">Sistemas que no cumplen Hola memoria recomendada y las especificaciones principales pueden no ser capaz de toodeploy Hola SQL RP.</span><span class="sxs-lookup"><span data-stu-id="0b855-149">Systems that do not meet hello recommended memory and core specifications may not be able toodeploy hello SQL RP.</span></span>
>

<span data-ttu-id="0b855-150">Este es un ejemplo que se puede ejecutar desde Hola PowerShell solicite (pero cambiar extremos de información y el portal de la cuenta de hello según sea necesario):</span><span class="sxs-lookup"><span data-stu-id="0b855-150">Here's an example you can run from hello PowerShell prompt (but change hello account information and portal endpoints as needed):</span></span>

```
# Install hello AzureRM.Bootstrapper module
Install-Module -Name AzureRm.BootStrapper -Force

# Installs and imports hello API Version Profile required by Azure Stack into hello current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile
Install-Module -Name AzureStack -RequiredVersion 1.2.10 -Force

# Download hello Azure Stack Tools from GitHub and set hello environment
cd c:\
Invoke-Webrequest https://github.com/Azure/AzureStack-Tools/archive/master.zip -OutFile master.zip
Expand-Archive master.zip -DestinationPath . -Force

# This endpoint may be different for your installation
Import-Module C:\AzureStack-Tools-master\Connect\AzureStack.Connect.psm1
Add-AzureRmEnvironment -Name AzureStackAdmin -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

# For AAD, use hello following
$tenantID = Get-AzsDirectoryTenantID -AADTenantName "<your directory name>" -EnvironmentName AzureStackAdmin

# For ADFS, replace hello previous line with
# $tenantID = Get-AzsDirectoryTenantID -ADFS -EnvironmentName AzureStackAdmin

$vmLocalAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("sqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory toohello folder where you extracted hello installation files 
# and adjust hello endpoints
<extracted file directory>\DeploySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "SqlRPRG" -VmName "SqlVM" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass
 ```

### <a name="deploysqlproviderps1-parameters"></a><span data-ttu-id="0b855-151">Parámetros de DeploySqlProvider.ps1</span><span class="sxs-lookup"><span data-stu-id="0b855-151">DeploySqlProvider.ps1 parameters</span></span>
<span data-ttu-id="0b855-152">Puede especificar estos parámetros en la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b855-152">You can specify these parameters in hello command line.</span></span> <span data-ttu-id="0b855-153">Si no lo hace, o se produce un error en cualquier validación de parámetros, se le solicitará tooprovide Hola requiere los.</span><span class="sxs-lookup"><span data-stu-id="0b855-153">If you do not, or any parameter validation fails, you are prompted tooprovide hello required ones.</span></span>

| <span data-ttu-id="0b855-154">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="0b855-154">Parameter Name</span></span> | <span data-ttu-id="0b855-155">Descripción</span><span class="sxs-lookup"><span data-stu-id="0b855-155">Description</span></span> | <span data-ttu-id="0b855-156">Comentario o valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="0b855-156">Comment or Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b855-157">**DirectoryTenantID**</span><span class="sxs-lookup"><span data-stu-id="0b855-157">**DirectoryTenantID**</span></span> | <span data-ttu-id="0b855-158">Hello Azure o el identificador de directorio de AD FS (guid).</span><span class="sxs-lookup"><span data-stu-id="0b855-158">hello Azure or ADFS Directory ID (guid).</span></span> | <span data-ttu-id="0b855-159">_obligatorio_</span><span class="sxs-lookup"><span data-stu-id="0b855-159">_required_</span></span> |
| <span data-ttu-id="0b855-160">**AzCredential**</span><span class="sxs-lookup"><span data-stu-id="0b855-160">**AzCredential**</span></span> | <span data-ttu-id="0b855-161">Proporcione las credenciales de Hola para hello cuenta de administrador de servicio de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="0b855-161">Provide hello credentials for hello Azure Stack Service Admin account.</span></span> <span data-ttu-id="0b855-162">Debe usar hello mismo las credenciales que usó para la implementación de pila de Azure).</span><span class="sxs-lookup"><span data-stu-id="0b855-162">You must use hello same credentials as you used for deploying Azure Stack).</span></span> | <span data-ttu-id="0b855-163">_obligatorio_</span><span class="sxs-lookup"><span data-stu-id="0b855-163">_required_</span></span> |
| <span data-ttu-id="0b855-164">**VMLocalCredential**</span><span class="sxs-lookup"><span data-stu-id="0b855-164">**VMLocalCredential**</span></span> | <span data-ttu-id="0b855-165">Definir las credenciales de hello para la cuenta de administrador local de Hola de proveedor de recursos SQL de hello VM.</span><span class="sxs-lookup"><span data-stu-id="0b855-165">Define hello credentials for hello local administrator account of hello SQL resource provider VM.</span></span> <span data-ttu-id="0b855-166">Esta contraseña también se utiliza para hello SQL **sa** cuenta.</span><span class="sxs-lookup"><span data-stu-id="0b855-166">This password is also used for hello SQL **sa** account.</span></span> | <span data-ttu-id="0b855-167">_obligatorio_</span><span class="sxs-lookup"><span data-stu-id="0b855-167">_required_</span></span> |
| <span data-ttu-id="0b855-168">**ResourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="0b855-168">**ResourceGroupName**</span></span> | <span data-ttu-id="0b855-169">Defina un nombre para un grupo de recursos en el que se almacenarán los elementos creados por este script.</span><span class="sxs-lookup"><span data-stu-id="0b855-169">Define a name for a Resource Group in which items created by this script will be stored.</span></span> <span data-ttu-id="0b855-170">Por ejemplo, *SqlRPRG*.</span><span class="sxs-lookup"><span data-stu-id="0b855-170">For example, *SqlRPRG*.</span></span> |  <span data-ttu-id="0b855-171">_requerido_</span><span class="sxs-lookup"><span data-stu-id="0b855-171">_required_</span></span> |
| <span data-ttu-id="0b855-172">**VmName**</span><span class="sxs-lookup"><span data-stu-id="0b855-172">**VmName**</span></span> | <span data-ttu-id="0b855-173">Definir nombre de Hola de máquina virtual de hello en qué proveedor de recursos de tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="0b855-173">Define hello name of hello virtual machine on which tooinstall hello resource provider.</span></span> <span data-ttu-id="0b855-174">Por ejemplo, *SqlVM*.</span><span class="sxs-lookup"><span data-stu-id="0b855-174">For example, *SqlVM*.</span></span> |  <span data-ttu-id="0b855-175">_requerido_</span><span class="sxs-lookup"><span data-stu-id="0b855-175">_required_</span></span> |
| <span data-ttu-id="0b855-176">**DependencyFilesLocalPath**</span><span class="sxs-lookup"><span data-stu-id="0b855-176">**DependencyFilesLocalPath**</span></span> | <span data-ttu-id="0b855-177">Los archivos de certificados se deben colocar también en este directorio.</span><span class="sxs-lookup"><span data-stu-id="0b855-177">Your certificate files must be placed in this directory as well.</span></span> | <span data-ttu-id="0b855-178">_opcional_</span><span class="sxs-lookup"><span data-stu-id="0b855-178">_optional_</span></span> |
| <span data-ttu-id="0b855-179">**DefaultSSLCertificatePassword**</span><span class="sxs-lookup"><span data-stu-id="0b855-179">**DefaultSSLCertificatePassword**</span></span> | <span data-ttu-id="0b855-180">contraseña de Hello para el archivo de certificado .pfx Hola</span><span class="sxs-lookup"><span data-stu-id="0b855-180">hello password for hello .pfx certificate</span></span> | <span data-ttu-id="0b855-181">_obligatorio_</span><span class="sxs-lookup"><span data-stu-id="0b855-181">_required_</span></span> |
| <span data-ttu-id="0b855-182">**MaxRetryCount**</span><span class="sxs-lookup"><span data-stu-id="0b855-182">**MaxRetryCount**</span></span> | <span data-ttu-id="0b855-183">Definir cuántas veces desea tooretry cada operación si se produce un error.</span><span class="sxs-lookup"><span data-stu-id="0b855-183">Define how many times you want tooretry each operation if there is a failure.</span></span>| <span data-ttu-id="0b855-184">2</span><span class="sxs-lookup"><span data-stu-id="0b855-184">2</span></span> |
| <span data-ttu-id="0b855-185">**RetryDuration**</span><span class="sxs-lookup"><span data-stu-id="0b855-185">**RetryDuration**</span></span> | <span data-ttu-id="0b855-186">Defina el tiempo de espera de hello entre reintentos, en segundos.</span><span class="sxs-lookup"><span data-stu-id="0b855-186">Define hello timeout between retries, in seconds.</span></span> | <span data-ttu-id="0b855-187">120</span><span class="sxs-lookup"><span data-stu-id="0b855-187">120</span></span> |
| <span data-ttu-id="0b855-188">**Desinstalación**</span><span class="sxs-lookup"><span data-stu-id="0b855-188">**Uninstall**</span></span> | <span data-ttu-id="0b855-189">Quitar el proveedor de recursos de Hola y todos los recursos asociados (vea las notas siguientes)</span><span class="sxs-lookup"><span data-stu-id="0b855-189">Remove hello resource provider and all associated resources (see notes below)</span></span> | <span data-ttu-id="0b855-190">No</span><span class="sxs-lookup"><span data-stu-id="0b855-190">No</span></span> |
| <span data-ttu-id="0b855-191">**DebugMode**</span><span class="sxs-lookup"><span data-stu-id="0b855-191">**DebugMode**</span></span> | <span data-ttu-id="0b855-192">Impide la limpieza automática en caso de error.</span><span class="sxs-lookup"><span data-stu-id="0b855-192">Prevents automatic cleanup on failure</span></span> | <span data-ttu-id="0b855-193">No</span><span class="sxs-lookup"><span data-stu-id="0b855-193">No</span></span> |


## <a name="verify-hello-deployment-using-hello-azure-stack-portal"></a><span data-ttu-id="0b855-194">Comprobar la implementación de hello mediante Hola Portal de la pila de Azure</span><span class="sxs-lookup"><span data-stu-id="0b855-194">Verify hello deployment using hello Azure Stack Portal</span></span>

> [!NOTE]
>  <span data-ttu-id="0b855-195">Una vez completado el script de instalación de hello, necesitará hoja de administración de toorefresh hello toosee portal Hola.</span><span class="sxs-lookup"><span data-stu-id="0b855-195">After hello installation script completes, you will need toorefresh hello portal toosee hello admin blade.</span></span>


1. <span data-ttu-id="0b855-196">En el escritorio de máquina virtual de la consola de hello, haga clic en **Portal de Microsoft Azure pila** e inicie sesión en el portal de toohello como administrador de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b855-196">On hello Console VM desktop, click **Microsoft Azure Stack Portal** and sign in toohello portal as hello service administrator.</span></span>

2. <span data-ttu-id="0b855-197">Compruebe que la implementación de Hola se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="0b855-197">Verify that hello deployment succeeded.</span></span> <span data-ttu-id="0b855-198">Haga clic en **grupos de recursos** &gt; haga clic en el grupo de recursos de Hola que usó y, a continuación, asegúrese de que esa parte de essentials Hola de lecturas de hoja (mitad superior) de hello  **_fecha_ (correcto)**.</span><span class="sxs-lookup"><span data-stu-id="0b855-198">Click **Resource Groups** &gt; click hello resource group you used and then make sure that hello essentials part of hello blade (upper half) reads **_date_ (Succeeded)**.</span></span>

      ![Comprobar la implementación de hello SQL RP](./media/azure-stack-sql-rp-deploy/sqlrp-verify.png)


## <a name="provide-capacity-by-connecting-tooa-hosting-sql-server"></a><span data-ttu-id="0b855-200">Proporcionar una capacidad mediante la conexión tooa que hospeda SQL server</span><span class="sxs-lookup"><span data-stu-id="0b855-200">Provide capacity by connecting tooa hosting SQL server</span></span>

1. <span data-ttu-id="0b855-201">Inicie sesión en toohello portal de administración de la pila de Azure como un administrador de servicios</span><span class="sxs-lookup"><span data-stu-id="0b855-201">Sign in toohello Azure Stack admin portal as a service admin</span></span>

2. <span data-ttu-id="0b855-202">Cree una máquina virtual SQL, a menos que tenga una ya disponible.</span><span class="sxs-lookup"><span data-stu-id="0b855-202">Create a SQL virtual machine, unless you have one already available.</span></span> <span data-ttu-id="0b855-203">Marketplace Management ofrece algunas opciones para implementar máquinas virtuales SQL.</span><span class="sxs-lookup"><span data-stu-id="0b855-203">Marketplace Management offers some options for deploying SQL VMs.</span></span>

3. <span data-ttu-id="0b855-204">Haga clic en **Proveedores de recursos** &gt; **SQLAdapter** &gt; **Hosting Servers** (Servidores de hospedaje) &gt; **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0b855-204">Click **Resource Providers** &gt; **SQLAdapter** &gt; **Hosting Servers** &gt; **+Add**.</span></span>

    <span data-ttu-id="0b855-205">Hola **servidores de hospedaje de SQL** hoja es donde puede conectar Hola proveedor de recursos de SQL Server tooactual instancias de SQL Server que actúan como Hola back-end del proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="0b855-205">hello **SQL Hosting Servers** blade is where you can connect hello SQL Server Resource Provider tooactual instances of SQL Server that serve as hello resource provider’s backend.</span></span>

    ![Servidores de hospedaje](./media/azure-stack-sql-rp-deploy/sqlrp-hostingserver.PNG)

4. <span data-ttu-id="0b855-207">Rellenar el formulario de hello con detalles de la conexión de saludo de la instancia de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0b855-207">Fill hello form with hello connection details of your SQL Server instance.</span></span>

    ![Nuevo servidor de hospedaje](./media/azure-stack-sql-rp-deploy/sqlrp-newhostingserver.PNG)

    > [!NOTE]
    > <span data-ttu-id="0b855-209">Siempre que puede tener acceso a la instancia SQL de Hola por inquilino hello y administración de Azure Resource Manager, se puede colocar bajo el control de proveedor de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b855-209">As long as hello SQL instance can be accessed by hello tenant and admin Azure Resource Manager, it can be placed under control of hello resource provider.</span></span> <span data-ttu-id="0b855-210">instancia de SQL de Hello __debe__ asignar exclusivamente toohello RP.</span><span class="sxs-lookup"><span data-stu-id="0b855-210">hello SQL instance __must__ be allocated exclusively toohello RP.</span></span>

5. <span data-ttu-id="0b855-211">Cuando agregue servidores, debe asignarlos tooa nuevas o existentes SKU toodifferentiate ofertas de servicio.</span><span class="sxs-lookup"><span data-stu-id="0b855-211">As you add servers, you must assign them tooa new or existing SKU toodifferentiate service offerings.</span></span> <span data-ttu-id="0b855-212">Por ejemplo, podría tener una instancia de SQL Enterprise proporciona capacidad de la base de datos y copia de seguridad automática, reservar servidores de alto rendimiento para que los departamentos individuales, nombre de SKU de hello etc. debe reflejar propiedades Hola para que los inquilinos pueden colocar sus bases de datos correctamente y deben tener todos los servidores de hospedaje en una SKU hello las mismas capacidades.</span><span class="sxs-lookup"><span data-stu-id="0b855-212">For example, you could have a SQL Enterprise instance providing database capacity and automatic backup, reserve high-performance servers for individual departments, etc. hello SKU name should reflect hello properties so that tenants can place their databases appropriately and all hosting servers in a SKU should have hello same capabilities.</span></span>

    <span data-ttu-id="0b855-213">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0b855-213">An example:</span></span>

    ![SKU](./media/azure-stack-sql-rp-deploy/sqlrp-newsku.png)

>[!NOTE]
<span data-ttu-id="0b855-215">SKU pueden tardar hasta tooan hora toobe visible en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b855-215">SKUs can take up tooan hour toobe visible in hello portal.</span></span> <span data-ttu-id="0b855-216">No se puede crear una base de datos hasta que Hola que SKU se crea.</span><span class="sxs-lookup"><span data-stu-id="0b855-216">You cannot create a database until hello SKU is created.</span></span>


## <a name="create-your-first-sql-database-tootest-your-deployment"></a><span data-ttu-id="0b855-217">Crear la implementación de su primera tootest de base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="0b855-217">Create your first SQL database tootest your deployment</span></span>

1. <span data-ttu-id="0b855-218">Inicie sesión en toohello portal de administración de la pila de Azure como administrador del servicio.</span><span class="sxs-lookup"><span data-stu-id="0b855-218">Sign in toohello Azure Stack admin portal as service admin.</span></span>

2. <span data-ttu-id="0b855-219">Haga clic en **+ Nuevo** &gt; **Datos y almacenamiento "** &gt; **SQL Server Datbase (versión preliminar)** &gt; **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0b855-219">Click **+ New** &gt;**Data + Storage"** &gt; **SQL Server Database (preview)** &gt; **Add**.</span></span>

3. <span data-ttu-id="0b855-220">Rellene el formulario de hello con los detalles de la base de datos, incluidos un **nombre de base de datos**, **tamaño máximo**, y cambio Hola otros parámetros según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0b855-220">Fill in hello form with database details, including a **Database Name**, **Maximum Size**, and change hello other parameters as necessary.</span></span> <span data-ttu-id="0b855-221">Es más frecuentes toopick una SKU para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="0b855-221">You are asked toopick a SKU for your database.</span></span> <span data-ttu-id="0b855-222">Cuando se agregan servidores de hospedaje, que están asignados a una SKU y las bases de datos se crean en ese grupo de servidores que componen Hola SKU de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="0b855-222">As hosting servers are added, they are assigned a SKU and databases are created in that pool of hosting servers that make up hello SKU.</span></span>

    ![Nueva base de datos](./media/azure-stack-sql-rp-deploy/newsqldb.png)


4. <span data-ttu-id="0b855-224">Rellene Hola configuración de inicio de sesión: **inicio de sesión de base de datos**, y **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0b855-224">Fill in hello Login Settings: **Database login**, and **Password**.</span></span> <span data-ttu-id="0b855-225">Se trata de una credencial de autenticación de SQL que se crea para el acceso toothis base de datos únicamente.</span><span class="sxs-lookup"><span data-stu-id="0b855-225">This is a SQL Authentication credential that is created for your access toothis database only.</span></span> <span data-ttu-id="0b855-226">nombre de usuario de inicio de sesión de Hello debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="0b855-226">hello login user name must be globally unique.</span></span> <span data-ttu-id="0b855-227">Cree una nueva configuración de inicio de sesión o seleccione una existente.</span><span class="sxs-lookup"><span data-stu-id="0b855-227">Either create a new login setting or select an existing one.</span></span> <span data-ttu-id="0b855-228">Configuración de inicio de sesión se puede reutilizar para otras bases de datos mediante Hola misma SKU.</span><span class="sxs-lookup"><span data-stu-id="0b855-228">You can reuse login settings for other databases using hello same SKU.</span></span>

    ![Creación de un nuevo inicio de sesión en la base de datos](./media/azure-stack-sql-rp-deploy/create-new-login.png)


5. <span data-ttu-id="0b855-230">Enviar el formulario de Hola y espere Hola implementación toocomplete.</span><span class="sxs-lookup"><span data-stu-id="0b855-230">Submit hello form and wait for hello deployment toocomplete.</span></span>

    <span data-ttu-id="0b855-231">En hoja resultante de hello, observe el campo de "Cadena de conexión" Hola.</span><span class="sxs-lookup"><span data-stu-id="0b855-231">In hello resulting blade, notice hello “Connection string” field.</span></span> <span data-ttu-id="0b855-232">Puede usar esa cadena en cualquier aplicación que requiera acceso a SQL Server (por ejemplo, una aplicación web) en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="0b855-232">You can use that string in any application that requires SQL Server access (for example, a web app) in your Azure Stack.</span></span>

    ![Recuperar la cadena de conexión de Hola](./media/azure-stack-sql-rp-deploy/sql-db-settings.png)

## <a name="add-capacity"></a><span data-ttu-id="0b855-234">Ampliación de capacidad</span><span class="sxs-lookup"><span data-stu-id="0b855-234">Add capacity</span></span>

<span data-ttu-id="0b855-235">Agregar más capacidad mediante la adición de hosts SQL adicionales en el portal de Azure pila hello y asociarlos a una SKU adecuado.</span><span class="sxs-lookup"><span data-stu-id="0b855-235">Add capacity by adding additional SQL hosts in hello Azure Stack portal and associate them with an appropriate SKU.</span></span> <span data-ttu-id="0b855-236">Si desea que otra instancia de SQL en lugar de hello uno instalado en el proveedor de hello VM toouse, haga clic en **proveedores de recursos** &gt; **SQLAdapter** &gt; **hospedaje de SQL Servidores** &gt; **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="0b855-236">If you wish toouse another instance of SQL instead of hello one installed on hello provider VM, click **Resource Providers** &gt; **SQLAdapter** &gt; **SQL Hosting Servers** &gt; **+Add**.</span></span>

## <a name="making-sql-databases-available-tootenants"></a><span data-ttu-id="0b855-237">Hacer que las bases de datos SQL tootenants disponibles</span><span class="sxs-lookup"><span data-stu-id="0b855-237">Making SQL databases available tootenants</span></span>

<span data-ttu-id="0b855-238">Crear planes y ofertas toomake bases de datos SQL disponibles para los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="0b855-238">Create plans and offers toomake SQL databases available for tenants.</span></span> <span data-ttu-id="0b855-239">Debe crear un plan, agregar hello Microsoft.SqlAdapter servicio toohello plan y agregar una cuota existente o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="0b855-239">You must create a plan, add hello Microsoft.SqlAdapter service toohello plan, and add an existing Quota, or create a new one.</span></span> <span data-ttu-id="0b855-240">Si creas una cuota, puede especificar el inquilino de hello capacidad tooallow Hola.</span><span class="sxs-lookup"><span data-stu-id="0b855-240">If you create a quota, you can specify hello capacity tooallow hello tenant.</span></span>
    <span data-ttu-id="0b855-241">![Crear planes y ofertas tooinclude bases de datos](./media/azure-stack-sql-rp-deploy/sqlrp-newplan.png)</span><span class="sxs-lookup"><span data-stu-id="0b855-241">![Create plans and offers tooinclude databases](./media/azure-stack-sql-rp-deploy/sqlrp-newplan.png)</span></span>

## <a name="tenant-usage-of-hello-resource-provider"></a><span data-ttu-id="0b855-242">Uso de inquilinos de hello proveedor de recursos</span><span class="sxs-lookup"><span data-stu-id="0b855-242">Tenant usage of hello Resource Provider</span></span>

<span data-ttu-id="0b855-243">Autoservicio de bases de datos se proporcionan a través de la experiencia del portal inquilino Hola.</span><span class="sxs-lookup"><span data-stu-id="0b855-243">Self-service databases are provided through hello tenant portal experience.</span></span>

## <a name="removing-hello-sql-adapter-resource-provider"></a><span data-ttu-id="0b855-244">Quitar Hola proveedor de recursos de adaptador de SQL</span><span class="sxs-lookup"><span data-stu-id="0b855-244">Removing hello SQL Adapter Resource Provider</span></span>

<span data-ttu-id="0b855-245">En el proveedor de recursos de orden tooremove hello, es fundamental toofirst quitar todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="0b855-245">In order tooremove hello resource provider, it is essential toofirst remove any dependencies.</span></span>

1. <span data-ttu-id="0b855-246">Asegúrese de que haya original paquete de implementación de Hola que has descargado para esta versión de Hola proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="0b855-246">Ensure you have hello original deployment package that you downloaded for this version of hello Resource Provider.</span></span>

2. <span data-ttu-id="0b855-247">Todas las bases de datos de inquilino deben eliminarse del proveedor de recursos de hello (Esto no eliminará los datos de hello).</span><span class="sxs-lookup"><span data-stu-id="0b855-247">All tenant databases must be deleted from hello resource provider (this will not delete hello data).</span></span> <span data-ttu-id="0b855-248">Esto debe realizarse por parte de inquilinos Hola por sí mismos.</span><span class="sxs-lookup"><span data-stu-id="0b855-248">This should be performed by hello tenants themselves.</span></span>

3. <span data-ttu-id="0b855-249">Administrador debe eliminar Hola hospedan servidores de hello adaptador de SQL</span><span class="sxs-lookup"><span data-stu-id="0b855-249">Administrator must delete hello hosting servers from hello SQL Adapter</span></span>

4. <span data-ttu-id="0b855-250">Administrador debe eliminar los planes que hacen referencia a Hola adaptador de SQL.</span><span class="sxs-lookup"><span data-stu-id="0b855-250">Administrator must delete any plans that reference hello SQL Adapter.</span></span>

5. <span data-ttu-id="0b855-251">Administrador debe eliminar todos los SKU y cuotas asociadas toohello adaptador de SQL.</span><span class="sxs-lookup"><span data-stu-id="0b855-251">Administrator must delete any SKUs and quotas associated toohello SQL Adapter.</span></span>

6. <span data-ttu-id="0b855-252">Vuelva a ejecutar el script de implementación de hello con hello - desinstalar parámetro, los puntos de conexión de Azure Resource Manager, DirectoryTenantID y las credenciales de cuenta de administrador del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b855-252">Rerun hello deployment script with hello -Uninstall parameter, Azure Resource Manager endpoints, DirectoryTenantID, and credentials for hello service administrator account.</span></span>



## <a name="next-steps"></a><span data-ttu-id="0b855-253">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0b855-253">Next steps</span></span>


<span data-ttu-id="0b855-254">Pruebe otros [servicios PaaS](azure-stack-tools-paas-services.md) como hello [proveedor de recursos de MySQL Server](azure-stack-mysql-resource-provider-deploy.md) hello y [proveedor de recursos de servicios de aplicaciones](azure-stack-app-service-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0b855-254">Try other [PaaS services](azure-stack-tools-paas-services.md) like hello [MySQL Server resource provider](azure-stack-mysql-resource-provider-deploy.md) and hello [App Services resource provider](azure-stack-app-service-overview.md).</span></span>
