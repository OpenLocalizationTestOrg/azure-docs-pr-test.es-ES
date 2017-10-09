---
title: aaaCreate un servicio confiable de Azure Service Fabric con C#
description: "Creación, implementación y depuración de una aplicación de servicio de confianza integrada en Azure Service Fabric, con Visual Studio."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a>Creación de su primera aplicación de Reliable Services con estado de Service Fabric en C#

Obtenga información acerca de cómo toodeploy su primera aplicación de Service Fabric para .NET en Windows en tan solo unos minutos. Cuando haya terminado, tendrá un clúster local que se ejecuta con una aplicación de servicio de confianza.

## <a name="prerequisites"></a>Requisitos previos

Antes de comenzar, asegúrese de haber [configurado el entorno de desarrollo](service-fabric-get-started.md). Esto incluye la instalación de SDK del servicio de Fabric de Hola y 2017 de Visual Studio o 2015.

## <a name="create-hello-application"></a>Crear aplicación hello

Inicie Visual Studio como **administrador**.

Creación de un proyecto con `CTRL`+`SHIFT`+`N`

Hola **nuevo proyecto** cuadro de diálogo, elija **en la nube > aplicación de servicio de Fabric**.

Nombre de la aplicación hello **MyApplication** y presione **Aceptar**.

   
![Cuadro de diálogo de proyecto nuevo en Visual Studio.][1]

Puede crear cualquier tipo de aplicación de Service Fabric del cuadro de diálogo siguiente Hola. Para esta guía de inicio rápido, elija **Servicio con estado**.

Nombre de servicio de hello **MyStatefulService** y presione **Aceptar**.

![Cuadro de diálogo de servicio nuevo en Visual Studio.][2]


Visual Studio crea el proyecto de aplicación de Hola y un proyecto de servicio con estado de Hola y mostrarlos en el Explorador de soluciones.

![Explorador de soluciones después de la creación de una aplicación con el servicio con estado][3]

proyecto de aplicación Hola (**MyApplication**) no contiene ningún código directamente. En su lugar, hace referencia a un conjunto de proyectos de servicio. Además, contiene otros tres tipos de contenido:

* **Perfiles de publicación**  
Perfiles para implementar entornos a toodifferent.

* **Scripts**  
Script de PowerShell para implementar o actualizar la aplicación.

* **Definición de la aplicación**  
Incluye el archivo de ApplicationManifest.xml hello en *ApplicationPackageRoot* que describe la composición de la aplicación. Archivos de parámetros de las aplicaciones asociadas están bajo *ApplicationParameters*, que puede ser usado toospecify parámetros específicos del entorno. Perfil de publicación se seleccionan Visual Studio asociado de un archivo de parámetros de la aplicación que se especifica en Hola durante el entorno de implementación tooa específico.
    
Para obtener información general del contenido de Hola Hola del proyecto del servicio, consulte [Introducción a servicios de confianza](service-fabric-reliable-services-quick-start.md).

## <a name="deploy-and-debug-hello-application"></a>Implementar y depurar la aplicación hello

Ahora que tiene una aplicación, ejecútela.

En Visual Studio, presione `F5` toodeploy aplicación de hello para la depuración.

>[!NOTE]
>Hola la primera vez que se ejecute e implementa aplicación de hello localmente, Visual Studio crea un clúster local para la depuración. Esto puede tardar algún tiempo. estado de creación de clúster de Hola se muestra en la ventana de salida de Visual Studio de hello.

Cuando esté listo clúster hello, obtendrá una notificación de aplicación Hola clúster local system bandeja manager incluido con hello SDK.
   
![Notificación de bandeja de sistema del clúster local][4]

Una vez empieza a aplicación Hola, Visual Studio muestra automáticamente hello **Visor de eventos de diagnóstico**, donde puede ver el resultado del seguimiento de los servicios.
   
![Visor de eventos de diagnóstico][5]

Hello plantilla de servicio con estado usamos simplemente muestra un aumento de valor de contador en hello `RunAsync` método **MyStatefulService.cs**.

Expanda una de hello toosee de eventos para obtener más detalles, incluido nodo Hola donde se está ejecutando código de hello. En este caso, es \_Node\_2, aunque puede que en su equipo sea otro.
   
![Detalle del Visor de eventos de diagnóstico][6]

clúster local de Hello contiene cinco nodos hospedados en un único equipo. En un entorno de producción, cada nodo se hospeda en una máquina virtual o física distinta. pérdida de hello toosimulate de una máquina al llevar a cabo Hola Visual Studio del depurador en hello mismo tiempo, vamos a poner sin conexión uno de los nodos de hello en clúster local de Hola.

Hola **el Explorador de soluciones** ventana, abra **MyStatefulService.cs**. 

Buscar hello `RunAsync` método y establezca un punto de interrupción en la primera línea del método hello de Hola.

![Punto de interrupción en el método RunAsync de servicio con estado][7]

Iniciar hello **Service Fabric Explorer** herramienta con el botón secundario en hello **Administrador de clústeres Local** aplicación de bandeja del sistema y elija **administrar clúster Local**.

![Inicie el Explorador de Service Fabric desde Hola Administrador de clústeres Local][systray-launch-sfx]

[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) ofrece una representación visual de un clúster. Incluye conjunto de Hola de las aplicaciones implementadas tooit y Hola de nodos físicos que lo componen.

En el panel izquierdo de hello, expanda **clúster > nodos** y buscar Hola nodo donde se ejecuta el código.

Haga clic en **acciones > desactivar (reiniciar)** toosimulate un reinicio del equipo.

![Detener un nodo en el Explorador de Service Fabric][sfx-stop-node]

En breve, debería ver el punto de interrupción alcanzado en Visual Studio como cálculo Hola que estabas haciendo perfectamente en un nodo conmuta por error tooanother.


A continuación, devolver toohello Visor de eventos de diagnóstico y observe los mensajes de saludo. contador de Hello ha ido incremento, incluso si los eventos de hello realmente proceden de un nodo diferente.

![Visor de eventos de diagnóstico después de la conmutación por error][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a>Limpiar el clúster local de hello (opcional)

Recuerde que este clúster local es real. Detener el depurador de hello quita la instancia de la aplicación y anula el registro de tipo de aplicación Hola. Sin embargo, el clúster de hello continúa toorun en segundo plano de Hola. Cuando esté listo toostop Hola local del clúster, hay un par de opciones.

### <a name="keep-application-and-trace-data"></a>Mantener los datos de aplicación y de seguimiento

Apagar clúster Hola con el botón secundario en hello **Administrador de clústeres Local** aplicación de bandeja del sistema y, a continuación, elija **detener clúster Local**.

### <a name="delete-hello-cluster-and-all-data"></a>Eliminar el clúster de Hola y todos los datos

Quitar clúster de hello con el botón secundario en hello **Administrador de clústeres Local** aplicación de bandeja del sistema y, a continuación, elija **quitar clúster Local**. 

Si elige esta opción, Visual Studio volverá a implementar Hola Hola de clúster siguiente tiempo de aplicación Hola a su ejecución. Elija esta opción si no tiene la intención de clúster local de toouse Hola durante algún tiempo o si necesita recursos tooreclaim.

## <a name="next-steps"></a>Pasos siguientes
Más información sobre [Reliable Services](service-fabric-reliable-services-introduction.md).
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
