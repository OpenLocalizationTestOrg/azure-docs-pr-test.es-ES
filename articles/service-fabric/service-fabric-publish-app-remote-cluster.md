---
title: "aaaPublish un clúster remoto tooa de aplicación con Visual Studio | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toopublish un tejido de servicio remoto tooa de aplicación de clúster mediante el uso de Visual Studio."
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: faecd892-eb54-4d9c-8023-c67442afb8e8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/29/2016
ms.author: cawa
ms.openlocfilehash: d0f06f120cc7e22f3f8e73ce0970e1da5823e647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-visual-studio"></a>Implementación y eliminación de aplicaciones con Visual Studio
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [API de FabricClient](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Hola extensión de Azure Service Fabric para Visual Studio proporciona una forma sencilla, repetibles y secuencias de comandos toopublish un clúster de Service Fabric tooa de aplicación.

## <a name="hello-artifacts-required-for-publishing"></a>artefactos de Hello necesarios para su publicación
### <a name="deploy-fabricapplicationps1"></a>Deploy-FabricApplication.ps1
Se trata de un script de PowerShell que usa una ruta de acceso del perfil de publicación como un parámetro para la publicación de aplicaciones de Service Fabric. Puesto que este script forma parte de la aplicación, son toomodify bienvenida, según sea necesario para la aplicación.

### <a name="publish-profiles"></a>Perfiles de publicación
Llama a una carpeta de proyecto de aplicación de Service Fabric hello **PublishProfiles** contiene los archivos XML que almacenan información esencial para publicar una aplicación, como:

* Parámetros de conexión del clúster de Service Fabric
* Archivo de parámetros de ruta de acceso tooan aplicación
* Configuración de actualización

De forma predeterminada, la aplicación incluirá tres perfiles de publicación: Local.1Node.xml, Local.5Node.xml y Cloud.xml. Puede agregar más perfiles copiando y pegando uno de los archivos predeterminados de Hola.

### <a name="application-parameter-files"></a>Archivos de parámetros de la aplicación
Llama a una carpeta de proyecto de aplicación de Service Fabric hello **ApplicationParameters** contiene archivos XML para los valores de parámetro de manifiesto de aplicación especificado por el usuario. Los archivos de manifiesto de la aplicación pueden tener parámetros para que se puedan usar otros valores para la configuración de implementación. toolearn más información acerca de la parametrización de la aplicación, consulte [administrar varios entornos de Service Fabric](service-fabric-manage-multiple-environment-app-configuration.md).

> [!NOTE]
> Para los servicios de actor, debe compilar el proyecto de hello primero antes de intentar el archivo de hello tooedit en un editor o a través de hello cuadro de diálogo de publicación. Esto es porque se generará una parte de los archivos de manifiesto de Hola durante la compilación de Hola.

## <a name="toopublish-an-application-using-hello-publish-service-fabric-application-dialog-box"></a>toopublish una aplicación mediante el cuadro de diálogo Publicar aplicación de servicio Fabric Hola
Hello pasos siguientes demuestran cómo toopublish una aplicación usando Hola **publicar aplicación de servicio de Fabric** cuadro de diálogo proporcionado por hello tejido de servicio de Visual Studio Tools.

1. En menú contextual de Hola Hola Service Fabric del proyecto de aplicación, elija **publicar...** Hola tooview **publicar aplicación de servicio de Fabric** cuadro de diálogo.
   
    ![Hola ** el cuadro de diálogo Publicar servicio Fabric aplicación **][0]
   
    archivo Hello seleccionado en hello **elegir como destino profile** cuadro de lista desplegable es donde todos los valores de hello, excepto **manifiesto versiones**, se guardan. Puede volver a usar un perfil existente o cree uno nuevo eligiendo **< administrar perfiles... >** en hello **elegir como destino profile** cuadro de lista desplegable. Cuando se elige un perfil de publicación, su contenido aparece en los campos correspondientes del cuadro de diálogo de Hola Hola. toosave los cambios en cualquier momento, elija hello **Guardar perfil** vínculo.    
2. Hola **extremo de la conexión** sección, especifique el extremo de publicación locales o remotos Service Fabric de un clúster. tooadd o cambiar Hola extremo de la conexión, haga clic en hello **extremo de la conexión** lista desplegable. lista de Hello muestra hello disponible Service Fabric clúster conexión extremos toowhich que puede publicar en función de sus suscripciones de Azure. Tenga en cuenta que si no se ha iniciado en tooVisual Studio, es posible que toodo solicitada así.
   
    Utilice Hola clúster selección diálogo cuadro toochoose de conjunto de Hola de suscripciones disponibles y clústeres.
   
    ![Hola ** el cuadro de diálogo Seleccionar servicio Fabric clúster **][1]
   
   > [!NOTE]
   > Si desea que toopublish tooan arbitrario extremo (por ejemplo, un clúster de entidad), vea hello **publica tooan clúster arbitrario extremo** sección más adelante.
   > 
   > 
   
    Una vez elegido un punto de conexión, Visual Studio valida el clúster de Service Fabric de hello conexión toohello seleccionado. Si el clúster de hello no está seguro, Visual Studio puede conectarse tooit inmediatamente. Sin embargo, si el clúster de hello es seguro, necesitará tooinstall un certificado en el equipo local antes de continuar. Vea [cómo tooconfigure proteger conexiones](service-fabric-visualstudio-configure-secure-connections.md) para obtener más información. Cuando haya terminado, elija hello **Aceptar** botón. clúster de Hello seleccionado aparece en hello **publicar aplicación de servicio de Fabric** cuadro de diálogo.
3. Hola **archivo de parámetros de la aplicación** lista desplegable, navegue tooan archivo de parámetros de aplicación. Un archivo de parámetros de la aplicación contiene los valores especificados por el usuario para los parámetros en el archivo de manifiesto de aplicación Hola. tooadd o cambiar un parámetro, elija hello **editar** botón. Escriba o cambie el valor del parámetro de Hola Hola **parámetros** cuadrícula. Cuando haya terminado, elija hello **guardar** botón.
   
    ![Hola ** el cuadro de diálogo Editar parámetros **][2]
4. Hola de uso **actualización Hola aplicación** toospecify de casilla de verificación si esta acción de publicación es una actualización. Las acciones de publicación de actualización difieren de las acciones de publicación habituales. Consulte [Actualización de la aplicación de Service Fabric](service-fabric-application-upgrade.md) para ver una lista de las diferencias. configuración de actualización de tooconfigure, elija hello **configurar opciones de actualización** vínculo. aparece el editor de parámetros de actualización de Hola. Vea [configurar Hola la actualización de una aplicación de Service Fabric](service-fabric-visualstudio-configure-upgrade.md) toolearn más acerca de los parámetros de actualización.
5. Elija hello **manifiesto versiones...** Hola de botón tooview **editar versiones** cuadro de diálogo. Necesitará tooupdate versiones de aplicación y servicio para un contexto de actualización tootake. Vea [tutorial de actualización de aplicaciones de Service Fabric](service-fabric-application-upgrade-tutorial.md) toolearn la aplicación y las versiones de manifiesto de servicio afectan a un proceso de actualización.
   
    ![Hola ** el cuadro de diálogo Editar versiones **][3]
   
    Si la aplicación hello y versiones de servicio utilizan el control de versiones semántico como 1.0.0 o valores numéricos con formato de hello 1.0.0.0, seleccione hello **actualizar automáticamente la aplicación y las versiones de servicio** opción. Cuando elige esta opción, el servicio de Hola y números de versión de la aplicación se actualizan automáticamente cada vez que un código, configuración, o se actualiza la versión del paquete de datos. Si prefiere versiones de hello tooedit manualmente, desactive Hola casilla toodisable esta característica.
   
   > [!NOTE]
   > Para todos los tooappear de entradas de paquete para un proyecto de actor, primero cree Hola proyecto toogenerate entradas de hello en los archivos de manifiesto de servicio de Hola.
   > 
   > 
6. Cuando haya terminado todos los valores necesarios de hello, especificar elija hello **publicar** botón toopublish su toohello de aplicación seleccionado clúster de Service Fabric. se aplican los valores de Hello que especificó toohello el proceso de publicación.

## <a name="publish-tooan-arbitrary-cluster-endpoint-including-party-clusters"></a>Publicar tooan de punto de conexión de clúster arbitrario (incluidos los clústeres de entidad)
Hola experiencia de publicación de Visual Studio está optimizada para la publicación de clústeres de tooremote asociados a una de las suscripciones de Azure. Sin embargo, es posible toopublish tooarbitrary puntos de conexión (por ejemplo, clústeres de la entidad de Service Fabric) por directamente edición Hola publicar XML del perfil. Como se describió anteriormente, tres perfiles de publicación se proporcionan de forma predeterminada:**Local.1Node.xml**, **Local.5Node.xml**, y **Cloud.xml**--pero estás toocreate bienvenida perfiles adicionales para diferentes entornos. Por ejemplo, podría desear toocreate un perfil de publicación tooparty clústeres, llamados **Party.xml**.

Si va a conectar tooan no segura de clúster, todo lo que se necesita es el extremo de la conexión de clúster hello, como `partycluster1.eastus.cloudapp.azure.com:19000`. En que los casos, extremo de la conexión de Hola Hola publicar perfil sería algo parecido a esto:

```XML
<ClusterConnectionParameters ConnectionEndpoint="partycluster1.eastus.cloudapp.azure.com:19000" />
```

  Si va a conectar tooa segura clúster, también necesitará tooprovide detalles de Hola de certificado de cliente de Hola de hello almacén local toobe utilizado para la autenticación. Para obtener más información, consulte [clúster de Service Fabric de configurar conexiones seguras tooa](service-fabric-visualstudio-configure-secure-connections.md).

  Una vez configurado el perfil de publicación, puede hacer referencia en hello cuadro de diálogo de publicación tal y como se muestra a continuación.

  ![Nuevo perfil de publicación en el cuadro de diálogo de publicación][4]

  Tenga en cuenta que en este caso, Hola de nuevo perfil de publicación apunta tooone de archivos de parámetros de aplicación Hola de forma predeterminada. Esto es apropiado si desea toopublish Hola mismo número de tooa de configuración de aplicación de entornos. Por el contrario, en casos donde desea toohave configuraciones diferentes para cada entorno que desee toopublish a, sería sentido toocreate un archivo de parámetros de aplicación correspondiente.

## <a name="next-steps"></a>Pasos siguientes
toolearn tooautomate proceso de publicación hello en un entorno de integración continua, vea [configurar la integración continua de Service Fabric](service-fabric-set-up-continuous-integration.md).

[0]: ./media/service-fabric-publish-app-remote-cluster/PublishDialog.png
[1]: ./media/service-fabric-publish-app-remote-cluster/SelectCluster.png
[2]: ./media/service-fabric-publish-app-remote-cluster/EditParams.png
[3]: ./media/service-fabric-publish-app-remote-cluster/EditVersions.png
[4]: ./media/service-fabric-publish-app-remote-cluster/publish-to-party-cluster.png
