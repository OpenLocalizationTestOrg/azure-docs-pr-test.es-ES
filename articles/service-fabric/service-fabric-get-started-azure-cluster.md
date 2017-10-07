---
title: "aaaSet de un clúster de Azure Service Fabric | Documentos de Microsoft"
description: "Inicio rápido: creación de un clúster de Windows o Linux Service Fabric en Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a>Creación del primer clúster de Service Fabric en Azure
Un [clúster de Service Fabric](service-fabric-deploy-anywhere.md) es un conjunto de máquinas físicas o virtuales conectadas a la red, en las que se implementan y administran los microservicios. Este inicio rápido le ayuda a un clúster de cinco nodos, que se ejecuta en Windows o Linux, a través de hello toocreate [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) o [portal de Azure](http://portal.azure.com) en tan solo unos minutos.  

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.


## <a name="use-hello-azure-portal"></a>Usar hello portal de Azure

Inicie sesión en toohello portal de Azure en [http://portal.azure.com](http://portal.azure.com).

### <a name="create-hello-cluster"></a>Crear clúster Hola

1. Haga clic en hello **New** encontró el botón en la esquina izquierda superior de Hola de hello portal de Azure.
2. Seleccione **proceso** de hello **nuevo** hoja y, a continuación, seleccione **clúster de Service Fabric** de hello **proceso** hoja.
3. Rellene Hola Service Fabric **Fundamentos** formulario. Para **sistema operativo**, seleccione la versión de Hola de Windows o Linux que desea Hola toorun de nodos de clúster. nombre de usuario de Hello y una contraseña escritos aquí es toolog usado en la máquina virtual de toohello. En **Grupo de recursos**, cree uno. Un grupo de recursos es un contenedor lógico en el que se administran y crean los recursos de Azure. Cuando haya terminado, haga clic en **Aceptar**.

    ![Salida de instalación de clúster][cluster-setup-basics]

4. Rellene hello **configuración de clúster** formulario.  En **Número de tipos de nodos**, escriba "1".

5. Seleccione **1 (principal) del tipo de nodo** y rellene hello **configuración de tipo de nodo** formulario.  Escriba un nombre de tipo de nodo y establezca hello [el nivel de durabilidad](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) demasiado "bronce".  Seleccione un tamaño de máquina virtual.

    Tipos de nodos definen tamaño de máquina virtual de hello, número de máquinas virtuales, los puntos de conexión personalizadas, y otras opciones de Hola máquinas virtuales de ese tipo. Cada tipo de nodo definido se configura como un conjunto de escala de máquina virtual independiente, que es usado toodeploy y máquinas virtuales administradas como un conjunto. Cada tipo de nodo se puede escalar o reducir verticalmente de forma independiente. Cada uno tiene diferentes conjuntos de puertos abiertos y puede tener distintas métricas de capacidad.  Hola primera o principal, tipo de nodo es donde los servicios del sistema de Service Fabric se hospedan y deben tener cinco o más máquinas virtuales.

    En cualquier implementación de producción, el [planeamiento de capacidad](service-fabric-cluster-capacity.md) es un paso importante.  Para este inicio rápido, sin embargo, no está ejecutando aplicaciones así que seleccione un tamaño de máquina virtual *DS1_v2 Estándar*.  Seleccione "Silver" para hello [nivel de confiabilidad](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) y una escala de la máquina virtual inicial establece capacidad de 5.  

    Extremos personalizados abrirán puertos en el equilibrador de carga de Azure de Hola para que puedan conectarse con aplicaciones que se ejecutan en el clúster de Hola.  Escriba "80, 8172" tooopen los puertos 80 y 8172.

    ¿Comprobar hello **configurar opciones avanzadas** box, que se utiliza para personalizar los extremos de la administración de TCP o HTTP, intervalos de puertos de la aplicación, [las restricciones de posición](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), y [capacidad propiedades](service-fabric-cluster-resource-manager-metrics.md).    

    Seleccione **Aceptar**.

6. Hola **configuración de clúster** formulario, establezca **diagnósticos** demasiado**en**.  Para este tutorial rápido, no es necesario tooenter cualquier [tejido establecer](service-fabric-cluster-fabric-settings.md) propiedades.  En **versión de Fabric**, seleccione **automática** actualizar el modo de modo que Microsoft actualiza automáticamente la versión Hola de código de fabric Hola ejecuta Hola clúster.  Establecer el modo de hello demasiado**Manual** si desea demasiado[elegir una versión compatible](service-fabric-cluster-upgrade.md) tooupgrade a. 

    ![Configuración del tipo de nodo][node-type-config]

    Seleccione **Aceptar**.

7. Rellene hello **seguridad** formulario.  Para este inicio rápido seleccione **No seguro**.  Es muy recomendable un clúster segura para las cargas de trabajo de producción, de toocreate sin embargo, dado que cualquiera puede conectarse tooan clúster y realizar operaciones de administración de forma anónima.  

    Los certificados se utilizan en toosecure de autenticación y cifrado de Service Fabric tooprovide diversos aspectos de un clúster y sus aplicaciones. Para más información sobre el modo en que se usan los certificados en Service Fabric, consulte los [Escenarios de seguridad de los clústeres de Service Fabric](service-fabric-cluster-security.md).  autenticación de usuario de tooenable mediante Azure Active Directory o tooset los certificados de seguridad de la aplicación, [crear un clúster desde una plantilla de administrador de recursos](service-fabric-cluster-creation-via-arm.md).

    Seleccione **Aceptar**.

8. Resumen de hello de revisión.  Si desea que toodownload una plantilla de administrador de recursos compilada a partir de la configuración de Hola que escribió, seleccione **descargar la plantilla y los parámetros**.  Seleccione **crear** clúster de hello toocreate.

    Puede ver el progreso de la creación de hello en las notificaciones de Hola. (Haga clic en el icono de campana"hello" cerca de la barra de estado de hello en la parte superior de hello derecha de la pantalla). Si hace clic en **Pin tooStartboard** al crear el clúster de hello, consulte **implementación de clúster de Service Fabric** anclado toohello **iniciar** panel.

### <a name="view-cluster-status"></a>Visualización del estado del clúster
Una vez creado el clúster, puede inspeccionar el clúster en hello **Introducción** hoja en el portal de Hola. Ahora puede ver detalles de hello del clúster en panel de hello, incluidos extremo público del clúster de Hola y un explorador de Fabric tooService de vínculo.

![Estado del clúster][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>Visualizar el clúster de hello mediante el Explorador de Service Fabric
[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) es una buena herramienta para visualizar el clúster y administrar aplicaciones.  Explorador de Service Fabric es un servicio que se ejecuta en el clúster de Hola.  Acceder a él mediante un explorador web, haga clic en hello **Service Fabric Explorer** vínculo de clúster de hello **Introducción** página del portal de Hola.  También puede especificar direcciones de hello directamente en el Explorador de hello: [http://quickstartcluster.westus.cloudapp.azure.com:19080/explorador](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)

panel de clúster de Hello proporciona una visión general del clúster, incluido un resumen de la aplicación y el estado de nodo. vista de nodo de Hello muestra el diseño físico de Hola de clúster de Hola. Para un nodo determinado, puede comprobar qué aplicaciones tienen el código implementado en ese nodo.

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a>Conectar el clúster toohello mediante PowerShell
Compruebe que ese clúster Hola se está ejecutando al conectar con PowerShell.  Hello ServiceFabric PowerShell se instala con hello [SDK del servicio de Fabric](service-fabric-get-started.md).  Hola [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establece un clúster de toohello de conexión.   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
Vea [clúster segura de conectar tooa](service-fabric-connect-to-secure-cluster.md) para obtener ejemplos de conexión de tooa de clúster. Después de la conexión de toohello de clúster, use hello [ServiceFabricNode Get](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay una lista de nodos en la información de clúster y el estado de Hola para cada nodo. **HealthState** debe ser *OK* para cada nodo.

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-hello-cluster"></a>Quitar clúster Hola
Además propio recurso de clúster toohello, un clúster de Service Fabric se compone de otros recursos de Azure. Por lo que toocompletely eliminar un clúster de Service Fabric debe toodelete que todos Hola recursos que está formada. clúster de Hola de manera más sencilla de Hello toodelete y todos los recursos de Hola que consume es grupo de recursos de toodelete Hola. Para otro toodelete formas un clúster o toodelete recursos Hola algunas (aunque no todos) en un grupo de recursos, consulte [eliminar un clúster](service-fabric-cluster-delete.md)

Eliminar un grupo de recursos en hello portal de Azure:
1. Navegar por clúster de Service Fabric toohello desea toodelete.
2. Haga clic en hello **grupo de recursos** nombre de página de hello clúster essentials.
3. Hola **Essentials de grupo de recursos** página, haga clic en **eliminar el grupo de recursos** y siga las instrucciones de hello en dicha eliminación de página toocomplete Hola Hola del grupo de recursos.
    ![Eliminar grupo de recursos de Hola][cluster-delete]


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a>Usar Powershell de Azure toodeploy un clúster segura
1. Descargar hello [Azure Powershell versión 4.0 o posterior del módulo](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) en su equipo.

2. Abra una ventana de Windows PowerShell, Hola de ejecución siguiente comando. 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    Debería aparecer un resultado similar toohello.

    ![ps-list][ps-list]

3. TooAzure de inicio de sesión y seleccione hello toowhich de suscripción que desea toocreate Hola clúster

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. Hola ejecución sigue toonow comando crea un clúster seguro. No olvide parámetros de hello toocustomize. 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    comando Hello puede durar entre 10 minutos too30 minutos toocomplete, al final de Hola de ella, debe obtener un siguiente toohello similar de salida. salida de Hello tiene información sobre el certificado de hello, hello KeyVault donde se cargaron en, y Hola carpeta local donde se copia el certificado de Hola. 

    ![ps-out][ps-out]

5. Copiar el resultado completo de Hola y guarde el archivo de texto de tooa como necesitamos toorefer tooit. Tome nota de hello siguiendo la información de salida de hello. 

    - **CertificateSavedLocalPath**: c:\mycertificates\mycluster20170504141137.pfx
    - **CertificateThumbprint**: C4C1E541AD512B8065280292A8BA6079C3F26F10
    - **ManagementEndpoint**: https://mycluster.southcentralus.cloudapp.azure.com:19080
    - **ClientConnectionEndpointPort**: 19000

### <a name="install-hello-certificate-on-your-local-machine"></a>Instalar certificado de hello en el equipo local
  
clúster de toohello tooconnect, necesita tooinstall Hola certificado en almacén de hello Personal del usuario actual de Hola. 

Ejecute hello después de PowerShell

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

Ya estás listo tooconnect tooyour segura clúster.

### <a name="connect-tooa-secure-cluster"></a>Conectar el clúster segura tooa 

Ejecute hello siguiente comando PowerShell tooconnect tooa segura clúster. Detalles del certificado Hola deben coincidir con un certificado que se usa tooset clúster Hola. 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


Hola siguiendo el ejemplo se muestra hello parámetros completed: 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Ejecute hello después toocheck de comando que está conectado y Hola clúster es correcto.

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a>Publicar su clúster de tooyour aplicaciones desde Visual Studio

Ahora que ha configurado un clúster de Azure, puede publicar su tooit de aplicaciones desde Visual Studio por hello siguiente [publicar tooan clúster](service-fabric-publish-app-remote-cluster.md) documento. 

### <a name="remove-hello-cluster"></a>Quitar clúster Hola
Además propio recurso de clúster toohello, un clúster se compone de otros recursos de Azure. clúster de Hola de manera más sencilla de Hello toodelete y todos los recursos de Hola que consume es grupo de recursos de toodelete Hola. 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha configurado un clúster de desarrollo, prueba Hola siguiente:
* [Crear un clúster seguro en el portal de Hola](service-fabric-cluster-creation-via-portal.md)
* [Crear un clúster a partir de una plantilla](service-fabric-cluster-creation-via-arm.md) 
* [Implemente aplicaciones mediante PowerShell](service-fabric-deploy-remove-applications.md).


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
