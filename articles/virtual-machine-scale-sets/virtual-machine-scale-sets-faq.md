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
# <a name="azure-virtual-machine-scale-sets-faqs"></a>Preguntas frecuentes sobre los conjuntos de escalado de máquinas virtuales de Azure

Obtenga respuestas toofrequently preguntas más frecuentes sobre la escala de la máquina virtual se establece en Azure.

## <a name="autoscale"></a>Autoscale

### <a name="what-are-best-practices-for-azure-autoscale"></a>¿Cuáles son los procedimientos recomendados para el escalado automático de Azure?

Para procedimientos recomendados para el escalado automático, consulte [Procedimientos recomendados de escalado automático en elementos virtuales](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a>¿Dónde puedo encontrar los nombres de métricas para un escalado automático que use métricas basadas en host?

Para nombres de métrica para un escalado automático que use métricas basadas en host, consulte [Métricas compatibles con Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a>¿Hay algún ejemplo de escalado automático basado en una longitud de cola y un tema de Azure Service Bus?

Sí. Para ejemplos de escalado automático basados en un tema de Service Bus y una longitud de cola, consulte [Métricas comunes de escalado automático de Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).

Para una cola de Bus de servicio, utilice Hola después JSON:

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

Para una cola de almacenamiento, utilice Hola después JSON:

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

Reemplace los valores de ejemplo con los identificadores uniformes de recursos (URI) del recurso.


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a>¿Debo realizar el escalado automático usando métricas basadas en host o usar una extensión de diagnóstico?

Puede crear una configuración de escalado automático en una métricas de nivel de host de máquina virtual toouse o las métricas de basado en el sistema operativo invitado.

Para obtener una lista de métricas admitidas, consulte [Métricas comunes de escalado automático de Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics). 

Para obtener un ejemplo completo para conjuntos de escalado de máquinas virtuales, consulte [Configuración avanzada de escalado automático con plantillas de Resource Manager para conjuntos de escalado de máquinas virtuales](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets). 

ejemplo de Hola usa métrica de CPU de nivel de host de hello y una métrica de recuento de mensajes.



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a>¿Cómo se configuran las reglas de alerta en un conjunto de escalado de máquinas virtuales?

Puede crear alertas en las métricas de los conjuntos de escalado de máquinas virtuales a través de PowerShell o CLI de Azure. Para más información, consulte [Ejemplos de inicio rápido de PowerShell de Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) y [Ejemplos de inicio rápido de CLI multiplataforma de Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).

Hola elemento TargetResourceId del conjunto de escalas de máquina virtual de hello tiene el siguiente aspecto: 

/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname

Puede elegir cualquier contador de rendimiento de la máquina virtual como Hola métrica tooset una alerta para. Para obtener más información, consulte [métricas de SO invitado para máquinas virtuales de Windows basada en el Administrador de recursos](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) y [métricas de SO invitado para máquinas virtuales Linux](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) en hello [métricas comunes de escalado automático de Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)artículo.

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a>¿Cómo se configura el escalado automático en un conjunto de escalado de máquinas virtuales utilizando PowerShell?

tooset de escalado automático en una escala de máquinas virtuales que se establece mediante el uso de PowerShell, consulte la entrada de blog hello [cómo establece tooadd escalado automático tooan escala de la máquina virtual de Azure](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).




## <a name="certificates"></a>Certificados

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a>¿Cómo distribuir forma segura un toohello certificado VM? ¿Cómo se puede aprovisionar un toorun de conjunto de escala un sitio Web donde hello SSL para el sitio Web de Hola se envía con seguridad de una configuración de certificado de máquina virtual? (operación de rotación de certificado común de hello podría ser casi Hola igual que una operación de actualización de configuración.) ¿Tiene un ejemplo de cómo toodo esto? 

toosecurely enviar un toohello certificado VM, puede instalar un certificado de cliente directamente en un almacén de certificados de Windows desde el almacén de claves del cliente de Hola.

Usar hello después JSON:

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

código de Hello es compatible con Windows y Linux.

Para más información, consulte el artículo sobre la [creación o actualización de un conjunto de escalado de máquinas virtuales](https://msdn.microsoft.com/library/mt589035.aspx).


### <a name="example-of-self-signed-certificate"></a>Ejemplo de un certificado autofirmado

1.  Creación de un certificado autofirmado en un almacén de claves.

    Usar hello siga los comandos de PowerShell:

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    Esto deja de comando Hola entrada para la plantilla de hello Azure Resource Manager.

    Para obtener un ejemplo de cómo toocreate un certificado autofirmado en un almacén de claves, consulte [escenarios de seguridad de clúster de Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).

2.  Cambiar la plantilla de administrador de recursos de Hola.

    Agregar esta propiedad también**virtualMachineProfile**, como parte del programa Hola recurso de conjunto de escalas de máquina virtual:

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
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a>¿Se puede especificar un toouse de par de claves de SSH para la autenticación de SSH con una escala de máquinas virtuales de Linux establecer a partir de una plantilla de administrador de recursos?  

Sí. Hola API de REST para **osProfile** es similar toohello API de REST de la máquina virtual estándar. 

Incluya **osProfile** en la plantilla:

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
 
Este bloque JSON se usa en [plantilla de inicio rápido de hello 101-vm-sshkey GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).
 
Hola perfil de sistema operativo también se utiliza en [grelayhost.json Hola rápida de GitHub iniciar plantilla](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).

Para más información, consulte el artículo sobre la [creación o actualización de un conjunto de escalado de máquinas virtuales](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).
  

### <a name="how-do-i-remove-deprecated-certificates"></a>¿Cómo se quitan los certificados en desuso? 

tooremove en desuso certificados, quitar Hola certificado antiguo de la lista de certificados del almacén de Hola. Dejar todos los certificados de Hola que desee tooremain en el equipo en la lista de Hola. No se quitará el certificado de Hola de todas las máquinas virtuales. No agrega Hola certificado toonew las máquinas virtuales que se crean en el conjunto de escalas de máquina virtual de Hola. 

certificado de hello tooremove de máquinas virtuales existentes, escribir un script personalizado extensión toomanually quitar Hola certificados desde el almacén de certificados.
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a>¿Cómo insertar una clave pública SSH existente en hello máquina virtual escala conjunto SSH capa durante el aprovisionamiento? Desea toostore Hola SSH valores de clave pública en el almacén de claves de Azure y utilizarlas en mi plantilla de administrador de recursos.

Si va a proporcionar Hola máquinas virtuales solo con una clave SSH pública, no es necesario tooput hello las claves públicas en el almacén de claves. Las claves públicas no son secretas.
 
Puede proporcionar claves públicas SSH en texto sin formato al crear una máquina virtual Linux:

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
 
Nombre del elemento de linuxConfiguration | Obligatorio | Tipo | Descripción
--- | --- | --- | --- |  ---
ssh | No | Colección | Especifica la configuración de la clave SSH Hola para un sistema operativo Linux
path | Sí | String | Especifica la ruta del archivo de Linux de Hola donde las claves SSH de Hola o certificado debe estar ubicado
keyData | Sí | string | Especifica una clave pública SSH codificada en base64

Para obtener un ejemplo, vea [plantilla de inicio rápido de hello 101-vm-sshkey GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a>Cuando ejecuto `Update-AzureRmVmss` después de agregar más de un certificado de hello misma clave almacén, veo Hola siguiente mensaje:
 
>Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed. (Update-AzureRmVmss: muestra secretos que contienen instancias repetidas de /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, lo que no se permite.)
 
Esto puede ocurrir si intentas toore-agregar Hola mismo almacén en lugar de utilizar un nuevo certificado de almacén para el almacén de origen existente de Hola. Hola `Add-AzureRmVmssSecret` comando no funciona correctamente si va a agregar secretos adicionales.
 
tooadd más secretos de hello mismo almacén de claves, la lista de $vmss.properties.osProfile.secrets[0].vaultCertificates Hola de actualización.
 
Para hello espera estructura de entrada, consulte [crear o actualizar una máquina virtual establecer](https://msdn.microsoft.com/library/azure/mt589035.aspx).
 
Buscar secreto hello en hello objeto de conjunto de escala de máquina virtual que se encuentra en el almacén de claves de Hola. A continuación, agregue la lista de toohello de referencia (dirección URL de Hola y el nombre de almacén secreto de hello) certificado asociada con el almacén de Hola.

> [!NOTE] 
> Actualmente, no se puede quitar certificados de las máquinas virtuales a través de API de conjunto de escala de hello máquina virtual.
>

Nuevas máquinas virtuales no tendrán el certificado antiguo de Hola. Sin embargo, las máquinas virtuales que tienen certificados de Hola y que ya se han implementado tendrá los certificados antiguos Hola.
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a>¿Push escalas de máquina virtual de certificados toohello establecer sin proporcionar la contraseña de hello, al certificado de Hola se encuentra en el almacén secreto de hello?

No es necesario toohard codifique las contraseñas en las secuencias de comandos. Puede recuperar dinámicamente las contraseñas con permisos de hello usar script de implementación de toorun Hola. Si tiene una secuencia de comandos que se mueve un certificado del almacén de claves de almacén secreto de hello, Hola almacén secreto `get certificate` comando contraseña Hola de archivo .pfx de hello también da como resultado.
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a>¿Cómo establecer propiedades de secretos de Hola de virtualMachineProfile.osProfile para una escala de máquinas virtuales el trabajo? ¿Por qué necesito valor sourceVault de hello cuando tengo toospecify Hola URI absoluto para un certificado mediante el uso de la propiedad de hello certificateUrl? 

Una referencia de certificado de administración remota de Windows (WinRM) debe estar presente en hello propiedad secretos de hello perfil de sistema operativo. 

Hola de que indica el almacén de origen Hola sirve tooenforce directivas de lista (ACL) de control de acceso que existen en el modelo de servicio de nube de Azure de un usuario. Si no se especifica el almacén de origen hello, los usuarios que no tienen permisos toodeploy o acceso secretos tooa almacén de claves sería toothrough capaz de un proveedor de recursos de proceso (PRC). Las ACL existen incluso para recursos que no existen.

Si se proporciona un identificador de almacén de origen incorrectos pero una dirección URL válida de almacén de claves, se notifica un error al sondear operación Hola.
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a>¿Si agrega tooan secretos existente conjunto de escalas de máquina virtual, se secretos Hola insertados en las máquinas virtuales existentes, o solo en otras nuevas? 

Los certificados se agregan tooall las máquinas virtuales, incluso preexistente los. Si la escala de máquinas virtuales establece upgradePolicy propiedad se establece demasiado**manual**, Hola agregar certificado toohello VM al realizar una actualización manual en hello máquina virtual.
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a>¿Dónde se ponen los certificados para las máquinas virtuales Linux?

toolearn toodeploy certificados para las máquinas virtuales de Linux, vea [implementar tooVMs certificados desde un almacén de claves administradas por el cliente](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a>¿Cómo se agrega un nuevo almacén certificado tooa nuevo objeto de certificado?

tooadd un secreto almacén certificado tooan existente, vea Hola siguiente ejemplo de PowerShell. Use un solo objeto secreto.
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a>¿Qué ocurre toocertificates si Restablecer imagen inicial de una máquina virtual?

Si restablece la imagen inicial de una máquina virtual, los certificados se eliminan. Restableciendo la imagen inicial eliminaciones Hola todo disco del sistema operativo. 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a>¿Qué ocurre si elimina un certificado del almacén de claves de hello?

Si secreto Hola se elimina del almacén de claves de hello y, a continuación, ejecute `stop deallocate` para todas las máquinas virtuales y, a continuación, vuelva a iniciarlas, se producirá un error. Error de Hola se produce porque Hola CRP necesita secretos de hello tooretrieve de almacén de claves de hello, pero no es posible. En este escenario, puede eliminar certificados Hola de modelo de conjunto de escala de máquina virtual de Hola. 

componente de Hello CRP no conserva los secretos de cliente. Si ejecuta `stop deallocate` para todas las máquinas virtuales en el conjunto de escalas de máquina virtual de hello, se elimina la caché de Hola. En este escenario, secretos se recuperan del almacén de claves de Hola.

No ocurre este problema mientras se escala horizontalmente porque no hay una copia en caché del secreto de hello en Azure Service Fabric (en el modelo de inquilino único tejido Hola).
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a>¿Por qué tengo la ubicación exacta de hello toospecify para hello certificado URL (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), como se indica en [escenarios de seguridad de clúster de Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?
 
Hola documentación del almacén de claves de Azure indica que Hola que obtener API de REST del secreto debe devolver la versión más reciente de Hola de secreto de Hola si no se especifica la versión de Hola.
 
Método | URL
--- | ---
GET | https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}

Reemplace {*nombre secreto*} con nombre hello y reemplazar {*secret-version*} con la versión de Hola de secreto de hello desea tooretrieve. puede excluir la versión de secreto Hola. En ese caso, se recupera la versión actual de Hola.
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a>¿Por qué tengo versión del certificado de hello toospecify al usar el almacén de claves?

Hola de versión del certificado de hello el almacén de claves requisito toospecify Hola sirve toomake toohello usuario claro qué certificado se implementa en sus máquinas virtuales.

Si crea una máquina virtual y, a continuación, actualizar el secreto en el almacén de claves de hello, Hola nuevo certificado no es tooyour descargado las máquinas virtuales. Pero las máquinas virtuales aparecen tooreference la base de datos y nuevas máquinas virtuales obtienen secreto nuevo Hola. tooavoid, son tooreference requiere una versión de secreto.

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a>Mi equipo funciona con varios certificados que se distribuyen toous como claves públicas de CER. ¿Qué es hello enfoque para la implementación de este conjunto de escala de certificados tooa máquina virtual recomendado?

conjunto de escalas de la máquina virtual de tooa de claves públicas con toodeploy .cer, puede generar un archivo .pfx que contiene solo los archivos de CER. toodo, use `X509ContentType = Pfx`. Por ejemplo, cargar el archivo .cer de hello como un objeto x509Certificate2 en C# o PowerShell y, a continuación, llame al método hello. 

Para más información, consulte [Método X509Certificate.Export (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a>No veo una opción para toopass de usuarios en los certificados como las cadenas base64. La mayoría de otros proveedores de recursos tienen esta opción.

tooemulate pasando un certificado como una cadena base64, puede extraer Hola última dirección URL con versiones en una plantilla de administrador de recursos. Hola después de la propiedad JSON en la plantilla de administrador de recursos se incluyen:

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a>¿Tengo certificados toowrap en objetos JSON en los almacenes de claves?

En los conjuntos de escalado de máquinas virtuales y las máquinas virtuales, los certificados se tienen que encapsular en objetos JSON. 

También se admite Hola tipo de contenido application/x-pkcs12. Para instrucciones sobre el uso de application/x-pkcs12, consulte [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/) (Certificados PFX en Azure Key Vault).
 
Actualmente no se admiten archivos .cer. archivos de toouse .cer, exportarlos en contenedores de pfx.



## <a name="compliance"></a>Cumplimiento normativo

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a>¿Son los conjuntos de escalado de máquinas virtuales compatibles con PCI?

Conjuntos de escalas de máquina virtual son una capa de API fina sobre Hola CRP. Ambos componentes forman parte de la plataforma de proceso de Hola Hola árbol del servicio de Azure.

Desde una perspectiva de cumplimiento, conjuntos de escalas de máquina virtual son una parte fundamental de la plataforma de proceso de Azure Hola. Que comparten un equipo, herramientas, procesos, metodología de implementación, los controles de seguridad, just-in-time (JIT) compilación, supervisión, alertas y así sucesivamente, CRP Hola propio. Conjuntos de escalas de máquina virtual son Payment Card Industry (PCI)-compatibles porque Hola CRP forma parte de atestación de hello actual PCI estándar (DSS, Data Security).

Para obtener más información, consulte [Hola Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).






## <a name="extensions"></a>Extensiones

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a>¿Cómo puedo eliminar una extensión del conjunto de escalado de máquinas virtuales?

toodelete una escala de máquinas virtuales establezca la extensión, Hola use el ejemplo de PowerShell siguiente:

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
Puede encontrar Hola NombreExtensión valor en `$vmss`.
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a>¿Hay un ejemplo de plantilla de conjunto de escalado de máquinas virtuales que se integre con Operations Management Suite?

Para una escala de máquinas virtuales del conjunto de ejemplo de plantilla que se integra con Operations Management Suite, vea el segundo ejemplo de Hola en [implementar un clúster de Azure Service Fabric y habilitar la supervisión mediante el uso de análisis de registros](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a>Extensiones parecen toorun en paralelo en conjuntos de escalas de máquina virtual. Esto hace que Mis toofail de extensión de script personalizado. ¿Qué puedo hacer toofix esto?

toolearn acerca de secuenciación de extensión en conjuntos de escalas de máquina virtual, consulte [secuenciación de extensión en conjuntos de escalas de máquina virtual de Azure](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a>¿Cómo restablecer contraseña Hola para las máquinas virtuales en el conjunto de escalas de máquina virtual?

contraseña de hello tooreset para las máquinas virtuales en la escala de máquinas virtuales establecido, utiliza extensiones de acceso de máquina virtual. 

Usar hello siguiente ejemplo de PowerShell:

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
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a>¿Cómo se agrega un tooall de extensión máquinas virtuales en el conjunto de escalas de máquina virtual?

Si la directiva de actualización se establece demasiado**automática**, volver a implementar plantilla Hola con nuevas propiedades de extensión Hola actualiza todas las máquinas virtuales.

Si la directiva de actualización se establece demasiado**manual**, en primer lugar actualizar extensión hello y, a continuación, actualizar manualmente todas las instancias en las máquinas virtuales.

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a>¿Si las extensiones de hello asociadas a un conjunto de escala de máquinas virtuales existentes se actualizan, existentes máquinas virtuales afectadas? (Es decir, se Hola máquinas virtuales *no* modelo de conjunto de escala de máquina virtual de coincidencia Hola?) ¿O se ignoran? ¿Cuando una máquina existente se ha reparado el servicio o se restablece la imagen inicial, secuencias de comandos de Hola que están actualmente configurados en el conjunto de escalas de máquina virtual de hello ejecuta o son secuencias de comandos de Hola que se configuraron cuando se usa Hola que máquina virtual se creó por primera vez?

Si establece la definición de extensión de hello en escalas de máquina virtual de Hola se actualiza el modelo y propiedad de upgradePolicy de Hola se establece demasiado**automática**, actualiza hello las máquinas virtuales. Si la propiedad de hello upgradePolicy se establece demasiado**manual**, las extensiones se marcan como no coincide con el modelo de Hola. 

Si una máquina virtual existente se ha reparado el servicio, aparecerá como un reinicio y extensiones de hello no se vuelven a ejecutar. Si se está restableciendo la imagen inicial, es como sustituir el disco de SO Hola con la imagen de origen de Hola. Cualquier especialización hello más reciente del modelo de, como las extensiones, se ejecutan.
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a>¿Cómo se puede unirse a un dominio de tooan Azure AD del conjunto de escala de máquina virtual?

un dominio de Active Directory de Azure (Azure AD) de máquina virtual escala conjunto tooan toojoin, puede definir una extensión. 

toodefine una extensión, utilice la propiedad de JsonADDomainExtension de hello:

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
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a>Una extensión de conjunto de escala de máquina virtual está intentando tooinstall algo que requiere un reinicio. Por ejemplo, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"

Si la extensión de conjunto de escala de máquina virtual está intentando tooinstall algo que requiere un reinicio, puede usar la extensión de configuración de estado deseado de Azure automatización (automatización DSC) de Hola. Si el sistema operativo de hello es Windows Server 2012 R2, Azure extrae en la instalación de Windows Management Framework (WMF) 5.0 hello, reinicios y, a continuación, continúa con la configuración de Hola. 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a>¿Cómo activo el antimalware en el conjunto de escalado de máquinas virtuales?

conjunto de tooturn en antimalware en la escala de máquinas virtuales, use Hola siguiente ejemplo de PowerShell:

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

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a>Necesito tooexecute un script personalizado que se hospeda en una cuenta de almacenamiento privado. script de Hola se ejecuta correctamente cuando el almacenamiento hello es público, pero cuando intento toouse una firma de acceso compartido (SAS), se produce un error. Se muestra este mensaje: "Faltan los parámetros obligatorios para la firma de acceso compartido". Vínculo + SAS funciona bien desde mi explorador local.

tooexecute un script personalizado que se hospeda en una cuenta de almacenamiento privado, establecer la configuración protegidos con clave de cuenta de almacenamiento de Hola y el nombre. Para más información, consulte la sección sobre la [Extensión del script personalizado para Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).







## <a name="networking"></a>Redes
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a>¿Es posible tooassign establece una escala de tooa del grupo de seguridad de red (NSG), por lo que aplicará tooall Hola NIC de VM en el conjunto de hello?

Sí. Un grupo de seguridad de red se pueden aplicar directamente escala tooa establece haciendo referencia a ella en la sección de networkInterfaceConfigurations de Hola Hola de perfil de red. Ejemplo:

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

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a>¿Cómo realizar un intercambio de VIP para conjuntos de escalas de máquina virtual en hello misma suscripción y la misma región?

Si tiene dos virtual conjuntos de escalas de máquina con servidores front-end de equilibrador de carga de Azure y están en Hola misma suscripción y región, puede cancelar la asignación de direcciones IP públicas de Hola desde cada uno de ellos y asignar toohello otro. Consulte, por ejemplo, [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) (Intercambio de VIP: implementación Blue-green en Azure Resource Manager). Esto implica un retraso aunque como Hola recursos son asignado o desasignado Hola a nivel de red. Una opción más rápida es toouse puerta de enlace de aplicaciones de Azure con dos grupos de back-end y una regla de enrutamiento. También puede hospedar la aplicación con [Azure App Service](https://azure.microsoft.com/en-us/services/app-service/), que permite realizar un cambio rápido entre las ranuras de ensayo y las de producción.
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a>¿Cómo se puede especificar un intervalo de toouse de direcciones IP privada para estático asignación de direcciones IP privada?

Las direcciones IP se seleccionan de una subred que especifique. 

método de asignación de Hola de direcciones IP de conjunto de escala de máquinas virtuales siempre es "dinámico", pero eso no significa que pueden cambiar estas direcciones IP. En este caso, "dinámico" solo significa que no se especifican direcciones IP de hello en una solicitud PUT. Especifique Hola estático establece mediante el uso de la subred de Hola. 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a>¿Cómo se puede implementar una máquina virtual escala conjunto tooan existente red virtual de Azure? 

red virtual de Azure existente para la tooan de conjuntos de toodeploy una escala de máquinas virtuales, vea [implementar una máquina virtual escala conjunto tooan red virtual existente](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet). 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a>¿Cómo se puede agregar dirección IP de Hola de hello primera VM en una escala de máquinas virtuales establece toohello salida de una plantilla?

dirección IP de hello tooadd de hello primera VM en una salida de toohello del conjunto de escala de máquina virtual de una plantilla, consulte [ARM: IP privadas de obtener VMSS](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a>¿Puedo usar conjuntos de escalado con redes aceleradas?

Sí. toouse accelerated redes, configurar enableAcceleratedNetworking tootrue en la escala del conjunto de networkInterfaceConfigurations. Por ejemplo,
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

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a>¿Cómo se puede configurar servidores DNS de hello utilizados por un conjunto de escala?

toocreate conjunto de escalas de VM con una configuración personalizada de DNS, agregue la que sección de networkInterfaceConfigurations del conjunto de una escala de toohello dnsSettings paquetes JSON. Ejemplo:
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a>¿Cómo puedo configurar un tooassign de conjunto de escala una tooeach de dirección IP virtual pública?

toocreate conjunto de escalas de VM que asigna una tooeach de dirección IP virtual pública, asegúrese de versión de API de Hola de hello Microsoft.Compute/virtualMAchineScaleSets recursos es 2017-03-30 y agregar un _publicipaddressconfiguration_ paquete JSON sección de ipConfigurations del conjunto de escala de toohello. Ejemplo:

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a>¿Puedo configurar un toowork de conjunto de escala con varias puertas de enlace de aplicaciones?

Sí. Puede agregar Hola Id. de recurso para varios toohello de grupos de direcciones de back-end Application Gateway _applicationGatewayBackendAddressPools_ lista Hola _ipConfigurations_ sección de su conjunto de escala perfil de red.

## <a name="scale"></a>Escala

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a>¿En qué casos podría crear un conjunto de escalado de máquinas virtuales con menos de dos máquinas virtuales?

Una de las razones toocreate una escala de máquinas virtuales establece con menos de dos máquinas virtuales debería establecerse propiedades elástico de hello toouse de una escala de máquinas virtuales. Por ejemplo, podría implementar un conjunto de escalas de máquina virtual con cero toodefine de máquinas virtuales de la infraestructura sin pagar la máquina virtual que ejecuta los costos. A continuación, cuando esté listo toodeploy las máquinas virtuales, aumentar la capacidad"hello" de recuento de instancias producción de hello máquina virtual escala conjunto toohello.

Otra razón por la que podría crear un conjunto de escalado de máquinas virtuales con menos de dos máquinas virtuales es si le preocupa menos la disponibilidad que el uso de un conjunto de disponibilidad con máquinas virtuales discretas. Conjuntos de escalas de máquina virtual ofrecen una toowork de manera con unidades de proceso no diferenciados que son fungible. Esta uniformidad es un diferenciador clave entre los conjuntos de escalado de máquinas virtuales y los conjuntos de disponibilidad. Muchas cargas de trabajo sin estado no realizan seguimiento de unidades individuales. Si se quita la carga de trabajo de hello, puede reducir tooone unidad de proceso y, a continuación, escalar toomany cuando aumenta la carga de trabajo de Hola.

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a>¿Cómo se cambia el número de Hola de máquinas virtuales en un conjunto de escalas de máquina virtual?

número de hello toochange de máquinas virtuales en un conjunto de escalas de máquina virtual, consulte [cambiar el número de instancias de Hola de un conjunto de escalas de máquina virtual](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a>¿Cómo puedo definir alertas personalizadas para cuando se alcanzan determinados umbrales?

Dispone de cierta flexibilidad en la manera de controlar las alertas de umbrales especificados. Por ejemplo, puede definir webhooks personalizados. Hola webhook ejemplo siguiente es de una plantilla de administrador de recursos:

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

En este ejemplo, una alerta pasa a tooPagerduty.com cuando se alcanza un umbral.



## <a name="patching-and-operations"></a>Aplicación de revisiones y operaciones

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a>¿Cómo creo un conjunto de escalado en un grupo de recursos existente?

Crear conjuntos de escala en un recurso existente grupo no aún es posible desde Hola portal de Azure, pero puede especificar un grupo de recursos existente cuando la implementación de una escala establecido desde una plantilla de Azure Resource Manager. También puede especificar un grupo de recursos existente al crear un conjunto de escalado con Azure PowerShell o CLI.

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a>¿Podemos mover que una escala establece el grupo de recursos de tooanother?

Sí, puede mover escala conjunto recursos tooa nueva suscripción o grupo de recursos.

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a>¿Cómo actualizar tooI mi escala de máquinas virtuales establece tooa nueva imagen? ¿Cómo administro la aplicación de revisiones?

Consulte tooupdate la escala de máquinas virtuales establece tooa nueva imagen y aplicación de revisiones toomanage [actualizar un conjunto de escalas de máquina virtual](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a>¿Puedo usar tooreset de operación de restablecimiento de imagen inicial de hello una máquina virtual sin cambiar la imagen de hello? (Es decir, desea restablecer una VM toofactory configuración en lugar de la nueva imagen de tooa.)

Sí, puede usar tooreset de operación de restablecimiento de imagen inicial de hello una máquina virtual sin cambiar la imagen de Hola. Sin embargo, si establece la escala de la máquina virtual hace referencia una imagen de plataforma con `version = latest`, la máquina virtual puede actualizar tooa imagen del sistema operativo posterior cuando se llama a `reimage`.

Para más información, consulte el artículo sobre la [administración de todas las máquinas virtuales de un conjunto de escalado de máquinas virtuales](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).



## <a name="troubleshooting"></a>Solución de problemas

### <a name="how-do-i-turn-on-boot-diagnostics"></a>¿Cómo se activa el diagnóstico de arranque?

tooturn en el diagnóstico de arranque, en primer lugar, cree una cuenta de almacenamiento. A continuación, coloque este bloque de JSON en el conjunto de escalas de máquina virtual **virtualMachineProfile**y actualizar el conjunto de escalas de máquina virtual de hello:

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

Cuando se crea una nueva máquina virtual, Hola propiedad InstanceView de hello VM muestra los detalles de hello para la captura de pantalla de Hola y así sucesivamente. Este es un ejemplo:
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a>Propiedades de máquina virtual

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a>¿Cómo obtengo información de propiedades de cada máquina virtual sin tener que realizar varias llamadas? ¿Por ejemplo, cómo obtendría dominio de error de Hola para cada uno de hello 100 máquinas virtuales en el conjunto de escalas de máquina virtual?

información de la propiedad tooget para cada máquina virtual sin realizar varias llamadas, puede llamar a `ListVMInstanceViews` realizando una API de REST `GET` en hello siguiente URI de recurso:

/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a>¿Pasar argumentos de extensión distinto toodifferent las máquinas virtuales en un conjunto de escalas de máquina virtual?

No, no se puede pasar argumentos de extensión distinto toodifferent las máquinas virtuales en un conjunto de escalas de máquina virtual. Sin embargo, las extensiones pueden actuar en función de propiedades únicas de Hola de VM que se ejecutan en, por ejemplo, como en el nombre de la máquina de Hola Hola. Las extensiones también pueden consultar metadatos de la instancia en http://169.254.169.254 tooget obtener más información acerca de hello VM.

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a>¿Por qué hay huecos entre los nombres de máquina virtual de mi conjunto de escalado de máquinas virtuales y los identificadores de máquina virtual? Por ejemplo: 0, 1, 3...

Hay espacios entre los nombres de máquina virtual de máquina virtual escala conjunto y el Id. de VM porque la escala de máquinas virtuales configurada **sobreaprovisionamiento** propiedad se establece el valor predeterminado de toohello de **true**. Si en exceso se establece demasiado**true**, más máquinas virtuales que solicitado se crean. Las máquinas virtuales adicionales se eliminan a continuación. En este caso, obtener implementación mayor confiabilidad, pero a costa de Hola de nombres contiguo y traducción de direcciones de red (NAT) contiguos reglas. 

Puede establecer esta propiedad demasiado**false**. Para conjuntos de escalado de máquinas virtuales pequeños, esto no afecta significativamente a confiabilidad de la implementación.

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a>¿Cuál es la diferencia de hello entre eliminar una máquina virtual en un conjunto de escalas de máquina virtual y desasignar Hola VM? ¿Cuándo debo elegir uno sobre Hola otro?

Hello diferencia principal entre la eliminación de una máquina virtual en un conjunto de escalas de máquina virtual y desasignar Hola VM es que `deallocate` Hola los discos duros virtuales (VHD), no se elimina. Hay costos de almacenamiento asociados con la ejecución de `stop deallocate`. Puede usar uno u Hola Sí para uno de hello siguientes motivos:

- Desee toostop pagar costos de proceso, pero desea tookeep Hola disco estado del programa Hola a máquinas virtuales.
- Desea toostart un conjunto de máquinas virtuales más rápidamente de lo que puede escalar horizontalmente un conjunto de escalas de máquina virtual.
  - Escenario de toothis relacionados, podría haber creado su propio motor de escalado automático y quiere una escala to-end más rápida.
- Tiene un conjunto de escalado de máquinas virtuales que se distribuye de forma irregular a través de dominios de error o dominios de actualización. Esto puede ser porque eliminó de forma selectiva las máquinas virtuales, o porque se eliminaron las máquinas virtuales después proveer en exceso. Ejecuta `stop deallocate` seguido `start` en la máquina virtual de hello escala establecida de manera uniforme distribuye hello las máquinas virtuales a través de dominios de error o dominios de actualización.

