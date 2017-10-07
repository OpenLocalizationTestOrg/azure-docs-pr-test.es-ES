---
title: "aaaCI/CD desde Jenkins tooAzure las máquinas virtuales con Team Services | Documentos de Microsoft"
description: "Configurar la integración continua (CI) y la implementación continua (CD) de una aplicación de Node.js con las máquinas virtuales de Jenkins tooAzure de la administración de versión de Visual Studio Team Services (VSTS) o Microsoft Team Foundation Server (TFS)"
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a>Implementar la VM de aplicación tooLinux con Jenkins y Team Services

La integración continua (CI) y la implementación continua (CD) constituyen una canalización mediante la que se puede compilar, publicar e implementar el código. Team Services proporciona un conjunto completo, completo CI/CD de herramientas de automatización para tooAzure de implementación. Jenkins es una popular herramienta basada en servidor de CI/CD de terceros que además proporciona automatización de CI/CD. Puede usar ambos conjuntamente toocustomize cómo entregar la aplicación en la nube o el servicio.

En este tutorial, utilice Jenkins toobuild una **aplicación web de Node.js**y Visual Studio Team Services toodeploy, tooa [grupo de implementación](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) que contiene máquinas virtuales de Linux.

Podrá:

> [!div class="checklist"]
> * Compilar la aplicación en Jenkins
> * Configurar Jenkins para la integración con Team Services
> * Crear un grupo de implementación para hello máquinas virtuales de Azure
> * Crear una definición de la versión que configura las máquinas virtuales de hello e implementa la aplicación hello

## <a name="before-you-begin"></a>Antes de empezar

* Necesita acceso tooa Jenkins cuenta. Si aún no ha creado un servidor de Jenkins, vea [Jenkins Documentation (Documentación de Jenkins)](https://jenkins.io/doc/). 

* Inicie sesión en tooyour cuenta de Team Services (`https://{youraccount}.visualstudio.com`). 
  Puede obtener una [cuenta de Team Services gratuita](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).

  > [!NOTE]
  > Para obtener más información, consulte [conectar servicios de tooTeam](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).

* Si aún no tiene uno, cree un token de acceso personal (PAT) en la cuenta de Team Services. Jenkins requiere esta tooaccess información de su cuenta de Team Services.
  Lectura [cómo crear un token de acceso personal para Team Services y TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn cómo toogenerate uno.

## <a name="get-hello-sample-app"></a>Obtener la aplicación de ejemplo de Hola

Es necesario un toodeploy de aplicación almacenado en un repositorio de Git.
Para este tutorial se recomienda usar [esta aplicación de ejemplo disponible en GitHub](https://github.com/azooinmyluggage/fabrikam-node).

1. Crear una bifurcación de esta aplicación y tome nota de hello ubicación (URL) para su uso en pasos posteriores de este tutorial.

1. Asegúrese de bifurcación de hello **público** toosimplify conectar tooGitHub más tarde.

> [!NOTE]
> Para más información, vea [Fork a repo (Bifurcar un repositorio)](https://help.github.com/articles/fork-a-repo/) y [Making a private repository public (Hacer público un repositorio privado)](https://help.github.com/articles/making-a-private-repository-public/).

> [!NOTE]
> aplicación Hello se compiló mediante [Yeoman](http://yeoman.io/learning/index.html); usa **Express**, **bower**, y **grunt**; y tiene algunos **npm**paquetes como dependencias.
> aplicación de ejemplo de Hola contiene un conjunto de [plantillas de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) que se toodynamically usado crear máquinas virtuales de hello para la implementación en Azure. Estas plantillas se utilizan las tareas de hello [definición de la versión de Team Services](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).
> plantilla de Hello principal crea un grupo de seguridad de red, una máquina virtual y una red virtual. Asigna una dirección IP pública y abre el puerto de entrada 80. También agrega una etiqueta que se usa por la implementación de hello implementación grupo demasiado seleccione Hola máquinas tooreceive Hola.
>
> ejemplo de Hola también contiene una secuencia de comandos que configura Nginx e implementa la aplicación hello. Se ejecuta en cada una de las máquinas virtuales Hola. En concreto, el script de Hola instala nodo, Nginx y PM2; configura Nginx y PM2; a continuación, inicia Hola nodo aplicación.

## <a name="configure-jenkins-plugins"></a>Configuración de complementos de Jenkins

En primer lugar, debe configurar dos complementos de Jenkins para **NodeJS** y la **integración con Team Services**.

1. Abra la cuenta de Jenkins y elija **Manage Jenkins** (Administrar Jenkins).

1. Hola **administrar Jenkins** página, elija **administrar complementos**.

1. Filtro Hola lista toolocate Hola **NodeJS** complemento e instalarlo sin necesidad de reiniciar.

   ![Agregar complemento tooJenkins de hello NodeJS](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. Filtro Hola lista toofind Hola **Team Foundation Server** complemento e instalarlo. (Este complemento funciona con Team Services y Team Foundation Server). No es necesario reiniciar Jenkins.

## <a name="configure-jenkins-build-for-nodejs"></a>Configuración de la compilación de Jenkins para Node.js

En Jenkins, cree un nuevo proyecto de compilación y configúrelo como se indica a continuación:

1. Hola **General** ficha, escriba un nombre para el proyecto de compilación.

1. Hola **administración de código fuente** ficha, seleccione **Git** y escriba los detalles de hello del repositorio de Hola y bifurcación de Hola que contiene el código de la aplicación.

   ![Agregar una compilación de tooyour de repositorio](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > Si el repositorio no es público, elija **agregar** y proporcionar credenciales tooconnect tooit.

1. Hola **crear desencadenadores** ficha, seleccione **sondeo SCM** y especifique la programación de hello `H/03 * * * *` repositorio de Git de hello toopoll cambios cada tres minutos. 

1. Hola **entorno de compilación de** ficha, seleccione **proporcionar nodo &amp; npm bin / ruta de acceso de carpeta** y escriba `NodeJS` para el valor de nodo JS instalación Hola. Deje **npmrc file** establecido en "Usar predeterminado del sistema".

1. Hola **generar** ficha, escriba el comando hello `npm install` tooensure se actualizan todas las dependencias.

## <a name="configure-jenkins-for-team-services-integration"></a>Configurar Jenkins para la integración con Team Services

1. Hola **acciones posteriores a la compilación** ficha, para **archivos tooarchive**, escriba `**/*` tooinclude todos los archivos.

1. Para **desencadenar el lanzamiento de TFS y Team Services**, escriba Hola de dirección URL completa de la cuenta (como `https://your-account-name.visualstudio.com`), Hola nombre del proyecto, un nombre para la definición de versión de hello (creado más adelante), y Hola cuenta de credenciales tooconnect tooyour.
   Necesita el nombre de usuario y Hola PAT que creó anteriormente. 

   ![Configuración de acciones posteriores a la compilación de Jenkins](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. Guarde el proyecto de compilación de Hola.

## <a name="create-a-jenkins-service-endpoint"></a>Creación de un punto de conexión de servicio de Jenkins

Un extremo de servicio permite Team Services tooconnect tooJenkins.

1. Abra hello **servicios** página en Team Services, abra hello **nuevo extremo de servicio** lista y elija **Jenkins**.

   ![Adición de un punto de conexión de Jenkins](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. Escriba un nombre que se va a utilizar toorefer toothis conexión.

1. Escriba Hola URL del servidor Jenkins y graduación hello **Aceptar los certificados SSL no es de confianza** opción.

1. Escriba el nombre de usuario de Hola y la contraseña de su cuenta de Jenkins.

1. Elija **Comprobar conexión** toocheck que Hola información es correcta.

1. Elija **Aceptar** extremo de servicio de toocreate Hola.

## <a name="create-a-deployment-group"></a>Creación de un grupo de implementación

Necesita un [grupo de implementación](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) demasiado contienen hello las máquinas virtuales.

1. Hola abierto **versiones** ficha de hello **generar &amp; versión** concentrador, a continuación, abra hello **grupos de implementación** y a **+ nuevo**.

1. Escriba un nombre para el grupo de implementación de hello y una descripción opcional.
   Luego elija **Crear**.

tarea de implementación de grupo de recursos de Azure de Hello crea y registra hello las máquinas virtuales cuando se ejecuta con la plantilla de hello Azure Resource Manager.
No necesita toocreate y registre las máquinas virtuales Hola usted mismo.

## <a name="create-a-release-definition"></a>Creación de una definición de versión

Una definición de versión especifica proceso Hola Team Services ejecutará la aplicación de hello toodeploy.
definición de versión de hello toocreate en Team Services:

1. Hola abierto **versiones** ficha de hello **compilar &amp; versión** concentrador, abra hello  **+**  desplegable en la lista de Hola de definiciones de versión y elija Hola **crear versión definición**. 

1. Seleccione hello **vacía** plantilla y elija **siguiente**.

1. Hola **artefactos** sección, haga clic en **vincular un artefacto** y elija **Jenkins**. Seleccione la conexión del punto de conexión de servicio de Jenkins. A continuación, seleccione Hola Jenkins origen trabajo y elija **crear**. 

1. Hola nueva definición de la versión, elija **+ agregar tareas** y agregue un **implementación de grupo de recursos de Azure** entorno de tarea toohello predeterminado.

1. Elija Hola desplegable flecha siguiente toohello **+ agregar tareas** vincular y agregar una definición de toohello de fase de grupo de implementación.

   ![Adición de una fase de grupo de implementación](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. En el catálogo de la tarea de hello, abra hello **utilidad** sección y agregue una instancia del programa Hola a **secuencia de comandos de Shell** tarea.

1. plantilla de parámetros de Hello utilizada en la tarea de implementación de grupo de recursos de Azure de hello establece Hola admin contraseña utilizada tooconnect toohello máquinas virtuales.
   Indique la contraseña con la variable de hello **$(adminpassword)**:
   
   - Abra hello **Variables** ficha y, en hello **Variables** sección, escriba el nombre de hello `adminpassword`.

   - Escriba la contraseña de administrador de Hola.

   - Elija Hola "candado" icono siguiente toohello valor textbox tooprotect Hola contraseña. 

## <a name="configure-hello-azure-resource-group-deployment-task"></a>Configurar la tarea de implementación de grupo de recursos de Azure de hello

Hola **implementación de grupo de recursos de Azure** tarea es el grupo de implementación de hello toocreate usado. Configúrelo de la siguiente forma:

* **Suscripción de Azure:** seleccione una conexión de lista de hello en **conexiones de servicio de Azure disponibles**. 
  Si no hay ninguna conexión aparece, elija **administrar**, seleccione **nuevo extremo de servicio** , a continuación, **Azure Resource Manager**y siga las indicaciones de Hola.
  Devolver tooyour versión definición, actualización hello **AzureRM suscripción** lista y conexión Hola select que ha creado.

* **Grupo de recursos**: escriba un nombre de grupo de recursos de Hola que creó anteriormente.

* **Ubicación**: seleccionar una región para la implementación de Hola.

  ![Creación de un nuevo grupo de recursos](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* **Ubicación de la plantilla**: `URL of hello file`

* **Vínculo de la plantilla**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`

* **Vínculo de parámetros de la plantilla**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`

* **Reemplazar parámetros de plantilla**: una lista de hello invalidar valores, por ejemplo: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.<br />Insertar sus propios valores específicos de Hola {marcadores de posición}. 

* **Habilitar requisitos previos**: `Configure with Deployment Group agent`

* **Punto de conexión TFS/VSTS**: elija **agregar** y, en el cuadro de diálogo "Agregar nueva conexión de los servicios servidor/equipo de Team Foundation" Hola, seleccione **autenticación basada en Token**. Escriba un nombre de conexión de Hola y Hola URL del proyecto de equipo. A continuación, generar y escriba un [símbolo (token) de acceso Personal (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) proyecto de equipo de tooauthenticate Hola conexión tooyour.

  ![Creación de un token de acceso personal](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* **Proyecto de equipo**: seleccione el proyecto actual.

* **Grupo de implementación**: escriba Hola el mismo nombre de grupo de implementación que ha usado para hello **grupo de recursos** parámetro.

configuración predeterminada de Hello para la tarea de implementación de grupo de recursos de Azure de hello es toocreate o actualiza un recurso y toodo de forma incremental. tarea Hello crea Hola Hola de máquinas virtuales de primera vez que se ejecuta y posteriormente simplemente actualizarlos.

## <a name="configure-hello-shell-script-task"></a>Configurar la tarea de secuencia de comandos de Shell de Hola

Hola **secuencia de comandos de Shell** tarea es la configuración de Hola de tooprovide usado para un toorun de script en cada aplicación de hello de servidor tooinstall Node.js e iniciar. Configúrelo de la siguiente forma:

* **Ruta de acceso del script**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`

* **Especificar directorio de trabajo**: `Checked`

* **Directorio de trabajo**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`
   
## <a name="rename-and-save-hello-release-definition"></a>Cambiar el nombre y guardar la definición de la versión de Hola

1. Editar nombre de Hola de nombre de definición toohello de hello versión especificada en el **acciones posteriores a la compilación** pestaña de generación de hello en Jenkins. Jenkins requiere este tootrigger capaz de una nueva versión toobe de nombre cuando se actualizan los artefactos de origen de Hola.

1. Si lo desea, cambie el nombre de hello del entorno de hello haciendo clic en el nombre de Hola. 

1. Elija **Guardar** y luego **Aceptar**.

## <a name="start-a-manual-deployment"></a>Inicio de una implementación manual

1. Elija **+ Versión** y seleccione **Crear versión**.

1. Seleccionar compilación de Hola que completado en la lista desplegable resaltada de Hola y elija **crear**.

1. Elija el vínculo de la versión de hello en mensajes de bienvenida del menú emergente. Por ejemplo: "Versión **Release-1** se ha creado".

1. Abra hello **registros** ficha salida de la consola de toowatch Hola versión.

1. En el explorador, abra Hola URL de uno de los servidores de hello Agregar grupo de implementación de tooyour. Por ejemplo, escriba `http://{your-server-ip-address}`

## <a name="start-a-cicd-deployment"></a>Inicio de una implementación de CI/CD

1. Hola de definición de la versión, desactive la opción hello **habilitado** checkbox en hello **opciones de Control** sección de configuración de hello para la tarea de implementación de grupo de recursos de Azure Hola.
   Para el grupo futuras implementaciones toohello de implementación, no es necesario toore-ejecutar esta tarea.

1. Vaya toohello repositorio de Git de origen y modificar contenido de Hola de hello **h1** encabezado en el archivo hello [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).

1. Confirme el cambio.

1. Después de unos minutos, verá una nueva versión que creó en hello **versiones** página de Team Services o TFS. Abra la implementación de Hola Hola versión toosee teniendo lugar. ¡Enhorabuena!

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, se Hola la implementación automatizada de un tooAzure de aplicación con compilación Jenkins y servicios de equipo para la versión. Ha aprendido a:

> [!div class="checklist"]
> * Compilar la aplicación en Jenkins
> * Configurar Jenkins para la integración con Team Services
> * Crear un grupo de implementación para hello máquinas virtuales de Azure
> * Crear una definición de la versión que configura las máquinas virtuales de hello e implementa la aplicación hello

Avanzar toohello siguiente tutorial toolearn más información acerca de cómo la pila toodeploy una luz (Linux, Apache, MySQL y PHP).

> [!div class="nextstepaction"]
> [Implementación de una pila de LAMP](tutorial-lamp-stack.md)