---
title: "clúster de Service Fabric aaaCreate en hello portal de Azure | Documentos de Microsoft"
description: "Este artículo describe cómo tooset un clúster de Service Fabric segura en Azure mediante Hola portal de Azure y el almacén de claves de Azure."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a><span data-ttu-id="97bfc-103">Crear un clúster de Service Fabric en Azure con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="97bfc-103">Create a Service Fabric cluster in Azure using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97bfc-104">Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="97bfc-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="97bfc-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="97bfc-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
> 
> 

<span data-ttu-id="97bfc-106">Esta es una guía paso a paso que le guiará por los pasos de Hola de configuración de un clúster de Service Fabric seguro en Azure con hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="97bfc-106">This is a step-by-step guide that walks you through hello steps of setting up a secure Service Fabric cluster in Azure using hello Azure portal.</span></span> <span data-ttu-id="97bfc-107">Esta guía describen Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="97bfc-107">This guide walks you through hello following steps:</span></span>

* <span data-ttu-id="97bfc-108">Configure el almacén de claves toomanage claves para seguridad de clúster.</span><span class="sxs-lookup"><span data-stu-id="97bfc-108">Set up Key Vault toomanage keys for cluster security.</span></span>
* <span data-ttu-id="97bfc-109">Crear un clúster protegido en Azure a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="97bfc-109">Create a secured cluster in Azure through hello Azure portal.</span></span>
* <span data-ttu-id="97bfc-110">Autenticación de los administradores mediante certificados.</span><span class="sxs-lookup"><span data-stu-id="97bfc-110">Authenticate administrators using certificates.</span></span>

> [!NOTE]
> <span data-ttu-id="97bfc-111">Para información sobre opciones de seguridad más avanzadas, como la autenticación de usuarios con Azure Active Directory y la configuración de certificados para la seguridad de las aplicaciones, [cree el clúster mediante Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="97bfc-111">For more advanced security options, such as user authentication with Azure Active Directory and setting up certificates for application security, [create your cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

<span data-ttu-id="97bfc-112">Un clúster seguro es un clúster que evite las operaciones de toomanagement de acceso no autorizado, que incluye implementar, actualizar y eliminar aplicaciones, servicios y datos de Hola que contienen.</span><span class="sxs-lookup"><span data-stu-id="97bfc-112">A secure cluster is a cluster that prevents unauthorized access toomanagement operations, which includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="97bfc-113">Un clúster es un clúster que cualquiera puede conectarse tooat en cualquier momento y realizar operaciones de administración.</span><span class="sxs-lookup"><span data-stu-id="97bfc-113">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="97bfc-114">Aunque es posible toocreate un clúster no seguro, es **recomienda toocreate un clúster segura**.</span><span class="sxs-lookup"><span data-stu-id="97bfc-114">Although it is possible toocreate an unsecure cluster, it is **highly recommended toocreate a secure cluster**.</span></span> <span data-ttu-id="97bfc-115">Un clúster no seguro **no se puede proteger en un momento posterior** -se debe crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="97bfc-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span></span>

<span data-ttu-id="97bfc-116">conceptos de Hola se Hola mismo para la creación de clústeres seguros, ya sea clústeres Hola son los clústeres de Linux o clústeres de Windows.</span><span class="sxs-lookup"><span data-stu-id="97bfc-116">hello concepts are hello same for creating secure clusters, whether hello clusters are Linux clusters or Windows clusters.</span></span> <span data-ttu-id="97bfc-117">Para más información y scripts de aplicaciones auxiliares para crear clústeres seguros de Linux, consulte [Creación de clústeres seguros en Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="97bfc-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span></span> <span data-ttu-id="97bfc-118">Hello parámetros obtenidos al script de aplicación auxiliar de hello proporcionado se pueden especificar directamente en el portal de hello tal y como se describe en la sección de hello [crear un clúster en el portal de Azure hello](#create-cluster-portal).</span><span class="sxs-lookup"><span data-stu-id="97bfc-118">hello parameters obtained by hello helper script provided can be input directly into hello portal as described in hello section [Create a cluster in hello Azure portal](#create-cluster-portal).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="97bfc-119">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="97bfc-119">Log in tooAzure</span></span>
<span data-ttu-id="97bfc-120">En esta guía se usa [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="97bfc-120">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="97bfc-121">Al iniciar una nueva sesión de PowerShell, inicie sesión en tooyour cuenta de Azure y seleccione su suscripción antes de ejecutar comandos de Azure.</span><span class="sxs-lookup"><span data-stu-id="97bfc-121">When starting a new PowerShell session, log in tooyour Azure account and select your subscription before executing Azure commands.</span></span>

<span data-ttu-id="97bfc-122">Inicie sesión en la cuenta de azure tooyour:</span><span class="sxs-lookup"><span data-stu-id="97bfc-122">Log in tooyour azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="97bfc-123">Seleccione su suscripción:</span><span class="sxs-lookup"><span data-stu-id="97bfc-123">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a><span data-ttu-id="97bfc-124">Configuración del Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="97bfc-124">Set up Key Vault</span></span>
<span data-ttu-id="97bfc-125">Esta parte de la Guía de hello le guía por la creación de un almacén de claves para un clúster de Service Fabric en Azure y para las aplicaciones de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="97bfc-125">This part of hello guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="97bfc-126">Para obtener una guía completa en el almacén de claves, vea hello [el almacén de claves Guía de introducción][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="97bfc-126">For a complete guide on Key Vault, see hello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="97bfc-127">Service Fabric utiliza certificados X.509 toosecure un clúster.</span><span class="sxs-lookup"><span data-stu-id="97bfc-127">Service Fabric uses X.509 certificates toosecure a cluster.</span></span> <span data-ttu-id="97bfc-128">Almacén de claves de Azure es toomanage usa certificados para los clústeres de Service Fabric en Azure.</span><span class="sxs-lookup"><span data-stu-id="97bfc-128">Azure Key Vault is used toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="97bfc-129">Cuando se implementa un clúster de Azure, proveedor de recursos de Azure de hello responsable de crear clústeres de Service Fabric extrae los certificados de almacén de claves y los instala en clúster de hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="97bfc-129">When a cluster is deployed in Azure, hello Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="97bfc-130">Hello siguiente diagrama ilustra Hola relación entre el almacén de claves, un clúster de Service Fabric y el proveedor de recursos de Azure de Hola que utiliza certificados almacenados en el almacén de claves cuando crea un clúster:</span><span class="sxs-lookup"><span data-stu-id="97bfc-130">hello following diagram illustrates hello relationship between Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span></span>

![Instalación del certificado][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="97bfc-132">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="97bfc-132">Create a Resource Group</span></span>
<span data-ttu-id="97bfc-133">Hola primer paso es toocreate un nuevo grupo de recursos específicamente para el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="97bfc-133">hello first step is toocreate a new resource group specifically for Key Vault.</span></span> <span data-ttu-id="97bfc-134">Poner el almacén de claves en su propio grupo de recursos se recomienda para que pueda quitar grupos de recursos de proceso y almacenamiento, como grupo de recursos de Hola que tiene el clúster de Service Fabric - sin perder sus claves y secretos.</span><span class="sxs-lookup"><span data-stu-id="97bfc-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as hello resource group that has your Service Fabric cluster - without losing your keys and secrets.</span></span> <span data-ttu-id="97bfc-135">grupo de recursos de Hola que tiene su almacén de claves debe estar en hello misma región que el clúster de Hola que lo está usando.</span><span class="sxs-lookup"><span data-stu-id="97bfc-135">hello resource group that has your Key Vault must be in hello same region as hello cluster that is using it.</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a><span data-ttu-id="97bfc-136">Create Key Vault</span><span class="sxs-lookup"><span data-stu-id="97bfc-136">Create Key Vault</span></span>
<span data-ttu-id="97bfc-137">Crear un almacén de claves en el nuevo grupo de recursos Hola.</span><span class="sxs-lookup"><span data-stu-id="97bfc-137">Create a Key Vault in hello new resource group.</span></span> <span data-ttu-id="97bfc-138">el almacén de claves de Hello **debe estar habilitada para la implementación** tooallow Hola certificados de tooget de proveedor de recursos de Service Fabric de ella e instalar en nodos de clúster:</span><span class="sxs-lookup"><span data-stu-id="97bfc-138">hello Key Vault **must be enabled for deployment** tooallow hello Service Fabric resource provider tooget certificates from it and install on cluster nodes:</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
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

<span data-ttu-id="97bfc-139">Si tiene un Almacén de claves existente, puede habilitarlo para implementación mediante la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="97bfc-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span></span>

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a><span data-ttu-id="97bfc-140">Agregar tooKey el almacén de certificados</span><span class="sxs-lookup"><span data-stu-id="97bfc-140">Add certificates tooKey Vault</span></span>
<span data-ttu-id="97bfc-141">Los certificados se utilizan en toosecure de autenticación y cifrado de Service Fabric tooprovide diversos aspectos de un clúster y sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="97bfc-141">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="97bfc-142">Para obtener más información sobre el modo en que se usan los certificados en Service Fabric, consulte los [Escenarios de seguridad de los clústeres de Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="97bfc-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="97bfc-143">Certificado de clúster y servidor (obligatorio)</span><span class="sxs-lookup"><span data-stu-id="97bfc-143">Cluster and server certificate (required)</span></span>
<span data-ttu-id="97bfc-144">Este certificado es necesario toosecure un clúster y evitar tooit de acceso no autorizado.</span><span class="sxs-lookup"><span data-stu-id="97bfc-144">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="97bfc-145">La seguridad adopta dos formas:</span><span class="sxs-lookup"><span data-stu-id="97bfc-145">It provides cluster security in a couple ways:</span></span>

* <span data-ttu-id="97bfc-146">**Autenticación del clúster:** se autentica la comunicación de nodo a nodo para la federación del clúster.</span><span class="sxs-lookup"><span data-stu-id="97bfc-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="97bfc-147">Sólo los nodos que se pueden demostrar su identidad con este certificado pueden unirse a clústeres de Hola.</span><span class="sxs-lookup"><span data-stu-id="97bfc-147">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="97bfc-148">**Autenticación de servidor:** autentica el cliente de administración de la tooa de los puntos de conexión de administración con hello clúster, por lo que hello administración cliente sabe está hablando clúster real toohello.</span><span class="sxs-lookup"><span data-stu-id="97bfc-148">**Server authentication:** Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="97bfc-149">Este certificado también proporciona SSL para hello API de administración de HTTPS y para el Explorador de Service Fabric a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="97bfc-149">This certificate also provides SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="97bfc-150">tooserve estos fines, certificado Hola debe cumplir Hola según los requisitos:</span><span class="sxs-lookup"><span data-stu-id="97bfc-150">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="97bfc-151">certificado de Hello debe contener una clave privada.</span><span class="sxs-lookup"><span data-stu-id="97bfc-151">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="97bfc-152">certificado de Hello debe crearse para el intercambio de claves, exportable tooa archivo de intercambio de información Personal (.pfx).</span><span class="sxs-lookup"><span data-stu-id="97bfc-152">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="97bfc-153">Hello nombre de sujeto del certificado debe coincidir con clúster de Service Fabric de hello dominio utilizado tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="97bfc-153">hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="97bfc-154">Esto es necesario tooprovide SSL de extremos de administración de HTTPS y el Explorador de Service Fabric del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="97bfc-154">This is required tooprovide SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="97bfc-155">No se puede obtener un certificado SSL de una entidad de certificación (CA) para hello `.cloudapp.azure.com` dominio.</span><span class="sxs-lookup"><span data-stu-id="97bfc-155">You cannot obtain an SSL certificate from a certificate authority (CA) for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="97bfc-156">Adquiera un nombre de dominio personalizado para el clúster.</span><span class="sxs-lookup"><span data-stu-id="97bfc-156">Acquire a custom domain name for your cluster.</span></span> <span data-ttu-id="97bfc-157">Cuando se solicita un certificado del nombre de sujeto del certificado de hello CA debe coincidir con nombre de dominio personalizado de hello utilizado para el clúster.</span><span class="sxs-lookup"><span data-stu-id="97bfc-157">When you request a certificate from a CA hello certificate's subject name must match hello custom domain name used for your cluster.</span></span>

### <a name="client-authentication-certificates"></a><span data-ttu-id="97bfc-158">Certificados de autenticación de cliente</span><span class="sxs-lookup"><span data-stu-id="97bfc-158">Client authentication certificates</span></span>
<span data-ttu-id="97bfc-159">Los certificados de cliente adicionales autentican a los administradores en las tareas de administración del clúster.</span><span class="sxs-lookup"><span data-stu-id="97bfc-159">Additional client certificates authenticate administrators for cluster management tasks.</span></span> <span data-ttu-id="97bfc-160">Service Fabric tiene dos niveles de acceso: **administrador** y **usuario de solo lectura**.</span><span class="sxs-lookup"><span data-stu-id="97bfc-160">Service Fabric has two access levels: **admin** and **read-only user**.</span></span> <span data-ttu-id="97bfc-161">Se debe usar como mínimo un certificado para el acceso administrativo.</span><span class="sxs-lookup"><span data-stu-id="97bfc-161">At minimum, a single certificate for administrative access should be used.</span></span> <span data-ttu-id="97bfc-162">Para accesos de nivel de usuario adicionales, se debe proporcionar un certificado diferente.</span><span class="sxs-lookup"><span data-stu-id="97bfc-162">For additional user-level access, a separate certificate must be provided.</span></span> <span data-ttu-id="97bfc-163">Para obtener más información sobre los roles de acceso, consulte [Control de acceso basado en roles para clientes de Service Fabric][service-fabric-cluster-security-roles].</span><span class="sxs-lookup"><span data-stu-id="97bfc-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span></span>

<span data-ttu-id="97bfc-164">No es necesario tooupload cliente autenticación certificados tooKey almacén toowork con Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="97bfc-164">You do not need tooupload Client authentication certificates tooKey Vault toowork with Service Fabric.</span></span> <span data-ttu-id="97bfc-165">Estos certificados solo necesitan toobe proporcionan toousers que estén autorizados para la administración de clúster.</span><span class="sxs-lookup"><span data-stu-id="97bfc-165">These certificates only need toobe provided toousers who are authorized for cluster management.</span></span> 

> [!NOTE]
> <span data-ttu-id="97bfc-166">Azure Active Directory es Hola recomienda a clientes de manera tooauthenticate para clúster de las operaciones de administración.</span><span class="sxs-lookup"><span data-stu-id="97bfc-166">Azure Active Directory is hello recommended way tooauthenticate clients for cluster management operations.</span></span> <span data-ttu-id="97bfc-167">toouse Azure Active Directory, debe [crear un clúster mediante el Administrador de recursos de Azure][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="97bfc-167">toouse Azure Active Directory, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

### <a name="application-certificates-optional"></a><span data-ttu-id="97bfc-168">Certificados de aplicación (opcionales)</span><span class="sxs-lookup"><span data-stu-id="97bfc-168">Application certificates (optional)</span></span>
<span data-ttu-id="97bfc-169">Se puede instalar un número cualquiera de certificados adicionales en un clúster para proteger la aplicación.</span><span class="sxs-lookup"><span data-stu-id="97bfc-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="97bfc-170">Antes de crear el clúster, considere la posibilidad de escenarios de seguridad de aplicación Hola que requieren un toobe de certificados instalado en nodos de hello, como:</span><span class="sxs-lookup"><span data-stu-id="97bfc-170">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="97bfc-171">Cifrado y descifrado de los valores de configuración de aplicación</span><span class="sxs-lookup"><span data-stu-id="97bfc-171">Encryption and decryption of application configuration values</span></span>
* <span data-ttu-id="97bfc-172">Cifrado de datos entre nodos durante la replicación</span><span class="sxs-lookup"><span data-stu-id="97bfc-172">Encryption of data across nodes during replication</span></span> 

<span data-ttu-id="97bfc-173">No se puede configurar certificados de aplicación al crear un clúster a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="97bfc-173">Application certificates cannot be configured when creating a cluster through hello Azure portal.</span></span> <span data-ttu-id="97bfc-174">tooconfigure certificados de aplicación en tiempo de instalación de clúster, debe [crear un clúster mediante el Administrador de recursos de Azure][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="97bfc-174">tooconfigure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span> <span data-ttu-id="97bfc-175">También puede agregar clúster de toohello certificados de aplicación una vez creada.</span><span class="sxs-lookup"><span data-stu-id="97bfc-175">You can also add application certificates toohello cluster after it has been created.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="97bfc-176">Formato de certificados para el uso del proveedor de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="97bfc-176">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="97bfc-177">Los archivos de clave privada (.pfx) se pueden agregar y usar directamente mediante el Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="97bfc-177">Private key files (.pfx) can be added and used directly through Key Vault.</span></span> <span data-ttu-id="97bfc-178">Sin embargo, el proveedor de recursos de Azure Hola requiere toobe de claves que se almacenan en un formato JSON especial que incluye .pfx Hola como un Base64 codificado hello y cadena de contraseña de clave privada.</span><span class="sxs-lookup"><span data-stu-id="97bfc-178">However, hello Azure resource provider requires keys toobe stored in a special JSON format that includes hello .pfx as a base-64 encoded string and hello private key password.</span></span> <span data-ttu-id="97bfc-179">tooaccommodate estos requisitos, las claves deben colocarse en una cadena JSON y, a continuación, se almacenan como *secretos* en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="97bfc-179">tooaccommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span></span>

<span data-ttu-id="97bfc-180">toomake facilitar este proceso, un módulo de PowerShell es [disponible en GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="97bfc-180">toomake this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="97bfc-181">Siga estos módulo de hello toouse de pasos:</span><span class="sxs-lookup"><span data-stu-id="97bfc-181">Follow these steps toouse hello module:</span></span>

1. <span data-ttu-id="97bfc-182">Descargar contenido completo de hello del repositorio de hello en un directorio local.</span><span class="sxs-lookup"><span data-stu-id="97bfc-182">Download hello entire contents of hello repo into a local directory.</span></span> 
2. <span data-ttu-id="97bfc-183">Importar el módulo de hello en la ventana de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="97bfc-183">Import hello module in your PowerShell window:</span></span>

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

<span data-ttu-id="97bfc-184">Hola `Invoke-AddCertToKeyVault` comandos en este módulo de PowerShell da formato a una clave privada del certificado en una cadena JSON y lo carga tooKey almacén automáticamente.</span><span class="sxs-lookup"><span data-stu-id="97bfc-184">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it tooKey Vault.</span></span> <span data-ttu-id="97bfc-185">Úsela certificado de clúster de hello tooadd y cualquier tooKey de certificados de aplicación adicionales almacén.</span><span class="sxs-lookup"><span data-stu-id="97bfc-185">Use it tooadd hello cluster certificate and any additional application certificates tooKey Vault.</span></span> <span data-ttu-id="97bfc-186">Repita este paso para todos los certificados adicionales que desee tooinstall en el clúster.</span><span class="sxs-lookup"><span data-stu-id="97bfc-186">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

<span data-ttu-id="97bfc-187">Se trata de todos los requisitos previos del almacén de claves de Hola para configurar una plantilla de administrador de recursos de clúster de Service Fabric que se instala certificados para la autenticación de nodo, seguridad del punto de conexión de administración y la autenticación y cualquier seguridad adicional para la aplicación características que usan certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="97bfc-187">These are all hello Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span></span> <span data-ttu-id="97bfc-188">En este punto, ahora debería tener Hola después de la instalación de Azure:</span><span class="sxs-lookup"><span data-stu-id="97bfc-188">At this point, you should now have hello following setup in Azure:</span></span>

* <span data-ttu-id="97bfc-189">Grupo de recursos del Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="97bfc-189">Key Vault resource group</span></span>
  * <span data-ttu-id="97bfc-190">Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="97bfc-190">Key Vault</span></span>
    * <span data-ttu-id="97bfc-191">Certificado de autenticación de servidor de clúster</span><span class="sxs-lookup"><span data-stu-id="97bfc-191">Cluster server authentication certificate</span></span>

<span data-ttu-id="97bfc-192"></a "create-cluster-portal" ></a></span><span class="sxs-lookup"><span data-stu-id="97bfc-192"></a "create-cluster-portal" ></a></span></span>

## <a name="create-cluster-in-hello-azure-portal"></a><span data-ttu-id="97bfc-193">Crear clúster en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="97bfc-193">Create cluster in hello Azure portal</span></span>
### <a name="search-for-hello-service-fabric-cluster-resource"></a><span data-ttu-id="97bfc-194">Busque Hola recurso de clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="97bfc-194">Search for hello Service Fabric cluster resource</span></span>
![Busque la plantilla de clúster de Service Fabric en hello portal de Azure.][SearchforServiceFabricClusterTemplate]

1. <span data-ttu-id="97bfc-196">Inicie sesión en toohello [portal de Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="97bfc-196">Sign in toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="97bfc-197">Haga clic en **New** tooadd una nueva plantilla de recursos.</span><span class="sxs-lookup"><span data-stu-id="97bfc-197">Click **New** tooadd a new resource template.</span></span> <span data-ttu-id="97bfc-198">Busque la plantilla de servicio de Cluster Server tejido Hola Hola **Marketplace** en **todo**.</span><span class="sxs-lookup"><span data-stu-id="97bfc-198">Search for hello Service Fabric Cluster template in hello **Marketplace** under **Everything**.</span></span>
3. <span data-ttu-id="97bfc-199">Seleccione **clúster de Service Fabric** de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="97bfc-199">Select **Service Fabric Cluster** from hello list.</span></span>
4. <span data-ttu-id="97bfc-200">Navegue toohello **clúster de Service Fabric** hoja, haga clic en **crear**,</span><span class="sxs-lookup"><span data-stu-id="97bfc-200">Navigate toohello **Service Fabric Cluster** blade, click **Create**,</span></span>
5. <span data-ttu-id="97bfc-201">Hola **clúster crear Service Fabric** hoja tiene Hola cuatro pasos.</span><span class="sxs-lookup"><span data-stu-id="97bfc-201">hello **Create Service Fabric cluster** blade has hello following four steps.</span></span>

#### <a name="1-basics"></a><span data-ttu-id="97bfc-202">1. Aspectos básicos</span><span class="sxs-lookup"><span data-stu-id="97bfc-202">1. Basics</span></span>
![Captura de pantalla de la creación de un grupo de recursos.][CreateRG]

<span data-ttu-id="97bfc-204">En la hoja de conceptos básicos de hello necesita detalles básicos de tooprovide hello para el clúster.</span><span class="sxs-lookup"><span data-stu-id="97bfc-204">In hello Basics blade you need tooprovide hello basic details for your cluster.</span></span>

1. <span data-ttu-id="97bfc-205">Escriba el nombre de hello del clúster.</span><span class="sxs-lookup"><span data-stu-id="97bfc-205">Enter hello name of your cluster.</span></span>
2. <span data-ttu-id="97bfc-206">Escriba un **nombre de usuario** y **contraseña** para escritorio remoto para hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="97bfc-206">Enter a **user name** and **password** for Remote Desktop for hello VMs.</span></span>
3. <span data-ttu-id="97bfc-207">Realizar seguro hello tooselect **suscripción** desea su toobe de clúster implementado, especialmente si tiene varias suscripciones.</span><span class="sxs-lookup"><span data-stu-id="97bfc-207">Make sure tooselect hello **Subscription** that you want your cluster toobe deployed to, especially if you have multiple subscriptions.</span></span>
4. <span data-ttu-id="97bfc-208">Cree un **nuevo grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="97bfc-208">Create a **new resource group**.</span></span> <span data-ttu-id="97bfc-209">Es mejor toogive lo Hola mismo nombre que el clúster de hello, ya que ayuda a buscar más adelante, especialmente cuando se está tratando de toomake cambios tooyour implementación o eliminar el clúster.</span><span class="sxs-lookup"><span data-stu-id="97bfc-209">It is best toogive it hello same name as hello cluster, since it helps in finding them later, especially when you are trying toomake changes tooyour deployment or delete your cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="97bfc-210">Aunque puede decidir toouse un grupo de recursos existente, es un toocreate recomendable un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="97bfc-210">Although you can decide toouse an existing resource group, it is a good practice toocreate a new resource group.</span></span> <span data-ttu-id="97bfc-211">Esto hace fácil toodelete clústeres que no es necesario.</span><span class="sxs-lookup"><span data-stu-id="97bfc-211">This makes it easy toodelete clusters that you do not need.</span></span>
   > 
   > 
5. <span data-ttu-id="97bfc-212">Seleccione hello **región** en que desea que el clúster de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="97bfc-212">Select hello **region** in which you want toocreate hello cluster.</span></span> <span data-ttu-id="97bfc-213">Debe usar hello misma región que la clave del almacén está en.</span><span class="sxs-lookup"><span data-stu-id="97bfc-213">You must use hello same region that your Key Vault is in.</span></span>

#### <a name="2-cluster-configuration"></a><span data-ttu-id="97bfc-214">2. Configuración del clúster</span><span class="sxs-lookup"><span data-stu-id="97bfc-214">2. Cluster configuration</span></span>
![Creación de un tipo de nodo][CreateNodeType]

<span data-ttu-id="97bfc-216">Configure los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="97bfc-216">Configure your cluster nodes.</span></span> <span data-ttu-id="97bfc-217">Tipos de nodos definen tamaños de máquinas virtuales de hello, Hola número de máquinas virtuales y sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="97bfc-217">Node types define hello VM sizes, hello number of VMs, and their properties.</span></span> <span data-ttu-id="97bfc-218">El clúster puede tener más de un tipo de nodo pero el tipo de nodo principal de hello (Hola la primera de ellas que define en el portal de hello) debe tener al menos cinco VM, puesto que éste es un tipo de nodo de Hola donde se colocan los servicios del sistema de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="97bfc-218">Your cluster can have more than one node type, but hello primary node type (hello first one that you define on hello portal) must have at least five VMs, as this is hello node type where Service Fabric system services are placed.</span></span> <span data-ttu-id="97bfc-219">No configure **Propiedades de ubicación** porque el sistema agrega automáticamente una propiedad de ubicación predeterminada de "NodeTypeName".</span><span class="sxs-lookup"><span data-stu-id="97bfc-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="97bfc-220">Un escenario común para varios tipos de nodos es una aplicación que contiene un servicio front-end y un servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="97bfc-220">A common scenario for multiple node types is an application that contains a front-end service and a back-end service.</span></span> <span data-ttu-id="97bfc-221">Desea que el servicio front-end de hello tooput en máquinas virtuales más pequeñas (tamaños de máquina virtual como D2) con puertos abiertos toohello Internet, pero desea tooput servicio de back-end de hello en máquinas virtuales más grandes (con tamaños de máquina virtual como D4, D6, D15 etc.) con ningún puerto de conexión a Internet abierto.</span><span class="sxs-lookup"><span data-stu-id="97bfc-221">You want tooput hello front-end service on smaller VMs (VM sizes like D2) with ports open toohello Internet, but you want tooput hello back-end service on larger VMs (with VM sizes like D4, D6, D15, and so on) with no Internet-facing ports open.</span></span>
> 
> 

1. <span data-ttu-id="97bfc-222">Elija un nombre para el tipo de nodo (1 too12 de caracteres que contiene solo letras y números).</span><span class="sxs-lookup"><span data-stu-id="97bfc-222">Choose a name for your node type (1 too12 characters containing only letters and numbers).</span></span>
2. <span data-ttu-id="97bfc-223">Hola mínimo **tamaño** de VM para el nodo principal de Hola Hola depende de tipo **durabilidad** nivel que elija para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="97bfc-223">hello minimum **size** of VMs for hello primary node type is driven by hello **durability** tier you choose for hello cluster.</span></span> <span data-ttu-id="97bfc-224">valor predeterminado de Hello para el nivel de durabilidad hello es Bronce.</span><span class="sxs-lookup"><span data-stu-id="97bfc-224">hello default for hello durability tier is bronze.</span></span> <span data-ttu-id="97bfc-225">Para obtener más información sobre la durabilidad, consulte [cómo toochoose Hola Service Fabric clúster confiabilidad y durabilidad][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="97bfc-225">For more information on durability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
3. <span data-ttu-id="97bfc-226">Seleccione el tamaño de la máquina virtual de Hola y nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="97bfc-226">Select hello VM size and pricing tier.</span></span> <span data-ttu-id="97bfc-227">Las máquinas virtuales de la serie D tienen unidades SSD y son muy recomendables para aplicaciones con estado.</span><span class="sxs-lookup"><span data-stu-id="97bfc-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span></span> <span data-ttu-id="97bfc-228">No utilice cualquier SKU de máquina virtual que tenga núcleos parciales o menos de 7 GB de capacidad de disco disponible.</span><span class="sxs-lookup"><span data-stu-id="97bfc-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span></span> 
4. <span data-ttu-id="97bfc-229">Hola mínimo **número** de VM para el nodo principal de Hola Hola depende de tipo **confiabilidad** nivel que elija.</span><span class="sxs-lookup"><span data-stu-id="97bfc-229">hello minimum **number** of VMs for hello primary node type is driven by hello **reliability** tier you choose.</span></span> <span data-ttu-id="97bfc-230">valor predeterminado de Hello para el nivel de confiabilidad de hello es plata.</span><span class="sxs-lookup"><span data-stu-id="97bfc-230">hello default for hello reliability tier is Silver.</span></span> <span data-ttu-id="97bfc-231">Para obtener más información sobre la confiabilidad, consulte [cómo toochoose Hola Service Fabric clúster confiabilidad y durabilidad][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="97bfc-231">For more information on reliability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
5. <span data-ttu-id="97bfc-232">Elegir Hola número de máquinas virtuales para el tipo de nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="97bfc-232">Choose hello number of VMs for hello node type.</span></span> <span data-ttu-id="97bfc-233">Puede escalar hacia arriba o hacia abajo el número de Hola de máquinas virtuales en un tipo de nodo más adelante, pero en el tipo de nodo principal de hello, Hola mínimo está controlada por el nivel de confiabilidad de Hola que ha elegido.</span><span class="sxs-lookup"><span data-stu-id="97bfc-233">You can scale up or down hello number of VMs in a node type later on, but on hello primary node type, hello minimum is driven by hello reliability level that you have chosen.</span></span> <span data-ttu-id="97bfc-234">Otros tipos de nodo pueden tener un mínimo de 1 máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="97bfc-234">Other node types can have a minimum of 1 VM.</span></span>
6. <span data-ttu-id="97bfc-235">Configure los puntos de conexión personalizados.</span><span class="sxs-lookup"><span data-stu-id="97bfc-235">Configure custom endpoints.</span></span> <span data-ttu-id="97bfc-236">Este campo le permite tooenter una lista separada por comas de puertos que desea que tooexpose a través de hello equilibrador de carga Azure toohello público de Internet para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="97bfc-236">This field allows you tooenter a comma-separated list of ports that you want tooexpose through hello Azure Load Balancer toohello public Internet for your applications.</span></span> <span data-ttu-id="97bfc-237">Por ejemplo, si tiene previsto toodeploy un clúster de tooyour de aplicación web, escriba "80" aquí tooallow tráfico en el puerto 80 en el clúster.</span><span class="sxs-lookup"><span data-stu-id="97bfc-237">For example, if you plan toodeploy a web application tooyour cluster, enter "80" here tooallow traffic on port 80 into your cluster.</span></span> <span data-ttu-id="97bfc-238">Para obtener más información sobre los puntos de conexión, consulte la [comunicación con las aplicaciones][service-fabric-connect-and-communicate-with-services].</span><span class="sxs-lookup"><span data-stu-id="97bfc-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span></span>
7. <span data-ttu-id="97bfc-239">Configure los **diagnósticos**de clúster.</span><span class="sxs-lookup"><span data-stu-id="97bfc-239">Configure cluster **diagnostics**.</span></span> <span data-ttu-id="97bfc-240">De forma predeterminada, se habilitan los diagnósticos en su tooassist de clúster con la solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="97bfc-240">By default, diagnostics are enabled on your cluster tooassist with troubleshooting issues.</span></span> <span data-ttu-id="97bfc-241">Si desea cambia de diagnóstico toodisable hello **estado** alternar demasiado**desactivar**.</span><span class="sxs-lookup"><span data-stu-id="97bfc-241">If you want toodisable diagnostics change hello **Status** toggle too**Off**.</span></span> <span data-ttu-id="97bfc-242">**No** se recomienda desactivar los diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="97bfc-242">Turning off diagnostics is **not** recommended.</span></span>
8. <span data-ttu-id="97bfc-243">Seleccione Hola tejido actualizar el modo que desea establecer el clúster.</span><span class="sxs-lookup"><span data-stu-id="97bfc-243">Select hello Fabric upgrade mode you want set your cluster to.</span></span> <span data-ttu-id="97bfc-244">Seleccione **automática**, si desea Hola sistema tooautomatically recogerá Hola última versión disponible e intente tooupgrade su tooit de clúster.</span><span class="sxs-lookup"><span data-stu-id="97bfc-244">Select **Automatic**, if you want hello system tooautomatically pick up hello latest available version and try tooupgrade your cluster tooit.</span></span> <span data-ttu-id="97bfc-245">Establecer el modo de hello demasiado**Manual**, si desea que toochoose una versión compatible.</span><span class="sxs-lookup"><span data-stu-id="97bfc-245">Set hello mode too**Manual**, if you want toochoose a supported version.</span></span>

> [!NOTE]
> <span data-ttu-id="97bfc-246">Se admiten solo los clústeres que ejecutan versiones compatibles de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="97bfc-246">We support only clusters that are running supported versions of service Fabric.</span></span> <span data-ttu-id="97bfc-247">Si selecciona hello **Manual** modo, va a realizar en hello responsabilidad tooupgrade su tooa admitida la versión de clúster.</span><span class="sxs-lookup"><span data-stu-id="97bfc-247">By selecting hello **Manual** mode, you are taking on hello responsibility tooupgrade your cluster tooa supported version.</span></span> <span data-ttu-id="97bfc-248">Para obtener más detalles sobre el modo de actualización de Fabric de Hola Hola, consulte [documento de servicio de fabric clúster de actualización.][service-fabric-cluster-upgrade]</span><span class="sxs-lookup"><span data-stu-id="97bfc-248">For more details on hello Fabric upgrade mode see hello [service-fabric-cluster-upgrade document.][service-fabric-cluster-upgrade]</span></span>
> 
> 

#### <a name="3-security"></a><span data-ttu-id="97bfc-249">3. Seguridad</span><span class="sxs-lookup"><span data-stu-id="97bfc-249">3. Security</span></span>
![Captura de pantalla de las configuraciones de seguridad del Portal de Azure.][SecurityConfigs]

<span data-ttu-id="97bfc-251">Hola último paso es clúster tooprovide certificado información toosecure Hola usando Hola el almacén de claves y el certificado información creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="97bfc-251">hello final step is tooprovide certificate information toosecure hello cluster using hello Key Vault and certificate information created earlier.</span></span>

* <span data-ttu-id="97bfc-252">Rellenar los campos de certificado principal de hello con salida de hello obtenido de cargar hello **certificado de clúster** tooKey almacén con Hola `Invoke-AddCertToKeyVault` comando de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97bfc-252">Populate hello primary certificate fields with hello output obtained from uploading hello **cluster certificate** tooKey Vault using hello `Invoke-AddCertToKeyVault` PowerShell command.</span></span>

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* <span data-ttu-id="97bfc-253">Comprobar hello **configurar opciones avanzadas** cuadro tooenter los certificados de cliente para **cliente de administración** y **cliente de solo lectura**.</span><span class="sxs-lookup"><span data-stu-id="97bfc-253">Check hello **Configure advanced settings** box tooenter client certificates for **admin client** and **read-only client**.</span></span> <span data-ttu-id="97bfc-254">En estos campos, escriba huella digital de Hola de su certificado de cliente de administración y la huella digital de Hola de su certificado de cliente de usuario de solo lectura, si procede.</span><span class="sxs-lookup"><span data-stu-id="97bfc-254">In these fields, enter hello thumbprint of your admin client certificate and hello thumbprint of your read-only user client certificate, if applicable.</span></span> <span data-ttu-id="97bfc-255">Cuando los administradores intentan tooconnect toohello clúster, se les concede acceso solo si tienen un certificado con una huella digital que coincide con los valores de huella digital de hello introducido aquí.</span><span class="sxs-lookup"><span data-stu-id="97bfc-255">When administrators attempt tooconnect toohello cluster, they are granted access only if they have a certificate with a thumbprint that matches hello thumbprint values entered here.</span></span>  

#### <a name="4-summary"></a><span data-ttu-id="97bfc-256">4. Resumen</span><span class="sxs-lookup"><span data-stu-id="97bfc-256">4. Summary</span></span>
![<span data-ttu-id="97bfc-257">Captura de pantalla de panel de inicio de hello mostrar "Clúster de tejido de servicio de implementación".</span><span class="sxs-lookup"><span data-stu-id="97bfc-257">Screen shot of hello start board displaying "Deploying Service Fabric Cluster."</span></span> ][Notifications]

<span data-ttu-id="97bfc-258">creación de clústeres de hello toocomplete, haga clic en **resumen** Hola a configuraciones de hello toosee que ha proporcionado o descargar plantilla de administrador de recursos de Azure que usan toodeploy el clúster.</span><span class="sxs-lookup"><span data-stu-id="97bfc-258">toocomplete hello cluster creation, click **Summary** toosee hello configurations that you have provided, or download hello Azure Resource Manager template that that used toodeploy your cluster.</span></span> <span data-ttu-id="97bfc-259">Después de haber proporcionado parámetros obligatorios hello, Hola **Aceptar** botón se convierte en verde y puede iniciar el proceso de creación de clúster de hello haciendo clic en él.</span><span class="sxs-lookup"><span data-stu-id="97bfc-259">After you have provided hello mandatory settings, hello **OK** button becomes green and you can start hello cluster creation process by clicking it.</span></span>

<span data-ttu-id="97bfc-260">Puede ver el progreso de la creación de hello en las notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="97bfc-260">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="97bfc-261">(Haga clic en el icono de campana"hello" cerca de la barra de estado de hello en la parte superior de hello derecha de la pantalla). Si hace clic en **Pin tooStartboard** al crear el clúster de hello, verá **implementación de clúster de Service Fabric** anclado toohello **iniciar** panel.</span><span class="sxs-lookup"><span data-stu-id="97bfc-261">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you will see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-your-cluster-status"></a><span data-ttu-id="97bfc-262">Visualización del estado del clúster</span><span class="sxs-lookup"><span data-stu-id="97bfc-262">View your cluster status</span></span>
![Captura de pantalla de detalles del clúster en el panel de Hola.][ClusterDashboard]

<span data-ttu-id="97bfc-264">Una vez creado el clúster, puede inspeccionar el clúster en el portal de hello:</span><span class="sxs-lookup"><span data-stu-id="97bfc-264">Once your cluster is created, you can inspect your cluster in hello portal:</span></span>

1. <span data-ttu-id="97bfc-265">Vaya demasiado**examinar** y haga clic en **clústeres del servicio de Fabric**.</span><span class="sxs-lookup"><span data-stu-id="97bfc-265">Go too**Browse** and click **Service Fabric Clusters**.</span></span>
2. <span data-ttu-id="97bfc-266">Busque su clúster y haga clic en él.</span><span class="sxs-lookup"><span data-stu-id="97bfc-266">Locate your cluster and click it.</span></span>
3. <span data-ttu-id="97bfc-267">Ahora puede ver detalles de hello del clúster en panel de hello, incluidos extremo público del clúster de Hola y un explorador de Fabric tooService de vínculo.</span><span class="sxs-lookup"><span data-stu-id="97bfc-267">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

<span data-ttu-id="97bfc-268">Hola **nodo Monitor** sección en la hoja de panel del clúster de hello indica el número de Hola de máquinas virtuales que están activados y no funciona correctamente.</span><span class="sxs-lookup"><span data-stu-id="97bfc-268">hello **Node Monitor** section on hello cluster's dashboard blade indicates hello number of VMs that are healthy and not healthy.</span></span> <span data-ttu-id="97bfc-269">Puede encontrar más detalles sobre el estado del clúster de hello en [introducción de modelo de mantenimiento de Service Fabric][service-fabric-health-introduction].</span><span class="sxs-lookup"><span data-stu-id="97bfc-269">You can find more details about hello cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span></span>

> [!NOTE]
> <span data-ttu-id="97bfc-270">Clústeres de Service Fabric requieren un cierto número de nodos toobe la disponibilidad de toomaintain siempre y conservan el estado - tooas que se hace referencia "mantenga el quórum".</span><span class="sxs-lookup"><span data-stu-id="97bfc-270">Service Fabric clusters require a certain number of nodes toobe up always toomaintain availability and preserve state - referred tooas "maintaining quorum".</span></span> <span data-ttu-id="97bfc-271">Por tanto, normalmente no es seguro tooshut hacia abajo de todas las máquinas de clúster de Hola a menos que primero ha llevado a cabo una [una copia de seguridad completa del estado del][service-fabric-reliable-services-backup-restore].</span><span class="sxs-lookup"><span data-stu-id="97bfc-271">Therfore, it is typically not safe tooshut down all machines in hello cluster unless you have first performed a [full backup of your state][service-fabric-reliable-services-backup-restore].</span></span>
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="97bfc-272">Instancia de conjunto de escala de máquinas virtuales de tooa o un nodo de clúster de conexión remota</span><span class="sxs-lookup"><span data-stu-id="97bfc-272">Remote connect tooa Virtual Machine Scale Set instance or a cluster node</span></span>
<span data-ttu-id="97bfc-273">Cada uno de hello NodeTypes especifica en los resultados de clúster en un conjunto de escala de máquinas virtuales para la obtención de instalación.</span><span class="sxs-lookup"><span data-stu-id="97bfc-273">Each of hello NodeTypes you specify in your cluster results in a Virtual Machine Scale Set getting set-up.</span></span> <span data-ttu-id="97bfc-274">Vea [remoto conectar la instancia de conjunto de escala de máquinas virtuales de tooa] [ remote-connect-to-a-vm-scale-set] para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="97bfc-274">See [Remote connect tooa Virtual Machine Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97bfc-275">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97bfc-275">Next steps</span></span>
<span data-ttu-id="97bfc-276">En este punto, tiene un clúster seguro mediante certificados para la autenticación de administración.</span><span class="sxs-lookup"><span data-stu-id="97bfc-276">At this point, you have a secure cluster using certificates for management authentication.</span></span> <span data-ttu-id="97bfc-277">Después, [conectar clúster tooyour](service-fabric-connect-to-secure-cluster.md) y obtenga información acerca de cómo demasiado[administrar secretos de aplicación](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="97bfc-277">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>  <span data-ttu-id="97bfc-278">Más información sobre las [opciones de soporte técnico de Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="97bfc-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span></span>

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
