---
title: "aaaUpgrade una independiente Azure Service Fabric de clúster en Windows Server | Documentos de Microsoft"
description: "Actualizar código de hello Azure Service Fabric o configuración que se ejecuta un clúster de Service Fabric independientes, incluida la configuración de modo de actualización de clúster de Hola."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 5132795e544b6f0185accedbf5092dcaafd66df0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a>Actualización del clúster de Azure Service Fabric independiente en Windows Server
> [!div class="op_single_selector"]
> * [Clúster de Azure](service-fabric-cluster-upgrade.md)
> * [Clúster independiente](service-fabric-cluster-upgrade-windows-server.md)
>
>

Para cualquier sistema moderna, Hola capacidad tooupgrade es un éxito a largo plazo toohello clave del producto. Un clúster de Azure Service Fabric es un recurso que usted posee. Este artículo describe cómo puede asegurarse de que ese clúster Hola siempre ejecuta en las versiones compatibles de código de Fabric de servicio y las configuraciones.

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a>Versión de Service Fabric Hola de control que se ejecuta en el clúster
tooset actualiza su toodownload de clúster de Service Fabric cuando Microsoft publica una nueva versión, conjunto hello **fabricClusterAutoupgradeEnabled** tootrue de configuración de clúster. una versión compatible de Service Fabric que desea que su toobe de clúster en conjunto hello tooselect **fabricClusterAutoupgradeEnabled** toofalse de configuración de clúster.

> [!NOTE]
> Asegúrese de que el clúster siempre ejecuta una versión compatible de Service Fabric. Cuando Microsoft anuncia el lanzamiento de Hola de una nueva versión de Service Fabric, versión anterior de hello está marcado para la finalización del soporte después de un mínimo de 60 días desde la fecha de Hola de anuncio Hola. Nuevas versiones se anuncian [en el blog del equipo de Service Fabric hello](https://blogs.msdn.microsoft.com/azureservicefabric/). nueva versión de Hello es toochoose disponible en ese momento.
>
>

Puede actualizar la nueva versión del clúster toohello solo si está usando una configuración de nodo de estilo de producción, donde cada nodo de Service Fabric está asignada a una máquina virtual o física independiente. Si tiene un clúster de desarrollo, donde más de un nodo de Service Fabric está en una única máquina física o virtual, deberá crear de nuevo clúster Hola con la nueva versión de hello.

Dos flujos de trabajo distintos pueden actualizar la versión más reciente de toohello de clúster o una versión compatible de Service Fabric. Un flujo de trabajo es para los clústeres que tienen la versión más reciente de conectividad toodownload Hola automáticamente. Hola otro flujo de trabajo es para los clústeres que no tiene la versión más reciente de Service Fabric de conectividad toodownload Hola.

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a>Actualizar clústeres que tienen la configuración y el código más reciente de conectividad toodownload Hola
Use estos pasos tooupgrade su tooa admitida la versión de clúster si los nodos del clúster tienen conectividad a Internet demasiado[http://download.microsoft.com](http://download.microsoft.com).

Para los clústeres que tienen conectividad también[http://download.microsoft.com](http://download.microsoft.com), Microsoft comprueba periódicamente la disponibilidad de Hola de nuevas versiones de Service Fabric.

Cuando hay disponible una nueva versión de Service Fabric, paquetes de saludo se descargan localmente toohello clúster y aprovisionado para la actualización. Además, cliente de hello tooinform de esta nueva versión, sistema de hello muestra una advertencia de estado de clúster explícito que sea similar toohello después de:

"Hola actual clúster versión # compatibilidad con la versión finaliza [Date]."

Después de clúster de Hola se ejecuta la versión más reciente de hello, advertencia Hola desaparece.

#### <a name="cluster-upgrade-workflow"></a>Flujo de trabajo de actualización de clúster
Una vez que aparezca la advertencia de estado del clúster de hello, Hola siguientes:

1. Conectar toohello clúster desde cualquier equipo que tenga equipos Hola de tooall de acceso de administrador que se muestran como nodos de clúster de Hola. máquina de Hola que este script se ejecuta en no tiene toobe parte del clúster de Hola.

    ```powershell

    ###### connect toohello secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. Obtener lista de Hola de versiones Service Fabric que puede actualizar a.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    Debería obtener un toothis similar de salida:

    ![obtener versiones de tejido][getfabversions]
3. Iniciar una versión disponible del tooan de actualización de clúster mediante el [ServiceFabricClusterUpgrade inicio](https://msdn.microsoft.com/library/mt125872.aspx) cmd de PowerShell.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   progreso de hello toomonitor de actualización de hello, puede utilizar Service Fabric Explorer o ejecución hello siguiente comando de Windows PowerShell.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Si no se cumplen las directivas de mantenimiento de clúster de hello, Hola actualización se ha revertido. las directivas de mantenimiento personalizado de toospecify para hello **inicio ServiceFabricClusterUpgrade** command, consulte la documentación de [ServiceFabricClusterUpgrade inicio](https://msdn.microsoft.com/library/mt125872.aspx).

Después de corregir los problemas de Hola que dan como resultado de reversión de hello, Iniciar actualización de hello nuevo por siguiente Hola mismos pasos como se describen anteriormente.

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a>Actualizar clústeres que tienen <U>sin conectividad</u> código más reciente de toodownload hello y configuración
Use estos pasos tooupgrade su tooa admitida la versión de clúster si los nodos del clúster no tiene conectividad a Internet demasiado[http://download.microsoft.com](http://download.microsoft.com).

> [!NOTE]
> Si está ejecutando un clúster que no esté conectado toohello Internet, tendrá toolearn toomonitor Hola Service Fabric team blog sobre una nueva versión. Hola sistema sin mostrar un tooalert de advertencia de estado de clúster de una nueva versión.  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a>Aprovisionamiento automático frente a aprovisionamiento manual
tooenable la descarga automática y el registro de versión de código más reciente de hello, configure el servicio de actualización de servicio de Fabric. Consulte toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt dentro de hello [paquete independiente](service-fabric-cluster-standalone-package-contents.md) para obtener instrucciones.
Para un proceso manual, siga estas instrucciones Hola.

Modifique su Hola de tooset de configuración de clúster después de propiedad toofalse antes de iniciar una actualización de la configuración.

        "fabricClusterAutoupgradeEnabled": false,

Consulte demasiado[ServiceFabricClusterConfigurationUpgrade inicio PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) para obtener detalles de uso. Asegúrese de tooupdate seguro 'clusterConfigurationVersion' en su JSON antes de empezar la actualización de la configuración de Hola.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a>Flujo de trabajo de actualización de clúster

1. Ejecute Get-ServiceFabricClusterUpgrade desde uno de los nodos de hello en clúster de hello y observe hello TargetCodeVersion.
2. Siguiente ejecución Hola desde un toolist de equipo conectado internet todos actualiza las versiones compatibles con la versión actual de Hola y descarga Hola correspondiente paquete de hello asociados vínculos de descarga.

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. Conectar toohello clúster desde cualquier equipo que tenga equipos Hola de tooall de acceso de administrador que se muestran como nodos de clúster de Hola. máquina de Hola que este script se ejecuta en no tiene toobe parte del clúster de Hola

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. Copie el paquete de hello descargado en almacén de imágenes de clúster de Hola.

5. Registrar el paquete de hello copiado.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. Iniciar una versión disponible del tooan de actualización de clúster.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   Puede supervisar el progreso de Hola de actualización de hello en el Explorador de Service Fabric o puede ejecutar el siguiente comando de PowerShell de Hola.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Si no se cumplen las directivas de mantenimiento de clúster de hello, Hola actualización se ha revertido. las directivas de mantenimiento personalizado de toospecify para hello **inicio ServiceFabricClusterUpgrade** command, consulte la documentación de Hola para [ServiceFabricClusterUpgrade inicio](https://msdn.microsoft.com/library/mt125872.aspx).

Después de corregir los problemas de Hola que dan como resultado de reversión de hello, Iniciar actualización de hello nuevo por siguiente Hola mismos pasos como se describen anteriormente.


## <a name="upgrade-hello-cluster-configuration"></a>Actualice la configuración de clúster de Hola
Antes de iniciar la actualización de la configuración de hello, puede probar el nuevo json de configuración de clúster mediante la ejecución de script de powershell de hello en el paquete independiente de Hola.

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
o

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

Algunas configuraciones no se pueden actualizar, como los puntos de conexión, el nombre del clúster, la dirección IP del nodo, etc. Esto probará Hola nuevo clúster configuración json contra Hola antiguo y producir errores en la ventana de Powershell de hello si hay algún problema.

actualización de la configuración de clúster de tooupgrade hello, ejecute **ServiceFabricClusterConfigurationUpgrade inicio**. actualización de la configuración de Hello es dominio de actualización procesado por dominio de actualización.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a>Actualización de la configuración de un certificado de clúster  
Certificado de clúster se utiliza para la autenticación entre los nodos de clúster, por lo que la sustitución del certificado de hello debe realizarse con precaución adicional porque logra, se bloqueará la comunicación Hola entre los nodos del clúster.  
Desde el punto de vista técnico, se admiten tres opciones:  

1. Actualización de los certificados única: ruta de actualización de hello es ' certificado (principal) -> (principal) del certificado B -> C de certificado (principal) ->...'.   
2. Actualización de certificados de Double: ruta de actualización de hello es ' certificado -> (principal) de certificados (principal) y B (secundario) -> B de certificado (principal) -> B de certificado (principal) y C (secundario) -> C de certificado (principal) ->...'.
3. Actualización del tipo de certificado: configuración de certificado basada en huella digital <-> Configuración de certificado basada en CommonName. Por ejemplo, Huella digital del certificado A (principal) y Huella digital B (secundaria) -> Certificado CommonName C.


## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo toocustomize algunos [configuración de clúster de Service Fabric](service-fabric-cluster-fabric-settings.md).
* Obtenga información acerca de cómo demasiado[escalar el clúster de entrada y salida](service-fabric-cluster-scale-up-down.md).
* Obtenga información sobre [actualizaciones de aplicaciones](service-fabric-application-upgrade.md).

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
