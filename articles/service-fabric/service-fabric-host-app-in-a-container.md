---
title: "una aplicación de .NET en un tejido de servicio de contenedor tooAzure aaaDeploy | Documentos de Microsoft"
description: "Le enseña cómo toopackage una aplicación .NET en Visual Studio en un contenedor de Docker. A continuación, se implementa esta nueva aplicación de \"contenedor\" clúster de Service Fabric tooa."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: mikhegn
ms.openlocfilehash: 094b0e71d76b2e56ffb9b23638dd8154b3aff5fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a>Implementar una aplicación .NET en un tooAzure de contenedor de Windows Service Fabric

Este tutorial muestra cómo toodeploy una aplicación ASP.NET existente en un contenedor de Windows Azure.

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Creación de un proyecto de Docker en Visual Studio
> * Inclusión de una aplicación existente en un contenedor
> * Configuración de la integración continua con Visual Studio y VSTS

## <a name="prerequisites"></a>Requisitos previos

1. Instale [Docker CE for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) para poder ejecutar contenedores en Windows 10.
2. Familiarícese con hello [inicio rápido de contenedores de Windows 10][link-container-quickstart].
3. Descargar hello [Fabrikam fibra CallCenter] [ link-fabrikam-github] aplicación de ejemplo.
4. Instale [Azure PowerShell][link-azure-powershell-install].
5. Instalar hello [extensión de herramientas de entrega continua para Visual Studio de 2017][link-visualstudio-cd-extension]
6. Cree una [suscripción de Azure][link-azure-subscription] y una [cuenta de Visual Studio Team Services][link-vsts-account]. 
7. [Creación de un clúster en Azure](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-hello-application"></a>Incluya la aplicación hello

Ahora que tiene un [clúster de Service Fabric se ejecuta en Azure](service-fabric-tutorial-create-cluster-azure-ps.md) están listo toocreate e implementar una aplicación en contenedores. toostart ejecuta la aplicación en un contenedor, necesitamos tooadd **soporte técnico de Docker** toohello proyecto en Visual Studio. Cuando se agrega **soporte técnico de Docker** toohello aplicación, suceden dos cosas. En primer lugar, un _Dockerfile_ se agrega el proyecto toohello. Este nuevo archivo describe la forma de imagen de contenedor de hello toobe integrada. A continuación, segundo, un nuevo _crear docker_ se agrega el proyecto de solución toohello. nuevo proyecto Hello contiene algunos archivos de redacción de docker. Crear docker archivos pueden ser utilizado toodescribe cómo se ejecuta el contenedor de Hola.

Más información sobre cómo trabajara con las [herramientas de contenedor de Visual Studio][link-visualstudio-container-tools].

>[!NOTE]
>Si es Hola primera vez que se ejecutan las imágenes de contenedor de Windows en el equipo, Docker CE debe extraerlo imágenes de base de Hola para los contenedores. imágenes de Hola que se utilizan en este tutorial son 14 GB. Voy a ejecutarlo Hola después de imágenes del comando terminal toopull Hola base:
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a>Agregue compatibilidad con Docker

Abra hello [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] archivo en Visual Studio.

Menú contextual hello **FabrikamFiber.Web** proyecto > **agregar** > **compatibilidad con Docker**.

### <a name="add-support-for-sql"></a>Agregar compatibilidad con SQL

Esta aplicación utiliza SQL como proveedor de datos de hello, por lo que un servidor SQL server es necesario toorun Hola aplicación. Haga referencia a una imagen del contenedor de SQL Server en el archivo docker-compose.override.yml.

En Visual Studio, abra **el Explorador de soluciones**, buscar **redactar docker**y el archivo abierto hello **docker compose.override.yml**.

Navegue toohello `services:` nodo, agregue un nodo denominado `db:` que define la entrada de SQL Server de hello para el contenedor de Hola.

```yml
  db:
    image: microsoft/mssql-server-windows-developer
    environment:
      sa_password: "Password1"
      ACCEPT_EULA: "Y"
    ports:
      - "1433"
    healthcheck:
      test: [ "CMD", "sqlcmd", "-U", "sa", "-P", "Password1", "-Q", "select 1" ]
      interval: 1s
      retries: 20
```

>[!NOTE]
>Puede utilizar cualquier servidor SQL Server que prefiera para la depuración local, siempre que sea accesible desde el host. Sin embargo, **localdb** no admite la comunicación `container -> host`.

>[!WARNING]
>La ejecución de SQL Server en un contenedor no admite el almacenamiento de datos. Cuando se detiene el contenedor de hello, se borran los datos. No utilice esta configuración para producción.

Navegue toohello `fabrikamfiber.web:` nodo y agregar un nodo secundario denominado `depends_on:`. Esto garantiza que hello `db` servicio (contenedor de SQL Server de Hola) se inicia antes de que la aplicación web (fabrikamfiber.web).

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a>Actualizar configuración de hello web

Nuevo en hello **FabrikamFiber.Web** del proyecto, cadena de conexión de actualización Hola Hola **web.config** toopoint toohello SQL Server en el contenedor de hello, de archivos.

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
>Si desea toouse otro SQL Server al compilar una versión de compilación de la aplicación web, agregue otro archivo de web.release.config de tooyour de cadena de conexión.

### <a name="test-your-container"></a>Prueba del contenedor

Presione **F5** toorun y depuración aplicación hello en el contenedor.

Borde abre la página de inicio definido de la aplicación con la dirección IP de hello del contenedor de Hola de red interna de NAT de hello (normalmente 172.x.x.x). vea toolearn más información acerca de la depuración de aplicaciones en contenedores con Visual Studio 2017 [este artículo][link-debug-container].

![ejemplo de fabrikam en un contenedor][image-web-preview]

contenedor de Hello ahora está listo toobe genera y empaqueta en una aplicación de Service Fabric. Una vez que tenga la imagen de contenedor de hello integrada en su equipo, puede insertarlo tooany registro de contenedor y tire hacia abajo tooany toorun de host.

## <a name="get-hello-application-ready-for-hello-cloud"></a>Preparar la aplicación hello para la nube de Hola

aplicación de hello tooget listo para ejecutarse en Service Fabric en Azure, necesitamos toocomplete dos pasos:

1. Exponer el puerto de Hola donde los deseamos toobe pueda tooreach nuestra aplicación web en el clúster de Service Fabric Hola.
2. Proporcionar una base de datos SQL preparada para producción para nuestra aplicación

### <a name="expose-hello-port-for-hello-app"></a>Exponer el puerto para la aplicación hello Hola
clúster de Service Fabric Hola hemos configurado, tiene puerto *80* abre de forma predeterminada en hello equilibrador de carga de Azure, que equilibra clúster de toohello tráfico entrante. Podemos exponer nuestro contenedor en este puerto mediante nuestro archivo docker.compose.yml.

En Visual Studio, abra **el Explorador de soluciones**, buscar **redactar docker**y el archivo abierto hello **docker compose.override.yml**.

Modificar hello `fabrikamfiber.web:` nodo, agregar un nodo secundario denominado `ports:`.

Agregue una entrada de cadena `- "80:80"`.

```yml
  version: '3'

  services:
    fabrikamfiber.web:
      image: fabrikamfiber.web
      build:
        context: .\FabrikamFiber.Web
        dockerfile: Dockerfile
      ports:
        - "80:80"
```

### <a name="use-a-production-sql-database"></a>Uso de una base de datos SQL de producción
Cuando se ejecutan en producción, es necesario que nuestros datos se conserven en nuestra base de datos. Actualmente no hay ningún dato persistente de manera tooguarantee en un contenedor, por lo tanto, no se puede almacenar datos de producción en SQL Server en un contenedor.

Se recomienda usar una instancia de Azure SQL Database. tooset seguridad y ejecutar un servidor administrado de SQL Server en Azure, visite hello [tutoriales rápidos de base de datos de SQL Azure] [ link-azure-sql] artículo.

>[!NOTE]
>Recuerde toochange Hola conexión cadenas toohello SQL server en hello **web.release.config** archivo Hola **FabrikamFiber.Web** proyecto.
>
>Esta aplicación genera errores leves si no se puede acceder a ninguna base de datos SQL. Puede elegir toogo con antelación e implementar aplicación hello con ningún servidor SQL server.

## <a name="deploy-with-visual-studio-team-services"></a>Implementación con Visual Studio Team Services

tooset la implementación mediante Visual Studio Team Services, necesita hello tooinstall [extensión de herramientas de entrega continua para Visual Studio de 2017][link-visualstudio-cd-extension]. Esta extensión resulta fácil toodeploy tooAzure mediante la configuración de Visual Studio Team Services y obtener su clúster de Service Fabric tooyour de aplicación implementado.

tooget iniciado, el código se debe hospedar en el control de código fuente. resto de Hola de esta sección se da por supuesto **git** se está usando.

### <a name="set-up-a-vsts-repo"></a>Configuración de un repositorio de VSTS
En la esquina inferior derecha de Hola de Visual Studio, haga clic en **agregar tooSource Control** > **Git** (o cualquier opción que prefiera).

![Presione el botón del control de código fuente de Hola][image-source-control]

Hola _Team Explorer_ panel, presione **publicar el repositorio de Git**.

Seleccione el nombre del repositorio VSTS y presione **Repositorio**.

![publicar tooVSTS de repositorio][image-publish-repo]

Ahora que el código está sincronizado con un repositorio de código fuente VSTS, puede configurar la integración continua y la entrega continua.

### <a name="setup-continuous-delivery"></a>Configuración de la entrega continua

En _el Explorador de soluciones_, contextual hello **solución** > **configurar la entrega continua**.

Seleccione Hola suscripción de Azure.

Establecer **tipo de Host** demasiado**clúster de Service Fabric**.

Establecer **Host de destino** toohello servicio de cluster Server tejido que creó en la sección anterior de Hola.

Elija un **registro de contenedor** toopublish que el contenedor.

>[!TIP]
>Hola de uso **editar** botón toocreate un registro de contenedor.

Presione **Aceptar**.

![Configuración de la integración continua para Service Fabric][image-setup-ci]
   
   Cuando se haya completado la configuración de hello, el contenedor es tooService implementado tejido. Cada vez que realice una inserción repositorio toohello de actualizaciones se ejecuta una versión y una nueva compilación.
   
   >[!NOTE]
   >Imágenes del contenedor de creación Hola tardar aproximadamente 15 minutos.
   >clúster de Service Fabric Hola primera implementación toohello hace Hola base Windows Server Core imágenes de contenedor toobe descargado. descarga de Hello toma toocomplete adicional 5-10 minutos.

Explorar aplicación de centro de llamadas de Fabrikam toohello mediante dirección url de hello del clúster: por ejemplo, *http://mycluster.westeurope.cloudapp.azure.com*

Ahora que ha en contenedores e implementado la solución de Fabrikam Call Center hello, puede abrir hello [portal de Azure] [ link-azure-portal] y ver aplicación hello ejecutando en Service Fabric. aplicación de hello tootry, abra un explorador web y vaya toohello URL del clúster de Service Fabric.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo:

> [!div class="checklist"]
> * Creación de un proyecto de Docker en Visual Studio
> * Inclusión de una aplicación existente en un contenedor
> * Configuración de la integración continua con Visual Studio y VSTS

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooit.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate tooAzure Web Apps](app-service-web-tutorial-custom-ssl.md)

## Next steps

- [Container Tooling in Visual Studio][link-visualstudio-container-tools]
- [Get started with containers in Service Fabric][link-servicefabric-containers]
- [Creating Service Fabric applications][link-servicefabric-createapp]
-->

[link-debug-container]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-fabrikam-github]: https://aka.ms/fabrikamcontainer
[link-container-quickstart]: /virtualization/windowscontainers/quick-start/quick-start-windows-10
[link-visualstudio-container-tools]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-azure-powershell-install]: /powershell/azure/install-azurerm-ps
[link-servicefabric-create-secure-clusters]: service-fabric-cluster-creation-via-arm.md
[link-visualstudio-cd-extension]: https://aka.ms/cd4vs
[link-servicefabric-containers]: service-fabric-get-started-containers.md
[link-servicefabric-createapp]: service-fabric-create-your-first-application-in-visual-studio.md
[link-azure-portal]: https://portal.azure.com
[link-sf-clustertemplate]: https://aka.ms/securepreviewonelineclustertemplate
[link-azure-pricing-calculator]: https://azure.microsoft.com/en-us/pricing/calculator/
[link-azure-subscription]: https://azure.microsoft.com/en-us/free/
[link-vsts-account]: https://www.visualstudio.com/team-services/pricing/
[link-azure-sql]: /azure/sql-database/

[image-web-preview]: media/service-fabric-host-app-in-a-container/fabrikam-web-sample.png
[image-source-control]: media/service-fabric-host-app-in-a-container/add-to-source-control.png
[image-publish-repo]: media/service-fabric-host-app-in-a-container/publish-repo.png
[image-setup-ci]: media/service-fabric-host-app-in-a-container/configure-continuous-integration.png
