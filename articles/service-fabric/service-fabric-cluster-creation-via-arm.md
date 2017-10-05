---
title: "Creación de un clúster de Azure Service Fabric a partir de una plantilla | Microsoft Docs"
description: "En este artículo se describe cómo configurar un clúster seguro de Service Fabric en Azure mediante Azure Resource Manager, Azure Key Vault y Azure Active Directory (Azure AD) para la autenticación de clientes."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: 420ea486e626763af65a23e49ce04033ea418fb4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a><span data-ttu-id="7360d-103">Creación de un clúster de Service Fabric con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7360d-103">Create a Service Fabric cluster by using Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7360d-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7360d-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="7360d-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="7360d-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="7360d-106">Esta guía paso a paso le lleva por la configuración de un clúster seguro de Azure Service Fabric en Azure con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7360d-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span></span> <span data-ttu-id="7360d-107">Sabemos que el artículo es largo.</span><span class="sxs-lookup"><span data-stu-id="7360d-107">We acknowledge that the article is long.</span></span> <span data-ttu-id="7360d-108">No obstante, a menos que ya esté familiarizado con el contenido, asegúrese de seguir cada paso con cuidado.</span><span class="sxs-lookup"><span data-stu-id="7360d-108">Nevertheless, unless you are already thoroughly familiar with the content, be sure to follow each step carefully.</span></span>

<span data-ttu-id="7360d-109">La guía abarca los siguientes procedimientos:</span><span class="sxs-lookup"><span data-stu-id="7360d-109">The guide covers the following procedures:</span></span>

* <span data-ttu-id="7360d-110">Configuración de un almacén de claves de Azure para cargar certificados de seguridad de clúster y aplicación</span><span class="sxs-lookup"><span data-stu-id="7360d-110">Setting up an Azure key vault to upload certificates for cluster and application security</span></span>
* <span data-ttu-id="7360d-111">Creación de un clúster protegido en Azure con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7360d-111">Creating a secured cluster in Azure by using Azure Resource Manager</span></span>
* <span data-ttu-id="7360d-112">Autenticación de usuarios con Azure Active Directory (Azure AD) para la administración del clúster</span><span class="sxs-lookup"><span data-stu-id="7360d-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span></span>

<span data-ttu-id="7360d-113">Un clúster seguro es el que impide el acceso no autorizado a las operaciones de administración.</span><span class="sxs-lookup"><span data-stu-id="7360d-113">A secure cluster is a cluster that prevents unauthorized access to management operations.</span></span> <span data-ttu-id="7360d-114">Esto incluye la implementación, la actualización y la eliminación de aplicaciones y servicios, y los datos que contienen.</span><span class="sxs-lookup"><span data-stu-id="7360d-114">This includes deploying, upgrading, and deleting applications, services, and the data they contain.</span></span> <span data-ttu-id="7360d-115">Un clúster no seguro es un clúster al que cualquiera puede conectarse en cualquier momento y realizar operaciones de administración.</span><span class="sxs-lookup"><span data-stu-id="7360d-115">An unsecure cluster is a cluster that anyone can connect to at any time and perform management operations.</span></span> <span data-ttu-id="7360d-116">Aunque se puede crear un clúster no seguro, se recomienda firmemente crear uno seguro desde el principio.</span><span class="sxs-lookup"><span data-stu-id="7360d-116">Although it is possible to create an unsecure cluster, we highly recommend that you create a secure cluster from the outset.</span></span> <span data-ttu-id="7360d-117">Los clústeres no seguros no se pueden proteger en un momento posterior, por lo que se debe crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="7360d-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span></span>

<span data-ttu-id="7360d-118">El concepto de creación de clústeres seguros es el mismo, tanto si son de Linux como de Windows.</span><span class="sxs-lookup"><span data-stu-id="7360d-118">The concept of creating secure clusters is the same, whether they are Linux or Windows clusters.</span></span> <span data-ttu-id="7360d-119">Para más información y scripts auxiliares para crear clústeres seguros de Linux, consulte [Creating secure clusters on Linux](#secure-linux-clusters) (Creación de clústeres seguros en Linux).</span><span class="sxs-lookup"><span data-stu-id="7360d-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span></span>

## <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="7360d-120">Inicio de sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="7360d-120">Sign in to your Azure account</span></span>
<span data-ttu-id="7360d-121">En esta guía se usa [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="7360d-121">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="7360d-122">Al iniciar una nueva sesión de PowerShell, inicie sesión en su cuenta de Azure y seleccione su suscripción antes de ejecutar comandos de Azure.</span><span class="sxs-lookup"><span data-stu-id="7360d-122">When you start a new PowerShell session, sign in to your Azure account and select your subscription before you execute Azure commands.</span></span>

<span data-ttu-id="7360d-123">Inicio de sesión en la cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="7360d-123">Sign in to your Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="7360d-124">Seleccione su suscripción:</span><span class="sxs-lookup"><span data-stu-id="7360d-124">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a><span data-ttu-id="7360d-125">Configuración de un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="7360d-125">Set up a key vault</span></span>
<span data-ttu-id="7360d-126">En esta sección se habla de la creación de un almacén de claves para un clúster de Service Fabric en Azure y aplicaciones de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7360d-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="7360d-127">Para una guía completa sobre Azure Key Vault, consulte [Introducción a Azure Key Vault][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="7360d-127">For a complete guide to Azure Key Vault, refer to the [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="7360d-128">Service Fabric usa certificados X.509 para proteger un clúster y proporcionar características de seguridad de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7360d-128">Service Fabric uses X.509 certificates to secure a cluster and provide application security features.</span></span> <span data-ttu-id="7360d-129">Azure Key Vault se usa para administrar certificados para clústeres de Service Fabric en Azure.</span><span class="sxs-lookup"><span data-stu-id="7360d-129">You use Key Vault to manage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="7360d-130">Cuando un clúster se implementa en Azure, el proveedor de recursos de Azure responsable de crear clústeres de Service Fabric extrae los certificados de Key Vault y los instala en las máquinas virtuales del clúster.</span><span class="sxs-lookup"><span data-stu-id="7360d-130">When a cluster is deployed in Azure, the Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on the cluster VMs.</span></span>

<span data-ttu-id="7360d-131">En el diagrama siguiente se ilustra la relación entre Azure Key Vault, un clúster de Service Fabric y el proveedor de recursos de Azure que usa los certificados almacenados en el almacén de claves cuando se crea el clúster:</span><span class="sxs-lookup"><span data-stu-id="7360d-131">The following diagram illustrates the relationship between Azure Key Vault, a Service Fabric cluster, and the Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span></span>

![Diagrama de instalación del certificado][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="7360d-133">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="7360d-133">Create a resource group</span></span>
<span data-ttu-id="7360d-134">El primer paso es crear un grupo de recursos específico para el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7360d-134">The first step is to create a resource group specifically for your key vault.</span></span> <span data-ttu-id="7360d-135">Se recomienda colocar el almacén de claves en su propio grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7360d-135">We recommend that you put the key vault into its own resource group.</span></span> <span data-ttu-id="7360d-136">Esto le permite quitar los grupos de recursos de proceso y almacenamiento, incluido el grupo de recursos que tiene el clúster de Service Fabric, sin perder las claves y los secretos.</span><span class="sxs-lookup"><span data-stu-id="7360d-136">This action lets you remove the compute and storage resource groups, including the resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="7360d-137">El grupo de recursos que contiene el almacén de claves _debe estar en la misma región_ que el clúster que lo usa.</span><span class="sxs-lookup"><span data-stu-id="7360d-137">The resource group that contains your key vault _must be in the same region_ as the cluster that is using it.</span></span>

<span data-ttu-id="7360d-138">Si tiene previsto implementar clústeres en varias regiones, se recomienda denominar el grupo de recursos y el almacén de claves de manera que indique la región a la que pertenecen.</span><span class="sxs-lookup"><span data-stu-id="7360d-138">If you plan to deploy clusters in multiple regions, we suggest that you name the resource group and the key vault in a way that indicates which region it belongs to.</span></span>  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
<span data-ttu-id="7360d-139">El resultado debe ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="7360d-139">The output should look like this:</span></span>

```powershell

    WARNING: The output object type of this cmdlet is going to be modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-the-new-resource-group"></a><span data-ttu-id="7360d-140">Cree un almacén de claves en el nuevo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="7360d-140">Create a key vault in the new resource group</span></span>
<span data-ttu-id="7360d-141">El almacén de claves _debe estar habilitado para la implementación_ de forma que el proveedor de recursos de proceso pueda recibir de él certificados e instalarlos en instancias de máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="7360d-141">The key vault _must be enabled for deployment_ to allow the compute resource provider to get certificates from it and install it on virtual machine instances:</span></span>

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

<span data-ttu-id="7360d-142">El resultado debe ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="7360d-142">The output should look like this:</span></span>

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions to Keys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions to Secrets   :    all


    Tags                             :
```
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a><span data-ttu-id="7360d-143">Uso de un almacén de claves existente</span><span class="sxs-lookup"><span data-stu-id="7360d-143">Use an existing key vault</span></span>

<span data-ttu-id="7360d-144">Para usar un almacén de claves existente, _debe estar habilitado para la implementación_, de forma que el proveedor de recursos de proceso pueda recibir de él certificados e instalarlos en nodos de clúster:</span><span class="sxs-lookup"><span data-stu-id="7360d-144">To use an existing key vault, you _must enable it for deployment_ to allow the compute resource provider to get certificates from it and install it on cluster nodes:</span></span>

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-to-your-key-vault"></a><span data-ttu-id="7360d-145">Introducción de certificados al almacén de claves</span><span class="sxs-lookup"><span data-stu-id="7360d-145">Add certificates to your key vault</span></span>

<span data-ttu-id="7360d-146">Los certificados se usan en Service Fabric para proporcionar autenticación y cifrado con el fin de proteger diversos aspectos de un clúster y sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7360d-146">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="7360d-147">Para obtener más información sobre el modo en que se usan los certificados en Service Fabric, consulte los [Escenarios de seguridad de los clústeres de Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="7360d-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="7360d-148">Certificado de clúster y servidor (obligatorio)</span><span class="sxs-lookup"><span data-stu-id="7360d-148">Cluster and server certificate (required)</span></span>
<span data-ttu-id="7360d-149">Este certificado es necesario para proteger un clúster e impedir el acceso no autorizado.</span><span class="sxs-lookup"><span data-stu-id="7360d-149">This certificate is required to secure a cluster and prevent unauthorized access to it.</span></span> <span data-ttu-id="7360d-150">Ofrece seguridad al clúster de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="7360d-150">It provides cluster security in two ways:</span></span>

* <span data-ttu-id="7360d-151">Autenticación del clúster: se autentica la comunicación de nodo a nodo para la federación del clúster.</span><span class="sxs-lookup"><span data-stu-id="7360d-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="7360d-152">Solo los nodos que pueden probar su identidad con este certificado pueden unirse al clúster.</span><span class="sxs-lookup"><span data-stu-id="7360d-152">Only nodes that can prove their identity with this certificate can join the cluster.</span></span>
* <span data-ttu-id="7360d-153">Autenticación del servidor: los puntos de conexión de administración del clúster se autentican en un cliente de administración, de forma que este sabe que está hablando con el clúster real.</span><span class="sxs-lookup"><span data-stu-id="7360d-153">Server authentication: Authenticates the cluster management endpoints to a management client, so that the management client knows it is talking to the real cluster.</span></span> <span data-ttu-id="7360d-154">Este certificado proporciona también SSL para la API de administración de HTTPS y para Service Fabric Explorer sobre HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7360d-154">This certificate also provides an SSL for the HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="7360d-155">Para servir a estos propósitos, el certificado debe cumplir los siguientes requisitos:</span><span class="sxs-lookup"><span data-stu-id="7360d-155">To serve these purposes, the certificate must meet the following requirements:</span></span>

* <span data-ttu-id="7360d-156">El certificado debe contener una clave privada.</span><span class="sxs-lookup"><span data-stu-id="7360d-156">The certificate must contain a private key.</span></span>
* <span data-ttu-id="7360d-157">El certificado debe crearse para el intercambio de claves, que se pueda exportar a un archivo Personal Information Exchange (.pfx).</span><span class="sxs-lookup"><span data-stu-id="7360d-157">The certificate must be created for key exchange, which is exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="7360d-158">El nombre de sujeto del certificado debe coincidir con el dominio usado para acceder al clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7360d-158">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="7360d-159">Esta coincidencia es necesaria para proporcionar SSL a los puntos de conexión de administración HTTPS y de Service Fabric Explorer del clúster.</span><span class="sxs-lookup"><span data-stu-id="7360d-159">This matching is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="7360d-160">No puede obtener un certificado SSL de una entidad de certificación (CA) para el dominio .cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="7360d-160">You cannot obtain an SSL certificate from a certificate authority (CA) for the .cloudapp.azure.com domain.</span></span> <span data-ttu-id="7360d-161">Debe adquirir un nombre de dominio personalizado para el clúster.</span><span class="sxs-lookup"><span data-stu-id="7360d-161">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="7360d-162">Cuando solicite un certificado de una CA, el nombre de sujeto del certificado debe coincidir con el nombre del dominio personalizado del clúster.</span><span class="sxs-lookup"><span data-stu-id="7360d-162">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

### <a name="application-certificates-optional"></a><span data-ttu-id="7360d-163">Certificados de aplicación (opcionales)</span><span class="sxs-lookup"><span data-stu-id="7360d-163">Application certificates (optional)</span></span>
<span data-ttu-id="7360d-164">Se puede instalar un número cualquiera de certificados adicionales en un clúster para proteger la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7360d-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="7360d-165">Antes de crear el clúster, tenga en cuenta los escenarios de seguridad de las aplicaciones que requieren que se instale un certificado en los nodos, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7360d-165">Before creating your cluster, consider the application security scenarios that require a certificate to be installed on the nodes, such as:</span></span>

* <span data-ttu-id="7360d-166">Cifrado y descifrado de los valores de configuración de aplicación.</span><span class="sxs-lookup"><span data-stu-id="7360d-166">Encryption and decryption of application configuration values.</span></span>
* <span data-ttu-id="7360d-167">Cifrado de datos entre nodos durante la replicación.</span><span class="sxs-lookup"><span data-stu-id="7360d-167">Encryption of data across nodes during replication.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="7360d-168">Formato de certificados para el uso del proveedor de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="7360d-168">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="7360d-169">Puede agregar y usar archivos de claves privadas (.pfx) directamente a través del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7360d-169">You can add and use private key files (.pfx) directly through your key vault.</span></span> <span data-ttu-id="7360d-170">Sin embargo, el proveedor de recursos de proceso de Azure requiere que las claves se almacenen en un formato especial de notación de objetos JavaScript (JSON).</span><span class="sxs-lookup"><span data-stu-id="7360d-170">However, the Azure compute resource provider requires keys to be stored in a special JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="7360d-171">El formato incluye el archivo .pfx como cadena con codificación de base 64 y la contraseña de clave privada.</span><span class="sxs-lookup"><span data-stu-id="7360d-171">The format includes the .pfx file as a base 64-encoded string and the private key password.</span></span> <span data-ttu-id="7360d-172">Para cumplir estos requisitos, las claves deben estar colocadas en una cadena JSON y luego almacenarse como "secretos" en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7360d-172">To accommodate these requirements, the keys must be placed in a JSON string and then stored as "secrets" in the key vault.</span></span>

<span data-ttu-id="7360d-173">Para facilitar este proceso, hay un módulo de PowerShell [disponible en GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="7360d-173">To make this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="7360d-174">Para usar el módulo, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7360d-174">To use the module, do the following:</span></span>

1. <span data-ttu-id="7360d-175">Descargue todo el contenido del repositorio en un directorio local.</span><span class="sxs-lookup"><span data-stu-id="7360d-175">Download the entire contents of the repo into a local directory.</span></span>
2. <span data-ttu-id="7360d-176">Vaya al directorio local.</span><span class="sxs-lookup"><span data-stu-id="7360d-176">Go to the local directory.</span></span>
2. <span data-ttu-id="7360d-177">Importe el módulo ServiceFabricRPHelpers en la ventana de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7360d-177">Import the ServiceFabricRPHelpers module in your PowerShell window:</span></span>

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

<span data-ttu-id="7360d-178">El comando `Invoke-AddCertToKeyVault` de este módulo de PowerShell convierte automáticamente una clave privada de certificado en una cadena JSON y la carga en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7360d-178">The `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it to the key vault.</span></span> <span data-ttu-id="7360d-179">Use el comando para agregar el certificado de clúster y cualquier certificado de aplicación adicional al almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7360d-179">Use the command to add the cluster certificate and any additional application certificates to the key vault.</span></span> <span data-ttu-id="7360d-180">Repita este paso con cualquier certificado adicional que quiera instalar en el clúster.</span><span class="sxs-lookup"><span data-stu-id="7360d-180">Repeat this step for any additional certificates you want to install in your cluster.</span></span>

#### <a name="uploading-an-existing-certificate"></a><span data-ttu-id="7360d-181">Carga de un certificado existente</span><span class="sxs-lookup"><span data-stu-id="7360d-181">Uploading an existing certificate</span></span>

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

<span data-ttu-id="7360d-182">Si se produce un error, como el que se muestra aquí, suele significar que tiene un conflicto con la dirección URL del recurso.</span><span class="sxs-lookup"><span data-stu-id="7360d-182">If you get an error, such as the one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="7360d-183">Para resolverlo, cambie el nombre del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7360d-183">To resolve the conflict, change the key vault name.</span></span>

```
Set-AzureKeyVaultSecret : The remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="7360d-184">Una vez resuelto, el resultado debería tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="7360d-184">After the conflict is resolved, the output should look like this:</span></span>

```

    Switching context to SubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: The output object type of this cmdlet is going to be modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret to mywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
><span data-ttu-id="7360d-185">Se necesitan las tres cadenas anteriores, CertificateThumbprint, SourceVault y CertificateURL, para configurar un clúster seguro de Service Fabric y obtener los certificados de aplicación que quizá esté usando para la seguridad de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7360d-185">You need the three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, to set up a secure Service Fabric cluster and to obtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="7360d-186">Si no guarda las cadenas, puede ser difícil recuperarlos mediante una consulta al almacén de claves más adelante.</span><span class="sxs-lookup"><span data-stu-id="7360d-186">If you do not save the strings, it can be difficult to retrieve them by querying the key vault later.</span></span>

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-to-the-key-vault"></a><span data-ttu-id="7360d-187">Creación de un certificado autofirmado para cargarlo en el almacén de claves</span><span class="sxs-lookup"><span data-stu-id="7360d-187">Creating a self-signed certificate and uploading it to the key vault</span></span>

<span data-ttu-id="7360d-188">Si ya ha cargado los certificados en el almacén de claves, omita este paso.</span><span class="sxs-lookup"><span data-stu-id="7360d-188">If you have already uploaded your certificates to the key vault, skip this step.</span></span> <span data-ttu-id="7360d-189">Este paso es para generar un nuevo certificado autofirmado y cargarlo en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7360d-189">This step is for generating a new self-signed certificate and uploading it to your key vault.</span></span> <span data-ttu-id="7360d-190">Después de cambiar los parámetro del script siguiente y ejecutarlo, se le solicitará una contraseña de certificado.</span><span class="sxs-lookup"><span data-stu-id="7360d-190">After you change the parameters in the following script and then run it, you should be prompted for a certificate password.</span></span>  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #The certificate's subject name must match the domain used to access the Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want the .PFX to be stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

<span data-ttu-id="7360d-191">Si se produce un error, como el que se muestra aquí, suele significar que tiene un conflicto con la dirección URL del recurso.</span><span class="sxs-lookup"><span data-stu-id="7360d-191">If you get an error, such as the one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="7360d-192">Para resolver el conflicto, cambie el nombre del almacén de claves, el nombre del grupo de recursos, etc.</span><span class="sxs-lookup"><span data-stu-id="7360d-192">To resolve the conflict, change the key vault name, RG name, and so forth.</span></span>

```
Set-AzureKeyVaultSecret : The remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="7360d-193">Una vez resuelto, el resultado debería tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="7360d-193">After the conflict is resolved, the output should look like this:</span></span>

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context to SubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: The output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret to chackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
><span data-ttu-id="7360d-194">Se necesitan las tres cadenas anteriores, CertificateThumbprint, SourceVault y CertificateURL, para configurar un clúster seguro de Service Fabric y obtener los certificados de aplicación que quizá esté usando para la seguridad de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7360d-194">You need the three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, to set up a secure Service Fabric cluster and to obtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="7360d-195">Si no guarda las cadenas, puede ser difícil recuperarlos mediante una consulta al almacén de claves más adelante.</span><span class="sxs-lookup"><span data-stu-id="7360d-195">If you do not save the strings, it can be difficult to retrieve them by querying the key vault later.</span></span>

 <span data-ttu-id="7360d-196">En este punto, debería tener los siguientes elementos en su lugar:</span><span class="sxs-lookup"><span data-stu-id="7360d-196">At this point, you should have the following elements in place:</span></span>

* <span data-ttu-id="7360d-197">El grupo de recursos del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7360d-197">The key vault resource group.</span></span>
* <span data-ttu-id="7360d-198">El almacén de claves y su dirección URL (llamado SourceVault en la salida de PowerShell anterior).</span><span class="sxs-lookup"><span data-stu-id="7360d-198">The key vault and its URL (called SourceVault in the preceding PowerShell output).</span></span>
* <span data-ttu-id="7360d-199">El certificado de autenticación de servidor de clúster y su dirección URL en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7360d-199">The cluster server authentication certificate and its URL in the key vault.</span></span>
* <span data-ttu-id="7360d-200">Los certificados de aplicación y sus direcciones URL en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7360d-200">The application certificates and their URLs in the key vault.</span></span>


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="7360d-201">Configuración de Azure Active Directory para la autenticación de cliente</span><span class="sxs-lookup"><span data-stu-id="7360d-201">Set up Azure Active Directory for client authentication</span></span>

<span data-ttu-id="7360d-202">Azure AD permite a las organizaciones (conocidas como inquilinos) administrar el acceso de los usuarios a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7360d-202">Azure AD enables organizations (known as tenants) to manage user access to applications.</span></span> <span data-ttu-id="7360d-203">Las aplicaciones se dividen en las que tienen interfaz de usuario de inicio de sesión basada en web y las que tienen una experiencia de cliente nativa.</span><span class="sxs-lookup"><span data-stu-id="7360d-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span></span> <span data-ttu-id="7360d-204">En este artículo se supone que ya ha creado un inquilino.</span><span class="sxs-lookup"><span data-stu-id="7360d-204">In this article, we assume that you have already created a tenant.</span></span> <span data-ttu-id="7360d-205">En caso de que no lo haya hecho, lea [Obtención de un inquilino de Azure Active Directory][active-directory-howto-tenant].</span><span class="sxs-lookup"><span data-stu-id="7360d-205">If you have not, start by reading [How to get an Azure Active Directory tenant][active-directory-howto-tenant].</span></span>

<span data-ttu-id="7360d-206">Un clúster de Service Fabric ofrece diversos puntos de entrada a su funcionalidad de administración, como [Service Fabric Explorer][service-fabric-visualizing-your-cluster] y [Visual Studio][service-fabric-manage-application-in-visual-studio] basados en web.</span><span class="sxs-lookup"><span data-stu-id="7360d-206">A Service Fabric cluster offers several entry points to its management functionality, including the web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span></span> <span data-ttu-id="7360d-207">Como resultado, creará dos aplicaciones de Azure AD para controlar el acceso al clúster, una aplicación web y otra nativa.</span><span class="sxs-lookup"><span data-stu-id="7360d-207">As a result, you create two Azure AD applications to control access to the cluster, one web application and one native application.</span></span>

<span data-ttu-id="7360d-208">Para simplificar algunos de los pasos necesarios para configurar Azure AD con un clúster de Service Fabric, hemos creado un conjunto de scripts de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7360d-208">To simplify some of the steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="7360d-209">Debe realizar los pasos siguientes antes de crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="7360d-209">You must complete the following steps before you create the cluster.</span></span> <span data-ttu-id="7360d-210">Dado que los scripts esperan los puntos de conexión y los nombres de los clústeres, los valores deben planearse y no se pueden usar los que ya haya creado.</span><span class="sxs-lookup"><span data-stu-id="7360d-210">Because the scripts expect cluster names and endpoints, the values should be planned and not values that you have already created.</span></span>

1. <span data-ttu-id="7360d-211">[Descargue los scripts][sf-aad-ps-script-download] en su equipo.</span><span class="sxs-lookup"><span data-stu-id="7360d-211">[Download the scripts][sf-aad-ps-script-download] to your computer.</span></span>
2. <span data-ttu-id="7360d-212">Haga clic con el botón derecho en el archivo zip, seleccione **Propiedades** y la casilla **Desbloquear**, y haga clic en **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="7360d-212">Right-click the zip file, select **Properties**, select the **Unblock** check box, and then click **Apply**.</span></span>
3. <span data-ttu-id="7360d-213">Extraiga el archivo ZIP.</span><span class="sxs-lookup"><span data-stu-id="7360d-213">Extract the zip file.</span></span>
4. <span data-ttu-id="7360d-214">Ejecute `SetupApplications.ps1` y proporcione los parámetros TenantId, ClusterName y WebApplicationReplyUrl.</span><span class="sxs-lookup"><span data-stu-id="7360d-214">Run `SetupApplications.ps1`, and provide the TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span></span> <span data-ttu-id="7360d-215">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7360d-215">For example:</span></span>

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    <span data-ttu-id="7360d-216">Ejecute el comando `Get-AzureSubscription` de PowerShell para encontrar su TenantId.</span><span class="sxs-lookup"><span data-stu-id="7360d-216">You can find your TenantId by executing the PowerShell command `Get-AzureSubscription`.</span></span> <span data-ttu-id="7360d-217">Al ejecutar este comando se muestra el valor de TenantId para cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="7360d-217">Executing this command displays the TenantId for every subscription.</span></span>

    <span data-ttu-id="7360d-218">El valor de ClusterName se usa como prefijo en las aplicaciones de Azure AD que crea el script.</span><span class="sxs-lookup"><span data-stu-id="7360d-218">ClusterName is used to prefix the Azure AD applications that are created by the script.</span></span> <span data-ttu-id="7360d-219">No es necesario que coincida exactamente con el nombre del clúster real.</span><span class="sxs-lookup"><span data-stu-id="7360d-219">It does not need to match the actual cluster name exactly.</span></span> <span data-ttu-id="7360d-220">Está diseñado solo para facilitar la asignación de artefactos de Azure AD al clúster de Service Fabric con el que se utilizan.</span><span class="sxs-lookup"><span data-stu-id="7360d-220">It is intended only to make it easier to map Azure AD artifacts to the Service Fabric cluster that they're being used with.</span></span>

    <span data-ttu-id="7360d-221">El valor de WebApplicationReplyUrl es el punto de conexión predeterminado al que Azure AD devuelve a los usuarios cuando terminan el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="7360d-221">WebApplicationReplyUrl is the default endpoint that Azure AD returns to your users after they finish signing in.</span></span> <span data-ttu-id="7360d-222">Establézcalo como el punto de conexión de Service Fabric Explorer para el clúster, que de manera predeterminada es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="7360d-222">Set this endpoint as the Service Fabric Explorer endpoint for your cluster, which by default is:</span></span>

    <span data-ttu-id="7360d-223">https://&lt;cluster_domain&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="7360d-223">https://&lt;cluster_domain&gt;:19080/Explorer</span></span>

    <span data-ttu-id="7360d-224">Se le pedirá que inicie sesión en una cuenta con privilegios administrativos para el inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7360d-224">You are prompted to sign in to an account that has administrative privileges for the Azure AD tenant.</span></span> <span data-ttu-id="7360d-225">Una vez iniciada la sesión, el script creará las aplicaciones web y nativa para representar el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7360d-225">After you sign in, the script creates the web and native applications to represent your Service Fabric cluster.</span></span> <span data-ttu-id="7360d-226">Si examina las aplicaciones del inquilino en el [Portal de Azure clásico][azure-classic-portal], debería ver dos entradas nuevas:</span><span class="sxs-lookup"><span data-stu-id="7360d-226">If you look at the tenant's applications in the [Azure classic portal][azure-classic-portal], you should see two new entries:</span></span>

   * <span data-ttu-id="7360d-227">*ClusterName*\_Clúster</span><span class="sxs-lookup"><span data-stu-id="7360d-227">*ClusterName*\_Cluster</span></span>
   * <span data-ttu-id="7360d-228">*ClusterName*\_Cliente</span><span class="sxs-lookup"><span data-stu-id="7360d-228">*ClusterName*\_Client</span></span>

   <span data-ttu-id="7360d-229">El script imprimirá el código JSON que necesita la plantilla de Azure Resource Manager al crear el clúster en la sección siguiente, por lo que es buena idea mantener abierta la ventana de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7360d-229">The script prints the JSON required by the Azure Resource Manager template when you create the cluster in the next section, so it's a good idea to keep the PowerShell window open.</span></span>

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a><span data-ttu-id="7360d-230">Creación de una plantilla de Resource Manager para el clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7360d-230">Create a Service Fabric cluster Resource Manager template</span></span>
<span data-ttu-id="7360d-231">En esta sección, se usarán las salidas de los comandos de PowerShell anteriores en una plantilla de Resource Manager para el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7360d-231">In this section, the outputs of the preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span></span>

<span data-ttu-id="7360d-232">Las plantillas de ejemplo de Resource Manager están disponibles en la [Galería de plantillas de inicio de rápido de Azure en GitHub][azure-quickstart-templates].</span><span class="sxs-lookup"><span data-stu-id="7360d-232">Sample Resource Manager templates are available in the [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span></span> <span data-ttu-id="7360d-233">Estas plantillas se pueden usar como punto de partida para crear la plantilla de clúster.</span><span class="sxs-lookup"><span data-stu-id="7360d-233">These templates can be used as a starting point for your cluster template.</span></span>

### <a name="create-the-resource-manager-template"></a><span data-ttu-id="7360d-234">Creación de la plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7360d-234">Create the Resource Manager template</span></span>
<span data-ttu-id="7360d-235">En esta guía se usa la plantilla de ejemplo de [clúster seguro de 5 nodos][service-fabric-secure-cluster-5-node-1-nodetype] y los parámetros de plantilla.</span><span class="sxs-lookup"><span data-stu-id="7360d-235">This guide uses the [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span></span> <span data-ttu-id="7360d-236">Descargue `azuredeploy.json` y `azuredeploy.parameters.json` en su equipo y abra ambos archivos en el editor de texto de su elección.</span><span class="sxs-lookup"><span data-stu-id="7360d-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` to your computer and open both files in your favorite text editor.</span></span>

### <a name="add-certificates"></a><span data-ttu-id="7360d-237">Adición de certificados</span><span class="sxs-lookup"><span data-stu-id="7360d-237">Add certificates</span></span>
<span data-ttu-id="7360d-238">Para agregar certificados a una plantilla de Resource Manager para el clúster, haga referencia al almacén de claves que contiene las claves de certificado.</span><span class="sxs-lookup"><span data-stu-id="7360d-238">You add certificates to a cluster Resource Manager template by referencing the key vault that contains the certificate keys.</span></span> <span data-ttu-id="7360d-239">Se recomienda colocar los valores del almacén de claves en un archivo de parámetros de plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7360d-239">We recommend that you place the key-vault values in a Resource Manager template parameters file.</span></span> <span data-ttu-id="7360d-240">De este modo se puede reutilizar el archivo de plantilla de Resource Manager y se mantiene libre de valores específicos a una implementación.</span><span class="sxs-lookup"><span data-stu-id="7360d-240">Doing so keeps the Resource Manager template file reusable and free of values specific to a deployment.</span></span>

#### <a name="add-all-certificates-to-the-virtual-machine-scale-set-osprofile"></a><span data-ttu-id="7360d-241">Incorporación de todos los certificados a osProfile del conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="7360d-241">Add all certificates to the virtual machine scale set osProfile</span></span>
<span data-ttu-id="7360d-242">Todos los certificados instalados en el clúster deben estar configurados en la sección osProfile del recurso del conjunto de escalado (Microsoft.Compute/virtualMachineScaleSets).</span><span class="sxs-lookup"><span data-stu-id="7360d-242">Every certificate that's installed in the cluster must be configured in the osProfile section of the scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span></span> <span data-ttu-id="7360d-243">Con ello se indica al proveedor de recursos que instale el certificado en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="7360d-243">This action instructs the resource provider to install the certificate on the VMs.</span></span> <span data-ttu-id="7360d-244">Esta instalación incluye tanto el certificado del clúster como los certificados de seguridad de la aplicación que planee usar para las aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="7360d-244">This installation includes both the cluster certificate and any application security certificates that you plan to use for your applications:</span></span>

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-the-service-fabric-cluster-certificate"></a><span data-ttu-id="7360d-245">Configuración del certificado de clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7360d-245">Configure the Service Fabric cluster certificate</span></span>
<span data-ttu-id="7360d-246">El certificado de autenticación del clúster debe estar configurado tanto en el recurso del clúster de Service Fabric (Microsoft.ServiceFabric/clusters) como en la extensión de Service Fabric para conjuntos de escalado de máquinas virtuales en el recurso de conjuntos de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="7360d-246">The cluster authentication certificate must be configured in both the Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and the Service Fabric extension for virtual machine scale sets in the virtual machine scale set resource.</span></span> <span data-ttu-id="7360d-247">Esta disposición permite al proveedor de recursos de Service Fabric configurarlo para su uso en la autenticación del clúster y la autenticación del servidor en los puntos de conexión de administración.</span><span class="sxs-lookup"><span data-stu-id="7360d-247">This arrangement allows the Service Fabric resource provider to configure it for use for cluster authentication and server authentication for management endpoints.</span></span>

##### <a name="virtual-machine-scale-set-resource"></a><span data-ttu-id="7360d-248">Recurso de conjunto de escalado de máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="7360d-248">Virtual machine scale set resource:</span></span>
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a><span data-ttu-id="7360d-249">Recurso de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="7360d-249">Service Fabric resource:</span></span>
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a><span data-ttu-id="7360d-250">Inserción de la configuración de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7360d-250">Insert Azure AD configuration</span></span>
<span data-ttu-id="7360d-251">La configuración de Azure AD que creó anteriormente se puede insertar directamente en la plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7360d-251">The Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span></span> <span data-ttu-id="7360d-252">Sin embargo, se recomienda que primero extraiga los valores a un archivo de parámetros para poder reutilizar la plantilla de Resource Manager, sin necesidad de valores específicos de una implementación.</span><span class="sxs-lookup"><span data-stu-id="7360d-252">However, we recommended that you first extract the values into a parameters file to keep the Resource Manager template reusable and free of values specific to a deployment.</span></span>

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### <span data-ttu-id="7360d-253"><a "configure-arm" ></a>Configuración de los parámetros de plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7360d-253"><a "configure-arm" ></a>Configure Resource Manager template parameters</span></span>
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since the link seems not to be redirecting correctly --->
<span data-ttu-id="7360d-254">Por último, utilice los valores de salida del almacén de claves y los comandos de PowerShell de Azure AD para rellenar el archivo de parámetros:</span><span class="sxs-lookup"><span data-stu-id="7360d-254">Finally, use the output values from the key vault and Azure AD PowerShell commands to populate the parameters file:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
<span data-ttu-id="7360d-255">En este punto, debería tener los siguientes elementos en su lugar:</span><span class="sxs-lookup"><span data-stu-id="7360d-255">At this point, you should have the following elements in place:</span></span>

* <span data-ttu-id="7360d-256">Grupo de recursos del almacén de claves</span><span class="sxs-lookup"><span data-stu-id="7360d-256">Key vault resource group</span></span>
  * <span data-ttu-id="7360d-257">Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="7360d-257">Key vault</span></span>
  * <span data-ttu-id="7360d-258">Certificado de autenticación de servidor de clúster</span><span class="sxs-lookup"><span data-stu-id="7360d-258">Cluster server authentication certificate</span></span>
  * <span data-ttu-id="7360d-259">Certificado de cifrado de datos</span><span class="sxs-lookup"><span data-stu-id="7360d-259">Data encipherment certificate</span></span>
* <span data-ttu-id="7360d-260">Inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7360d-260">Azure Active Directory tenant</span></span>
  * <span data-ttu-id="7360d-261">Aplicación de Azure AD para la administración basada en web y Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="7360d-261">Azure AD application for web-based management and Service Fabric Explorer</span></span>
  * <span data-ttu-id="7360d-262">Aplicación de Azure AD para la administración de cliente nativo</span><span class="sxs-lookup"><span data-stu-id="7360d-262">Azure AD application for native client management</span></span>
  * <span data-ttu-id="7360d-263">Usuarios y roles asignados</span><span class="sxs-lookup"><span data-stu-id="7360d-263">Users and their assigned roles</span></span>
* <span data-ttu-id="7360d-264">Plantilla de Resource Manager para el clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7360d-264">Service Fabric cluster Resource Manager template</span></span>
  * <span data-ttu-id="7360d-265">Certificados configurados mediante el almacén de claves</span><span class="sxs-lookup"><span data-stu-id="7360d-265">Certificates configured through key vault</span></span>
  * <span data-ttu-id="7360d-266">Azure Active Directory configurado</span><span class="sxs-lookup"><span data-stu-id="7360d-266">Azure Active Directory configured</span></span>

<span data-ttu-id="7360d-267">En el diagrama siguiente se ilustra el lugar que ocupa el almacén de claves y la configuración de Azure AD en la plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7360d-267">The following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span></span>

![Asignación de dependencias de Resource Manager][cluster-security-arm-dependency-map]

## <a name="create-the-cluster"></a><span data-ttu-id="7360d-269">Creación de clústeres</span><span class="sxs-lookup"><span data-stu-id="7360d-269">Create the cluster</span></span>
<span data-ttu-id="7360d-270">Ahora está listo para crear el clúster con la [implementación de la plantilla de recursos de Azure][resource-group-template-deploy].</span><span class="sxs-lookup"><span data-stu-id="7360d-270">You are now ready to create the cluster by using [Azure resource template deployment][resource-group-template-deploy].</span></span>

#### <a name="test-it"></a><span data-ttu-id="7360d-271">Pruébelo.</span><span class="sxs-lookup"><span data-stu-id="7360d-271">Test it</span></span>
<span data-ttu-id="7360d-272">Utilice el siguiente comando de PowerShell para probar la plantilla de Resource Manager con un archivo de parámetros:</span><span class="sxs-lookup"><span data-stu-id="7360d-272">Use the following PowerShell command to test your Resource Manager template with a parameters file:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a><span data-ttu-id="7360d-273">Impleméntelo.</span><span class="sxs-lookup"><span data-stu-id="7360d-273">Deploy it</span></span>
<span data-ttu-id="7360d-274">Si la prueba de la plantilla de Resource Manager es satisfactoria, use el siguiente comando de PowerShell para implementar dicha plantilla con un archivo de parámetros:</span><span class="sxs-lookup"><span data-stu-id="7360d-274">If the Resource Manager template test passes, use the following PowerShell command to deploy your Resource Manager template with a parameters file:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-to-roles"></a><span data-ttu-id="7360d-275">Asignación de usuarios a roles</span><span class="sxs-lookup"><span data-stu-id="7360d-275">Assign users to roles</span></span>
<span data-ttu-id="7360d-276">Una vez que haya creado las aplicaciones para representar el clúster, debe asignar los usuarios a los roles compatibles con Service Fabric: solo lectura y administrador. Puede asignar los roles mediante el [Portal de Azure clásico][azure-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="7360d-276">After you have created the applications to represent your cluster, assign your users to the roles supported by Service Fabric: read-only and admin. You can assign the roles by using the [Azure classic portal][azure-classic-portal].</span></span>

1. <span data-ttu-id="7360d-277">En Azure Portal, vaya a su inquilino y seleccione **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7360d-277">In the Azure portal, go to your tenant, and then select **Applications**.</span></span>
2. <span data-ttu-id="7360d-278">Elija la aplicación web, cuyo nombre se parece a `myTestCluster_Cluster`.</span><span class="sxs-lookup"><span data-stu-id="7360d-278">Select the web application, which has a name like `myTestCluster_Cluster`.</span></span>
3. <span data-ttu-id="7360d-279">Haga clic en la pestaña **Usuarios** .</span><span class="sxs-lookup"><span data-stu-id="7360d-279">Click the **Users** tab.</span></span>
4. <span data-ttu-id="7360d-280">Seleccione un usuario para asignar y haga clic en el botón **Asignar** situado en la parte inferior de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="7360d-280">Select a user to assign, and then click the **Assign** button at the bottom of the screen.</span></span>

    ![Botón para asignar usuarios a roles][assign-users-to-roles-button]
5. <span data-ttu-id="7360d-282">Seleccione el rol que quiere asignar al usuario.</span><span class="sxs-lookup"><span data-stu-id="7360d-282">Select the role to assign to the user.</span></span>

    ![Cuadro de diálogo "Asignar usuarios"][assign-users-to-roles-dialog]

> [!NOTE]
> <span data-ttu-id="7360d-284">Para más información sobre los roles de Service Fabric, consulte [Control de acceso basado en roles para clientes de Service Fabric](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="7360d-284">For more information about roles in Service Fabric, see [Role-based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused the wrong redirection of the link --->

## <a name="create-secure-clusters-on-linux"></a><span data-ttu-id="7360d-285">Creación de clústeres seguros en Linux</span><span class="sxs-lookup"><span data-stu-id="7360d-285">Create secure clusters on Linux</span></span>
<span data-ttu-id="7360d-286">Para facilitar el proceso, se ha proporcionado un [script auxiliar](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span><span class="sxs-lookup"><span data-stu-id="7360d-286">To make the process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span></span> <span data-ttu-id="7360d-287">Antes de usar este script auxiliar, asegúrese de que ya tiene la interfaz de la línea de comandos (CLI) de Azure instalada y se encuentra en la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="7360d-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span></span> <span data-ttu-id="7360d-288">Asegúrese de que el script tiene permisos de ejecución ejecutando `chmod +x cert_helper.py` después de descargarlo.</span><span class="sxs-lookup"><span data-stu-id="7360d-288">Make sure that the script has permissions to execute by running `chmod +x cert_helper.py` after downloading it.</span></span> <span data-ttu-id="7360d-289">El primer paso es iniciar sesión en su cuenta de Azure mediante la CLI con el comando `azure login`.</span><span class="sxs-lookup"><span data-stu-id="7360d-289">The first step is to sign in to your Azure account by using CLI with the `azure login` command.</span></span> <span data-ttu-id="7360d-290">Después de iniciar sesión en su cuenta de Azure, use el script auxiliar con su certificado firmado por la entidad de certificación, como se muestra en el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7360d-290">After signing in to your Azure account, use the helper script with your CA signed certificate, as the following command shows:</span></span>

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

<span data-ttu-id="7360d-291">El parámetro -ifile puede tomar un archivo .pfx o un .pem como entrada, con el tipo de certificado (pfx o pem, o ss si es un certificado autofirmado).</span><span class="sxs-lookup"><span data-stu-id="7360d-291">The -ifile parameter can take a .pfx file or a .pem file as input, with the certificate type (pfx or pem, or ss if it is a self-signed certificate).</span></span>
<span data-ttu-id="7360d-292">El parámetro -h imprime el texto de ayuda.</span><span class="sxs-lookup"><span data-stu-id="7360d-292">The parameter -h prints out the help text.</span></span>


<span data-ttu-id="7360d-293">Este comando devuelve las siguientes tres cadenas como salida:</span><span class="sxs-lookup"><span data-stu-id="7360d-293">This command returns the following three strings as the output:</span></span>

* <span data-ttu-id="7360d-294">SourceVaultID, el identificador para el nuevo KeyVault ResourceGroup que creó para usted</span><span class="sxs-lookup"><span data-stu-id="7360d-294">SourceVaultID, which is the ID for the new KeyVault ResourceGroup it created for you</span></span>
* <span data-ttu-id="7360d-295">CertificateUrl para acceder al certificado</span><span class="sxs-lookup"><span data-stu-id="7360d-295">CertificateUrl for accessing the certificate</span></span>
* <span data-ttu-id="7360d-296">CertificateThumbprint, que se utiliza para la autenticación</span><span class="sxs-lookup"><span data-stu-id="7360d-296">CertificateThumbprint, which is used for authentication</span></span>

<span data-ttu-id="7360d-297">En el ejemplo siguiente se muestra cómo utilizar el comando:</span><span class="sxs-lookup"><span data-stu-id="7360d-297">The following example shows how to use the command:</span></span>

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
<span data-ttu-id="7360d-298">La ejecución del comando anterior le proporciona las tres cadenas como sigue:</span><span class="sxs-lookup"><span data-stu-id="7360d-298">Executing the preceding command gives you the three strings as follows:</span></span>

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

<span data-ttu-id="7360d-299">El nombre de sujeto del certificado debe coincidir con el dominio usado para acceder al clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7360d-299">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="7360d-300">Esta coincidencia es necesaria para proporcionar SSL a los puntos de conexión de administración HTTPS y de Service Fabric Explorer del clúster.</span><span class="sxs-lookup"><span data-stu-id="7360d-300">This match is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="7360d-301">No puede obtener un certificado SSL de una entidad de certificación (CA) para el dominio `.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="7360d-301">You cannot obtain an SSL certificate from a CA for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="7360d-302">Debe adquirir un nombre de dominio personalizado para el clúster.</span><span class="sxs-lookup"><span data-stu-id="7360d-302">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="7360d-303">Cuando solicite un certificado de una CA, el nombre de sujeto del certificado debe coincidir con el nombre del dominio personalizado del clúster.</span><span class="sxs-lookup"><span data-stu-id="7360d-303">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="7360d-304">Estos nombres de sujeto son las entradas necesarias para crear un clúster seguro de Service Fabric (sin Azure AD) tal y como se describe en [Configuración de los parámetros de plantilla de Resource Manager](#configure-arm).</span><span class="sxs-lookup"><span data-stu-id="7360d-304">These subject names are the entries you need to create a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span></span> <span data-ttu-id="7360d-305">Puede conectarse al clúster seguro mediante las instrucciones de [autenticación del acceso de cliente a un clúster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="7360d-305">You can connect to the secure cluster by following the instructions for [authenticating client access to a cluster](service-fabric-connect-to-secure-cluster.md).</span></span> <span data-ttu-id="7360d-306">Los clústeres de versión preliminar de Linux no admiten la autenticación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7360d-306">Linux preview clusters do not support Azure AD authentication.</span></span> <span data-ttu-id="7360d-307">Puede asignar roles de administrador y cliente como se indica en la sección [Asignación de usuarios a roles](#assign-roles).</span><span class="sxs-lookup"><span data-stu-id="7360d-307">You can assign admin and client roles as described in the [Assign roles to users](#assign-roles) section.</span></span> <span data-ttu-id="7360d-308">Al especificar los roles de administrador y cliente para un clúster de versión preliminar de Linux, tendrá que proporcionar huellas digitales de certificado para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="7360d-308">When you specify admin and client roles for a Linux preview cluster, you have to provide certificate thumbprints for authentication.</span></span> <span data-ttu-id="7360d-309">(No proporciona el nombre del sujeto, ya que no se realiza ninguna validación o revocación de la cadena en esta versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="7360d-309">(You do not provide the subject name, because no chain validation or revocation is being performed in this preview release.)</span></span>

<span data-ttu-id="7360d-310">Si desea usar un certificado autofirmado para pruebas, puede usar el mismo script para generar uno.</span><span class="sxs-lookup"><span data-stu-id="7360d-310">If you want to use a self-signed certificate for testing, you can use the same script to generate one.</span></span> <span data-ttu-id="7360d-311">A continuación, puede cargar el certificado en el almacén de claves al proporcionar la marca `ss` en lugar de proporcionar la ruta de acceso y el nombre del certificado.</span><span class="sxs-lookup"><span data-stu-id="7360d-311">You can then upload the certificate to your key vault by providing the flag `ss` instead of providing the certificate path and certificate name.</span></span> <span data-ttu-id="7360d-312">Por ejemplo, observe el siguiente comando para crear y cargar un certificado autofirmado:</span><span class="sxs-lookup"><span data-stu-id="7360d-312">For example, see the following command for creating and uploading a self-signed certificate:</span></span>

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
<span data-ttu-id="7360d-313">Este comando devuelve las mismas tres cadenas: SourceVault, CertificateUrl y CertificateThumbprint.</span><span class="sxs-lookup"><span data-stu-id="7360d-313">This command returns the same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span></span> <span data-ttu-id="7360d-314">A continuación, puede usar las cadenas para crear un clúster de Linux seguro y una ubicación donde colocar el certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="7360d-314">You can then use the strings to create both a secure Linux cluster and a location where the self-signed certificate is placed.</span></span> <span data-ttu-id="7360d-315">Necesita el certificado autofirmado para conectarse al clúster.</span><span class="sxs-lookup"><span data-stu-id="7360d-315">You need the self-signed certificate to connect to the cluster.</span></span> <span data-ttu-id="7360d-316">Puede conectarse al clúster seguro mediante las instrucciones de [autenticación del acceso de cliente a un clúster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="7360d-316">You can connect to the secure cluster by following the instructions for [authenticating client access to a cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="7360d-317">El nombre de sujeto del certificado debe coincidir con el dominio usado para acceder al clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7360d-317">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="7360d-318">Esta coincidencia es necesaria para proporcionar SSL a los puntos de conexión de administración HTTPS y de Service Fabric Explorer del clúster.</span><span class="sxs-lookup"><span data-stu-id="7360d-318">This match is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="7360d-319">No puede obtener un certificado SSL de una entidad de certificación (CA) para el dominio `.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="7360d-319">You cannot obtain an SSL certificate from a CA for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="7360d-320">Debe adquirir un nombre de dominio personalizado para el clúster.</span><span class="sxs-lookup"><span data-stu-id="7360d-320">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="7360d-321">Cuando solicite un certificado de una CA, el nombre de sujeto del certificado debe coincidir con el nombre del dominio personalizado del clúster.</span><span class="sxs-lookup"><span data-stu-id="7360d-321">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="7360d-322">Puede rellenar los parámetros del script auxiliar en Azure Portal, como se describe en la sección [Creación de un clúster en Azure Portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="7360d-322">You can fill the parameters from the helper script in the Azure portal, as described in the [Create a cluster in the Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7360d-323">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7360d-323">Next steps</span></span>
<span data-ttu-id="7360d-324">En este punto, tiene un clúster seguro con autenticación de Azure Active Directory que proporciona autenticación de administración.</span><span class="sxs-lookup"><span data-stu-id="7360d-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span></span> <span data-ttu-id="7360d-325">Después, [conéctese al clúster](service-fabric-connect-to-secure-cluster.md) y aprenda a [administrar secretos de aplicación](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="7360d-325">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span></span>

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="7360d-326">Solución de problemas de configuración de Azure Active Directory para la autenticación de cliente</span><span class="sxs-lookup"><span data-stu-id="7360d-326">Troubleshoot setting up Azure Active Directory for client authentication</span></span>
<span data-ttu-id="7360d-327">Si experimenta algún problema al configurar Azure AD para la autenticación de cliente, revise las posibles soluciones de esta sección.</span><span class="sxs-lookup"><span data-stu-id="7360d-327">If you run into an issue while you're setting up Azure AD for client authentication, review the potential solutions in this section.</span></span>

### <a name="service-fabric-explorer-prompts-you-to-select-a-certificate"></a><span data-ttu-id="7360d-328">Service Fabric Explorer le solicita que seleccione el certificado</span><span class="sxs-lookup"><span data-stu-id="7360d-328">Service Fabric Explorer prompts you to select a certificate</span></span>
#### <a name="problem"></a><span data-ttu-id="7360d-329">Problema</span><span class="sxs-lookup"><span data-stu-id="7360d-329">Problem</span></span>
<span data-ttu-id="7360d-330">Después de conectarse correctamente a Azure AD en Service Fabric Explorer, el explorador vuelve a la página principal, pero un mensaje le pide que seleccione un certificado.</span><span class="sxs-lookup"><span data-stu-id="7360d-330">After you sign in successfully to Azure AD in Service Fabric Explorer, the browser returns to the home page but a message prompts you to select a certificate.</span></span>

![Cuadro de diálogo de selección de certificado de SFX][sfx-select-certificate-dialog]

#### <a name="reason"></a><span data-ttu-id="7360d-332">Motivo</span><span class="sxs-lookup"><span data-stu-id="7360d-332">Reason</span></span>
<span data-ttu-id="7360d-333">Al usuario no se le ha asignado un rol en la aplicación de clúster de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7360d-333">The user isn’t assigned a role in the Azure AD cluster application.</span></span> <span data-ttu-id="7360d-334">Por tanto, se produce un error en la autenticación de Azure AD en el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7360d-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span></span> <span data-ttu-id="7360d-335">Service Fabric Explorer recurre a la autenticación de certificado.</span><span class="sxs-lookup"><span data-stu-id="7360d-335">Service Fabric Explorer falls back to certificate authentication.</span></span>

#### <a name="solution"></a><span data-ttu-id="7360d-336">Solución</span><span class="sxs-lookup"><span data-stu-id="7360d-336">Solution</span></span>
<span data-ttu-id="7360d-337">Siga las instrucciones de configuración de Azure AD y de asignación de roles de usuario.</span><span class="sxs-lookup"><span data-stu-id="7360d-337">Follow the instructions for setting up Azure AD, and assign user roles.</span></span> <span data-ttu-id="7360d-338">Además, se recomienda activar "Asignación de usuario necesaria para acceder a la aplicación", como hace `SetupApplications.ps1`.</span><span class="sxs-lookup"><span data-stu-id="7360d-338">Also, we recommend that you turn on “User assignment required to access app,” as `SetupApplications.ps1` does.</span></span>

### <a name="connection-with-powershell-fails-with-an-error-the-specified-credentials-are-invalid"></a><span data-ttu-id="7360d-339">Error de conexión con PowerShell: "Las credenciales especificadas no son válidas"</span><span class="sxs-lookup"><span data-stu-id="7360d-339">Connection with PowerShell fails with an error: "The specified credentials are invalid"</span></span>
#### <a name="problem"></a><span data-ttu-id="7360d-340">Problema</span><span class="sxs-lookup"><span data-stu-id="7360d-340">Problem</span></span>
<span data-ttu-id="7360d-341">Cuando usa PowerShell para conectarse al clúster mediante el modo de seguridad "AzureActiveDirectory", después de iniciar sesión correctamente en Azure AD, se produce un error de conexión con el mensaje "Las credenciales especificadas no son válidas".</span><span class="sxs-lookup"><span data-stu-id="7360d-341">When you use PowerShell to connect to the cluster by using “AzureActiveDirectory” security mode, after you sign in successfully to Azure AD, the connection fails with an error: "The specified credentials are invalid."</span></span>

#### <a name="solution"></a><span data-ttu-id="7360d-342">Solución</span><span class="sxs-lookup"><span data-stu-id="7360d-342">Solution</span></span>
<span data-ttu-id="7360d-343">Esta solución es la mismo que la anterior.</span><span class="sxs-lookup"><span data-stu-id="7360d-343">This solution is the same as the preceding one.</span></span>

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a><span data-ttu-id="7360d-344">Service Fabric Explorer devuelve un error al iniciar sesión: "AADSTS50011"</span><span class="sxs-lookup"><span data-stu-id="7360d-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span></span>
#### <a name="problem"></a><span data-ttu-id="7360d-345">Problema</span><span class="sxs-lookup"><span data-stu-id="7360d-345">Problem</span></span>
<span data-ttu-id="7360d-346">Al intentar iniciar sesión en Azure AD en Service Fabric Explorer, la página devuelve el error: "AADSTS50011: The reply address &lt;url&gt; does not match the reply addresses configured for the application: &lt;guid&gt;" (AADSTS50011: La dirección <url> de respuesta no coincide con las direcciones de respuesta configuradas para la aplicación: <guid>).</span><span class="sxs-lookup"><span data-stu-id="7360d-346">When you try to sign in to Azure AD in Service Fabric Explorer, the page returns a failure: "AADSTS50011: The reply address &lt;url&gt; does not match the reply addresses configured for the application: &lt;guid&gt;."</span></span>

![La dirección de respuesta SFX no coincide][sfx-reply-address-not-match]

#### <a name="reason"></a><span data-ttu-id="7360d-348">Motivo</span><span class="sxs-lookup"><span data-stu-id="7360d-348">Reason</span></span>
<span data-ttu-id="7360d-349">La aplicación del clúster (web) que representa Service Fabric Explorer intenta la autenticación en Azure AD y, como parte de la solicitud, proporciona la dirección URL de retorno de redireccionamiento.</span><span class="sxs-lookup"><span data-stu-id="7360d-349">The cluster (web) application that represents Service Fabric Explorer attempts to authenticate against Azure AD, and as part of the request it provides the redirect return URL.</span></span> <span data-ttu-id="7360d-350">Pero no aparece en la lista **URL DE RESPUESTA** de la aplicación Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7360d-350">But the URL is not listed in the Azure AD application **REPLY URL** list.</span></span>

#### <a name="solution"></a><span data-ttu-id="7360d-351">Solución</span><span class="sxs-lookup"><span data-stu-id="7360d-351">Solution</span></span>
<span data-ttu-id="7360d-352">En la pestaña **Configurar** de la aplicación del clúster (web), agregue la dirección URL de Service Fabric Explorer a la lista **URL DE RESPUESTA** o reemplace uno de los elementos de la lista.</span><span class="sxs-lookup"><span data-stu-id="7360d-352">On the **Configure** tab of the cluster (web) application, add the URL of Service Fabric Explorer to the **REPLY URL** list or replace one of the items in the list.</span></span> <span data-ttu-id="7360d-353">Cuando haya terminado, guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="7360d-353">When you have finished, save your change.</span></span>

![Dirección URL de respuesta de la aplicación web][web-application-reply-url]

### <a name="connect-the-cluster-by-using-azure-ad-authentication-via-powershell"></a><span data-ttu-id="7360d-355">Conexión del clúster mediante la autenticación de Azure AD a través de PowerShell</span><span class="sxs-lookup"><span data-stu-id="7360d-355">Connect the cluster by using Azure AD authentication via PowerShell</span></span>
<span data-ttu-id="7360d-356">Para conectar el clúster de Service Fabric, use el siguiente ejemplo de comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7360d-356">To connect the Service Fabric cluster, use the following PowerShell command example:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

<span data-ttu-id="7360d-357">Para más información sobre el cmdlet Connect-ServiceFabricCluster, consulte [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span><span class="sxs-lookup"><span data-stu-id="7360d-357">To learn about the Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span></span>

### <a name="can-i-reuse-the-same-azure-ad-tenant-in-multiple-clusters"></a><span data-ttu-id="7360d-358">¿Se puede reutilizar el mismo inquilino de Azure AD para varios clústeres?</span><span class="sxs-lookup"><span data-stu-id="7360d-358">Can I reuse the same Azure AD tenant in multiple clusters?</span></span>
<span data-ttu-id="7360d-359">Sí.</span><span class="sxs-lookup"><span data-stu-id="7360d-359">Yes.</span></span> <span data-ttu-id="7360d-360">Pero recuerde agregar la dirección URL de Service Fabric Explorer a la aplicación del clúster (web).</span><span class="sxs-lookup"><span data-stu-id="7360d-360">But remember to add the URL of Service Fabric Explorer to your cluster (web) application.</span></span> <span data-ttu-id="7360d-361">De lo contrario, Service Fabric Explorer no funciona.</span><span class="sxs-lookup"><span data-stu-id="7360d-361">Otherwise, Service Fabric Explorer doesn’t work.</span></span>

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a><span data-ttu-id="7360d-362">¿Por qué todavía necesito el certificado de servidor con Azure AD habilitado?</span><span class="sxs-lookup"><span data-stu-id="7360d-362">Why do I still need a server certificate while Azure AD is enabled?</span></span>
<span data-ttu-id="7360d-363">FabricClient y FabricGateway realizan una autenticación mutua.</span><span class="sxs-lookup"><span data-stu-id="7360d-363">FabricClient and FabricGateway perform a mutual authentication.</span></span> <span data-ttu-id="7360d-364">Durante la autenticación de Azure AD, la integración de Azure AD proporciona la identidad del cliente al servidor y el certificado de servidor se utiliza para comprobar la identidad del servidor.</span><span class="sxs-lookup"><span data-stu-id="7360d-364">During Azure AD authentication, Azure AD integration provides a client identity to the server, and the server certificate is used to verify the server identity.</span></span> <span data-ttu-id="7360d-365">Para más información sobre cómo funciona el certificado en Service Fabric, consulte [Certificados X.509 y Service Fabric][x509-certificates-and-service-fabric].</span><span class="sxs-lookup"><span data-stu-id="7360d-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span></span>

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

