---
title: "escala de máquinas virtuales de aaaAzure establece preguntas más frecuentes | Documentos de Microsoft"
description: "Obtener toofrequently respuestas preguntas más frecuentes sobre conjuntos de escalas de máquina virtual."
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
ms.openlocfilehash: 0deb9e2bb79f87f17bbf748397b94dc53070cfbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a><span data-ttu-id="c45a1-103">Preguntas frecuentes sobre los conjuntos de escalado de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="c45a1-103">Azure virtual machine scale sets FAQs</span></span>

<span data-ttu-id="c45a1-104">Obtenga respuestas toofrequently preguntas más frecuentes sobre la escala de la máquina virtual se establece en Azure.</span><span class="sxs-lookup"><span data-stu-id="c45a1-104">Get answers toofrequently asked questions about virtual machine scale sets in Azure.</span></span>

## <a name="autoscale"></a><span data-ttu-id="c45a1-105">Autoscale</span><span class="sxs-lookup"><span data-stu-id="c45a1-105">Autoscale</span></span>

### <a name="what-are-best-practices-for-azure-autoscale"></a><span data-ttu-id="c45a1-106">¿Cuáles son los procedimientos recomendados para el escalado automático de Azure?</span><span class="sxs-lookup"><span data-stu-id="c45a1-106">What are best practices for Azure Autoscale?</span></span>

<span data-ttu-id="c45a1-107">Para procedimientos recomendados para el escalado automático, consulte [Procedimientos recomendados de escalado automático en elementos virtuales](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span><span class="sxs-lookup"><span data-stu-id="c45a1-107">For best practices for Autoscale, see [Best practices for autoscaling virtual machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span></span>

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a><span data-ttu-id="c45a1-108">¿Dónde puedo encontrar los nombres de métricas para un escalado automático que use métricas basadas en host?</span><span class="sxs-lookup"><span data-stu-id="c45a1-108">Where do I find metric names for autoscaling that uses host-based metrics?</span></span>

<span data-ttu-id="c45a1-109">Para nombres de métrica para un escalado automático que use métricas basadas en host, consulte [Métricas compatibles con Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span><span class="sxs-lookup"><span data-stu-id="c45a1-109">For metric names for autoscaling that uses host-based metrics, see [Supported metrics with Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span></span>

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a><span data-ttu-id="c45a1-110">¿Hay algún ejemplo de escalado automático basado en una longitud de cola y un tema de Azure Service Bus?</span><span class="sxs-lookup"><span data-stu-id="c45a1-110">Are there any examples of autoscaling based on an Azure Service Bus topic and queue length?</span></span>

<span data-ttu-id="c45a1-111">Sí.</span><span class="sxs-lookup"><span data-stu-id="c45a1-111">Yes.</span></span> <span data-ttu-id="c45a1-112">Para ejemplos de escalado automático basados en un tema de Service Bus y una longitud de cola, consulte [Métricas comunes de escalado automático de Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span><span class="sxs-lookup"><span data-stu-id="c45a1-112">For examples of autoscaling based on an Azure Service Bus topic and queue length, see [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span></span>

<span data-ttu-id="c45a1-113">Para una cola de Bus de servicio, utilice Hola después JSON:</span><span class="sxs-lookup"><span data-stu-id="c45a1-113">For a Service Bus queue, use hello following JSON:</span></span>

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

<span data-ttu-id="c45a1-114">Para una cola de almacenamiento, utilice Hola después JSON:</span><span class="sxs-lookup"><span data-stu-id="c45a1-114">For a storage queue, use hello following JSON:</span></span>

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

<span data-ttu-id="c45a1-115">Reemplace los valores de ejemplo con los identificadores uniformes de recursos (URI) del recurso.</span><span class="sxs-lookup"><span data-stu-id="c45a1-115">Replace example values with your resource Uniform Resource Identifiers (URIs).</span></span>


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a><span data-ttu-id="c45a1-116">¿Debo realizar el escalado automático usando métricas basadas en host o usar una extensión de diagnóstico?</span><span class="sxs-lookup"><span data-stu-id="c45a1-116">Should I autoscale by using host-based metrics or a diagnostics extension?</span></span>

<span data-ttu-id="c45a1-117">Puede crear una configuración de escalado automático en una métricas de nivel de host de máquina virtual toouse o las métricas de basado en el sistema operativo invitado.</span><span class="sxs-lookup"><span data-stu-id="c45a1-117">You can create an autoscale setting on a VM toouse host-level metrics or guest OS-based metrics.</span></span>

<span data-ttu-id="c45a1-118">Para obtener una lista de métricas admitidas, consulte [Métricas comunes de escalado automático de Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span><span class="sxs-lookup"><span data-stu-id="c45a1-118">For a list of supported metrics, see [Azure Monitor autoscaling common metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span></span> 

<span data-ttu-id="c45a1-119">Para obtener un ejemplo completo para conjuntos de escalado de máquinas virtuales, consulte [Configuración avanzada de escalado automático con plantillas de Resource Manager para conjuntos de escalado de máquinas virtuales](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span><span class="sxs-lookup"><span data-stu-id="c45a1-119">For a full sample for virtual machine scale sets, see [Advanced autoscale configuration by using Resource Manager templates for virtual machine scale sets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span></span> 

<span data-ttu-id="c45a1-120">ejemplo de Hola usa métrica de CPU de nivel de host de hello y una métrica de recuento de mensajes.</span><span class="sxs-lookup"><span data-stu-id="c45a1-120">hello sample uses hello host-level CPU metric and a message count metric.</span></span>



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a><span data-ttu-id="c45a1-121">¿Cómo se configuran las reglas de alerta en un conjunto de escalado de máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="c45a1-121">How do I set alert rules on a virtual machine scale set?</span></span>

<span data-ttu-id="c45a1-122">Puede crear alertas en las métricas de los conjuntos de escalado de máquinas virtuales a través de PowerShell o CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="c45a1-122">You can create alerts on metrics for virtual machine scale sets via PowerShell or Azure CLI.</span></span> <span data-ttu-id="c45a1-123">Para más información, consulte [Ejemplos de inicio rápido de PowerShell de Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) y [Ejemplos de inicio rápido de CLI multiplataforma de Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span><span class="sxs-lookup"><span data-stu-id="c45a1-123">For more information, see [Azure Monitor PowerShell quick start samples](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) and [Azure Monitor cross-platform CLI quick start samples](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span></span>

<span data-ttu-id="c45a1-124">Hola elemento TargetResourceId del conjunto de escalas de máquina virtual de hello tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="c45a1-124">hello TargetResourceId of hello virtual machine scale set looks like this:</span></span> 

<span data-ttu-id="c45a1-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span><span class="sxs-lookup"><span data-stu-id="c45a1-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span></span>

<span data-ttu-id="c45a1-126">Puede elegir cualquier contador de rendimiento de la máquina virtual como Hola métrica tooset una alerta para.</span><span class="sxs-lookup"><span data-stu-id="c45a1-126">You can choose any VM performance counter as hello metric tooset an alert for.</span></span> <span data-ttu-id="c45a1-127">Para obtener más información, consulte [métricas de SO invitado para máquinas virtuales de Windows basada en el Administrador de recursos](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) y [métricas de SO invitado para máquinas virtuales Linux](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) en hello [métricas comunes de escalado automático de Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)artículo.</span><span class="sxs-lookup"><span data-stu-id="c45a1-127">For more information, see [Guest OS metrics for Resource Manager-based Windows VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) and [Guest OS metrics for Linux VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in hello [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/) article.</span></span>

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a><span data-ttu-id="c45a1-128">¿Cómo se configura el escalado automático en un conjunto de escalado de máquinas virtuales utilizando PowerShell?</span><span class="sxs-lookup"><span data-stu-id="c45a1-128">How do I set up autoscale on a virtual machine scale set by using PowerShell?</span></span>

<span data-ttu-id="c45a1-129">tooset de escalado automático en una escala de máquinas virtuales que se establece mediante el uso de PowerShell, consulte la entrada de blog hello [cómo establece tooadd escalado automático tooan escala de la máquina virtual de Azure](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="c45a1-129">tooset up autoscale on a virtual machine scale set by using PowerShell, see hello blog post [How tooadd autoscale tooan Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span></span>




## <a name="certificates"></a><span data-ttu-id="c45a1-130">Certificados</span><span class="sxs-lookup"><span data-stu-id="c45a1-130">Certificates</span></span>

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a><span data-ttu-id="c45a1-131">¿Cómo distribuir forma segura un toohello certificado VM?</span><span class="sxs-lookup"><span data-stu-id="c45a1-131">How do I securely ship a certificate toohello VM?</span></span> <span data-ttu-id="c45a1-132">¿Cómo se puede aprovisionar un toorun de conjunto de escala un sitio Web donde hello SSL para el sitio Web de Hola se envía con seguridad de una configuración de certificado de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="c45a1-132">How do I provision a virtual machine scale set toorun a website where hello SSL for hello website is shipped securely from a certificate configuration?</span></span> <span data-ttu-id="c45a1-133">(operación de rotación de certificado común de hello podría ser casi Hola igual que una operación de actualización de configuración.) ¿Tiene un ejemplo de cómo toodo esto?</span><span class="sxs-lookup"><span data-stu-id="c45a1-133">(hello common certificate rotation operation would be almost hello same as a configuration update operation.) Do you have an example of how toodo this?</span></span> 

<span data-ttu-id="c45a1-134">toosecurely enviar un toohello certificado VM, puede instalar un certificado de cliente directamente en un almacén de certificados de Windows desde el almacén de claves del cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-134">toosecurely ship a certificate toohello VM, you can install a customer certificate directly into a Windows certificate store from hello customer's key vault.</span></span>

<span data-ttu-id="c45a1-135">Usar hello después JSON:</span><span class="sxs-lookup"><span data-stu-id="c45a1-135">Use hello following JSON:</span></span>

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

<span data-ttu-id="c45a1-136">código de Hello es compatible con Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="c45a1-136">hello code supports Windows and Linux.</span></span>

<span data-ttu-id="c45a1-137">Para más información, consulte el artículo sobre la [creación o actualización de un conjunto de escalado de máquinas virtuales](https://msdn.microsoft.com/library/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="c45a1-137">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx).</span></span>


### <a name="example-of-self-signed-certificate"></a><span data-ttu-id="c45a1-138">Ejemplo de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="c45a1-138">Example of Self-signed certificate</span></span>

1.  <span data-ttu-id="c45a1-139">Creación de un certificado autofirmado en un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="c45a1-139">Create a self-signed certificate in a key vault.</span></span>

    <span data-ttu-id="c45a1-140">Usar hello siga los comandos de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c45a1-140">Use hello following PowerShell commands:</span></span>

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    <span data-ttu-id="c45a1-141">Esto deja de comando Hola entrada para la plantilla de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c45a1-141">This command gives you hello input for hello Azure Resource Manager template.</span></span>

    <span data-ttu-id="c45a1-142">Para obtener un ejemplo de cómo toocreate un certificado autofirmado en un almacén de claves, consulte [escenarios de seguridad de clúster de Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span><span class="sxs-lookup"><span data-stu-id="c45a1-142">For an example of how toocreate a self-signed certificate in a key vault, see [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span></span>

2.  <span data-ttu-id="c45a1-143">Cambiar la plantilla de administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-143">Change hello Resource Manager template.</span></span>

    <span data-ttu-id="c45a1-144">Agregar esta propiedad también**virtualMachineProfile**, como parte del programa Hola recurso de conjunto de escalas de máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="c45a1-144">Add this property too**virtualMachineProfile**, as part of hello virtual machine scale set resource:</span></span>

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
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a><span data-ttu-id="c45a1-145">¿Se puede especificar un toouse de par de claves de SSH para la autenticación de SSH con una escala de máquinas virtuales de Linux establecer a partir de una plantilla de administrador de recursos?</span><span class="sxs-lookup"><span data-stu-id="c45a1-145">Can I specify an SSH key pair toouse for SSH authentication with a Linux virtual machine scale set from a Resource Manager template?</span></span>  

<span data-ttu-id="c45a1-146">Sí.</span><span class="sxs-lookup"><span data-stu-id="c45a1-146">Yes.</span></span> <span data-ttu-id="c45a1-147">Hola API de REST para **osProfile** es similar toohello API de REST de la máquina virtual estándar.</span><span class="sxs-lookup"><span data-stu-id="c45a1-147">hello REST API for **osProfile** is similar toohello standard VM REST API.</span></span> 

<span data-ttu-id="c45a1-148">Incluya **osProfile** en la plantilla:</span><span class="sxs-lookup"><span data-stu-id="c45a1-148">Include **osProfile** in your template:</span></span>

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
 
<span data-ttu-id="c45a1-149">Este bloque JSON se usa en [plantilla de inicio rápido de hello 101-vm-sshkey GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="c45a1-149">This JSON block is used in [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>
 
<span data-ttu-id="c45a1-150">Hola perfil de sistema operativo también se utiliza en [grelayhost.json Hola rápida de GitHub iniciar plantilla](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span><span class="sxs-lookup"><span data-stu-id="c45a1-150">hello OS profile also is used in [hello grelayhost.json GitHub quick start template](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span></span>

<span data-ttu-id="c45a1-151">Para más información, consulte el artículo sobre la [creación o actualización de un conjunto de escalado de máquinas virtuales](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span><span class="sxs-lookup"><span data-stu-id="c45a1-151">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span></span>
  

### <a name="how-do-i-remove-deprecated-certificates"></a><span data-ttu-id="c45a1-152">¿Cómo se quitan los certificados en desuso?</span><span class="sxs-lookup"><span data-stu-id="c45a1-152">How do I remove deprecated certificates?</span></span> 

<span data-ttu-id="c45a1-153">tooremove en desuso certificados, quitar Hola certificado antiguo de la lista de certificados del almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-153">tooremove deprecated certificates, remove hello old certificate from hello vault certificates list.</span></span> <span data-ttu-id="c45a1-154">Dejar todos los certificados de Hola que desee tooremain en el equipo en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-154">Leave all hello certificates that you want tooremain on your computer in hello list.</span></span> <span data-ttu-id="c45a1-155">No se quitará el certificado de Hola de todas las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c45a1-155">This does not remove hello certificate from all your VMs.</span></span> <span data-ttu-id="c45a1-156">No agrega Hola certificado toonew las máquinas virtuales que se crean en el conjunto de escalas de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-156">It also does not add hello certificate toonew VMs that are created in hello virtual machine scale set.</span></span> 

<span data-ttu-id="c45a1-157">certificado de hello tooremove de máquinas virtuales existentes, escribir un script personalizado extensión toomanually quitar Hola certificados desde el almacén de certificados.</span><span class="sxs-lookup"><span data-stu-id="c45a1-157">tooremove hello certificate from existing VMs, write a custom script extension toomanually remove hello certificates from your certificate store.</span></span>
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a><span data-ttu-id="c45a1-158">¿Cómo insertar una clave pública SSH existente en hello máquina virtual escala conjunto SSH capa durante el aprovisionamiento?</span><span class="sxs-lookup"><span data-stu-id="c45a1-158">How do I inject an existing SSH public key into hello virtual machine scale set SSH layer during provisioning?</span></span> <span data-ttu-id="c45a1-159">Desea toostore Hola SSH valores de clave pública en el almacén de claves de Azure y utilizarlas en mi plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="c45a1-159">I want toostore hello SSH public key values in Azure Key Vault, and then use them in my Resource Manager template.</span></span>

<span data-ttu-id="c45a1-160">Si va a proporcionar Hola máquinas virtuales solo con una clave SSH pública, no es necesario tooput hello las claves públicas en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="c45a1-160">If you are providing hello VMs only with a public SSH key, you don't need tooput hello public keys in Key Vault.</span></span> <span data-ttu-id="c45a1-161">Las claves públicas no son secretas.</span><span class="sxs-lookup"><span data-stu-id="c45a1-161">Public keys are not secret.</span></span>
 
<span data-ttu-id="c45a1-162">Puede proporcionar claves públicas SSH en texto sin formato al crear una máquina virtual Linux:</span><span class="sxs-lookup"><span data-stu-id="c45a1-162">You can provide SSH public keys in plain text when you create a Linux VM:</span></span>

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
 
<span data-ttu-id="c45a1-163">Nombre del elemento de linuxConfiguration</span><span class="sxs-lookup"><span data-stu-id="c45a1-163">linuxConfiguration element name</span></span> | <span data-ttu-id="c45a1-164">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="c45a1-164">Required</span></span> | <span data-ttu-id="c45a1-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="c45a1-165">Type</span></span> | <span data-ttu-id="c45a1-166">Descripción</span><span class="sxs-lookup"><span data-stu-id="c45a1-166">Description</span></span>
--- | --- | --- | --- |  ---
<span data-ttu-id="c45a1-167">ssh</span><span class="sxs-lookup"><span data-stu-id="c45a1-167">ssh</span></span> | <span data-ttu-id="c45a1-168">No</span><span class="sxs-lookup"><span data-stu-id="c45a1-168">No</span></span> | <span data-ttu-id="c45a1-169">Colección</span><span class="sxs-lookup"><span data-stu-id="c45a1-169">Collection</span></span> | <span data-ttu-id="c45a1-170">Especifica la configuración de la clave SSH Hola para un sistema operativo Linux</span><span class="sxs-lookup"><span data-stu-id="c45a1-170">Specifies hello SSH key configuration for a Linux OS</span></span>
<span data-ttu-id="c45a1-171">path</span><span class="sxs-lookup"><span data-stu-id="c45a1-171">path</span></span> | <span data-ttu-id="c45a1-172">Sí</span><span class="sxs-lookup"><span data-stu-id="c45a1-172">Yes</span></span> | <span data-ttu-id="c45a1-173">String</span><span class="sxs-lookup"><span data-stu-id="c45a1-173">String</span></span> | <span data-ttu-id="c45a1-174">Especifica la ruta del archivo de Linux de Hola donde las claves SSH de Hola o certificado debe estar ubicado</span><span class="sxs-lookup"><span data-stu-id="c45a1-174">Specifies hello Linux file path where hello SSH keys or certificate should be located</span></span>
<span data-ttu-id="c45a1-175">keyData</span><span class="sxs-lookup"><span data-stu-id="c45a1-175">keyData</span></span> | <span data-ttu-id="c45a1-176">Sí</span><span class="sxs-lookup"><span data-stu-id="c45a1-176">Yes</span></span> | <span data-ttu-id="c45a1-177">string</span><span class="sxs-lookup"><span data-stu-id="c45a1-177">String</span></span> | <span data-ttu-id="c45a1-178">Especifica una clave pública SSH codificada en base64</span><span class="sxs-lookup"><span data-stu-id="c45a1-178">Specifies a base64-encoded SSH public key</span></span>

<span data-ttu-id="c45a1-179">Para obtener un ejemplo, vea [plantilla de inicio rápido de hello 101-vm-sshkey GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="c45a1-179">For an example, see [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a><span data-ttu-id="c45a1-180">Cuando ejecuto `Update-AzureRmVmss` después de agregar más de un certificado de hello misma clave almacén, veo Hola siguiente mensaje:</span><span class="sxs-lookup"><span data-stu-id="c45a1-180">When I run `Update-AzureRmVmss` after adding more than one certificate from hello same key vault, I see hello following message:</span></span>
 
><span data-ttu-id="c45a1-181">Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed. (Update-AzureRmVmss: muestra secretos que contienen instancias repetidas de /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, lo que no se permite.)</span><span class="sxs-lookup"><span data-stu-id="c45a1-181">Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed.</span></span>
 
<span data-ttu-id="c45a1-182">Esto puede ocurrir si intentas toore-agregar Hola mismo almacén en lugar de utilizar un nuevo certificado de almacén para el almacén de origen existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-182">This can happen if you try toore-add hello same vault instead of using a new vault certificate for hello existing source vault.</span></span> <span data-ttu-id="c45a1-183">Hola `Add-AzureRmVmssSecret` comando no funciona correctamente si va a agregar secretos adicionales.</span><span class="sxs-lookup"><span data-stu-id="c45a1-183">hello `Add-AzureRmVmssSecret` command does not work correctly if you are adding additional secrets.</span></span>
 
<span data-ttu-id="c45a1-184">tooadd más secretos de hello mismo almacén de claves, la lista de $vmss.properties.osProfile.secrets[0].vaultCertificates Hola de actualización.</span><span class="sxs-lookup"><span data-stu-id="c45a1-184">tooadd more secrets from hello same key vault, update hello $vmss.properties.osProfile.secrets[0].vaultCertificates list.</span></span>
 
<span data-ttu-id="c45a1-185">Para hello espera estructura de entrada, consulte [crear o actualizar una máquina virtual establecer](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="c45a1-185">For hello expected input structure, see [Create or update a virtual machine set](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span></span>
 
<span data-ttu-id="c45a1-186">Buscar secreto hello en hello objeto de conjunto de escala de máquina virtual que se encuentra en el almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-186">Find hello secret in hello virtual machine scale set object that is in hello key vault.</span></span> <span data-ttu-id="c45a1-187">A continuación, agregue la lista de toohello de referencia (dirección URL de Hola y el nombre de almacén secreto de hello) certificado asociada con el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-187">Then, add your certificate reference (hello URL and hello secret store name) toohello list associated with hello vault.</span></span>

> [!NOTE] 
> <span data-ttu-id="c45a1-188">Actualmente, no se puede quitar certificados de las máquinas virtuales a través de API de conjunto de escala de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c45a1-188">Currently, you cannot remove certificates from VMs by using hello virtual machine scale set API.</span></span>
>

<span data-ttu-id="c45a1-189">Nuevas máquinas virtuales no tendrán el certificado antiguo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-189">New VMs will not have hello old certificate.</span></span> <span data-ttu-id="c45a1-190">Sin embargo, las máquinas virtuales que tienen certificados de Hola y que ya se han implementado tendrá los certificados antiguos Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-190">However, VMs that have hello certificate and which are already deployed will have hello old certificate.</span></span>
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a><span data-ttu-id="c45a1-191">¿Push escalas de máquina virtual de certificados toohello establecer sin proporcionar la contraseña de hello, al certificado de Hola se encuentra en el almacén secreto de hello?</span><span class="sxs-lookup"><span data-stu-id="c45a1-191">Can I push certificates toohello virtual machine scale set without providing hello password, when hello certificate is in hello secret store?</span></span>

<span data-ttu-id="c45a1-192">No es necesario toohard codifique las contraseñas en las secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="c45a1-192">You do not need toohard-code passwords in scripts.</span></span> <span data-ttu-id="c45a1-193">Puede recuperar dinámicamente las contraseñas con permisos de hello usar script de implementación de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-193">You can dynamically retrieve passwords with hello permissions you use toorun hello deployment script.</span></span> <span data-ttu-id="c45a1-194">Si tiene una secuencia de comandos que se mueve un certificado del almacén de claves de almacén secreto de hello, Hola almacén secreto `get certificate` comando contraseña Hola de archivo .pfx de hello también da como resultado.</span><span class="sxs-lookup"><span data-stu-id="c45a1-194">If you have a script that moves a certificate from hello secret store key vault, hello secret store `get certificate` command also outputs hello password of hello .pfx file.</span></span>
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a><span data-ttu-id="c45a1-195">¿Cómo establecer propiedades de secretos de Hola de virtualMachineProfile.osProfile para una escala de máquinas virtuales el trabajo?</span><span class="sxs-lookup"><span data-stu-id="c45a1-195">How does hello Secrets property of virtualMachineProfile.osProfile for a virtual machine scale set work?</span></span> <span data-ttu-id="c45a1-196">¿Por qué necesito valor sourceVault de hello cuando tengo toospecify Hola URI absoluto para un certificado mediante el uso de la propiedad de hello certificateUrl?</span><span class="sxs-lookup"><span data-stu-id="c45a1-196">Why do I need hello sourceVault value when I have toospecify hello absolute URI for a certificate by using hello certificateUrl property?</span></span> 

<span data-ttu-id="c45a1-197">Una referencia de certificado de administración remota de Windows (WinRM) debe estar presente en hello propiedad secretos de hello perfil de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="c45a1-197">A Windows Remote Management (WinRM) certificate reference must be present in hello Secrets property of hello OS profile.</span></span> 

<span data-ttu-id="c45a1-198">Hola de que indica el almacén de origen Hola sirve tooenforce directivas de lista (ACL) de control de acceso que existen en el modelo de servicio de nube de Azure de un usuario.</span><span class="sxs-lookup"><span data-stu-id="c45a1-198">hello purpose of indicating hello source vault is tooenforce access control list (ACL) policies that exist in a user's Azure Cloud Service model.</span></span> <span data-ttu-id="c45a1-199">Si no se especifica el almacén de origen hello, los usuarios que no tienen permisos toodeploy o acceso secretos tooa almacén de claves sería toothrough capaz de un proveedor de recursos de proceso (PRC).</span><span class="sxs-lookup"><span data-stu-id="c45a1-199">If hello source vault isn't specified, users who do not have permissions toodeploy or access secrets tooa key vault would be able toothrough a Compute Resource Provider (CRP).</span></span> <span data-ttu-id="c45a1-200">Las ACL existen incluso para recursos que no existen.</span><span class="sxs-lookup"><span data-stu-id="c45a1-200">ACLs exist even for resources that do not exist.</span></span>

<span data-ttu-id="c45a1-201">Si se proporciona un identificador de almacén de origen incorrectos pero una dirección URL válida de almacén de claves, se notifica un error al sondear operación Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-201">If you provide an incorrect source vault ID but a valid key vault URL, an error is reported when you poll hello operation.</span></span>
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a><span data-ttu-id="c45a1-202">¿Si agrega tooan secretos existente conjunto de escalas de máquina virtual, se secretos Hola insertados en las máquinas virtuales existentes, o solo en otras nuevas?</span><span class="sxs-lookup"><span data-stu-id="c45a1-202">If I add secrets tooan existing virtual machine scale set, are hello secrets injected into existing VMs, or only into new ones?</span></span> 

<span data-ttu-id="c45a1-203">Los certificados se agregan tooall las máquinas virtuales, incluso preexistente los.</span><span class="sxs-lookup"><span data-stu-id="c45a1-203">Certificates are added tooall your VMs, even preexisting ones.</span></span> <span data-ttu-id="c45a1-204">Si la escala de máquinas virtuales establece upgradePolicy propiedad se establece demasiado**manual**, Hola agregar certificado toohello VM al realizar una actualización manual en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c45a1-204">If your virtual machine scale set upgradePolicy property is set too**manual**, hello certificate is added toohello VM when you perform a manual update on hello VM.</span></span>
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a><span data-ttu-id="c45a1-205">¿Dónde se ponen los certificados para las máquinas virtuales Linux?</span><span class="sxs-lookup"><span data-stu-id="c45a1-205">Where do I put certificates for Linux VMs?</span></span>

<span data-ttu-id="c45a1-206">toolearn toodeploy certificados para las máquinas virtuales de Linux, vea [implementar tooVMs certificados desde un almacén de claves administradas por el cliente](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="c45a1-206">toolearn how toodeploy certificates for Linux VMs, see [Deploy certificates tooVMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span></span>
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a><span data-ttu-id="c45a1-207">¿Cómo se agrega un nuevo almacén certificado tooa nuevo objeto de certificado?</span><span class="sxs-lookup"><span data-stu-id="c45a1-207">How do I add a new vault certificate tooa new certificate object?</span></span>

<span data-ttu-id="c45a1-208">tooadd un secreto almacén certificado tooan existente, vea Hola siguiente ejemplo de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c45a1-208">tooadd a vault certificate tooan existing secret, see hello following PowerShell example.</span></span> <span data-ttu-id="c45a1-209">Use un solo objeto secreto.</span><span class="sxs-lookup"><span data-stu-id="c45a1-209">Use only one secret object.</span></span>
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a><span data-ttu-id="c45a1-210">¿Qué ocurre toocertificates si Restablecer imagen inicial de una máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="c45a1-210">What happens toocertificates if you reimage a VM?</span></span>

<span data-ttu-id="c45a1-211">Si restablece la imagen inicial de una máquina virtual, los certificados se eliminan.</span><span class="sxs-lookup"><span data-stu-id="c45a1-211">If you reimage a VM, certificates are deleted.</span></span> <span data-ttu-id="c45a1-212">Restableciendo la imagen inicial eliminaciones Hola todo disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="c45a1-212">Reimaging deletes hello entire OS disk.</span></span> 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a><span data-ttu-id="c45a1-213">¿Qué ocurre si elimina un certificado del almacén de claves de hello?</span><span class="sxs-lookup"><span data-stu-id="c45a1-213">What happens if you delete a certificate from hello key vault?</span></span>

<span data-ttu-id="c45a1-214">Si secreto Hola se elimina del almacén de claves de hello y, a continuación, ejecute `stop deallocate` para todas las máquinas virtuales y, a continuación, vuelva a iniciarlas, se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="c45a1-214">If hello secret is deleted from hello key vault, and then you run `stop deallocate` for all your VMs and then start them again, you will encounter a failure.</span></span> <span data-ttu-id="c45a1-215">Error de Hola se produce porque Hola CRP necesita secretos de hello tooretrieve de almacén de claves de hello, pero no es posible.</span><span class="sxs-lookup"><span data-stu-id="c45a1-215">hello failure occurs because hello CRP needs tooretrieve hello secrets from hello key vault, but it cannot.</span></span> <span data-ttu-id="c45a1-216">En este escenario, puede eliminar certificados Hola de modelo de conjunto de escala de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-216">In this scenario, you can delete hello certificates from hello virtual machine scale set model.</span></span> 

<span data-ttu-id="c45a1-217">componente de Hello CRP no conserva los secretos de cliente.</span><span class="sxs-lookup"><span data-stu-id="c45a1-217">hello CRP component does not persist customer secrets.</span></span> <span data-ttu-id="c45a1-218">Si ejecuta `stop deallocate` para todas las máquinas virtuales en el conjunto de escalas de máquina virtual de hello, se elimina la caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-218">If you run `stop deallocate` for all VMs in hello virtual machine scale set, hello cache is deleted.</span></span> <span data-ttu-id="c45a1-219">En este escenario, secretos se recuperan del almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-219">In this scenario, secrets are retrieved from hello key vault.</span></span>

<span data-ttu-id="c45a1-220">No ocurre este problema mientras se escala horizontalmente porque no hay una copia en caché del secreto de hello en Azure Service Fabric (en el modelo de inquilino único tejido Hola).</span><span class="sxs-lookup"><span data-stu-id="c45a1-220">You don't encounter this problem when scaling out because there is a cached copy of hello secret in Azure Service Fabric (in hello single-fabric tenant model).</span></span>
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a><span data-ttu-id="c45a1-221">¿Por qué tengo la ubicación exacta de hello toospecify para hello certificado URL (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), como se indica en [escenarios de seguridad de clúster de Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span><span class="sxs-lookup"><span data-stu-id="c45a1-221">Why do I have toospecify hello exact location for hello certificate URL (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), as indicated in [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span></span>
 
<span data-ttu-id="c45a1-222">Hola documentación del almacén de claves de Azure indica que Hola que obtener API de REST del secreto debe devolver la versión más reciente de Hola de secreto de Hola si no se especifica la versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-222">hello Azure Key Vault documentation states that hello Get Secret REST API should return hello latest version of hello secret if hello version is not specified.</span></span>
 
<span data-ttu-id="c45a1-223">Método</span><span class="sxs-lookup"><span data-stu-id="c45a1-223">Method</span></span> | <span data-ttu-id="c45a1-224">URL</span><span class="sxs-lookup"><span data-stu-id="c45a1-224">URL</span></span>
--- | ---
<span data-ttu-id="c45a1-225">GET</span><span class="sxs-lookup"><span data-stu-id="c45a1-225">GET</span></span> | <span data-ttu-id="c45a1-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span><span class="sxs-lookup"><span data-stu-id="c45a1-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span></span>

<span data-ttu-id="c45a1-227">Reemplace {*nombre secreto*} con nombre hello y reemplazar {*secret-version*} con la versión de Hola de secreto de hello desea tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="c45a1-227">Replace {*secret-name*} with hello name, and replace {*secret-version*} with hello version of hello secret you want tooretrieve.</span></span> <span data-ttu-id="c45a1-228">puede excluir la versión de secreto Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-228">hello secret version might be excluded.</span></span> <span data-ttu-id="c45a1-229">En ese caso, se recupera la versión actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-229">In that case, hello current version is retrieved.</span></span>
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a><span data-ttu-id="c45a1-230">¿Por qué tengo versión del certificado de hello toospecify al usar el almacén de claves?</span><span class="sxs-lookup"><span data-stu-id="c45a1-230">Why do I have toospecify hello certificate version when I use Key Vault?</span></span>

<span data-ttu-id="c45a1-231">Hola de versión del certificado de hello el almacén de claves requisito toospecify Hola sirve toomake toohello usuario claro qué certificado se implementa en sus máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c45a1-231">hello purpose of hello Key Vault requirement toospecify hello certificate version is toomake it clear toohello user what certificate is deployed on their VMs.</span></span>

<span data-ttu-id="c45a1-232">Si crea una máquina virtual y, a continuación, actualizar el secreto en el almacén de claves de hello, Hola nuevo certificado no es tooyour descargado las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c45a1-232">If you create a VM and then update your secret in hello key vault, hello new certificate is not downloaded tooyour VMs.</span></span> <span data-ttu-id="c45a1-233">Pero las máquinas virtuales aparecen tooreference la base de datos y nuevas máquinas virtuales obtienen secreto nuevo Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-233">But your VMs appear tooreference it, and new VMs get hello new secret.</span></span> <span data-ttu-id="c45a1-234">tooavoid, son tooreference requiere una versión de secreto.</span><span class="sxs-lookup"><span data-stu-id="c45a1-234">tooavoid this, you are required tooreference a secret version.</span></span>

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a><span data-ttu-id="c45a1-235">Mi equipo funciona con varios certificados que se distribuyen toous como claves públicas de CER.</span><span class="sxs-lookup"><span data-stu-id="c45a1-235">My team works with several certificates that are distributed toous as .cer public keys.</span></span> <span data-ttu-id="c45a1-236">¿Qué es hello enfoque para la implementación de este conjunto de escala de certificados tooa máquina virtual recomendado?</span><span class="sxs-lookup"><span data-stu-id="c45a1-236">What is hello recommended approach for deploying these certificates tooa virtual machine scale set?</span></span>

<span data-ttu-id="c45a1-237">conjunto de escalas de la máquina virtual de tooa de claves públicas con toodeploy .cer, puede generar un archivo .pfx que contiene solo los archivos de CER.</span><span class="sxs-lookup"><span data-stu-id="c45a1-237">toodeploy .cer public keys tooa virtual machine scale set, you can generate a .pfx file that contains only .cer files.</span></span> <span data-ttu-id="c45a1-238">toodo, use `X509ContentType = Pfx`.</span><span class="sxs-lookup"><span data-stu-id="c45a1-238">toodo this, use `X509ContentType = Pfx`.</span></span> <span data-ttu-id="c45a1-239">Por ejemplo, cargar el archivo .cer de hello como un objeto x509Certificate2 en C# o PowerShell y, a continuación, llame al método hello.</span><span class="sxs-lookup"><span data-stu-id="c45a1-239">For example, load hello .cer file as an x509Certificate2 object in C# or PowerShell, and then call hello method.</span></span> 

<span data-ttu-id="c45a1-240">Para más información, consulte [Método X509Certificate.Export (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span><span class="sxs-lookup"><span data-stu-id="c45a1-240">For more information, see [X509Certificate.Export Method (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span></span>

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a><span data-ttu-id="c45a1-241">No veo una opción para toopass de usuarios en los certificados como las cadenas base64.</span><span class="sxs-lookup"><span data-stu-id="c45a1-241">I do not see an option for users toopass in certificates as base64 strings.</span></span> <span data-ttu-id="c45a1-242">La mayoría de otros proveedores de recursos tienen esta opción.</span><span class="sxs-lookup"><span data-stu-id="c45a1-242">Most other resource providers have this option.</span></span>

<span data-ttu-id="c45a1-243">tooemulate pasando un certificado como una cadena base64, puede extraer Hola última dirección URL con versiones en una plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="c45a1-243">tooemulate passing in a certificate as a base64 string, you can extract hello latest versioned URL in a Resource Manager template.</span></span> <span data-ttu-id="c45a1-244">Hola después de la propiedad JSON en la plantilla de administrador de recursos se incluyen:</span><span class="sxs-lookup"><span data-stu-id="c45a1-244">Include hello following JSON property in your Resource Manager template:</span></span>

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a><span data-ttu-id="c45a1-245">¿Tengo certificados toowrap en objetos JSON en los almacenes de claves?</span><span class="sxs-lookup"><span data-stu-id="c45a1-245">Do I have toowrap certificates in JSON objects in key vaults?</span></span>

<span data-ttu-id="c45a1-246">En los conjuntos de escalado de máquinas virtuales y las máquinas virtuales, los certificados se tienen que encapsular en objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="c45a1-246">In virtual machine scale sets and VMs, certificates must be wrapped in JSON objects.</span></span> 

<span data-ttu-id="c45a1-247">También se admite Hola tipo de contenido application/x-pkcs12.</span><span class="sxs-lookup"><span data-stu-id="c45a1-247">We also support hello content type application/x-pkcs12.</span></span> <span data-ttu-id="c45a1-248">Para instrucciones sobre el uso de application/x-pkcs12, consulte [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/) (Certificados PFX en Azure Key Vault).</span><span class="sxs-lookup"><span data-stu-id="c45a1-248">For instructions on using application/x-pkcs12, see [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span></span>
 
<span data-ttu-id="c45a1-249">Actualmente no se admiten archivos .cer.</span><span class="sxs-lookup"><span data-stu-id="c45a1-249">We currently do not support .cer files.</span></span> <span data-ttu-id="c45a1-250">archivos de toouse .cer, exportarlos en contenedores de pfx.</span><span class="sxs-lookup"><span data-stu-id="c45a1-250">toouse .cer files, export them into .pfx containers.</span></span>



## <a name="compliance"></a><span data-ttu-id="c45a1-251">Cumplimiento normativo</span><span class="sxs-lookup"><span data-stu-id="c45a1-251">Compliance</span></span>

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a><span data-ttu-id="c45a1-252">¿Son los conjuntos de escalado de máquinas virtuales compatibles con PCI?</span><span class="sxs-lookup"><span data-stu-id="c45a1-252">Are virtual machine scale sets PCI-compliant?</span></span>

<span data-ttu-id="c45a1-253">Conjuntos de escalas de máquina virtual son una capa de API fina sobre Hola CRP.</span><span class="sxs-lookup"><span data-stu-id="c45a1-253">Virtual machine scale sets are a thin API layer on top of hello CRP.</span></span> <span data-ttu-id="c45a1-254">Ambos componentes forman parte de la plataforma de proceso de Hola Hola árbol del servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="c45a1-254">Both components are part of hello compute platform in hello Azure service tree.</span></span>

<span data-ttu-id="c45a1-255">Desde una perspectiva de cumplimiento, conjuntos de escalas de máquina virtual son una parte fundamental de la plataforma de proceso de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-255">From a compliance perspective, virtual machine scale sets are a fundamental part of hello Azure compute platform.</span></span> <span data-ttu-id="c45a1-256">Que comparten un equipo, herramientas, procesos, metodología de implementación, los controles de seguridad, just-in-time (JIT) compilación, supervisión, alertas y así sucesivamente, CRP Hola propio.</span><span class="sxs-lookup"><span data-stu-id="c45a1-256">They share a team, tools, processes, deployment methodology, security controls, just-in-time (JIT) compilation, monitoring, alerting, and so on, with hello CRP itself.</span></span> <span data-ttu-id="c45a1-257">Conjuntos de escalas de máquina virtual son Payment Card Industry (PCI)-compatibles porque Hola CRP forma parte de atestación de hello actual PCI estándar (DSS, Data Security).</span><span class="sxs-lookup"><span data-stu-id="c45a1-257">Virtual machine scale sets are Payment Card Industry (PCI)-compliant because hello CRP is part of hello current PCI Data Security Standard (DSS) attestation.</span></span>

<span data-ttu-id="c45a1-258">Para obtener más información, consulte [Hola Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span><span class="sxs-lookup"><span data-stu-id="c45a1-258">For more information, see [hello Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span></span>






## <a name="extensions"></a><span data-ttu-id="c45a1-259">Extensiones</span><span class="sxs-lookup"><span data-stu-id="c45a1-259">Extensions</span></span>

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a><span data-ttu-id="c45a1-260">¿Cómo puedo eliminar una extensión del conjunto de escalado de máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="c45a1-260">How do I delete a virtual machine scale set extension?</span></span>

<span data-ttu-id="c45a1-261">toodelete una escala de máquinas virtuales establezca la extensión, Hola use el ejemplo de PowerShell siguiente:</span><span class="sxs-lookup"><span data-stu-id="c45a1-261">toodelete a virtual machine scale set extension, use hello following PowerShell example:</span></span>

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
<span data-ttu-id="c45a1-262">Puede encontrar Hola NombreExtensión valor en `$vmss`.</span><span class="sxs-lookup"><span data-stu-id="c45a1-262">You can find hello extensionName value in `$vmss`.</span></span>
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a><span data-ttu-id="c45a1-263">¿Hay un ejemplo de plantilla de conjunto de escalado de máquinas virtuales que se integre con Operations Management Suite?</span><span class="sxs-lookup"><span data-stu-id="c45a1-263">Is there a virtual machine scale set template example that integrates with Operations Management Suite?</span></span>

<span data-ttu-id="c45a1-264">Para una escala de máquinas virtuales del conjunto de ejemplo de plantilla que se integra con Operations Management Suite, vea el segundo ejemplo de Hola en [implementar un clúster de Azure Service Fabric y habilitar la supervisión mediante el uso de análisis de registros](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span><span class="sxs-lookup"><span data-stu-id="c45a1-264">For a virtual machine scale set template example that integrates with Operations Management Suite, see hello second example in [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span></span>
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a><span data-ttu-id="c45a1-265">Extensiones parecen toorun en paralelo en conjuntos de escalas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c45a1-265">Extensions seem toorun in parallel on virtual machine scale sets.</span></span> <span data-ttu-id="c45a1-266">Esto hace que Mis toofail de extensión de script personalizado.</span><span class="sxs-lookup"><span data-stu-id="c45a1-266">This causes my custom script extension toofail.</span></span> <span data-ttu-id="c45a1-267">¿Qué puedo hacer toofix esto?</span><span class="sxs-lookup"><span data-stu-id="c45a1-267">What can I do toofix this?</span></span>

<span data-ttu-id="c45a1-268">toolearn acerca de secuenciación de extensión en conjuntos de escalas de máquina virtual, consulte [secuenciación de extensión en conjuntos de escalas de máquina virtual de Azure](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="c45a1-268">toolearn about extension sequencing in virtual machine scale sets, see [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span></span>
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="c45a1-269">¿Cómo restablecer contraseña Hola para las máquinas virtuales en el conjunto de escalas de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="c45a1-269">How do I reset hello password for VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="c45a1-270">contraseña de hello tooreset para las máquinas virtuales en la escala de máquinas virtuales establecido, utiliza extensiones de acceso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c45a1-270">tooreset hello password for VMs in your virtual machine scale set, use VM access extensions.</span></span> 

<span data-ttu-id="c45a1-271">Usar hello siguiente ejemplo de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c45a1-271">Use hello following PowerShell example:</span></span>

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
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="c45a1-272">¿Cómo se agrega un tooall de extensión máquinas virtuales en el conjunto de escalas de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="c45a1-272">How do I add an extension tooall VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="c45a1-273">Si la directiva de actualización se establece demasiado**automática**, volver a implementar plantilla Hola con nuevas propiedades de extensión Hola actualiza todas las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c45a1-273">If update policy is set too**automatic**, redeploying hello template with hello new extension properties updates all VMs.</span></span>

<span data-ttu-id="c45a1-274">Si la directiva de actualización se establece demasiado**manual**, en primer lugar actualizar extensión hello y, a continuación, actualizar manualmente todas las instancias en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c45a1-274">If update policy is set too**manual**, first update hello extension, and then manually update all instances in your VMs.</span></span>

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a><span data-ttu-id="c45a1-275">¿Si las extensiones de hello asociadas a un conjunto de escala de máquinas virtuales existentes se actualizan, existentes máquinas virtuales afectadas?</span><span class="sxs-lookup"><span data-stu-id="c45a1-275">If hello extensions associated with an existing virtual machine scale set are updated, are existing VMs affected?</span></span> <span data-ttu-id="c45a1-276">(Es decir, se Hola máquinas virtuales *no* modelo de conjunto de escala de máquina virtual de coincidencia Hola?) ¿O se ignoran?</span><span class="sxs-lookup"><span data-stu-id="c45a1-276">(That is, will hello VMs *not* match hello virtual machine scale set model?) Or are they ignored?</span></span> <span data-ttu-id="c45a1-277">¿Cuando una máquina existente se ha reparado el servicio o se restablece la imagen inicial, secuencias de comandos de Hola que están actualmente configurados en el conjunto de escalas de máquina virtual de hello ejecuta o son secuencias de comandos de Hola que se configuraron cuando se usa Hola que máquina virtual se creó por primera vez?</span><span class="sxs-lookup"><span data-stu-id="c45a1-277">When an existing machine is service-healed or reimaged, are hello scripts that are currently configured on hello virtual machine scale set executed, or are hello scripts that were configured when hello VM was first created used?</span></span>

<span data-ttu-id="c45a1-278">Si establece la definición de extensión de hello en escalas de máquina virtual de Hola se actualiza el modelo y propiedad de upgradePolicy de Hola se establece demasiado**automática**, actualiza hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c45a1-278">If hello extension definition in hello virtual machine scale set model is updated and hello upgradePolicy property is set too**automatic**, it updates hello VMs.</span></span> <span data-ttu-id="c45a1-279">Si la propiedad de hello upgradePolicy se establece demasiado**manual**, las extensiones se marcan como no coincide con el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-279">If hello upgradePolicy property is set too**manual**, extensions are flagged as not matching hello model.</span></span> 

<span data-ttu-id="c45a1-280">Si una máquina virtual existente se ha reparado el servicio, aparecerá como un reinicio y extensiones de hello no se vuelven a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="c45a1-280">If an existing VM is service-healed, it appears as a reboot, and hello extensions are not rerun.</span></span> <span data-ttu-id="c45a1-281">Si se está restableciendo la imagen inicial, es como sustituir el disco de SO Hola con la imagen de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-281">If it is reimaged, it's like replacing hello OS drive with hello source image.</span></span> <span data-ttu-id="c45a1-282">Cualquier especialización hello más reciente del modelo de, como las extensiones, se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="c45a1-282">Any specialization from hello latest model, such as extensions, are run.</span></span>
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a><span data-ttu-id="c45a1-283">¿Cómo se puede unirse a un dominio de tooan Azure AD del conjunto de escala de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="c45a1-283">How do I join a virtual machine scale set tooan Azure AD domain?</span></span>

<span data-ttu-id="c45a1-284">un dominio de Active Directory de Azure (Azure AD) de máquina virtual escala conjunto tooan toojoin, puede definir una extensión.</span><span class="sxs-lookup"><span data-stu-id="c45a1-284">toojoin a virtual machine scale set tooan Azure Active Directory (Azure AD) domain, you can define an extension.</span></span> 

<span data-ttu-id="c45a1-285">toodefine una extensión, utilice la propiedad de JsonADDomainExtension de hello:</span><span class="sxs-lookup"><span data-stu-id="c45a1-285">toodefine an extension, use hello JsonADDomainExtension property:</span></span>

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
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a><span data-ttu-id="c45a1-286">Una extensión de conjunto de escala de máquina virtual está intentando tooinstall algo que requiere un reinicio.</span><span class="sxs-lookup"><span data-stu-id="c45a1-286">My virtual machine scale set extension is trying tooinstall something that requires a reboot.</span></span> <span data-ttu-id="c45a1-287">Por ejemplo, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span><span class="sxs-lookup"><span data-stu-id="c45a1-287">For example, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span></span>

<span data-ttu-id="c45a1-288">Si la extensión de conjunto de escala de máquina virtual está intentando tooinstall algo que requiere un reinicio, puede usar la extensión de configuración de estado deseado de Azure automatización (automatización DSC) de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-288">If your virtual machine scale set extension is trying tooinstall something that requires a reboot, you can use hello Azure Automation Desired State Configuration (Automation DSC) extension.</span></span> <span data-ttu-id="c45a1-289">Si el sistema operativo de hello es Windows Server 2012 R2, Azure extrae en la instalación de Windows Management Framework (WMF) 5.0 hello, reinicios y, a continuación, continúa con la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-289">If hello operating system is Windows Server 2012 R2, Azure pulls in hello Windows Management Framework (WMF) 5.0 setup, reboots, and then continues with hello configuration.</span></span> 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a><span data-ttu-id="c45a1-290">¿Cómo activo el antimalware en el conjunto de escalado de máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="c45a1-290">How do I turn on antimalware in my virtual machine scale set?</span></span>

<span data-ttu-id="c45a1-291">conjunto de tooturn en antimalware en la escala de máquinas virtuales, use Hola siguiente ejemplo de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c45a1-291">tooturn on antimalware on your virtual machine scale set, use hello following PowerShell example:</span></span>

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve hello most recent version number of hello extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a><span data-ttu-id="c45a1-292">Necesito tooexecute un script personalizado que se hospeda en una cuenta de almacenamiento privado.</span><span class="sxs-lookup"><span data-stu-id="c45a1-292">I need tooexecute a custom script that's hosted in a private storage account.</span></span> <span data-ttu-id="c45a1-293">script de Hola se ejecuta correctamente cuando el almacenamiento hello es público, pero cuando intento toouse una firma de acceso compartido (SAS), se produce un error.</span><span class="sxs-lookup"><span data-stu-id="c45a1-293">hello script runs successfully when hello storage is public, but when I try toouse a Shared Access Signature (SAS), it fails.</span></span> <span data-ttu-id="c45a1-294">Se muestra este mensaje: "Faltan los parámetros obligatorios para la firma de acceso compartido".</span><span class="sxs-lookup"><span data-stu-id="c45a1-294">This message is displayed: “Missing mandatory parameters for valid Shared Access Signature”.</span></span> <span data-ttu-id="c45a1-295">Vínculo + SAS funciona bien desde mi explorador local.</span><span class="sxs-lookup"><span data-stu-id="c45a1-295">Link+SAS works fine from my local browser.</span></span>

<span data-ttu-id="c45a1-296">tooexecute un script personalizado que se hospeda en una cuenta de almacenamiento privado, establecer la configuración protegidos con clave de cuenta de almacenamiento de Hola y el nombre.</span><span class="sxs-lookup"><span data-stu-id="c45a1-296">tooexecute a custom script that's hosted in a private storage account, set up protected settings with hello storage account key and name.</span></span> <span data-ttu-id="c45a1-297">Para más información, consulte la sección sobre la [Extensión del script personalizado para Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span><span class="sxs-lookup"><span data-stu-id="c45a1-297">For more information, see [Custom Script Extension for Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span></span>







## <a name="networking"></a><span data-ttu-id="c45a1-298">Redes</span><span class="sxs-lookup"><span data-stu-id="c45a1-298">Networking</span></span>
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a><span data-ttu-id="c45a1-299">¿Es posible tooassign establece una escala de tooa del grupo de seguridad de red (NSG), por lo que aplicará tooall Hola NIC de VM en el conjunto de hello?</span><span class="sxs-lookup"><span data-stu-id="c45a1-299">Is it possible tooassign a Network Security Group (NSG) tooa scale set, so that it will apply tooall hello VM NICs in hello set?</span></span>

<span data-ttu-id="c45a1-300">Sí.</span><span class="sxs-lookup"><span data-stu-id="c45a1-300">Yes.</span></span> <span data-ttu-id="c45a1-301">Un grupo de seguridad de red se pueden aplicar directamente escala tooa establece haciendo referencia a ella en la sección de networkInterfaceConfigurations de Hola Hola de perfil de red.</span><span class="sxs-lookup"><span data-stu-id="c45a1-301">A Network Security Group can be applied directly tooa scale set by referencing it in hello networkInterfaceConfigurations section of hello network profile.</span></span> <span data-ttu-id="c45a1-302">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c45a1-302">Example:</span></span>

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

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a><span data-ttu-id="c45a1-303">¿Cómo realizar un intercambio de VIP para conjuntos de escalas de máquina virtual en hello misma suscripción y la misma región?</span><span class="sxs-lookup"><span data-stu-id="c45a1-303">How do I do a VIP swap for virtual machine scale sets in hello same subscription and same region?</span></span>

<span data-ttu-id="c45a1-304">Si tiene dos virtual conjuntos de escalas de máquina con servidores front-end de equilibrador de carga de Azure y están en Hola misma suscripción y región, puede cancelar la asignación de direcciones IP públicas de Hola desde cada uno de ellos y asignar toohello otro.</span><span class="sxs-lookup"><span data-stu-id="c45a1-304">If you have two virtual machine scale sets with Azure Load Balancer front-ends, and they are in hello same subscription and region, you could deallocate hello public IP addresses from each one, and assign toohello other.</span></span> <span data-ttu-id="c45a1-305">Consulte, por ejemplo, [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) (Intercambio de VIP: implementación Blue-green en Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="c45a1-305">See [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) for example.</span></span> <span data-ttu-id="c45a1-306">Esto implica un retraso aunque como Hola recursos son asignado o desasignado Hola a nivel de red.</span><span class="sxs-lookup"><span data-stu-id="c45a1-306">This does imply a delay though as hello resources are deallocated/allocated at hello network level.</span></span> <span data-ttu-id="c45a1-307">Una opción más rápida es toouse puerta de enlace de aplicaciones de Azure con dos grupos de back-end y una regla de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="c45a1-307">A faster option is toouse Azure Application Gateway with two backend pools, and a routing rule.</span></span> <span data-ttu-id="c45a1-308">También puede hospedar la aplicación con [Azure App Service](https://azure.microsoft.com/en-us/services/app-service/), que permite realizar un cambio rápido entre las ranuras de ensayo y las de producción.</span><span class="sxs-lookup"><span data-stu-id="c45a1-308">Alternatively, you could host your application with [Azure App service](https://azure.microsoft.com/en-us/services/app-service/) which provides support for fast switching between staging and production slots.</span></span>
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a><span data-ttu-id="c45a1-309">¿Cómo se puede especificar un intervalo de toouse de direcciones IP privada para estático asignación de direcciones IP privada?</span><span class="sxs-lookup"><span data-stu-id="c45a1-309">How do I specify a range of private IP addresses toouse for static private IP address allocation?</span></span>

<span data-ttu-id="c45a1-310">Las direcciones IP se seleccionan de una subred que especifique.</span><span class="sxs-lookup"><span data-stu-id="c45a1-310">IP addresses are selected from a subnet that you specify.</span></span> 

<span data-ttu-id="c45a1-311">método de asignación de Hola de direcciones IP de conjunto de escala de máquinas virtuales siempre es "dinámico", pero eso no significa que pueden cambiar estas direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="c45a1-311">hello allocation method of virtual machine scale set IP addresses is always “dynamic,” but that doesn't mean that these IP addresses can change.</span></span> <span data-ttu-id="c45a1-312">En este caso, "dinámico" solo significa que no se especifican direcciones IP de hello en una solicitud PUT.</span><span class="sxs-lookup"><span data-stu-id="c45a1-312">In this case, "dynamic" only means that you do not specify hello IP address in a PUT request.</span></span> <span data-ttu-id="c45a1-313">Especifique Hola estático establece mediante el uso de la subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-313">Specify hello static set by using hello subnet.</span></span> 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a><span data-ttu-id="c45a1-314">¿Cómo se puede implementar una máquina virtual escala conjunto tooan existente red virtual de Azure?</span><span class="sxs-lookup"><span data-stu-id="c45a1-314">How do I deploy a virtual machine scale set tooan existing Azure virtual network?</span></span> 

<span data-ttu-id="c45a1-315">red virtual de Azure existente para la tooan de conjuntos de toodeploy una escala de máquinas virtuales, vea [implementar una máquina virtual escala conjunto tooan red virtual existente](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="c45a1-315">toodeploy a virtual machine scale set tooan existing Azure virtual network, see [Deploy a virtual machine scale set tooan existing virtual network](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span></span> 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a><span data-ttu-id="c45a1-316">¿Cómo se puede agregar dirección IP de Hola de hello primera VM en una escala de máquinas virtuales establece toohello salida de una plantilla?</span><span class="sxs-lookup"><span data-stu-id="c45a1-316">How do I add hello IP address of hello first VM in a virtual machine scale set toohello output of a template?</span></span>

<span data-ttu-id="c45a1-317">dirección IP de hello tooadd de hello primera VM en una salida de toohello del conjunto de escala de máquina virtual de una plantilla, consulte [ARM: IP privadas de obtener VMSS](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span><span class="sxs-lookup"><span data-stu-id="c45a1-317">tooadd hello IP address of hello first VM in a virtual machine scale set toohello output of a template, see [ARM: Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span></span>

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a><span data-ttu-id="c45a1-318">¿Puedo usar conjuntos de escalado con redes aceleradas?</span><span class="sxs-lookup"><span data-stu-id="c45a1-318">Can I use scale sets with Accelerated Networking?</span></span>

<span data-ttu-id="c45a1-319">Sí.</span><span class="sxs-lookup"><span data-stu-id="c45a1-319">Yes.</span></span> <span data-ttu-id="c45a1-320">toouse accelerated redes, configurar enableAcceleratedNetworking tootrue en la escala del conjunto de networkInterfaceConfigurations.</span><span class="sxs-lookup"><span data-stu-id="c45a1-320">toouse accelerated networking, set enableAcceleratedNetworking tootrue in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="c45a1-321">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="c45a1-321">E.g.</span></span>
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

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a><span data-ttu-id="c45a1-322">¿Cómo se puede configurar servidores DNS de hello utilizados por un conjunto de escala?</span><span class="sxs-lookup"><span data-stu-id="c45a1-322">How can I configure hello DNS servers used by a scale set?</span></span>

<span data-ttu-id="c45a1-323">toocreate conjunto de escalas de VM con una configuración personalizada de DNS, agregue la que sección de networkInterfaceConfigurations del conjunto de una escala de toohello dnsSettings paquetes JSON.</span><span class="sxs-lookup"><span data-stu-id="c45a1-323">toocreate a VM scale set with a custom DNS configuration, add a dnsSettings JSON packet toohello scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="c45a1-324">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c45a1-324">Example:</span></span>
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a><span data-ttu-id="c45a1-325">¿Cómo puedo configurar un tooassign de conjunto de escala una tooeach de dirección IP virtual pública?</span><span class="sxs-lookup"><span data-stu-id="c45a1-325">How can I configure a scale set tooassign a public IP address tooeach VM?</span></span>

<span data-ttu-id="c45a1-326">toocreate conjunto de escalas de VM que asigna una tooeach de dirección IP virtual pública, asegúrese de versión de API de Hola de hello Microsoft.Compute/virtualMAchineScaleSets recursos es 2017-03-30 y agregar un _publicipaddressconfiguration_ paquete JSON sección de ipConfigurations del conjunto de escala de toohello.</span><span class="sxs-lookup"><span data-stu-id="c45a1-326">toocreate a VM scale set that assigns a public IP address tooeach VM, make sure hello API version of hello Microsoft.Compute/virtualMAchineScaleSets resource is 2017-03-30, and add a _publicipaddressconfiguration_ JSON packet toohello scale set ipConfigurations section.</span></span> <span data-ttu-id="c45a1-327">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c45a1-327">Example:</span></span>

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a><span data-ttu-id="c45a1-328">¿Puedo configurar un toowork de conjunto de escala con varias puertas de enlace de aplicaciones?</span><span class="sxs-lookup"><span data-stu-id="c45a1-328">Can I configure a scale set toowork with multiple Application Gateways?</span></span>

<span data-ttu-id="c45a1-329">Sí.</span><span class="sxs-lookup"><span data-stu-id="c45a1-329">Yes.</span></span> <span data-ttu-id="c45a1-330">Puede agregar Hola Id. de recurso para varios toohello de grupos de direcciones de back-end Application Gateway _applicationGatewayBackendAddressPools_ lista Hola _ipConfigurations_ sección de su conjunto de escala perfil de red.</span><span class="sxs-lookup"><span data-stu-id="c45a1-330">You can add hello resource id's for multiple Application Gateway backend address pools toohello _applicationGatewayBackendAddressPools_ list in hello _ipConfigurations_ section of your scale set network profile.</span></span>

## <a name="scale"></a><span data-ttu-id="c45a1-331">Escala</span><span class="sxs-lookup"><span data-stu-id="c45a1-331">Scale</span></span>

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a><span data-ttu-id="c45a1-332">¿En qué casos podría crear un conjunto de escalado de máquinas virtuales con menos de dos máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="c45a1-332">In what case would I create a virtual machine scale set with fewer than two VMs?</span></span>

<span data-ttu-id="c45a1-333">Una de las razones toocreate una escala de máquinas virtuales establece con menos de dos máquinas virtuales debería establecerse propiedades elástico de hello toouse de una escala de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c45a1-333">One reason toocreate a virtual machine scale set with fewer than two VMs would be toouse hello elastic properties of a virtual machine scale set.</span></span> <span data-ttu-id="c45a1-334">Por ejemplo, podría implementar un conjunto de escalas de máquina virtual con cero toodefine de máquinas virtuales de la infraestructura sin pagar la máquina virtual que ejecuta los costos.</span><span class="sxs-lookup"><span data-stu-id="c45a1-334">For example, you could deploy a virtual machine scale set with zero VMs toodefine your infrastructure without paying VM running costs.</span></span> <span data-ttu-id="c45a1-335">A continuación, cuando esté listo toodeploy las máquinas virtuales, aumentar la capacidad"hello" de recuento de instancias producción de hello máquina virtual escala conjunto toohello.</span><span class="sxs-lookup"><span data-stu-id="c45a1-335">Then, when you are ready toodeploy VMs, increase hello “capacity” of hello virtual machine scale set toohello production instance count.</span></span>

<span data-ttu-id="c45a1-336">Otra razón por la que podría crear un conjunto de escalado de máquinas virtuales con menos de dos máquinas virtuales es si le preocupa menos la disponibilidad que el uso de un conjunto de disponibilidad con máquinas virtuales discretas.</span><span class="sxs-lookup"><span data-stu-id="c45a1-336">Another reason you might create a virtual machine scale set with fewer than two VMs is if you're concerned less with availability than in using an availability set with discrete VMs.</span></span> <span data-ttu-id="c45a1-337">Conjuntos de escalas de máquina virtual ofrecen una toowork de manera con unidades de proceso no diferenciados que son fungible.</span><span class="sxs-lookup"><span data-stu-id="c45a1-337">Virtual machine scale sets give you a way toowork with undifferentiated compute units that are fungible.</span></span> <span data-ttu-id="c45a1-338">Esta uniformidad es un diferenciador clave entre los conjuntos de escalado de máquinas virtuales y los conjuntos de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="c45a1-338">This uniformity is a key differentiator for virtual machine scale sets versus availability sets.</span></span> <span data-ttu-id="c45a1-339">Muchas cargas de trabajo sin estado no realizan seguimiento de unidades individuales.</span><span class="sxs-lookup"><span data-stu-id="c45a1-339">Many stateless workloads do not track individual units.</span></span> <span data-ttu-id="c45a1-340">Si se quita la carga de trabajo de hello, puede reducir tooone unidad de proceso y, a continuación, escalar toomany cuando aumenta la carga de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-340">If hello workload drops, you can scale down tooone compute unit, and then scale up toomany when hello workload increases.</span></span>

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="c45a1-341">¿Cómo se cambia el número de Hola de máquinas virtuales en un conjunto de escalas de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="c45a1-341">How do I change hello number of VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="c45a1-342">número de hello toochange de máquinas virtuales en un conjunto de escalas de máquina virtual, consulte [cambiar el número de instancias de Hola de un conjunto de escalas de máquina virtual](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="c45a1-342">toochange hello number of VMs in a virtual machine scale set, see [Change hello instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span></span>

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a><span data-ttu-id="c45a1-343">¿Cómo puedo definir alertas personalizadas para cuando se alcanzan determinados umbrales?</span><span class="sxs-lookup"><span data-stu-id="c45a1-343">How do I define custom alerts for when certain thresholds are reached?</span></span>

<span data-ttu-id="c45a1-344">Dispone de cierta flexibilidad en la manera de controlar las alertas de umbrales especificados.</span><span class="sxs-lookup"><span data-stu-id="c45a1-344">You have some flexibility in how you handle alerts for specified thresholds.</span></span> <span data-ttu-id="c45a1-345">Por ejemplo, puede definir webhooks personalizados.</span><span class="sxs-lookup"><span data-stu-id="c45a1-345">For example, you can define customized webhooks.</span></span> <span data-ttu-id="c45a1-346">Hola webhook ejemplo siguiente es de una plantilla de administrador de recursos:</span><span class="sxs-lookup"><span data-stu-id="c45a1-346">hello following webhook example is from a Resource Manager template:</span></span>

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

<span data-ttu-id="c45a1-347">En este ejemplo, una alerta pasa a tooPagerduty.com cuando se alcanza un umbral.</span><span class="sxs-lookup"><span data-stu-id="c45a1-347">In this example, an alert goes tooPagerduty.com when a threshold is reached.</span></span>



## <a name="patching-and-operations"></a><span data-ttu-id="c45a1-348">Aplicación de revisiones y operaciones</span><span class="sxs-lookup"><span data-stu-id="c45a1-348">Patching and operations</span></span>

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a><span data-ttu-id="c45a1-349">¿Cómo creo un conjunto de escalado en un grupo de recursos existente?</span><span class="sxs-lookup"><span data-stu-id="c45a1-349">How do I create a scale set in an existing resource group?</span></span>

<span data-ttu-id="c45a1-350">Crear conjuntos de escala en un recurso existente grupo no aún es posible desde Hola portal de Azure, pero puede especificar un grupo de recursos existente cuando la implementación de una escala establecido desde una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c45a1-350">Creating scale sets in an existing resource group is not yet possible from hello Azure portal, but you can specify an existing resource group when deploying a scale set from an Azure Resource Manager template.</span></span> <span data-ttu-id="c45a1-351">También puede especificar un grupo de recursos existente al crear un conjunto de escalado con Azure PowerShell o CLI.</span><span class="sxs-lookup"><span data-stu-id="c45a1-351">You can also specify an existing resource group when creating a scale set using Azure PowerShell or CLI.</span></span>

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a><span data-ttu-id="c45a1-352">¿Podemos mover que una escala establece el grupo de recursos de tooanother?</span><span class="sxs-lookup"><span data-stu-id="c45a1-352">Can we move a scale set tooanother resource group?</span></span>

<span data-ttu-id="c45a1-353">Sí, puede mover escala conjunto recursos tooa nueva suscripción o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c45a1-353">Yes, you can move scale set resources tooa new subscription or resource group.</span></span>

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a><span data-ttu-id="c45a1-354">¿Cómo actualizar tooI mi escala de máquinas virtuales establece tooa nueva imagen?</span><span class="sxs-lookup"><span data-stu-id="c45a1-354">How tooI update my virtual machine scale set tooa new image?</span></span> <span data-ttu-id="c45a1-355">¿Cómo administro la aplicación de revisiones?</span><span class="sxs-lookup"><span data-stu-id="c45a1-355">How do I manage patching?</span></span>

<span data-ttu-id="c45a1-356">Consulte tooupdate la escala de máquinas virtuales establece tooa nueva imagen y aplicación de revisiones toomanage [actualizar un conjunto de escalas de máquina virtual](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span><span class="sxs-lookup"><span data-stu-id="c45a1-356">tooupdate your virtual machine scale set tooa new image, and toomanage patching, see [Upgrade a virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span></span>

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a><span data-ttu-id="c45a1-357">¿Puedo usar tooreset de operación de restablecimiento de imagen inicial de hello una máquina virtual sin cambiar la imagen de hello?</span><span class="sxs-lookup"><span data-stu-id="c45a1-357">Can I use hello reimage operation tooreset a VM without changing hello image?</span></span> <span data-ttu-id="c45a1-358">(Es decir, desea restablecer una VM toofactory configuración en lugar de la nueva imagen de tooa.)</span><span class="sxs-lookup"><span data-stu-id="c45a1-358">(That is, I want reset a VM toofactory settings rather than tooa new image.)</span></span>

<span data-ttu-id="c45a1-359">Sí, puede usar tooreset de operación de restablecimiento de imagen inicial de hello una máquina virtual sin cambiar la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-359">Yes, you can use hello reimage operation tooreset a VM without changing hello image.</span></span> <span data-ttu-id="c45a1-360">Sin embargo, si establece la escala de la máquina virtual hace referencia una imagen de plataforma con `version = latest`, la máquina virtual puede actualizar tooa imagen del sistema operativo posterior cuando se llama a `reimage`.</span><span class="sxs-lookup"><span data-stu-id="c45a1-360">However, if your virtual machine scale set references a platform image with `version = latest`, your VM can update tooa later OS image when you call `reimage`.</span></span>

<span data-ttu-id="c45a1-361">Para más información, consulte el artículo sobre la [administración de todas las máquinas virtuales de un conjunto de escalado de máquinas virtuales](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span><span class="sxs-lookup"><span data-stu-id="c45a1-361">For more information, see [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="c45a1-362">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="c45a1-362">Troubleshooting</span></span>

### <a name="how-do-i-turn-on-boot-diagnostics"></a><span data-ttu-id="c45a1-363">¿Cómo se activa el diagnóstico de arranque?</span><span class="sxs-lookup"><span data-stu-id="c45a1-363">How do I turn on boot diagnostics?</span></span>

<span data-ttu-id="c45a1-364">tooturn en el diagnóstico de arranque, en primer lugar, cree una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c45a1-364">tooturn on boot diagnostics, first, create a storage account.</span></span> <span data-ttu-id="c45a1-365">A continuación, coloque este bloque de JSON en el conjunto de escalas de máquina virtual **virtualMachineProfile**y actualizar el conjunto de escalas de máquina virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="c45a1-365">Then, put this JSON block in your virtual machine scale set **virtualMachineProfile**, and update hello virtual machine scale set:</span></span>

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

<span data-ttu-id="c45a1-366">Cuando se crea una nueva máquina virtual, Hola propiedad InstanceView de hello VM muestra los detalles de hello para la captura de pantalla de Hola y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="c45a1-366">When a new VM is created, hello InstanceView property of hello VM shows hello details for hello screenshot, and so on.</span></span> <span data-ttu-id="c45a1-367">Este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c45a1-367">Here's an example:</span></span>
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a><span data-ttu-id="c45a1-368">Propiedades de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c45a1-368">Virtual machine properties</span></span>

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="c45a1-369">¿Cómo obtengo información de propiedades de cada máquina virtual sin tener que realizar varias llamadas?</span><span class="sxs-lookup"><span data-stu-id="c45a1-369">How do I get property information for each VM without making multiple calls?</span></span> <span data-ttu-id="c45a1-370">¿Por ejemplo, cómo obtendría dominio de error de Hola para cada uno de hello 100 máquinas virtuales en el conjunto de escalas de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="c45a1-370">For example, how would I get hello fault domain for each of hello 100 VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="c45a1-371">información de la propiedad tooget para cada máquina virtual sin realizar varias llamadas, puede llamar a `ListVMInstanceViews` realizando una API de REST `GET` en hello siguiente URI de recurso:</span><span class="sxs-lookup"><span data-stu-id="c45a1-371">tooget property information for each VM without making multiple calls, you can call `ListVMInstanceViews` by doing a REST API `GET` on hello following resource URI:</span></span>

<span data-ttu-id="c45a1-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span><span class="sxs-lookup"><span data-stu-id="c45a1-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span></span>

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="c45a1-373">¿Pasar argumentos de extensión distinto toodifferent las máquinas virtuales en un conjunto de escalas de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="c45a1-373">Can I pass different extension arguments toodifferent VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="c45a1-374">No, no se puede pasar argumentos de extensión distinto toodifferent las máquinas virtuales en un conjunto de escalas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c45a1-374">No, you cannot pass different extension arguments toodifferent VMs in a virtual machine scale set.</span></span> <span data-ttu-id="c45a1-375">Sin embargo, las extensiones pueden actuar en función de propiedades únicas de Hola de VM que se ejecutan en, por ejemplo, como en el nombre de la máquina de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a1-375">However, extensions can act based on hello unique properties of hello VM they are running on, such as on hello machine name.</span></span> <span data-ttu-id="c45a1-376">Las extensiones también pueden consultar metadatos de la instancia en http://169.254.169.254 tooget obtener más información acerca de hello VM.</span><span class="sxs-lookup"><span data-stu-id="c45a1-376">Extensions also can query instance metadata on http://169.254.169.254 tooget more information about hello VM.</span></span>

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a><span data-ttu-id="c45a1-377">¿Por qué hay huecos entre los nombres de máquina virtual de mi conjunto de escalado de máquinas virtuales y los identificadores de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="c45a1-377">Why are there gaps between my virtual machine scale set VM machine names and VM IDs?</span></span> <span data-ttu-id="c45a1-378">Por ejemplo: 0, 1, 3...</span><span class="sxs-lookup"><span data-stu-id="c45a1-378">For example: 0, 1, 3...</span></span>

<span data-ttu-id="c45a1-379">Hay espacios entre los nombres de máquina virtual de máquina virtual escala conjunto y el Id. de VM porque la escala de máquinas virtuales configurada **sobreaprovisionamiento** propiedad se establece el valor predeterminado de toohello de **true**.</span><span class="sxs-lookup"><span data-stu-id="c45a1-379">There are gaps between your virtual machine scale set VM machine names and VM IDs because your virtual machine scale set **overprovision** property is set toohello default value of **true**.</span></span> <span data-ttu-id="c45a1-380">Si en exceso se establece demasiado**true**, más máquinas virtuales que solicitado se crean.</span><span class="sxs-lookup"><span data-stu-id="c45a1-380">If overprovisioning is set too**true**, more VMs than requested are created.</span></span> <span data-ttu-id="c45a1-381">Las máquinas virtuales adicionales se eliminan a continuación.</span><span class="sxs-lookup"><span data-stu-id="c45a1-381">Extra VMs are then deleted.</span></span> <span data-ttu-id="c45a1-382">En este caso, obtener implementación mayor confiabilidad, pero a costa de Hola de nombres contiguo y traducción de direcciones de red (NAT) contiguos reglas.</span><span class="sxs-lookup"><span data-stu-id="c45a1-382">In this case, you gain increased deployment reliability, but at hello expense of contiguous naming and contiguous Network Address Translation (NAT) rules.</span></span> 

<span data-ttu-id="c45a1-383">Puede establecer esta propiedad demasiado**false**.</span><span class="sxs-lookup"><span data-stu-id="c45a1-383">You can set this property too**false**.</span></span> <span data-ttu-id="c45a1-384">Para conjuntos de escalado de máquinas virtuales pequeños, esto no afecta significativamente a confiabilidad de la implementación.</span><span class="sxs-lookup"><span data-stu-id="c45a1-384">For small virtual machine scale sets, this doesn't significantly affect deployment reliability.</span></span>

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a><span data-ttu-id="c45a1-385">¿Cuál es la diferencia de hello entre eliminar una máquina virtual en un conjunto de escalas de máquina virtual y desasignar Hola VM?</span><span class="sxs-lookup"><span data-stu-id="c45a1-385">What is hello difference between deleting a VM in a virtual machine scale set and deallocating hello VM?</span></span> <span data-ttu-id="c45a1-386">¿Cuándo debo elegir uno sobre Hola otro?</span><span class="sxs-lookup"><span data-stu-id="c45a1-386">When should I choose one over hello other?</span></span>

<span data-ttu-id="c45a1-387">Hello diferencia principal entre la eliminación de una máquina virtual en un conjunto de escalas de máquina virtual y desasignar Hola VM es que `deallocate` Hola los discos duros virtuales (VHD), no se elimina.</span><span class="sxs-lookup"><span data-stu-id="c45a1-387">hello main difference between deleting a VM in a virtual machine scale set and deallocating hello VM is that `deallocate` doesn’t delete hello virtual hard disks (VHDs).</span></span> <span data-ttu-id="c45a1-388">Hay costos de almacenamiento asociados con la ejecución de `stop deallocate`.</span><span class="sxs-lookup"><span data-stu-id="c45a1-388">There are storage costs associated with running `stop deallocate`.</span></span> <span data-ttu-id="c45a1-389">Puede usar uno u Hola Sí para uno de hello siguientes motivos:</span><span class="sxs-lookup"><span data-stu-id="c45a1-389">You might use one or hello other for one of hello following reasons:</span></span>

- <span data-ttu-id="c45a1-390">Desee toostop pagar costos de proceso, pero desea tookeep Hola disco estado del programa Hola a máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c45a1-390">You want toostop paying compute costs, but you want tookeep hello disk state of hello VMs.</span></span>
- <span data-ttu-id="c45a1-391">Desea toostart un conjunto de máquinas virtuales más rápidamente de lo que puede escalar horizontalmente un conjunto de escalas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c45a1-391">You want toostart a set of VMs more quickly than you could scale out a virtual machine scale set.</span></span>
  - <span data-ttu-id="c45a1-392">Escenario de toothis relacionados, podría haber creado su propio motor de escalado automático y quiere una escala to-end más rápida.</span><span class="sxs-lookup"><span data-stu-id="c45a1-392">Related toothis scenario, you might have created your own autoscale engine and want a faster end-to-end scale.</span></span>
- <span data-ttu-id="c45a1-393">Tiene un conjunto de escalado de máquinas virtuales que se distribuye de forma irregular a través de dominios de error o dominios de actualización.</span><span class="sxs-lookup"><span data-stu-id="c45a1-393">You have a virtual machine scale set that is unevenly distributed across fault domains or update domains.</span></span> <span data-ttu-id="c45a1-394">Esto puede ser porque eliminó de forma selectiva las máquinas virtuales, o porque se eliminaron las máquinas virtuales después proveer en exceso.</span><span class="sxs-lookup"><span data-stu-id="c45a1-394">This might be because you selectively deleted VMs, or because VMs were deleted after overprovisioning.</span></span> <span data-ttu-id="c45a1-395">Ejecuta `stop deallocate` seguido `start` en la máquina virtual de hello escala establecida de manera uniforme distribuye hello las máquinas virtuales a través de dominios de error o dominios de actualización.</span><span class="sxs-lookup"><span data-stu-id="c45a1-395">Running `stop deallocate` followed by `start` on hello virtual machine scale set evenly distributes hello VMs across fault domains or update domains.</span></span>

