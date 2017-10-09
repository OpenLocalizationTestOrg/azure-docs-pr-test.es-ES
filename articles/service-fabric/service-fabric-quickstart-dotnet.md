---
title: "aaaCreate una aplicación .NET Service Fabric en Azure | Documentos de Microsoft"
description: "Crear una aplicación .NET de Azure con el ejemplo de inicio rápido de Service Fabric Hola."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: 20ef88dbf9fb0def31234ef05679a19009b9b529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-service-fabric-application-in-azure"></a>Crear una aplicación .NET de Service Fabric en Azure
Azure Service Fabric es una plataforma de sistemas distribuidos para implementar y administrar microservicios y contenedores escalables y confiables. 

Este tutorial rápido muestra cómo toodeploy su primer tooService de aplicación .NET tejido. Cuando haya terminado, tiene una aplicación con un front-end que guarda los resultados de la votos en un servicio back-end con estado en el clúster de hello web de ASP.NET Core derecho a voto.

![Captura de pantalla de la aplicación](./media/service-fabric-quickstart-dotnet/application-screenshot.png)

Mediante el uso de esta aplicación, aprenderá a hacer lo siguiente:
> [!div class="checklist"]
> * Crear una aplicación con .NET y Service Fabric
> * Usar ASP.NET Core como front-end web
> * Almacenar datos de la aplicación en un servicio con estado
> * Depurar la aplicación de forma local
> * Implementar Hola aplicación tooa clúster en Azure
> * Aplicación Hola de escalabilidad horizontal en varios nodos
> * Realizar una actualización gradual de aplicaciones

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tutorial rápido:
1. [Instalar Visual Studio de 2017](https://www.visualstudio.com/) con hello **desarrollo Azure** y **ASP.NET y desarrollo web** las cargas de trabajo.
2. [Instalación de Git](https://git-scm.com/)
3. [Instalar SDK del servicio de Microsoft Azure Fabric Hola](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK)
4. Ejecute hello después comando tooenable Visual Studio toodeploy toohello Service Fabric clúster local:
    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
    ```

## <a name="download-hello-sample"></a>Descargar el ejemplo hello
En una ventana de comandos, ejecute hello después comando tooclone Hola ejemplo aplicación repositorio tooyour equipo local.
```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="run-hello-application-locally"></a>Ejecutar la aplicación hello localmente
Haga clic en el icono de Visual Studio Hola Hola menú Inicio y elija **ejecutar como administrador**. En orden tooattach Hola depurador tooyour los servicios, debe toorun Visual Studio como administrador.

Abra hello **Voting.sln** solución de Visual Studio del repositorio de Hola se clonó.

aplicación de hello toodeploy, presione **F5**.

> [!NOTE]
> Hola la primera vez que se ejecute e implementa aplicación hello, Visual Studio crea un clúster local para la depuración. Es posible que esta operación tarde un tiempo. estado de creación de clúster de Hola se muestra en la ventana de salida de Visual Studio de hello.

Una vez completada la implementación de hello, inicie un explorador y abrir esta página: `http://localhost:8080` -web Hola front-end de la aplicación hello.

![Front-end de la aplicación](./media/service-fabric-quickstart-dotnet/application-screenshot-new.png)

Ahora puede agregar una serie de opciones de votación y empezar a recibir votos. Hola ejecuta la aplicación y almacena todos los datos en el clúster de Service Fabric, sin necesidad de Hola de una base de datos independiente.

## <a name="walk-through-hello-voting-sample-application"></a>Recorrer Hola votos de aplicación de ejemplo
Hola votos aplicación consta de dos servicios:
- Servicio de front-end (VotingWeb) Web: An ASP.NET Core servicio front-end, que sirve de página web de Hola y expone web toocommunicate de API con el servicio back-end de Hola.
- Servicio de back-end (VotingData)-servicio de web de un núcleo de ASP.NET, que expone un voto de hello API toostore da como resultado un diccionario confiable se conserva en el disco.

![Diagrama de aplicaciones](./media/service-fabric-quickstart-dotnet/application-diagram.png)

Eventos se producen cuando votar Hola Hola de aplicaciones siguientes:
1. JavaScript envía API web solicitud toohello para hello voto en el servicio front-end web de hello como una solicitud PUT de HTTP.

2. servicio front-end de Hello web utiliza un proxy toolocate y reenviar un servicio de back-end de toohello de solicitud HTTP PUT.

3. servicio de back-end de Hello toma la solicitud entrante de Hola y Hola almacenes actualiza resultado en un diccionario confiable, que obtiene toomultiple replicada nodos en clúster de Hola y se conserva en el disco. Datos de todas las aplicación Hola se almacenan en el clúster de hello, por lo que no se necesita ninguna base de datos.

## <a name="debug-in-visual-studio"></a>Depurar en Visual Studio
Cuando se depura una aplicación en Visual Studio, se usa un clúster de desarrollo de Service Fabric local. Tener Hola opción tooadjust su escenario de tooyour de experiencia de depuración. En esta aplicación, almacenamos los datos en nuestro servicio back-end mediante un diccionario confiable. Visual Studio quita aplicación hello de forma predeterminada cuando se detiene el depurador Hola. Quitar aplicación hello hace que los datos de hello en hello back-end puede quitar tooalso de servicio. datos de hello toopersist entre las sesiones de depuración, puede cambiar hello **modo de depuración de la aplicación** como una propiedad en hello **votación** proyecto en Visual Studio.

toolook en lo que sucede en el código de hello, Hola completa pasos:
1. Hola abierto **VotesController.cs** de archivos y establecer un punto de interrupción en web Hola API **colocar** método (línea 47): puede buscar archivo Hola Hola el Explorador de soluciones en Visual Studio.

2. Abra hello **VoteDataController.cs** de archivos y establezca un punto de interrupción en esta API de web **colocar** método (línea 50).

3. Volver atrás toohello explorador y haga clic en una opción de votación o agregue una nueva opción de voto. Se alcanza el primer punto de interrupción hello en el controlador de api de hello web front-end.
    - Esto es donde hello JavaScript en el Explorador de hello envía un controlador de API web de solicitud toohello en el servicio front-end de Hola.
    
    ![Incorporación del servicio front-end de voto](./media/service-fabric-quickstart-dotnet/addvote-frontend.png)

    - Primero creamos Hola URL toohello ReverseProxy para nuestro servicio back-end **(1)**.
    - A continuación, enviamos Hola solicitud PUT de HTTP toohello ReverseProxy **(2)**.
    - Por último, hello se devuelva la respuesta de Hola de hello servicio back-end toohello cliente **(3)**.

4. Presione **F5** toocontinue
    - Ya estás hello en punto de interrupción en el servicio de back-end de Hola.
    
    ![Incorporación del servicio back-end de voto](./media/service-fabric-quickstart-dotnet/addvote-backend.png)

    - Primera línea de hello en método hello **(1)** , usamos hello `StateManager` tooget o agregar un diccionario confiable denominado `counts`.
    - Todas las interacciones con valores de un diccionario confiable requieren una transacción. Esta instrucción using **(2)** crea dicha transacción.
    - En transacciones de hello, actualizamos, a continuación, valor de Hola de clave relevante Hola Hola votar la opción y confirmaciones Hola operación **(3)**. Una vez Hola confirme método devuelve, Hola datos se actualizan en el diccionario de Hola y replican tooother nodos de clúster de Hola. datos de Hello ahora se almacenan de forma segura en clúster de Hola y servicio back-end de hello puede conmutar por error nodos tooother, sigue teniendo datos Hola disponibles.
5. Presione **F5** toocontinue

Hola toostop depuración de sesión, presione **MAYÚS+F5**.

## <a name="deploy-hello-application-tooazure"></a>Implementar Hola aplicación tooAzure
clúster de tooa de toodeploy Hola aplicación en Azure, puede elegir toocreate su propio clúster o use un clúster de entidad.

Clústeres de entidades son libres, por tiempo limitado para los clústeres Service Fabric hospedado en Azure y ejecutar, equipo de Service Fabric Hola que cualquiera puede implementar aplicaciones y obtener información acerca de la plataforma de Hola. tooget acceso tooa clúster de entidad, [siga las instrucciones de hello](http://aka.ms/tryservicefabric). 

Para obtener información sobre cómo crear su propio clúster, vea [Creación del primer clúster de Service Fabric en Azure](service-fabric-get-started-azure-cluster.md).

> [!Note]
> servicio de Hello web front-end es toolisten configurado en el puerto 8080 para el tráfico entrante. Asegúrese de que dicho puerto está abierto en el clúster. Si usas Hola entidad clúster, este puerto está abierto.
>

### <a name="deploy-hello-application-using-visual-studio"></a>Implementar la aplicación hello mediante Visual Studio
Ahora que la aplicación hello está listo, puede implementarlo tooa clúster directamente desde Visual Studio.

1. Haga clic en **votación** en hello en el Explorador de soluciones y elija **publicar**. aparece el cuadro de diálogo de publicación de Hola.

    ![Cuadro de diálogo de publicación](./media/service-fabric-quickstart-dotnet/publish-app.png)

2. Escriba Hola extremo de la conexión de clúster Hola Hola **extremo de la conexión** campo y haga clic en **publicar**. Al registrarse para hello clúster de entidad, Hola extremo de la conexión se proporciona en el Explorador de Hola. por ejemplo, `winh1x87d1d.westus.cloudapp.azure.com:19000`.

3. Abra un explorador y escriba en la dirección del clúster hello - por ejemplo, `http://winh1x87d1d.westus.cloudapp.azure.com`. Ahora debería ver aplicación Hola que se ejecuta en el clúster de hello en Azure.

![Front-end de la aplicación](./media/service-fabric-quickstart-dotnet/application-screenshot-new-azure.png)

## <a name="scale-applications-and-services-in-a-cluster"></a>Escalar aplicaciones y servicios en un clúster
Servicios de Service Fabric fácilmente se pueden escalar a través de un tooaccommodate de clúster si hay cambios en la carga de hello en los servicios de Hola. Escalar un servicio cambiando Hola número de instancias que se ejecutan en el clúster de Hola. Existen varias formas de escalar los servicios, ya sea mediante scripts o comandos de PowerShell o la CLI de Service Fabric (sfctl). En este ejemplo, usamos Service Fabric Explorer.

Explorador de Service Fabric se ejecuta en todos los clústeres de Service Fabric y puede tener acceso desde un explorador, al examinar el puerto de administración de clústeres HTTP toohello (19080), por ejemplo, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.

Hola tooscale servicio front-end web, Hola lo siguiente:

1. Abra Service Fabric Explorer en el clúster, por ejemplo, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.
2. Haga clic en toohello siguiente de puntos suspensivos (tres puntos) de hello **fabric: / votación/VotingWeb** nodo en Hola treeview y elija **servicio escala**.

    ![Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scale.png)

    Ahora puede elegir el número de hello tooscale de instancias de servicio de hello web front-end.

3. Cambiar el número de hello demasiado**2** y haga clic en **servicio escala**.
4. Haga clic en hello **fabric: / votación/VotingWeb** nodo en vista de árbol de Hola y Expandir nodo de partición de hello (representado por un GUID).

    ![Escalar servicio de Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scaled-service.png)

    Ahora puede ver que servicio hello tiene dos instancias, y en la vista de árbol de hello verá los nodos que se ejecutan las instancias de hello en.

Por esta tarea de administración simple, se duplican recursos Hola disponibles para nuestra carga de usuarios de tooprocess servicio front-end. Es importante toounderstand que no se necesitan varias instancias de un toohave de servicio ejecutan de forma confiable. Si se produce un error en un servicio, Service Fabric asegura que una nueva instancia de servicio se ejecuta en el clúster de Hola.

## <a name="perform-a-rolling-application-upgrade"></a>Realizar una actualización gradual de aplicaciones
Al implementar la nueva aplicación de tooyour de actualizaciones, Service Fabric implementa Hola update de forma segura. Las actualizaciones graduales eliminan el tiempo de inactividad durante el proceso de actualización y permiten la reversión automática en caso de que se produzcan errores.

tooupgrade Hola aplicación, Hola siguientes:

1. Abra hello **Index.cshtml** archivo en Visual Studio, puede buscar archivo Hola Hola el Explorador de soluciones en Visual Studio.
2. Cambiar el título de hello en la página de hello mediante la adición de texto: por ejemplo.
    ```html
        <div class="col-xs-8 col-xs-offset-2 text-center">
            <h2>Service Fabric Voting Sample v2</h2>
        </div>
    ```
3. Guarde el archivo hello.
4. Haga clic en **votación** en hello en el Explorador de soluciones y elija **publicar**. aparece el cuadro de diálogo de publicación de Hola.
5. Haga clic en hello **manifiesto versión** versión de hello toochange de botón de servicio de Hola y de aplicación.
6. Cambiar la versión de Hola de hello **código** elemento bajo **VotingWebPkg** demasiado "2.0.0", por ejemplo y haga clic en **guardar**.

    ![Cuadro de diálogo para cambiar versión](./media/service-fabric-quickstart-dotnet/change-version.png)
7. Hola **publicar aplicación de servicio de Fabric** cuadro de diálogo, casilla de verificación Hola Hola actualización aplicación y haga clic en **publicar**.

    ![Configuración de actualización del cuadro de diálogo de publicación](./media/service-fabric-quickstart-dotnet/upgrade-app.png)
8. Abra el explorador y busque toohello dirección de clúster en el puerto 19080 - por ejemplo, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.
9. Haga clic en hello **aplicaciones** nodo en la vista de árbol de hello y, a continuación, **las actualizaciones en curso** en el panel derecho de Hola. Verá cómo se agrupa el actualización Hola a través de dominios de actualización de hello en el clúster, asegurándose de que cada dominio es correcto antes de continuar toohello a continuación.
    ![Vista de actualización en Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/upgrading.png)

    Service Fabric hace actualizaciones seguro espera dos minutos después de actualizar el servicio de hello en cada nodo de clúster de Hola. Esperar Hola toda actualización tootake ocho minutos aproximadamente.

10. Mientras se ejecuta la actualización de hello, todavía puede usar aplicación hello. Dado que tiene dos instancias de servicio de Hola que se ejecuta en el clúster de hello, algunas de las solicitudes pueden obtener una versión actualizada de la aplicación hello, mientras otros todavía pueden obtener una versión antigua Hola.

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha aprendido a hacer lo siguiente:

> [!div class="checklist"]
> * Crear una aplicación con .NET y Service Fabric
> * Usar ASP.NET Core como front-end web
> * Almacenar datos de la aplicación en un servicio con estado
> * Depurar la aplicación de forma local
> * Implementar Hola aplicación tooa clúster en Azure
> * Aplicación Hola de escalabilidad horizontal en varios nodos
> * Realizar una actualización gradual de aplicaciones

toolearn más información acerca de Service Fabric y. NET, eche un vistazo a este tutorial:
> [!div class="nextstepaction"]
> [Aplicación .NET en Service Fabric](service-fabric-tutorial-create-dotnet-app.md)