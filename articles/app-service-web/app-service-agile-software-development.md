---
title: "desarrollo de software de aaaAgile con el servicio de aplicación de Azure"
description: "Obtenga información acerca de cómo toocreate gran escala aplicaciones complejas con el servicio de aplicación de Azure de forma que admite el desarrollo de software ágil."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: c0fdb676-36a6-4738-925f-65b4835d187f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: a1c1c78cfff711774943b0235ed762f03f48fc6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="agile-software-development-with-azure-app-service"></a>Agile Software Development con el Servicio de aplicaciones de Azure
En este tutorial, aprenderá cómo aplicaciones complejas de gran escala toocreate con [servicio de aplicaciones de Azure](/azure/app-service/) de forma que admita [desarrollo de software ágil](https://en.wikipedia.org/wiki/Agile_software_development). Supone que ya sabe cómo demasiado[implementar aplicaciones complejas predecible en Azure](app-service-deploy-complex-application-predictably.md).

Limitaciones en procesos técnicas a menudo pueden ser en forma de Hola de implementación correcta de las metodologías de agile. Servicio de aplicaciones de Azure con otras características, como [publicación continua](app-service-continuous-deployment.md), [entornos de ensayo](web-sites-staged-publishing.md) (ranuras), y [supervisión](web-sites-monitor.md), cuando se acopla con cuidado con la orquestación de Hola y administración de implementación en [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), puede formar parte de una excelente solución para los desarrolladores que adoptan el desarrollo de software ágil.

Hola tabla siguiente es una lista breve de requisitos asociados con el desarrollo ágil, y cómo habilitar los servicios de Azure cada uno de ellos.

| Requisito | Habilitación de Azure |
| --- | --- |
| - Compilación con cada confirmación<br>- Compilación automática y rápida |Cuando se configura con implementación continua, el Servicio de aplicaciones de Azure puede funcionar como compilaciones de ejecución en directo que se basan en una rama de desarrollo. Cada vez que código se inserta toohello sucursales, es generada automáticamente y en ejecución en vivo en Azure. |
| - Creación de pruebas automáticas de compilaciones |Cargar pruebas, las pruebas web, etc., se puede implementar con la plantilla de hello Azure Resource Manager. |
| - Realización de pruebas en un clon del entorno de producción |Plantillas de administrador de recursos de Azure pueden ser usado toocreate clones del entorno de producción de Azure hello (incluida la configuración de la aplicación, plantillas de cadenas de conexión, ajuste de escala, etc.) para probar rápidamente y predecible. |
| - Fácil visualización de los resultados de la última compilación |TooAzure de implementación continua desde un repositorio significa que puede probar el nuevo código en una aplicación activa inmediatamente después de confirmar los cambios. |
| -Confirmar bifurcación main toohello cada día<br>- Automatización de la implementación |La integración continua de una aplicación de producción con la bifurcación main del repositorio implementa automáticamente cada tooproduction de confirmación/merge toohello bifurcación main. |

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>Lo que hará
Le guiará a través de un flujo de trabajo de desarrollo pruebas fase de producción típico en orden toopublish nuevos cambios toohello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) aplicación de ejemplo, que consta de dos [aplicaciones web](/services/app-service/web/), uno es un front-end (FE) y Hola a otro en un API Web back-end (BE) y un [base de datos SQL](/services/sql-database/). Funcionará con hello después de la arquitectura de implementación:

![](./media/app-service-agile-software-development/what-1-architecture.png)

imagen de hello tooput en palabras:

* arquitectura de implementación de Hola se divide en tres entornos distintos (o [grupos de recursos](../azure-resource-manager/resource-group-overview.md) en Azure), cada uno con su propio [plan de servicio de aplicaciones](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), [escalado](web-sites-scale.md) configuración, y la base de datos SQL. 
* Cada entorno se puede administrar por separado. Incluso pueden existir en distintas suscripciones.
* Ensayo y producción se implementan como dos ranuras de hello misma aplicación de servicio de aplicaciones. bifurcación principal de Hola se configura para la integración continua con hello ranura de ensayo.
* Cuando se comprueba una bifurcación de toomaster de confirmación en hello ranura (con datos de producción) de almacenamiento provisional, Hola comprobado la aplicación de almacenamiento provisional se intercambia a ranura de producción de hello [sin tiempo de inactividad](web-sites-staged-publishing.md).

entorno de producción y ensayo Hello se define una plantilla de hello en [  *&lt;repository_root >*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json).

Hola dev y entornos de prueba se definen mediante la plantilla de hello en [  *&lt;repository_root >*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json).

Estrategia de bifurcación típico de hello, también utiliza con el código móvil de la bifurcación dev de hello una bifurcación de prueba de toohello, toohello bifurcación principal (mover hacia arriba en la calidad, por lo que toospeak).

![](./media/app-service-agile-software-development/what-2-branches.png) 

## <a name="what-you-need"></a>Lo que necesita
* Una cuenta de Azure
* Una cuenta [GitHub](https://github.com/)
* GIT Shell (instalado con [GitHub para Windows](https://windows.github.com/))-habilita toorun ambos Hola Git y PowerShell comandos Hola mismo sesión 
* Bits más recientes de [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)
* Conocimientos básicos de hello siguientes herramientas:
  * Implementación de plantillas de [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) (vea también [Implementación predecible de una aplicación compleja en Azure](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> Necesita una cuenta de Azure toocomplete este tutorial:
> 
> * También puede [abrir una cuenta de Azure de forma gratuita](https://azure.microsoft.com/pricing/free-trial/) -obtendrá créditos puede usar tootry los servicios de Azure de pago e incluso después de que agoten puede mantener la cuenta de hello y libre de usar servicios de Azure, como las aplicaciones Web.
> * Puede [activar las ventajas de suscriptor de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) : su suscripción a Visual Studio le proporciona crédito todos los meses que puede usar con servicios de Azure de pago.
> 
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="set-up-your-production-environment"></a>Configuración del entorno de producción
> [!NOTE]
> script de Hola usado en este tutorial, automáticamente configura publicación continua desde el repositorio de GitHub. Esto requiere que las credenciales de GitHub ya están almacenadas en Azure, en caso contrario Hola scripts implementación produce un error al intentar tooconfigure configuración de control de código fuente para las aplicaciones web de Hola. 
> 
> toostore su GitHub credenciales de Azure, cree una aplicación web en hello [portal de Azure](https://portal.azure.com/) y [configurar la implementación de GitHub](app-service-continuous-deployment.md). Solo necesita esta vez toodo. 
> 
> 

En un escenario típico de DevOps, tiene una aplicación que se ejecuta en Azure y desea toomake cambios tooit a través de la publicación continua. En este escenario, tiene una plantilla que se toodeploy desarrollado, probado y usar Hola entorno de producción. La configurará en esta sección.

1. Crear su propia bifurcación de hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repositorio. Para obtener información sobre la creación de la bifurcación, consulte [Bifurcación de un repositorio](https://help.github.com/articles/fork-a-repo/). Una vez creada la bifurcación, puede verla en el explorador.
   
    ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Abra una sesión del Shell de Git. Si aún no tiene el Shell de Git, instale ahora [GitHub para Windows](https://windows.github.com/) .
3. Crear un clon de la bifurcación local mediante la ejecución de hello siguiente comando:

        git clone https://github.com/<your_fork>/ToDoApp.git 
4. Una vez que tenga el clon local, vaya demasiado*&lt;repository_root >*\ARMTemplates y deploy.ps1 Hola de ejecución de secuencias de comandos como se indica a continuación:
   
        .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git
5. Cuando se le solicite, escriba el nombre de usuario de hello deseado y una contraseña para el acceso a la base de datos.
   
   Debería ver Hola aprovisionamiento progreso por varios recursos de Azure. Cuando se completa la implementación, el script de Hola inicia la aplicación hello en el Explorador de Hola y proporcionarle un bip descriptivo.
   
    ![](./media/app-service-agile-software-development/production-2-app-in-browser.png)
   
   > [!TIP]
   > Eche un vistazo a  *&lt;repository_root >*\ARMTemplates\Deploy.ps1, toosee cómo genera recursos con identificadores únicos. Puede usar Hola mismo toocreate de enfoque que se clona de Hola misma implementación sin preocuparse por los nombres de recursos en conflicto.
   > 
   > 
6. De nuevo en la sesión del Shell de Git, ejecute:
   
        .\swap –Name ToDoApp<unique_string>master
   
    ![](./media/app-service-agile-software-development/production-4-swap.png)
7. Cuando finaliza el script de Hola, vuelva atrás toobrowse toohello dirección del front-end (http://ToDoApp*&lt;unique_string >*master.azurewebsites.net/) toosee Hola ejecuta aplicación en producción.
8. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) y eche un vistazo a lo que se crea.
   
   Debe ser capaz de toosee dos aplicaciones de web Hola mismo grupo de recursos, uno con hello `Api` sufijo de nombre de Hola. Si observa en vista de grupo de recursos de hello, verá también Hola base de datos SQL y servidor, Hola plan de servicio de aplicaciones y zonas de ensayo de Hola para las aplicaciones web de Hola. Examine los distintos recursos de Hola y compararlos con  *&lt;repository_root >*toosee \ARMTemplates\ProdAndStage.json cómo estén configuradas en la plantilla de Hola.
   
    ![](./media/app-service-agile-software-development/production-3-resource-group-view.png)

Ahora ha configurado el entorno de producción de hello. A continuación, se lanzará una nueva aplicación toohello de actualización.

## <a name="create-dev-and-test-branches"></a>Creación de ramas de desarrollo y prueba
Ahora que tiene una aplicación compleja que se ejecuta en el entorno de producción de Azure, hará que una aplicación de tooyour actualización de acuerdo con la metodología ágil. En esta sección, creará Hola bifurcaciones de desarrollo y pruebas que necesitará toomake Hola requiere actualizaciones.

1. Crear entorno de prueba de hello en primer lugar. En la sesión de Git Shell, siguiente ejecución Hola comandos toocreate entorno de Hola para una nueva bifurcación denominada **NewUpdate**. 
   
        git checkout -b NewUpdate
        git push origin NewUpdate 
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch NewUpdate
2. Cuando se le solicite, escriba el nombre de usuario de hello deseado y una contraseña para el acceso a la base de datos. 
   
   Cuando se completa la implementación, el script de Hola inicia la aplicación hello en el Explorador de Hola y proporcionarle un bip descriptivo. Ahora tiene una nueva rama con su propio entorno de prueba. Realizar una tooreview momento algunos aspectos de este entorno de prueba:
   
   * Puede crearlo en cualquier suscripción de Azure. Esto significa el entorno de producción de hello puede administrarse por separado desde el entorno de prueba.
   * El entorno de prueba se ejecuta en directo en Azure.
   * El entorno de prueba es el entorno de producción toohello idénticas, salvo hello las ranuras de almacenamiento provisional y configuración de escala de Hola. Sabe que porque son las únicas diferencias de hello entre ProdandStage.json y Dev.json.
   * Puede administrar su entorno de prueba en su propio plan de Servicio de aplicaciones, con un nivel de precio diferente (como **Gratis**).
   * Eliminación de este entorno de prueba es tan sencilla como eliminar grupo de recursos de Hola. Encontrará más información sobre cómo toodo esto [más adelante](#delete).
3. Vaya toocreate una bifurcación dev mediante la ejecución de Hola siguientes comandos:
   
        git checkout -b Dev
        git push origin Dev
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch Dev
4. Cuando se le solicite, escriba el nombre de usuario de hello deseado y una contraseña para el acceso a la base de datos. 
   
   Realizar una tooreview momento algunos aspectos de este entorno de desarrollo: 
   
   * El entorno de desarrollo tiene un entorno de prueba de configuración idénticos toohello porque está implementado con hello misma plantilla.
   * Cada entorno de desarrollo puede crearse en hello del desarrollador suscripción a Azure, dejando toobe de entorno de prueba de hello administrado por separado.
   * El entorno de desarrollo se ejecuta en directo en Azure.
   * Eliminar dev Hola entorno es tan sencillo como eliminar grupo de recursos de Hola. Encontrará más información sobre cómo toodo esto [más adelante](#delete).

> [!NOTE]
> Cuando haya varios desarrolladores que trabajan en la nueva actualización de hello, cada uno de ellos fácilmente puede crear una bifurcación y el entorno de desarrollo dedicado con hello pasos:
> 
> 1. Crear su propia bifurcación del repositorio de hello en GitHub (consulte [bifurcar un repositorio](https://help.github.com/articles/fork-a-repo/)).
> 2. Clonar bifurcar hello en su equipo local
> 3. Ejecute hello mismo comandos toocreate su propia bifurcación dev y entorno.
> 
> 

Al terminar, la bifurcación de GitHub debe tener tres ramas:

![](./media/app-service-agile-software-development/test-1-github-view.png)

Y usted debe tener seis aplicaciones web (tres conjuntos de dos) en tres grupos de recursos independientes:

![](./media/app-service-agile-software-development/test-2-all-webapps.png)

> [!NOTE]
> ProdandStage.json especifica Hola de toouse de entorno de producción de hello **estándar** tarifa, lo cual resulta adecuado para la escalabilidad de aplicaciones de producción de hello.
> 
> 

## <a name="build-and-test-every-commit"></a>Compilación y prueba de cada confirmación
Hola archivos de plantilla ProdAndStage.json y Dev.json ya especificar parámetros de control de código fuente de hello, que de forma predeterminada se establece la publicación continua de la aplicación web de hello. Por lo tanto, cada rama de GitHub de confirmación toohello desencadena una tooAzure de implementación automática de esa bifurcación. Veamos cómo funciona ahora su instalación.

1. Asegúrese de que está en la bifurcación Dev de hello del repositorio local Hola. toodo, Hola ejecución siguiente comando en el Shell de Git:
   
        git checkout Dev
2. Asegúrese de capa de interfaz de usuario de la aplicación de toohello cambio cambiando Hola código toouse [arranque](http://getbootstrap.com/components/) enumera. Abra  *&lt;repository_root >*\src\MultiChannelToDo.Web\index.cshtml y asegúrese de que Hola siguiente cambio de resaltado:
   
    ![](./media/app-service-agile-software-development/commit-1-changes.png)
   
    > [!NOTE]
    > Si no se puede leer Hola imagen anterior: 
    > 
    > * En la línea 18, cambiar `check-list` demasiado`list-group`.
    > * En línea 19, cambie `class="check-list-item"` demasiado`class="list-group-item"`.
    > 
    > 
3. Guarde el cambio de Hola. Hacer copias en el Shell de Git, ejecute hello siguientes comandos:
   
        cd <repository_root>
        git add .
        git commit -m "changed toobootstrap style"
        git push origin Dev
   
   Estos comandos de git son similares demasiado "comprobación en el código" en otro sistema de control de código fuente como TFS. Al ejecutar `git push`, confirmación nueva Hola desencadena una tooAzure de inserción automática de código, que vuelve a generar, a continuación, Hola aplicación tooreflect Hola cambio en el entorno de desarrollo de Hola.
4. Ir a página de aplicación web del entorno de desarrollo tooyour de tooverify que se ha producido este entorno de desarrollo de tooyour de inserción de código, y examine hello **implementación** parte. Debe ser capaz de toosee la última confirmación del mensaje no existe.
   
    ![](./media/app-service-agile-software-development/commit-2-deployed.png)
5. Desde allí, haga clic en **examinar** toosee Hola nuevo cambio en vivo de las aplicaciones hello en Azure.
   
    ![](./media/app-service-agile-software-development/commit-3-webapp-in-browser.png)
   
   Es una aplicación de toohello cambio menor. Sin embargo, muchas veces nueva aplicación de cambios tooa web complejas tienen efectos secundarios no deseados y no deseados. Está probando tooeasily capaz de cada confirmación en las compilaciones en directo permite toocatch estos problemas antes de que los clientes ven.

Por ahora, debe tener destreza en la realización de Hola que, como desarrollador en hello **NewUpdate** proyecto, puede crear un entorno de desarrollo para usted mismo, a continuación, compilar cada confirmación y probar cada compilación.

## <a name="merge-code-into-test-environment"></a>Combinación del código en el entorno de prueba
Cuando esté listo toopush bifurcar el código de desarrollo una rama tooNewUpdate, es Hola git estándar proceso:

1. Combinar cualquier nueva tooNewUpdate confirmaciones en la bifurcación Dev de hello en GitHub, por ejemplo, confirmaciones creadas por otros desarrolladores. Cualquier nueva confirmación en GitHub desencadena una inserción de código y compilar en el entorno de desarrollo de Hola. A continuación, puede asegurarse de que el código en la bifurcación Dev funciona también con bits más recientes de Hola de bifurcación NewUpdate.
2. Combine todas las nuevas confirmaciones de la rama de desarrollo en la rama NewUpdate de GitHub. Esta acción desencadena una inserción de código y compilar en el entorno de prueba de Hola. 

Nuevo, tenga en cuenta que, como la implementación continua ya está configurada con estas bifurcaciones git, no necesita tootake cualquier otra acción, como ejecutar integración compilaciones. Basta con git prácticas recomendadas de control de origen estándar de tooperform y Azure realiza todos los procesos de compilación de hello automáticamente.

Ahora, vamos a insertar el código demasiado**NewUpdate** bifurcación. En el Shell de Git, ejecute hello siguientes comandos:

    git checkout NewUpdate
    git pull origin NewUpdate
    git merge Dev
    git push origin NewUpdate

¡Ya está! 

Página de la aplicación web vaya toohello para su toosee de entorno de prueba envíe ahora entorno de prueba de toohello la confirmación nuevo (combinada en bifurcación NewUpdate). A continuación, haga clic en **examinar** toosee que Hola cambiar estilo ahora se está ejecutando en vivo en Azure.

## <a name="deploy-update-tooproduction"></a>Implementar actualización tooproduction
Insertar código toohello entorno de ensayo y producción se sentirá no sea diferente de lo que ya ha hecho cuando inserta el entorno de prueba de toohello de código. Es así de sencillo. 

En el Shell de Git, ejecute hello siguientes comandos:

    git checkout master
    git pull origin master
    git merge NewUpdate
    git push origin master

Recuerde que se basan en forma de hello está configurado el entorno de ensayo y producción de hello en ProdandStage.json, el código nuevo se inserta toohello **de ensayo** ranura y se está ejecutando no existe. Por lo que si se desplaza la dirección URL de la ranura de toohello almacenamiento provisional, consulte se ejecuta de nuevo código de hello. toodo, Hola ejecución siguiente cmdlet en el Shell de Git.

    Start-Process -FilePath "http://ToDoApp<unique_string>master-Staging.azurewebsites.net"

Y ahora, una vez comprobado actualización Hola Hola ranura de ensayo, Hola solo lo dejado toodo es tooswap en producción. En el Shell de Git, ejecutar simplemente Hola siguientes comandos:

    cd <repository_root>\ARMTemplates
    .\swap.ps1 -Name ToDoApp<unique_string>master

¡Enhorabuena! Se ha publicado correctamente una nueva aplicación web de actualización tooyour producción. Es más, lo hizo creando fácilmente entornos de desarrollo y prueba, y compilando y probando cada confirmación. Estos son los bloques de creación fundamentales de Agile Software Development.

<a name="delete"></a>

## <a name="delete-dev-and-test-environments"></a>Eliminación de entornos de desarrollo y prueba
Dado que se ha diseñado intencionalmente el desarrollo y grupos de recursos independientes de toobe de entornos de prueba, es fácil toodelete ellos. Hola toodelete que ha creado en este tutorial, bifurcaciones de GitHub de Hola y artefactos de Azure, simplemente ejecute Hola siga los comandos en el Shell de Git:

    git branch -d Dev
    git push origin :Dev
    git branch -d NewUpdate
    git push origin :NewUpdate
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>dev-group -Force -Verbose
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>newupdate-group -Force -Verbose

## <a name="summary"></a>Resumen
Desarrollo de software ágil es indispensable para muchas empresas que quieran tooadopt Azure como su plataforma de aplicaciones. En este tutorial, ha aprendido cómo toocreate y desactivación hacia abajo réplicas exactas o cerca de las réplicas de Hola entorno de producción con facilidad, incluso para aplicaciones complejas. También ha aprendido cómo tooleverage esta toocreate capacidad un desarrollo procesar que puede compilar y probar cada confirmación única en Azure. Este tutorial es de esperar que haya mostrado cómo puede mejor usar servicio de aplicaciones de Azure y Azure Resource Manager toocreate conjuntamente una solución de DevOps que se encarga de las metodologías de tooagile. Luego, puede basarse en este escenario para realizar técnicas de DevOps avanzadas como [pruebas en producción](app-service-web-test-in-production-get-start.md). Para ver un escenario común de pruebas en producción, consulte [Implementación de la distribución de paquetes piloto (pruebas beta) en el Servicio de aplicaciones de Azure](app-service-web-test-in-production-controlled-test-flight.md).

## <a name="more-resources"></a>Más recursos
* [Implementación predecible de una aplicación compleja en Azure](app-service-deploy-complex-application-predictably.md)
* [Desarrollo ágil en la práctica: trucos y sugerencias para un ciclo de desarrollo actualizado](http://channel9.msdn.com/Events/Ignite/2015/BRK3707)
* [Estrategias de implementación avanzada para Aplicaciones web de Azure con plantillas de Administrador de recursos](http://channel9.msdn.com/Events/Build/2015/2-620)
* [Creación de plantillas del Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - Hola validador de JSON](http://jsonlint.com/)
* [ARMClient: configurar la publicación toosite de GitHub](https://github.com/projectKudu/ARMClient/wiki/Setup-GitHub-publishing-to-Site)
* [Creación de ramas de Git: combinación y creación de ramas básicas](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Blog de David Ebbo](http://blog.davidebbo.com/)
* [Azure PowerShell](/powershell/azure/overview)
* [Herramientas de línea de comandos multiplataforma de Azure](../cli-install-nodejs.md)
* [Creación o edición de usuarios en Azure AD](https://msdn.microsoft.com/library/azure/hh967632.aspx#BKMK_1)
* [Wiki de Project Kudu](https://github.com/projectkudu/kudu/wiki)

