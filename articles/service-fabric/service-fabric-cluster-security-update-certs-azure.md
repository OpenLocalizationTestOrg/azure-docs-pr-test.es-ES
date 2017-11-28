---
title: "certificados aaaManage en un clúster de Azure Service Fabric | Documentos de Microsoft"
description: "Describe cómo tooadd nuevos certificados, el certificado de sustitución y quitar certificados tooor desde un clúster de Service Fabric."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: 8e57bd95dbb800ecc04cf6988047e3abdc2fe56a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a><span data-ttu-id="368e4-103">Agregar o quitar certificados para un clúster de Service Fabric de Azure</span><span class="sxs-lookup"><span data-stu-id="368e4-103">Add or remove certificates for a Service Fabric cluster in Azure</span></span>
<span data-ttu-id="368e4-104">Se recomienda que familiarizarse con cómo Service Fabric utiliza los certificados X.509 y estar familiarizado con hello [los escenarios de seguridad de clúster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="368e4-104">It is recommended that you familiarize yourself with how Service Fabric uses X.509 certificates and be familiar with hello [Cluster security scenarios](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="368e4-105">Debe entender qué es un certificado de clúster y para qué se usa antes de seguir avanzando.</span><span class="sxs-lookup"><span data-stu-id="368e4-105">You must understand what a cluster certificate is and what is used for, before you proceed further.</span></span>

<span data-ttu-id="368e4-106">Servicio fabric le permite que especificar que dos clústeres certificados, principal y un elemento secundario, al configurar certificados seguridad durante la creación del clúster, en los certificados de tooclient de adición.</span><span class="sxs-lookup"><span data-stu-id="368e4-106">Service fabric lets you specify two cluster certificates, a primary and a secondary, when you configure certificate security during cluster creation, in addition tooclient certificates.</span></span> <span data-ttu-id="368e4-107">Consulte demasiado[crear un clúster mediante el portal de azure](service-fabric-cluster-creation-via-portal.md) o [creación de un clúster de azure mediante Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) para obtener más información sobre cómo configurarlas en el momento de su creación.</span><span class="sxs-lookup"><span data-stu-id="368e4-107">Refer too[creating an azure cluster via portal](service-fabric-cluster-creation-via-portal.md) or [creating an azure cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) for details on setting them up at create time.</span></span> <span data-ttu-id="368e4-108">Si especifica solo un certificado de clúster en el momento de creación, a continuación, en el que se usa como certificado principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="368e4-108">If you specify only one cluster certificate at create time, then that is used as hello primary certificate.</span></span> <span data-ttu-id="368e4-109">Después de la creación del clúster, puede agregar un nuevo certificado como elemento secundario.</span><span class="sxs-lookup"><span data-stu-id="368e4-109">After cluster creation, you can add a new certificate as a secondary.</span></span>

> [!NOTE]
> <span data-ttu-id="368e4-110">Para un clúster de seguro, siempre deberá certificado de al menos un clúster (no revocados y no expirados) válidos (principal o secundario) implementado (si no, Hola clúster dejará de funcionar).</span><span class="sxs-lookup"><span data-stu-id="368e4-110">For a secure cluster, you will always need at least one valid (not revoked and not expired) cluster certificate (primary or secondary) deployed (if not, hello cluster stops functioning).</span></span> <span data-ttu-id="368e4-111">90 días antes de que todos los certificados válidos alcancen la expiración, sistema de hello genera un seguimiento de advertencia y también un evento de estado de advertencia en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="368e4-111">90 days before all valid certificates reach expiration, hello system generates a warning trace and also a warning health event on hello node.</span></span> <span data-ttu-id="368e4-112">Actualmente, Service Fabric no envía ningún mensaje de correo electrónico ni cualquier otra notificación sobre este tema.</span><span class="sxs-lookup"><span data-stu-id="368e4-112">There is currently no email or any other notification that service fabric sends out on this topic.</span></span> 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-hello-portal"></a><span data-ttu-id="368e4-113">Agregar un certificado de clúster secundario mediante el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="368e4-113">Add a secondary cluster certificate using hello portal</span></span>

<span data-ttu-id="368e4-114">No se puede agregar el certificado de clúster secundario a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="368e4-114">Secondary cluster certificate cannot be added through hello Azure portal.</span></span> <span data-ttu-id="368e4-115">Tiene toouse Azure powershell para que.</span><span class="sxs-lookup"><span data-stu-id="368e4-115">You have toouse Azure powershell for that.</span></span> <span data-ttu-id="368e4-116">proceso de Hola se describe más adelante en este documento.</span><span class="sxs-lookup"><span data-stu-id="368e4-116">hello process is outlined later in this document.</span></span>

## <a name="swap-hello-cluster-certificates-using-hello-portal"></a><span data-ttu-id="368e4-117">Intercambiar los certificados de clúster de hello mediante el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="368e4-117">Swap hello cluster certificates using hello portal</span></span>

<span data-ttu-id="368e4-118">Después de haber implementado correctamente un certificado de clúster secundario, si desea tooswap Hola principal y secundaria, a continuación, navegue toohello hoja de seguridad y la opción hello 'Intercambio con principal' de hello contexto menú tooswap Hola secundaria cert con certificado principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="368e4-118">After you have successfully deployed a secondary cluster certificate, if you want tooswap hello primary and secondary, then navigate toohello Security blade, and select hello 'Swap with primary' option from hello context menu tooswap hello secondary cert with hello primary cert.</span></span>

![Intercambiar certificado][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-hello-portal"></a><span data-ttu-id="368e4-120">Quitar un certificado de clúster mediante el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="368e4-120">Remove a cluster certificate using hello portal</span></span>

<span data-ttu-id="368e4-121">Para un clúster de seguro, siempre necesitará al menos un válido (no revocado y no expirado) certificado (principal o secundario) implementado en caso contrario, Hola clúster dejará de funcionar.</span><span class="sxs-lookup"><span data-stu-id="368e4-121">For a secure cluster, you will always need at least one valid (not revoked and not expired) certificate (primary or secondary) deployed if not, hello cluster stops functioning.</span></span>

<span data-ttu-id="368e4-122">tooremove certificado secundario se utilice para la seguridad de clúster, Navigate toohello Security blade y opción de 'Delete' hello seleccione del menú contextual de hello en certificado secundario Hola.</span><span class="sxs-lookup"><span data-stu-id="368e4-122">tooremove a secondary certificate from being used for cluster security, Navigate toohello Security blade and select hello 'Delete' option from hello context menu on hello secondary certificate.</span></span>

<span data-ttu-id="368e4-123">Si su intención es certificado de hello tooremove marcado principal y, a continuación, deberá tooswap con Hola secundaria en primer lugar y, a continuación, eliminar Hola secundaria una vez completada la actualización Hola.</span><span class="sxs-lookup"><span data-stu-id="368e4-123">If your intent is tooremove hello certificate that is marked primary, then you will need tooswap it with hello secondary first, and then delete hello secondary after hello upgrade has completed.</span></span>

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a><span data-ttu-id="368e4-124">Incorporación de un certificado secundario mediante Powershell para Resource Manager</span><span class="sxs-lookup"><span data-stu-id="368e4-124">Add a secondary certificate using Resource Manager Powershell</span></span>

<span data-ttu-id="368e4-125">Estos pasos se supone que está familiarizado con cómo funciona el Administrador de recursos y ha implementado al menos un clúster de Service Fabric mediante una plantilla de administrador de recursos y tiene plantilla de Hola que usa tooset clúster Hola práctica.</span><span class="sxs-lookup"><span data-stu-id="368e4-125">These steps assume that you are familiar with how Resource Manager works and have deployed atleast one Service Fabric cluster using a Resource Manager template, and have hello template that you used tooset up hello cluster handy.</span></span> <span data-ttu-id="368e4-126">También se da por hecho que está familiarizado con el uso de JSON.</span><span class="sxs-lookup"><span data-stu-id="368e4-126">It is also assumed that you are comfortable using JSON.</span></span>

> [!NOTE]
> <span data-ttu-id="368e4-127">Si desea obtener una plantilla de ejemplo y los parámetros que se puede usar toofollow a lo largo o como punto de partida, descárguelo desde esta [repositorio de git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="368e4-127">If you are looking for a sample template and parameters that you can use toofollow along or as a starting point, then download it from this [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span> 
> 
> 

### <a name="edit-your-resource-manager-template"></a><span data-ttu-id="368e4-128">Edición de la plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="368e4-128">Edit your Resource Manager template</span></span>

<span data-ttu-id="368e4-129">Para facilitar su siguiente a lo largo, ejemplo 5-VM-1-NodeTypes-Secure_Step2.JSON contiene todas las ediciones de hello que realizaremos.</span><span class="sxs-lookup"><span data-stu-id="368e4-129">For ease of following along, sample 5-VM-1-NodeTypes-Secure_Step2.JSON contains all hello edits we will be making.</span></span> <span data-ttu-id="368e4-130">ejemplo de Hola está disponible en [repositorio de git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="368e4-130">hello sample is available at [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span>

<span data-ttu-id="368e4-131">**Asegúrese de toofollow seguro de todos los pasos de Hola**</span><span class="sxs-lookup"><span data-stu-id="368e4-131">**Make sure toofollow all hello steps**</span></span>

<span data-ttu-id="368e4-132">**Paso 1:** abra una plantilla de administrador de recursos de hello usa toodeploy del clúster.</span><span class="sxs-lookup"><span data-stu-id="368e4-132">**Step 1:** Open up hello Resource Manager template you used toodeploy you Cluster.</span></span> <span data-ttu-id="368e4-133">(Si ha descargado el ejemplo hello de Hola por encima del repositorio, a continuación, utilizar 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy un clúster segura y, a continuación, abrir dicha plantilla).</span><span class="sxs-lookup"><span data-stu-id="368e4-133">(If you have downloaded hello sample from hello above repo, then Use 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy a secure cluster and then open up that template).</span></span>

<span data-ttu-id="368e4-134">**Paso 2:** agregar **dos parámetros nuevos** "secCertificateThumbprint" y "secCertificateUrlValue" de tipo "string" toohello sección de parámetros de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="368e4-134">**Step 2:** Add **two new parameters** "secCertificateThumbprint" and "secCertificateUrlValue" of type "string" toohello parameter section of your template.</span></span> <span data-ttu-id="368e4-135">Puede copiar Hola siguiente fragmento de código y Agregar plantilla toohello.</span><span class="sxs-lookup"><span data-stu-id="368e4-135">You can copy hello following code snippet and add it toohello template.</span></span> <span data-ttu-id="368e4-136">Según el origen de saludo de la plantilla, ya puede tener estos, caso en ese mover toohello siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="368e4-136">Depending on hello source of your template, you may already have these defined, if so move toohello next step.</span></span> 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

<span data-ttu-id="368e4-137">**Paso 3:** realizar cambios toohello **Microsoft.ServiceFabric/clusters** recurso, busque la definición de recursos "Microsoft.ServiceFabric/clusters" hello en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="368e4-137">**Step 3:** Make changes toohello **Microsoft.ServiceFabric/clusters** resource - Locate hello "Microsoft.ServiceFabric/clusters" resource definition in your template.</span></span> <span data-ttu-id="368e4-138">En Propiedades de esa definición, encontrará "Certificado" JSON etiqueta, que debe ser similar Hola siguiente fragmento de JSON:</span><span class="sxs-lookup"><span data-stu-id="368e4-138">Under properties of that definition, you will find "Certificate" JSON tag, which should look something like hello following JSON snippet:</span></span>

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="368e4-139">Agregue una nueva etiqueta "thumbprintSecondary" y asígnele un valor "[parameters('secCertificateThumbprint')]".</span><span class="sxs-lookup"><span data-stu-id="368e4-139">Add a new tag "thumbprintSecondary" and give it a value "[parameters('secCertificateThumbprint')]".</span></span>  

<span data-ttu-id="368e4-140">Por lo que ahora la definición de recursos de hello debería ser similar Hola siguiente (dependiendo del origen de plantilla de hello, puede que no sea exactamente igual que Hola de fragmento de código siguiente).</span><span class="sxs-lookup"><span data-stu-id="368e4-140">So now hello resource definition should look like hello following (depending on your source of hello template, it may not be exactly like hello snippet below).</span></span> 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="368e4-141">Si desea demasiado**certificado de sustitución hello**, a continuación, especifique el nuevo certificado de hello como principal actual de hello principal y mover como base de datos secundaria.</span><span class="sxs-lookup"><span data-stu-id="368e4-141">If you want too**rollover hello cert**, then specify hello new cert as primary and moving hello current primary as secondary.</span></span> <span data-ttu-id="368e4-142">Esto da como resultado en sustitución de Hola de su certificado primario toohello nuevo certificado actual en un paso de implementación.</span><span class="sxs-lookup"><span data-stu-id="368e4-142">This results in hello rollover of your current primary certificate toohello new certificate in one deployment step.</span></span>

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


<span data-ttu-id="368e4-143">**Paso 4:** realizar cambios demasiado**todos los** hello **Microsoft.Compute/virtualMachineScaleSets** las definiciones de recursos - busque hello Microsoft.Compute/virtualMachineScaleSets recurso definición.</span><span class="sxs-lookup"><span data-stu-id="368e4-143">**Step 4:** Make changes too**all** hello **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate hello Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="368e4-144">Desplácese toohello "publisher": "Microsoft.Azure.ServiceFabric" en "virtualMachineProfile".</span><span class="sxs-lookup"><span data-stu-id="368e4-144">Scroll toohello "publisher": "Microsoft.Azure.ServiceFabric", under "virtualMachineProfile".</span></span>

<span data-ttu-id="368e4-145">En configuración del publicador de hello service fabric, debería ver algo parecido a esto.</span><span class="sxs-lookup"><span data-stu-id="368e4-145">In hello service fabric publisher settings, you should see something like this.</span></span>

![Json_Pub_Setting1][Json_Pub_Setting1]

<span data-ttu-id="368e4-147">Agregar Hola nuevo certificado entradas tooit</span><span class="sxs-lookup"><span data-stu-id="368e4-147">Add hello new cert entries tooit</span></span>

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

<span data-ttu-id="368e4-148">propiedades de Hello deben tener el siguiente aspecto</span><span class="sxs-lookup"><span data-stu-id="368e4-148">hello properties should now look like this</span></span>

![Json_Pub_Setting2][Json_Pub_Setting2]

<span data-ttu-id="368e4-150">Si desea demasiado**certificado de sustitución hello**, a continuación, especifique el nuevo certificado de hello como principal actual de hello principal y mover como base de datos secundaria.</span><span class="sxs-lookup"><span data-stu-id="368e4-150">If you want too**rollover hello cert**, then specify hello new cert as primary and moving hello current primary as secondary.</span></span> <span data-ttu-id="368e4-151">Esto da como resultado en sustitución de Hola de su certificado toohello nuevo certificado actual en un paso de implementación.</span><span class="sxs-lookup"><span data-stu-id="368e4-151">This results in hello rollover of your current certificate toohello new certificate in one deployment step.</span></span> 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
<span data-ttu-id="368e4-152">propiedades de Hello deben tener el siguiente aspecto</span><span class="sxs-lookup"><span data-stu-id="368e4-152">hello properties should now look like this</span></span>

![Json_Pub_Setting3][Json_Pub_Setting3]


<span data-ttu-id="368e4-154">**Paso 5:** realizar cambios demasiado**todos los** hello **Microsoft.Compute/virtualMachineScaleSets** las definiciones de recursos - busque hello Microsoft.Compute/virtualMachineScaleSets recurso definición.</span><span class="sxs-lookup"><span data-stu-id="368e4-154">**Step 5:** Make Changes too**all** hello **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate hello Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="368e4-155">Desplácese toohello "vaultCertificates":, en "OSProfile".</span><span class="sxs-lookup"><span data-stu-id="368e4-155">Scroll toohello "vaultCertificates": , under "OSProfile".</span></span> <span data-ttu-id="368e4-156">Tendrá un aspecto similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="368e4-156">it should look something like this.</span></span>


![Json_Pub_Setting4][Json_Pub_Setting4]

<span data-ttu-id="368e4-158">Agregar hello secCertificateUrlValue tooit.</span><span class="sxs-lookup"><span data-stu-id="368e4-158">Add hello secCertificateUrlValue tooit.</span></span> <span data-ttu-id="368e4-159">usar hello siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="368e4-159">use hello following snippet:</span></span>

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
<span data-ttu-id="368e4-160">Ahora Hola resultante Json debe tener un aspecto similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="368e4-160">Now hello resulting Json should look something like this.</span></span>
<span data-ttu-id="368e4-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span><span class="sxs-lookup"><span data-stu-id="368e4-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span></span>


> [!NOTE]
> <span data-ttu-id="368e4-162">Asegúrese de que se repite los pasos 4 y 5 para todas las definiciones de recursos de Nodetypes/Microsoft.Compute/virtualMachineScaleSets hello en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="368e4-162">Make sure that you have repeated steps 4 and 5 for all hello Nodetypes/Microsoft.Compute/virtualMachineScaleSets resource definitions in your template.</span></span> <span data-ttu-id="368e4-163">Si se salta a uno de ellos, no podrá instalarse certificado hello en ese VMSS y tendrá resultados imprevisibles en el clúster, incluidos los clúster Hola dirigiéndose hacia abajo (si se terminará con ningún certificado válido que puede utilizar ese clúster hello para la seguridad.</span><span class="sxs-lookup"><span data-stu-id="368e4-163">If you miss one of them, hello certificate will not get installed on that VMSS and you will have unpredictable results in your cluster, including hello cluster going down (if you end up with no valid certificates that hello cluster can use for security.</span></span> <span data-ttu-id="368e4-164">Compruébelo dos veces antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="368e4-164">So please double check, before proceeding further.</span></span>
> 
> 


### <a name="edit-your-template-file-tooreflect-hello-new-parameters-you-added-above"></a><span data-ttu-id="368e4-165">Editar los plantilla archivo tooreflect Hola nuevos parámetros que agregó anteriormente</span><span class="sxs-lookup"><span data-stu-id="368e4-165">Edit your template file tooreflect hello new parameters you added above</span></span>
<span data-ttu-id="368e4-166">Si usas ejemplo Hola Hola [repositorio de git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow desde el principio, puede iniciar toomake cambios en el ejemplo hello 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span><span class="sxs-lookup"><span data-stu-id="368e4-166">If you are using hello sample from hello [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow along, you can start toomake changes in hello sample 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span></span> 

<span data-ttu-id="368e4-167">Editar el parámetro de plantilla de administrador de recursos del archivo, agregue dos parámetros nuevos Hola para secCertificateThumbprint y secCertificateUrlValue.</span><span class="sxs-lookup"><span data-stu-id="368e4-167">Edit your Resource Manager Template parameter File, add hello two new parameters for secCertificateThumbprint and secCertificateUrlValue.</span></span> 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-hello-template-tooazure"></a><span data-ttu-id="368e4-168">Implementar Hola plantilla tooAzure</span><span class="sxs-lookup"><span data-stu-id="368e4-168">Deploy hello template tooAzure</span></span>

- <span data-ttu-id="368e4-169">Se está ahora listo toodeploy su tooAzure de plantilla.</span><span class="sxs-lookup"><span data-stu-id="368e4-169">You are now ready toodeploy your template tooAzure.</span></span> <span data-ttu-id="368e4-170">Abra un símbolo del sistema de Azure PS versión 1 o superior.</span><span class="sxs-lookup"><span data-stu-id="368e4-170">Open an Azure PS version 1+ command prompt.</span></span>
- <span data-ttu-id="368e4-171">Inicie sesión en tooyour cuenta de Azure y seleccione la suscripción de azure específica Hola.</span><span class="sxs-lookup"><span data-stu-id="368e4-171">Log in tooyour Azure Account and select hello specific azure subscription.</span></span> <span data-ttu-id="368e4-172">Se trata de un paso importante para personas que tienen acceso toomore a una suscripción de azure.</span><span class="sxs-lookup"><span data-stu-id="368e4-172">This is an important step for folks who have access toomore than one azure subscription.</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

<span data-ttu-id="368e4-173">Probar Hola plantilla anterior toodeploying lo.</span><span class="sxs-lookup"><span data-stu-id="368e4-173">Test hello template prior toodeploying it.</span></span> <span data-ttu-id="368e4-174">Use Hola mismo grupo de recursos que el clúster está implementado actualmente en.</span><span class="sxs-lookup"><span data-stu-id="368e4-174">Use hello same Resource Group that your cluster is currently deployed to.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

<span data-ttu-id="368e4-175">Implementar grupo de recursos de hello plantilla tooyour.</span><span class="sxs-lookup"><span data-stu-id="368e4-175">Deploy hello template tooyour resource group.</span></span> <span data-ttu-id="368e4-176">Use Hola mismo grupo de recursos que el clúster está implementado actualmente en.</span><span class="sxs-lookup"><span data-stu-id="368e4-176">Use hello same Resource Group that your cluster is currently deployed to.</span></span> <span data-ttu-id="368e4-177">Ejecute hello AzureRmResourceGroupDeployment nuevo comando.</span><span class="sxs-lookup"><span data-stu-id="368e4-177">Run hello New-AzureRmResourceGroupDeployment command.</span></span> <span data-ttu-id="368e4-178">No es necesario el modo de hello toospecify, puesto que es el valor predeterminado de hello **incremental**.</span><span class="sxs-lookup"><span data-stu-id="368e4-178">You do not need toospecify hello mode, since hello default value is **incremental**.</span></span>

> [!NOTE]
> <span data-ttu-id="368e4-179">Si establece el modo tooComplete, puede eliminar accidentalmente los recursos que no están en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="368e4-179">If you set Mode tooComplete, you can inadvertently delete resources that are not in your template.</span></span> <span data-ttu-id="368e4-180">Por ello no lo utilice en este escenario.</span><span class="sxs-lookup"><span data-stu-id="368e4-180">So do not use it in this scenario.</span></span>
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

<span data-ttu-id="368e4-181">Esta es una forma rellena ejemplo de Hola powershell mismo.</span><span class="sxs-lookup"><span data-stu-id="368e4-181">Here is a filled out example of hello same powershell.</span></span>

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

<span data-ttu-id="368e4-182">Una vez completada la implementación de hello, conectar tooyour clúster con Hola nuevo certificado y realizar algunas consultas.</span><span class="sxs-lookup"><span data-stu-id="368e4-182">Once hello deployment is complete, connect tooyour cluster using hello new Certificate and perform some queries.</span></span> <span data-ttu-id="368e4-183">Si es capaz de toodo.</span><span class="sxs-lookup"><span data-stu-id="368e4-183">If you are able toodo.</span></span> <span data-ttu-id="368e4-184">A continuación, puede eliminar los certificados antiguos Hola.</span><span class="sxs-lookup"><span data-stu-id="368e4-184">Then you can delete hello old certificate.</span></span> 

<span data-ttu-id="368e4-185">Si está utilizando un certificado autofirmado, no olvide tooimport en su almacén de certificados local TrustedPeople.</span><span class="sxs-lookup"><span data-stu-id="368e4-185">If you are using a self-signed certificate, do not forget tooimport them into your local TrustedPeople cert store.</span></span>

```powershell
######## Set up hello certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
<span data-ttu-id="368e4-186">Referencia rápida mostramos clúster segura de hello comando tooconnect tooa</span><span class="sxs-lookup"><span data-stu-id="368e4-186">For quick reference here is hello command tooconnect tooa secure cluster</span></span> 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
<span data-ttu-id="368e4-187">Referencia rápida aquí es el estado de clúster de hello comando tooget</span><span class="sxs-lookup"><span data-stu-id="368e4-187">For quick reference here is hello command tooget cluster health</span></span>

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-toohello-cluster"></a><span data-ttu-id="368e4-188">Implementación de clúster de toohello de certificados de aplicación.</span><span class="sxs-lookup"><span data-stu-id="368e4-188">Deploying Application certificates toohello cluster.</span></span>

<span data-ttu-id="368e4-189">Puede usar Hola mismo pasos tal como se describe en los pasos 5 anteriormente toohave Hola certificados implementados a partir de un toohello keyvault nodos.</span><span class="sxs-lookup"><span data-stu-id="368e4-189">You can use hello same steps as outlined in Steps 5 above toohave hello certificates deployed from a keyvault toohello Nodes.</span></span> <span data-ttu-id="368e4-190">Solo necesita definir y usar parámetros diferentes.</span><span class="sxs-lookup"><span data-stu-id="368e4-190">you just need define and use different parameters.</span></span>


## <a name="adding-or-removing-client-certificates"></a><span data-ttu-id="368e4-191">Incorporación o eliminación de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="368e4-191">Adding or removing Client certificates</span></span>

<span data-ttu-id="368e4-192">En los certificados de clúster de suma toohello, puede agregar operaciones de administración de tooperform de certificados de cliente en un clúster de service fabric.</span><span class="sxs-lookup"><span data-stu-id="368e4-192">In addition toohello cluster certificates, you can add client certificates tooperform management operations on a service fabric cluster.</span></span>

<span data-ttu-id="368e4-193">Puede agregar dos tipos de certificados de cliente: administrador o solo lectura.</span><span class="sxs-lookup"><span data-stu-id="368e4-193">You can add two kinds of client certificates - Admin or Read-only.</span></span> <span data-ttu-id="368e4-194">A continuación, puede tratarse de operaciones de administración de toocontrol usa acceso toohello y operaciones de consulta en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="368e4-194">These then can be used toocontrol access toohello admin operations and Query operations on hello cluster.</span></span> <span data-ttu-id="368e4-195">De forma predeterminada, los certificados de clúster de Hola se agregan toohello lista de certificados de administración de elementos permitido.</span><span class="sxs-lookup"><span data-stu-id="368e4-195">By default, hello cluster certificates are added toohello allowed Admin certificates list.</span></span>

<span data-ttu-id="368e4-196">Puede especificar cualquier número de certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="368e4-196">you can specify any number of client certificates.</span></span> <span data-ttu-id="368e4-197">Resultados de cada adición o eliminación en un clúster de configuración update toohello service fabric</span><span class="sxs-lookup"><span data-stu-id="368e4-197">Each addition/deletion results in a configuration update toohello service fabric cluster</span></span>


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a><span data-ttu-id="368e4-198">Incorporación de certificados de cliente de administrador o solo lectura mediante el portal</span><span class="sxs-lookup"><span data-stu-id="368e4-198">Adding client certificates - Admin or Read-Only via portal</span></span>

1. <span data-ttu-id="368e4-199">Desplácese toohello hoja de seguridad y seleccione Hola "+ autenticación" botón encima de la hoja de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="368e4-199">Navigate toohello Security blade, and select hello '+ Authentication' button on top of hello security blade.</span></span>
2. <span data-ttu-id="368e4-200">En la hoja de 'Agregar autenticación' hello, elija hello 'Autenticación de tipo' - 'Solo lectura cliente' o ' Admin'</span><span class="sxs-lookup"><span data-stu-id="368e4-200">On hello 'Add Authentication' blade, choose hello 'Authentication Type' - 'Read-only client' or 'Admin client'</span></span>
3. <span data-ttu-id="368e4-201">Elegir método de autorización de hello.</span><span class="sxs-lookup"><span data-stu-id="368e4-201">Now choose hello Authorization method.</span></span> <span data-ttu-id="368e4-202">Esto indica tooService tejido si debe buscar este certificado mediante el nombre del firmante de Hola o huella digital de Hola.</span><span class="sxs-lookup"><span data-stu-id="368e4-202">This indicates tooService Fabric whether it should look up this certificate by using hello subject name or hello thumbprint.</span></span> <span data-ttu-id="368e4-203">En general, no es un método de autorización de seguridad buena práctica toouse Hola de nombre de sujeto.</span><span class="sxs-lookup"><span data-stu-id="368e4-203">In general, it is not a good security practice toouse hello authorization method of subject name.</span></span> 

![Incorporación de certificados de cliente][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-hello-portal"></a><span data-ttu-id="368e4-205">Eliminación de certificados de cliente - administrador o solo lectura, utilice Hola portal</span><span class="sxs-lookup"><span data-stu-id="368e4-205">Deletion of Client Certificates - Admin or Read-Only using hello portal</span></span>

<span data-ttu-id="368e4-206">tooremove certificado secundario se utilice para la seguridad de clúster, Navigate toohello Security blade y opción de 'Delete' hello seleccione del menú contextual de hello en certificado específico de Hola.</span><span class="sxs-lookup"><span data-stu-id="368e4-206">tooremove a secondary certificate from being used for cluster security, Navigate toohello Security blade and select hello 'Delete' option from hello context menu on hello specific certificate.</span></span>



## <a name="next-steps"></a><span data-ttu-id="368e4-207">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="368e4-207">Next steps</span></span>
<span data-ttu-id="368e4-208">Lea estos artículos para más información sobre la administración de clúster:</span><span class="sxs-lookup"><span data-stu-id="368e4-208">Read these articles for more information on cluster management:</span></span>

* [<span data-ttu-id="368e4-209">Proceso de actualización del clúster de Service Fabric y expectativas del usuario</span><span class="sxs-lookup"><span data-stu-id="368e4-209">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="368e4-210">Control de acceso basado en roles para clientes de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="368e4-210">Setup role-based access for clients</span></span>](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


