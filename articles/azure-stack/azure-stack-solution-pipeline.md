---
title: "aaaDeploy su aplicación tooAzure y la pila de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy aplicaciones tooAzure y pila de Azure con un elemento de configuración/CD híbrido de canalización."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: helaw
ms.custom: mvc
ms.openlocfilehash: a468d7da6f34d04809ee98463a8c4146da581015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-apps-tooazure-and-azure-stack"></a>Implementar aplicaciones tooAzure y la pila de Azure
Híbrido [integración continua](https://www.visualstudio.com/learn/what-is-continuous-integration/)/[la entrega continua](https://www.visualstudio.com/learn/what-is-continuous-delivery/)canalización (CI/CD) le permite toobuild, probar e implementar sus nubes de toomultiple de aplicación.  En este tutorial, va a crear un toolearn de entorno de ejemplo cómo puede ayudarle a una canalización de CI/CD híbrida:
 
> [!div class="checklist"]
> * Iniciar una nueva compilación basada en el repositorio de código confirmaciones tooyour Visual Studio Team Services (VSTS).
> * Implementar automáticamente su tooAzure de código recién creado para las pruebas de aceptación de usuario.
> * Una vez que el código ha pasado la prueba, implementar automáticamente tooAzure pila. 


## <a name="prerequisites"></a>Requisitos previos
Algunos componentes son necesario toobuild una canalización de CI/CD híbrida y pueden tardar algún tiempo tooprepare.  Si ya tiene algunos de estos componentes, asegúrese de que cumplen los requisitos de hello antes de comenzar.

En este tema también se da por supuesto que tiene algunos conocimientos de Azure y Azure Stack. Si desea que toolearn más antes de continuar, ser seguro toostart con estos temas:

- [Introducción tooAzure](https://docs.microsoft.com/azure/fundamentals-introduction-to-azure)
- [Conceptos clave de Azure Stack](azure-stack-key-features.md)

### <a name="azure"></a>Azure
 - Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.
 - Cree una [aplicación web](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md) y configúrela para [publicación FTP](../app-service-web/app-service-deploy-ftp.md).  Tome nota de Hola nuevo de dirección URL de aplicación Web, tal como se utiliza más adelante.


### <a name="azure-stack"></a>Azure Stack
 - [Implementación de Azure Stack](azure-stack-run-powershell-script.md).  instalación de Hello normalmente tarda unos toocomplete horas, por lo que planear en consecuencia.
 - Implementar [servicio de aplicaciones](azure-stack-app-service-deploy.md) tooAzure pila de servicios de PaaS.
 - Cree una aplicación web y configúrela para [publicación FTP](azure-stack-app-service-enable-ftp.md).  Tome nota de Hola nuevo de dirección URL de aplicación Web, tal como se utiliza más adelante.  

### <a name="developer-tools"></a>Herramientas para desarrolladores
 - Cree un [área de trabajo de VSTS](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).  proceso de registro de Hello crea un proyecto denominado "MyFirstProject."  
 - [Instalar Visual Studio de 2017](https://docs.microsoft.com/visualstudio/install/install-visual-studio) y [tooVSTS de inicio de sesión](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#connect-and-share-code-from-visual-studio)
 - Conectar a proyecto toohello y [clonar localmente](https://www.visualstudio.com/docs/git/gitquickstart).
 - Cree un [grupo de agentes](https://www.visualstudio.com/docs/build/concepts/agents/pools-queues#creating-agent-pools-and-queues) en VSTS.
 - Instalar Visual Studio e implementar un [agente de compilación de VSTS](https://www.visualstudio.com/docs/build/actions/agents/v2-windows) tooa virtual machine en la pila de Azure. 
 

## <a name="create-app--push-toovsts"></a>Crear la aplicación e inserción tooVSTS

### <a name="create-application"></a>Creación de la aplicación
En esta sección, crear una aplicación ASP.NET simple y empújelo tooVSTS.  Estos pasos representan el flujo de trabajo de saludo habitual del desarrollador y pueden adaptar para los lenguajes y herramientas de desarrollo. 

1.  Abra Visual Studio.
2.  De hello espacio de Team Explorer y **soluciones...**  área, haga clic en **nuevo**.
3.  Seleccione **Visual C#** > **Web** > **Aplicación web ASP.NET (.NET Framework)**.
4.  Proporcione un nombre para la aplicación hello y haga clic en **Aceptar**.
5.  En la siguiente pantalla de bienvenida, mantenga los valores predeterminados de hello (formularios Web forms) y haga clic en **Aceptar**.

### <a name="commit-and-push-changes-toovsts"></a>Confirme e inserte cambios tooVSTS
1.  Con Team Explorer en Visual Studio, seleccione la lista desplegable de Hola y haga clic en **cambios**.
2.  Agregue un mensaje de confirmación y seleccione **Confirmar todo**. Puede ser solicitadas toosave Hola solución archivo, haga clic en Sí toosave todos.
3.  Una vez confirmado, Visual Studio ofrece proyecto tooyour de toosync cambios. Seleccione **Sincronizar**.

    ![pantalla de confirmación de bienvenida de imagen que muestra una vez completada la confirmación](./media/azure-stack-solution-pipeline/image1.png)

4.  En la pestaña de la sincronización de hello, en *saliente*, verá que la confirmación nuevo.  Seleccione **Push** toosynchronize Hola cambiar tooVSTS.

    ![imagen que muestra los pasos de sincronización](./media/azure-stack-solution-pipeline/image2.png)

### <a name="review-code-in-vsts"></a>Revisión del código en VSTS
Una vez se ha confirmado un cambio e inserta tooVSTS, compruebe el código desde el portal VSTS Hola.  Seleccione **código**y, a continuación, **archivos** desde el menú desplegable de Hola.  Puede ver la solución de hello creada.

## <a name="create-build-definition"></a>Creación de la definición de compilación
proceso de compilación de Hello define cómo la aplicación se compila y empaqueta para su implementación en cada confirmación de cambios de código. En nuestro ejemplo, utilizamos Hola incluida plantilla tooconfigure Hola proceso de compilación para una aplicación ASP.NET, aunque esta configuración podría ser adaptada dependiendo de la aplicación.

1.  Inicie sesión en tooyour área de trabajo VSTS desde un explorador web.
2.  En el banner de hello, seleccione **compilar & versión** y, a continuación, **genera**.
3.  Haga clic en **+ Nueva definición**.
4.  En la lista Hola de plantillas, seleccione **ASP.NET (versión preliminar)** y seleccione **aplicar**.
5.  Modificar hello *argumentos de MSBuild* campo *generar solución* paso a paso para:

    `/p:DeployOnBuild=True /p:WebPublishMethod=FileSystem /p:DeployDefaultTarget=WebPublish /p:publishUrl="$(build.artifactstagingdirectory)\\"`

6.  Seleccione hello **opciones** ficha y seleccione Hola la cola del agente para hello agente de compilación que haya implementado tooa máquina virtual en la pila de Azure. 
7.  Seleccione hello **desencadenadores** y a habilitar **integración continua**.
7.  Haga clic en **Guardar & cola** y, a continuación, seleccione **guardar** de lista desplegable de Hola. 

## <a name="create-release-definition"></a>Creación de la definición de versión
proceso de lanzamiento de Hello define cómo compilaciones del paso anterior Hola son entorno tooan implementado.  En este tutorial, publicamos nuestra aplicación ASP.NET con FTP tooan aplicación Web de Azure. tooconfigure un tooAzure versión, use Hola pasos:

1.  En la pancarta VSTS hello, seleccione **compilar & versión** y, a continuación, **versiones**.
2.  Haga clic en hello verde **+ nueva definición**.
3.  Seleccione **Vacía** y haga clic en **Siguiente**.
4.  Casilla de Hola para *implementación continua*y, a continuación, haga clic en **crear**.

Ahora que ha creado una definición de versión vacío y vinculada toohello compilación, agregamos pasos para hello entorno de Azure:

1.  Haga clic en hello verde  **+**  tooadd tareas.
2.  Seleccione **todos los**y, a continuación, en lista de hello, agregue **FTP cargar** y seleccione **cerrar**.
3.  Seleccione hello **FTP cargar** tarea se acaba de agregar y configurar Hola parámetros siguientes:
    
    | Parámetro | Valor |
    | ----- | ----- |
    |Método de autenticación| Escribir credenciales|
    |Dirección URL del servidor | Dirección URL de FTP de la aplicación web recuperada de Azure Portal |
    |Nombre de usuario | Nombre de usuario que configuró al crear las credenciales de FTP para la aplicación web |
    |Password | Contraseña que creó al establecer las credenciales FTP para la aplicación web|
    |Directorio de origen | $(System.DefaultWorkingDirectory)\**\ |
    |Directorio remoto | /site/wwwroot/ |
    |Mantener las rutas de acceso de los archivos | Habilitado (activado)|

4.  Haga clic en **Guardar**

Por último, configure Hola versión definición toouse Hola agente grupo que contiene a agente Hola implementada mediante Hola pasos:
1.  Seleccione la definición de la versión de Hola y haga clic en **editar**.
2.  Seleccione **se ejecutan en agente** de la columna central Hola.  En la columna derecha de hello, seleccione la cola de agente de Hola que contiene el agente de compilación de hello ejecutando en la pila de Azure.  
    ![configuración de imagen que muestra de cola específica de versión definición toouse](./media/azure-stack-solution-pipeline/image3.png)


## <a name="deploy-your-app-tooazure"></a>Implementar la aplicación tooAzure
Este paso usa la recién creado CI/CD canalización toodeploy Hola ASP.NET aplicación tooa aplicación Web en Azure. 

1.  En la pancarta de hello en VSTS, seleccione **compilar & versión**y, a continuación, seleccione **genera**.
2.  Haga clic en **...**  en hello creado previamente de definición de compilación y seleccione **poner nueva compilación en cola**.
3.  Acepte los valores predeterminados de Hola y haga clic en **Aceptar**.  compilación de Hello comienza y muestra el progreso.
4.  Una vez completada la compilación de hello, puede realizar seguimiento del estado Hola seleccionando **compilar & versión** y seleccionando **versiones**.
5.  Una vez completada la compilación de hello, visite sitio Web de hello mediante dirección URL de Hola se indicó al crear la aplicación Web de Hola.    


## <a name="add-azure-stack-toopipeline"></a>Agregar toopipeline de pila de Azure
Ahora que ha probado la canalización de CI/CD mediante la implementación de tooAzure, es hora tooadd canalización toohello de pila de Azure.  Hola pasos, cree un nuevo entorno y agregar una tarea FTP cargar, toodeploy la pila de aplicación tooAzure.  También agregará un aprobador de versión, que actúa como un toosimulate de manera "firmar" en un tooAzure de versión de código pila.  

1.  En la definición de la versión de hello, seleccione **+ agregar entorno** y **crear nuevo entorno**.
2.  Seleccione **Vacío** y haga clic en **Siguiente**.
3.  Seleccione **Usuarios específicos** y especifique su cuenta.  Seleccione **Crear**.
4.  Cambiar el nombre de entorno de hello seleccionando nombre existente de Hola y escribiendo *Azure pila*.
5.  Ahora, selección Hola entorno de pila de Azure, a continuación, seleccione **agregar tareas**.
6.  Seleccione hello **FTP cargar** de tareas y seleccione **agregar**, a continuación, seleccione **cerrar**.


### <a name="configure-ftp-task"></a>Configuración de la tarea FTP
Ahora que ha creado una versión, configurará los pasos de hello necesarios para toohello publicar la aplicación Web en la pila de Azure.  Al igual que configuró tarea de carga de FTP de Hola para Azure, configurar tarea hello para la pila de Azure:

1.  Seleccione hello **FTP cargar** tarea se acaba de agregar y configurar Hola parámetros siguientes:
    
    | Parámetro | Valor |
    | -----     | ----- |
    |Método de autenticación| Escribir credenciales|
    |Dirección URL del servidor | Dirección URL de FTP de la aplicación web recuperada de Azure Stack Portal |
    |Nombre de usuario | Nombre de usuario que configuró al crear las credenciales de FTP para la aplicación web |
    |Password | Contraseña que creó al establecer las credenciales FTP para la aplicación web|
    |Directorio de origen | $(System.DefaultWorkingDirectory)\**\ |
    |Directorio remoto | /site/wwwroot/|
    |Mantener las rutas de acceso de los archivos | Habilitado (activado)|

2.  Haga clic en **Guardar**

Por último, configure Hola versión definición toouse Hola agente grupo que contiene a agente Hola implementada mediante Hola pasos:
1.  Seleccione la definición de la versión de Hola y haga clic en **editar**
2.  Seleccione **se ejecutan en agente** de la columna central Hola. En la columna derecha de hello, seleccione la cola de agente de Hola que contiene el agente de compilación de hello ejecutando en la pila de Azure.  
    ![configuración de imagen que muestra de cola específica de versión definición toouse](./media/azure-stack-solution-pipeline/image3.png)

## <a name="deploy-new-code"></a>Implementación de nuevo código
Ahora puede probar la canalización de CI/CD híbrida hello, con hello paso final publicación tooAzure pila.  En esta sección, modifique el pie de página del sitio de Hola y comience a través de la canalización de Hola.  Una vez completado, verá los cambios implementarán tooAzure para su revisión, a continuación, una vez que aprobar la versión de Hola, son publicado tooAzure pila.

1. En Visual Studio, abra hello *site.master* y cambie esta línea:
    
    `
        <p>&copy; <%: DateTime.Now.Year %> - My ASP.NET Application</p>
    `

    toothis:

    `
        <p>&copy; <%: DateTime.Now.Year %> - My ASP.NET Application delivered by VSTS, Azure, and Azure Stack</p>
    `
3.  Confirmar los cambios de Hola y tooVSTS de sincronización.  
4.  Desde el área de trabajo VSTS hello, comprobar el estado de generación de hello seleccionando **compilar & versión** > **de compilación**
5.  Verá una compilación en curso.  Haga doble clic en el estado de hello, y puede ver el progreso de compilación de Hola.  Una vez que vea "Build terminado" en la consola de hello, mover en la versión de Hola toocheck desde **compilar & versión** > **versión**.  Haga doble clic en la versión de Hola.
6.  Recibirá una notificación que indica que una versión requiere ser revisada. Compruebe Hola URL de la aplicación Web y los cambios nuevo Hola están presentes.  Aprobar versión de hello en VSTS.
    ![configuración de imagen que muestra de cola específica de versión definición toouse](./media/azure-stack-solution-pipeline/image4.png)
    
7.  Compruebe la publicación tooAzure que pila está completa visitando el sitio Web de hello mediante dirección URL de Hola se indicó al crear la aplicación Web de Hola.
    ![imagen que muestra la aplicación ASP.NET con el pie de página cambiado](./media/azure-stack-solution-pipeline/image5.png)


Ahora puede usar la nueva canalización de CI/CD híbrida como un bloque de creación para otros modelos de nube híbrida.

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha aprendido cómo toobuild un elemento de configuración/CD híbrido de canalización que:

> [!div class="checklist"]
> * Inicia una nueva compilación basada en el repositorio de código confirmaciones tooyour Visual Studio Team Services (VSTS).
> * Implementa automáticamente su tooAzure de código recién creado para las pruebas de aceptación de usuario.
> * Una vez que el código ha pasado la prueba, implementa automáticamente tooAzure pila. 

Ahora que tiene una canalización de CI/CD híbrida, continuar por aprendizaje cómo toodevelop aplicaciones para la pila de Azure.

> [!div class="nextstepaction"]
> [Desarrollo para Azure Stack](azure-stack-developer.md)


