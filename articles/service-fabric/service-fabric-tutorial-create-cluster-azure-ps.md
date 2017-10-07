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
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a>Creación de un clúster seguro en Azure mediante PowerShell
Este tutorial muestra cómo toocreate un tejido de servicio de clúster (Windows o Linux) que se ejecute en Azure. Cuando haya terminado, tendrá un clúster que ejecuta en la nube de Hola que puede implementar las aplicaciones.

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Creación de un clúster de Service Fabric en Azure mediante PowerShell
> * Clúster de hello segura con un certificado X.509
> * Conectar el clúster toohello mediante PowerShell
> * Eliminación de un clúster

## <a name="prerequisites"></a>Requisitos previos
Antes de empezar este tutorial:
- Si no tiene ninguna suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- Instalar hello [módulo de PowerShell y el SDK del servicio de Fabric](service-fabric-get-started.md)
- Instalar hello [versión 4.1 o superior del módulo de Powershell de Azure](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)

Hola siguiendo el procedimiento crea una clúster de Service Fabric de vista previa de nodo único (un único equipo virtual). clúster de Hello está protegido por un certificado autofirmado que obtiene crea junto con el clúster de hello y, a continuación, se coloca en un almacén de claves. Clústeres de nodo único no se puede escalar más allá de una máquina virtual y clústeres de vista previa no pueden ser versiones toonewer actualizado.

costo toocalculate producido mediante la ejecución de un clúster de Service Fabric en Azure use hello [Calculadora de precios de Azure](https://azure.microsoft.com/pricing/calculator/).
Para más información sobre la creación de clústeres de Service Fabric, consulte el artículo [Creación de un clúster de Service Fabric con Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).

## <a name="create-hello-cluster-using-azure-powershell"></a>Crear clúster de hello mediante PowerShell de Azure
1. Descargar una copia local de la plantilla de Azure Resource Manager hello y archivo de parámetros de Hola de hello [plantilla del Administrador de recursos de Azure para Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) repositorio de GitHub.  *azuredeploy.JSON* es hello Azure Resource Manager plantilla que define un clúster de Service Fabric. *azuredeploy.Parameters.JSON* es un archivo de parámetros para la implementación de clúster de hello toocustomize.

2. Personalizar Hola parámetros Hola siguientes *azuredeploy.parameters.json* archivo de parámetros:

   | Parámetro       | Descripción | Valor sugerido |
   | --------------- | ----------- | --------------- |
   | clusterLocation | clúster de Hello región de Azure toowhich toodeploy Hola. | *Por ejemplo, westeurope, eastasia, eastus* |
   | clusterName     | Nombre del clúster de Hola que desea toocreate. | *Por ejemplo, bobs-sfpreviewcluster* |
   | adminUserName   | cuenta de administrador local de Hello en máquinas virtuales del clúster Hola. | *Cualquier nombre de usuario válido de Windows Server* |
   | adminPassword   | Contraseña de cuenta de administrador local de hello en máquinas virtuales del clúster Hola. | *Cualquier contraseña válida de Windows Server* |
   | clusterCodeVersion | Hola toorun de versión de Service Fabric. (255.255.X.255 son versiones preliminares). | **255.255.5718.255** |
   | vmInstanceCount | número de Hola de máquinas virtuales en el clúster (puede ser 1 o 3-99). | **1** | *Para un clúster de versión preliminar, especifique solo una máquina virtual*. |

3. Abra una consola de PowerShell, tooAzure de inicio de sesión y seleccione suscripción Hola que desea que toodeploy Hola clúster en:

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. Cree y cifrar una contraseña para hello certificado toobe utilizado por Service Fabric.

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. Crear clúster hello y su certificado ejecutando el siguiente comando de hello:

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
   >Hola `-CertificateSubjectName` parámetro debe alinearse con el parámetro de clusterName Hola especificado en el archivo de parámetros de hello, así como Hola dominio vinculado toohello región de Azure ha elegido, como: `clustername.eastus.cloudapp.azure.com`.

Una vez finalizada la configuración de hello, envía la información acerca de clúster de hello creado en Azure. También copia Hola certificado toohello - CertificateOutputFolder directorio del clúster especificado para este parámetro de ruta de acceso de Hola. Necesita esta tooaccess certificado Service Fabric Explorer y ver el estado del Hola del clúster.

Tome nota de la dirección URL de hello para el clúster, que puede ser similar toohello después de la dirección URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a>Modificar el certificado de Hola y tener acceso a Service Fabric Explorer ##

1. Haga doble clic en hello tooopen de certificado Hola Asistente para importación de certificados.

2. Utilizar la configuración predeterminada, pero que realmente Hola toocheck **marcar esta clave como exportable.** casilla de verificación, Hola **protección de clave privada** paso. Visual Studio necesita certificado de hello tooexport al configurar la autenticación de clúster de tejido de registro de contenedor de Azure tooService más adelante en este tutorial.

3. Ahora puede abrir Service Fabric Explorer en un explorador. toodo navegue por lo tanto, toohello **ManagementEndpoint** dirección URL para el clúster mediante un explorador web y un certificado de hello select que se guardó en su equipo.

>[!NOTE]
>Al abrir Service Fabric Explorer, verá un error de certificado, ya que está usando un certificado autofirmado. En el borde, tendrás que tooclick *detalles* y, a continuación, Hola *ir en la página Web toohello* vínculo. En Chrome, tendrá que tooclick *avanzadas* y, a continuación, Hola *continuar* vínculo.

>[!NOTE]
>Si se produce un error en la creación del clúster hello, siempre puede volver a ejecutar el comando hello, que actualiza los recursos de hello ya implementados. Si un certificado se creó como parte de la implementación de hello error, se genera uno nuevo. creación del clúster tootroubleshoot, consulte [crear un clúster de Service Fabric mediante Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).

## <a name="connect-toohello-secure-cluster"></a>Conectar el clúster segura toohello
Conectar con módulo de PowerShell de tejido de servicio de hello instalado con hello tejido SDK del servicio de clúster de toohello.  En primer lugar, instalar el certificado de hello en almacén de hello Personal del usuario actual de hello en el equipo.  Ejecute el siguiente comando de PowerShell de hello:

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

Ya estás listo tooconnect tooyour segura clúster.

Hola **Service Fabric** módulo de PowerShell proporciona muchos de los cmdlets para administrar clústeres, aplicaciones y servicios de Service Fabric.  Hola de uso [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) toohello de tooconnect cmdlet clúster segura. Hola huella digital del certificado y detalles del extremo de conexión se encuentran en la salida de hello en un paso anterior.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Compruebe que está conectado y clúster de hello es correcto usar hello [ServiceFabricClusterHealth Get](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a>Limpieza de recursos

Además propio recurso de clúster toohello, un clúster se compone de otros recursos de Azure. clúster de Hola de manera más sencilla de Hello toodelete y todos los recursos de Hola que consume es grupo de recursos de toodelete Hola.

Inicie sesión en tooAzure y seleccione Hola Id. de suscripción con el que desea que el clúster de Hola de tooremove.  Puede encontrar el identificador de suscripción, inicie sesión toohello [portal de Azure](http://portal.azure.com). Eliminar el grupo de recursos de Hola y todos los recursos de clúster de hello con hello [cmdlet Remove-AzureRMResourceGroup](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha aprendido cómo:

> [!div class="checklist"]
> * Creación de un clúster de Service Fabric en Azure
> * Clúster de hello segura con un certificado X.509
> * Conectar el clúster toohello mediante PowerShell
> * Eliminación de un clúster

A continuación, avanzar toohello después toolearn tutorial cómo toodeploy una aplicación existente.
> [!div class="nextstepaction"]
> [Implementación de una aplicación .NET con Docker Compose](service-fabric-host-app-in-a-container.md)
