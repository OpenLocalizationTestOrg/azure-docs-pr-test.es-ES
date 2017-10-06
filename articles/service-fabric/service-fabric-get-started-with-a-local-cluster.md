---
title: aaaDeploy y actualizar Azure microservicios localmente | Documentos de Microsoft
description: "Obtenga información acerca de cómo implementar un tooit de aplicación existente tooset de un clúster de Service Fabric local y, a continuación, actualizar esa aplicación."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 60a1f6a5-5478-46c0-80a8-18fe62da17a8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi;mikhegn
ms.openlocfilehash: e5f5adc9edb71433b2a7635e9d661ff92a4b18ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a>Introducción a la implementación y actualización de aplicaciones en un clúster local
Hello Azure Service Fabric SDK incluye un entorno de desarrollo local completa que puede usar tooquickly Introducción a la implementación y administración de aplicaciones en un clúster local. En este artículo, crear un clúster local, implementar una tooit de aplicación existente y, a continuación, actualizar esa aplicación tooa nueva versión, todo ello desde Windows PowerShell.

> [!NOTE]
> En este artículo se asume que ya [configuró un entorno de desarrollo](service-fabric-get-started.md).
> 
> 

## <a name="create-a-local-cluster"></a>Creación de un clúster local
Un clúster de Service Fabric representa un conjunto de recursos de hardware en los que se pueden implementar aplicaciones. Por lo general, un clúster se compone de cualquier parte de cinco toomany miles de máquinas. Sin embargo, Hola tejido SDK del servicio incluye una configuración de clúster que se puede ejecutar en un único equipo.

Es importante toounderstand que Hola clúster local de Service Fabric no es un emulador o simulador. Se ejecuta Hola mismo código de plataforma que se encuentra en los clústeres de varios equipos. Hola única diferencia es que se ejecuta los procesos de plataforma de Hola que normalmente se reparten entre cinco equipos en un equipo.

Hola SDK proporciona tooset de dos maneras de un clúster local: un Windows PowerShell hello y script el Administrador de clústeres Local system aplicación de bandeja. En este tutorial, usamos el script de PowerShell de Hola.

> [!NOTE]
> Si creó un clúster local mediante la implementación de una aplicación desde Visual Studio, puede omitir esta sección.
> 
> 

1. Inicie una ventana nueva de PowerShell como administrador.
2. Ejecute el script de instalación de clúster de Hola desde la carpeta del SDK de hello:
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    La instalación del clúster tardará unos instantes. Una vez finalizada la instalación, debería ver una salida similar a esta:
   
    ![Salida de instalación de clúster][cluster-setup-success]
   
    Ya estás listo tootry implementación de un clúster de tooyour de aplicación.

## <a name="deploy-an-application"></a>Implementar una aplicación
Hola tejido SDK del servicio incluye un amplio conjunto de marcos de trabajo y herramientas para crear aplicaciones para el desarrollador. Si está interesado en aprender cómo las aplicaciones de toocreate en Visual Studio, vea [crear su primera aplicación de Service Fabric en Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).

En este tutorial, usará una aplicación de ejemplo existente (denominada WordCount) para que pueda centrarse en los aspectos de la administración de plataforma de Hola Hola: implementación, supervisión y actualización.

1. Inicie una ventana nueva de PowerShell como administrador.
2. Importe el módulo de PowerShell de SDK de tejido de servicio de Hola.
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. Crear una aplicación hello toostore de directorio que descargar e implementar, como C:\ServiceFabric.
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. [Descargar la aplicación WordCount de hello](http://aka.ms/servicefabric-wordcountapp) ubicación toohello que ha creado.  Nota: explorador Microsoft Edge de hello guarda el archivo hello con un *.zip* extensión.  Cambiar la extensión de archivo hello demasiado*.sfpkg*.
5. Conecte el clúster local toohello:
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. Cree una nueva aplicación mediante el comando de implementación del SDK de hello con un nombre y un paquete de aplicación de toohello de ruta de acceso.
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    Si todo funciona correctamente, debería ver Hola después de salida:
   
    ![Implementar un clúster local de aplicación toohello][deploy-app-to-local-cluster]
7. aplicación de hello toosee en acción, inicie el Explorador de Hola y navegue demasiado[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html). Debería ver lo siguiente:
   
    ![Interfaz de usuario de aplicación implementada][deployed-app-ui]
   
    Hola aplicación WordCount es sencillo. Incluye en el cliente JavaScript toogenerate aleatorio cinco caracteres "palabras de código", que son, a continuación, retransmite toohello aplicación a través de la API Web de ASP.NET. Un servicio con estado realiza un número de Hola de recuento de palabras. Se crean particiones basadas en el primer carácter de palabra Hola de Hola. Puede encontrar código de origen de Hola de aplicación WordCount de hello en hello [clásico Introducción ejemplos](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).
   
    aplicación Hola que implementamos contiene cuatro particiones. Por lo que las palabras que empiezan con la A la G se almacenan en la primera partición de hello, palabras que empiezan con H y N se almacenan en hello segunda partición y así sucesivamente.

## <a name="view-application-details-and-status"></a>Visualización de los detalles y estado de la aplicación
Ahora que hemos implementado aplicación hello, echemos un vistazo a algunos de los detalles de la aplicación hello en PowerShell.

1. Consultar todas las aplicaciones implementadas en clúster de hello:
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    Suponiendo que sólo ha implementado la aplicación WordCount de hello, verá algo parecido a:
   
    ![Consultar todas las aplicaciones implementadas en PowerShell][ps-getsfapp]
2. Vaya toohello siguiente nivel mediante una consulta de conjunto de hello de servicios que se incluyen en la aplicación WordCount de hello.
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Lista de servicios para la aplicación hello en PowerShell][ps-getsfsvc]
   
    aplicación Hello se compone de dos servicios, hello web front-end y servicio con estado Hola que administra palabras hello.
3. Por último, busque en la lista de Hola de particiones WordCountService:
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![Ver las particiones de servicio de hello en PowerShell][ps-getsfpartitions]
   
    Hola conjunto de comandos que utilizan, al igual que todos los comandos de PowerShell de tejido de servicio, están disponibles para los clústeres que se podrían conectar a local o remoto.
   
    Para una toointeract de manera más visual con clúster de hello, puede utilizar herramienta Explorador de Service Fabric basada en web de hello desplazándose demasiado[http://localhost:19080/explorador](http://localhost:19080/Explorer) en el Explorador de Hola.
   
    ![Ver detalles de aplicación en el Explorador de Service Fabric][sfx-service-overview]
   
   > [!NOTE]
   > toolearn más información acerca del explorador de Service Fabric, vea [visualizar el clúster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
   > 
   > 

## <a name="upgrade-an-application"></a>Actualizar una aplicación
Service Fabric proporciona actualizaciones sin tiempo de inactividad mediante la supervisión de estado de saludo de la aplicación hello tal y como implementa en el clúster de Hola. Realizar una actualización de hello aplicación WordCount.

nueva versión de Hello de aplicación hello ahora cuenta solo las palabras que empiecen por una vocal. Tal y como se implementa la actualización de hello, veremos dos cambios de comportamiento de la aplicación hello. En primer lugar, debe lenta tasa de hello en el que aumenta el recuento de hello, puesto que están siendo contados breves. En segundo lugar, puesto que la primera partición de hello tiene las dos vocales (A y E) y todas las demás particiones sólo contienen cada, su recuento finalmente inicie toooutpace Hola otros.

1. [Descargar paquete de la versión 2 de hello WordCount](http://aka.ms/servicefabric-wordcountappv2) toohello misma ubicación donde descargó el paquete de la versión 1 de Hola.
2. Devolver tooyour ventana de PowerShell y utilice el comando de actualización del SDK de hello tooregister Hola la nueva versión en clúster de Hola. A continuación, comience a actualizar fabric hello: / aplicación WordCount.
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    Debería ver Hola siguiente de PowerShell como Hola actualización comienza.
   
    ![Progreso de la actualización en PowerShell][ps-appupgradeprogress]
3. Mientras está actualización hello, quizá le resulte más fácil toomonitor su estado desde el Explorador de Service Fabric. Inicie una ventana del explorador y navegue demasiado[http://localhost:19080/explorador](http://localhost:19080/Explorer). Expanda **aplicaciones** en árbol Hola Hola izquierda, a continuación, elija **WordCount**y, finalmente, **fabric: / WordCount**. En la ficha de essentials hello, verá Hola estado de actualización de hello mientras pasa a través de dominios de actualización del clúster de Hola.
   
    ![Progreso de la actualización en el Explorador de Service Fabric][sfx-upgradeprogress]
   
    Tal y como se realiza la actualización de Hola a través de cada dominio, las comprobaciones de mantenimiento son realizada tooensure que aplicación hello se comporta correctamente.
4. Si vuelve a ejecutar Hola anteriormente de consulta de conjunto de hello de servicios en el tejido de hello: / aplicación WordCount, tenga en cuenta que Hola versión WordCountService cambiado pero Hola versión WordCountWebService no:
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Consultar servicios de aplicación después de la actualización][ps-getsfsvc-postupgrade]
   
    Este ejemplo resalta cómo Service Fabric administra las actualizaciones de aplicaciones. Modifica solo Hola conjunto de servicios (o paquetes de código o de configuración dentro de esos servicios) que han cambiado, lo que hace el proceso de Hola de actualización más rápidas y confiables.
5. Por último, devuelve el comportamiento del toohello explorador tooobserve hello de la nueva versión de la aplicación de Hola. Como se esperaba, Hola más lentamente que progresa de recuento y Hola primera partición termine con un poco más de volumen de Hola.
   
    ![Nueva versión de hello de vista de la aplicación hello en el Explorador de Hola][deployed-app-ui-v2]

## <a name="cleaning-up"></a>Limpiar
Antes de ajustar la, es importante tooremember que Hola clúster local es real. Las aplicaciones seguirán toorun en segundo plano de hello hasta que se quiten.  Según la naturaleza Hola de las aplicaciones, una aplicación en ejecución puede ocupar recursos significativos en su equipo. Tiene varias aplicaciones de toomanage de opciones y clúster de hello:

1. tooremove una aplicación individual y todos de datos, ejecute el siguiente comando de hello:
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    O bien, elimine la aplicación hello de hello Service Fabric Explorer **acciones** u Hola menú contextual en la vista de lista de hello aplicación izquierdo.
   
    ![Eliminación de una aplicación en el explorador de Service Fabric][sfe-delete-application]
2. Después de eliminar la aplicación hello de clúster de hello, anular el registro de las versiones 1.0.0 y 2.0.0 del tipo de aplicación WordCount Hola. La eliminación quita los paquetes de aplicaciones de hello, incluidos el código de hello y configuración del clúster de hello almacén de imágenes.
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    O bien, en el Explorador de tejido de servicio, elija **anule tipo** para la aplicación hello.
3. tooshut hacia abajo clúster Hola pero mantener datos de la aplicación de Hola y seguimientos, haga clic en **detener clúster Local** en la aplicación de bandeja del sistema de hello.
4. por completo, haga clic en el clúster de hello toodelete **quitar clúster Local** en la aplicación de bandeja del sistema de hello. Esta opción se producirá otro Hola lenta implementación próxima vez que presiones F5 en Visual Studio. Quitar clúster local de hello solo si no piensa toouse durante algún tiempo o si necesita recursos tooreclaim.

## <a name="one-node-and-five-node-cluster-mode"></a>Modo de clúster de uno y cinco nodos
Al desarrollar aplicaciones, a menudo se encuentra realizando iteraciones rápidas de escritura de código, depuración, cambio de código y depuración. toohelp optimizar este proceso, puede ejecutar el clúster local de hello en dos modos: uno o cinco nodos. Ambos modos de clúster tienen sus ventajas. El modo de clúster de cinco nodos permite toowork con un clúster real. Puede probar escenarios de conmutación por error, trabajar con más instancias y réplicas de los servicios. Modo de clúster de un nodo es una implementación rápida toodo optimizada y el registro de servicios, toohelp rápidamente valide el código con el tiempo de ejecución de hello Service Fabric.

Ni el modo de clúster de un nodo ni el de cinco nodos es un emulador o un simulador. clúster de desarrollo local Hola ejecuciones Hola mismo código de plataforma que se encuentra en los clústeres de varios equipos.

> [!WARNING]
> Al cambiar el modo de clúster de hello, el clúster actual Hola se quita de su sistema y se crea un nuevo clúster. datos de Hello almacenados en el clúster de Hola se eliminan cuando se cambia el modo de clúster.
> 
> 

toochange Hola modo tooone clúster de nodo, seleccione **modo de clúster de conmutación** Hola Administrador de clústeres Local de Service Fabric.

![Cambio del modo de clúster][switch-cluster-mode]

O bien, cambiar el modo de clúster de hello con PowerShell:

1. Inicie una ventana nueva de PowerShell como administrador.
2. Ejecute el script de instalación de clúster de Hola desde la carpeta del SDK de hello:
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    La instalación del clúster tardará unos instantes. Una vez finalizada la instalación, debería ver una salida similar a esta:
   
    ![Salida de instalación de clúster][cluster-setup-success-1-node]

## <a name="next-steps"></a>Pasos siguientes
* Tras la implementación y actualización de algunas aplicaciones pregeneradas, puede [intentar compilar la suya propia en Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).
* Todas las acciones de hello llevadas a cabo en el clúster local de hello en este artículo pueden realizarse en un [clúster Azure](service-fabric-cluster-creation-via-portal.md) así.
* actualización de Hola que hemos realizado en este artículo era básica. Vea hello [documentación de actualización](service-fabric-application-upgrade.md) toolearn más información acerca de hello potencia y flexibilidad de las actualizaciones de Service Fabric.

<!-- Images -->

[cluster-setup-success]: ./media/service-fabric-get-started-with-a-local-cluster/LocalClusterSetup.png
[extracted-app-package]: ./media/service-fabric-get-started-with-a-local-cluster/ExtractedAppPackage.png
[deploy-app-to-local-cluster]: ./media/service-fabric-get-started-with-a-local-cluster/DeployAppToLocalCluster.png
[deployed-app-ui]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-v1.png
[deployed-app-ui-v2]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-PostUpgrade.png
[sfx-app-instance]: ./media/service-fabric-get-started-with-a-local-cluster/SfxAppInstance.png
[sfx-two-app-instances-different-partitions]: ./media/service-fabric-get-started-with-a-local-cluster/SfxTwoAppInstances-DifferentPartitionCount.png
[ps-getsfapp]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFApp.png
[ps-getsfsvc]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc.png
[ps-getsfpartitions]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFPartitions.png
[ps-appupgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/PS-AppUpgradeProgress.png
[ps-getsfsvc-postupgrade]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc-PostUpgrade.png
[sfx-upgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/SfxUpgradeOverview.png
[sfx-service-overview]: ./media/service-fabric-get-started-with-a-local-cluster/sfx-service-overview.png
[sfe-delete-application]: ./media/service-fabric-get-started-with-a-local-cluster/sfe-delete-application.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[switch-cluster-mode]: ./media/service-fabric-get-started-with-a-local-cluster/switch-cluster-mode.png
