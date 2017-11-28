---
title: "aaaCreate un tejido de servicio de clúster en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo agrupar toocreate Windows o Linux Service Fabric en Azure con PowerShell."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi
ms.openlocfilehash: e697e2a2e99f67cb02422efdb368c664c9fd5a97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a><span data-ttu-id="a3dac-103">Creación de un clúster seguro en Azure mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3dac-103">Create a secure cluster on Azure using PowerShell</span></span>
<span data-ttu-id="a3dac-104">Este tutorial muestra cómo toocreate un tejido de servicio de clúster (Windows o Linux) que se ejecute en Azure.</span><span class="sxs-lookup"><span data-stu-id="a3dac-104">This tutorial shows you how toocreate a Service Fabric cluster (Windows or Linux) running in Azure.</span></span> <span data-ttu-id="a3dac-105">Cuando haya terminado, tendrá un clúster que ejecuta en la nube de Hola que puede implementar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a3dac-105">When you're finished, you have a cluster running in hello cloud that you can deploy applications to.</span></span>

<span data-ttu-id="a3dac-106">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="a3dac-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a3dac-107">Creación de un clúster de Service Fabric en Azure mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3dac-107">Create a secure Service Fabric cluster in Azure using PowerShell</span></span>
> * <span data-ttu-id="a3dac-108">Clúster de hello segura con un certificado X.509</span><span class="sxs-lookup"><span data-stu-id="a3dac-108">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="a3dac-109">Conectar el clúster toohello mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3dac-109">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="a3dac-110">Eliminación de un clúster</span><span class="sxs-lookup"><span data-stu-id="a3dac-110">Remove a cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3dac-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a3dac-111">Prerequisites</span></span>
<span data-ttu-id="a3dac-112">Antes de empezar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="a3dac-112">Before you begin this tutorial:</span></span>
- <span data-ttu-id="a3dac-113">Si no tiene ninguna suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="a3dac-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="a3dac-114">Instalar hello [módulo de PowerShell y el SDK del servicio de Fabric](service-fabric-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="a3dac-114">Install hello [Service Fabric SDK and PowerShell module](service-fabric-get-started.md)</span></span>
- <span data-ttu-id="a3dac-115">Instalar hello [versión 4.1 o superior del módulo de Powershell de Azure](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span><span class="sxs-lookup"><span data-stu-id="a3dac-115">Install hello [Azure Powershell module version 4.1 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span></span>

<span data-ttu-id="a3dac-116">Hola siguiendo el procedimiento crea una clúster de Service Fabric de vista previa de nodo único (un único equipo virtual).</span><span class="sxs-lookup"><span data-stu-id="a3dac-116">hello following procedure creates a single-node (single virtual machine) preview Service Fabric cluster.</span></span> <span data-ttu-id="a3dac-117">clúster de Hello está protegido por un certificado autofirmado que obtiene crea junto con el clúster de hello y, a continuación, se coloca en un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="a3dac-117">hello cluster is secured by a self-signed certificate that gets created along with hello cluster and then placed in a key vault.</span></span> <span data-ttu-id="a3dac-118">Clústeres de nodo único no se puede escalar más allá de una máquina virtual y clústeres de vista previa no pueden ser versiones toonewer actualizado.</span><span class="sxs-lookup"><span data-stu-id="a3dac-118">Single-node clusters cannot be scaled beyond one virtual machine and preview clusters cannot be upgraded toonewer versions.</span></span>

<span data-ttu-id="a3dac-119">costo toocalculate producido mediante la ejecución de un clúster de Service Fabric en Azure use hello [Calculadora de precios de Azure](https://azure.microsoft.com/pricing/calculator/).</span><span class="sxs-lookup"><span data-stu-id="a3dac-119">toocalculate cost incurred by running a Service Fabric cluster in Azure use hello [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).</span></span>
<span data-ttu-id="a3dac-120">Para más información sobre la creación de clústeres de Service Fabric, consulte el artículo [Creación de un clúster de Service Fabric con Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a3dac-120">For more information on creating Service Fabric clusters, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="create-hello-cluster-using-azure-powershell"></a><span data-ttu-id="a3dac-121">Crear clúster de hello mediante PowerShell de Azure</span><span class="sxs-lookup"><span data-stu-id="a3dac-121">Create hello cluster using Azure PowerShell</span></span>
1. <span data-ttu-id="a3dac-122">Descargar una copia local de la plantilla de Azure Resource Manager hello y archivo de parámetros de Hola de hello [plantilla del Administrador de recursos de Azure para Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="a3dac-122">Download a local copy of hello Azure Resource Manager template and hello parameter file from hello [Azure Resource Manager template for Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub repository.</span></span>  <span data-ttu-id="a3dac-123">*azuredeploy.JSON* es hello Azure Resource Manager plantilla que define un clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a3dac-123">*azuredeploy.json* is hello Azure Resource Manager template that defines a Service Fabric cluster.</span></span> <span data-ttu-id="a3dac-124">*azuredeploy.Parameters.JSON* es un archivo de parámetros para la implementación de clúster de hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="a3dac-124">*azuredeploy.parameters.json* is a parameters file for you toocustomize hello cluster deployment.</span></span>

2. <span data-ttu-id="a3dac-125">Personalizar Hola parámetros Hola siguientes *azuredeploy.parameters.json* archivo de parámetros:</span><span class="sxs-lookup"><span data-stu-id="a3dac-125">Customize hello following parameters in hello *azuredeploy.parameters.json* parameters file:</span></span>

   | <span data-ttu-id="a3dac-126">Parámetro</span><span class="sxs-lookup"><span data-stu-id="a3dac-126">Parameter</span></span>       | <span data-ttu-id="a3dac-127">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3dac-127">Description</span></span> | <span data-ttu-id="a3dac-128">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="a3dac-128">Suggested Value</span></span> |
   | --------------- | ----------- | --------------- |
   | <span data-ttu-id="a3dac-129">clusterLocation</span><span class="sxs-lookup"><span data-stu-id="a3dac-129">clusterLocation</span></span> | <span data-ttu-id="a3dac-130">clúster de Hello región de Azure toowhich toodeploy Hola.</span><span class="sxs-lookup"><span data-stu-id="a3dac-130">hello Azure region toowhich toodeploy hello cluster.</span></span> | <span data-ttu-id="a3dac-131">*Por ejemplo, westeurope, eastasia, eastus*</span><span class="sxs-lookup"><span data-stu-id="a3dac-131">*for example, westeurope, eastasia, eastus*</span></span> |
   | <span data-ttu-id="a3dac-132">clusterName</span><span class="sxs-lookup"><span data-stu-id="a3dac-132">clusterName</span></span>     | <span data-ttu-id="a3dac-133">Nombre del clúster de Hola que desea toocreate.</span><span class="sxs-lookup"><span data-stu-id="a3dac-133">Name of hello cluster you want toocreate.</span></span> | <span data-ttu-id="a3dac-134">*Por ejemplo, bobs-sfpreviewcluster*</span><span class="sxs-lookup"><span data-stu-id="a3dac-134">*for example, bobs-sfpreviewcluster*</span></span> |
   | <span data-ttu-id="a3dac-135">adminUserName</span><span class="sxs-lookup"><span data-stu-id="a3dac-135">adminUserName</span></span>   | <span data-ttu-id="a3dac-136">cuenta de administrador local de Hello en máquinas virtuales del clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="a3dac-136">hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="a3dac-137">*Cualquier nombre de usuario válido de Windows Server*</span><span class="sxs-lookup"><span data-stu-id="a3dac-137">*Any valid Windows Server username*</span></span> |
   | <span data-ttu-id="a3dac-138">adminPassword</span><span class="sxs-lookup"><span data-stu-id="a3dac-138">adminPassword</span></span>   | <span data-ttu-id="a3dac-139">Contraseña de cuenta de administrador local de hello en máquinas virtuales del clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="a3dac-139">Password of hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="a3dac-140">*Cualquier contraseña válida de Windows Server*</span><span class="sxs-lookup"><span data-stu-id="a3dac-140">*Any valid Windows Server password*</span></span> |
   | <span data-ttu-id="a3dac-141">clusterCodeVersion</span><span class="sxs-lookup"><span data-stu-id="a3dac-141">clusterCodeVersion</span></span> | <span data-ttu-id="a3dac-142">Hola toorun de versión de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a3dac-142">hello Service Fabric version toorun.</span></span> <span data-ttu-id="a3dac-143">(255.255.X.255 son versiones preliminares).</span><span class="sxs-lookup"><span data-stu-id="a3dac-143">(255.255.X.255 are preview versions).</span></span> | <span data-ttu-id="a3dac-144">**255.255.5718.255**</span><span class="sxs-lookup"><span data-stu-id="a3dac-144">**255.255.5718.255**</span></span> |
   | <span data-ttu-id="a3dac-145">vmInstanceCount</span><span class="sxs-lookup"><span data-stu-id="a3dac-145">vmInstanceCount</span></span> | <span data-ttu-id="a3dac-146">número de Hola de máquinas virtuales en el clúster (puede ser 1 o 3-99).</span><span class="sxs-lookup"><span data-stu-id="a3dac-146">hello number of virtual machines in your cluster (can be 1 or 3-99).</span></span> | <span data-ttu-id="a3dac-147">**1**</span><span class="sxs-lookup"><span data-stu-id="a3dac-147">**1**</span></span> | <span data-ttu-id="a3dac-148">*Para un clúster de versión preliminar, especifique solo una máquina virtual*.</span><span class="sxs-lookup"><span data-stu-id="a3dac-148">*For a preview cluster specify only one virtual machine*</span></span> |

3. <span data-ttu-id="a3dac-149">Abra una consola de PowerShell, tooAzure de inicio de sesión y seleccione suscripción Hola que desea que toodeploy Hola clúster en:</span><span class="sxs-lookup"><span data-stu-id="a3dac-149">Open a PowerShell console, login tooAzure, and select hello subscription you want toodeploy hello cluster in:</span></span>

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. <span data-ttu-id="a3dac-150">Cree y cifrar una contraseña para hello certificado toobe utilizado por Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a3dac-150">Create and encrypt a password for hello certificate toobe used by Service Fabric.</span></span>

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. <span data-ttu-id="a3dac-151">Crear clúster hello y su certificado ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="a3dac-151">Create hello cluster and its certificate by running hello following command:</span></span>

   ```powershell
      New-AzureRmServiceFabricCluster
          -TemplateFile C:\Users\me\Desktop\azuredeploy.json `
          -ParameterFile C:\Users\me\Desktop\azuredeploy.parameters.json `
          -CertificateOutputFolder C:\Users\me\Desktop\ `
          -CertificatePassword $pwd `
          -CertificateSubjectName "mycluster.westeurope.cloudapp.azure.com" `
          -ResourceGroupName myclusterRG
   ```

   >[!NOTE]
   ><span data-ttu-id="a3dac-152">Hola `-CertificateSubjectName` parámetro debe alinearse con el parámetro de clusterName Hola especificado en el archivo de parámetros de hello, así como Hola dominio vinculado toohello región de Azure ha elegido, como: `clustername.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="a3dac-152">hello `-CertificateSubjectName` parameter should align with hello clusterName parameter specified in hello parameters file, as well as hello domain tied toohello Azure region you chose, such as: `clustername.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="a3dac-153">Una vez finalizada la configuración de hello, envía la información acerca de clúster de hello creado en Azure.</span><span class="sxs-lookup"><span data-stu-id="a3dac-153">Once hello configuration finishes, it outputs information about hello cluster created in Azure.</span></span> <span data-ttu-id="a3dac-154">También copia Hola certificado toohello - CertificateOutputFolder directorio del clúster especificado para este parámetro de ruta de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3dac-154">It also copies hello cluster certificate toohello -CertificateOutputFolder directory on hello path you specified for this parameter.</span></span> <span data-ttu-id="a3dac-155">Necesita esta tooaccess certificado Service Fabric Explorer y ver el estado del Hola del clúster.</span><span class="sxs-lookup"><span data-stu-id="a3dac-155">You need this certificate tooaccess Service Fabric Explorer and view hello health of your cluster.</span></span>

<span data-ttu-id="a3dac-156">Tome nota de la dirección URL de hello para el clúster, que puede ser similar toohello después de la dirección URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span><span class="sxs-lookup"><span data-stu-id="a3dac-156">Take note of hello URL for your cluster, which may be similar toohello following URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span></span>

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a><span data-ttu-id="a3dac-157">Modificar el certificado de Hola y tener acceso a Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="a3dac-157">Modify hello certificate & access Service Fabric Explorer</span></span> ##

1. <span data-ttu-id="a3dac-158">Haga doble clic en hello tooopen de certificado Hola Asistente para importación de certificados.</span><span class="sxs-lookup"><span data-stu-id="a3dac-158">Double-click hello certificate tooopen hello Certificate Import Wizard.</span></span>

2. <span data-ttu-id="a3dac-159">Utilizar la configuración predeterminada, pero que realmente Hola toocheck **marcar esta clave como exportable.**</span><span class="sxs-lookup"><span data-stu-id="a3dac-159">Use default settings, but make sure toocheck hello **Mark this key as exportable.**</span></span> <span data-ttu-id="a3dac-160">casilla de verificación, Hola **protección de clave privada** paso.</span><span class="sxs-lookup"><span data-stu-id="a3dac-160">check box, in hello **private key protection** step.</span></span> <span data-ttu-id="a3dac-161">Visual Studio necesita certificado de hello tooexport al configurar la autenticación de clúster de tejido de registro de contenedor de Azure tooService más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="a3dac-161">Visual Studio needs tooexport hello certificate when configuring Azure Container Registry tooService Fabric Cluster authentication later in this tutorial.</span></span>

3. <span data-ttu-id="a3dac-162">Ahora puede abrir Service Fabric Explorer en un explorador.</span><span class="sxs-lookup"><span data-stu-id="a3dac-162">You can now open Service Fabric Explorer in a browser.</span></span> <span data-ttu-id="a3dac-163">toodo navegue por lo tanto, toohello **ManagementEndpoint** dirección URL para el clúster mediante un explorador web y un certificado de hello select que se guardó en su equipo.</span><span class="sxs-lookup"><span data-stu-id="a3dac-163">toodo so, navigate toohello **ManagementEndpoint** URL for your cluster using a web browser, and select hello certificate that was saved on your machine.</span></span>

>[!NOTE]
><span data-ttu-id="a3dac-164">Al abrir Service Fabric Explorer, verá un error de certificado, ya que está usando un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="a3dac-164">When opening Service Fabric Explorer, you see a certificate error, as you are using a self-signed certificate.</span></span> <span data-ttu-id="a3dac-165">En el borde, tendrás que tooclick *detalles* y, a continuación, Hola *ir en la página Web toohello* vínculo.</span><span class="sxs-lookup"><span data-stu-id="a3dac-165">In Edge, you have tooclick *Details* and then hello *Go on toohello webpage* link.</span></span> <span data-ttu-id="a3dac-166">En Chrome, tendrá que tooclick *avanzadas* y, a continuación, Hola *continuar* vínculo.</span><span class="sxs-lookup"><span data-stu-id="a3dac-166">In Chrome, you have tooclick *Advanced* and then hello *proceed* link.</span></span>

>[!NOTE]
><span data-ttu-id="a3dac-167">Si se produce un error en la creación del clúster hello, siempre puede volver a ejecutar el comando hello, que actualiza los recursos de hello ya implementados.</span><span class="sxs-lookup"><span data-stu-id="a3dac-167">If hello cluster creation fails, you can always rerun hello command, which updates hello resources already deployed.</span></span> <span data-ttu-id="a3dac-168">Si un certificado se creó como parte de la implementación de hello error, se genera uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="a3dac-168">If a certificate was created as part of hello failed deployment, a new one is generated.</span></span> <span data-ttu-id="a3dac-169">creación del clúster tootroubleshoot, consulte [crear un clúster de Service Fabric mediante Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a3dac-169">tootroubleshoot cluster creation, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="connect-toohello-secure-cluster"></a><span data-ttu-id="a3dac-170">Conectar el clúster segura toohello</span><span class="sxs-lookup"><span data-stu-id="a3dac-170">Connect toohello secure cluster</span></span>
<span data-ttu-id="a3dac-171">Conectar con módulo de PowerShell de tejido de servicio de hello instalado con hello tejido SDK del servicio de clúster de toohello.</span><span class="sxs-lookup"><span data-stu-id="a3dac-171">Connect toohello cluster using hello Service Fabric PowerShell module installed with hello Service Fabric SDK.</span></span>  <span data-ttu-id="a3dac-172">En primer lugar, instalar el certificado de hello en almacén de hello Personal del usuario actual de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="a3dac-172">First, install hello certificate into hello Personal (My) store of hello current user on your computer.</span></span>  <span data-ttu-id="a3dac-173">Ejecute el siguiente comando de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="a3dac-173">Run hello following PowerShell command:</span></span>

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

<span data-ttu-id="a3dac-174">Ya estás listo tooconnect tooyour segura clúster.</span><span class="sxs-lookup"><span data-stu-id="a3dac-174">You are now ready tooconnect tooyour secure cluster.</span></span>

<span data-ttu-id="a3dac-175">Hola **Service Fabric** módulo de PowerShell proporciona muchos de los cmdlets para administrar clústeres, aplicaciones y servicios de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a3dac-175">hello **Service Fabric** PowerShell module provides many cmdlets for managing Service Fabric clusters, applications, and services.</span></span>  <span data-ttu-id="a3dac-176">Hola de uso [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) toohello de tooconnect cmdlet clúster segura.</span><span class="sxs-lookup"><span data-stu-id="a3dac-176">Use hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello secure cluster.</span></span> <span data-ttu-id="a3dac-177">Hola huella digital del certificado y detalles del extremo de conexión se encuentran en la salida de hello en un paso anterior.</span><span class="sxs-lookup"><span data-stu-id="a3dac-177">hello certificate thumbprint and connection endpoint details are found in hello output from a previous step.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="a3dac-178">Compruebe que está conectado y clúster de hello es correcto usar hello [ServiceFabricClusterHealth Get](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a3dac-178">Check that you are connected and hello cluster is healthy using hello [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span></span>

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a><span data-ttu-id="a3dac-179">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="a3dac-179">Clean up resources</span></span>

<span data-ttu-id="a3dac-180">Además propio recurso de clúster toohello, un clúster se compone de otros recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a3dac-180">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="a3dac-181">clúster de Hola de manera más sencilla de Hello toodelete y todos los recursos de Hola que consume es grupo de recursos de toodelete Hola.</span><span class="sxs-lookup"><span data-stu-id="a3dac-181">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span>

<span data-ttu-id="a3dac-182">Inicie sesión en tooAzure y seleccione Hola Id. de suscripción con el que desea que el clúster de Hola de tooremove.</span><span class="sxs-lookup"><span data-stu-id="a3dac-182">Log in tooAzure and select hello subscription ID with which you want tooremove hello cluster.</span></span>  <span data-ttu-id="a3dac-183">Puede encontrar el identificador de suscripción, inicie sesión toohello [portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a3dac-183">You can find your subscription ID by logging in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="a3dac-184">Eliminar el grupo de recursos de Hola y todos los recursos de clúster de hello con hello [cmdlet Remove-AzureRMResourceGroup](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="a3dac-184">Delete hello resource group and all hello cluster resources using hello [Remove-AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a><span data-ttu-id="a3dac-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a3dac-185">Next steps</span></span>
<span data-ttu-id="a3dac-186">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="a3dac-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a3dac-187">Creación de un clúster de Service Fabric en Azure</span><span class="sxs-lookup"><span data-stu-id="a3dac-187">Create a Service Fabric cluster in Azure</span></span>
> * <span data-ttu-id="a3dac-188">Clúster de hello segura con un certificado X.509</span><span class="sxs-lookup"><span data-stu-id="a3dac-188">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="a3dac-189">Conectar el clúster toohello mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3dac-189">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="a3dac-190">Eliminación de un clúster</span><span class="sxs-lookup"><span data-stu-id="a3dac-190">Remove a cluster</span></span>

<span data-ttu-id="a3dac-191">A continuación, avanzar toohello después toolearn tutorial cómo toodeploy una aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="a3dac-191">Next, advance toohello following tutorial toolearn how toodeploy an existing application.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="a3dac-192">Implementación de una aplicación .NET con Docker Compose</span><span class="sxs-lookup"><span data-stu-id="a3dac-192">Deploy an existing .NET application with Docker Compose</span></span>](service-fabric-host-app-in-a-container.md)
