---
title: "Administración de certificados en un clúster de Azure Service Fabric | Microsoft Docs"
description: "Describe cómo agregar nuevos certificados, sustituir certificados y quitar certificados de un clúster de Service Fabric."
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
ms.openlocfilehash: c433e8683755e454f9561f094269c3daccf78a62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a><span data-ttu-id="d824a-103">Agregar o quitar certificados para un clúster de Service Fabric de Azure</span><span class="sxs-lookup"><span data-stu-id="d824a-103">Add or remove certificates for a Service Fabric cluster in Azure</span></span>
<span data-ttu-id="d824a-104">Se recomienda leer [Escenarios de seguridad de los clústeres de Service Fabric](service-fabric-cluster-security.md) para familiarizarse con cómo Service Fabric usa los certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="d824a-104">It is recommended that you familiarize yourself with how Service Fabric uses X.509 certificates and be familiar with the [Cluster security scenarios](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="d824a-105">Debe entender qué es un certificado de clúster y para qué se usa antes de seguir avanzando.</span><span class="sxs-lookup"><span data-stu-id="d824a-105">You must understand what a cluster certificate is and what is used for, before you proceed further.</span></span>

<span data-ttu-id="d824a-106">Además de los certificados de client, al configurar la seguridad mediante certificados durante la creación del clúster, Service Fabric le permite especificar dos certificados de clúster: uno principal y uno secundario.</span><span class="sxs-lookup"><span data-stu-id="d824a-106">Service fabric lets you specify two cluster certificates, a primary and a secondary, when you configure certificate security during cluster creation, in addition to client certificates.</span></span> <span data-ttu-id="d824a-107">Consulte el artículo sobre la [creación de un clúster de Service Fabric en Azure Portal](service-fabric-cluster-creation-via-portal.md) o la [creación de un clúster de Azure a través de Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) para más información sobre cómo configurarlos en tiempo de creación.</span><span class="sxs-lookup"><span data-stu-id="d824a-107">Refer to [creating an azure cluster via portal](service-fabric-cluster-creation-via-portal.md) or [creating an azure cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) for details on setting them up at create time.</span></span> <span data-ttu-id="d824a-108">Si se especifica un único certificado de clúster en tiempo de creación, este se utilizará como el certificado principal.</span><span class="sxs-lookup"><span data-stu-id="d824a-108">If you specify only one cluster certificate at create time, then that is used as the primary certificate.</span></span> <span data-ttu-id="d824a-109">Después de la creación del clúster, puede agregar un nuevo certificado como elemento secundario.</span><span class="sxs-lookup"><span data-stu-id="d824a-109">After cluster creation, you can add a new certificate as a secondary.</span></span>

> [!NOTE]
> <span data-ttu-id="d824a-110">Para que un clúster sea seguro, siempre deberá tener implementado al menos un certificado de clúster principal o secundario válido (no revocado ni caducado), o el clúster dejará de funcionar.</span><span class="sxs-lookup"><span data-stu-id="d824a-110">For a secure cluster, you will always need at least one valid (not revoked and not expired) cluster certificate (primary or secondary) deployed (if not, the cluster stops functioning).</span></span> <span data-ttu-id="d824a-111">Cuando falten 90 días para la caducidad de todos los certificados válidos, el sistema genera un seguimiento de advertencias y un evento de estado de advertencia en el nodo.</span><span class="sxs-lookup"><span data-stu-id="d824a-111">90 days before all valid certificates reach expiration, the system generates a warning trace and also a warning health event on the node.</span></span> <span data-ttu-id="d824a-112">Actualmente, Service Fabric no envía ningún mensaje de correo electrónico ni cualquier otra notificación sobre este tema.</span><span class="sxs-lookup"><span data-stu-id="d824a-112">There is currently no email or any other notification that service fabric sends out on this topic.</span></span> 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-the-portal"></a><span data-ttu-id="d824a-113">Incorporación de un certificado de clúster secundario mediante el portal</span><span class="sxs-lookup"><span data-stu-id="d824a-113">Add a secondary cluster certificate using the portal</span></span>

<span data-ttu-id="d824a-114">No se pueden agregar certificados de clúster secundarios mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d824a-114">Secondary cluster certificate cannot be added through the Azure portal.</span></span> <span data-ttu-id="d824a-115">Tendrá que usar Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d824a-115">You have to use Azure powershell for that.</span></span> <span data-ttu-id="d824a-116">El proceso se describe más adelante en este documento.</span><span class="sxs-lookup"><span data-stu-id="d824a-116">The process is outlined later in this document.</span></span>

## <a name="swap-the-cluster-certificates-using-the-portal"></a><span data-ttu-id="d824a-117">Intercambio de los certificados de clúster mediante el portal</span><span class="sxs-lookup"><span data-stu-id="d824a-117">Swap the cluster certificates using the portal</span></span>

<span data-ttu-id="d824a-118">Después de implementar correctamente un certificado de clúster secundario, si desea intercambiar los certificados principales y secundarios, vaya a la hoja Seguridad y, en el menú contextual, seleccione 'Intercambiar con principal' para intercambiar el certificado secundario con el certificado principal.</span><span class="sxs-lookup"><span data-stu-id="d824a-118">After you have successfully deployed a secondary cluster certificate, if you want to swap the primary and secondary, then navigate to the Security blade, and select the 'Swap with primary' option from the context menu to swap the secondary cert with the primary cert.</span></span>

![Intercambiar certificado][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-the-portal"></a><span data-ttu-id="d824a-120">Eliminación de un certificado de clúster mediante el portal</span><span class="sxs-lookup"><span data-stu-id="d824a-120">Remove a cluster certificate using the portal</span></span>

<span data-ttu-id="d824a-121">Para que un clúster sea seguro, siempre deberá tener implementado al menos un certificado principal o secundario válido (no revocado ni caducado), o el clúster dejará de funcionar.</span><span class="sxs-lookup"><span data-stu-id="d824a-121">For a secure cluster, you will always need at least one valid (not revoked and not expired) certificate (primary or secondary) deployed if not, the cluster stops functioning.</span></span>

<span data-ttu-id="d824a-122">Para quitar un certificado secundario y dejar de usarlo para la seguridad del clúster, vaya a la hoja Seguridad y seleccione “Eliminar” en el menú contextual del certificado secundario.</span><span class="sxs-lookup"><span data-stu-id="d824a-122">To remove a secondary certificate from being used for cluster security, Navigate to the Security blade and select the 'Delete' option from the context menu on the secondary certificate.</span></span>

<span data-ttu-id="d824a-123">Si su intención es quitar el certificado que está marcado como principal, debe intercambiarlo primero con el certificado secundario y, después, eliminar la base de datos secundaria una vez completada la actualización.</span><span class="sxs-lookup"><span data-stu-id="d824a-123">If your intent is to remove the certificate that is marked primary, then you will need to swap it with the secondary first, and then delete the secondary after the upgrade has completed.</span></span>

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a><span data-ttu-id="d824a-124">Incorporación de un certificado secundario mediante Powershell para Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d824a-124">Add a secondary certificate using Resource Manager Powershell</span></span>

<span data-ttu-id="d824a-125">En estos pasos se da por hecho que está familiarizado con el funcionamiento de Resource Manager, que ha implementado al menos un clúster de Service Fabric mediante una plantilla de Resource Manager, y que tiene a mano la plantilla que utilizó para configurar el clúster.</span><span class="sxs-lookup"><span data-stu-id="d824a-125">These steps assume that you are familiar with how Resource Manager works and have deployed atleast one Service Fabric cluster using a Resource Manager template, and have the template that you used to set up the cluster handy.</span></span> <span data-ttu-id="d824a-126">También se da por hecho que está familiarizado con el uso de JSON.</span><span class="sxs-lookup"><span data-stu-id="d824a-126">It is also assumed that you are comfortable using JSON.</span></span>

> [!NOTE]
> <span data-ttu-id="d824a-127">Si necesita una plantilla de ejemplo y parámetros para usar como guía o punto de partida, descárguelos desde este [repositorio de GitHub](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="d824a-127">If you are looking for a sample template and parameters that you can use to follow along or as a starting point, then download it from this [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span> 
> 
> 

### <a name="edit-your-resource-manager-template"></a><span data-ttu-id="d824a-128">Edición de la plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d824a-128">Edit your Resource Manager template</span></span>

<span data-ttu-id="d824a-129">Para facilitar las siguientes tareas, el ejemplo 5-VM-1-NodeTypes-Secure_Step2.JSON contiene todas las modificaciones que se van a realizar.</span><span class="sxs-lookup"><span data-stu-id="d824a-129">For ease of following along, sample 5-VM-1-NodeTypes-Secure_Step2.JSON contains all the edits we will be making.</span></span> <span data-ttu-id="d824a-130">El ejemplo está disponible [en el repositorio de GitHub](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="d824a-130">the sample is available at [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span>

<span data-ttu-id="d824a-131">**Asegúrese de seguir todos los pasos**</span><span class="sxs-lookup"><span data-stu-id="d824a-131">**Make sure to follow all the steps**</span></span>

<span data-ttu-id="d824a-132">**Paso 1:** abra la plantilla de Resource Manager que usó para implementar el clúster.</span><span class="sxs-lookup"><span data-stu-id="d824a-132">**Step 1:** Open up the Resource Manager template you used to deploy you Cluster.</span></span> <span data-ttu-id="d824a-133">(Si ha descargado el ejemplo del repositorio anterior, use 5-VM-1-NodeTypes-Secure_Step1.JSON para implementar un clúster seguro y, después, abra esa plantilla).</span><span class="sxs-lookup"><span data-stu-id="d824a-133">(If you have downloaded the sample from the above repo, then Use 5-VM-1-NodeTypes-Secure_Step1.JSON to deploy a secure cluster and then open up that template).</span></span>

<span data-ttu-id="d824a-134">**Paso 2:** agregue **dos parámetros nuevos** "secCertificateThumbprint" y "secCertificateUrlValue" del tipo "string" en la sección de parámetros de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="d824a-134">**Step 2:** Add **two new parameters** "secCertificateThumbprint" and "secCertificateUrlValue" of type "string" to the parameter section of your template.</span></span> <span data-ttu-id="d824a-135">Puede copiar el siguiente fragmento de código y agregarlo a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="d824a-135">You can copy the following code snippet and add it to the template.</span></span> <span data-ttu-id="d824a-136">En función del origen de la plantilla, esto ya estará definido; si es así, continúe con el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="d824a-136">Depending on the source of your template, you may already have these defined, if so move to the next step.</span></span> 
 
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
        "description": "Refers to the location URL in your key vault where the certificate was uploaded, it is should be in the format of https://<name of the vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

<span data-ttu-id="d824a-137">**Paso 3:** modifique el recurso **Microsoft.ServiceFabric/clusters**; busque la definición del recurso "Microsoft.ServiceFabric/clusters" en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="d824a-137">**Step 3:** Make changes to the **Microsoft.ServiceFabric/clusters** resource - Locate the "Microsoft.ServiceFabric/clusters" resource definition in your template.</span></span> <span data-ttu-id="d824a-138">En las propiedades de esa definición, encontrará una etiqueta JSON "Certificate", similar al siguiente fragmento de código JSON:</span><span class="sxs-lookup"><span data-stu-id="d824a-138">Under properties of that definition, you will find "Certificate" JSON tag, which should look something like the following JSON snippet:</span></span>

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="d824a-139">Agregue una nueva etiqueta "thumbprintSecondary" y asígnele un valor "[parameters('secCertificateThumbprint')]".</span><span class="sxs-lookup"><span data-stu-id="d824a-139">Add a new tag "thumbprintSecondary" and give it a value "[parameters('secCertificateThumbprint')]".</span></span>  

<span data-ttu-id="d824a-140">Ahora, la definición del recurso debería ser similar a la siguiente (en función del origen de la plantilla, puede que no sea exactamente igual que este fragmento de código).</span><span class="sxs-lookup"><span data-stu-id="d824a-140">So now the resource definition should look like the following (depending on your source of the template, it may not be exactly like the snippet below).</span></span> 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="d824a-141">Si desea **sustituir el certificado**, especifique el nuevo certificado como principal y cambie el principal actual a secundario.</span><span class="sxs-lookup"><span data-stu-id="d824a-141">If you want to **rollover the cert**, then specify the new cert as primary and moving the current primary as secondary.</span></span> <span data-ttu-id="d824a-142">Como resultado, el certificado principal actual se sustituye por el nuevo certificado en un paso de implementación.</span><span class="sxs-lookup"><span data-stu-id="d824a-142">This results in the rollover of your current primary certificate to the new certificate in one deployment step.</span></span>

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


<span data-ttu-id="d824a-143">**Paso 4:** modifique **todas** las definiciones del recurso **Microsoft.Compute/virtualMachineScaleSets**; busque la definición del recurso Microsoft.Compute/virtualMachineScaleSets.</span><span class="sxs-lookup"><span data-stu-id="d824a-143">**Step 4:** Make changes to **all** the **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate the Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="d824a-144">Desplácese hasta el valor "Microsoft.Azure.ServiceFabric" de "publisher", en "virtualMachineProfile".</span><span class="sxs-lookup"><span data-stu-id="d824a-144">Scroll to the "publisher": "Microsoft.Azure.ServiceFabric", under "virtualMachineProfile".</span></span>

<span data-ttu-id="d824a-145">En la configuración de publicador de Service Fabric, verá algo parecido a esto.</span><span class="sxs-lookup"><span data-stu-id="d824a-145">In the service fabric publisher settings, you should see something like this.</span></span>

![Json_Pub_Setting1][Json_Pub_Setting1]

<span data-ttu-id="d824a-147">Agregue las nuevas entradas de certificado.</span><span class="sxs-lookup"><span data-stu-id="d824a-147">Add the new cert entries to it</span></span>

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

<span data-ttu-id="d824a-148">Las propiedades tendrán ahora un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="d824a-148">The properties should now look like this</span></span>

![Json_Pub_Setting2][Json_Pub_Setting2]

<span data-ttu-id="d824a-150">Si desea **sustituir el certificado**, especifique el nuevo certificado como principal y cambie el principal actual a secundario.</span><span class="sxs-lookup"><span data-stu-id="d824a-150">If you want to **rollover the cert**, then specify the new cert as primary and moving the current primary as secondary.</span></span> <span data-ttu-id="d824a-151">Esto provoca la sustitución del certificado actual por el nuevo certificado en un paso de implementación.</span><span class="sxs-lookup"><span data-stu-id="d824a-151">This results in the rollover of your current certificate to the new certificate in one deployment step.</span></span> 


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
<span data-ttu-id="d824a-152">Las propiedades tendrán ahora un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="d824a-152">The properties should now look like this</span></span>

![Json_Pub_Setting3][Json_Pub_Setting3]


<span data-ttu-id="d824a-154">**Paso 5:** modifique **todas** las definiciones del recurso **Microsoft.Compute/virtualMachineScaleSets**; busque la definición del recurso Microsoft.Compute/virtualMachineScaleSets.</span><span class="sxs-lookup"><span data-stu-id="d824a-154">**Step 5:** Make Changes to **all** the **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate the Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="d824a-155">Vaya a "vaultCertificates":, en "OSProfile".</span><span class="sxs-lookup"><span data-stu-id="d824a-155">Scroll to the "vaultCertificates": , under "OSProfile".</span></span> <span data-ttu-id="d824a-156">Tendrá un aspecto similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="d824a-156">it should look something like this.</span></span>


![Json_Pub_Setting4][Json_Pub_Setting4]

<span data-ttu-id="d824a-158">Agregue el valor de secCertificateUrlValue.</span><span class="sxs-lookup"><span data-stu-id="d824a-158">Add the secCertificateUrlValue to it.</span></span> <span data-ttu-id="d824a-159">Use el siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="d824a-159">use the following snippet:</span></span>

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
<span data-ttu-id="d824a-160">Ahora, el código JSON resultante será similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="d824a-160">Now the resulting Json should look something like this.</span></span>
<span data-ttu-id="d824a-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span><span class="sxs-lookup"><span data-stu-id="d824a-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span></span>


> [!NOTE]
> <span data-ttu-id="d824a-162">Asegúrese de repetir los pasos 4 y 5 para todas las definiciones del recurso Nodetypes/Microsoft.Compute/virtualMachineScaleSets de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="d824a-162">Make sure that you have repeated steps 4 and 5 for all the Nodetypes/Microsoft.Compute/virtualMachineScaleSets resource definitions in your template.</span></span> <span data-ttu-id="d824a-163">Si se salta una, el certificado no se instalará en esa máquina VMSS y tendrá resultados impredecibles en el clúster, incluso el clúster puede deja de funcionar (si finalmente no hay ningún certificado válido que el clúster pueda usar para la seguridad).</span><span class="sxs-lookup"><span data-stu-id="d824a-163">If you miss one of them, the certificate will not get installed on that VMSS and you will have unpredictable results in your cluster, including the cluster going down (if you end up with no valid certificates that the cluster can use for security.</span></span> <span data-ttu-id="d824a-164">Compruébelo dos veces antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="d824a-164">So please double check, before proceeding further.</span></span>
> 
> 


### <a name="edit-your-template-file-to-reflect-the-new-parameters-you-added-above"></a><span data-ttu-id="d824a-165">Edición del archivo de plantilla para reflejar los nuevos parámetros agregados anteriormente</span><span class="sxs-lookup"><span data-stu-id="d824a-165">Edit your template file to reflect the new parameters you added above</span></span>
<span data-ttu-id="d824a-166">Si está usando el ejemplo del [repositorio de GitHub](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) para seguir el artículo, puede empezar a hacer estos cambios en el ejemplo 5-VM-1-NodeTypes-Secure_Step2.JSON.</span><span class="sxs-lookup"><span data-stu-id="d824a-166">If you are using the sample from the [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) to follow along, you can start to make changes in The sample 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span></span> 

<span data-ttu-id="d824a-167">Modifique el parámetro File de la plantilla de Resource Manager, y agregue los dos nuevos parámetros para secCertificateThumbprint y secCertificateUrlValue.</span><span class="sxs-lookup"><span data-stu-id="d824a-167">Edit your Resource Manager Template parameter File, add the two new parameters for secCertificateThumbprint and secCertificateUrlValue.</span></span> 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers to the location URL in your key vault where the certificate was uploaded, it is should be in the format of https://<name of the vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-the-template-to-azure"></a><span data-ttu-id="d824a-168">Implementación de la plantilla en Azure</span><span class="sxs-lookup"><span data-stu-id="d824a-168">Deploy the template to Azure</span></span>

- <span data-ttu-id="d824a-169">Ahora está preparado para implementar la plantilla en Azure.</span><span class="sxs-lookup"><span data-stu-id="d824a-169">You are now ready to deploy your template to Azure.</span></span> <span data-ttu-id="d824a-170">Abra un símbolo del sistema de Azure PS versión 1 o superior.</span><span class="sxs-lookup"><span data-stu-id="d824a-170">Open an Azure PS version 1+ command prompt.</span></span>
- <span data-ttu-id="d824a-171">Inicie sesión en su cuenta de Azure y seleccione la suscripción de Azure específica.</span><span class="sxs-lookup"><span data-stu-id="d824a-171">Log in to your Azure Account and select the specific azure subscription.</span></span> <span data-ttu-id="d824a-172">Este es un paso importante para personas que tienen acceso a más de una suscripción.</span><span class="sxs-lookup"><span data-stu-id="d824a-172">This is an important step for folks who have access to more than one azure subscription.</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

<span data-ttu-id="d824a-173">Pruebe la plantilla antes de implementarla.</span><span class="sxs-lookup"><span data-stu-id="d824a-173">Test the template prior to deploying it.</span></span> <span data-ttu-id="d824a-174">Utilice el grupo de recursos en el que esté implementado el clúster actualmente.</span><span class="sxs-lookup"><span data-stu-id="d824a-174">Use the same Resource Group that your cluster is currently deployed to.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

<span data-ttu-id="d824a-175">Implemente la plantilla en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d824a-175">Deploy the template to your resource group.</span></span> <span data-ttu-id="d824a-176">Utilice el grupo de recursos en el que esté implementado el clúster actualmente.</span><span class="sxs-lookup"><span data-stu-id="d824a-176">Use the same Resource Group that your cluster is currently deployed to.</span></span> <span data-ttu-id="d824a-177">Ejecute el comando New-AzureRmResourceGroupDeployment.</span><span class="sxs-lookup"><span data-stu-id="d824a-177">Run the New-AzureRmResourceGroupDeployment command.</span></span> <span data-ttu-id="d824a-178">No es necesario especificar el modo, ya que el valor predeterminado es **incremental**.</span><span class="sxs-lookup"><span data-stu-id="d824a-178">You do not need to specify the mode, since the default value is **incremental**.</span></span>

> [!NOTE]
> <span data-ttu-id="d824a-179">Si establece el modo completo, podría eliminar accidentalmente los recursos que no estén en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="d824a-179">If you set Mode to Complete, you can inadvertently delete resources that are not in your template.</span></span> <span data-ttu-id="d824a-180">Por ello no lo utilice en este escenario.</span><span class="sxs-lookup"><span data-stu-id="d824a-180">So do not use it in this scenario.</span></span>
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

<span data-ttu-id="d824a-181">Este es un ejemplo ya rellenado del mismo powershell.</span><span class="sxs-lookup"><span data-stu-id="d824a-181">Here is a filled out example of the same powershell.</span></span>

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

<span data-ttu-id="d824a-182">Una vez completada la implementación, conecte el clúster mediante el nuevo certificado y realice algunas consultas.</span><span class="sxs-lookup"><span data-stu-id="d824a-182">Once the deployment is complete, connect to your cluster using the new Certificate and perform some queries.</span></span> <span data-ttu-id="d824a-183">Siempre que sea capaz de ello.</span><span class="sxs-lookup"><span data-stu-id="d824a-183">If you are able to do.</span></span> <span data-ttu-id="d824a-184">Después, puede eliminar el antiguo certificado.</span><span class="sxs-lookup"><span data-stu-id="d824a-184">Then you can delete the old certificate.</span></span> 

<span data-ttu-id="d824a-185">Si está utilizando un certificado autofirmado, no olvide importarlo en su almacén de certificados local TrustedPeople.</span><span class="sxs-lookup"><span data-stu-id="d824a-185">If you are using a self-signed certificate, do not forget to import them into your local TrustedPeople cert store.</span></span>

```powershell
######## Set up the certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
<span data-ttu-id="d824a-186">Como referencia rápida, este es el comando para conectarse a un clúster seguro</span><span class="sxs-lookup"><span data-stu-id="d824a-186">For quick reference here is the command to connect to a secure cluster</span></span> 

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
<span data-ttu-id="d824a-187">Como referencia rápida, este es el comando para obtener el estado del clúster</span><span class="sxs-lookup"><span data-stu-id="d824a-187">For quick reference here is the command to get cluster health</span></span>

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-to-the-cluster"></a><span data-ttu-id="d824a-188">Implementación de certificados de aplicación en el clúster.</span><span class="sxs-lookup"><span data-stu-id="d824a-188">Deploying Application certificates to the cluster.</span></span>

<span data-ttu-id="d824a-189">Puede usar los mismos pasos descritos en el paso 5 anterior para implementar los certificados en los nodos desde un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="d824a-189">You can use the same steps as outlined in Steps 5 above to have the certificates deployed from a keyvault to the Nodes.</span></span> <span data-ttu-id="d824a-190">Solo necesita definir y usar parámetros diferentes.</span><span class="sxs-lookup"><span data-stu-id="d824a-190">you just need define and use different parameters.</span></span>


## <a name="adding-or-removing-client-certificates"></a><span data-ttu-id="d824a-191">Incorporación o eliminación de certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="d824a-191">Adding or removing Client certificates</span></span>

<span data-ttu-id="d824a-192">Además de los certificados de clúster, puede agregar certificados de cliente para llevar a cabo operaciones de administración en un clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d824a-192">In addition to the cluster certificates, you can add client certificates to perform management operations on a service fabric cluster.</span></span>

<span data-ttu-id="d824a-193">Puede agregar dos tipos de certificados de cliente: administrador o solo lectura.</span><span class="sxs-lookup"><span data-stu-id="d824a-193">You can add two kinds of client certificates - Admin or Read-only.</span></span> <span data-ttu-id="d824a-194">Estos se pueden usar para controlar el acceso a las operaciones de administración y a las operaciones de consulta en el clúster.</span><span class="sxs-lookup"><span data-stu-id="d824a-194">These then can be used to control access to the admin operations and Query operations on the cluster.</span></span> <span data-ttu-id="d824a-195">De forma predeterminada, los certificados de clúster se agregan a la lista de certificados de administración permitidos.</span><span class="sxs-lookup"><span data-stu-id="d824a-195">By default, the cluster certificates are added to the allowed Admin certificates list.</span></span>

<span data-ttu-id="d824a-196">Puede especificar cualquier número de certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="d824a-196">you can specify any number of client certificates.</span></span> <span data-ttu-id="d824a-197">Cada incorporación o eliminación provoca una actualización de la configuración en el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d824a-197">Each addition/deletion results in a configuration update to the service fabric cluster</span></span>


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a><span data-ttu-id="d824a-198">Incorporación de certificados de cliente de administrador o solo lectura mediante el portal</span><span class="sxs-lookup"><span data-stu-id="d824a-198">Adding client certificates - Admin or Read-Only via portal</span></span>

1. <span data-ttu-id="d824a-199">Vaya a la hoja Seguridad y seleccione el botón "+ Autenticación" en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="d824a-199">Navigate to the Security blade, and select the '+ Authentication' button on top of the security blade.</span></span>
2. <span data-ttu-id="d824a-200">En la hoja 'Agregar autenticación', en 'Tipo de autenticación', elija 'Cliente de solo lectura' o 'Cliente de administración'.</span><span class="sxs-lookup"><span data-stu-id="d824a-200">On the 'Add Authentication' blade, choose the 'Authentication Type' - 'Read-only client' or 'Admin client'</span></span>
3. <span data-ttu-id="d824a-201">Ahora, elija el método de autorización.</span><span class="sxs-lookup"><span data-stu-id="d824a-201">Now choose the Authorization method.</span></span> <span data-ttu-id="d824a-202">Indica a Service Fabric si se debe buscar este certificado mediante el nombre del sujeto o la huella digital.</span><span class="sxs-lookup"><span data-stu-id="d824a-202">This indicates to Service Fabric whether it should look up this certificate by using the subject name or the thumbprint.</span></span> <span data-ttu-id="d824a-203">Por lo general, no es una buena práctica de seguridad usar el método de autorización de nombre de sujeto.</span><span class="sxs-lookup"><span data-stu-id="d824a-203">In general, it is not a good security practice to use the authorization method of subject name.</span></span> 

![Incorporación de certificados de cliente][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-the-portal"></a><span data-ttu-id="d824a-205">Eliminación de certificados de cliente de administrador o solo lectura mediante el portal</span><span class="sxs-lookup"><span data-stu-id="d824a-205">Deletion of Client Certificates - Admin or Read-Only using the portal</span></span>

<span data-ttu-id="d824a-206">Para quitar un certificado secundario y dejar de usarlo para la seguridad del clúster, vaya a la hoja Seguridad y seleccione “Eliminar” en el menú contextual del certificado especificado.</span><span class="sxs-lookup"><span data-stu-id="d824a-206">To remove a secondary certificate from being used for cluster security, Navigate to the Security blade and select the 'Delete' option from the context menu on the specific certificate.</span></span>



## <a name="next-steps"></a><span data-ttu-id="d824a-207">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d824a-207">Next steps</span></span>
<span data-ttu-id="d824a-208">Lea estos artículos para más información sobre la administración de clúster:</span><span class="sxs-lookup"><span data-stu-id="d824a-208">Read these articles for more information on cluster management:</span></span>

* [<span data-ttu-id="d824a-209">Proceso de actualización del clúster de Service Fabric y expectativas del usuario</span><span class="sxs-lookup"><span data-stu-id="d824a-209">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="d824a-210">Control de acceso basado en roles para clientes de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d824a-210">Setup role-based access for clients</span></span>](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


