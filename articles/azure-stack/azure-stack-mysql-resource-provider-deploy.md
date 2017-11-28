---
title: las bases de datos MySQL aaaUse como PaaS en pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo puede implementar el proveedor de recursos MySQL hello y proporcionan bases de datos de MySQL como servicio en la pila de Azure"
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
ms.openlocfilehash: 634e408eae9f3d8257a8610c60def0978ce333c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-mysql-databases-on-microsoft-azure-stack"></a><span data-ttu-id="c4551-103">Usar bases de datos MySQL en Microsoft Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c4551-103">Use MySQL databases on Microsoft Azure Stack</span></span>


<span data-ttu-id="c4551-104">Puede implementar un proveedor de recursos MySQL en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c4551-104">You can deploy a MySQL resource provider on Azure Stack.</span></span> <span data-ttu-id="c4551-105">Después de implementar el proveedor de recursos de hello, puede crear servidores MySQL Server y bases de datos mediante plantillas de implementación del Administrador de recursos de Azure y proporcionar las bases de datos de MySQL como un servicio.</span><span class="sxs-lookup"><span data-stu-id="c4551-105">After you deploy hello resource provider, you can create MySQL servers and databases through Azure Resource Manager deployment templates and provide MySQL databases as a service.</span></span> <span data-ttu-id="c4551-106">Las bases de datos MySQL, que son comunes en los sitios web, admiten muchas plataformas de sitio web.</span><span class="sxs-lookup"><span data-stu-id="c4551-106">MySQL databases, which are common on web sites, support many website platforms.</span></span> <span data-ttu-id="c4551-107">Por ejemplo, después de implementar el proveedor de recursos de hello, puede crear sitios Web de WordPress de plataforma de aplicaciones Web de Azure Hola como un complemento de servicio (PaaS) para la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="c4551-107">As an example, after you deploy hello resource provider, you can create WordPress websites from hello Azure Web Apps platform as a service (PaaS) add-on for Azure Stack.</span></span>

<span data-ttu-id="c4551-108">proveedor de MySQL toodeploy hello en un sistema que no tiene acceso a internet, puede copiar el archivo hello [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Download/sConnector-Net/mysql-connector-net-6.9.9.msi) tooa local comparte y proporcionar ese nombre de recurso compartido cuando se le solicite (ver abajo).</span><span class="sxs-lookup"><span data-stu-id="c4551-108">toodeploy hello MySQL provider on a system that does not have internet access, you can copy hello file [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Download/sConnector-Net/mysql-connector-net-6.9.9.msi) tooa local share and provide that share name when prompted (see below).</span></span> <span data-ttu-id="c4551-109">También debe instalar los módulos de Azure y Azure PowerShell de pila de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-109">You must also install hello Azure and Azure Stack PowerShell modules.</span></span>


## <a name="mysql-server-resource-provider-adapter-architecture"></a><span data-ttu-id="c4551-110">Arquitectura de adaptador del proveedor de recursos MySQL Server</span><span class="sxs-lookup"><span data-stu-id="c4551-110">MySQL Server Resource Provider Adapter architecture</span></span>

<span data-ttu-id="c4551-111">proveedor de recursos de Hola se compone de tres componentes:</span><span class="sxs-lookup"><span data-stu-id="c4551-111">hello resource provider is made up of three components:</span></span>

- <span data-ttu-id="c4551-112">**adaptador de proveedor de recursos de MySQL de Hello VM**, que es una máquina virtual de Windows ejecuta Servicios de proveedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-112">**hello MySQL resource provider adapter VM**, which is a Windows virtual machine running hello provider services.</span></span>
- <span data-ttu-id="c4551-113">**proveedor de recursos de Hello propio**, que procesa las solicitudes de aprovisionamiento y expone recursos de base de datos.</span><span class="sxs-lookup"><span data-stu-id="c4551-113">**hello resource provider itself**, which processes provisioning requests and exposes database resources.</span></span>
- <span data-ttu-id="c4551-114">**Los servidores que hospedan MySQL Server**, que proporcionan capacidad para las bases de datos, conocidos como servidores host.</span><span class="sxs-lookup"><span data-stu-id="c4551-114">**Servers that host MySQL Server**, which provide capacity for databases, called Hosting Servers.</span></span> 

<span data-ttu-id="c4551-115">Esta versión ya no crea una instancia de MySQL.</span><span class="sxs-lookup"><span data-stu-id="c4551-115">This release no longer creates a MySQL instance.</span></span> <span data-ttu-id="c4551-116">Debe crearlos y proporcionar acceso a instancias de SQL tooexternal.</span><span class="sxs-lookup"><span data-stu-id="c4551-116">You must create them and/or provide access tooexternal SQL instances.</span></span> <span data-ttu-id="c4551-117">Puede visitar hello [Galería de inicio rápido de Azure pila](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) para una plantilla de ejemplo que puede crear un servidor de MySQL para usted o descargar e implementar un servidor MySQL de hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c4551-117">You can visit hello [Azure Stack Quickstart Gallery](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) for an example template that can create a MySQL server for you or download and deploy a MySQL Server from hello Marketplace.</span></span>

## <a name="deploy-hello-resource-provider"></a><span data-ttu-id="c4551-118">Implementar el proveedor de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="c4551-118">Deploy hello resource provider</span></span>

1. <span data-ttu-id="c4551-119">Si no lo ha hecho ya, registre el kit de desarrollo y descargue Hola centro de datos de Windows Server 2016 - Eval imagen que se pueden descargar a través de administración de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c4551-119">If you have not already done so, register your development kit and download hello Windows Server 2016 Datacenter - Eval image downloadable through Marketplace Management.</span></span> <span data-ttu-id="c4551-120">También puede utilizar una secuencia de comandos toocreate un [imagen de Windows Server 2016](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span><span class="sxs-lookup"><span data-stu-id="c4551-120">You can also use a script toocreate a [Windows Server 2016 image](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span></span>

2. <span data-ttu-id="c4551-121">[Descargar archivo de los archivos binarios del proveedor de recursos de hello MySQL](https://aka.ms/azurestackmysqlrp) y extraerlo en el host de kit de desarrollo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-121">[Download hello MySQL resource provider binaries file](https://aka.ms/azurestackmysqlrp) and extract it on hello development kit host.</span></span>

3. <span data-ttu-id="c4551-122">Inicie sesión en el host de kit de desarrollo de toohello y extraer Hola directorio temporal del tooa de archivo instalador MySQL RP.</span><span class="sxs-lookup"><span data-stu-id="c4551-122">Sign in toohello development kit host, and extract hello MySQL RP installer file tooa temporary directory.</span></span>

4. <span data-ttu-id="c4551-123">certificado de raíz de Hello Azure pila se recuperan y se crea un certificado autofirmado como parte de este proceso.</span><span class="sxs-lookup"><span data-stu-id="c4551-123">hello Azure Stack root certificate is retrieved and a self-signed certificate is created as part of this process.</span></span> 

    <span data-ttu-id="c4551-124">__Opcional:__ si necesita tooprovide su propietario, preparar certificados hello y copiar el directorio local de tooa si desea toocustomize certificados hello (script de instalación toohello pasado).</span><span class="sxs-lookup"><span data-stu-id="c4551-124">__Optional:__ If you need tooprovide your own, prepare hello certificates and copy tooa local directory if you wish toocustomize hello certificates (passed toohello installation script).</span></span> <span data-ttu-id="c4551-125">Necesita Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="c4551-125">You need hello following:</span></span>

    <span data-ttu-id="c4551-126">a.</span><span class="sxs-lookup"><span data-stu-id="c4551-126">a.</span></span> <span data-ttu-id="c4551-127">Un certificado comodín para *.dbadapter.\<región\>.\<fqdn externo\>.</span><span class="sxs-lookup"><span data-stu-id="c4551-127">A wildcard certificate for *.dbadapter.\<region\>.\<external fqdn\>.</span></span> <span data-ttu-id="c4551-128">Este certificado debe ser de confianza, como podría ser emitido por una entidad de certificación (es decir, cadena Hola de confianza debe existir sin necesidad de certificados intermedios). (Un certificado de sitio solo puede utilizarse con nombre VM explícito Hola que proporcionar durante la instalación).</span><span class="sxs-lookup"><span data-stu-id="c4551-128">This certificate must be trusted, such as would be issued by a certificate authority (that is, hello chain of trust must exist without requiring intermediate certificates.) (A single site certificate can be used with hello explicit VM name you provide during install.)</span></span>

    <span data-ttu-id="c4551-129">b.</span><span class="sxs-lookup"><span data-stu-id="c4551-129">b.</span></span> <span data-ttu-id="c4551-130">certificado de raíz de Hello utilizado por hello Azure Resource Manager para la instancia de la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="c4551-130">hello root certificate used by hello Azure Resource Manager for your instance of Azure Stack.</span></span> <span data-ttu-id="c4551-131">Si no se encuentra, se recuperará el certificado de raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-131">If it is not found, hello root certificate will be retrieved.</span></span>

5. <span data-ttu-id="c4551-132">Abra un **nueva** elevados de PowerShell de la consola y cambie el directorio de toohello donde extrajo los archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-132">Open a **new** elevated PowerShell console and change toohello directory where you extracted hello files.</span></span> <span data-ttu-id="c4551-133">Usar un nuevo tooavoid problemas de ventana que pueden surgir de módulos de PowerShell incorrectos ya están cargados en el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-133">Use a new window tooavoid problems that may arise from incorrect PowerShell modules already loaded on hello system.</span></span>

6. <span data-ttu-id="c4551-134">Si ha instalado cualquier versión de Hola AzureRm o AzureStack PowerShell módulos que no sean 1.2.9 o 1.2.10, es posible que tooremove solicitada ellos u Hola instalación no continuará.</span><span class="sxs-lookup"><span data-stu-id="c4551-134">If you have installed any versions of hello AzureRm or AzureStack PowerShell modules other than 1.2.9 or 1.2.10, you will be prompted tooremove them or hello install will not proceed.</span></span> <span data-ttu-id="c4551-135">Se incluyen las versiones 1.3 o posterior.</span><span class="sxs-lookup"><span data-stu-id="c4551-135">This includes versions 1.3 or greater.</span></span>

7. <span data-ttu-id="c4551-136">Ejecute DeployMySqlProvider.ps1.</span><span class="sxs-lookup"><span data-stu-id="c4551-136">Run DeployMySqlProvider.ps1.</span></span>

<span data-ttu-id="c4551-137">Este script sigue estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c4551-137">This script performs these steps:</span></span>

* <span data-ttu-id="c4551-138">Si es necesario, descargue una versión compatible de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4551-138">If necessary, download a compatible version of Azure PowerShell.</span></span>
* <span data-ttu-id="c4551-139">Descargue Hola MySQL connector binario (Esto puede proporcionar sin conexión).</span><span class="sxs-lookup"><span data-stu-id="c4551-139">Download hello MySQL connector binary (this can be provided offline).</span></span>
* <span data-ttu-id="c4551-140">Cargar certificado de Hola y todos los demás tooan artefactos cuenta de almacenamiento de la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="c4551-140">Upload hello certificate and all other artifacts tooan Azure Stack storage account.</span></span>
* <span data-ttu-id="c4551-141">Publicar paquetes de la Galería para que pueda implementar bases de datos de MySQL a través de la Galería de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-141">Publish gallery packages so that you can deploy MySQL databases through hello gallery.</span></span>
* <span data-ttu-id="c4551-142">Implemente una máquina virtual (VM) que hospede al proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="c4551-142">Deploy a virtual machine (VM) that hosts your resource provider.</span></span>
* <span data-ttu-id="c4551-143">Registrar un registro DNS local que se asigna el proveedor de recursos de tooyour máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4551-143">Register a local DNS record that maps tooyour resource provider VM.</span></span>
* <span data-ttu-id="c4551-144">Registre el proveedor de recursos con hello Azure Resource Manager local.</span><span class="sxs-lookup"><span data-stu-id="c4551-144">Register your resource provider with hello local Azure Resource Manager.</span></span>

<span data-ttu-id="c4551-145">Especifique al menos Hola parámetros necesarios en la línea de comandos de hello, o bien, si se ejecuta sin ningún parámetro, son tooenter solicitada ellos.</span><span class="sxs-lookup"><span data-stu-id="c4551-145">Either specify at least hello required parameters on hello command line, or, if you run without any parameters, you are prompted tooenter them.</span></span> 

<span data-ttu-id="c4551-146">Este es un ejemplo que se puede ejecutar desde Hola PowerShell solicite (pero cambiar extremos de información y el portal de la cuenta de hello según sea necesario):</span><span class="sxs-lookup"><span data-stu-id="c4551-146">Here's an example you can run from hello PowerShell prompt (but change hello account information and portal endpoints as needed):</span></span>


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
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("mysqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory toohello folder where you extracted hello installation files 
# and adjust hello endpoints
<extracted file directory>\DeployMySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "MySqlRG" -VmName "MySQLRP" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass -DependencyFilesLocalPath
 ```

### <a name="deploymysqlproviderps1-parameters"></a><span data-ttu-id="c4551-147">Parámetros de DeployMySqlProvider.ps1</span><span class="sxs-lookup"><span data-stu-id="c4551-147">DeployMySqlProvider.ps1 parameters</span></span>

<span data-ttu-id="c4551-148">Puede especificar estos parámetros en la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-148">You can specify these parameters in hello command line.</span></span> <span data-ttu-id="c4551-149">Si no lo hace, o se produce un error en cualquier validación de parámetros, se le solicitará tooprovide Hola requiere los.</span><span class="sxs-lookup"><span data-stu-id="c4551-149">If you do not, or any parameter validation fails, you are prompted tooprovide hello required ones.</span></span>

| <span data-ttu-id="c4551-150">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="c4551-150">Parameter Name</span></span> | <span data-ttu-id="c4551-151">Descripción</span><span class="sxs-lookup"><span data-stu-id="c4551-151">Description</span></span> | <span data-ttu-id="c4551-152">Comentario o valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c4551-152">Comment or Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c4551-153">**DirectoryTenantID**</span><span class="sxs-lookup"><span data-stu-id="c4551-153">**DirectoryTenantID**</span></span> | <span data-ttu-id="c4551-154">Hola Azure o Id. de directorio de AD FS (guid)</span><span class="sxs-lookup"><span data-stu-id="c4551-154">hello Azure or ADFS Directory ID (guid)</span></span> | <span data-ttu-id="c4551-155">_obligatorio_</span><span class="sxs-lookup"><span data-stu-id="c4551-155">_required_</span></span> |
| <span data-ttu-id="c4551-156">**ArmEndpoint**</span><span class="sxs-lookup"><span data-stu-id="c4551-156">**ArmEndpoint**</span></span> | <span data-ttu-id="c4551-157">Hello Azure pila administrativo Administrador de recursos del extremo de Azure</span><span class="sxs-lookup"><span data-stu-id="c4551-157">hello Azure Stack Administrative Azure Resource Manager Endpoint</span></span> | <span data-ttu-id="c4551-158">_obligatorio_</span><span class="sxs-lookup"><span data-stu-id="c4551-158">_required_</span></span> |
| <span data-ttu-id="c4551-159">**TenantArmEndpoint**</span><span class="sxs-lookup"><span data-stu-id="c4551-159">**TenantArmEndpoint**</span></span> | <span data-ttu-id="c4551-160">Hello Azure pila Azure Administrador de recursos del extremo del inquilino</span><span class="sxs-lookup"><span data-stu-id="c4551-160">hello Azure Stack Tenant Azure Resource Manager Endpoint</span></span> | <span data-ttu-id="c4551-161">_obligatorio_</span><span class="sxs-lookup"><span data-stu-id="c4551-161">_required_</span></span> |
| <span data-ttu-id="c4551-162">**AzCredential**</span><span class="sxs-lookup"><span data-stu-id="c4551-162">**AzCredential**</span></span> | <span data-ttu-id="c4551-163">Credencial de la cuenta de administrador de servicios de pila Azure (Hola de uso misma cuenta que usó para la implementación de pila de Azure)</span><span class="sxs-lookup"><span data-stu-id="c4551-163">Azure Stack Service Admin account credential (use hello same account as you used for deploying Azure Stack)</span></span> | <span data-ttu-id="c4551-164">_obligatorio_</span><span class="sxs-lookup"><span data-stu-id="c4551-164">_required_</span></span> |
| <span data-ttu-id="c4551-165">**VMLocalCredential**</span><span class="sxs-lookup"><span data-stu-id="c4551-165">**VMLocalCredential**</span></span> | <span data-ttu-id="c4551-166">cuenta de administrador local de Hola de proveedor de recursos de MySQL de hello VM</span><span class="sxs-lookup"><span data-stu-id="c4551-166">hello local administrator account of hello MySQL resource provider VM</span></span> | <span data-ttu-id="c4551-167">_obligatorio_</span><span class="sxs-lookup"><span data-stu-id="c4551-167">_required_</span></span> |
| <span data-ttu-id="c4551-168">**ResourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="c4551-168">**ResourceGroupName**</span></span> | <span data-ttu-id="c4551-169">Grupo de recursos para los elementos de hello creados por esta secuencia de comandos</span><span class="sxs-lookup"><span data-stu-id="c4551-169">Resource Group for hello items created by this script</span></span> |  <span data-ttu-id="c4551-170">_obligatorio_</span><span class="sxs-lookup"><span data-stu-id="c4551-170">_required_</span></span> |
| <span data-ttu-id="c4551-171">**VmName**</span><span class="sxs-lookup"><span data-stu-id="c4551-171">**VmName**</span></span> | <span data-ttu-id="c4551-172">Nombre de explotación de VM de hello proveedor de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="c4551-172">Name of hello VM holding hello resource provider</span></span> |  <span data-ttu-id="c4551-173">_obligatorio_</span><span class="sxs-lookup"><span data-stu-id="c4551-173">_required_</span></span> |
| <span data-ttu-id="c4551-174">**AcceptLicense**</span><span class="sxs-lookup"><span data-stu-id="c4551-174">**AcceptLicense**</span></span> | <span data-ttu-id="c4551-175">Omite Hola tooaccept prompt Hola licencia de GPL (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)</span><span class="sxs-lookup"><span data-stu-id="c4551-175">Skips hello prompt tooaccept hello GPL License  (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)</span></span> | |
| <span data-ttu-id="c4551-176">**DependencyFilesLocalPath**</span><span class="sxs-lookup"><span data-stu-id="c4551-176">**DependencyFilesLocalPath**</span></span> | <span data-ttu-id="c4551-177">Recurso compartido local que contiene de ruta de acceso tooa [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi).</span><span class="sxs-lookup"><span data-stu-id="c4551-177">Path tooa local share containing [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi).</span></span> <span data-ttu-id="c4551-178">Si proporciona los archivos de certificados, se deben colocar también en este directorio.</span><span class="sxs-lookup"><span data-stu-id="c4551-178">If you provide them, certificate files must be placed in this directory as well.</span></span> | <span data-ttu-id="c4551-179">_opcional_</span><span class="sxs-lookup"><span data-stu-id="c4551-179">_optional_</span></span> |
| <span data-ttu-id="c4551-180">**DefaultSSLCertificatePassword**</span><span class="sxs-lookup"><span data-stu-id="c4551-180">**DefaultSSLCertificatePassword**</span></span> | <span data-ttu-id="c4551-181">contraseña de Hello para el archivo de certificado .pfx Hola</span><span class="sxs-lookup"><span data-stu-id="c4551-181">hello password for hello .pfx certificate</span></span> | <span data-ttu-id="c4551-182">_obligatorio_</span><span class="sxs-lookup"><span data-stu-id="c4551-182">_required_</span></span> |
| <span data-ttu-id="c4551-183">**MaxRetryCount**</span><span class="sxs-lookup"><span data-stu-id="c4551-183">**MaxRetryCount**</span></span> | <span data-ttu-id="c4551-184">Se vuelve a intentar cada operación si se produce un error.</span><span class="sxs-lookup"><span data-stu-id="c4551-184">Each operation is retried if there is a failure</span></span> | <span data-ttu-id="c4551-185">2</span><span class="sxs-lookup"><span data-stu-id="c4551-185">2</span></span> |
| <span data-ttu-id="c4551-186">**RetryDuration**</span><span class="sxs-lookup"><span data-stu-id="c4551-186">**RetryDuration**</span></span> | <span data-ttu-id="c4551-187">Tiempo de expiración entre reintentos, en segundos</span><span class="sxs-lookup"><span data-stu-id="c4551-187">Timeout between retries, in seconds</span></span> | <span data-ttu-id="c4551-188">120</span><span class="sxs-lookup"><span data-stu-id="c4551-188">120</span></span> |
| <span data-ttu-id="c4551-189">**Desinstalación**</span><span class="sxs-lookup"><span data-stu-id="c4551-189">**Uninstall**</span></span> | <span data-ttu-id="c4551-190">Quitar proveedor de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="c4551-190">Remove hello resource provider</span></span> | <span data-ttu-id="c4551-191">No</span><span class="sxs-lookup"><span data-stu-id="c4551-191">No</span></span> |
| <span data-ttu-id="c4551-192">**DebugMode**</span><span class="sxs-lookup"><span data-stu-id="c4551-192">**DebugMode**</span></span> | <span data-ttu-id="c4551-193">Impide la limpieza automática en caso de error.</span><span class="sxs-lookup"><span data-stu-id="c4551-193">Prevents automatic cleanup on failure</span></span> | <span data-ttu-id="c4551-194">No</span><span class="sxs-lookup"><span data-stu-id="c4551-194">No</span></span> |


<span data-ttu-id="c4551-195">Función de velocidades de rendimiento y descarga de sistema de hello, instalación puede tardar tan sólo como 20 minutos o como larga como varias horas.</span><span class="sxs-lookup"><span data-stu-id="c4551-195">Depending on hello system performance and download speeds, installation may take as little as 20 minutes or as long as several hours.</span></span> <span data-ttu-id="c4551-196">Debe actualizar el portal de administración de hello si hoja de hello MySQLAdapter no está disponible.</span><span class="sxs-lookup"><span data-stu-id="c4551-196">You must refresh hello admin portal if hello MySQLAdapter blade is not available.</span></span>

> [!NOTE]
> <span data-ttu-id="c4551-197">Si la instalación de hello tiene más de 90 minutos, se puede producir un error y verá un mensaje de error en la pantalla de bienvenida y en el archivo de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="c4551-197">If hello installation takes more than 90 minutes, it may fail and you will see a failure message on hello screen and in hello log file.</span></span> <span data-ttu-id="c4551-198">implementación de Hola se reintenta de hello errores paso.</span><span class="sxs-lookup"><span data-stu-id="c4551-198">hello deployment is retried from hello failing step.</span></span> <span data-ttu-id="c4551-199">Sistemas que no cumplen Hola memoria recomendada y las especificaciones principales pueden no ser capaz de toodeploy Hola MySQL RP.</span><span class="sxs-lookup"><span data-stu-id="c4551-199">Systems that do not meet hello recommended memory and core specifications may not be able toodeploy hello MySQL RP.</span></span>


## <a name="provide-capacity-by-connecting-tooa-mysql-hosting-server"></a><span data-ttu-id="c4551-200">Proporcionar una capacidad mediante la conexión de servidor de hospedaje de MySQL tooa</span><span class="sxs-lookup"><span data-stu-id="c4551-200">Provide capacity by connecting tooa MySQL hosting server</span></span>

1. <span data-ttu-id="c4551-201">Inicie sesión en toohello portal de la pila de Azure como un administrador del servicio.</span><span class="sxs-lookup"><span data-stu-id="c4551-201">Sign in toohello Azure Stack portal as a service admin.</span></span>

2. <span data-ttu-id="c4551-202">Haga clic en **Proveedores de recursos** &gt; **MySQLAdapter** &gt; **Hosting Servers** (Servidores host)&gt; **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c4551-202">Click **Resource Providers** &gt; **MySQLAdapter** &gt; **Hosting Servers** &gt; **+Add**.</span></span>

    <span data-ttu-id="c4551-203">Hola **servidores de hospedaje de MySQL** hoja es donde puede conectar Hola proveedor de recursos de MySQL Server tooactual instancias de MySQL Server que actúan como Hola back-end del proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="c4551-203">hello **MySQL Hosting Servers** blade is where you can connect hello MySQL Server Resource Provider tooactual instances of MySQL Server that serve as hello resource provider’s backend.</span></span>

    ![Servidores de hospedaje](./media/azure-stack-mysql-rp-deploy/mysql-add-hosting-server-2.png)

3. <span data-ttu-id="c4551-205">Rellenar el formulario de hello con detalles de la conexión de saludo de la instancia del servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="c4551-205">Fill hello form with hello connection details of your MySQL Server instance.</span></span> <span data-ttu-id="c4551-206">Proporcione el nombre de dominio completo (FQDN) de Hola o una dirección IPv4 válida y no Hola VM nombre corto.</span><span class="sxs-lookup"><span data-stu-id="c4551-206">Provide hello fully qualified domain name (FQDN) or a valid IPv4 address, and not hello short VM name.</span></span> <span data-ttu-id="c4551-207">Esta instalación ya no proporciona una instancia de MySQL predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c4551-207">This installation no longer provides a default MySQL instance.</span></span> <span data-ttu-id="c4551-208">Hola tamaño proporciona ayuda a proveedor de recursos de Hola a administrar la capacidad de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-208">hello size provided helps hello resource provider manage hello database capacity.</span></span> <span data-ttu-id="c4551-209">Debe ser toohello cerrar la capacidad física del servidor de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-209">It should be close toohello physical capacity of hello database server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c4551-210">Siempre que puede tener acceso a la instancia de MySQL de Hola por inquilino hello y administración de Azure Resource Manager, se puede colocar bajo el control de proveedor de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-210">As long as hello MySQL instance can be accessed by hello tenant and admin Azure Resource Manager, it can be placed under control of hello resource provider.</span></span> <span data-ttu-id="c4551-211">instancia de MySQL de Hello __debe__ asignar exclusivamente toohello RP.</span><span class="sxs-lookup"><span data-stu-id="c4551-211">hello MySQL instance __must__ be allocated exclusively toohello RP.</span></span>

4. <span data-ttu-id="c4551-212">Cuando agregue servidores, debe asignarlos tooa nueva o existente SKU tooallow diferenciación de ofertas de servicio.</span><span class="sxs-lookup"><span data-stu-id="c4551-212">As you add servers, you must assign them tooa new or existing SKU tooallow differentiation of service offerings.</span></span> <span data-ttu-id="c4551-213">Por ejemplo, podría tener una instancia de enterprise proporciona capacidad de la base de datos y copia de seguridad automática, reservar servidores de alto rendimiento para que los departamentos individuales, nombre de SKU de hello etc. debe reflejar propiedades Hola para que los inquilinos pueden colocar sus bases de datos correctamente y deben tener todos los servidores de hospedaje en una SKU hello las mismas capacidades.</span><span class="sxs-lookup"><span data-stu-id="c4551-213">For example, you could have an enterprise instance providing database capacity and automatic backup, reserve high-performance servers for individual departments, etc. hello SKU name should reflect hello properties so that tenants can place their databases appropriately and all hosting servers in a SKU should have hello same capabilities.</span></span>

    ![Crear una SKU de MySQL](./media/azure-stack-mysql-rp-deploy/mysql-new-sku.png)


>[!NOTE]
<span data-ttu-id="c4551-215">SKU pueden tardar hasta tooan hora toobe visible en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-215">SKUs can take up tooan hour toobe visible in hello portal.</span></span> <span data-ttu-id="c4551-216">No se puede crear una base de datos hasta que Hola que SKU se crea.</span><span class="sxs-lookup"><span data-stu-id="c4551-216">You cannot create a database until hello SKU is created.</span></span>


## <a name="create-your-first-mysql-database-tootest-your-deployment"></a><span data-ttu-id="c4551-217">Crear la implementación de su primera tootest de base de datos de MySQL</span><span class="sxs-lookup"><span data-stu-id="c4551-217">Create your first MySQL database tootest your deployment</span></span>


1. <span data-ttu-id="c4551-218">Inicie sesión en toohello portal de la pila de Azure como administrador del servicio.</span><span class="sxs-lookup"><span data-stu-id="c4551-218">Sign in toohello Azure Stack portal as service admin.</span></span>

2. <span data-ttu-id="c4551-219">Haga clic en hello **+ nuevo** botón &gt; **datos + almacenamiento** &gt; **(vista previa) de base de datos de MySQL**.</span><span class="sxs-lookup"><span data-stu-id="c4551-219">Click hello **+ New** button &gt; **Data + Storage** &gt; **MySQL Database (preview)**.</span></span>

3. <span data-ttu-id="c4551-220">Rellene el formulario de hello con detalles de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-220">Fill in hello form with hello database details.</span></span>

    ![Crear una base de datos MySQL de prueba](./media/azure-stack-mysql-rp-deploy/mysql-create-db.png)

4. <span data-ttu-id="c4551-222">Seleccione una SKU.</span><span class="sxs-lookup"><span data-stu-id="c4551-222">Select a SKU.</span></span>

    ![Seleccionar una SKU](./media/azure-stack-mysql-rp-deploy/mysql-select-a-sku.png)

5. <span data-ttu-id="c4551-224">Cree una configuración de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="c4551-224">Create a login setting.</span></span> <span data-ttu-id="c4551-225">se puede reutilizar la configuración de inicio de sesión de Hola o crea uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="c4551-225">hello login setting can be reused or a new one created.</span></span> <span data-ttu-id="c4551-226">Esto contiene el nombre de usuario de Hola y la contraseña de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-226">This contains hello user name and password for hello database.</span></span>

    ![Creación de un nuevo inicio de sesión en la base de datos](./media/azure-stack-mysql-rp-deploy/create-new-login.png)

    <span data-ttu-id="c4551-228">cadena de conexión de Hello incluye el nombre del servidor de base de datos reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-228">hello connections string includes hello real database server name.</span></span> <span data-ttu-id="c4551-229">Copiarlo desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-229">Copy it from hello portal.</span></span>

    ![Obtener la cadena de conexión de hello para la base de datos de MySQL Hola](./media/azure-stack-mysql-rp-deploy/mysql-db-created.png)

> [!NOTE]
> <span data-ttu-id="c4551-231">longitud de Hola Hola de nombres de usuario no puede superar los 32 caracteres con MySQL 5.7 o en versiones anteriores de 16 caracteres.</span><span class="sxs-lookup"><span data-stu-id="c4551-231">hello length of hello user names cannot exceed 32 characters with MySQL 5.7 or 16 characters in earlier editions.</span></span> <span data-ttu-id="c4551-232">Se trata de una limitación de las implementaciones de MySQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-232">This is a limitation of hello MySQL implementations.</span></span>


## <a name="add-capacity"></a><span data-ttu-id="c4551-233">Ampliación de capacidad</span><span class="sxs-lookup"><span data-stu-id="c4551-233">Add capacity</span></span>

<span data-ttu-id="c4551-234">Agregar más capacidad al agregar más servidores de MySQL en el portal de Azure pila Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-234">Add capacity by adding additional MySQL servers in hello Azure Stack portal.</span></span> <span data-ttu-id="c4551-235">Si desea toouse otra instancia de MySQL, haga clic en **proveedores de recursos** &gt; **MySQLAdapter** &gt; **servidores de hospedaje de MySQL** &gt; **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c4551-235">If you wish toouse another instance of MySQL, click **Resource Providers** &gt; **MySQLAdapter** &gt; **MySQL Hosting Servers** &gt; **+Add**.</span></span>


## <a name="making-mysql-databases-available-tootenants"></a><span data-ttu-id="c4551-236">Hacer que las bases de datos de MySQL tootenants disponibles</span><span class="sxs-lookup"><span data-stu-id="c4551-236">Making MySQL databases available tootenants</span></span>
<span data-ttu-id="c4551-237">Crear planes y ofertas toomake bases de datos de MySQL disponibles para los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="c4551-237">Create plans and offers toomake MySQL databases available for tenants.</span></span> <span data-ttu-id="c4551-238">Agregar servicio de hello Microsoft.MySqlAdapter, agregue una cuota, etcetera.</span><span class="sxs-lookup"><span data-stu-id="c4551-238">Add hello Microsoft.MySqlAdapter service, add a quota, etc.</span></span>

![Crear planes y ofertas tooinclude bases de datos](./media/azure-stack-mysql-rp-deploy/mysql-new-plan.png)

## <a name="removing-hello-mysql-adapter-resource-provider"></a><span data-ttu-id="c4551-240">Quitar Hola proveedor de recursos de adaptador de MySQL</span><span class="sxs-lookup"><span data-stu-id="c4551-240">Removing hello MySQL Adapter Resource Provider</span></span>

<span data-ttu-id="c4551-241">proveedor de recursos de tooremove hello, es esencial toofirst quitar todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="c4551-241">tooremove hello resource provider, it is essential toofirst remove any dependencies.</span></span>

1. <span data-ttu-id="c4551-242">Asegúrese de que haya original paquete de implementación de Hola que has descargado para esta versión de Hola proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="c4551-242">Ensure you have hello original deployment package that you downloaded for this version of hello Resource Provider.</span></span>

2. <span data-ttu-id="c4551-243">Todas las bases de datos de inquilino deben eliminarse del proveedor de recursos de hello (Esto no eliminará los datos de hello).</span><span class="sxs-lookup"><span data-stu-id="c4551-243">All tenant databases must be deleted from hello resource provider (this will not delete hello data).</span></span> <span data-ttu-id="c4551-244">Esto debe realizarse por parte de inquilinos Hola por sí mismos.</span><span class="sxs-lookup"><span data-stu-id="c4551-244">This should be performed by hello tenants themselves.</span></span>

3. <span data-ttu-id="c4551-245">Deben anular el registro de los inquilinos del espacio de nombres de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-245">Tenants must unregister from hello namespace.</span></span>

4. <span data-ttu-id="c4551-246">Administrador debe eliminar Hola servidores de MySQL adaptador Hola de hospedaje</span><span class="sxs-lookup"><span data-stu-id="c4551-246">Administrator must delete hello hosting servers from hello MySQL Adapter</span></span>

5. <span data-ttu-id="c4551-247">Administrador debe eliminar los planes que hacen referencia a Hola adaptador de MySQL.</span><span class="sxs-lookup"><span data-stu-id="c4551-247">Administrator must delete any plans that reference hello MySQL Adapter.</span></span>

6. <span data-ttu-id="c4551-248">Administrador debe eliminar cualquier toohello asociado el adaptador de MySQL de cuotas.</span><span class="sxs-lookup"><span data-stu-id="c4551-248">Administrator must delete any quotas associated toohello MySQL Adapter.</span></span>

7. <span data-ttu-id="c4551-249">Vuelva a ejecutar el script de implementación de hello con hello - desinstalar parámetro, los puntos de conexión de Azure Resource Manager, DirectoryTenantID y las credenciales de cuenta de administrador del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4551-249">Rerun hello deployment script with hello -Uninstall parameter, Azure Resource Manager endpoints, DirectoryTenantID, and credentials for hello service administrator account.</span></span>




## <a name="next-steps"></a><span data-ttu-id="c4551-250">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c4551-250">Next steps</span></span>


<span data-ttu-id="c4551-251">Pruebe otros [servicios PaaS](azure-stack-tools-paas-services.md) como hello [proveedor de recursos de SQL Server](azure-stack-sql-resource-provider-deploy.md) hello y [proveedor de recursos de servicios de aplicaciones](azure-stack-app-service-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c4551-251">Try other [PaaS services](azure-stack-tools-paas-services.md) like hello [SQL Server resource provider](azure-stack-sql-resource-provider-deploy.md) and hello [App Services resource provider](azure-stack-app-service-overview.md).</span></span>
