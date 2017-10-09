---
title: "aaaSet la integración continua de Azure microservicios | Documentos de Microsoft"
description: "Obtener una visión general de cómo tooset la integración continua y de implementación para una aplicación de Service Fabric mediante el uso de Visual Studio Team Services (VSTS)."
services: service-fabric
documentationcenter: na
author: mthalman-msft
manager: timlt
editor: 
ms.assetid: 3e8c2290-9e7a-456a-9b2c-db44d1b3988d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 12/06/2016
ms.author: mthalman;mikhegn
ms.openlocfilehash: 041e081f4a42f379394f2d21f07db4f6de045b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-service-fabric-continuous-integration-and-deployment-with-visual-studio-team-services"></a>Configuración de la integración continua y la implementación de Service Fabric con Visual Studio Team Services
Este artículo describe Hola pasos tooset la integración continua y la implementación de una aplicación de Azure Service Fabric mediante Visual Studio Team Services (VSTS).

Este documento refleja el procedimiento actual de Hola y es toochange esperado con el tiempo.

## <a name="prerequisites"></a>Requisitos previos
tooget iniciado, siga estos pasos:

1. Asegúrese de que tiene acceso tooa Team Services cuenta o [crearlo](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services) usted mismo.
2. Asegúrese de que tiene el proyecto de equipo de acceso tooa Team Services o [crearlo](https://www.visualstudio.com/docs/setup-admin/create-team-project) usted mismo.
3. Asegúrese de que tiene un toowhich de clúster de Service Fabric puede implementar la aplicación o crear uno mediante hello [portal de Azure](service-fabric-cluster-creation-via-portal.md), [plantilla de Azure Resource Manager](service-fabric-cluster-creation-via-arm.md), o [Visual Studio ](service-fabric-cluster-creation-via-visual-studio.md).
4. Ya ha creado un proyecto de aplicación de Service Fabric (.sfproj). Debe tener un proyecto que se ha creado o actualizado con Service Fabric SDK 2.1 o superior (archivo de hello .sfproj debe contener un valor de propiedad ProjectVersion de 1.1 o superior).

> [!NOTE]
> Ya no se requieren agentes de compilación personalizados. Ahora, los agentes hospedados de Team Services vienen preinstalados con el software de administración de clústeres de Service Fabric, con lo que las aplicaciones pueden implementarse directamente desde dichos agentes.
> 
> 

## <a name="configure-and-share-your-source-files"></a>Configuración y uso compartido de los archivos de origen
en primer lugar de Hola que desee toodo es preparar un perfil de publicación para su uso por proceso de implementación de Hola que se ejecuta dentro de Team Services.  Hola perfil de publicación debe ser el clúster de hello tootarget configurado que preparó previamente:

1. Elija un perfil de publicación en el proyecto de aplicación que desea toouse del flujo de trabajo de integración continua. Siga hello [publicar instrucciones](service-fabric-publish-app-remote-cluster.md) acerca de cómo toopublish un clúster remoto tooa de aplicación. No necesita realmente toopublish la aplicación aunque. Puede hacer clic en hello **guardar** hipervínculo Hola cuadro de diálogo de publicación una vez haya configurado cosas adecuadamente.
2. Si desea que su toobe de aplicación actualizado para todas las implementaciones que se produce dentro de los servicios del equipo, desea hello tooconfigure actualización tooenable de perfil de publicación. Hola mismo cuadro de diálogo que se usa de publicación en el paso 1, asegúrese de que hello **actualización Hola aplicación** casilla de verificación está activada.  Obtenga más información sobre [cómo configurar más opciones de actualización](service-fabric-visualstudio-configure-upgrade.md). Haga clic en hello **guardar** hipervínculo toosave Hola configuración toohello el perfil de publicación.
3. Asegúrese de que ha guardado los cambios toohello publicar perfil y cancelar Hola cuadro de diálogo Publicar.
4. Ahora es el momento demasiado[compartir los archivos de origen del proyecto de aplicación](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#vs) con Team Services. Una vez que los archivos de origen están accesibles en Team Services, ahora puede mover en toohello el paso siguiente consiste en generar compilaciones. 

## <a name="create-a-build-definition"></a>Creación de una definición de compilación
Una definición de compilación de Team Services describe un flujo de trabajo compuesto por una serie de pasos de compilación que se ejecutan de manera secuencial. objetivo de Hola de definición de compilación de Hola que va a crear es tooproduce un paquete de aplicación de Service Fabric y otros artefactos, que pueden ser utilizados toodeploy Hola aplicación. Obtenga más información sobre las [definiciones de compilación](https://www.visualstudio.com/docs/build/define/create)de Team Services.

### <a name="create-a-definition-from-hello-build-template"></a>Crear una definición de plantilla de compilación de Hola
1. Abra el proyecto de equipo en Visual Studio Team Services.
2. Seleccione hello **generar** ficha.
3. Verde Hola seleccione  **+**  firmar toocreate una nueva definición de compilación.
4. En el cuadro de diálogo de Hola que se abre, seleccione **aplicación de Azure Service Fabric** en hello **generar** categoría de la plantilla.
5. Seleccione **Siguiente**.
6. Seleccione el repositorio de Hola y bifurcación asociado a la aplicación de Service Fabric.
7. Seleccione la cola del agente de hello desea toouse. Se admiten agentes hospedados.
8. Seleccione **Crear**.
9. Guardar la definición de compilación de Hola y proporcione un nombre.
10. Hola párrafo siguiente es una descripción de los pasos de compilación Hola generado por la plantilla de hello:

| Paso de compilación | Descripción |
| --- | --- |
| NuGet restore |Restaura los paquetes de NuGet de hello para la solución de Hola. |
| Build solution \*.sln (Compilar solución *.sln) |Compila la solución completa de Hola. |
| Build solution \*.sfproj (Compilar solución *.sfproj) |Se genera el paquete de aplicación de Service Fabric Hola que es usado toodeploy Hola aplicación. ubicación del paquete de aplicación Hello es toobe especificado en el directorio de artefactos de la compilación de Hola. |
| Update Service Fabric App Versions (Actualizar versiones de la aplicación de Service Fabric) |Actualiza valores de versión de Hola contenidos en tooallow de archivos de manifiesto del paquete de aplicación Hola para compatibilidad con la actualización. Vea hello [página de documentación de tarea](https://go.microsoft.com/fwlink/?LinkId=820529) para obtener más información. |
| Copiar archivos |Hola copias publicar perfil y toobe de artefactos de la compilación de aplicaciones parámetros archivos toohello utilizado para la implementación. |
| Publish Artifact (Publicar artefacto) |Publica los artefactos de la compilación de Hola. Permite una definición de la versión de artefactos de la compilación de tooconsume Hola. |

### <a name="verify-hello-default-set-of-tasks"></a>Compruebe el conjunto predeterminado de Hola de tareas
1. Comprobar hello **solución** campo de entrada para hello **restauración de NuGet** y **compilar solución** pasos de compilación.  De forma predeterminada, estos pasos de compilación ejecutar con todos los archivos de solución que se encuentran en el repositorio de hello asociado.  Si solo desea hello toooperate de definición de compilación en uno de los archivos de solución, necesita el archivo toothat ruta de acceso de tooexplicitly actualización Hola.
2. Comprobar hello **solución** campo de entrada para hello **empaquetar aplicación** paso de compilación.  De forma predeterminada, este paso de compilación supone que solo un proyecto de aplicación de tejido de servicio (.sfproj) existe en el repositorio de Hola.  Si tiene varios archivos de este tipo en el repositorio y desea tootarget solo uno de ellos para esta definición de compilación, necesita el archivo toothat ruta de acceso de tooexplicitly actualización Hola.  Si desea toopackage aplicación de varios proyectos en el repositorio, necesita toocreate adicionales **Visual Studio Build** los pasos de la definición de compilación de Hola que cada destino de un proyecto de aplicación.  A continuación, sería necesario también hello tooupdate **argumentos de MSBuild** campo para cada uno de los pasos de compilación para que la ubicación del paquete hello es único para cada uno de ellos.
3. Compruebe el comportamiento de las versiones de hello definido en hello **versiones de actualización de Service Fabric aplicación** paso de compilación.  De forma predeterminada, este paso de compilación agrega valores de versión tooall número de Hola de compilación en archivos de manifiesto del paquete de aplicación Hola. Vea hello [página de documentación de tarea](https://go.microsoft.com/fwlink/?LinkId=820529) para obtener más información. Esto es útil para admitir la actualización de la aplicación debido a que la implementación de cada actualización requiere diferentes valores de versión de la implementación anterior Hola. Si no está previsto toouse actualización de la aplicación en el flujo de trabajo, puede deshabilitar este paso de compilación. Debe deshabilitarse si su intención es tooproduce una compilación que puede ser toooverwrite usa una aplicación existente de Service Fabric. se produce un error en la implementación de Hello si versión Hola de aplicación Hola generado por la compilación de hello no coincide con la versión de Hola de aplicación hello en clúster de Hola.
4. Si la solución contiene un proyecto de .NET Core, debe asegurarse de que la definición de compilación contiene un paso de compilación que restaura las dependencias de hello:
   1. Seleccione **Agregar el paso de compilación**.
   2. Busque hello **de línea de comandos** de tareas dentro de la pestaña de utilidad hello y haga clic en el botón Agregar.
   3. Para los campos de entrada de la tarea de hello, utilice Hola siguientes valores:
   4. Herramienta: dotnet
   5. Argumentos: restore
   6. Arrastre la tarea hello para que esté inmediatamente después de hello **restauración de NuGet** paso.
5. Guardar los cambios que haya realizado la definición de compilación toohello.

### <a name="try-it"></a>Pruébelo
Seleccione **poner en cola compilación** toomanually iniciar una compilación. Las compilaciones también se desencadenan después de una inserción o una protección. Una vez que haya comprobado que la compilación Hola se ejecuta correctamente, ahora puede mover en toodefining una definición de la versión que implementa el clúster de tooa de aplicación.

## <a name="create-a-release-definition"></a>Creación de una definición de versión
Una definición de versión de Team Services describe un flujo de trabajo compuesto por una serie de tareas que se ejecutan de manera secuencial. objetivo de Hola de definición de la versión de Hola que va a crear es tootake un paquete de aplicación e implementarla tooa clúster. Cuando se usan juntos, Hola definición de compilación y definición de versión puede ejecutar el flujo de trabajo completo de Hola desde a partir de tooending de archivos de origen con una aplicación en ejecución en el clúster. Obtenga más información sobre las [definiciones de versión](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition)de Team Services.

### <a name="create-a-definition-from-hello-release-template"></a>Crear una definición de plantilla de versión de Hola
1. Abra el proyecto en Visual Studio Team Services.
2. Seleccione hello **versión** ficha.
3. Seleccione Hola verde  **+**  toocreate una nueva versión de definición de sesión y seleccione **crear versión definición** en el menú de Hola.
4. En el cuadro de diálogo de Hola que se abre, seleccione **Azure Service Fabric implementación** en hello **implementación** categoría de la plantilla.
5. Seleccione **Siguiente**.
6. Seleccione definición de compilación de Hola que quiera toouse como origen de Hola de esta definición de versión.  definición de compilación de Hello versión definición referencias Hola artefactos generados por hello seleccionado.
7. Comprobar hello **implementación continua** casilla de verificación si desea toohave Team Services automáticamente crear una nueva versión e implementar la aplicación de Service Fabric hello siempre que se complete una compilación.
8. Seleccione la cola del agente de hello desea toouse. Se admiten agentes hospedados.
9. Seleccione **Crear**.
10. Editar nombre de la definición de hello haciendo clic en el icono de lápiz Hola al principio de Hola de página de Hola.
11. Seleccione hello toowhich de clúster se debe implementar la aplicación de hello **conexión de clúster** campo de entrada de tarea hello. conexión de clúster de Hello proporciona información necesarios de Hola que permite Hola implementación tarea tooconnect toohello clúster. Si aún no dispone de una conexión de clúster para el clúster, seleccione hello **administrar** hipervínculo siguiente toohello campo tooadd uno. En página de Hola que se abre, realice Hola pasos:
    1. Seleccione **nuevo extremo de servicio** y, a continuación, seleccione **Azure Service Fabric** en el menú de Hola.
    2. Seleccione el tipo de Hola de autenticación utilizado por clúster Hola objetivo de este punto de conexión.
    3. Definir un nombre para la conexión en hello **nombre de la conexión** campo.  Normalmente, se debe utilizar el nombre de hello del clúster.
    4. Definir la URL de extremo de conexión de cliente de Hola Hola **punto de conexión de clúster** campo.  Ejemplo: tcp://contoso.westus.cloudapp.azure.com:19000.
    5. Para las credenciales de Azure Active Directory, definir las credenciales de hello desea toouse tooconnect toohello clúster Hola **nombre de usuario** y **contraseña** campos.
    6. Para la autenticación basada en certificado, definir codificación Hola Base64 del archivo de certificado de cliente de Hola Hola **certificado de cliente** campo.  Consulte la ventana emergente de Ayuda de hello en ese campo para obtener información acerca de cómo tooget ese valor.  Si el certificado está protegido por contraseña, Definir contraseña Hola Hola **contraseña** campo.
    7. Confirme los cambios haciendo clic en **Aceptar**. Después de navegar tooyour back-definición de la versión, haga clic en el icono de actualización de hello en hello **conexión de clúster** que acaba de agregar el punto de conexión de Hola a toosee de campo.
12. Guardar la definición de la versión de Hola.

> [!NOTE]
> Cuentas de Microsoft (por ejemplo, @hotmail.com o @outlook.com) no se admiten con la autenticación de Azure Active Directory.
> 
> 

definición de Hola que se crea se compone de una tarea de tipo **implementación de aplicación de servicio de Fabric**. Vea hello [página de documentación de tarea](https://go.microsoft.com/fwlink/?LinkId=820528) para obtener más información acerca de esta tarea.

### <a name="verify-hello-template-defaults"></a>Compruebe los valores predeterminados de hello plantilla
1. Comprobar hello **un perfil de publicación** campo de entrada para hello **implementar aplicación de servicio tejido** tarea. De forma predeterminada, este campo hace referencia a un perfil de publicación denominado Cloud.xml contenidos en los artefactos de la compilación de Hola. Si desea que un perfil de publicación diferentes tooreference o compilación de hello contiene varios paquetes de aplicación en sus artefactos, se necesita tooupdate Hola ruta adecuadamente.
2. Comprobar hello **paquete de aplicación** campo de entrada para hello **implementar aplicación de servicio tejido** tarea. De forma predeterminada, este campo hace referencia a utilizado en la plantilla de definición de compilación de hello de la ruta del paquete de aplicación de Hola de forma predeterminada.  Si ha modificado la ruta de acceso de paquete de aplicación de hello predeterminada en hello definición de compilación, deberá ruta de acceso de tooupdate Hola adecuadamente aquí también.

### <a name="try-it"></a>Pruébelo
Seleccione **crear versión** de hello **versión** toomanually de menú del botón Crear una versión. En el cuadro de diálogo de Hola que se abre, seleccione la compilación de Hola que desee toobase versión de hello en y, a continuación, haga clic en **crear**. Si ha habilitado la implementación continua, las versiones se creará automáticamente cuando completa la definición de compilación de hello asociado una compilación.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de la integración continua con aplicaciones de Service Fabric, leer Hola siguientes artículos:

* [Página de inicio de la documentación de Team Services](https://www.visualstudio.com/docs/overview)
* [Administración de compilaciones en Team Services](https://www.visualstudio.com/docs/build/overview)
* [Administración de versiones en Team Services](https://www.visualstudio.com/docs/release/overview)

