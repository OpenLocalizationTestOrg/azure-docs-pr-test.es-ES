---
title: "aaaQuickly implementar un clúster de Azure Service Fabric de tooan de aplicación existente"
description: "Usar un toohost de clúster de Azure Service Fabric una aplicación existente de Node.js con Visual Studio."
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a>Hospedaje de una aplicación de Node.js en Azure Service Fabric

Este inicio rápido le ayudará a implementar un clúster existente de Service Fabric de tooa de aplicación (Node.js en este ejemplo) se ejecuta en Azure.

## <a name="prerequisites"></a>Requisitos previos

Antes de comenzar, asegúrese de haber [configurado el entorno de desarrollo](service-fabric-get-started.md). Que incluye la instalación de SDK del servicio de Fabric de Hola y 2017 de Visual Studio o 2015.

También debe toohave una aplicación existente de Node.js para la implementación. Esta guía de rápido usa un sitio Web en Node.js simple que se puede descargar [aquí][download-sample]. Extraer este archivo tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` carpeta después de crear el proyecto de hello en el paso siguiente de saludo.

Si no tiene una suscripción a Azure, cree una [cuenta gratuita][create-account].

## <a name="create-hello-service"></a>Crear servicio Hola

Inicie Visual Studio como **administrador**.

Creación de un proyecto con `CTRL`+`SHIFT`+`N`

Hola **nuevo proyecto** cuadro de diálogo, elija **en la nube > aplicación de servicio de Fabric**.

Nombre de la aplicación hello **MyGuestApp** y presione **Aceptar**.

>[!IMPORTANT]
>Node.js fácilmente puede interrumpir el límite de hello 260 caracteres para rutas de acceso que tiene windows. Use una ruta de acceso corta propio proyecto de hello como **c:\code\svc1**.
   
![Cuadro de diálogo de proyecto nuevo en Visual Studio.][new-project]

Puede crear cualquier tipo de servicio de Service Fabric del cuadro de diálogo siguiente Hola. Para esta guía de inicio rápido, elija **Archivo ejecutable invitado**.

Nombre de servicio de Hola **MyGuestService** y establecer opciones de hello en hello derecho toohello siguientes valores:

| Configuración                   | Valor |
| ------------------------- | ------ |
| Carpeta del paquete de código       | _&lt;carpeta de Hello con la aplicación Node.js&gt;_ |
| Comportamiento del paquete de código     | Copie la carpeta contenido tooproject |
| Programa                   | node.exe |
| Argumentos                 | server.js |
| Carpeta de trabajo            | CodePackage |

Presione **Aceptar**.

![Cuadro de diálogo de servicio nuevo en Visual Studio.][new-service]

Visual Studio crea el proyecto de aplicación de Hola y un proyecto de servicio de actor hello y mostrarlos en el Explorador de soluciones.

proyecto de aplicación Hola (**MyGuestApp**) no contiene ningún código directamente. En su lugar, hace referencia a un conjunto de proyectos de servicio. Además, contiene otros tres tipos de contenido:

* **Perfiles de publicación**  
Preferencias en cuanto a las herramientas para los diferentes entornos.

* **Scripts**  
Script de PowerShell para implementar o actualizar la aplicación.

* **Definición de la aplicación**  
Incluye el manifiesto de aplicación hello en *ApplicationPackageRoot*. Archivos de parámetros de las aplicaciones asociadas están bajo *ApplicationParameters*, que definen la aplicación hello y le permiten tooconfigure específicamente para un entorno determinado.
    
Para obtener información general del contenido de Hola Hola del proyecto del servicio, consulte [Introducción a servicios de confianza](service-fabric-reliable-services-quick-start.md).

## <a name="set-up-networking"></a>Configuración de las redes

ejemplo de Hola aplicación Node.js nos estamos implementando utiliza el puerto **80** y necesitamos tootell Service Fabric que necesitamos que expone el puerto.

Abra hello **ServiceManifest.xml** archivo de proyecto de Hola. En parte inferior de hello del manifiesto de hello, hay una `<Resources> \ <Endpoints>` con una entrada ya definida. Modificar esa entrada tooadd `Port`, `Protocol`, y `Type`. 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a>Implementar tooAzure

Si presiona **F5** y ejecutar el proyecto de hello, resulta toohello implementado de clúster local. Sin embargo, vamos a implementar tooAzure en su lugar.

Haga doble clic en el proyecto de Hola y elija **publicar...**  que abre un tooAzure de toopublish del cuadro de diálogo.

![Publicar el cuadro de diálogo de tooazure para un servicio de fabric][publish]

Seleccione hello **PublishProfiles\Cloud.xml** perfil de destino.

Si no lo ha hecho anteriormente, elija un toodeploy cuenta de Azure para. Si aún no tiene ninguno, [regístrese para obtenerlo][create-account].

En **extremo de la conexión**, seleccione Hola toodeploy de clúster de Service Fabric a. Si no tiene uno, seleccione  **&lt;crear un nuevo clúster... &gt;**  que abrirá toohello de ventana de explorador web portal de Azure. Para obtener más información, consulte [crear un clúster en el portal de hello](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal). 

Cuando se crea el clúster de Service Fabric hello, que seguro Hola de tooset **los puntos de conexión personalizado** configuración demasiado**80**.

![Configuración del tipo de nodo de Service Fabric con el punto de conexión personalizado][custom-endpoint]

Crear un nuevo clúster de Service Fabric tiene algunos toocomplete de tiempo. Una vez se ha creado, vaya toohello back-cuadro de diálogo Publicar y seleccione  **&lt;actualizar&gt;**. Hola nuevo se encuentre en el cuadro de lista desplegable de hello; Seleccione esta opción.

Presione **publicar** y espere Hola implementación toofinish.

Esta operación puede tardar unos minutos. Una vez que se complete, puede tardar unos minutos para toobe de aplicación Hola totalmente disponible.

## <a name="test-hello-website"></a>Sitio Web de Hola de prueba

Una vez publicado su servicio, pruébelo en un explorador web. 

En primer lugar, abra Hola portal de Azure y busque el servicio de Service Fabric.

Compruebe la hoja de información general de Hola Hola de dirección de servicio. Usar el nombre de dominio de Hola Hola _extremo de la conexión de cliente_ propiedad. Por ejemplo: `http://mysvcfab1.westus2.cloudapp.azure.com`.

![Hoja de información general de tejido de servicio en hello portal de Azure][overview]

Navegar por la dirección de toothis donde podrá ver hello `HELLO WORLD` respuesta.

## <a name="delete-hello-cluster"></a>Eliminar el clúster de Hola

No olvide toodelete todos los recursos de Hola que haya creado para este tutorial rápido, que se le cobrará por dichos recursos.

## <a name="next-steps"></a>Pasos siguientes
Más información sobre [ejecutables de invitado](service-fabric-deploy-existing-app.md).

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F