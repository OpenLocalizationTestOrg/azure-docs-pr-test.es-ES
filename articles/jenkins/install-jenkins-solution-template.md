---
title: aaaCreate un servidor Jenkins en Azure
description: "Instalar Jenkins en una máquina virtual de Linux de Azure desde la plantilla de solución de hello Jenkins y generar una aplicación de Java de ejemplo."
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 82ab2ac52594acba131414b449b608978591d4b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a>Crear un servidor Jenkins en una máquina virtual Linux de Azure de hello portal de Azure

Este tutorial rápido muestra cómo tooinstall [Jenkins](https://jenkins.io) en una VM de Linux Ubuntu con las herramientas de Hola y toowork complementos configurados con Azure. Cuando haya terminado, dispondrá de un servidor de Jenkins en ejecución en Azure que permitirá compilar una aplicación Java de ejemplo desde [GitHub](https://github.com).

## <a name="prerequisites"></a>Requisitos previos

* Una suscripción de Azure
* TooSSH de acceso en línea de comandos del equipo (como Hola shell de Bash o [PuTTY](http://www.putty.org/))

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a>Crear Hola Jenkins VM desde plantilla de solución de Hola

Abra hello [una imagen de marketplace para Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) en su explorador web y seleccione **obtener TI ahora** del lado izquierdo de Hola de página Hola. Hola de revisión de precios detalles y seleccione **continuar**, a continuación, seleccione **crear** servidor tooconfigure Hola Jenkins Hola portal de Azure. 
   
![Cuadro de diálogo de Azure Portal](./media/install-jenkins-solution-template/ap-create.png)

Hola **configurar valores básicos** ficha, rellene Hola siguientes campos:

![Configuración básica](./media/install-jenkins-solution-template/ap-basic.png)

* Use **Jenkins** en **Nombre**.
* Escriba un **nombre de usuario**. nombre de usuario de Hello debe cumplir [requisitos específicos](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).
* Seleccione **contraseña** como hello **tipo de autenticación** y escriba una contraseña. Hola contraseña debe contener un carácter en mayúscula, un número y un carácter especial.
* Use **myJenkinsResourceGroup** para hello **grupo de recursos**.
* Elija hello **UU** [región de Azure](https://azure.microsoft.com/regions/) de hello **ubicación** lista desplegable.

Seleccione **Aceptar** tooproceed toohello **configurar opciones adicionales** ficha. Escriba un único tooidentify Hola Jenkins servidor DNS y seleccione **Aceptar**.

![Configurar opciones adicionales](./media/install-jenkins-solution-template/ap-addtional.png)  

 Una vez que la validación es correcta, seleccione **Aceptar** nuevo desde hello **resumen** ficha. Por último, seleccione **compra** toocreate Hola Jenkins VM. Cuando el servidor está listo, recibirá una notificación en hello portal de Azure:   

![Notificación de que Jenkins está listo](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a>Conectar tooJenkins

Navegar por máquina virtual de tooyour (por ejemplo, http://jenkins2517454.eastus.cloudapp.azure.com/) en el explorador web. consola de Hello Jenkins es accesible a través de HTTP no segura, por lo que se proporcionan instrucciones en consola Hola página tooaccess Hola Jenkins forma segura desde su equipo usando un túnel SSH.

![Desbloquear jenkins](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

Configurar el túnel de hello con hello `ssh` comando página Hola desde la línea de comandos de hello, reemplazando `username` con el nombre de Hola de usuario de administrador de máquina virtual de hello elegido anteriormente al configurar la máquina virtual de Hola de plantilla de solución de Hola.

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

Después de haber iniciado túnel hello, navegue toohttp://localhost:8080 / en el equipo local. 

Obtener la contraseña inicial de hello ejecutando el siguiente comando en línea de comandos de hello mientras está conectado a través de SSH toohello Jenkins VM de Hola.

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

Desbloquear el panel de Jenkins Hola para hello primera vez que usa esta contraseña inicial.

![Desbloquear jenkins](./media/install-jenkins-solution-template/jenkins-unlock.png)

Seleccione **instalar complementos sugerido** en hello, página siguiente y, a continuación, crear un panel Jenkins admin usuario utiliza tooaccess Hola Jenkins.

![Jenkins ya está listo.](./media/install-jenkins-solution-template/jenkins-welcome.png)

Hola Jenkins servidor está listo toobuild código.

## <a name="create-your-first-job"></a>Creación del primer trabajo

Seleccione **crear trabajos nuevos** desde la consola de Jenkins hello, a continuación, asígnele el nombre **mySampleApp** y seleccione **proyecto estilo libre**, a continuación, seleccione **Aceptar**.

![Crear un nuevo trabajo](./media/install-jenkins-solution-template/jenkins-new-job.png) 

Seleccione hello **administración de código fuente** ficha, habilite **Git**y escriba Hola después de la dirección URL en **dirección URL de repositorio** campo:`https://github.com/spring-guides/gs-spring-boot.git`

![Definir el repositorio de Git Hola](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

Seleccione hello **generar** y, después, seleccione **agregar el paso de compilación**, **Gradle invocar script**. Seleccione **Use Gradle Wrapper** (Usar contenedor de Gradle). A continuación, escriba `complete` en **Wrapper location** (Ubicación del contenedor) y `build` en **Tasks** (Tareas).

![Usar hello Gradle contenedor toobuild](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

Seleccione **Advanced** (Avanzadas) y, a continuación, escriba `complete` en hello **raíz Generar script** campo. Seleccione **Guardar**.

![Establecer la configuración avanzada en el paso de compilación de contenedor de hello Gradle](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a>Compilar código de hello

Seleccione **generar ahora** toocompile Hola código y el paquete Hola aplicación de ejemplo. Cuando se complete la compilación, seleccione hello **área de trabajo** vínculo de proyecto Hola.

![Examinar toohello el archivo JAR de área de trabajo tooget Hola de compilación de Hola](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

Navegue demasiado`complete/build/libs` y asegúrese de hello `gs-spring-boot-0.1.0.jar` hay tooverify que la compilación fue correcta. Sus Jenkins servidor ahora está listo toobuild sus propios proyectos de Azure.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Agregar máquinas virtuales de Azure como agentes de Jenkins](jenkins-azure-vm-agents.md)
