---
title: Usar bases de datos MySQL como PaaS en Azure Stack | Microsoft Docs
description: "Aprenda cómo puede implementar el proveedor de recursos de MySQL y proporcionar bases de datos MySQL como servicio en Azure Stack"
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
ms.openlocfilehash: 4e9da524ef9dfa2d5b7150bc6a888536a1435dfd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-mysql-databases-on-microsoft-azure-stack"></a><span data-ttu-id="f5d78-103">Usar bases de datos MySQL en Microsoft Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f5d78-103">Use MySQL databases on Microsoft Azure Stack</span></span>


<span data-ttu-id="f5d78-104">Puede implementar un proveedor de recursos MySQL en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f5d78-104">You can deploy a MySQL resource provider on Azure Stack.</span></span> <span data-ttu-id="f5d78-105">Después de implementar el proveedor de recursos, puede crear servidores y bases de datos MySQL mediante plantillas de implementación de Azure Resource Manager y proporcionar las bases de datos MySQL como servicio.</span><span class="sxs-lookup"><span data-stu-id="f5d78-105">After you deploy the resource provider, you can create MySQL servers and databases through Azure Resource Manager deployment templates and provide MySQL databases as a service.</span></span> <span data-ttu-id="f5d78-106">Las bases de datos MySQL, que son comunes en los sitios web, admiten muchas plataformas de sitio web.</span><span class="sxs-lookup"><span data-stu-id="f5d78-106">MySQL databases, which are common on web sites, support many website platforms.</span></span> <span data-ttu-id="f5d78-107">Por ejemplo, después de implementar el proveedor de recursos, puede crear sitios web de WordPress desde el complemento de plataforma como servicio (PaaS) Azure Web Apps para Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f5d78-107">As an example, after you deploy the resource provider, you can create WordPress websites from the Azure Web Apps platform as a service (PaaS) add-on for Azure Stack.</span></span>

<span data-ttu-id="f5d78-108">Para implementar el proveedor de MySQL en un sistema que no tiene acceso a Internet, puede copiar el archivo [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Download/sConnector-Net/mysql-connector-net-6.9.9.msi) a un recurso compartido local y proporcionar ese nombre de recurso compartido cuando se le solicite (consulte la información que encontrará a continuación).</span><span class="sxs-lookup"><span data-stu-id="f5d78-108">To deploy the MySQL provider on a system that does not have internet access, you can copy the file [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Download/sConnector-Net/mysql-connector-net-6.9.9.msi) to a local share and provide that share name when prompted (see below).</span></span> <span data-ttu-id="f5d78-109">También debe instalar los módulos PowerShell de Azure y Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f5d78-109">You must also install the Azure and Azure Stack PowerShell modules.</span></span>


## <a name="mysql-server-resource-provider-adapter-architecture"></a><span data-ttu-id="f5d78-110">Arquitectura de adaptador del proveedor de recursos MySQL Server</span><span class="sxs-lookup"><span data-stu-id="f5d78-110">MySQL Server Resource Provider Adapter architecture</span></span>

<span data-ttu-id="f5d78-111">El proveedor de recursos se compone de tres componentes:</span><span class="sxs-lookup"><span data-stu-id="f5d78-111">The resource provider is made up of three components:</span></span>

- <span data-ttu-id="f5d78-112">**La VM de adaptador del proveedor de recursos MySQL**, que es una máquina virtual con Windows que ejecuta los servicios del proveedor.</span><span class="sxs-lookup"><span data-stu-id="f5d78-112">**The MySQL resource provider adapter VM**, which is a Windows virtual machine running the provider services.</span></span>
- <span data-ttu-id="f5d78-113">**El proveedor de recursos en sí**, que procesa las solicitudes de aprovisionamiento y expone los recursos de las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="f5d78-113">**The resource provider itself**, which processes provisioning requests and exposes database resources.</span></span>
- <span data-ttu-id="f5d78-114">**Los servidores que hospedan MySQL Server**, que proporcionan capacidad para las bases de datos, conocidos como servidores host.</span><span class="sxs-lookup"><span data-stu-id="f5d78-114">**Servers that host MySQL Server**, which provide capacity for databases, called Hosting Servers.</span></span> 

<span data-ttu-id="f5d78-115">Esta versión ya no crea una instancia de MySQL.</span><span class="sxs-lookup"><span data-stu-id="f5d78-115">This release no longer creates a MySQL instance.</span></span> <span data-ttu-id="f5d78-116">Debe crearlas o proporcionar acceso a instancias externas de SQL.</span><span class="sxs-lookup"><span data-stu-id="f5d78-116">You must create them and/or provide access to external SQL instances.</span></span> <span data-ttu-id="f5d78-117">Puede visitar la [galería de inicio rápido de Azure Stack](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) para ver una plantilla de ejemplo que puede crear un servidor MySQL por usted, o puede descargar e implementar un servidor MySQL Server de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f5d78-117">You can visit the [Azure Stack Quickstart Gallery](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) for an example template that can create a MySQL server for you or download and deploy a MySQL Server from the Marketplace.</span></span>

## <a name="deploy-the-resource-provider"></a><span data-ttu-id="f5d78-118">Implementar el proveedor de recursos</span><span class="sxs-lookup"><span data-stu-id="f5d78-118">Deploy the resource provider</span></span>

1. <span data-ttu-id="f5d78-119">Si no lo ha hecho ya, registre el kit de desarrollo y descargue la imagen de Windows Server 2016 Datacenter - Eval, que puede descargarse desde la administración de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f5d78-119">If you have not already done so, register your development kit and download the Windows Server 2016 Datacenter - Eval image downloadable through Marketplace Management.</span></span> <span data-ttu-id="f5d78-120">También puede usar un script para crear una [imagen de Windows Server 2016](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span><span class="sxs-lookup"><span data-stu-id="f5d78-120">You can also use a script to create a [Windows Server 2016 image](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span></span>

2. <span data-ttu-id="f5d78-121">[Descargue el archivo de binarios del proveedor de recursos MySQL](https://aka.ms/azurestackmysqlrp) y extráigalo en el host del kit de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="f5d78-121">[Download the MySQL resource provider binaries file](https://aka.ms/azurestackmysqlrp) and extract it on the development kit host.</span></span>

3. <span data-ttu-id="f5d78-122">Inicie sesión en el host del kit de desarrollo y extraiga el archivo de instalador del RP MySQL en un directorio temporal.</span><span class="sxs-lookup"><span data-stu-id="f5d78-122">Sign in to the development kit host, and extract the MySQL RP installer file to a temporary directory.</span></span>

4. <span data-ttu-id="f5d78-123">Se recupera el certificado raíz de Azure Stack, y se crea un certificado autofirmado como parte de este proceso.</span><span class="sxs-lookup"><span data-stu-id="f5d78-123">The Azure Stack root certificate is retrieved and a self-signed certificate is created as part of this process.</span></span> 

    <span data-ttu-id="f5d78-124">__Opcional:__ Si tiene que proporcionar los propios, prepare los certificados y cópielos a un directorio local si quiere personalizar los certificados (que se pasan al script de instalación).</span><span class="sxs-lookup"><span data-stu-id="f5d78-124">__Optional:__ If you need to provide your own, prepare the certificates and copy to a local directory if you wish to customize the certificates (passed to the installation script).</span></span> <span data-ttu-id="f5d78-125">Necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f5d78-125">You need the following:</span></span>

    <span data-ttu-id="f5d78-126">a.</span><span class="sxs-lookup"><span data-stu-id="f5d78-126">a.</span></span> <span data-ttu-id="f5d78-127">Un certificado comodín para *.dbadapter.\<región\>.\<fqdn externo\>.</span><span class="sxs-lookup"><span data-stu-id="f5d78-127">A wildcard certificate for *.dbadapter.\<region\>.\<external fqdn\>.</span></span> <span data-ttu-id="f5d78-128">Este certificado debe ser de confianza, como podría ser uno emitido por una entidad de certificación (es decir, la cadena de confianza debe existir sin necesidad de certificados intermedios). (Puede usarse un único certificado de sitio con el nombre explícito de VM que proporcione durante la instalación.)</span><span class="sxs-lookup"><span data-stu-id="f5d78-128">This certificate must be trusted, such as would be issued by a certificate authority (that is, the chain of trust must exist without requiring intermediate certificates.) (A single site certificate can be used with the explicit VM name you provide during install.)</span></span>

    <span data-ttu-id="f5d78-129">b.</span><span class="sxs-lookup"><span data-stu-id="f5d78-129">b.</span></span> <span data-ttu-id="f5d78-130">El certificado raíz utilizado por Azure Resource Manager para la instancia de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f5d78-130">The root certificate used by the Azure Resource Manager for your instance of Azure Stack.</span></span> <span data-ttu-id="f5d78-131">Si no se encuentra, se recuperará el certificado raíz.</span><span class="sxs-lookup"><span data-stu-id="f5d78-131">If it is not found, the root certificate will be retrieved.</span></span>

5. <span data-ttu-id="f5d78-132">Abra una **nueva** consola de PowerShell con privilegios elevados y cambie al directorio al que extrajo los archivos.</span><span class="sxs-lookup"><span data-stu-id="f5d78-132">Open a **new** elevated PowerShell console and change to the directory where you extracted the files.</span></span> <span data-ttu-id="f5d78-133">Use una nueva ventana para evitar problemas que puedan surgir de los módulos de PowerShell incorrectos que ya están cargados en el sistema.</span><span class="sxs-lookup"><span data-stu-id="f5d78-133">Use a new window to avoid problems that may arise from incorrect PowerShell modules already loaded on the system.</span></span>

6. <span data-ttu-id="f5d78-134">Si ha instalado alguna de las versiones de los módulos de AzureRm o AzureStack PowerShell que no sean 1.2.9 o 1.2.10, deberá quitarlas. De lo contrario, la instalación no continuará.</span><span class="sxs-lookup"><span data-stu-id="f5d78-134">If you have installed any versions of the AzureRm or AzureStack PowerShell modules other than 1.2.9 or 1.2.10, you will be prompted to remove them or the install will not proceed.</span></span> <span data-ttu-id="f5d78-135">Esto incluye las versiones 1.3 o posterior.</span><span class="sxs-lookup"><span data-stu-id="f5d78-135">This includes versions 1.3 or greater.</span></span>

7. <span data-ttu-id="f5d78-136">Ejecute DeployMySqlProvider.ps1.</span><span class="sxs-lookup"><span data-stu-id="f5d78-136">Run DeployMySqlProvider.ps1.</span></span>

<span data-ttu-id="f5d78-137">Este script sigue estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f5d78-137">This script performs these steps:</span></span>

* <span data-ttu-id="f5d78-138">Si es necesario, descargue una versión compatible de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f5d78-138">If necessary, download a compatible version of Azure PowerShell.</span></span>
* <span data-ttu-id="f5d78-139">Descargue el archivo binario del conector de MySQL (puede proporcionarse sin conexión).</span><span class="sxs-lookup"><span data-stu-id="f5d78-139">Download the MySQL connector binary (this can be provided offline).</span></span>
* <span data-ttu-id="f5d78-140">Cargue el certificado y todos los demás artefactos en una cuenta de almacenamiento de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f5d78-140">Upload the certificate and all other artifacts to an Azure Stack storage account.</span></span>
* <span data-ttu-id="f5d78-141">Publique los paquetes de la galería para poder implementar las bases de datos MySQL a través de la galería.</span><span class="sxs-lookup"><span data-stu-id="f5d78-141">Publish gallery packages so that you can deploy MySQL databases through the gallery.</span></span>
* <span data-ttu-id="f5d78-142">Implemente una máquina virtual (VM) que hospede al proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="f5d78-142">Deploy a virtual machine (VM) that hosts your resource provider.</span></span>
* <span data-ttu-id="f5d78-143">Registre un registro de DNS local que se asigne a la VM del proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="f5d78-143">Register a local DNS record that maps to your resource provider VM.</span></span>
* <span data-ttu-id="f5d78-144">Registre el proveedor de recursos en Azure Resource Manager local.</span><span class="sxs-lookup"><span data-stu-id="f5d78-144">Register your resource provider with the local Azure Resource Manager.</span></span>

<span data-ttu-id="f5d78-145">Especifique al menos los parámetros obligatorios en la línea de comandos o, si ejecuta sin ningún parámetro, se le pedirá que los escriba.</span><span class="sxs-lookup"><span data-stu-id="f5d78-145">Either specify at least the required parameters on the command line, or, if you run without any parameters, you are prompted to enter them.</span></span> 

<span data-ttu-id="f5d78-146">Este es un ejemplo que puede ejecutar desde el símbolo del sistema de PowerShell (pero cambie la información de la cuenta y los puntos de conexión del portal según sea necesario):</span><span class="sxs-lookup"><span data-stu-id="f5d78-146">Here's an example you can run from the PowerShell prompt (but change the account information and portal endpoints as needed):</span></span>


```
# Install the AzureRM.Bootstrapper module
Install-Module -Name AzureRm.BootStrapper -Force

# Installs and imports the API Version Profile required by Azure Stack into the current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile
Install-Module -Name AzureStack -RequiredVersion 1.2.10 -Force

# Download the Azure Stack Tools from GitHub and set the environment
cd c:\
Invoke-Webrequest https://github.com/Azure/AzureStack-Tools/archive/master.zip -OutFile master.zip
Expand-Archive master.zip -DestinationPath . -Force

# This endpoint may be different for your installation
Import-Module C:\AzureStack-Tools-master\Connect\AzureStack.Connect.psm1
Add-AzureRmEnvironment -Name AzureStackAdmin -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

# For AAD, use the following
$tenantID = Get-AzsDirectoryTenantID -AADTenantName "<your directory name>" -EnvironmentName AzureStackAdmin

# For ADFS, replace the previous line with
# $tenantID = Get-AzsDirectoryTenantID -ADFS -EnvironmentName AzureStackAdmin

$vmLocalAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("mysqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory to the folder where you extracted the installation files 
# and adjust the endpoints
<extracted file directory>\DeployMySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "MySqlRG" -VmName "MySQLRP" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass -DependencyFilesLocalPath
 ```

### <a name="deploymysqlproviderps1-parameters"></a><span data-ttu-id="f5d78-147">Parámetros de DeployMySqlProvider.ps1</span><span class="sxs-lookup"><span data-stu-id="f5d78-147">DeployMySqlProvider.ps1 parameters</span></span>

<span data-ttu-id="f5d78-148">Puede especificar estos parámetros en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="f5d78-148">You can specify these parameters in the command line.</span></span> <span data-ttu-id="f5d78-149">Si no lo hace, o se produce un error en la validación de algún parámetro, se le pide que proporcione los requeridos.</span><span class="sxs-lookup"><span data-stu-id="f5d78-149">If you do not, or any parameter validation fails, you are prompted to provide the required ones.</span></span>

| <span data-ttu-id="f5d78-150">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="f5d78-150">Parameter Name</span></span> | <span data-ttu-id="f5d78-151">Descripción</span><span class="sxs-lookup"><span data-stu-id="f5d78-151">Description</span></span> | <span data-ttu-id="f5d78-152">Comentario o valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="f5d78-152">Comment or Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5d78-153">**DirectoryTenantID**</span><span class="sxs-lookup"><span data-stu-id="f5d78-153">**DirectoryTenantID**</span></span> | <span data-ttu-id="f5d78-154">El identificador (GUID) de directorio de AD FS o Azure</span><span class="sxs-lookup"><span data-stu-id="f5d78-154">The Azure or ADFS Directory ID (guid)</span></span> | <span data-ttu-id="f5d78-155">_obligatorio_</span><span class="sxs-lookup"><span data-stu-id="f5d78-155">_required_</span></span> |
| <span data-ttu-id="f5d78-156">**ArmEndpoint**</span><span class="sxs-lookup"><span data-stu-id="f5d78-156">**ArmEndpoint**</span></span> | <span data-ttu-id="f5d78-157">El punto de conexión administrativo de Azure Resource Manager de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f5d78-157">The Azure Stack Administrative Azure Resource Manager Endpoint</span></span> | <span data-ttu-id="f5d78-158">_obligatorio_</span><span class="sxs-lookup"><span data-stu-id="f5d78-158">_required_</span></span> |
| <span data-ttu-id="f5d78-159">**TenantArmEndpoint**</span><span class="sxs-lookup"><span data-stu-id="f5d78-159">**TenantArmEndpoint**</span></span> | <span data-ttu-id="f5d78-160">El punto de conexión de inquilino de Azure Resource Manager de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f5d78-160">The Azure Stack Tenant Azure Resource Manager Endpoint</span></span> | <span data-ttu-id="f5d78-161">_obligatorio_</span><span class="sxs-lookup"><span data-stu-id="f5d78-161">_required_</span></span> |
| <span data-ttu-id="f5d78-162">**AzCredential**</span><span class="sxs-lookup"><span data-stu-id="f5d78-162">**AzCredential**</span></span> | <span data-ttu-id="f5d78-163">Credencial de la cuenta de administrador de servicios de Azure Stack (use la misma cuenta que usó para implementar Azure Stack)</span><span class="sxs-lookup"><span data-stu-id="f5d78-163">Azure Stack Service Admin account credential (use the same account as you used for deploying Azure Stack)</span></span> | <span data-ttu-id="f5d78-164">_obligatorio_</span><span class="sxs-lookup"><span data-stu-id="f5d78-164">_required_</span></span> |
| <span data-ttu-id="f5d78-165">**VMLocalCredential**</span><span class="sxs-lookup"><span data-stu-id="f5d78-165">**VMLocalCredential**</span></span> | <span data-ttu-id="f5d78-166">La cuenta de administrador local de la VM del proveedor de recursos MySQL</span><span class="sxs-lookup"><span data-stu-id="f5d78-166">The local administrator account of the MySQL resource provider VM</span></span> | <span data-ttu-id="f5d78-167">_obligatorio_</span><span class="sxs-lookup"><span data-stu-id="f5d78-167">_required_</span></span> |
| <span data-ttu-id="f5d78-168">**ResourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="f5d78-168">**ResourceGroupName**</span></span> | <span data-ttu-id="f5d78-169">Grupo de recursos para los elementos creados por este script</span><span class="sxs-lookup"><span data-stu-id="f5d78-169">Resource Group for the items created by this script</span></span> |  <span data-ttu-id="f5d78-170">_obligatorio_</span><span class="sxs-lookup"><span data-stu-id="f5d78-170">_required_</span></span> |
| <span data-ttu-id="f5d78-171">**VmName**</span><span class="sxs-lookup"><span data-stu-id="f5d78-171">**VmName**</span></span> | <span data-ttu-id="f5d78-172">Nombre de la VM que contiene el proveedor de recursos</span><span class="sxs-lookup"><span data-stu-id="f5d78-172">Name of the VM holding the resource provider</span></span> |  <span data-ttu-id="f5d78-173">_obligatorio_</span><span class="sxs-lookup"><span data-stu-id="f5d78-173">_required_</span></span> |
| <span data-ttu-id="f5d78-174">**AcceptLicense**</span><span class="sxs-lookup"><span data-stu-id="f5d78-174">**AcceptLicense**</span></span> | <span data-ttu-id="f5d78-175">Omite el símbolo del sistema para aceptar la licencia de GPL (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)</span><span class="sxs-lookup"><span data-stu-id="f5d78-175">Skips the prompt to accept the GPL License  (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)</span></span> | |
| <span data-ttu-id="f5d78-176">**DependencyFilesLocalPath**</span><span class="sxs-lookup"><span data-stu-id="f5d78-176">**DependencyFilesLocalPath**</span></span> | <span data-ttu-id="f5d78-177">Ruta de acceso a un recurso compartido local que contiene [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi).</span><span class="sxs-lookup"><span data-stu-id="f5d78-177">Path to a local share containing [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi).</span></span> <span data-ttu-id="f5d78-178">Si proporciona los archivos de certificados, se deben colocar también en este directorio.</span><span class="sxs-lookup"><span data-stu-id="f5d78-178">If you provide them, certificate files must be placed in this directory as well.</span></span> | <span data-ttu-id="f5d78-179">_opcional_</span><span class="sxs-lookup"><span data-stu-id="f5d78-179">_optional_</span></span> |
| <span data-ttu-id="f5d78-180">**DefaultSSLCertificatePassword**</span><span class="sxs-lookup"><span data-stu-id="f5d78-180">**DefaultSSLCertificatePassword**</span></span> | <span data-ttu-id="f5d78-181">La contraseña para el certificado .pfx</span><span class="sxs-lookup"><span data-stu-id="f5d78-181">The password for the .pfx certificate</span></span> | <span data-ttu-id="f5d78-182">_requerido_</span><span class="sxs-lookup"><span data-stu-id="f5d78-182">_required_</span></span> |
| <span data-ttu-id="f5d78-183">**MaxRetryCount**</span><span class="sxs-lookup"><span data-stu-id="f5d78-183">**MaxRetryCount**</span></span> | <span data-ttu-id="f5d78-184">Se vuelve a intentar cada operación si se produce un error.</span><span class="sxs-lookup"><span data-stu-id="f5d78-184">Each operation is retried if there is a failure</span></span> | <span data-ttu-id="f5d78-185">2</span><span class="sxs-lookup"><span data-stu-id="f5d78-185">2</span></span> |
| <span data-ttu-id="f5d78-186">**RetryDuration**</span><span class="sxs-lookup"><span data-stu-id="f5d78-186">**RetryDuration**</span></span> | <span data-ttu-id="f5d78-187">Tiempo de expiración entre reintentos, en segundos</span><span class="sxs-lookup"><span data-stu-id="f5d78-187">Timeout between retries, in seconds</span></span> | <span data-ttu-id="f5d78-188">120</span><span class="sxs-lookup"><span data-stu-id="f5d78-188">120</span></span> |
| <span data-ttu-id="f5d78-189">**Desinstalación**</span><span class="sxs-lookup"><span data-stu-id="f5d78-189">**Uninstall**</span></span> | <span data-ttu-id="f5d78-190">Quita el proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="f5d78-190">Remove the resource provider</span></span> | <span data-ttu-id="f5d78-191">No</span><span class="sxs-lookup"><span data-stu-id="f5d78-191">No</span></span> |
| <span data-ttu-id="f5d78-192">**DebugMode**</span><span class="sxs-lookup"><span data-stu-id="f5d78-192">**DebugMode**</span></span> | <span data-ttu-id="f5d78-193">Impide la limpieza automática en caso de error.</span><span class="sxs-lookup"><span data-stu-id="f5d78-193">Prevents automatic cleanup on failure</span></span> | <span data-ttu-id="f5d78-194">No</span><span class="sxs-lookup"><span data-stu-id="f5d78-194">No</span></span> |


<span data-ttu-id="f5d78-195">Dependiendo del rendimiento del sistema y de las velocidades de descarga, la instalación puede tardar tan solo 20 minutos o hasta varias horas.</span><span class="sxs-lookup"><span data-stu-id="f5d78-195">Depending on the system performance and download speeds, installation may take as little as 20 minutes or as long as several hours.</span></span> <span data-ttu-id="f5d78-196">Debe actualizar el portal de administración si la hoja MySQLAdapter no está disponible.</span><span class="sxs-lookup"><span data-stu-id="f5d78-196">You must refresh the admin portal if the MySQLAdapter blade is not available.</span></span>

> [!NOTE]
> <span data-ttu-id="f5d78-197">Si la instalación tarda más de 90 minutos, se puede producir un error y verá un mensaje de error en la pantalla y en el archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="f5d78-197">If the installation takes more than 90 minutes, it may fail and you will see a failure message on the screen and in the log file.</span></span> <span data-ttu-id="f5d78-198">Se vuelve a intentar la implementación desde el paso que da error.</span><span class="sxs-lookup"><span data-stu-id="f5d78-198">The deployment is retried from the failing step.</span></span> <span data-ttu-id="f5d78-199">Es posible que los sistemas que no cumplan las especificaciones recomendadas de memoria y núcleos no puedan implementar el RP MySQL.</span><span class="sxs-lookup"><span data-stu-id="f5d78-199">Systems that do not meet the recommended memory and core specifications may not be able to deploy the MySQL RP.</span></span>


## <a name="provide-capacity-by-connecting-to-a-mysql-hosting-server"></a><span data-ttu-id="f5d78-200">Proporcionar capacidad conectando con un servidor host MySQL</span><span class="sxs-lookup"><span data-stu-id="f5d78-200">Provide capacity by connecting to a MySQL hosting server</span></span>

1. <span data-ttu-id="f5d78-201">Inicie sesión en el portal de Azure Stack como administrador de servicios.</span><span class="sxs-lookup"><span data-stu-id="f5d78-201">Sign in to the Azure Stack portal as a service admin.</span></span>

2. <span data-ttu-id="f5d78-202">Haga clic en **Proveedores de recursos** &gt; **MySQLAdapter** &gt; **Hosting Servers** (Servidores host)&gt; **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f5d78-202">Click **Resource Providers** &gt; **MySQLAdapter** &gt; **Hosting Servers** &gt; **+Add**.</span></span>

    <span data-ttu-id="f5d78-203">En la hoja **MySQL Hosting Servers** (Servidores host de MySQL) puede conectar el proveedor de recursos del servidor MySQL a instancias reales de MySQL Server que actúan como back-end del proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="f5d78-203">The **MySQL Hosting Servers** blade is where you can connect the MySQL Server Resource Provider to actual instances of MySQL Server that serve as the resource provider’s backend.</span></span>

    ![Servidores host](./media/azure-stack-mysql-rp-deploy/mysql-add-hosting-server-2.png)

3. <span data-ttu-id="f5d78-205">Rellene el formulario con los detalles de conexión de la instancia de MySQL Server.</span><span class="sxs-lookup"><span data-stu-id="f5d78-205">Fill the form with the connection details of your MySQL Server instance.</span></span> <span data-ttu-id="f5d78-206">Proporcione el nombre de dominio completo (FQDN) o una dirección IPv4 válida, y no el nombre corto de la VM.</span><span class="sxs-lookup"><span data-stu-id="f5d78-206">Provide the fully qualified domain name (FQDN) or a valid IPv4 address, and not the short VM name.</span></span> <span data-ttu-id="f5d78-207">Esta instalación ya no proporciona una instancia de MySQL predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f5d78-207">This installation no longer provides a default MySQL instance.</span></span> <span data-ttu-id="f5d78-208">El tamaño especificado ayuda al proveedor de recursos a administrar la capacidad de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f5d78-208">The size provided helps the resource provider manage the database capacity.</span></span> <span data-ttu-id="f5d78-209">Debe ser similar a la capacidad física del servidor de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="f5d78-209">It should be close to the physical capacity of the database server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f5d78-210">Siempre que Azure Resource Manager del inquilino y del administrador tenga acceso a la instancia de MySQL, puede ponerse bajo el control del proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="f5d78-210">As long as the MySQL instance can be accessed by the tenant and admin Azure Resource Manager, it can be placed under control of the resource provider.</span></span> <span data-ttu-id="f5d78-211">La instancia de MySQL __debe__ asignase exclusivamente al RP.</span><span class="sxs-lookup"><span data-stu-id="f5d78-211">The MySQL instance __must__ be allocated exclusively to the RP.</span></span>

4. <span data-ttu-id="f5d78-212">A medida que agregue servidores, debe asignarlos a una SKU nueva o existente para permitir la diferenciación de las ofertas de servicio.</span><span class="sxs-lookup"><span data-stu-id="f5d78-212">As you add servers, you must assign them to a new or existing SKU to allow differentiation of service offerings.</span></span> <span data-ttu-id="f5d78-213">Por ejemplo, podría tener una instancia empresarial que proporcione capacidad de base de datos y copia de seguridad automática, reservar servidores de alto rendimiento para departamentos individuales, etc. El nombre de la SKU debe reflejar las propiedades para que los inquilinos puedan colocar sus bases de datos correctamente, y todos los servidores host en una SKU deben tener la misma funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="f5d78-213">For example, you could have an enterprise instance providing database capacity and automatic backup, reserve high-performance servers for individual departments, etc. The SKU name should reflect the properties so that tenants can place their databases appropriately and all hosting servers in a SKU should have the same capabilities.</span></span>

    ![Crear una SKU de MySQL](./media/azure-stack-mysql-rp-deploy/mysql-new-sku.png)


>[!NOTE]
<span data-ttu-id="f5d78-215">Las SKU pueden tardar hasta una hora en estar visibles en el portal.</span><span class="sxs-lookup"><span data-stu-id="f5d78-215">SKUs can take up to an hour to be visible in the portal.</span></span> <span data-ttu-id="f5d78-216">No puede crear una base de datos hasta que se cree la SKU.</span><span class="sxs-lookup"><span data-stu-id="f5d78-216">You cannot create a database until the SKU is created.</span></span>


## <a name="create-your-first-mysql-database-to-test-your-deployment"></a><span data-ttu-id="f5d78-217">Crear la primera base de datos MySQL para probar la implementación</span><span class="sxs-lookup"><span data-stu-id="f5d78-217">Create your first MySQL database to test your deployment</span></span>


1. <span data-ttu-id="f5d78-218">Inicie sesión en el portal de Azure Stack como administrador de servicios.</span><span class="sxs-lookup"><span data-stu-id="f5d78-218">Sign in to the Azure Stack portal as service admin.</span></span>

2. <span data-ttu-id="f5d78-219">Haga clic en el botón **+ Nuevo** &gt; **Data + Storage** (Datos y almacenamiento)&gt; **Base de datos MySQL (versión preliminar)**.</span><span class="sxs-lookup"><span data-stu-id="f5d78-219">Click the **+ New** button &gt; **Data + Storage** &gt; **MySQL Database (preview)**.</span></span>

3. <span data-ttu-id="f5d78-220">Rellene el formulario con los detalles de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f5d78-220">Fill in the form with the database details.</span></span>

    ![Crear una base de datos MySQL de prueba](./media/azure-stack-mysql-rp-deploy/mysql-create-db.png)

4. <span data-ttu-id="f5d78-222">Seleccione una SKU.</span><span class="sxs-lookup"><span data-stu-id="f5d78-222">Select a SKU.</span></span>

    ![Seleccionar una SKU](./media/azure-stack-mysql-rp-deploy/mysql-select-a-sku.png)

5. <span data-ttu-id="f5d78-224">Cree una configuración de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="f5d78-224">Create a login setting.</span></span> <span data-ttu-id="f5d78-225">Se puede reutilizar la configuración de inicio de sesión o puede crearse una nueva.</span><span class="sxs-lookup"><span data-stu-id="f5d78-225">The login setting can be reused or a new one created.</span></span> <span data-ttu-id="f5d78-226">Contiene el nombre de usuario y la contraseña para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f5d78-226">This contains the user name and password for the database.</span></span>

    ![Crear un nuevo inicio de sesión en la base de datos](./media/azure-stack-mysql-rp-deploy/create-new-login.png)

    <span data-ttu-id="f5d78-228">La cadena de conexión incluye el nombre real del servidor de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="f5d78-228">The connections string includes the real database server name.</span></span> <span data-ttu-id="f5d78-229">Cópielo del portal.</span><span class="sxs-lookup"><span data-stu-id="f5d78-229">Copy it from the portal.</span></span>

    ![Obtener la cadena de conexión para la base de datos MySQL](./media/azure-stack-mysql-rp-deploy/mysql-db-created.png)

> [!NOTE]
> <span data-ttu-id="f5d78-231">La longitud de los nombres de usuario no puede superar los 32 caracteres con MySQL 5.7 ni los 16 caracteres en versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="f5d78-231">The length of the user names cannot exceed 32 characters with MySQL 5.7 or 16 characters in earlier editions.</span></span> <span data-ttu-id="f5d78-232">Se trata de una limitación de las implementaciones de MySQL.</span><span class="sxs-lookup"><span data-stu-id="f5d78-232">This is a limitation of the MySQL implementations.</span></span>


## <a name="add-capacity"></a><span data-ttu-id="f5d78-233">Agregar capacidad</span><span class="sxs-lookup"><span data-stu-id="f5d78-233">Add capacity</span></span>

<span data-ttu-id="f5d78-234">Para agregar capacidad, agregue servidores MySQL adicionales en el portal de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f5d78-234">Add capacity by adding additional MySQL servers in the Azure Stack portal.</span></span> <span data-ttu-id="f5d78-235">Si quiere utilizar otra instancia de MySQL, haga clic en **Proveedores de recursos** &gt; **MySQLAdapter** &gt; **MySQL Hosting Servers** &gt; (Servidores host MySQL) **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f5d78-235">If you wish to use another instance of MySQL, click **Resource Providers** &gt; **MySQLAdapter** &gt; **MySQL Hosting Servers** &gt; **+Add**.</span></span>


## <a name="making-mysql-databases-available-to-tenants"></a><span data-ttu-id="f5d78-236">Poner las bases de datos MySQL a disposición de los inquilinos</span><span class="sxs-lookup"><span data-stu-id="f5d78-236">Making MySQL databases available to tenants</span></span>
<span data-ttu-id="f5d78-237">Cree planes y ofertas para poner las bases de datos MySQL a disposición de los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="f5d78-237">Create plans and offers to make MySQL databases available for tenants.</span></span> <span data-ttu-id="f5d78-238">Agregue el servicio Microsoft.MySqlAdapter, agregue una cuota, etc.</span><span class="sxs-lookup"><span data-stu-id="f5d78-238">Add the Microsoft.MySqlAdapter service, add a quota, etc.</span></span>

![Crear planes y ofertas para incluir las bases de datos](./media/azure-stack-mysql-rp-deploy/mysql-new-plan.png)

## <a name="removing-the-mysql-adapter-resource-provider"></a><span data-ttu-id="f5d78-240">Quitar el proveedor de recursos de adaptador de MySQL</span><span class="sxs-lookup"><span data-stu-id="f5d78-240">Removing the MySQL Adapter Resource Provider</span></span>

<span data-ttu-id="f5d78-241">Para quitar el proveedor de recursos, es esencial quitar antes todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="f5d78-241">To remove the resource provider, it is essential to first remove any dependencies.</span></span>

1. <span data-ttu-id="f5d78-242">Asegúrese de tener el paquete de implementación original que descargó para esta versión del proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="f5d78-242">Ensure you have the original deployment package that you downloaded for this version of the Resource Provider.</span></span>

2. <span data-ttu-id="f5d78-243">Todas las bases de datos de inquilino deben eliminarse del proveedor de recursos (así no se eliminarán los datos).</span><span class="sxs-lookup"><span data-stu-id="f5d78-243">All tenant databases must be deleted from the resource provider (this will not delete the data).</span></span> <span data-ttu-id="f5d78-244">Esto deben realizarlo los inquilinos mismos.</span><span class="sxs-lookup"><span data-stu-id="f5d78-244">This should be performed by the tenants themselves.</span></span>

3. <span data-ttu-id="f5d78-245">Los inquilinos deben anular el registro del espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="f5d78-245">Tenants must unregister from the namespace.</span></span>

4. <span data-ttu-id="f5d78-246">El administrador debe eliminar los servidores host del adaptador de MySQL.</span><span class="sxs-lookup"><span data-stu-id="f5d78-246">Administrator must delete the hosting servers from the MySQL Adapter</span></span>

5. <span data-ttu-id="f5d78-247">El administrador debe eliminar los planes que hacen referencia el adaptador de MySQL.</span><span class="sxs-lookup"><span data-stu-id="f5d78-247">Administrator must delete any plans that reference the MySQL Adapter.</span></span>

6. <span data-ttu-id="f5d78-248">El administrador debe eliminar las cuotas asociadas al adaptador de MySQL.</span><span class="sxs-lookup"><span data-stu-id="f5d78-248">Administrator must delete any quotas associated to the MySQL Adapter.</span></span>

7. <span data-ttu-id="f5d78-249">Vuelva a ejecutar el script de implementación con el parámetro -Uninstall, los puntos de conexión de Azure Resource Manager, DirectoryTenantID y las credenciales para la cuenta de administrador del servicio.</span><span class="sxs-lookup"><span data-stu-id="f5d78-249">Rerun the deployment script with the -Uninstall parameter, Azure Resource Manager endpoints, DirectoryTenantID, and credentials for the service administrator account.</span></span>




## <a name="next-steps"></a><span data-ttu-id="f5d78-250">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f5d78-250">Next steps</span></span>


<span data-ttu-id="f5d78-251">Pruebe otros [servicios PaaS](azure-stack-tools-paas-services.md), como el [proveedor de recursos de SQL Server](azure-stack-sql-resource-provider-deploy.md) y el [proveedor de recursos de App Services](azure-stack-app-service-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f5d78-251">Try other [PaaS services](azure-stack-tools-paas-services.md) like the [SQL Server resource provider](azure-stack-sql-resource-provider-deploy.md) and the [App Services resource provider](azure-stack-app-service-overview.md).</span></span>
