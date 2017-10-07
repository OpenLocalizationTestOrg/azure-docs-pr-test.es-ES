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
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a>Creación de un clúster de Service Fabric con Azure Resource Manager
> [!div class="op_single_selector"]
> * [Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
> * [Portal de Azure](service-fabric-cluster-creation-via-portal.md)
>
>

Esta guía paso a paso le lleva por la configuración de un clúster seguro de Azure Service Fabric en Azure con Azure Resource Manager. Sabemos que dicho artículo hello es largo. No obstante, a menos que ya estén familiarizadas con contenido de hello, ser toofollow seguro de cada paso con cuidado.

Guía de Hello abarca Hola procedimientos siguientes:

* Cómo configurar un certificados tooupload de almacén de claves de Azure para la seguridad de clúster y la aplicación
* Creación de un clúster protegido en Azure con Azure Resource Manager
* Autenticación de usuarios con Azure Active Directory (Azure AD) para la administración del clúster

Un clúster seguro es un clúster que evite las operaciones de toomanagement de acceso no autorizado. Esto incluye implementar, actualizar y eliminar aplicaciones, servicios y datos de Hola que contienen. Un clúster es un clúster que cualquiera puede conectarse tooat en cualquier momento y realizar operaciones de administración. Aunque es posible toocreate un clúster no seguro, se recomienda que cree un clúster seguro desde el principio de Hola. Los clústeres no seguros no se pueden proteger en un momento posterior, por lo que se debe crear uno nuevo.

concepto de Hola de creación de clústeres seguros se Hola mismo, independientemente de si están clústeres de Linux o Windows. Para más información y scripts auxiliares para crear clústeres seguros de Linux, consulte [Creating secure clusters on Linux](#secure-linux-clusters) (Creación de clústeres seguros en Linux).

## <a name="sign-in-tooyour-azure-account"></a>Inicie sesión en tooyour cuenta de Azure
En esta guía se usa [Azure PowerShell][azure-powershell]. Cuando se inicia una nueva sesión de PowerShell, inicie sesión en tooyour cuenta de Azure y seleccione su suscripción antes de ejecutar comandos de Azure.

Inicie sesión en tooyour cuenta de Azure:

```powershell
Login-AzureRmAccount
```

Seleccione su suscripción:

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a>Configuración de un almacén de claves
En esta sección se habla de la creación de un almacén de claves para un clúster de Service Fabric en Azure y aplicaciones de Service Fabric. Para un almacén de claves de guía completa tooAzure, consulte toohello [el almacén de claves Guía de introducción][key-vault-get-started].

Service Fabric utiliza certificados X.509 toosecure un clúster y proporcionar características de seguridad de la aplicación. Se utilizan certificados de toomanage de almacén de claves para los clústeres de Service Fabric en Azure. Cuando se implementa un clúster de Azure, proveedor de recursos de Azure de Hola que es responsable de la creación de clústeres de Service Fabric extrae los certificados de almacén de claves y los instala en clúster de hello las máquinas virtuales.

Hello siguiente diagrama ilustra Hola relación entre el almacén de claves de Azure, un clúster de Service Fabric y el proveedor de recursos de Azure de Hola que utiliza certificados almacenados en un almacén de claves cuando crea un clúster:

![Diagrama de instalación del certificado][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>Crear un grupo de recursos
Hola primer paso es toocreate un grupo de recursos específicamente para el almacén de claves. Se recomienda que coloque el almacén de claves de hello en su propio grupo de recursos. Esta acción le permite quitar Hola cálculo y almacenamiento de grupos de recursos, incluido el grupo de recursos de Hola que contiene el clúster de Service Fabric, sin perder sus claves y secretos. grupo de recursos de Hola que contiene el almacén de claves _debe estar en hello misma región_ como clúster de Hola que lo está usando.

Si tiene previsto toodeploy clústeres en varias regiones, sugerimos que nombre de grupo de recursos de Hola y el almacén de claves de Hola de manera que indica qué región al que pertenece.  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
salida de Hello debería tener este aspecto:

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a>Crear un almacén de claves en el nuevo grupo de recursos Hola
almacén de claves de Hello _debe estar habilitada para la implementación_ tooallow Hola proceso recursos proveedor tooget certificados de él y lo instala en instancias de máquina virtual:

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

salida de Hello debería tener este aspecto:

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

## <a name="use-an-existing-key-vault"></a>Uso de un almacén de claves existente

toouse un almacén de claves existente, se _debe habilitarla para la implementación_ tooallow Hola proceso recursos proveedor tooget certificados de él y lo instala en nodos de clúster:

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a>Agregar el almacén de claves de certificados tooyour

Los certificados se utilizan en toosecure de autenticación y cifrado de Service Fabric tooprovide diversos aspectos de un clúster y sus aplicaciones. Para obtener más información sobre el modo en que se usan los certificados en Service Fabric, consulte los [Escenarios de seguridad de los clústeres de Service Fabric][service-fabric-cluster-security].

### <a name="cluster-and-server-certificate-required"></a>Certificado de clúster y servidor (obligatorio)
Este certificado es necesario toosecure un clúster y evitar tooit de acceso no autorizado. Ofrece seguridad al clúster de dos maneras:

* Autenticación del clúster: se autentica la comunicación de nodo a nodo para la federación del clúster. Sólo los nodos que se pueden demostrar su identidad con este certificado pueden unirse a clústeres de Hola.
* Autenticación de servidor: autentica el cliente de administración de la tooa de los puntos de conexión de administración con hello clúster, por lo que hello administración cliente sabe está hablando clúster real toohello. Este certificado también proporciona un SSL para hello API de administración de HTTPS y para Service Fabric Explorer a través de HTTPS.

tooserve estos fines, certificado Hola debe cumplir Hola según los requisitos:

* certificado de Hello debe contener una clave privada.
* certificado de Hello debe crearse para el intercambio de claves, que es exportable tooa archivo de intercambio de información Personal (.pfx).
* nombre de sujeto del certificado de Hello debe coincidir con dominio Hola que usar clúster de Service Fabric tooaccess Hola. La coincidencia distingue tooprovide requiere SSL para extremos de administración del clúster de hello HTTPS y el Explorador de Service Fabric. No se puede obtener un certificado SSL de una entidad de certificación (CA) para hello. cloudapp.azure.com dominio. Debe adquirir un nombre de dominio personalizado para el clúster. Cuando solicite un certificado de una entidad de certificación, hello nombre de sujeto del certificado debe coincidir con nombre de dominio personalizado de Hola que usa para el clúster.

### <a name="application-certificates-optional"></a>Certificados de aplicación (opcionales)
Se puede instalar un número cualquiera de certificados adicionales en un clúster para proteger la aplicación. Antes de crear el clúster, considere la posibilidad de escenarios de seguridad de aplicación Hola que requieren un toobe de certificados instalado en nodos de hello, como:

* Cifrado y descifrado de los valores de configuración de aplicación.
* Cifrado de datos entre nodos durante la replicación.

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Formato de certificados para el uso del proveedor de recursos de Azure
Puede agregar y usar archivos de claves privadas (.pfx) directamente a través del almacén de claves. Sin embargo, el proveedor de recursos de proceso de Azure de hello requiere toobe de claves que se almacenan en formato JavaScript Object Notation (JSON) especial. formato de Hello incluye archivo .pfx de hello como una cadena de cifrado de base64 base y la contraseña de clave privada de Hola. tooaccommodate del almacén de estos requisitos, Hola claves deben colocarse en una cadena JSON y, a continuación, se almacenan como "secretos" en la clave de Hola.

toomake este proceso, un [módulo de PowerShell está disponible en GitHub][service-fabric-rp-helpers]. módulo de hello toouse, Hola siguientes:

1. Descargar contenido completo de hello del repositorio de hello en un directorio local.
2. Vaya toohello directorio local.
2. Importar el módulo de ServiceFabricRPHelpers de hello en la ventana de PowerShell:

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

Hola `Invoke-AddCertToKeyVault` comandos en este módulo de PowerShell da formato a una clave privada del certificado en una cadena JSON y lo carga en el almacén de claves toohello automáticamente. Usar certificado de clúster de hello comando tooadd hello y cualquier aplicación adicional certificados toohello el almacén de claves. Repita este paso para todos los certificados adicionales que desee tooinstall en el clúster.

#### <a name="uploading-an-existing-certificate"></a>Carga de un certificado existente

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

Si se produce un error, como Hola se muestra aquí, normalmente significa que tiene un conflicto de dirección URL del recurso. conflicto de hello tooresolve, cambiar el nombre de almacén de claves de Hola.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Después de que se resuelve el conflicto de hello, resultado de hello debería tener este aspecto:

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
>Necesita Hola tres anterior cadenas, CertificateThumbprint, SourceVault y CertificateURL, tooset un clúster de Service Fabric segura y tooobtain todos los certificados de aplicación puede que esté usando para la seguridad de la aplicación. Si no guarda las cadenas de hello, puede ser difícil tooretrieve ellos consultando clave Hola del almacén de versiones posteriores.

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a>Crear un certificado autofirmado y cargarlo en el almacén de claves toohello

Si ya ha cargado el almacén de claves de certificados toohello, omita este paso. Este paso es para generar un nuevo certificado autofirmado y cargarlo en el almacén de claves tooyour. Después de cambiar los parámetros de hello en la siguiente secuencia de comandos de Hola y, a continuación, ejecutarlo, debe ser solicitará una contraseña de certificado.  

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

Si se produce un error, como Hola se muestra aquí, normalmente significa que tiene un conflicto de dirección URL del recurso. conflicto de hello tooresolve, cambiar el nombre de almacén de claves de hello, nombre RG y así sucesivamente.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Después de que se resuelve el conflicto de hello, resultado de hello debería tener este aspecto:

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
>Necesita Hola tres anterior cadenas, CertificateThumbprint, SourceVault y CertificateURL, tooset un clúster de Service Fabric segura y tooobtain todos los certificados de aplicación puede que esté usando para la seguridad de la aplicación. Si no guarda las cadenas de hello, puede ser difícil tooretrieve ellos consultando clave Hola del almacén de versiones posteriores.

 En este punto, debe tener Hola siguientes elementos en su lugar:

* grupo de recursos del almacén de claves de Hola.
* Hola almacén de claves y su dirección URL (denominado SourceVault en hello anterior a la salida de PowerShell).
* certificado de autenticación de servidor de clúster de Hola y su dirección URL en el almacén de claves de Hola.
* certificados de la aplicación Hello y sus direcciones URL en el almacén de claves de Hola.


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a>Configuración de Azure Active Directory para la autenticación de cliente

Azure AD ofrece tooapplications de acceso de usuario de toomanage organizaciones (conocido como inquilinos). Las aplicaciones se dividen en las que tienen interfaz de usuario de inicio de sesión basada en web y las que tienen una experiencia de cliente nativa. En este artículo se supone que ya ha creado un inquilino. Si no fue así, empiece por leer [cómo inquilino de Azure Active Directory tooget][active-directory-howto-tenant].

Un clúster de Service Fabric ofrece tooits de puntos de entrada varias funciones de administración, incluidos Hola basada en web [Service Fabric Explorer] [ service-fabric-visualizing-your-cluster] y [Visual Studio] [service-fabric-manage-application-in-visual-studio]. Como resultado, crea dos Azure AD aplicaciones toocontrol acceso toohello clúster, una aplicación web y una aplicación nativa.

toosimplify algunos de los pasos de hello implicados en la configuración de Azure AD con un clúster de Service Fabric, hemos creado un conjunto de scripts de Windows PowerShell.

> [!NOTE]
> Debe completar Hola siguiendo los pasos antes de crear el clúster de Hola. Dado que las secuencias de comandos de hello espera que los puntos de conexión y nombres de los clústeres, los valores de hello debe planearse y no los valores que ya ha creado.

1. [Descargar los scripts de hello] [ sf-aad-ps-script-download] tooyour equipo.
2. Menú contextual Hola archivo zip del, seleccione **propiedades**, seleccione hello **Unblock** casilla de verificación y, a continuación, haga clic en **aplicar**.
3. Extraiga el archivo zip de Hola.
4. Ejecutar `SetupApplications.ps1`y proporcionar hello TenantId, nombre del clúster y WebApplicationReplyUrl como parámetros. Por ejemplo:

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    Puede encontrar el TenantId mediante la ejecución de comandos de PowerShell de hello `Get-AzureSubscription`. Al ejecutar este comando muestra hello TenantId para cada suscripción.

    Nombre del clúster es las aplicaciones de hello Azure AD tooprefix usado creados por el script de Hola. No es necesario el nombre del clúster real de toomatch Hola exactamente. Está previsto toomake solo lo más fácil toomap Azure AD artefactos toohello Service Fabric clúster que se utilizan con.

    WebApplicationReplyUrl es el punto de conexión predeterminado de Hola que Azure AD devuelve tooyour a los usuarios después de que terminen de inicio de sesión. Establezca este extremo como extremo de Service Fabric Explorer hello para el clúster, cuyo valor predeterminado es:

    https://&lt;cluster_domain&gt;:19080/Explorer

    Son toosign solicitada en tooan cuenta que tenga privilegios administrativos para el inquilino de hello Azure AD. Después de iniciar la sesión, script de Hola crea hello web y aplicaciones nativas toorepresent su clúster de Service Fabric. Si se examinan las aplicaciones del inquilino de Hola Hola [portal de Azure clásico][azure-classic-portal], debería ver dos entradas nuevas:

   * *ClusterName*\_Clúster
   * *ClusterName*\_Cliente

   script de Hola imprime Hola JSON requiere hello Azure Resource Manager plantilla al crear el clúster de hello en la siguiente sección hello, por lo que es una ventana de PowerShell de buena idea tookeep Hola abrir.

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a>Creación de una plantilla de Resource Manager para el clúster de Service Fabric
En esta sección, Hola da como resultado de hello anterior se usan comandos de PowerShell en una plantilla de administrador de recursos de clúster de Service Fabric.

Plantillas de administrador de recursos de ejemplo están disponibles en hello [Galería de plantillas de inicio rápido de Azure en GitHub][azure-quickstart-templates]. Estas plantillas se pueden usar como punto de partida para crear la plantilla de clúster.

### <a name="create-hello-resource-manager-template"></a>Crear plantilla de administrador de recursos de Hola
Esta guía usan hello [5 nodos clúster segura] [ service-fabric-secure-cluster-5-node-1-nodetype] plantilla de ejemplo y los parámetros de plantilla. Descargar `azuredeploy.json` y `azuredeploy.parameters.json` tooyour equipo y abra ambos archivos en el editor de texto que prefiera.

### <a name="add-certificates"></a>Adición de certificados
Agregar plantilla de administrador de recursos de clúster de certificados tooa haciendo referencia a almacén de claves de Hola que contiene las claves de certificado de Hola. Se recomienda colocar los valores del almacén de claves de hello en un archivo de parámetros de plantilla de administrador de recursos. Si lo hace, mantiene Hola, Administrador de recursos del archivo de plantilla reutilizable y libre de implementación de tooa específico de valores.

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a>Agregar que conjuntos de escalas de máquina virtual de todos los certificados toohello osProfile
Todos los certificados que se instala en el clúster de hello deben configurarse en la sección de osProfile de Hola de recurso de conjunto de escala de hello (Microsoft.Compute/virtualMachineScaleSets). Esta acción indica al certificado del proveedor tooinstall Hola de hello recursos en hello las máquinas virtuales. Esta instalación incluye el certificado de clúster de Hola y los certificados de seguridad de aplicación que planea toouse para las aplicaciones:

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

#### <a name="configure-hello-service-fabric-cluster-certificate"></a>Configurar certificado de clúster de Service Fabric Hola
certificado de autenticación del clúster de Hola debe configurarse en ambos recurso de clúster de Service Fabric (Microsoft.ServiceFabric/clusters) de Hola y Hola extensión Service Fabric para escalas de máquina virtual se establece en el recurso de conjunto de escala de máquina virtual de Hola. Esta disposición permite tooconfigure de proveedor de recursos de Service Fabric hello, para su uso para la autenticación de clúster y autenticación de servidor para los puntos de conexión de administración.

##### <a name="virtual-machine-scale-set-resource"></a>Recurso de conjunto de escalado de máquinas virtuales:
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

##### <a name="service-fabric-resource"></a>Recurso de Service Fabric:
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

### <a name="insert-azure-ad-configuration"></a>Inserción de la configuración de Azure AD
configuración de Hello Azure AD que creó anteriormente se puede insertar directamente en la plantilla de administrador de recursos. Sin embargo, se recomienda que primero extraer valores de hello en parámetros archivo tookeep Hola Administrador de recursos plantilla reutilizable y sin necesidad de implementación de tooa específico de valores.

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

### <a "configure-arm" ></a>Configuración de los parámetros de plantilla de Resource Manager
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
Por último, utilice valores de salida de hello del almacén de claves de Hola y el archivo de parámetros de Hola de toopopulate de comandos de PowerShell de Azure AD:

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
En este punto, debe tener Hola siguientes elementos en su lugar:

* Grupo de recursos del almacén de claves
  * Almacén de claves
  * Certificado de autenticación de servidor de clúster
  * Certificado de cifrado de datos
* Inquilino de Azure Active Directory
  * Aplicación de Azure AD para la administración basada en web y Service Fabric Explorer
  * Aplicación de Azure AD para la administración de cliente nativo
  * Usuarios y roles asignados
* Plantilla de Resource Manager para el clúster de Service Fabric
  * Certificados configurados mediante el almacén de claves
  * Azure Active Directory configurado

Hola siguiente diagrama ilustra cómo encajan las el almacén de claves y la configuración de Azure AD en la plantilla de administrador de recursos.

![Asignación de dependencias de Resource Manager][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a>Crear clúster Hola
Ya estás listo toocreate clúster de hello mediante el uso de [implementación de plantilla de recursos de Azure][resource-group-template-deploy].

#### <a name="test-it"></a>Pruébelo.
Utilice Hola después tootest de comandos de PowerShell la plantilla de administrador de recursos con un archivo de parámetros:

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a>Impleméntelo.
Si pasa la prueba de la plantilla de hello Administrador de recursos, utilice Hola después toodeploy de comandos de PowerShell la plantilla de administrador de recursos con un archivo de parámetros:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a>Asignar usuarios tooroles
Después de haber creado Hola aplicaciones toorepresent el clúster, asignar los usuarios roles toohello compatibles con Service Fabric: solo lectura y administrador. Puede asignar roles de hello mediante hello [portal de Azure clásico][azure-classic-portal].

1. Hola portal de Azure, vaya tooyour inquilino y, a continuación, seleccione **aplicaciones**.
2. Seleccione la aplicación web de hello, que tiene un nombre como `myTestCluster_Cluster`.
3. Haga clic en hello **usuarios** ficha.
4. Seleccione un tooassign de usuario y, a continuación, haga clic en hello **asignar** situado en la parte inferior de Hola de pantalla de bienvenida.

    ![Los usuarios tooroles botón asignar][assign-users-to-roles-button]
5. Seleccione Hola rol tooassign toohello usuario.

    ![Cuadro de diálogo "Asignar usuarios"][assign-users-to-roles-dialog]

> [!NOTE]
> Para más información sobre los roles de Service Fabric, consulte [Control de acceso basado en roles para clientes de Service Fabric](service-fabric-cluster-security-roles.md).
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a>Creación de clústeres seguros en Linux
proceso de hello toomake más fácil, hemos proporcionado un [script auxiliar](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux). Antes de usar este script auxiliar, asegúrese de que ya tiene la interfaz de la línea de comandos (CLI) de Azure instalada y se encuentra en la ruta de acceso. Asegúrese de que script de Hola tiene permisos tooexecute ejecutando `chmod +x cert_helper.py` después de descargarlo. Hola primer paso es toosign en tooyour cuenta de Azure mediante CLI con hello `azure login` comando. Tras iniciar sesión en tooyour cuenta de Azure, use Hola auxiliar script con la entidad de certificación firmó el certificado, como Hola después del comando mostrará:

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

parámetro - ifile de Hello puede tomar un archivo .pfx o un archivo PEM como entrada, con un tipo de certificado de hello (pfx o pem o ss si es un certificado autofirmado).
parámetro -h de Hello imprime texto de Ayuda de Hola.


Este comando devuelve Hola después de tres cadenas como salida de hello:

* SourceVaultID, que es el Id. de Hola para hello nueva KeyVault ResourceGroup crea automáticamente
* CertificateUrl para tener acceso a certificados de Hola
* CertificateThumbprint, que se utiliza para la autenticación

Hola de ejemplo siguiente muestra cómo toouse Hola comando:

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
Ejecutar Hola anterior proporciona comandos Hola tres cadenas como sigue:

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

nombre de sujeto del certificado de Hello debe coincidir con dominio Hola que usar clúster de Service Fabric tooaccess Hola. Esta coincidencia es tooprovide requiere SSL para extremos de administración del clúster de hello HTTPS y el Explorador de Service Fabric. No se puede obtener un certificado SSL de una entidad de certificación para hello `.cloudapp.azure.com` dominio. Debe adquirir un nombre de dominio personalizado para el clúster. Cuando solicite un certificado de una entidad de certificación, hello nombre de sujeto del certificado debe coincidir con nombre de dominio personalizado de Hola que usa para el clúster.

Estos nombres de asunto son entradas de hello necesita toocreate un clúster de Service Fabric segura (sin Azure AD), como se describe en [parámetros de plantilla de configurar el Administrador de recursos](#configure-arm). Puede conectarse toohello segura clúster siguiendo las instrucciones de Hola de [clúster de tooa de acceso de cliente de autenticación](service-fabric-connect-to-secure-cluster.md). Los clústeres de versión preliminar de Linux no admiten la autenticación de Azure AD. Puede asignar roles de administrador y cliente tal y como se describe en hello [asignar roles toousers](#assign-roles) sección. Al especificar los roles de administrador y cliente para un clúster de vista previa de Linux, deberá tooprovide huellas digitales de certificado para la autenticación. (No proporciona nombre del asunto Hola, porque no hay validación de la cadena o la revocación se realiza en esta versión preliminar.)

Si desea toouse un certificado autofirmado para pruebas, puede usar Hola mismo toogenerate script uno. A continuación, puede cargar el almacén de claves tooyour Hola certificado proporcionando marca hello `ss` en lugar de proporcionar el nombre de la ruta de acceso y el certificado del certificado de Hola. Por ejemplo, vea el siguiente comando para crear y cargar un certificado autofirmado de hello:

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
Este comando devuelve Hola mismas tres cadenas: SourceVault, CertificateUrl y CertificateThumbprint. A continuación, puede usar Hola cadenas toocreate un clúster de Linux segura y una ubicación donde se coloca el certificado autofirmado de Hola. Necesita tooconnect toohello clúster de hello certificado autofirmado. Puede conectarse toohello segura clúster siguiendo las instrucciones de Hola de [clúster de tooa de acceso de cliente de autenticación](service-fabric-connect-to-secure-cluster.md).

nombre de sujeto del certificado de Hello debe coincidir con dominio Hola que usar clúster de Service Fabric tooaccess Hola. Esta coincidencia es tooprovide requiere SSL para extremos de administración del clúster de hello HTTPS y el Explorador de Service Fabric. No se puede obtener un certificado SSL de una entidad de certificación para hello `.cloudapp.azure.com` dominio. Debe adquirir un nombre de dominio personalizado para el clúster. Cuando solicite un certificado de una entidad de certificación, hello nombre de sujeto del certificado debe coincidir con nombre de dominio personalizado de Hola que usa para el clúster.

Puede rellenar parámetros Hola desde un script de aplicación auxiliar de Hola Hola portal de Azure, como se describe en hello [crear un clúster en el portal de Azure hello](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) sección.

## <a name="next-steps"></a>Pasos siguientes
En este punto, tiene un clúster seguro con autenticación de Azure Active Directory que proporciona autenticación de administración. Después, [conectar clúster tooyour](service-fabric-connect-to-secure-cluster.md) y obtenga información acerca de cómo demasiado[administrar secretos de aplicación](service-fabric-application-secret-management.md).

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a>Solución de problemas de configuración de Azure Active Directory para la autenticación de cliente
Si surge un problema mientras se está configurando Azure AD para la autenticación de cliente, revise las posibles soluciones de hello en esta sección.

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a>Explorador de Service Fabric solicita tooselect un certificado
#### <a name="problem"></a>Problema
Después de iniciar sesión en correctamente tooAzure AD en el Explorador de Service Fabric, explorador Hola devuelve una página de inicio de toohello pero un mensaje le pedirá tooselect un certificado.

![Cuadro de diálogo de selección de certificado de SFX][sfx-select-certificate-dialog]

#### <a name="reason"></a>Motivo
usuario de Hello no está asignado a un rol en hello aplicación de clúster de Azure AD. Por tanto, se produce un error en la autenticación de Azure AD en el clúster de Service Fabric. Explorador de Service Fabric vuelve toocertificate autenticación.

#### <a name="solution"></a>Solución
Siga las instrucciones de Hola para configurar Azure AD y asignar roles de usuario. Además, se recomienda activar "Aplicación de tooaccess necesarios de asignación de usuario", como `SetupApplications.ps1` does.

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a>Se produce un error en la conexión con PowerShell con un error: "¡hello especificado credenciales no son válidas"
#### <a name="problem"></a>Problema
Cuando se usa PowerShell tooconnect toohello clúster mediante el modo de seguridad de "AzureActiveDirectory", después de iniciar sesión en correctamente tooAzure AD, conexión Hola produce un error: "¡hello especifica credenciales no son válidas."

#### <a name="solution"></a>Solución
Esta solución es hello que igual Hola anteriores.

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a>Service Fabric Explorer devuelve un error al iniciar sesión: "AADSTS50011"
#### <a name="problem"></a>Problema
Cuando intente toosign en tooAzure AD en el Explorador de Service Fabric, página de Hola que devuelva un error: "AADSTS50011: Hola dirección de respuesta &lt;url&gt; no coincide con direcciones de respuesta de hello configuradas para la aplicación hello: &lt;guid&gt;."

![La dirección de respuesta SFX no coincide][sfx-reply-address-not-match]

#### <a name="reason"></a>Motivo
aplicación de clúster (web) de Hola que representa el Explorador de Service Fabric trata tooauthenticate en Azure AD y, como parte de la solicitud de hello proporciona Hola de dirección URL de redireccionamiento de retorno. Pero la dirección URL de hello no aparece en la aplicación hello Azure AD **dirección URL de respuesta** lista.

#### <a name="solution"></a>Solución
En hello **configurar** ficha de hello aplicación (web) de clúster, agregue Hola dirección URL del explorador de Service Fabric toohello **dirección URL de respuesta** lista o reemplazar uno de los elementos de hello en lista de Hola. Cuando haya terminado, guarde los cambios.

![Dirección URL de respuesta de la aplicación web][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a>Conecta el clúster de hello mediante la autenticación de Azure AD a través de PowerShell
Hola tooconnect clúster de Service Fabric, utilice Hola siguiente ejemplo de comando de PowerShell:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

toolearn sobre cmdlet Connect-ServiceFabricCluster hello, consulte [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a>¿Puedo volver a usar a inquilino Hola misma instancia de Azure AD en varios clústeres?
Sí. Pero recuerde que aplicación de clúster (web) de tooyour de tooadd hello dirección URL del explorador de Service Fabric. De lo contrario, Service Fabric Explorer no funciona.

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a>¿Por qué todavía necesito el certificado de servidor con Azure AD habilitado?
FabricClient y FabricGateway realizan una autenticación mutua. Durante la autenticación de Azure AD, integración de Azure AD proporciona a un cliente de servidor de toohello de identidad y certificado de servidor de hello es la identidad del servidor hello tooverify usado. Para más información sobre cómo funciona el certificado en Service Fabric, consulte [Certificados X.509 y Service Fabric][x509-certificates-and-service-fabric].

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

