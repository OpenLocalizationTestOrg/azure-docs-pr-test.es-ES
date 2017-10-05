---
title: "Preguntas frecuentes sobre los conjuntos de escalado de máquinas virtuales de Azure | Microsoft Docs"
description: "Obtenga respuestas a preguntas frecuentes sobre los conjuntos de escalado de máquinas virtuales."
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: negat
ms.custom: na
ms.openlocfilehash: f320dd5d1f8c99317792f4ae9e09bc5adaf79e25
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a><span data-ttu-id="9e511-103">Preguntas frecuentes sobre los conjuntos de escalado de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="9e511-103">Azure virtual machine scale sets FAQs</span></span>

<span data-ttu-id="9e511-104">Obtenga respuestas a preguntas frecuentes sobre los conjuntos de escalado de máquinas virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="9e511-104">Get answers to frequently asked questions about virtual machine scale sets in Azure.</span></span>

## <a name="autoscale"></a><span data-ttu-id="9e511-105">Autoscale</span><span class="sxs-lookup"><span data-stu-id="9e511-105">Autoscale</span></span>

### <a name="what-are-best-practices-for-azure-autoscale"></a><span data-ttu-id="9e511-106">¿Cuáles son los procedimientos recomendados para el escalado automático de Azure?</span><span class="sxs-lookup"><span data-stu-id="9e511-106">What are best practices for Azure Autoscale?</span></span>

<span data-ttu-id="9e511-107">Para procedimientos recomendados para el escalado automático, consulte [Procedimientos recomendados de escalado automático en elementos virtuales](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span><span class="sxs-lookup"><span data-stu-id="9e511-107">For best practices for Autoscale, see [Best practices for autoscaling virtual machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span></span>

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a><span data-ttu-id="9e511-108">¿Dónde puedo encontrar los nombres de métricas para un escalado automático que use métricas basadas en host?</span><span class="sxs-lookup"><span data-stu-id="9e511-108">Where do I find metric names for autoscaling that uses host-based metrics?</span></span>

<span data-ttu-id="9e511-109">Para nombres de métrica para un escalado automático que use métricas basadas en host, consulte [Métricas compatibles con Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span><span class="sxs-lookup"><span data-stu-id="9e511-109">For metric names for autoscaling that uses host-based metrics, see [Supported metrics with Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span></span>

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a><span data-ttu-id="9e511-110">¿Hay algún ejemplo de escalado automático basado en una longitud de cola y un tema de Azure Service Bus?</span><span class="sxs-lookup"><span data-stu-id="9e511-110">Are there any examples of autoscaling based on an Azure Service Bus topic and queue length?</span></span>

<span data-ttu-id="9e511-111">Sí.</span><span class="sxs-lookup"><span data-stu-id="9e511-111">Yes.</span></span> <span data-ttu-id="9e511-112">Para ejemplos de escalado automático basados en un tema de Service Bus y una longitud de cola, consulte [Métricas comunes de escalado automático de Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span><span class="sxs-lookup"><span data-stu-id="9e511-112">For examples of autoscaling based on an Azure Service Bus topic and queue length, see [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span></span>

<span data-ttu-id="9e511-113">Para una cola de Service Bus, use el siguiente JSON:</span><span class="sxs-lookup"><span data-stu-id="9e511-113">For a Service Bus queue, use the following JSON:</span></span>

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

<span data-ttu-id="9e511-114">Para una cola de almacenamiento, use el siguiente JSON:</span><span class="sxs-lookup"><span data-stu-id="9e511-114">For a storage queue, use the following JSON:</span></span>

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

<span data-ttu-id="9e511-115">Reemplace los valores de ejemplo con los identificadores uniformes de recursos (URI) del recurso.</span><span class="sxs-lookup"><span data-stu-id="9e511-115">Replace example values with your resource Uniform Resource Identifiers (URIs).</span></span>


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a><span data-ttu-id="9e511-116">¿Debo realizar el escalado automático usando métricas basadas en host o usar una extensión de diagnóstico?</span><span class="sxs-lookup"><span data-stu-id="9e511-116">Should I autoscale by using host-based metrics or a diagnostics extension?</span></span>

<span data-ttu-id="9e511-117">Puede crear una configuración de escalado automático en una máquina virtual para usar las métricas de nivel de host, o usar las métricas basadas en SO invitado.</span><span class="sxs-lookup"><span data-stu-id="9e511-117">You can create an autoscale setting on a VM to use host-level metrics or guest OS-based metrics.</span></span>

<span data-ttu-id="9e511-118">Para obtener una lista de métricas admitidas, consulte [Métricas comunes de escalado automático de Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span><span class="sxs-lookup"><span data-stu-id="9e511-118">For a list of supported metrics, see [Azure Monitor autoscaling common metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span></span> 

<span data-ttu-id="9e511-119">Para obtener un ejemplo completo para conjuntos de escalado de máquinas virtuales, consulte [Configuración avanzada de escalado automático con plantillas de Resource Manager para conjuntos de escalado de máquinas virtuales](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span><span class="sxs-lookup"><span data-stu-id="9e511-119">For a full sample for virtual machine scale sets, see [Advanced autoscale configuration by using Resource Manager templates for virtual machine scale sets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span></span> 

<span data-ttu-id="9e511-120">El ejemplo utiliza la métrica de CPU de nivel de host y una métrica de recuento de mensajes.</span><span class="sxs-lookup"><span data-stu-id="9e511-120">The sample uses the host-level CPU metric and a message count metric.</span></span>



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a><span data-ttu-id="9e511-121">¿Cómo se configuran las reglas de alerta en un conjunto de escalado de máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="9e511-121">How do I set alert rules on a virtual machine scale set?</span></span>

<span data-ttu-id="9e511-122">Puede crear alertas en las métricas de los conjuntos de escalado de máquinas virtuales a través de PowerShell o CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e511-122">You can create alerts on metrics for virtual machine scale sets via PowerShell or Azure CLI.</span></span> <span data-ttu-id="9e511-123">Para más información, consulte [Ejemplos de inicio rápido de PowerShell de Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) y [Ejemplos de inicio rápido de CLI multiplataforma de Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span><span class="sxs-lookup"><span data-stu-id="9e511-123">For more information, see [Azure Monitor PowerShell quick start samples](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) and [Azure Monitor cross-platform CLI quick start samples](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span></span>

<span data-ttu-id="9e511-124">El elemento TargetResourceId del conjunto de escalado de máquinas virtuales tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="9e511-124">The TargetResourceId of the virtual machine scale set looks like this:</span></span> 

<span data-ttu-id="9e511-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span><span class="sxs-lookup"><span data-stu-id="9e511-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span></span>

<span data-ttu-id="9e511-126">Puede elegir cualquier contador de rendimiento de máquina virtual como métrica sobre la que establecer la alerta.</span><span class="sxs-lookup"><span data-stu-id="9e511-126">You can choose any VM performance counter as the metric to set an alert for.</span></span> <span data-ttu-id="9e511-127">Para más información, consulte [Métricas de SO invitado para máquinas virtuales Windows basadas en Resource Manager](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) y [Métricas de SO invitado para máquinas virtuales Linux](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) en el artículo [Métricas comunes de escalado automático de Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span><span class="sxs-lookup"><span data-stu-id="9e511-127">For more information, see [Guest OS metrics for Resource Manager-based Windows VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) and [Guest OS metrics for Linux VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in the [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/) article.</span></span>

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a><span data-ttu-id="9e511-128">¿Cómo se configura el escalado automático en un conjunto de escalado de máquinas virtuales utilizando PowerShell?</span><span class="sxs-lookup"><span data-stu-id="9e511-128">How do I set up autoscale on a virtual machine scale set by using PowerShell?</span></span>

<span data-ttu-id="9e511-129">Para configurar el escalado automático en un conjunto de escalado de máquinas virtuales que se establece mediante el uso de PowerShell, consulte la entrada de blog [How to add autoscale to an Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/) (Cómo agregar escalado automático a un conjunto de escalado de máquinas virtuales de Azure).</span><span class="sxs-lookup"><span data-stu-id="9e511-129">To set up autoscale on a virtual machine scale set by using PowerShell, see the blog post [How to add autoscale to an Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span></span>




## <a name="certificates"></a><span data-ttu-id="9e511-130">Certificados</span><span class="sxs-lookup"><span data-stu-id="9e511-130">Certificates</span></span>

### <a name="how-do-i-securely-ship-a-certificate-to-the-vm-how-do-i-provision-a-virtual-machine-scale-set-to-run-a-website-where-the-ssl-for-the-website-is-shipped-securely-from-a-certificate-configuration-the-common-certificate-rotation-operation-would-be-almost-the-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-to-do-this"></a><span data-ttu-id="9e511-131">¿Cómo se envía de forma segura un certificado a la máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="9e511-131">How do I securely ship a certificate to the VM?</span></span> <span data-ttu-id="9e511-132">¿Cómo puedo realizar el aprovisionamiento de un conjunto de escalado de máquinas virtuales para ejecutar un sitio web donde el SSL del sitio web se envíe de forma segura a partir de una configuración de certificado?</span><span class="sxs-lookup"><span data-stu-id="9e511-132">How do I provision a virtual machine scale set to run a website where the SSL for the website is shipped securely from a certificate configuration?</span></span> <span data-ttu-id="9e511-133">(La operación común de rotación de certificados sería casi igual a una operación de actualización de la configuración). ¿Puedo ver un ejemplo de cómo hacerlo?</span><span class="sxs-lookup"><span data-stu-id="9e511-133">(The common certificate rotation operation would be almost the same as a configuration update operation.) Do you have an example of how to do this?</span></span> 

<span data-ttu-id="9e511-134">Para enviar de forma segura un certificado a la máquina virtual, puede instalar un certificado de cliente directamente en un almacén de certificados de Windows desde el almacén de claves del cliente.</span><span class="sxs-lookup"><span data-stu-id="9e511-134">To securely ship a certificate to the VM, you can install a customer certificate directly into a Windows certificate store from the customer's key vault.</span></span>

<span data-ttu-id="9e511-135">Use el siguiente JSON:</span><span class="sxs-lookup"><span data-stu-id="9e511-135">Use the following JSON:</span></span>

```json
"secrets": [
    {
        "sourceVault": {
            "id": "/subscriptions/{subscriptionid}/resourceGroups/myrg1/providers/Microsoft.KeyVault/vaults/mykeyvault1"
        },
        "vaultCertificates": [
            {
                "certificateUrl": "https://mykeyvault1.vault.azure.net/secrets/{secretname}/{secret-version}",
                "certificateStore": "certificateStoreName"
            }
        ]
    }
]
```

<span data-ttu-id="9e511-136">El código admite Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="9e511-136">The code supports Windows and Linux.</span></span>

<span data-ttu-id="9e511-137">Para más información, consulte el artículo sobre la [creación o actualización de un conjunto de escalado de máquinas virtuales](https://msdn.microsoft.com/library/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e511-137">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx).</span></span>


### <a name="example-of-self-signed-certificate"></a><span data-ttu-id="9e511-138">Ejemplo de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="9e511-138">Example of Self-signed certificate</span></span>

1.  <span data-ttu-id="9e511-139">Creación de un certificado autofirmado en un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="9e511-139">Create a self-signed certificate in a key vault.</span></span>

    <span data-ttu-id="9e511-140">Utilice los siguientes comandos de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9e511-140">Use the following PowerShell commands:</span></span>

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    <span data-ttu-id="9e511-141">Este comando le proporciona la entrada para la plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9e511-141">This command gives you the input for the Azure Resource Manager template.</span></span>

    <span data-ttu-id="9e511-142">Para obtener un ejemplo de cómo crear un certificado autofirmado en un almacén de claves, consulte [Escenarios de seguridad de los clústeres de Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span><span class="sxs-lookup"><span data-stu-id="9e511-142">For an example of how to create a self-signed certificate in a key vault, see [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span></span>

2.  <span data-ttu-id="9e511-143">Creación de la plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9e511-143">Change the Resource Manager template.</span></span>

    <span data-ttu-id="9e511-144">Agregue esta propiedad a **virtualMachineProfile** como parte del recurso del conjunto de escalado de máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="9e511-144">Add this property to **virtualMachineProfile**, as part of the virtual machine scale set resource:</span></span>

    ```json 
    "osProfile": {
        "computerNamePrefix": "[variables('namingInfix')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "secrets": [
            {
                "sourceVault": {
                    "id": "[resourceId('KeyVault', 'Microsoft.KeyVault/vaults', 'MikhegnVault')]"
                },
                "vaultCertificates": [
                    {
                        "certificateUrl": "https://mikhegnvault.vault.azure.net:443/secrets/VMSSCert/20709ca8faee4abb84bc6f4611b088a4",
                        "certificateStore": "My"
                    }
                ]
            }
        ]
    }
    ```
  

### <a name="can-i-specify-an-ssh-key-pair-to-use-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a><span data-ttu-id="9e511-145">¿Puedo especificar un par de claves SSH para usar en la autenticación de SSH con un conjunto de escalado de máquinas virtuales Linux desde una plantilla de Resource Manager?</span><span class="sxs-lookup"><span data-stu-id="9e511-145">Can I specify an SSH key pair to use for SSH authentication with a Linux virtual machine scale set from a Resource Manager template?</span></span>  

<span data-ttu-id="9e511-146">Sí.</span><span class="sxs-lookup"><span data-stu-id="9e511-146">Yes.</span></span> <span data-ttu-id="9e511-147">La API de REST para **osProfile** es similar a la API de REST de máquina virtual estándar.</span><span class="sxs-lookup"><span data-stu-id="9e511-147">The REST API for **osProfile** is similar to the standard VM REST API.</span></span> 

<span data-ttu-id="9e511-148">Incluya **osProfile** en la plantilla:</span><span class="sxs-lookup"><span data-stu-id="9e511-148">Include **osProfile** in your template:</span></span>

```json 
"osProfile": {
    "computerName": "[variables('vmName')]",
    "adminUsername": "[parameters('adminUserName')]",
    "linuxConfiguration": {
        "disablePasswordAuthentication": "true",
        "ssh": {
            "publicKeys": [
                {
                    "path": "[variables('sshKeyPath')]",
                    "keyData": "[parameters('sshKeyData')]"
                }
            ]
        }
    }
}
```
 
<span data-ttu-id="9e511-149">Este bloque JSON se usa en [la plantilla de inicio rápido de GitHub 101-vm-sshkey](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="9e511-149">This JSON block is used in [the 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>
 
<span data-ttu-id="9e511-150">El perfil de SO se utiliza también en [la plantilla de inicio rápido de GitHub grelayhost.json](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span><span class="sxs-lookup"><span data-stu-id="9e511-150">The OS profile also is used in [the grelayhost.json GitHub quick start template](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span></span>

<span data-ttu-id="9e511-151">Para más información, consulte el artículo sobre la [creación o actualización de un conjunto de escalado de máquinas virtuales](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span><span class="sxs-lookup"><span data-stu-id="9e511-151">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span></span>
  

### <a name="how-do-i-remove-deprecated-certificates"></a><span data-ttu-id="9e511-152">¿Cómo se quitan los certificados en desuso?</span><span class="sxs-lookup"><span data-stu-id="9e511-152">How do I remove deprecated certificates?</span></span> 

<span data-ttu-id="9e511-153">Para quitar certificados en desuso, quite el certificado antiguo de la lista de certificados del almacén.</span><span class="sxs-lookup"><span data-stu-id="9e511-153">To remove deprecated certificates, remove the old certificate from the vault certificates list.</span></span> <span data-ttu-id="9e511-154">Deje en la lista todos los certificados que desee que permanezcan en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9e511-154">Leave all the certificates that you want to remain on your computer in the list.</span></span> <span data-ttu-id="9e511-155">Esto no quita el certificado de todas las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9e511-155">This does not remove the certificate from all your VMs.</span></span> <span data-ttu-id="9e511-156">Tampoco agrega el certificado a las nuevas máquinas virtuales que se creen en el conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9e511-156">It also does not add the certificate to new VMs that are created in the virtual machine scale set.</span></span> 

<span data-ttu-id="9e511-157">Para quitar el certificado de las máquinas virtuales existentes, tiene que escribir una extensión de script personalizado que quite manualmente los certificados del almacén de certificados.</span><span class="sxs-lookup"><span data-stu-id="9e511-157">To remove the certificate from existing VMs, write a custom script extension to manually remove the certificates from your certificate store.</span></span>
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-the-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-to-store-the-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a><span data-ttu-id="9e511-158">¿Cómo puedo inyectar una clave pública SSH existente en la capa SSH del conjunto de escalado de máquinas virtuales durante el aprovisionamiento?</span><span class="sxs-lookup"><span data-stu-id="9e511-158">How do I inject an existing SSH public key into the virtual machine scale set SSH layer during provisioning?</span></span> <span data-ttu-id="9e511-159">Quiero almacenar los valores de clave pública SSH en Azure Key Vault y luego usarlos en la plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9e511-159">I want to store the SSH public key values in Azure Key Vault, and then use them in my Resource Manager template.</span></span>

<span data-ttu-id="9e511-160">Si va a proporcionar a las máquinas virtuales solo una clave SSH pública, no es necesario colocar las claves públicas en Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9e511-160">If you are providing the VMs only with a public SSH key, you don't need to put the public keys in Key Vault.</span></span> <span data-ttu-id="9e511-161">Las claves públicas no son secretas.</span><span class="sxs-lookup"><span data-stu-id="9e511-161">Public keys are not secret.</span></span>
 
<span data-ttu-id="9e511-162">Puede proporcionar claves públicas SSH en texto sin formato al crear una máquina virtual Linux:</span><span class="sxs-lookup"><span data-stu-id="9e511-162">You can provide SSH public keys in plain text when you create a Linux VM:</span></span>

```json
"linuxConfiguration": {
    "ssh": {
        "publicKeys": [
            {
                "path": "path",
                "keyData": "publickey"
            }
        ]
    }
```
 
<span data-ttu-id="9e511-163">Nombre del elemento de linuxConfiguration</span><span class="sxs-lookup"><span data-stu-id="9e511-163">linuxConfiguration element name</span></span> | <span data-ttu-id="9e511-164">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="9e511-164">Required</span></span> | <span data-ttu-id="9e511-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="9e511-165">Type</span></span> | <span data-ttu-id="9e511-166">Descripción</span><span class="sxs-lookup"><span data-stu-id="9e511-166">Description</span></span>
--- | --- | --- | --- |  ---
<span data-ttu-id="9e511-167">ssh</span><span class="sxs-lookup"><span data-stu-id="9e511-167">ssh</span></span> | <span data-ttu-id="9e511-168">No</span><span class="sxs-lookup"><span data-stu-id="9e511-168">No</span></span> | <span data-ttu-id="9e511-169">Colección</span><span class="sxs-lookup"><span data-stu-id="9e511-169">Collection</span></span> | <span data-ttu-id="9e511-170">Especifica la configuración de la clave SSH para un sistema operativo Linux</span><span class="sxs-lookup"><span data-stu-id="9e511-170">Specifies the SSH key configuration for a Linux OS</span></span>
<span data-ttu-id="9e511-171">path</span><span class="sxs-lookup"><span data-stu-id="9e511-171">path</span></span> | <span data-ttu-id="9e511-172">Sí</span><span class="sxs-lookup"><span data-stu-id="9e511-172">Yes</span></span> | <span data-ttu-id="9e511-173">string</span><span class="sxs-lookup"><span data-stu-id="9e511-173">String</span></span> | <span data-ttu-id="9e511-174">Especifica la ruta de acceso de Linux en donde se deben colocar las claves SSH o el certificado</span><span class="sxs-lookup"><span data-stu-id="9e511-174">Specifies the Linux file path where the SSH keys or certificate should be located</span></span>
<span data-ttu-id="9e511-175">keyData</span><span class="sxs-lookup"><span data-stu-id="9e511-175">keyData</span></span> | <span data-ttu-id="9e511-176">Sí</span><span class="sxs-lookup"><span data-stu-id="9e511-176">Yes</span></span> | <span data-ttu-id="9e511-177">string</span><span class="sxs-lookup"><span data-stu-id="9e511-177">String</span></span> | <span data-ttu-id="9e511-178">Especifica una clave pública SSH codificada en base64</span><span class="sxs-lookup"><span data-stu-id="9e511-178">Specifies a base64-encoded SSH public key</span></span>

<span data-ttu-id="9e511-179">Para ver un ejemplo, consulte [la plantilla de inicio rápido de GitHub 101-vm-sshkey ](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="9e511-179">For an example, see [the 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-the-same-key-vault-i-see-the-following-message"></a><span data-ttu-id="9e511-180">Cuando ejecuto `Update-AzureRmVmss` después de agregar más de un certificado desde el mismo almacén de claves, me aparece el mensaje siguiente:</span><span class="sxs-lookup"><span data-stu-id="9e511-180">When I run `Update-AzureRmVmss` after adding more than one certificate from the same key vault, I see the following message:</span></span>
 
><span data-ttu-id="9e511-181">Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed. (Update-AzureRmVmss: muestra secretos que contienen instancias repetidas de /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, lo que no se permite.)</span><span class="sxs-lookup"><span data-stu-id="9e511-181">Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed.</span></span>
 
<span data-ttu-id="9e511-182">Esto puede ocurrir si se intenta volver a agregar el mismo almacén en lugar de utilizar un nuevo certificado de almacén para el almacén de origen existente.</span><span class="sxs-lookup"><span data-stu-id="9e511-182">This can happen if you try to re-add the same vault instead of using a new vault certificate for the existing source vault.</span></span> <span data-ttu-id="9e511-183">El comando `Add-AzureRmVmssSecret` no funciona correctamente si agrega secretos adicionales.</span><span class="sxs-lookup"><span data-stu-id="9e511-183">The `Add-AzureRmVmssSecret` command does not work correctly if you are adding additional secrets.</span></span>
 
<span data-ttu-id="9e511-184">Para agregar más secretos desde el mismo almacén de claves, actualice la lista $vmss.properties.osProfile.secrets[0].vaultCertificates.</span><span class="sxs-lookup"><span data-stu-id="9e511-184">To add more secrets from the same key vault, update the $vmss.properties.osProfile.secrets[0].vaultCertificates list.</span></span>
 
<span data-ttu-id="9e511-185">Para la estructura de entrada esperada, consulte el articulo sobre [creación o actualización de un conjunto de escalado de máquinas virtuales](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e511-185">For the expected input structure, see [Create or update a virtual machine set](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span></span>
 
<span data-ttu-id="9e511-186">Busque el secreto en el objeto de conjunto de escalado de máquinas virtuales que se encuentra en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="9e511-186">Find the secret in the virtual machine scale set object that is in the key vault.</span></span> <span data-ttu-id="9e511-187">Luego, agregue la referencia del certificado (la dirección URL junto con el nombre del secreto) a la lista asociada con el almacén.</span><span class="sxs-lookup"><span data-stu-id="9e511-187">Then, add your certificate reference (the URL and the secret store name) to the list associated with the vault.</span></span>

> [!NOTE] 
> <span data-ttu-id="9e511-188">Actualmente no se pueden quitar certificados de las máquinas virtuales mediante la API del conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9e511-188">Currently, you cannot remove certificates from VMs by using the virtual machine scale set API.</span></span>
>

<span data-ttu-id="9e511-189">Las nuevas máquinas virtuales no tendrán el certificado antiguo.</span><span class="sxs-lookup"><span data-stu-id="9e511-189">New VMs will not have the old certificate.</span></span> <span data-ttu-id="9e511-190">Sin embargo, las máquinas virtuales que tienen el certificado y que ya se han implementado tendrán el certificado antiguo.</span><span class="sxs-lookup"><span data-stu-id="9e511-190">However, VMs that have the certificate and which are already deployed will have the old certificate.</span></span>
 
### <a name="can-i-push-certificates-to-the-virtual-machine-scale-set-without-providing-the-password-when-the-certificate-is-in-the-secret-store"></a><span data-ttu-id="9e511-191">¿Puedo insertar certificados en el conjunto de escalado de máquinas virtuales sin proporcionar la contraseña cuando el certificado está en el almacén secreto?</span><span class="sxs-lookup"><span data-stu-id="9e511-191">Can I push certificates to the virtual machine scale set without providing the password, when the certificate is in the secret store?</span></span>

<span data-ttu-id="9e511-192">No es necesario codificar las contraseñas en los scripts.</span><span class="sxs-lookup"><span data-stu-id="9e511-192">You do not need to hard-code passwords in scripts.</span></span> <span data-ttu-id="9e511-193">Puede recuperar dinámicamente las contraseñas con los permisos que usa para ejecutar el script de implementación.</span><span class="sxs-lookup"><span data-stu-id="9e511-193">You can dynamically retrieve passwords with the permissions you use to run the deployment script.</span></span> <span data-ttu-id="9e511-194">Si tiene un script que mueve un certificado del almacén de secretos al almacén de claves, el comando `get certificate` del almacén de secretos también genera la contraseña del archivo. pfx.</span><span class="sxs-lookup"><span data-stu-id="9e511-194">If you have a script that moves a certificate from the secret store key vault, the secret store `get certificate` command also outputs the password of the .pfx file.</span></span>
 
### <a name="how-does-the-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-the-sourcevault-value-when-i-have-to-specify-the-absolute-uri-for-a-certificate-by-using-the-certificateurl-property"></a><span data-ttu-id="9e511-195">¿Cómo funciona la propiedad de secretos de virtualMachineProfile.osProfile de un conjunto de escalado de máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="9e511-195">How does the Secrets property of virtualMachineProfile.osProfile for a virtual machine scale set work?</span></span> <span data-ttu-id="9e511-196">¿Por qué necesito el valor de sourceVault cuando tengo que especificar el URI absoluto para un certificado mediante la propiedad certificateUrl?</span><span class="sxs-lookup"><span data-stu-id="9e511-196">Why do I need the sourceVault value when I have to specify the absolute URI for a certificate by using the certificateUrl property?</span></span> 

<span data-ttu-id="9e511-197">Es necesario que una referencia de certificado de administración remota de Windows (WinRM) esté presente en la propiedad de secretos del perfil de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="9e511-197">A Windows Remote Management (WinRM) certificate reference must be present in the Secrets property of the OS profile.</span></span> 

<span data-ttu-id="9e511-198">El propósito de indicar el almacén de origen es aplicar directivas de lista de control de acceso (ACL) que existen en el modelo de servicio de Azure Cloud de un usuario.</span><span class="sxs-lookup"><span data-stu-id="9e511-198">The purpose of indicating the source vault is to enforce access control list (ACL) policies that exist in a user's Azure Cloud Service model.</span></span> <span data-ttu-id="9e511-199">Si el almacén de origen no está especificado, los usuarios que no tengan permisos para implementar secretos o acceder a ellos en un almacén de claves podrían hacerlo mediante un proveedor de recursos de proceso (CRP).</span><span class="sxs-lookup"><span data-stu-id="9e511-199">If the source vault isn't specified, users who do not have permissions to deploy or access secrets to a key vault would be able to through a Compute Resource Provider (CRP).</span></span> <span data-ttu-id="9e511-200">Las ACL existen incluso para recursos que no existen.</span><span class="sxs-lookup"><span data-stu-id="9e511-200">ACLs exist even for resources that do not exist.</span></span>

<span data-ttu-id="9e511-201">Si proporciona un identificador de almacén de origen incorrecto pero una dirección URL de almacén de claves válida, se informará de un error cuando sondee la operación.</span><span class="sxs-lookup"><span data-stu-id="9e511-201">If you provide an incorrect source vault ID but a valid key vault URL, an error is reported when you poll the operation.</span></span>
 
### <a name="if-i-add-secrets-to-an-existing-virtual-machine-scale-set-are-the-secrets-injected-into-existing-vms-or-only-into-new-ones"></a><span data-ttu-id="9e511-202">Si agrego secretos a un conjunto de escalado de máquinas virtuales ¿los secretos se insertan en las máquinas virtuales existentes, o solo en las nuevas?</span><span class="sxs-lookup"><span data-stu-id="9e511-202">If I add secrets to an existing virtual machine scale set, are the secrets injected into existing VMs, or only into new ones?</span></span> 

<span data-ttu-id="9e511-203">Los certificados se agregan a todas las máquinas virtuales, incluso a las ya existentes.</span><span class="sxs-lookup"><span data-stu-id="9e511-203">Certificates are added to all your VMs, even preexisting ones.</span></span> <span data-ttu-id="9e511-204">Si la propiedad upgradePolicy de la máquina virtual está establecida en **manual**, el certificado se agrega a la máquina virtual al realizar una actualización manual en ella.</span><span class="sxs-lookup"><span data-stu-id="9e511-204">If your virtual machine scale set upgradePolicy property is set to **manual**, the certificate is added to the VM when you perform a manual update on the VM.</span></span>
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a><span data-ttu-id="9e511-205">¿Dónde se ponen los certificados para las máquinas virtuales Linux?</span><span class="sxs-lookup"><span data-stu-id="9e511-205">Where do I put certificates for Linux VMs?</span></span>

<span data-ttu-id="9e511-206">Para información sobre cómo implementar certificados para las máquinas virtuales Linux, consulte [Deploy certificates to VMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) (Implementación de certificados en máquinas virtuales desde un almacén de claves administrado por el cliente).</span><span class="sxs-lookup"><span data-stu-id="9e511-206">To learn how to deploy certificates for Linux VMs, see [Deploy certificates to VMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span></span>
  
### <a name="how-do-i-add-a-new-vault-certificate-to-a-new-certificate-object"></a><span data-ttu-id="9e511-207">¿Cómo se agrega un nuevo certificado de almacén a un nuevo objeto de certificado?</span><span class="sxs-lookup"><span data-stu-id="9e511-207">How do I add a new vault certificate to a new certificate object?</span></span>

<span data-ttu-id="9e511-208">Para agregar un certificado del almacén a un secreto existente, vea el ejemplo siguiente de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9e511-208">To add a vault certificate to an existing secret, see the following PowerShell example.</span></span> <span data-ttu-id="9e511-209">Use un solo objeto secreto.</span><span class="sxs-lookup"><span data-stu-id="9e511-209">Use only one secret object.</span></span>
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-to-certificates-if-you-reimage-a-vm"></a><span data-ttu-id="9e511-210">¿Qué ocurre con los certificados si restablece la imagen inicial de una máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="9e511-210">What happens to certificates if you reimage a VM?</span></span>

<span data-ttu-id="9e511-211">Si restablece la imagen inicial de una máquina virtual, los certificados se eliminan.</span><span class="sxs-lookup"><span data-stu-id="9e511-211">If you reimage a VM, certificates are deleted.</span></span> <span data-ttu-id="9e511-212">El restablecimiento de la imagen inicial elimina todo el contenido del disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="9e511-212">Reimaging deletes the entire OS disk.</span></span> 
 
### <a name="what-happens-if-you-delete-a-certificate-from-the-key-vault"></a><span data-ttu-id="9e511-213">¿Qué ocurre si se elimina un certificado del almacén de claves?</span><span class="sxs-lookup"><span data-stu-id="9e511-213">What happens if you delete a certificate from the key vault?</span></span>

<span data-ttu-id="9e511-214">Si elimina el secreto del almacén de claves y ejecuta `stop deallocate` para todas las máquinas virtuales y luego las inicia de nuevo, se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="9e511-214">If the secret is deleted from the key vault, and then you run `stop deallocate` for all your VMs and then start them again, you will encounter a failure.</span></span> <span data-ttu-id="9e511-215">El error se produce porque el CRP necesita recuperar los secretos desde el almacén de claves, pero no puede.</span><span class="sxs-lookup"><span data-stu-id="9e511-215">The failure occurs because the CRP needs to retrieve the secrets from the key vault, but it cannot.</span></span> <span data-ttu-id="9e511-216">En este escenario, puede eliminar los certificados del conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9e511-216">In this scenario, you can delete the certificates from the virtual machine scale set model.</span></span> 

<span data-ttu-id="9e511-217">El componente de CRP no conserva los secretos de cliente.</span><span class="sxs-lookup"><span data-stu-id="9e511-217">The CRP component does not persist customer secrets.</span></span> <span data-ttu-id="9e511-218">Si ejecuta `stop deallocate` para todas las máquinas virtuales en el conjunto de escalado de máquinas virtuales, se elimina la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="9e511-218">If you run `stop deallocate` for all VMs in the virtual machine scale set, the cache is deleted.</span></span> <span data-ttu-id="9e511-219">En este escenario, los secretos se recuperan del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="9e511-219">In this scenario, secrets are retrieved from the key vault.</span></span>

<span data-ttu-id="9e511-220">Este problema no se produce en el escalado horizontal porque hay una copia en caché del secreto en Azure Service Fabric (en el modelo de inquilino único de estructura).</span><span class="sxs-lookup"><span data-stu-id="9e511-220">You don't encounter this problem when scaling out because there is a cached copy of the secret in Azure Service Fabric (in the single-fabric tenant model).</span></span>
 
### <a name="why-do-i-have-to-specify-the-exact-location-for-the-certificate-url-httpsname-of-the-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a><span data-ttu-id="9e511-221">¿Por qué tengo que especificar la ubicación exacta de la dirección URL de certificado (https://<name of the vault>.vault.azure.net:443/secrets/<exact location>), como se indica en [Escenarios de seguridad de los clústeres de Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span><span class="sxs-lookup"><span data-stu-id="9e511-221">Why do I have to specify the exact location for the certificate URL (https://<name of the vault>.vault.azure.net:443/secrets/<exact location>), as indicated in [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span></span>
 
<span data-ttu-id="9e511-222">Según la documentación de Azure Key Vault, la API de REST Get Secret debe devolver la versión más reciente del secreto si no se especifica la versión.</span><span class="sxs-lookup"><span data-stu-id="9e511-222">The Azure Key Vault documentation states that the Get Secret REST API should return the latest version of the secret if the version is not specified.</span></span>
 
<span data-ttu-id="9e511-223">Método</span><span class="sxs-lookup"><span data-stu-id="9e511-223">Method</span></span> | <span data-ttu-id="9e511-224">URL</span><span class="sxs-lookup"><span data-stu-id="9e511-224">URL</span></span>
--- | ---
<span data-ttu-id="9e511-225">GET</span><span class="sxs-lookup"><span data-stu-id="9e511-225">GET</span></span> | <span data-ttu-id="9e511-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span><span class="sxs-lookup"><span data-stu-id="9e511-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span></span>

<span data-ttu-id="9e511-227">Reemplace {*secret-name*} por el nombre y {*secret-version*} por la versión del secreto que quiere recuperar.</span><span class="sxs-lookup"><span data-stu-id="9e511-227">Replace {*secret-name*} with the name, and replace {*secret-version*} with the version of the secret you want to retrieve.</span></span> <span data-ttu-id="9e511-228">Se puede excluir la versión del secreto.</span><span class="sxs-lookup"><span data-stu-id="9e511-228">The secret version might be excluded.</span></span> <span data-ttu-id="9e511-229">En ese caso, se recupera la versión actual.</span><span class="sxs-lookup"><span data-stu-id="9e511-229">In that case, the current version is retrieved.</span></span>
  
### <a name="why-do-i-have-to-specify-the-certificate-version-when-i-use-key-vault"></a><span data-ttu-id="9e511-230">¿Por qué tengo que especificar la versión de certificado al usar Key Vault?</span><span class="sxs-lookup"><span data-stu-id="9e511-230">Why do I have to specify the certificate version when I use Key Vault?</span></span>

<span data-ttu-id="9e511-231">El propósito del requisito de Key Vault de especificar la versión del certificado es que el usuario vea claramente qué certificado se implementa en sus máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9e511-231">The purpose of the Key Vault requirement to specify the certificate version is to make it clear to the user what certificate is deployed on their VMs.</span></span>

<span data-ttu-id="9e511-232">Si crea una máquina virtual y luego actualiza el secreto en el almacén de claves, ese nuevo certificado no se descarga en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9e511-232">If you create a VM and then update your secret in the key vault, the new certificate is not downloaded to your VMs.</span></span> <span data-ttu-id="9e511-233">Pero parece que las máquinas virtuales hacen referencia a él y las nuevas máquinas virtuales obtienen el nuevo secreto.</span><span class="sxs-lookup"><span data-stu-id="9e511-233">But your VMs appear to reference it, and new VMs get the new secret.</span></span> <span data-ttu-id="9e511-234">Para evitar esta situación, se le pide la referencia de la versión de secreto.</span><span class="sxs-lookup"><span data-stu-id="9e511-234">To avoid this, you are required to reference a secret version.</span></span>

### <a name="my-team-works-with-several-certificates-that-are-distributed-to-us-as-cer-public-keys-what-is-the-recommended-approach-for-deploying-these-certificates-to-a-virtual-machine-scale-set"></a><span data-ttu-id="9e511-235">Mi equipo funciona con varios certificados que se distribuyen como claves públicas .cer.</span><span class="sxs-lookup"><span data-stu-id="9e511-235">My team works with several certificates that are distributed to us as .cer public keys.</span></span> <span data-ttu-id="9e511-236">¿Cuál es el enfoque recomendado para implementar estos certificados en un conjunto de escalado de máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="9e511-236">What is the recommended approach for deploying these certificates to a virtual machine scale set?</span></span>

<span data-ttu-id="9e511-237">Para implementar el conjunto de claves públicas .cer en un conjunto de escalado de máquinas virtuales, puede generar un archivo .pfx que contenga solo los archivos .cer.</span><span class="sxs-lookup"><span data-stu-id="9e511-237">To deploy .cer public keys to a virtual machine scale set, you can generate a .pfx file that contains only .cer files.</span></span> <span data-ttu-id="9e511-238">Para ello, use `X509ContentType = Pfx`.</span><span class="sxs-lookup"><span data-stu-id="9e511-238">To do this, use `X509ContentType = Pfx`.</span></span> <span data-ttu-id="9e511-239">Por ejemplo, cargue el archivo .cer como un objeto x509Certificate2 en C# o PowerShell y, a continuación, llame al método.</span><span class="sxs-lookup"><span data-stu-id="9e511-239">For example, load the .cer file as an x509Certificate2 object in C# or PowerShell, and then call the method.</span></span> 

<span data-ttu-id="9e511-240">Para más información, consulte [Método X509Certificate.Export (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span><span class="sxs-lookup"><span data-stu-id="9e511-240">For more information, see [X509Certificate.Export Method (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span></span>

### <a name="i-do-not-see-an-option-for-users-to-pass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a><span data-ttu-id="9e511-241">No veo una opción para que los usuarios pasen certificados como cadenas base64.</span><span class="sxs-lookup"><span data-stu-id="9e511-241">I do not see an option for users to pass in certificates as base64 strings.</span></span> <span data-ttu-id="9e511-242">La mayoría de otros proveedores de recursos tienen esta opción.</span><span class="sxs-lookup"><span data-stu-id="9e511-242">Most other resource providers have this option.</span></span>

<span data-ttu-id="9e511-243">Para emular el pase de un certificado como una cadena base64, puede extraer la última dirección URL con versiones en una plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9e511-243">To emulate passing in a certificate as a base64 string, you can extract the latest versioned URL in a Resource Manager template.</span></span> <span data-ttu-id="9e511-244">Incluya la siguiente propiedad JSON en la plantilla de Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="9e511-244">Include the following JSON property in your Resource Manager template:</span></span>

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-to-wrap-certificates-in-json-objects-in-key-vaults"></a><span data-ttu-id="9e511-245">¿Tengo que encapsular los certificados en objetos JSON en almacenes de claves?</span><span class="sxs-lookup"><span data-stu-id="9e511-245">Do I have to wrap certificates in JSON objects in key vaults?</span></span>

<span data-ttu-id="9e511-246">En los conjuntos de escalado de máquinas virtuales y las máquinas virtuales, los certificados se tienen que encapsular en objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="9e511-246">In virtual machine scale sets and VMs, certificates must be wrapped in JSON objects.</span></span> 

<span data-ttu-id="9e511-247">También se admite el tipo de contenido application/x-pkcs12.</span><span class="sxs-lookup"><span data-stu-id="9e511-247">We also support the content type application/x-pkcs12.</span></span> <span data-ttu-id="9e511-248">Para instrucciones sobre el uso de application/x-pkcs12, consulte [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/) (Certificados PFX en Azure Key Vault).</span><span class="sxs-lookup"><span data-stu-id="9e511-248">For instructions on using application/x-pkcs12, see [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span></span>
 
<span data-ttu-id="9e511-249">Actualmente no se admiten archivos .cer.</span><span class="sxs-lookup"><span data-stu-id="9e511-249">We currently do not support .cer files.</span></span> <span data-ttu-id="9e511-250">Para usar archivos .cer, expórtelos en contenedores .pfx.</span><span class="sxs-lookup"><span data-stu-id="9e511-250">To use .cer files, export them into .pfx containers.</span></span>



## <a name="compliance"></a><span data-ttu-id="9e511-251">Cumplimiento normativo</span><span class="sxs-lookup"><span data-stu-id="9e511-251">Compliance</span></span>

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a><span data-ttu-id="9e511-252">¿Son los conjuntos de escalado de máquinas virtuales compatibles con PCI?</span><span class="sxs-lookup"><span data-stu-id="9e511-252">Are virtual machine scale sets PCI-compliant?</span></span>

<span data-ttu-id="9e511-253">Los conjuntos de escalado de máquinas virtuales son una capa de API fina sobre el CRP.</span><span class="sxs-lookup"><span data-stu-id="9e511-253">Virtual machine scale sets are a thin API layer on top of the CRP.</span></span> <span data-ttu-id="9e511-254">Ambos componentes forman parte de la plataforma de proceso en el árbol de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e511-254">Both components are part of the compute platform in the Azure service tree.</span></span>

<span data-ttu-id="9e511-255">Desde la perspectiva del cumplimiento, los conjuntos de escalado de máquinas virtuales son una parte fundamental de la plataforma de proceso de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e511-255">From a compliance perspective, virtual machine scale sets are a fundamental part of the Azure compute platform.</span></span> <span data-ttu-id="9e511-256">Comparten un equipo, herramientas, procesos, metodología de implementación, controles de seguridad, compilación just-in-time (JIT), supervisión, alertas y así sucesivamente, con el CRP propio.</span><span class="sxs-lookup"><span data-stu-id="9e511-256">They share a team, tools, processes, deployment methodology, security controls, just-in-time (JIT) compilation, monitoring, alerting, and so on, with the CRP itself.</span></span> <span data-ttu-id="9e511-257">Los conjuntos de escalado de máquinas virtuales son compatibles con la Industria de tarjetas de pago (PCI) porque el CRP forma parte de la certificación de estándares de seguridad de datos de PCI (DSS) actual.</span><span class="sxs-lookup"><span data-stu-id="9e511-257">Virtual machine scale sets are Payment Card Industry (PCI)-compliant because the CRP is part of the current PCI Data Security Standard (DSS) attestation.</span></span>

<span data-ttu-id="9e511-258">Para más información, consulte el [Centro de confianza de Microsoft](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span><span class="sxs-lookup"><span data-stu-id="9e511-258">For more information, see [the Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span></span>






## <a name="extensions"></a><span data-ttu-id="9e511-259">Extensiones</span><span class="sxs-lookup"><span data-stu-id="9e511-259">Extensions</span></span>

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a><span data-ttu-id="9e511-260">¿Cómo puedo eliminar una extensión del conjunto de escalado de máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="9e511-260">How do I delete a virtual machine scale set extension?</span></span>

<span data-ttu-id="9e511-261">Para eliminar una extensión del conjunto de escalado de máquinas virtuales, utilice el siguiente ejemplo de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9e511-261">To delete a virtual machine scale set extension, use the following PowerShell example:</span></span>

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
<span data-ttu-id="9e511-262">Puede encontrar el valor extensionName en `$vmss`.</span><span class="sxs-lookup"><span data-stu-id="9e511-262">You can find the extensionName value in `$vmss`.</span></span>
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a><span data-ttu-id="9e511-263">¿Hay un ejemplo de plantilla de conjunto de escalado de máquinas virtuales que se integre con Operations Management Suite?</span><span class="sxs-lookup"><span data-stu-id="9e511-263">Is there a virtual machine scale set template example that integrates with Operations Management Suite?</span></span>

<span data-ttu-id="9e511-264">Para un ejemplo de plantilla de conjunto de escalado de máquinas virtuales que se integre con Operations Management Suite, vea el segundo ejemplo de [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric) (Implementar un clúster de Azure Service Fabric y habilitar la supervisión mediante el uso de Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="9e511-264">For a virtual machine scale set template example that integrates with Operations Management Suite, see the second example in [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span></span>
   
### <a name="extensions-seem-to-run-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-to-fail-what-can-i-do-to-fix-this"></a><span data-ttu-id="9e511-265">Parece que las extensiones se ejecutan en paralelo en los conjuntos de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9e511-265">Extensions seem to run in parallel on virtual machine scale sets.</span></span> <span data-ttu-id="9e511-266">Esto hace que una extensión de script personalizado genere un error.</span><span class="sxs-lookup"><span data-stu-id="9e511-266">This causes my custom script extension to fail.</span></span> <span data-ttu-id="9e511-267">¿Qué puedo hacer para solucionar esto?</span><span class="sxs-lookup"><span data-stu-id="9e511-267">What can I do to fix this?</span></span>

<span data-ttu-id="9e511-268">Para aprender sobre la secuenciación de extensión en conjuntos de escalado de máquinas virtuales, consulte [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/) (Secuenciación de extensión en conjuntos de escalado de máquinas virtuales de Azure).</span><span class="sxs-lookup"><span data-stu-id="9e511-268">To learn about extension sequencing in virtual machine scale sets, see [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span></span>
 
 
### <a name="how-do-i-reset-the-password-for-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="9e511-269">¿Cómo se restablece la contraseña para las máquinas virtuales en el conjunto de escalado de máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="9e511-269">How do I reset the password for VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="9e511-270">Para restablecer la contraseña para las máquinas virtuales del conjunto de escalado de máquinas virtuales, use las extensiones de acceso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9e511-270">To reset the password for VMs in your virtual machine scale set, use VM access extensions.</span></span> 

<span data-ttu-id="9e511-271">Utilice el siguiente ejemplo de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9e511-271">Use the following PowerShell example:</span></span>

```powershell
$vmssName = "myvmss"
$vmssResourceGroup = "myvmssrg"
$publicConfig = @{"UserName" = "newuser"}
$privateConfig = @{"Password" = "********"}
 
$extName = "VMAccessAgent"
$publisher = "Microsoft.Compute"
$vmss = Get-AzureRmVmss -ResourceGroupName $vmssResourceGroup -VMScaleSetName $vmssName
$vmss = Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name $extName -Publisher $publisher -Setting $publicConfig -ProtectedSetting $privateConfig -Type $extName -TypeHandlerVersion "2.0" -AutoUpgradeMinorVersion $true
Update-AzureRmVmss -ResourceGroupName $vmssResourceGroup -Name $vmssName -VirtualMachineScaleSet $vmss
```
 
 
### <a name="how-do-i-add-an-extension-to-all-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="9e511-272">¿Cómo agrego una extensión a todas las máquinas virtuales del conjunto de escalado de máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="9e511-272">How do I add an extension to all VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="9e511-273">Si la directiva de actualización se establece en **automática**, al volver a implementar la plantilla con las nuevas propiedades de extensión se actualizan todas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9e511-273">If update policy is set to **automatic**, redeploying the template with the new extension properties updates all VMs.</span></span>

<span data-ttu-id="9e511-274">Si la directiva de actualización se establece en **manual**, actualice primero la extensión y, a continuación, actualice manualmente todas las instancias en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9e511-274">If update policy is set to **manual**, first update the extension, and then manually update all instances in your VMs.</span></span>

  
### <a name="if-the-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-the-vms-not-match-the-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-the-scripts-that-are-currently-configured-on-the-virtual-machine-scale-set-executed-or-are-the-scripts-that-were-configured-when-the-vm-was-first-created-used"></a><span data-ttu-id="9e511-275">Si las extensiones asociadas con un conjunto de escalado de máquinas virtuales existente se actualizan, ¿afectará a las máquinas virtuales ya existentes?</span><span class="sxs-lookup"><span data-stu-id="9e511-275">If the extensions associated with an existing virtual machine scale set are updated, are existing VMs affected?</span></span> <span data-ttu-id="9e511-276">(Es decir, ¿*no* coincidirán las máquinas virtuales con el modelo de conjunto de escalado de máquinas virtuales?) ¿O se ignoran?</span><span class="sxs-lookup"><span data-stu-id="9e511-276">(That is, will the VMs *not* match the virtual machine scale set model?) Or are they ignored?</span></span> <span data-ttu-id="9e511-277">Cuando se recuperan los servicios de una máquina existente o se restablece su imagen inicial, ¿se ejecutarán los scripts que están configurados actualmente en el conjunto de escalado de máquinas virtuales, o se usarán los que se configuraron la primera vez que se creó la máquina?</span><span class="sxs-lookup"><span data-stu-id="9e511-277">When an existing machine is service-healed or reimaged, are the scripts that are currently configured on the virtual machine scale set executed, or are the scripts that were configured when the VM was first created used?</span></span>

<span data-ttu-id="9e511-278">Si la definición de extensión en el modelo del conjunto de escalado de máquinas virtuales se actualiza y se establece la propiedad upgradePolicy en **automática**, actualiza las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9e511-278">If the extension definition in the virtual machine scale set model is updated and the upgradePolicy property is set to **automatic**, it updates the VMs.</span></span> <span data-ttu-id="9e511-279">Si se establece la propiedad upgradePolicy en **manual**, las extensiones se marcan como que no coinciden con el modelo.</span><span class="sxs-lookup"><span data-stu-id="9e511-279">If the upgradePolicy property is set to **manual**, extensions are flagged as not matching the model.</span></span> 

<span data-ttu-id="9e511-280">Si se ha recuperado el servicio de una máquina virtual existente, aparece como un reinicio y las extensiones no se ejecutan de nuevo.</span><span class="sxs-lookup"><span data-stu-id="9e511-280">If an existing VM is service-healed, it appears as a reboot, and the extensions are not rerun.</span></span> <span data-ttu-id="9e511-281">Si se restablece su imagen inicial es como a sustituir el disco de sistema operativo con la imagen de origen.</span><span class="sxs-lookup"><span data-stu-id="9e511-281">If it is reimaged, it's like replacing the OS drive with the source image.</span></span> <span data-ttu-id="9e511-282">Cualquier especialización del modelo más reciente, como las extensiones, se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="9e511-282">Any specialization from the latest model, such as extensions, are run.</span></span>
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-to-an-azure-ad-domain"></a><span data-ttu-id="9e511-283">¿Cómo puedo unir un conjunto de escalado de máquinas virtuales a un dominio de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="9e511-283">How do I join a virtual machine scale set to an Azure AD domain?</span></span>

<span data-ttu-id="9e511-284">Para unir un conjunto de escalado de máquinas virtuales a un dominio de Azure Active Directory (Azure AD), puede definir una extensión.</span><span class="sxs-lookup"><span data-stu-id="9e511-284">To join a virtual machine scale set to an Azure Active Directory (Azure AD) domain, you can define an extension.</span></span> 

<span data-ttu-id="9e511-285">Para definir una extensión, utilice la propiedad JsonADDomainExtension:</span><span class="sxs-lookup"><span data-stu-id="9e511-285">To define an extension, use the JsonADDomainExtension property:</span></span>

```json
"extensionProfile": {
    "extensions": [
        {
            "name": "joindomain",
            "properties": {
                "publisher": "Microsoft.Compute",
                "type": "JsonADDomainExtension",
                "typeHandlerVersion": "1.3",
                "settings": {
                    "Name": "[parameters('domainName')]",
                    "OUPath": "[variables('ouPath')]",
                    "User": "[variables('domainAndUsername')]",
                    "Restart": "true",
                    "Options": "[variables('domainJoinOptions')]"
                },
                "protectedsettings": {
                    "Password": "[parameters('domainJoinPassword')]"
                }
            }
        }
    ]
}
```
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-to-install-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a><span data-ttu-id="9e511-286">Una extensión de conjunto de escalado de máquinas virtuales está intentando instalar algo que requiere un reinicio.</span><span class="sxs-lookup"><span data-stu-id="9e511-286">My virtual machine scale set extension is trying to install something that requires a reboot.</span></span> <span data-ttu-id="9e511-287">Por ejemplo, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span><span class="sxs-lookup"><span data-stu-id="9e511-287">For example, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span></span>

<span data-ttu-id="9e511-288">Si la extensión de conjunto de escalado de máquinas virtuales está intentando instalar algo que requiere un reinicio, puede usar la extensión de configuración de estado deseado de Azure Automation (DSC de Automatización).</span><span class="sxs-lookup"><span data-stu-id="9e511-288">If your virtual machine scale set extension is trying to install something that requires a reboot, you can use the Azure Automation Desired State Configuration (Automation DSC) extension.</span></span> <span data-ttu-id="9e511-289">Si el sistema operativo es Windows Server 2012 R2, Azure extrae en el programa de instalación de Windows Management Framework (WMF) 5.0, reinicia y continúa con la configuración.</span><span class="sxs-lookup"><span data-stu-id="9e511-289">If the operating system is Windows Server 2012 R2, Azure pulls in the Windows Management Framework (WMF) 5.0 setup, reboots, and then continues with the configuration.</span></span> 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a><span data-ttu-id="9e511-290">¿Cómo activo el antimalware en el conjunto de escalado de máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="9e511-290">How do I turn on antimalware in my virtual machine scale set?</span></span>

<span data-ttu-id="9e511-291">Para activar el antimalware en el conjunto de escalado de máquinas virtuales, utilice el siguiente ejemplo de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9e511-291">To turn on antimalware on your virtual machine scale set, use the following PowerShell example:</span></span>

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve the most recent version number of the extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-to-execute-a-custom-script-thats-hosted-in-a-private-storage-account-the-script-runs-successfully-when-the-storage-is-public-but-when-i-try-to-use-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a><span data-ttu-id="9e511-292">Tengo que ejecutar un script personalizado hospedado en una cuenta de almacenamiento privada.</span><span class="sxs-lookup"><span data-stu-id="9e511-292">I need to execute a custom script that's hosted in a private storage account.</span></span> <span data-ttu-id="9e511-293">El script se ejecuta correctamente cuando el almacenamiento es público, pero cuando intento usar una firma de acceso compartido (SAS), se produce un error.</span><span class="sxs-lookup"><span data-stu-id="9e511-293">The script runs successfully when the storage is public, but when I try to use a Shared Access Signature (SAS), it fails.</span></span> <span data-ttu-id="9e511-294">Se muestra este mensaje: "Faltan los parámetros obligatorios para la firma de acceso compartido".</span><span class="sxs-lookup"><span data-stu-id="9e511-294">This message is displayed: “Missing mandatory parameters for valid Shared Access Signature”.</span></span> <span data-ttu-id="9e511-295">Vínculo + SAS funciona bien desde mi explorador local.</span><span class="sxs-lookup"><span data-stu-id="9e511-295">Link+SAS works fine from my local browser.</span></span>

<span data-ttu-id="9e511-296">Para ejecutar un script personalizado que está hospedado en una cuenta de almacenamiento privado, establezca una configuración protegida con el nombre y la clave de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9e511-296">To execute a custom script that's hosted in a private storage account, set up protected settings with the storage account key and name.</span></span> <span data-ttu-id="9e511-297">Para más información, consulte la sección sobre la [Extensión del script personalizado para Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span><span class="sxs-lookup"><span data-stu-id="9e511-297">For more information, see [Custom Script Extension for Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span></span>







## <a name="networking"></a><span data-ttu-id="9e511-298">Redes</span><span class="sxs-lookup"><span data-stu-id="9e511-298">Networking</span></span>
 
### <a name="is-it-possible-to-assign-a-network-security-group-nsg-to-a-scale-set-so-that-it-will-apply-to-all-the-vm-nics-in-the-set"></a><span data-ttu-id="9e511-299">¿Es posible asignar un grupo de seguridad de red (NSG) a un conjunto de escalado, para que se aplique a todas las NIC de VM en el conjunto?</span><span class="sxs-lookup"><span data-stu-id="9e511-299">Is it possible to assign a Network Security Group (NSG) to a scale set, so that it will apply to all the VM NICs in the set?</span></span>

<span data-ttu-id="9e511-300">Sí.</span><span class="sxs-lookup"><span data-stu-id="9e511-300">Yes.</span></span> <span data-ttu-id="9e511-301">Un grupo de seguridad de red se puede aplicar directamente a un conjunto de escalado haciendo referencia a él en la sección networkInterfaceConfigurations del perfil de red.</span><span class="sxs-lookup"><span data-stu-id="9e511-301">A Network Security Group can be applied directly to a scale set by referencing it in the networkInterfaceConfigurations section of the network profile.</span></span> <span data-ttu-id="9e511-302">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9e511-302">Example:</span></span>

```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                 }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-the-same-subscription-and-same-region"></a><span data-ttu-id="9e511-303">¿Cómo hago un intercambio de VIP para conjuntos de escalado de máquinas virtuales de la misma suscripción y la misma región?</span><span class="sxs-lookup"><span data-stu-id="9e511-303">How do I do a VIP swap for virtual machine scale sets in the same subscription and same region?</span></span>

<span data-ttu-id="9e511-304">Si tiene dos conjuntos de escalado de máquinas virtuales con servidores front-end de Azure Load Balancer, y están en la misma suscripción y región, puede desasignar las direcciones IP públicas de cada uno de ellos y asignarlas al otro.</span><span class="sxs-lookup"><span data-stu-id="9e511-304">If you have two virtual machine scale sets with Azure Load Balancer front-ends, and they are in the same subscription and region, you could deallocate the public IP addresses from each one, and assign to the other.</span></span> <span data-ttu-id="9e511-305">Consulte, por ejemplo, [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) (Intercambio de VIP: implementación Blue-green en Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="9e511-305">See [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) for example.</span></span> <span data-ttu-id="9e511-306">Esto implica un retraso ya que los recursos se desasignan y asignan a nivel de red.</span><span class="sxs-lookup"><span data-stu-id="9e511-306">This does imply a delay though as the resources are deallocated/allocated at the network level.</span></span> <span data-ttu-id="9e511-307">Una opción más rápida es usar Azure Application Gateway con dos grupos de back-end y una regla de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="9e511-307">A faster option is to use Azure Application Gateway with two backend pools, and a routing rule.</span></span> <span data-ttu-id="9e511-308">También puede hospedar la aplicación con [Azure App Service](https://azure.microsoft.com/en-us/services/app-service/), que permite realizar un cambio rápido entre las ranuras de ensayo y las de producción.</span><span class="sxs-lookup"><span data-stu-id="9e511-308">Alternatively, you could host your application with [Azure App service](https://azure.microsoft.com/en-us/services/app-service/) which provides support for fast switching between staging and production slots.</span></span>
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-to-use-for-static-private-ip-address-allocation"></a><span data-ttu-id="9e511-309">¿Cómo especifico un intervalo de direcciones IP privadas para la asignación estática de direcciones IP privadas?</span><span class="sxs-lookup"><span data-stu-id="9e511-309">How do I specify a range of private IP addresses to use for static private IP address allocation?</span></span>

<span data-ttu-id="9e511-310">Las direcciones IP se seleccionan de una subred que especifique.</span><span class="sxs-lookup"><span data-stu-id="9e511-310">IP addresses are selected from a subnet that you specify.</span></span> 

<span data-ttu-id="9e511-311">El método de asignación de direcciones IP de un conjunto de escalado de máquinas virtuales siempre es "dinámico", pero eso no significa que estas direcciones IP pueden cambiar.</span><span class="sxs-lookup"><span data-stu-id="9e511-311">The allocation method of virtual machine scale set IP addresses is always “dynamic,” but that doesn't mean that these IP addresses can change.</span></span> <span data-ttu-id="9e511-312">En este caso, "dinámico" solo significa que no tiene que especificar la dirección IP en una solicitud PUT.</span><span class="sxs-lookup"><span data-stu-id="9e511-312">In this case, "dynamic" only means that you do not specify the IP address in a PUT request.</span></span> <span data-ttu-id="9e511-313">Especifique el conjunto estático mediante el uso de la subred.</span><span class="sxs-lookup"><span data-stu-id="9e511-313">Specify the static set by using the subnet.</span></span> 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-to-an-existing-azure-virtual-network"></a><span data-ttu-id="9e511-314">¿Cómo se puede implementar un conjunto de escalado de máquinas virtuales en una red virtual de Azure existente?</span><span class="sxs-lookup"><span data-stu-id="9e511-314">How do I deploy a virtual machine scale set to an existing Azure virtual network?</span></span> 

<span data-ttu-id="9e511-315">Para implementar un conjunto de escalado de máquinas virtuales en una red virtual de Azure existente, consulte el documento sobre [implementación de un conjunto de escalado de máquinas virtuales en una red virtual existente](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="9e511-315">To deploy a virtual machine scale set to an existing Azure virtual network, see [Deploy a virtual machine scale set to an existing virtual network](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span></span> 

### <a name="how-do-i-add-the-ip-address-of-the-first-vm-in-a-virtual-machine-scale-set-to-the-output-of-a-template"></a><span data-ttu-id="9e511-316">¿Cómo se agrega la dirección IP de la primera máquina virtual de un conjunto de escalado de máquinas virtuales en la salida de una plantilla?</span><span class="sxs-lookup"><span data-stu-id="9e511-316">How do I add the IP address of the first VM in a virtual machine scale set to the output of a template?</span></span>

<span data-ttu-id="9e511-317">Para agregar la dirección IP de la primera máquina virtual de un conjunto de escalado de máquinas virtuales en la salida de una plantilla, consulte [ARM - Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips) (ARM: obtención de las IP privadas de VMSS).</span><span class="sxs-lookup"><span data-stu-id="9e511-317">To add the IP address of the first VM in a virtual machine scale set to the output of a template, see [ARM: Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span></span>

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a><span data-ttu-id="9e511-318">¿Puedo usar conjuntos de escalado con redes aceleradas?</span><span class="sxs-lookup"><span data-stu-id="9e511-318">Can I use scale sets with Accelerated Networking?</span></span>

<span data-ttu-id="9e511-319">Sí.</span><span class="sxs-lookup"><span data-stu-id="9e511-319">Yes.</span></span> <span data-ttu-id="9e511-320">Para usar las redes aceleradas, establezca enableAcceleratedNetworking en true en los ajustes de networkInterfaceConfigurations de su conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="9e511-320">To use accelerated networking, set enableAcceleratedNetworking to true in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="9e511-321">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="9e511-321">E.g.</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
        "name": "niconfig1",
        "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
                ]
            }
            }
        ]
        }
    }
    ]
}
```

### <a name="how-can-i-configure-the-dns-servers-used-by-a-scale-set"></a><span data-ttu-id="9e511-322">¿Cómo puedo configurar los servidores DNS usados por un conjunto de escalado?</span><span class="sxs-lookup"><span data-stu-id="9e511-322">How can I configure the DNS servers used by a scale set?</span></span>

<span data-ttu-id="9e511-323">Para crear un conjunto de escalado de máquina virtual con una configuración de DNS personalizada, agregue un paquete JSON dnsSettings a la sección de networkInterfaceConfigurations del conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="9e511-323">To create a VM scale set with a custom DNS configuration, add a dnsSettings JSON packet to the scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="9e511-324">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9e511-324">Example:</span></span>
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-to-assign-a-public-ip-address-to-each-vm"></a><span data-ttu-id="9e511-325">¿Cómo puedo configurar conjunto de escalado para asignar una dirección IP pública a cada máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="9e511-325">How can I configure a scale set to assign a public IP address to each VM?</span></span>

<span data-ttu-id="9e511-326">Para crear un conjunto de escalado de máquina virtual que asigne una dirección IP pública a cada máquina virtual, asegúrese de que la versión de API del recurso Microsoft.Compute/virtualMAchineScaleSets es 2017-03-30 y agregue un paquete JSON _publicipaddressconfiguration_ a la sección ipConfigurations del conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="9e511-326">To create a VM scale set that assigns a public IP address to each VM, make sure the API version of the Microsoft.Compute/virtualMAchineScaleSets resource is 2017-03-30, and add a _publicipaddressconfiguration_ JSON packet to the scale set ipConfigurations section.</span></span> <span data-ttu-id="9e511-327">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9e511-327">Example:</span></span>

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-to-work-with-multiple-application-gateways"></a><span data-ttu-id="9e511-328">¿Puedo configurar un conjunto de escalado para trabajar con varias instancias de Application Gateway?</span><span class="sxs-lookup"><span data-stu-id="9e511-328">Can I configure a scale set to work with multiple Application Gateways?</span></span>

<span data-ttu-id="9e511-329">Sí.</span><span class="sxs-lookup"><span data-stu-id="9e511-329">Yes.</span></span> <span data-ttu-id="9e511-330">Puede agregar el identificador de recurso de varios grupos de direcciones back-end de Application Gateway a la lista _applicationGatewayBackendAddressPools_ de la sección _ipConfigurations_, en el perfil de red del conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="9e511-330">You can add the resource id's for multiple Application Gateway backend address pools to the _applicationGatewayBackendAddressPools_ list in the _ipConfigurations_ section of your scale set network profile.</span></span>

## <a name="scale"></a><span data-ttu-id="9e511-331">Escala</span><span class="sxs-lookup"><span data-stu-id="9e511-331">Scale</span></span>

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a><span data-ttu-id="9e511-332">¿En qué casos podría crear un conjunto de escalado de máquinas virtuales con menos de dos máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="9e511-332">In what case would I create a virtual machine scale set with fewer than two VMs?</span></span>

<span data-ttu-id="9e511-333">Una de las razones para crear un conjunto de escalado de máquinas virtuales con menos de dos máquinas virtuales sería usar las propiedades elásticas de un conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9e511-333">One reason to create a virtual machine scale set with fewer than two VMs would be to use the elastic properties of a virtual machine scale set.</span></span> <span data-ttu-id="9e511-334">Por ejemplo, podría implementar un conjunto de escalado de máquinas virtuales con cero máquinas virtuales a fin de definir su infraestructura sin pagar por los costos de ejecución de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9e511-334">For example, you could deploy a virtual machine scale set with zero VMs to define your infrastructure without paying VM running costs.</span></span> <span data-ttu-id="9e511-335">Luego, cuando esté listo para implementar máquinas virtuales, aumente la "capacidad" del conjunto de escalado de máquinas virtuales hasta el recuento de instancia de producción.</span><span class="sxs-lookup"><span data-stu-id="9e511-335">Then, when you are ready to deploy VMs, increase the “capacity” of the virtual machine scale set to the production instance count.</span></span>

<span data-ttu-id="9e511-336">Otra razón por la que podría crear un conjunto de escalado de máquinas virtuales con menos de dos máquinas virtuales es si le preocupa menos la disponibilidad que el uso de un conjunto de disponibilidad con máquinas virtuales discretas.</span><span class="sxs-lookup"><span data-stu-id="9e511-336">Another reason you might create a virtual machine scale set with fewer than two VMs is if you're concerned less with availability than in using an availability set with discrete VMs.</span></span> <span data-ttu-id="9e511-337">Los conjuntos de escalado de máquinas virtuales le proporcionan una forma de trabajar con unidades de proceso indiscriminadas que son fungibles.</span><span class="sxs-lookup"><span data-stu-id="9e511-337">Virtual machine scale sets give you a way to work with undifferentiated compute units that are fungible.</span></span> <span data-ttu-id="9e511-338">Esta uniformidad es un diferenciador clave entre los conjuntos de escalado de máquinas virtuales y los conjuntos de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="9e511-338">This uniformity is a key differentiator for virtual machine scale sets versus availability sets.</span></span> <span data-ttu-id="9e511-339">Muchas cargas de trabajo sin estado no realizan seguimiento de unidades individuales.</span><span class="sxs-lookup"><span data-stu-id="9e511-339">Many stateless workloads do not track individual units.</span></span> <span data-ttu-id="9e511-340">Si baja la carga de trabajo, puede reducir verticalmente a una unidad de proceso y escalar verticalmente a varias cuando aumente la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="9e511-340">If the workload drops, you can scale down to one compute unit, and then scale up to many when the workload increases.</span></span>

### <a name="how-do-i-change-the-number-of-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="9e511-341">¿Cómo se cambia el número de máquinas virtuales en un conjunto de escalado de máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="9e511-341">How do I change the number of VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="9e511-342">Para cambiar el número de máquinas virtuales en un conjunto de escalado de máquinas virtuales, consulte [Change the instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/) (Cambio del recuento de instancias de un conjunto de escalado de máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="9e511-342">To change the number of VMs in a virtual machine scale set, see [Change the instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span></span>

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a><span data-ttu-id="9e511-343">¿Cómo puedo definir alertas personalizadas para cuando se alcanzan determinados umbrales?</span><span class="sxs-lookup"><span data-stu-id="9e511-343">How do I define custom alerts for when certain thresholds are reached?</span></span>

<span data-ttu-id="9e511-344">Dispone de cierta flexibilidad en la manera de controlar las alertas de umbrales especificados.</span><span class="sxs-lookup"><span data-stu-id="9e511-344">You have some flexibility in how you handle alerts for specified thresholds.</span></span> <span data-ttu-id="9e511-345">Por ejemplo, puede definir webhooks personalizados.</span><span class="sxs-lookup"><span data-stu-id="9e511-345">For example, you can define customized webhooks.</span></span> <span data-ttu-id="9e511-346">El ejemplo del siguiente webhook procede de una plantilla de Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="9e511-346">The following webhook example is from a Resource Manager template:</span></span>

```json
{
    "type": "Microsoft.Insights/autoscaleSettings",
    "apiVersion": "[variables('insightsApi')]",
    "name": "autoscale",
    "location": "[parameters('resourceLocation')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
    ],
    "properties": {
        "name": "autoscale",
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/',  resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
        "enabled": true,
        "notifications": [
            {
                "operation": "Scale",
                "email": {
                    "sendToSubscriptionAdministrator": true,
                    "sendToSubscriptionCoAdministrators": true,
                    "customEmails": [
                        "youremail@address.com"
                    ]
                },
                "webhooks": [
                    {
                        "serviceUri": "https://events.pagerduty.com/integration/0b75b57246814149b4d87fa6e1273687/enqueue",
                        "properties": {
                            "key1": "custommetric",
                            "key2": "scalevmss"
                        }
                    }
                ]
            }
        ],
```

<span data-ttu-id="9e511-347">En este ejemplo, una alerta va a Pagerduty.com cuando se alcanza un umbral.</span><span class="sxs-lookup"><span data-stu-id="9e511-347">In this example, an alert goes to Pagerduty.com when a threshold is reached.</span></span>



## <a name="patching-and-operations"></a><span data-ttu-id="9e511-348">Aplicación de revisiones y operaciones</span><span class="sxs-lookup"><span data-stu-id="9e511-348">Patching and operations</span></span>

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a><span data-ttu-id="9e511-349">¿Cómo creo un conjunto de escalado en un grupo de recursos existente?</span><span class="sxs-lookup"><span data-stu-id="9e511-349">How do I create a scale set in an existing resource group?</span></span>

<span data-ttu-id="9e511-350">Todavía no es posible crear conjuntos de escalado en un grupo de recursos existente desde Azure Portal, pero puede especificar un grupo de recursos existente al implementar un conjunto de escalado desde una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9e511-350">Creating scale sets in an existing resource group is not yet possible from the Azure portal, but you can specify an existing resource group when deploying a scale set from an Azure Resource Manager template.</span></span> <span data-ttu-id="9e511-351">También puede especificar un grupo de recursos existente al crear un conjunto de escalado con Azure PowerShell o CLI.</span><span class="sxs-lookup"><span data-stu-id="9e511-351">You can also specify an existing resource group when creating a scale set using Azure PowerShell or CLI.</span></span>

### <a name="can-we-move-a-scale-set-to-another-resource-group"></a><span data-ttu-id="9e511-352">¿Podemos mover un conjunto de escalado a otro grupo de recursos?</span><span class="sxs-lookup"><span data-stu-id="9e511-352">Can we move a scale set to another resource group?</span></span>

<span data-ttu-id="9e511-353">Sí, se pueden mover recursos del conjunto de escalado a una nueva suscripción o a un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9e511-353">Yes, you can move scale set resources to a new subscription or resource group.</span></span>

### <a name="how-to-i-update-my-virtual-machine-scale-set-to-a-new-image-how-do-i-manage-patching"></a><span data-ttu-id="9e511-354">¿Cómo actualizo mi conjunto de escalado de máquinas virtuales a una nueva imagen?</span><span class="sxs-lookup"><span data-stu-id="9e511-354">How to I update my virtual machine scale set to a new image?</span></span> <span data-ttu-id="9e511-355">¿Cómo administro la aplicación de revisiones?</span><span class="sxs-lookup"><span data-stu-id="9e511-355">How do I manage patching?</span></span>

<span data-ttu-id="9e511-356">Para actualizar su conjunto de escalado de máquinas virtuales con una nueva imagen y para administrar la aplicación de revisiones consulte [Actualización de un conjunto de escalado de máquinas virtuales](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span><span class="sxs-lookup"><span data-stu-id="9e511-356">To update your virtual machine scale set to a new image, and to manage patching, see [Upgrade a virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span></span>

### <a name="can-i-use-the-reimage-operation-to-reset-a-vm-without-changing-the-image-that-is-i-want-reset-a-vm-to-factory-settings-rather-than-to-a-new-image"></a><span data-ttu-id="9e511-357">¿Puedo usar la operación de restablecimiento de la imagen inicial para restablecer una máquina virtual sin cambiar la imagen?</span><span class="sxs-lookup"><span data-stu-id="9e511-357">Can I use the reimage operation to reset a VM without changing the image?</span></span> <span data-ttu-id="9e511-358">(Es decir, quiero restablecer una máquina virtual a la configuración de fábrica en lugar de a una nueva imagen).</span><span class="sxs-lookup"><span data-stu-id="9e511-358">(That is, I want reset a VM to factory settings rather than to a new image.)</span></span>

<span data-ttu-id="9e511-359">Sí, puede usar la operación de restablecimiento de la imagen inicial para restablecer una máquina virtual sin cambiar la imagen.</span><span class="sxs-lookup"><span data-stu-id="9e511-359">Yes, you can use the reimage operation to reset a VM without changing the image.</span></span> <span data-ttu-id="9e511-360">Sin embargo, si el conjunto de escalado de máquinas virtuales hace referencia a una imagen de plataforma con `version = latest`, la máquina virtual se puede actualizar a una imagen del SO posterior cuando llame a `reimage`.</span><span class="sxs-lookup"><span data-stu-id="9e511-360">However, if your virtual machine scale set references a platform image with `version = latest`, your VM can update to a later OS image when you call `reimage`.</span></span>

<span data-ttu-id="9e511-361">Para más información, consulte el artículo sobre la [administración de todas las máquinas virtuales de un conjunto de escalado de máquinas virtuales](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span><span class="sxs-lookup"><span data-stu-id="9e511-361">For more information, see [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="9e511-362">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="9e511-362">Troubleshooting</span></span>

### <a name="how-do-i-turn-on-boot-diagnostics"></a><span data-ttu-id="9e511-363">¿Cómo se activa el diagnóstico de arranque?</span><span class="sxs-lookup"><span data-stu-id="9e511-363">How do I turn on boot diagnostics?</span></span>

<span data-ttu-id="9e511-364">Para activar el diagnóstico de arranque, en primer lugar, cree una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9e511-364">To turn on boot diagnostics, first, create a storage account.</span></span> <span data-ttu-id="9e511-365">Luego coloque este bloque JSON en el elemento **virtualMachineProfile** del conjunto de escalado de máquinas virtuales y actualice el conjunto:</span><span class="sxs-lookup"><span data-stu-id="9e511-365">Then, put this JSON block in your virtual machine scale set **virtualMachineProfile**, and update the virtual machine scale set:</span></span>

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

<span data-ttu-id="9e511-366">Cuando se crea una nueva máquina virtual, el elemento InstanceView de la máquina virtual, muestran los detalles de la captura de pantalla, etc.</span><span class="sxs-lookup"><span data-stu-id="9e511-366">When a new VM is created, the InstanceView property of the VM shows the details for the screenshot, and so on.</span></span> <span data-ttu-id="9e511-367">Este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9e511-367">Here's an example:</span></span>
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a><span data-ttu-id="9e511-368">Propiedades de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9e511-368">Virtual machine properties</span></span>

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-the-fault-domain-for-each-of-the-100-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="9e511-369">¿Cómo obtengo información de propiedades de cada máquina virtual sin tener que realizar varias llamadas?</span><span class="sxs-lookup"><span data-stu-id="9e511-369">How do I get property information for each VM without making multiple calls?</span></span> <span data-ttu-id="9e511-370">Por ejemplo, ¿cómo obtendría el dominio de error para cada una de las 100 máquinas virtuales del conjunto de escalado de máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="9e511-370">For example, how would I get the fault domain for each of the 100 VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="9e511-371">Para informarse sobre propiedad de cada máquina virtual sin realizar varias llamadas, puede llamar a `ListVMInstanceViews` realizando un `GET` de API de REST en el siguiente URI de recurso:</span><span class="sxs-lookup"><span data-stu-id="9e511-371">To get property information for each VM without making multiple calls, you can call `ListVMInstanceViews` by doing a REST API `GET` on the following resource URI:</span></span>

<span data-ttu-id="9e511-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span><span class="sxs-lookup"><span data-stu-id="9e511-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span></span>

### <a name="can-i-pass-different-extension-arguments-to-different-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="9e511-373">¿Puedo pasar diferentes argumentos de extensión a diferentes máquinas virtuales de un conjunto de escalado de máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="9e511-373">Can I pass different extension arguments to different VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="9e511-374">No, no puede pasar diferentes argumentos de extensión a diferentes máquinas virtuales de un conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9e511-374">No, you cannot pass different extension arguments to different VMs in a virtual machine scale set.</span></span> <span data-ttu-id="9e511-375">De todas formas, las extensiones pueden actuar en función de propiedades únicas de la máquina virtual en la que se ejecutan, como el nombre de la máquina.</span><span class="sxs-lookup"><span data-stu-id="9e511-375">However, extensions can act based on the unique properties of the VM they are running on, such as on the machine name.</span></span> <span data-ttu-id="9e511-376">Además, las extensiones pueden consultar metadatos de instancias en http://169.254.169.254 para más información sobre la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9e511-376">Extensions also can query instance metadata on http://169.254.169.254 to get more information about the VM.</span></span>

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a><span data-ttu-id="9e511-377">¿Por qué hay huecos entre los nombres de máquina virtual de mi conjunto de escalado de máquinas virtuales y los identificadores de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="9e511-377">Why are there gaps between my virtual machine scale set VM machine names and VM IDs?</span></span> <span data-ttu-id="9e511-378">Por ejemplo: 0, 1, 3...</span><span class="sxs-lookup"><span data-stu-id="9e511-378">For example: 0, 1, 3...</span></span>

<span data-ttu-id="9e511-379">Hay huecos entre los nombres de máquina virtual del conjunto de escalado de máquinas virtuales y el identificador de la máquina virtual porque la propiedad **overprovision** del conjunto de escalado de máquinas virtuales está establecida en el valor predeterminado de **true**.</span><span class="sxs-lookup"><span data-stu-id="9e511-379">There are gaps between your virtual machine scale set VM machine names and VM IDs because your virtual machine scale set **overprovision** property is set to the default value of **true**.</span></span> <span data-ttu-id="9e511-380">Si la propiedad overprovision se establece en **true**, se crean más máquinas de las solicitadas.</span><span class="sxs-lookup"><span data-stu-id="9e511-380">If overprovisioning is set to **true**, more VMs than requested are created.</span></span> <span data-ttu-id="9e511-381">Las máquinas virtuales adicionales se eliminan a continuación.</span><span class="sxs-lookup"><span data-stu-id="9e511-381">Extra VMs are then deleted.</span></span> <span data-ttu-id="9e511-382">En este caso, lo que consigue es una mayor confiabilidad en la implementación a cambio de reglas de traducción de direcciones de red (NAT) contiguas y de nomenclatura contiguas.</span><span class="sxs-lookup"><span data-stu-id="9e511-382">In this case, you gain increased deployment reliability, but at the expense of contiguous naming and contiguous Network Address Translation (NAT) rules.</span></span> 

<span data-ttu-id="9e511-383">Puede establecer esta propiedad en **false**.</span><span class="sxs-lookup"><span data-stu-id="9e511-383">You can set this property to **false**.</span></span> <span data-ttu-id="9e511-384">Para conjuntos de escalado de máquinas virtuales pequeños, esto no afecta significativamente a confiabilidad de la implementación.</span><span class="sxs-lookup"><span data-stu-id="9e511-384">For small virtual machine scale sets, this doesn't significantly affect deployment reliability.</span></span>

### <a name="what-is-the-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-the-vm-when-should-i-choose-one-over-the-other"></a><span data-ttu-id="9e511-385">¿Cuál es la diferencia entre eliminar una máquina virtual de un conjunto de escalado y desasignar la máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="9e511-385">What is the difference between deleting a VM in a virtual machine scale set and deallocating the VM?</span></span> <span data-ttu-id="9e511-386">¿Cuándo debo elegir una u otra opción?</span><span class="sxs-lookup"><span data-stu-id="9e511-386">When should I choose one over the other?</span></span>

<span data-ttu-id="9e511-387">La principal diferencia entre eliminar una máquina virtual en un conjunto de escalado de máquinas virtuales y cancelar la asignación de la máquina virtual es que `deallocate` no elimina los discos duros virtuales (VHD).</span><span class="sxs-lookup"><span data-stu-id="9e511-387">The main difference between deleting a VM in a virtual machine scale set and deallocating the VM is that `deallocate` doesn’t delete the virtual hard disks (VHDs).</span></span> <span data-ttu-id="9e511-388">Hay costos de almacenamiento asociados con la ejecución de `stop deallocate`.</span><span class="sxs-lookup"><span data-stu-id="9e511-388">There are storage costs associated with running `stop deallocate`.</span></span> <span data-ttu-id="9e511-389">Puede usar uno de los dos por una de las siguientes razones:</span><span class="sxs-lookup"><span data-stu-id="9e511-389">You might use one or the other for one of the following reasons:</span></span>

- <span data-ttu-id="9e511-390">Quiere dejar de pagar por los costos de proceso pero mantener el estado del disco de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9e511-390">You want to stop paying compute costs, but you want to keep the disk state of the VMs.</span></span>
- <span data-ttu-id="9e511-391">Quiere iniciar un conjunto de máquinas virtuales más rápidamente de lo que puede escalar horizontalmente un conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9e511-391">You want to start a set of VMs more quickly than you could scale out a virtual machine scale set.</span></span>
  - <span data-ttu-id="9e511-392">Relacionado con este escenario, puede haber creado su propio motor de escalado automático y quiere un escalado completo más rápido.</span><span class="sxs-lookup"><span data-stu-id="9e511-392">Related to this scenario, you might have created your own autoscale engine and want a faster end-to-end scale.</span></span>
- <span data-ttu-id="9e511-393">Tiene un conjunto de escalado de máquinas virtuales que se distribuye de forma irregular a través de dominios de error o dominios de actualización.</span><span class="sxs-lookup"><span data-stu-id="9e511-393">You have a virtual machine scale set that is unevenly distributed across fault domains or update domains.</span></span> <span data-ttu-id="9e511-394">Esto puede ser porque eliminó de forma selectiva las máquinas virtuales, o porque se eliminaron las máquinas virtuales después proveer en exceso.</span><span class="sxs-lookup"><span data-stu-id="9e511-394">This might be because you selectively deleted VMs, or because VMs were deleted after overprovisioning.</span></span> <span data-ttu-id="9e511-395">Ejecutar `stop deallocate` seguido de `start` en el conjunto de escalado de máquinas virtuales distribuye de manera uniforme las máquinas virtuales a través de dominios de error o dominios de actualización.</span><span class="sxs-lookup"><span data-stu-id="9e511-395">Running `stop deallocate` followed by `start` on the virtual machine scale set evenly distributes the VMs across fault domains or update domains.</span></span>

