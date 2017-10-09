---
title: "Implementación de Git de aaaLocal tooAzure servicio de aplicaciones"
description: "Obtenga información acerca de cómo tooenable local Git implementación tooAzure servicio de aplicaciones."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 1905e0b7acd58d8dd6496a14f6e4f38f9f8c0212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="local-git-deployment-tooazure-app-service"></a>TooAzure de implementación de Git local servicio de aplicaciones
Este tutorial muestra cómo toodeploy su aplicación demasiado[servicio de aplicaciones de Azure] desde un repositorio de Git en el equipo local. Servicio de aplicaciones es compatible con este enfoque con hello **Git Local** opción de implementación en hello [Portal de Azure].  
Muchos de los comandos de Git Hola se describe en este artículo se realizan automáticamente al crear una aplicación de servicio de aplicaciones con hello [interfaz de línea de comandos de Azure] tal como se describe [aquí](app-service-web-get-started.md).

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tutorial, necesita:

* Git. Puede descargar los binarios de instalación de hello [aquí](http://www.git-scm.com/downloads).  
* Conocimientos básicos de Git.
* Una cuenta de Microsoft Azure. Si aún no tiene ninguna, puede [registrarse para una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial) o [activar las ventajas de suscriptor de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.  
> 
> 

## <a name="Step1"></a>Paso 1: Creación de un repositorio local
Realizar Hola después tareas toocreate un nuevo repositorio Git.

1. Inicie una herramienta de línea de comandos, como **GitBash** (Windows) o **Bash** (shell de Unix). En sistemas de OS X pueden acceder a los Hola de línea de comandos a través de hello **Terminal** aplicación.
2. Navegue directorio toohello donde esté ubicado toodeploy contenido Hola.
3. Usar hello después de un nuevo repositorio Git del comando tooinitialize:

```bash  
git init
```

## <a name="Step2"></a>Paso 2: Confirmación del contenido
El Servicio de aplicaciones admite aplicaciones creadas en varios lenguajes de programación. 

1. Si el repositorio ya incluye contenido omitir este punto y mover toopoint 2 a continuación. Si el repositorio todavía no incluye contenido, simplemente llénelo con un archivo .html estático, tal como se indica a continuación: 
   
   * Con un editor de texto, cree un nuevo archivo denominado **index.html** en raíz de hello del repositorio de Git Hola
   * Agregar Hola después de texto como contenido de Hola para index.html Hola de archivo y guárdelo: *Git Hola!*
2. Desde la línea de comandos de hello, compruebe que se encuentra bajo la raíz de Hola de su repositorio de Git. A continuación, usar hello después de repositorio de comando tooadd archivos tooyour:

```bash  
git add -A
```
3. A continuación, confirmar toohello repositorio de hello cambios mediante el uso de hello siguiente comando:

```bash  
git commit -m "Hello Azure App Service"
```  

## <a name="Step3"></a>Paso 3: Habilitar Hola repositorio de aplicación de servicio de aplicaciones
Realizar Hola siguiendo los pasos tooenable un repositorio Git para la aplicación de servicio de aplicaciones.

1. Inicie sesión en toohello [Portal de Azure].
2. En la hoja de su aplicación de App Service, haga clic en **Configuración > Origen de implementación**. Haga clic en **Elegir recurso**, luego en **Repositorio de Git local** y, finalmente, en **Aceptar**.  
   
    ![Repositorio de Git local](./media/app-service-deploy-local-git/local_git_selection.png)
3. Si se trata de la primera configuración de tiempo de un repositorio de Azure, necesita credenciales de inicio de sesión de toocreate para él. Se usará ellos toolog en hello Azure repositorio e insertar los cambios desde el repositorio Git local. En la hoja de la aplicación, haga clic en **Configuración > Credenciales de implementación** y configure el nombre de usuario y la contraseña de la implementación. Cuando haya terminado, haga clic en **Guardar**.
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <a name="Step4"></a>Paso 4: Implementación del proyecto
Usar hello siguiendo los pasos toopublish su tooApp mediante Git Local del servicio de aplicación.

1. En la hoja de la aplicación Hola Portal de Azure, haga clic en **configuración > propiedades** para hello **dirección URL de Git**.
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    **Dirección URL de GIT** es Hola referencia remoto toodeploy toofrom el repositorio local. Usará esta dirección URL en hello pasos.
2. Use Hola de línea de comandos, para comprobar que está en la raíz de Hola de su repositorio de Git local.
3. Use `git remote` aparece en referencia tooadd Hola remoto **dirección URL de Git** del paso 1. El comando tendrá un aspecto similar siguiente toohello:
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > Hola **remoto** comando agrega un repositorio remoto de tooa de referencia con nombre. En este ejemplo, se crea una referencia llamada "azure" para el repositorio de la aplicación web.
   > 
   > 
4. Insertar el contenido tooApp servicio usando Hola nueva **azure** remoto que acaba de crear.

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. Volver atrás tooyour aplicación Hola Portal de Azure. Una entrada del registro de la última inserción debe mostrarse en hello **implementaciones** hoja. 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. Haga clic en hello **examinar** situado en la parte superior de Hola de Hola de tooverify de hoja de la aplicación hello contenido se ha implementado. 

## <a name="Step5"></a>Solución de problemas
siguiente Hola es errores o problemas más comunes al usar Git toopublish tooan aplicación de servicio de aplicaciones en Azure:

- - -
**Síntoma**: no se puede tooaccess '[siteURL]': no se pudo tooconnect demasiado [scmAddress]

**Causa**: este error puede producirse si la aplicación hello no se está ejecutando.

**Resolución de**: inicio de aplicación de hello en hello Portal de Azure. Implementación de GIT no funcionará a menos que se ejecuta la aplicación hello. 

- - -
**Síntoma**: no se pudo resolver el host "nombre de host".

**Causa**: este error puede producirse si escribe la información de dirección de hello al crear hello 'azure' remoto era incorrecto.

**Resolución**: Hola uso `git remote -v` comando toolist todos los controles remotos, junto con la dirección URL de hello asociado. Compruebe que la dirección URL de Hola para hello 'azure' remoto es correcto. Si es necesario, quitar y volver a crear este remoto con la dirección URL correcta de Hola.

- - -
**Síntoma**: no hay referencias en común y no se ha especificado nada; sin hacer nada. Quizá hay que especificar una rama como "principal".

**Causa**: este error puede producirse si no especifica una bifurcación al realizar una operación de inserción de git y tener no hello push.default valor establecido utilizando Git.

**Resolución**: realizar la operación de inserción de hello nuevo, especificando la bifurcación principal de Hola. Por ejemplo:

```bash  
git push azure master
```
- - -
**Síntoma**: src refspec [branchname] no coincide con ninguna.

**Causa**: este error puede producirse si intenta toopush tooa rama distinta de la maestra en hello 'azure' remoto.

**Resolución**: realizar la operación de inserción de hello nuevo, especificando la bifurcación principal de Hola. Por ejemplo:

```bash  
git push azure master
```
- - -
**Síntoma**: error de RPC; resultado=22; código HTTP=502.

**Causa**: este error puede producirse si intenta toopush un repositorio git grandes a través de HTTPS.

**Resolución**: cambiar la configuración de git hello en enviamos de Hola de hello máquina local toomake más grande

```bash  
git config --global http.postBuffer 524288000
```
- - -
**Síntoma**: Error: repositorio de tooremote Confirmar cambios pero la aplicación web no actualizada.

**Causa**: este error puede ocurrir si está implementando una aplicación Node.js que contiene un archivo package.json que especifica módulos requeridos adicionales.

**Resolución**: los mensajes adicionales que contienen 'npm ERR!' debe ser error toothis anterior ha iniciado y puede proporcionar contexto adicional en caso de error de Hola. siguiente Hola se conocen las causas de este error y Hola correspondiente 'npm ERR!' correspondiente:

* **Archivo package.json con estructura incorrecta**: npm ERR! No se pudieron leer las dependencias.
* **Módulo nativo que no tiene una distribución binaria para Windows**:
  
  * npm ERR! \`cmd "/c" "node-gyp rebuild"\` failed with 1
    
      OR
  * npm ERR! [modulename@version] preinstall: \`make || gmake\`

## <a name="additional-resources"></a>Recursos adicionales
* [Documentación de Git](http://git-scm.com/documentation)
* [Documentación de Project Kudu](https://github.com/projectkudu/kudu/wiki)
* [Implementación continua tooAzure servicio de aplicaciones](app-service-continuous-deployment.md)
* [¿Cómo toouse PowerShell de Azure](/powershell/azure/overview)
* [¿Cómo toouse Hola interfaz de línea de comandos de Azure](../cli-install-nodejs.md)

[servicio de aplicaciones de Azure]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[Portal de Azure]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[interfaz de línea de comandos de Azure]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
