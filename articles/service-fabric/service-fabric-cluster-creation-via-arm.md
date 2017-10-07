---
title: "clúster de aaaCreate un tejido de servicio de Azure desde una plantilla | Documentos de Microsoft"
description: "Este artículo describe cómo tooset seguridad un tejido segura de servicio de clúster en Azure mediante el uso de Azure Resource Manager, el almacén de claves de Azure y Azure Active Directory (Azure AD) para la autenticación de cliente."
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
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a><span data-ttu-id="9b1dd-103">Creación de un clúster de Service Fabric con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9b1dd-103">Create a Service Fabric cluster by using Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b1dd-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9b1dd-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="9b1dd-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9b1dd-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="9b1dd-106">Esta guía paso a paso le lleva por la configuración de un clúster seguro de Azure Service Fabric en Azure con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span></span> <span data-ttu-id="9b1dd-107">Sabemos que dicho artículo hello es largo.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-107">We acknowledge that hello article is long.</span></span> <span data-ttu-id="9b1dd-108">No obstante, a menos que ya estén familiarizadas con contenido de hello, ser toofollow seguro de cada paso con cuidado.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-108">Nevertheless, unless you are already thoroughly familiar with hello content, be sure toofollow each step carefully.</span></span>

<span data-ttu-id="9b1dd-109">Guía de Hello abarca Hola procedimientos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-109">hello guide covers hello following procedures:</span></span>

* <span data-ttu-id="9b1dd-110">Cómo configurar un certificados tooupload de almacén de claves de Azure para la seguridad de clúster y la aplicación</span><span class="sxs-lookup"><span data-stu-id="9b1dd-110">Setting up an Azure key vault tooupload certificates for cluster and application security</span></span>
* <span data-ttu-id="9b1dd-111">Creación de un clúster protegido en Azure con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9b1dd-111">Creating a secured cluster in Azure by using Azure Resource Manager</span></span>
* <span data-ttu-id="9b1dd-112">Autenticación de usuarios con Azure Active Directory (Azure AD) para la administración del clúster</span><span class="sxs-lookup"><span data-stu-id="9b1dd-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span></span>

<span data-ttu-id="9b1dd-113">Un clúster seguro es un clúster que evite las operaciones de toomanagement de acceso no autorizado.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-113">A secure cluster is a cluster that prevents unauthorized access toomanagement operations.</span></span> <span data-ttu-id="9b1dd-114">Esto incluye implementar, actualizar y eliminar aplicaciones, servicios y datos de Hola que contienen.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-114">This includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="9b1dd-115">Un clúster es un clúster que cualquiera puede conectarse tooat en cualquier momento y realizar operaciones de administración.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-115">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="9b1dd-116">Aunque es posible toocreate un clúster no seguro, se recomienda que cree un clúster seguro desde el principio de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-116">Although it is possible toocreate an unsecure cluster, we highly recommend that you create a secure cluster from hello outset.</span></span> <span data-ttu-id="9b1dd-117">Los clústeres no seguros no se pueden proteger en un momento posterior, por lo que se debe crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span></span>

<span data-ttu-id="9b1dd-118">concepto de Hola de creación de clústeres seguros se Hola mismo, independientemente de si están clústeres de Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-118">hello concept of creating secure clusters is hello same, whether they are Linux or Windows clusters.</span></span> <span data-ttu-id="9b1dd-119">Para más información y scripts auxiliares para crear clústeres seguros de Linux, consulte [Creating secure clusters on Linux](#secure-linux-clusters) (Creación de clústeres seguros en Linux).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span></span>

## <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="9b1dd-120">Inicie sesión en tooyour cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="9b1dd-120">Sign in tooyour Azure account</span></span>
<span data-ttu-id="9b1dd-121">En esta guía se usa [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="9b1dd-121">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="9b1dd-122">Cuando se inicia una nueva sesión de PowerShell, inicie sesión en tooyour cuenta de Azure y seleccione su suscripción antes de ejecutar comandos de Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-122">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>

<span data-ttu-id="9b1dd-123">Inicie sesión en tooyour cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-123">Sign in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="9b1dd-124">Seleccione su suscripción:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-124">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a><span data-ttu-id="9b1dd-125">Configuración de un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="9b1dd-125">Set up a key vault</span></span>
<span data-ttu-id="9b1dd-126">En esta sección se habla de la creación de un almacén de claves para un clúster de Service Fabric en Azure y aplicaciones de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="9b1dd-127">Para un almacén de claves de guía completa tooAzure, consulte toohello [el almacén de claves Guía de introducción][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="9b1dd-127">For a complete guide tooAzure Key Vault, refer toohello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="9b1dd-128">Service Fabric utiliza certificados X.509 toosecure un clúster y proporcionar características de seguridad de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-128">Service Fabric uses X.509 certificates toosecure a cluster and provide application security features.</span></span> <span data-ttu-id="9b1dd-129">Se utilizan certificados de toomanage de almacén de claves para los clústeres de Service Fabric en Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-129">You use Key Vault toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="9b1dd-130">Cuando se implementa un clúster de Azure, proveedor de recursos de Azure de Hola que es responsable de la creación de clústeres de Service Fabric extrae los certificados de almacén de claves y los instala en clúster de hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-130">When a cluster is deployed in Azure, hello Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="9b1dd-131">Hello siguiente diagrama ilustra Hola relación entre el almacén de claves de Azure, un clúster de Service Fabric y el proveedor de recursos de Azure de Hola que utiliza certificados almacenados en un almacén de claves cuando crea un clúster:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-131">hello following diagram illustrates hello relationship between Azure Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span></span>

![Diagrama de instalación del certificado][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="9b1dd-133">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9b1dd-133">Create a resource group</span></span>
<span data-ttu-id="9b1dd-134">Hola primer paso es toocreate un grupo de recursos específicamente para el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-134">hello first step is toocreate a resource group specifically for your key vault.</span></span> <span data-ttu-id="9b1dd-135">Se recomienda que coloque el almacén de claves de hello en su propio grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-135">We recommend that you put hello key vault into its own resource group.</span></span> <span data-ttu-id="9b1dd-136">Esta acción le permite quitar Hola cálculo y almacenamiento de grupos de recursos, incluido el grupo de recursos de Hola que contiene el clúster de Service Fabric, sin perder sus claves y secretos.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-136">This action lets you remove hello compute and storage resource groups, including hello resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="9b1dd-137">grupo de recursos de Hola que contiene el almacén de claves _debe estar en hello misma región_ como clúster de Hola que lo está usando.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-137">hello resource group that contains your key vault _must be in hello same region_ as hello cluster that is using it.</span></span>

<span data-ttu-id="9b1dd-138">Si tiene previsto toodeploy clústeres en varias regiones, sugerimos que nombre de grupo de recursos de Hola y el almacén de claves de Hola de manera que indica qué región al que pertenece.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-138">If you plan toodeploy clusters in multiple regions, we suggest that you name hello resource group and hello key vault in a way that indicates which region it belongs to.</span></span>  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
<span data-ttu-id="9b1dd-139">salida de Hello debería tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-139">hello output should look like this:</span></span>

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a><span data-ttu-id="9b1dd-140">Crear un almacén de claves en el nuevo grupo de recursos Hola</span><span class="sxs-lookup"><span data-stu-id="9b1dd-140">Create a key vault in hello new resource group</span></span>
<span data-ttu-id="9b1dd-141">almacén de claves de Hello _debe estar habilitada para la implementación_ tooallow Hola proceso recursos proveedor tooget certificados de él y lo instala en instancias de máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-141">hello key vault _must be enabled for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on virtual machine instances:</span></span>

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

<span data-ttu-id="9b1dd-142">salida de Hello debería tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-142">hello output should look like this:</span></span>

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
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a><span data-ttu-id="9b1dd-143">Uso de un almacén de claves existente</span><span class="sxs-lookup"><span data-stu-id="9b1dd-143">Use an existing key vault</span></span>

<span data-ttu-id="9b1dd-144">toouse un almacén de claves existente, se _debe habilitarla para la implementación_ tooallow Hola proceso recursos proveedor tooget certificados de él y lo instala en nodos de clúster:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-144">toouse an existing key vault, you _must enable it for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on cluster nodes:</span></span>

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a><span data-ttu-id="9b1dd-145">Agregar el almacén de claves de certificados tooyour</span><span class="sxs-lookup"><span data-stu-id="9b1dd-145">Add certificates tooyour key vault</span></span>

<span data-ttu-id="9b1dd-146">Los certificados se utilizan en toosecure de autenticación y cifrado de Service Fabric tooprovide diversos aspectos de un clúster y sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-146">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="9b1dd-147">Para obtener más información sobre el modo en que se usan los certificados en Service Fabric, consulte los [Escenarios de seguridad de los clústeres de Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="9b1dd-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="9b1dd-148">Certificado de clúster y servidor (obligatorio)</span><span class="sxs-lookup"><span data-stu-id="9b1dd-148">Cluster and server certificate (required)</span></span>
<span data-ttu-id="9b1dd-149">Este certificado es necesario toosecure un clúster y evitar tooit de acceso no autorizado.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-149">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="9b1dd-150">Ofrece seguridad al clúster de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-150">It provides cluster security in two ways:</span></span>

* <span data-ttu-id="9b1dd-151">Autenticación del clúster: se autentica la comunicación de nodo a nodo para la federación del clúster.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="9b1dd-152">Sólo los nodos que se pueden demostrar su identidad con este certificado pueden unirse a clústeres de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-152">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="9b1dd-153">Autenticación de servidor: autentica el cliente de administración de la tooa de los puntos de conexión de administración con hello clúster, por lo que hello administración cliente sabe está hablando clúster real toohello.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-153">Server authentication: Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="9b1dd-154">Este certificado también proporciona un SSL para hello API de administración de HTTPS y para Service Fabric Explorer a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-154">This certificate also provides an SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="9b1dd-155">tooserve estos fines, certificado Hola debe cumplir Hola según los requisitos:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-155">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="9b1dd-156">certificado de Hello debe contener una clave privada.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-156">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="9b1dd-157">certificado de Hello debe crearse para el intercambio de claves, que es exportable tooa archivo de intercambio de información Personal (.pfx).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-157">hello certificate must be created for key exchange, which is exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="9b1dd-158">nombre de sujeto del certificado de Hello debe coincidir con dominio Hola que usar clúster de Service Fabric tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-158">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="9b1dd-159">La coincidencia distingue tooprovide requiere SSL para extremos de administración del clúster de hello HTTPS y el Explorador de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-159">This matching is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="9b1dd-160">No se puede obtener un certificado SSL de una entidad de certificación (CA) para hello. cloudapp.azure.com dominio.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-160">You cannot obtain an SSL certificate from a certificate authority (CA) for hello .cloudapp.azure.com domain.</span></span> <span data-ttu-id="9b1dd-161">Debe adquirir un nombre de dominio personalizado para el clúster.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-161">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="9b1dd-162">Cuando solicite un certificado de una entidad de certificación, hello nombre de sujeto del certificado debe coincidir con nombre de dominio personalizado de Hola que usa para el clúster.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-162">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

### <a name="application-certificates-optional"></a><span data-ttu-id="9b1dd-163">Certificados de aplicación (opcionales)</span><span class="sxs-lookup"><span data-stu-id="9b1dd-163">Application certificates (optional)</span></span>
<span data-ttu-id="9b1dd-164">Se puede instalar un número cualquiera de certificados adicionales en un clúster para proteger la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="9b1dd-165">Antes de crear el clúster, considere la posibilidad de escenarios de seguridad de aplicación Hola que requieren un toobe de certificados instalado en nodos de hello, como:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-165">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="9b1dd-166">Cifrado y descifrado de los valores de configuración de aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-166">Encryption and decryption of application configuration values.</span></span>
* <span data-ttu-id="9b1dd-167">Cifrado de datos entre nodos durante la replicación.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-167">Encryption of data across nodes during replication.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="9b1dd-168">Formato de certificados para el uso del proveedor de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="9b1dd-168">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="9b1dd-169">Puede agregar y usar archivos de claves privadas (.pfx) directamente a través del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-169">You can add and use private key files (.pfx) directly through your key vault.</span></span> <span data-ttu-id="9b1dd-170">Sin embargo, el proveedor de recursos de proceso de Azure de hello requiere toobe de claves que se almacenan en formato JavaScript Object Notation (JSON) especial.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-170">However, hello Azure compute resource provider requires keys toobe stored in a special JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="9b1dd-171">formato de Hello incluye archivo .pfx de hello como una cadena de cifrado de base64 base y la contraseña de clave privada de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-171">hello format includes hello .pfx file as a base 64-encoded string and hello private key password.</span></span> <span data-ttu-id="9b1dd-172">tooaccommodate del almacén de estos requisitos, Hola claves deben colocarse en una cadena JSON y, a continuación, se almacenan como "secretos" en la clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-172">tooaccommodate these requirements, hello keys must be placed in a JSON string and then stored as "secrets" in hello key vault.</span></span>

<span data-ttu-id="9b1dd-173">toomake este proceso, un [módulo de PowerShell está disponible en GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="9b1dd-173">toomake this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="9b1dd-174">módulo de hello toouse, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-174">toouse hello module, do hello following:</span></span>

1. <span data-ttu-id="9b1dd-175">Descargar contenido completo de hello del repositorio de hello en un directorio local.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-175">Download hello entire contents of hello repo into a local directory.</span></span>
2. <span data-ttu-id="9b1dd-176">Vaya toohello directorio local.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-176">Go toohello local directory.</span></span>
2. <span data-ttu-id="9b1dd-177">Importar el módulo de ServiceFabricRPHelpers de hello en la ventana de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-177">Import hello ServiceFabricRPHelpers module in your PowerShell window:</span></span>

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

<span data-ttu-id="9b1dd-178">Hola `Invoke-AddCertToKeyVault` comandos en este módulo de PowerShell da formato a una clave privada del certificado en una cadena JSON y lo carga en el almacén de claves toohello automáticamente.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-178">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it toohello key vault.</span></span> <span data-ttu-id="9b1dd-179">Usar certificado de clúster de hello comando tooadd hello y cualquier aplicación adicional certificados toohello el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-179">Use hello command tooadd hello cluster certificate and any additional application certificates toohello key vault.</span></span> <span data-ttu-id="9b1dd-180">Repita este paso para todos los certificados adicionales que desee tooinstall en el clúster.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-180">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

#### <a name="uploading-an-existing-certificate"></a><span data-ttu-id="9b1dd-181">Carga de un certificado existente</span><span class="sxs-lookup"><span data-stu-id="9b1dd-181">Uploading an existing certificate</span></span>

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

<span data-ttu-id="9b1dd-182">Si se produce un error, como Hola se muestra aquí, normalmente significa que tiene un conflicto de dirección URL del recurso.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-182">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="9b1dd-183">conflicto de hello tooresolve, cambiar el nombre de almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-183">tooresolve hello conflict, change hello key vault name.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="9b1dd-184">Después de que se resuelve el conflicto de hello, resultado de hello debería tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-184">After hello conflict is resolved, hello output should look like this:</span></span>

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
><span data-ttu-id="9b1dd-185">Necesita Hola tres anterior cadenas, CertificateThumbprint, SourceVault y CertificateURL, tooset un clúster de Service Fabric segura y tooobtain todos los certificados de aplicación puede que esté usando para la seguridad de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-185">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="9b1dd-186">Si no guarda las cadenas de hello, puede ser difícil tooretrieve ellos consultando clave Hola del almacén de versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-186">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a><span data-ttu-id="9b1dd-187">Crear un certificado autofirmado y cargarlo en el almacén de claves toohello</span><span class="sxs-lookup"><span data-stu-id="9b1dd-187">Creating a self-signed certificate and uploading it toohello key vault</span></span>

<span data-ttu-id="9b1dd-188">Si ya ha cargado el almacén de claves de certificados toohello, omita este paso.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-188">If you have already uploaded your certificates toohello key vault, skip this step.</span></span> <span data-ttu-id="9b1dd-189">Este paso es para generar un nuevo certificado autofirmado y cargarlo en el almacén de claves tooyour.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-189">This step is for generating a new self-signed certificate and uploading it tooyour key vault.</span></span> <span data-ttu-id="9b1dd-190">Después de cambiar los parámetros de hello en la siguiente secuencia de comandos de Hola y, a continuación, ejecutarlo, debe ser solicitará una contraseña de certificado.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-190">After you change hello parameters in hello following script and then run it, you should be prompted for a certificate password.</span></span>  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

<span data-ttu-id="9b1dd-191">Si se produce un error, como Hola se muestra aquí, normalmente significa que tiene un conflicto de dirección URL del recurso.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-191">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="9b1dd-192">conflicto de hello tooresolve, cambiar el nombre de almacén de claves de hello, nombre RG y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-192">tooresolve hello conflict, change hello key vault name, RG name, and so forth.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="9b1dd-193">Después de que se resuelve el conflicto de hello, resultado de hello debería tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-193">After hello conflict is resolved, hello output should look like this:</span></span>

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
><span data-ttu-id="9b1dd-194">Necesita Hola tres anterior cadenas, CertificateThumbprint, SourceVault y CertificateURL, tooset un clúster de Service Fabric segura y tooobtain todos los certificados de aplicación puede que esté usando para la seguridad de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-194">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="9b1dd-195">Si no guarda las cadenas de hello, puede ser difícil tooretrieve ellos consultando clave Hola del almacén de versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-195">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

 <span data-ttu-id="9b1dd-196">En este punto, debe tener Hola siguientes elementos en su lugar:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-196">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="9b1dd-197">grupo de recursos del almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-197">hello key vault resource group.</span></span>
* <span data-ttu-id="9b1dd-198">Hola almacén de claves y su dirección URL (denominado SourceVault en hello anterior a la salida de PowerShell).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-198">hello key vault and its URL (called SourceVault in hello preceding PowerShell output).</span></span>
* <span data-ttu-id="9b1dd-199">certificado de autenticación de servidor de clúster de Hola y su dirección URL en el almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-199">hello cluster server authentication certificate and its URL in hello key vault.</span></span>
* <span data-ttu-id="9b1dd-200">certificados de la aplicación Hello y sus direcciones URL en el almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-200">hello application certificates and their URLs in hello key vault.</span></span>


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="9b1dd-201">Configuración de Azure Active Directory para la autenticación de cliente</span><span class="sxs-lookup"><span data-stu-id="9b1dd-201">Set up Azure Active Directory for client authentication</span></span>

<span data-ttu-id="9b1dd-202">Azure AD ofrece tooapplications de acceso de usuario de toomanage organizaciones (conocido como inquilinos).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-202">Azure AD enables organizations (known as tenants) toomanage user access tooapplications.</span></span> <span data-ttu-id="9b1dd-203">Las aplicaciones se dividen en las que tienen interfaz de usuario de inicio de sesión basada en web y las que tienen una experiencia de cliente nativa.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span></span> <span data-ttu-id="9b1dd-204">En este artículo se supone que ya ha creado un inquilino.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-204">In this article, we assume that you have already created a tenant.</span></span> <span data-ttu-id="9b1dd-205">Si no fue así, empiece por leer [cómo inquilino de Azure Active Directory tooget][active-directory-howto-tenant].</span><span class="sxs-lookup"><span data-stu-id="9b1dd-205">If you have not, start by reading [How tooget an Azure Active Directory tenant][active-directory-howto-tenant].</span></span>

<span data-ttu-id="9b1dd-206">Un clúster de Service Fabric ofrece tooits de puntos de entrada varias funciones de administración, incluidos Hola basada en web [Service Fabric Explorer] [ service-fabric-visualizing-your-cluster] y [Visual Studio] [service-fabric-manage-application-in-visual-studio].</span><span class="sxs-lookup"><span data-stu-id="9b1dd-206">A Service Fabric cluster offers several entry points tooits management functionality, including hello web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span></span> <span data-ttu-id="9b1dd-207">Como resultado, crea dos Azure AD aplicaciones toocontrol acceso toohello clúster, una aplicación web y una aplicación nativa.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-207">As a result, you create two Azure AD applications toocontrol access toohello cluster, one web application and one native application.</span></span>

<span data-ttu-id="9b1dd-208">toosimplify algunos de los pasos de hello implicados en la configuración de Azure AD con un clúster de Service Fabric, hemos creado un conjunto de scripts de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-208">toosimplify some of hello steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="9b1dd-209">Debe completar Hola siguiendo los pasos antes de crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-209">You must complete hello following steps before you create hello cluster.</span></span> <span data-ttu-id="9b1dd-210">Dado que las secuencias de comandos de hello espera que los puntos de conexión y nombres de los clústeres, los valores de hello debe planearse y no los valores que ya ha creado.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-210">Because hello scripts expect cluster names and endpoints, hello values should be planned and not values that you have already created.</span></span>

1. <span data-ttu-id="9b1dd-211">[Descargar los scripts de hello] [ sf-aad-ps-script-download] tooyour equipo.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-211">[Download hello scripts][sf-aad-ps-script-download] tooyour computer.</span></span>
2. <span data-ttu-id="9b1dd-212">Menú contextual Hola archivo zip del, seleccione **propiedades**, seleccione hello **Unblock** casilla de verificación y, a continuación, haga clic en **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-212">Right-click hello zip file, select **Properties**, select hello **Unblock** check box, and then click **Apply**.</span></span>
3. <span data-ttu-id="9b1dd-213">Extraiga el archivo zip de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-213">Extract hello zip file.</span></span>
4. <span data-ttu-id="9b1dd-214">Ejecutar `SetupApplications.ps1`y proporcionar hello TenantId, nombre del clúster y WebApplicationReplyUrl como parámetros.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-214">Run `SetupApplications.ps1`, and provide hello TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span></span> <span data-ttu-id="9b1dd-215">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-215">For example:</span></span>

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    <span data-ttu-id="9b1dd-216">Puede encontrar el TenantId mediante la ejecución de comandos de PowerShell de hello `Get-AzureSubscription`.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-216">You can find your TenantId by executing hello PowerShell command `Get-AzureSubscription`.</span></span> <span data-ttu-id="9b1dd-217">Al ejecutar este comando muestra hello TenantId para cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-217">Executing this command displays hello TenantId for every subscription.</span></span>

    <span data-ttu-id="9b1dd-218">Nombre del clúster es las aplicaciones de hello Azure AD tooprefix usado creados por el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-218">ClusterName is used tooprefix hello Azure AD applications that are created by hello script.</span></span> <span data-ttu-id="9b1dd-219">No es necesario el nombre del clúster real de toomatch Hola exactamente.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-219">It does not need toomatch hello actual cluster name exactly.</span></span> <span data-ttu-id="9b1dd-220">Está previsto toomake solo lo más fácil toomap Azure AD artefactos toohello Service Fabric clúster que se utilizan con.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-220">It is intended only toomake it easier toomap Azure AD artifacts toohello Service Fabric cluster that they're being used with.</span></span>

    <span data-ttu-id="9b1dd-221">WebApplicationReplyUrl es el punto de conexión predeterminado de Hola que Azure AD devuelve tooyour a los usuarios después de que terminen de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-221">WebApplicationReplyUrl is hello default endpoint that Azure AD returns tooyour users after they finish signing in.</span></span> <span data-ttu-id="9b1dd-222">Establezca este extremo como extremo de Service Fabric Explorer hello para el clúster, cuyo valor predeterminado es:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-222">Set this endpoint as hello Service Fabric Explorer endpoint for your cluster, which by default is:</span></span>

    <span data-ttu-id="9b1dd-223">https://&lt;cluster_domain&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="9b1dd-223">https://&lt;cluster_domain&gt;:19080/Explorer</span></span>

    <span data-ttu-id="9b1dd-224">Son toosign solicitada en tooan cuenta que tenga privilegios administrativos para el inquilino de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-224">You are prompted toosign in tooan account that has administrative privileges for hello Azure AD tenant.</span></span> <span data-ttu-id="9b1dd-225">Después de iniciar la sesión, script de Hola crea hello web y aplicaciones nativas toorepresent su clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-225">After you sign in, hello script creates hello web and native applications toorepresent your Service Fabric cluster.</span></span> <span data-ttu-id="9b1dd-226">Si se examinan las aplicaciones del inquilino de Hola Hola [portal de Azure clásico][azure-classic-portal], debería ver dos entradas nuevas:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-226">If you look at hello tenant's applications in hello [Azure classic portal][azure-classic-portal], you should see two new entries:</span></span>

   * <span data-ttu-id="9b1dd-227">*ClusterName*\_Clúster</span><span class="sxs-lookup"><span data-stu-id="9b1dd-227">*ClusterName*\_Cluster</span></span>
   * <span data-ttu-id="9b1dd-228">*ClusterName*\_Cliente</span><span class="sxs-lookup"><span data-stu-id="9b1dd-228">*ClusterName*\_Client</span></span>

   <span data-ttu-id="9b1dd-229">script de Hola imprime Hola JSON requiere hello Azure Resource Manager plantilla al crear el clúster de hello en la siguiente sección hello, por lo que es una ventana de PowerShell de buena idea tookeep Hola abrir.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-229">hello script prints hello JSON required by hello Azure Resource Manager template when you create hello cluster in hello next section, so it's a good idea tookeep hello PowerShell window open.</span></span>

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a><span data-ttu-id="9b1dd-230">Creación de una plantilla de Resource Manager para el clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9b1dd-230">Create a Service Fabric cluster Resource Manager template</span></span>
<span data-ttu-id="9b1dd-231">En esta sección, Hola da como resultado de hello anterior se usan comandos de PowerShell en una plantilla de administrador de recursos de clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-231">In this section, hello outputs of hello preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span></span>

<span data-ttu-id="9b1dd-232">Plantillas de administrador de recursos de ejemplo están disponibles en hello [Galería de plantillas de inicio rápido de Azure en GitHub][azure-quickstart-templates].</span><span class="sxs-lookup"><span data-stu-id="9b1dd-232">Sample Resource Manager templates are available in hello [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span></span> <span data-ttu-id="9b1dd-233">Estas plantillas se pueden usar como punto de partida para crear la plantilla de clúster.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-233">These templates can be used as a starting point for your cluster template.</span></span>

### <a name="create-hello-resource-manager-template"></a><span data-ttu-id="9b1dd-234">Crear plantilla de administrador de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="9b1dd-234">Create hello Resource Manager template</span></span>
<span data-ttu-id="9b1dd-235">Esta guía usan hello [5 nodos clúster segura] [ service-fabric-secure-cluster-5-node-1-nodetype] plantilla de ejemplo y los parámetros de plantilla.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-235">This guide uses hello [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span></span> <span data-ttu-id="9b1dd-236">Descargar `azuredeploy.json` y `azuredeploy.parameters.json` tooyour equipo y abra ambos archivos en el editor de texto que prefiera.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` tooyour computer and open both files in your favorite text editor.</span></span>

### <a name="add-certificates"></a><span data-ttu-id="9b1dd-237">Adición de certificados</span><span class="sxs-lookup"><span data-stu-id="9b1dd-237">Add certificates</span></span>
<span data-ttu-id="9b1dd-238">Agregar plantilla de administrador de recursos de clúster de certificados tooa haciendo referencia a almacén de claves de Hola que contiene las claves de certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-238">You add certificates tooa cluster Resource Manager template by referencing hello key vault that contains hello certificate keys.</span></span> <span data-ttu-id="9b1dd-239">Se recomienda colocar los valores del almacén de claves de hello en un archivo de parámetros de plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-239">We recommend that you place hello key-vault values in a Resource Manager template parameters file.</span></span> <span data-ttu-id="9b1dd-240">Si lo hace, mantiene Hola, Administrador de recursos del archivo de plantilla reutilizable y libre de implementación de tooa específico de valores.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-240">Doing so keeps hello Resource Manager template file reusable and free of values specific tooa deployment.</span></span>

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a><span data-ttu-id="9b1dd-241">Agregar que conjuntos de escalas de máquina virtual de todos los certificados toohello osProfile</span><span class="sxs-lookup"><span data-stu-id="9b1dd-241">Add all certificates toohello virtual machine scale set osProfile</span></span>
<span data-ttu-id="9b1dd-242">Todos los certificados que se instala en el clúster de hello deben configurarse en la sección de osProfile de Hola de recurso de conjunto de escala de hello (Microsoft.Compute/virtualMachineScaleSets).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-242">Every certificate that's installed in hello cluster must be configured in hello osProfile section of hello scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span></span> <span data-ttu-id="9b1dd-243">Esta acción indica al certificado del proveedor tooinstall Hola de hello recursos en hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-243">This action instructs hello resource provider tooinstall hello certificate on hello VMs.</span></span> <span data-ttu-id="9b1dd-244">Esta instalación incluye el certificado de clúster de Hola y los certificados de seguridad de aplicación que planea toouse para las aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-244">This installation includes both hello cluster certificate and any application security certificates that you plan toouse for your applications:</span></span>

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

#### <a name="configure-hello-service-fabric-cluster-certificate"></a><span data-ttu-id="9b1dd-245">Configurar certificado de clúster de Service Fabric Hola</span><span class="sxs-lookup"><span data-stu-id="9b1dd-245">Configure hello Service Fabric cluster certificate</span></span>
<span data-ttu-id="9b1dd-246">certificado de autenticación del clúster de Hola debe configurarse en ambos recurso de clúster de Service Fabric (Microsoft.ServiceFabric/clusters) de Hola y Hola extensión Service Fabric para escalas de máquina virtual se establece en el recurso de conjunto de escala de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-246">hello cluster authentication certificate must be configured in both hello Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and hello Service Fabric extension for virtual machine scale sets in hello virtual machine scale set resource.</span></span> <span data-ttu-id="9b1dd-247">Esta disposición permite tooconfigure de proveedor de recursos de Service Fabric hello, para su uso para la autenticación de clúster y autenticación de servidor para los puntos de conexión de administración.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-247">This arrangement allows hello Service Fabric resource provider tooconfigure it for use for cluster authentication and server authentication for management endpoints.</span></span>

##### <a name="virtual-machine-scale-set-resource"></a><span data-ttu-id="9b1dd-248">Recurso de conjunto de escalado de máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-248">Virtual machine scale set resource:</span></span>
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

##### <a name="service-fabric-resource"></a><span data-ttu-id="9b1dd-249">Recurso de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-249">Service Fabric resource:</span></span>
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

### <a name="insert-azure-ad-configuration"></a><span data-ttu-id="9b1dd-250">Inserción de la configuración de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b1dd-250">Insert Azure AD configuration</span></span>
<span data-ttu-id="9b1dd-251">configuración de Hello Azure AD que creó anteriormente se puede insertar directamente en la plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-251">hello Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span></span> <span data-ttu-id="9b1dd-252">Sin embargo, se recomienda que primero extraer valores de hello en parámetros archivo tookeep Hola Administrador de recursos plantilla reutilizable y sin necesidad de implementación de tooa específico de valores.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-252">However, we recommended that you first extract hello values into a parameters file tookeep hello Resource Manager template reusable and free of values specific tooa deployment.</span></span>

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

### <span data-ttu-id="9b1dd-253"><a "configure-arm" ></a>Configuración de los parámetros de plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9b1dd-253"><a "configure-arm" ></a>Configure Resource Manager template parameters</span></span>
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
<span data-ttu-id="9b1dd-254">Por último, utilice valores de salida de hello del almacén de claves de Hola y el archivo de parámetros de Hola de toopopulate de comandos de PowerShell de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-254">Finally, use hello output values from hello key vault and Azure AD PowerShell commands toopopulate hello parameters file:</span></span>

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
<span data-ttu-id="9b1dd-255">En este punto, debe tener Hola siguientes elementos en su lugar:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-255">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="9b1dd-256">Grupo de recursos del almacén de claves</span><span class="sxs-lookup"><span data-stu-id="9b1dd-256">Key vault resource group</span></span>
  * <span data-ttu-id="9b1dd-257">Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="9b1dd-257">Key vault</span></span>
  * <span data-ttu-id="9b1dd-258">Certificado de autenticación de servidor de clúster</span><span class="sxs-lookup"><span data-stu-id="9b1dd-258">Cluster server authentication certificate</span></span>
  * <span data-ttu-id="9b1dd-259">Certificado de cifrado de datos</span><span class="sxs-lookup"><span data-stu-id="9b1dd-259">Data encipherment certificate</span></span>
* <span data-ttu-id="9b1dd-260">Inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b1dd-260">Azure Active Directory tenant</span></span>
  * <span data-ttu-id="9b1dd-261">Aplicación de Azure AD para la administración basada en web y Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="9b1dd-261">Azure AD application for web-based management and Service Fabric Explorer</span></span>
  * <span data-ttu-id="9b1dd-262">Aplicación de Azure AD para la administración de cliente nativo</span><span class="sxs-lookup"><span data-stu-id="9b1dd-262">Azure AD application for native client management</span></span>
  * <span data-ttu-id="9b1dd-263">Usuarios y roles asignados</span><span class="sxs-lookup"><span data-stu-id="9b1dd-263">Users and their assigned roles</span></span>
* <span data-ttu-id="9b1dd-264">Plantilla de Resource Manager para el clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9b1dd-264">Service Fabric cluster Resource Manager template</span></span>
  * <span data-ttu-id="9b1dd-265">Certificados configurados mediante el almacén de claves</span><span class="sxs-lookup"><span data-stu-id="9b1dd-265">Certificates configured through key vault</span></span>
  * <span data-ttu-id="9b1dd-266">Azure Active Directory configurado</span><span class="sxs-lookup"><span data-stu-id="9b1dd-266">Azure Active Directory configured</span></span>

<span data-ttu-id="9b1dd-267">Hola siguiente diagrama ilustra cómo encajan las el almacén de claves y la configuración de Azure AD en la plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-267">hello following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span></span>

![Asignación de dependencias de Resource Manager][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a><span data-ttu-id="9b1dd-269">Crear clúster Hola</span><span class="sxs-lookup"><span data-stu-id="9b1dd-269">Create hello cluster</span></span>
<span data-ttu-id="9b1dd-270">Ya estás listo toocreate clúster de hello mediante el uso de [implementación de plantilla de recursos de Azure][resource-group-template-deploy].</span><span class="sxs-lookup"><span data-stu-id="9b1dd-270">You are now ready toocreate hello cluster by using [Azure resource template deployment][resource-group-template-deploy].</span></span>

#### <a name="test-it"></a><span data-ttu-id="9b1dd-271">Pruébelo.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-271">Test it</span></span>
<span data-ttu-id="9b1dd-272">Utilice Hola después tootest de comandos de PowerShell la plantilla de administrador de recursos con un archivo de parámetros:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-272">Use hello following PowerShell command tootest your Resource Manager template with a parameters file:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a><span data-ttu-id="9b1dd-273">Impleméntelo.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-273">Deploy it</span></span>
<span data-ttu-id="9b1dd-274">Si pasa la prueba de la plantilla de hello Administrador de recursos, utilice Hola después toodeploy de comandos de PowerShell la plantilla de administrador de recursos con un archivo de parámetros:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-274">If hello Resource Manager template test passes, use hello following PowerShell command toodeploy your Resource Manager template with a parameters file:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a><span data-ttu-id="9b1dd-275">Asignar usuarios tooroles</span><span class="sxs-lookup"><span data-stu-id="9b1dd-275">Assign users tooroles</span></span>
<span data-ttu-id="9b1dd-276">Después de haber creado Hola aplicaciones toorepresent el clúster, asignar los usuarios roles toohello compatibles con Service Fabric: solo lectura y administrador. Puede asignar roles de hello mediante hello [portal de Azure clásico][azure-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="9b1dd-276">After you have created hello applications toorepresent your cluster, assign your users toohello roles supported by Service Fabric: read-only and admin. You can assign hello roles by using hello [Azure classic portal][azure-classic-portal].</span></span>

1. <span data-ttu-id="9b1dd-277">Hola portal de Azure, vaya tooyour inquilino y, a continuación, seleccione **aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-277">In hello Azure portal, go tooyour tenant, and then select **Applications**.</span></span>
2. <span data-ttu-id="9b1dd-278">Seleccione la aplicación web de hello, que tiene un nombre como `myTestCluster_Cluster`.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-278">Select hello web application, which has a name like `myTestCluster_Cluster`.</span></span>
3. <span data-ttu-id="9b1dd-279">Haga clic en hello **usuarios** ficha.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-279">Click hello **Users** tab.</span></span>
4. <span data-ttu-id="9b1dd-280">Seleccione un tooassign de usuario y, a continuación, haga clic en hello **asignar** situado en la parte inferior de Hola de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-280">Select a user tooassign, and then click hello **Assign** button at hello bottom of hello screen.</span></span>

    ![Los usuarios tooroles botón asignar][assign-users-to-roles-button]
5. <span data-ttu-id="9b1dd-282">Seleccione Hola rol tooassign toohello usuario.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-282">Select hello role tooassign toohello user.</span></span>

    ![Cuadro de diálogo "Asignar usuarios"][assign-users-to-roles-dialog]

> [!NOTE]
> <span data-ttu-id="9b1dd-284">Para más información sobre los roles de Service Fabric, consulte [Control de acceso basado en roles para clientes de Service Fabric](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-284">For more information about roles in Service Fabric, see [Role-based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a><span data-ttu-id="9b1dd-285">Creación de clústeres seguros en Linux</span><span class="sxs-lookup"><span data-stu-id="9b1dd-285">Create secure clusters on Linux</span></span>
<span data-ttu-id="9b1dd-286">proceso de hello toomake más fácil, hemos proporcionado un [script auxiliar](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-286">toomake hello process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span></span> <span data-ttu-id="9b1dd-287">Antes de usar este script auxiliar, asegúrese de que ya tiene la interfaz de la línea de comandos (CLI) de Azure instalada y se encuentra en la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span></span> <span data-ttu-id="9b1dd-288">Asegúrese de que script de Hola tiene permisos tooexecute ejecutando `chmod +x cert_helper.py` después de descargarlo.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-288">Make sure that hello script has permissions tooexecute by running `chmod +x cert_helper.py` after downloading it.</span></span> <span data-ttu-id="9b1dd-289">Hola primer paso es toosign en tooyour cuenta de Azure mediante CLI con hello `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-289">hello first step is toosign in tooyour Azure account by using CLI with hello `azure login` command.</span></span> <span data-ttu-id="9b1dd-290">Tras iniciar sesión en tooyour cuenta de Azure, use Hola auxiliar script con la entidad de certificación firmó el certificado, como Hola después del comando mostrará:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-290">After signing in tooyour Azure account, use hello helper script with your CA signed certificate, as hello following command shows:</span></span>

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

<span data-ttu-id="9b1dd-291">parámetro - ifile de Hello puede tomar un archivo .pfx o un archivo PEM como entrada, con un tipo de certificado de hello (pfx o pem o ss si es un certificado autofirmado).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-291">hello -ifile parameter can take a .pfx file or a .pem file as input, with hello certificate type (pfx or pem, or ss if it is a self-signed certificate).</span></span>
<span data-ttu-id="9b1dd-292">parámetro -h de Hello imprime texto de Ayuda de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-292">hello parameter -h prints out hello help text.</span></span>


<span data-ttu-id="9b1dd-293">Este comando devuelve Hola después de tres cadenas como salida de hello:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-293">This command returns hello following three strings as hello output:</span></span>

* <span data-ttu-id="9b1dd-294">SourceVaultID, que es el Id. de Hola para hello nueva KeyVault ResourceGroup crea automáticamente</span><span class="sxs-lookup"><span data-stu-id="9b1dd-294">SourceVaultID, which is hello ID for hello new KeyVault ResourceGroup it created for you</span></span>
* <span data-ttu-id="9b1dd-295">CertificateUrl para tener acceso a certificados de Hola</span><span class="sxs-lookup"><span data-stu-id="9b1dd-295">CertificateUrl for accessing hello certificate</span></span>
* <span data-ttu-id="9b1dd-296">CertificateThumbprint, que se utiliza para la autenticación</span><span class="sxs-lookup"><span data-stu-id="9b1dd-296">CertificateThumbprint, which is used for authentication</span></span>

<span data-ttu-id="9b1dd-297">Hola de ejemplo siguiente muestra cómo toouse Hola comando:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-297">hello following example shows how toouse hello command:</span></span>

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
<span data-ttu-id="9b1dd-298">Ejecutar Hola anterior proporciona comandos Hola tres cadenas como sigue:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-298">Executing hello preceding command gives you hello three strings as follows:</span></span>

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

<span data-ttu-id="9b1dd-299">nombre de sujeto del certificado de Hello debe coincidir con dominio Hola que usar clúster de Service Fabric tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-299">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="9b1dd-300">Esta coincidencia es tooprovide requiere SSL para extremos de administración del clúster de hello HTTPS y el Explorador de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-300">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="9b1dd-301">No se puede obtener un certificado SSL de una entidad de certificación para hello `.cloudapp.azure.com` dominio.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-301">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="9b1dd-302">Debe adquirir un nombre de dominio personalizado para el clúster.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-302">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="9b1dd-303">Cuando solicite un certificado de una entidad de certificación, hello nombre de sujeto del certificado debe coincidir con nombre de dominio personalizado de Hola que usa para el clúster.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-303">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="9b1dd-304">Estos nombres de asunto son entradas de hello necesita toocreate un clúster de Service Fabric segura (sin Azure AD), como se describe en [parámetros de plantilla de configurar el Administrador de recursos](#configure-arm).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-304">These subject names are hello entries you need toocreate a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span></span> <span data-ttu-id="9b1dd-305">Puede conectarse toohello segura clúster siguiendo las instrucciones de Hola de [clúster de tooa de acceso de cliente de autenticación](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-305">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span> <span data-ttu-id="9b1dd-306">Los clústeres de versión preliminar de Linux no admiten la autenticación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-306">Linux preview clusters do not support Azure AD authentication.</span></span> <span data-ttu-id="9b1dd-307">Puede asignar roles de administrador y cliente tal y como se describe en hello [asignar roles toousers](#assign-roles) sección.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-307">You can assign admin and client roles as described in hello [Assign roles toousers](#assign-roles) section.</span></span> <span data-ttu-id="9b1dd-308">Al especificar los roles de administrador y cliente para un clúster de vista previa de Linux, deberá tooprovide huellas digitales de certificado para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-308">When you specify admin and client roles for a Linux preview cluster, you have tooprovide certificate thumbprints for authentication.</span></span> <span data-ttu-id="9b1dd-309">(No proporciona nombre del asunto Hola, porque no hay validación de la cadena o la revocación se realiza en esta versión preliminar.)</span><span class="sxs-lookup"><span data-stu-id="9b1dd-309">(You do not provide hello subject name, because no chain validation or revocation is being performed in this preview release.)</span></span>

<span data-ttu-id="9b1dd-310">Si desea toouse un certificado autofirmado para pruebas, puede usar Hola mismo toogenerate script uno.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-310">If you want toouse a self-signed certificate for testing, you can use hello same script toogenerate one.</span></span> <span data-ttu-id="9b1dd-311">A continuación, puede cargar el almacén de claves tooyour Hola certificado proporcionando marca hello `ss` en lugar de proporcionar el nombre de la ruta de acceso y el certificado del certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-311">You can then upload hello certificate tooyour key vault by providing hello flag `ss` instead of providing hello certificate path and certificate name.</span></span> <span data-ttu-id="9b1dd-312">Por ejemplo, vea el siguiente comando para crear y cargar un certificado autofirmado de hello:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-312">For example, see hello following command for creating and uploading a self-signed certificate:</span></span>

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
<span data-ttu-id="9b1dd-313">Este comando devuelve Hola mismas tres cadenas: SourceVault, CertificateUrl y CertificateThumbprint.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-313">This command returns hello same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span></span> <span data-ttu-id="9b1dd-314">A continuación, puede usar Hola cadenas toocreate un clúster de Linux segura y una ubicación donde se coloca el certificado autofirmado de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-314">You can then use hello strings toocreate both a secure Linux cluster and a location where hello self-signed certificate is placed.</span></span> <span data-ttu-id="9b1dd-315">Necesita tooconnect toohello clúster de hello certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-315">You need hello self-signed certificate tooconnect toohello cluster.</span></span> <span data-ttu-id="9b1dd-316">Puede conectarse toohello segura clúster siguiendo las instrucciones de Hola de [clúster de tooa de acceso de cliente de autenticación](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-316">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="9b1dd-317">nombre de sujeto del certificado de Hello debe coincidir con dominio Hola que usar clúster de Service Fabric tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-317">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="9b1dd-318">Esta coincidencia es tooprovide requiere SSL para extremos de administración del clúster de hello HTTPS y el Explorador de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-318">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="9b1dd-319">No se puede obtener un certificado SSL de una entidad de certificación para hello `.cloudapp.azure.com` dominio.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-319">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="9b1dd-320">Debe adquirir un nombre de dominio personalizado para el clúster.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-320">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="9b1dd-321">Cuando solicite un certificado de una entidad de certificación, hello nombre de sujeto del certificado debe coincidir con nombre de dominio personalizado de Hola que usa para el clúster.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-321">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="9b1dd-322">Puede rellenar parámetros Hola desde un script de aplicación auxiliar de Hola Hola portal de Azure, como se describe en hello [crear un clúster en el portal de Azure hello](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) sección.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-322">You can fill hello parameters from hello helper script in hello Azure portal, as described in hello [Create a cluster in hello Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b1dd-323">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b1dd-323">Next steps</span></span>
<span data-ttu-id="9b1dd-324">En este punto, tiene un clúster seguro con autenticación de Azure Active Directory que proporciona autenticación de administración.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span></span> <span data-ttu-id="9b1dd-325">Después, [conectar clúster tooyour](service-fabric-connect-to-secure-cluster.md) y obtenga información acerca de cómo demasiado[administrar secretos de aplicación](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-325">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="9b1dd-326">Solución de problemas de configuración de Azure Active Directory para la autenticación de cliente</span><span class="sxs-lookup"><span data-stu-id="9b1dd-326">Troubleshoot setting up Azure Active Directory for client authentication</span></span>
<span data-ttu-id="9b1dd-327">Si surge un problema mientras se está configurando Azure AD para la autenticación de cliente, revise las posibles soluciones de hello en esta sección.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-327">If you run into an issue while you're setting up Azure AD for client authentication, review hello potential solutions in this section.</span></span>

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a><span data-ttu-id="9b1dd-328">Explorador de Service Fabric solicita tooselect un certificado</span><span class="sxs-lookup"><span data-stu-id="9b1dd-328">Service Fabric Explorer prompts you tooselect a certificate</span></span>
#### <a name="problem"></a><span data-ttu-id="9b1dd-329">Problema</span><span class="sxs-lookup"><span data-stu-id="9b1dd-329">Problem</span></span>
<span data-ttu-id="9b1dd-330">Después de iniciar sesión en correctamente tooAzure AD en el Explorador de Service Fabric, explorador Hola devuelve una página de inicio de toohello pero un mensaje le pedirá tooselect un certificado.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-330">After you sign in successfully tooAzure AD in Service Fabric Explorer, hello browser returns toohello home page but a message prompts you tooselect a certificate.</span></span>

![Cuadro de diálogo de selección de certificado de SFX][sfx-select-certificate-dialog]

#### <a name="reason"></a><span data-ttu-id="9b1dd-332">Motivo</span><span class="sxs-lookup"><span data-stu-id="9b1dd-332">Reason</span></span>
<span data-ttu-id="9b1dd-333">usuario de Hello no está asignado a un rol en hello aplicación de clúster de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-333">hello user isn’t assigned a role in hello Azure AD cluster application.</span></span> <span data-ttu-id="9b1dd-334">Por tanto, se produce un error en la autenticación de Azure AD en el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span></span> <span data-ttu-id="9b1dd-335">Explorador de Service Fabric vuelve toocertificate autenticación.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-335">Service Fabric Explorer falls back toocertificate authentication.</span></span>

#### <a name="solution"></a><span data-ttu-id="9b1dd-336">Solución</span><span class="sxs-lookup"><span data-stu-id="9b1dd-336">Solution</span></span>
<span data-ttu-id="9b1dd-337">Siga las instrucciones de Hola para configurar Azure AD y asignar roles de usuario.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-337">Follow hello instructions for setting up Azure AD, and assign user roles.</span></span> <span data-ttu-id="9b1dd-338">Además, se recomienda activar "Aplicación de tooaccess necesarios de asignación de usuario", como `SetupApplications.ps1` does.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-338">Also, we recommend that you turn on “User assignment required tooaccess app,” as `SetupApplications.ps1` does.</span></span>

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a><span data-ttu-id="9b1dd-339">Se produce un error en la conexión con PowerShell con un error: "¡hello especificado credenciales no son válidas"</span><span class="sxs-lookup"><span data-stu-id="9b1dd-339">Connection with PowerShell fails with an error: "hello specified credentials are invalid"</span></span>
#### <a name="problem"></a><span data-ttu-id="9b1dd-340">Problema</span><span class="sxs-lookup"><span data-stu-id="9b1dd-340">Problem</span></span>
<span data-ttu-id="9b1dd-341">Cuando se usa PowerShell tooconnect toohello clúster mediante el modo de seguridad de "AzureActiveDirectory", después de iniciar sesión en correctamente tooAzure AD, conexión Hola produce un error: "¡hello especifica credenciales no son válidas."</span><span class="sxs-lookup"><span data-stu-id="9b1dd-341">When you use PowerShell tooconnect toohello cluster by using “AzureActiveDirectory” security mode, after you sign in successfully tooAzure AD, hello connection fails with an error: "hello specified credentials are invalid."</span></span>

#### <a name="solution"></a><span data-ttu-id="9b1dd-342">Solución</span><span class="sxs-lookup"><span data-stu-id="9b1dd-342">Solution</span></span>
<span data-ttu-id="9b1dd-343">Esta solución es hello que igual Hola anteriores.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-343">This solution is hello same as hello preceding one.</span></span>

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a><span data-ttu-id="9b1dd-344">Service Fabric Explorer devuelve un error al iniciar sesión: "AADSTS50011"</span><span class="sxs-lookup"><span data-stu-id="9b1dd-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span></span>
#### <a name="problem"></a><span data-ttu-id="9b1dd-345">Problema</span><span class="sxs-lookup"><span data-stu-id="9b1dd-345">Problem</span></span>
<span data-ttu-id="9b1dd-346">Cuando intente toosign en tooAzure AD en el Explorador de Service Fabric, página de Hola que devuelva un error: "AADSTS50011: Hola dirección de respuesta &lt;url&gt; no coincide con direcciones de respuesta de hello configuradas para la aplicación hello: &lt;guid&gt;."</span><span class="sxs-lookup"><span data-stu-id="9b1dd-346">When you try toosign in tooAzure AD in Service Fabric Explorer, hello page returns a failure: "AADSTS50011: hello reply address &lt;url&gt; does not match hello reply addresses configured for hello application: &lt;guid&gt;."</span></span>

![La dirección de respuesta SFX no coincide][sfx-reply-address-not-match]

#### <a name="reason"></a><span data-ttu-id="9b1dd-348">Motivo</span><span class="sxs-lookup"><span data-stu-id="9b1dd-348">Reason</span></span>
<span data-ttu-id="9b1dd-349">aplicación de clúster (web) de Hola que representa el Explorador de Service Fabric trata tooauthenticate en Azure AD y, como parte de la solicitud de hello proporciona Hola de dirección URL de redireccionamiento de retorno.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-349">hello cluster (web) application that represents Service Fabric Explorer attempts tooauthenticate against Azure AD, and as part of hello request it provides hello redirect return URL.</span></span> <span data-ttu-id="9b1dd-350">Pero la dirección URL de hello no aparece en la aplicación hello Azure AD **dirección URL de respuesta** lista.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-350">But hello URL is not listed in hello Azure AD application **REPLY URL** list.</span></span>

#### <a name="solution"></a><span data-ttu-id="9b1dd-351">Solución</span><span class="sxs-lookup"><span data-stu-id="9b1dd-351">Solution</span></span>
<span data-ttu-id="9b1dd-352">En hello **configurar** ficha de hello aplicación (web) de clúster, agregue Hola dirección URL del explorador de Service Fabric toohello **dirección URL de respuesta** lista o reemplazar uno de los elementos de hello en lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-352">On hello **Configure** tab of hello cluster (web) application, add hello URL of Service Fabric Explorer toohello **REPLY URL** list or replace one of hello items in hello list.</span></span> <span data-ttu-id="9b1dd-353">Cuando haya terminado, guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-353">When you have finished, save your change.</span></span>

![Dirección URL de respuesta de la aplicación web][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a><span data-ttu-id="9b1dd-355">Conecta el clúster de hello mediante la autenticación de Azure AD a través de PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b1dd-355">Connect hello cluster by using Azure AD authentication via PowerShell</span></span>
<span data-ttu-id="9b1dd-356">Hola tooconnect clúster de Service Fabric, utilice Hola siguiente ejemplo de comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-356">tooconnect hello Service Fabric cluster, use hello following PowerShell command example:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

<span data-ttu-id="9b1dd-357">toolearn sobre cmdlet Connect-ServiceFabricCluster hello, consulte [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-357">toolearn about hello Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span></span>

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a><span data-ttu-id="9b1dd-358">¿Puedo volver a usar a inquilino Hola misma instancia de Azure AD en varios clústeres?</span><span class="sxs-lookup"><span data-stu-id="9b1dd-358">Can I reuse hello same Azure AD tenant in multiple clusters?</span></span>
<span data-ttu-id="9b1dd-359">Sí.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-359">Yes.</span></span> <span data-ttu-id="9b1dd-360">Pero recuerde que aplicación de clúster (web) de tooyour de tooadd hello dirección URL del explorador de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-360">But remember tooadd hello URL of Service Fabric Explorer tooyour cluster (web) application.</span></span> <span data-ttu-id="9b1dd-361">De lo contrario, Service Fabric Explorer no funciona.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-361">Otherwise, Service Fabric Explorer doesn’t work.</span></span>

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a><span data-ttu-id="9b1dd-362">¿Por qué todavía necesito el certificado de servidor con Azure AD habilitado?</span><span class="sxs-lookup"><span data-stu-id="9b1dd-362">Why do I still need a server certificate while Azure AD is enabled?</span></span>
<span data-ttu-id="9b1dd-363">FabricClient y FabricGateway realizan una autenticación mutua.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-363">FabricClient and FabricGateway perform a mutual authentication.</span></span> <span data-ttu-id="9b1dd-364">Durante la autenticación de Azure AD, integración de Azure AD proporciona a un cliente de servidor de toohello de identidad y certificado de servidor de hello es la identidad del servidor hello tooverify usado.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-364">During Azure AD authentication, Azure AD integration provides a client identity toohello server, and hello server certificate is used tooverify hello server identity.</span></span> <span data-ttu-id="9b1dd-365">Para más información sobre cómo funciona el certificado en Service Fabric, consulte [Certificados X.509 y Service Fabric][x509-certificates-and-service-fabric].</span><span class="sxs-lookup"><span data-stu-id="9b1dd-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span></span>

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

