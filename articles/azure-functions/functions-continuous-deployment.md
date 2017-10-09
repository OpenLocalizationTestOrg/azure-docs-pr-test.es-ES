---
title: "implementación de aaaContinuous para las funciones de Azure | Documentos de Microsoft"
description: "Utilizar servicios de implementación continua del servicio de aplicaciones de Azure toopublish las funciones de Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 28c44f737dad3feab3cf54f7dd42b6a978d0617e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-for-azure-functions"></a>Implementación continua para Azure Functions
Las funciones de Azure hace fácil toodeploy la aplicación de función mediante la integración continua de servicio de aplicaciones. Functions se integra con BitBucket, Dropbox, GitHub y Visual Studio Team Services (VSTS). Esto permite que un flujo de trabajo que actualiza el código de la función realizada mediante uno de estos tooAzure de implementación del desencadenador de servicios integrados. Si son nuevas funciones de tooAzure, comience con [información general de las funciones de Azure](functions-overview.md).

La implementación continua representa una buena opción para los proyectos donde se integran contribuciones diversas y frecuentes. También le permite mantener el control de código fuente en el código de las funciones. actualmente se admite Hola siguientes orígenes de implementación:

* [Bitbucket](https://bitbucket.org/)
* [Dropbox](https://www.dropbox.com/)
* Repositorio externo (Git o Mercurial)
* [Repositorio local de GIT](../app-service-web/app-service-deploy-local-git.md)
* [GitHub](https://github.com)
* [OneDrive](https://onedrive.live.com/)
* [Visual Studio Team Services](https://www.visualstudio.com/team-services/)

Las implementaciones se configuran por Function App. Después de habilita la implementación continua, código de acceso toofunction en el portal de Hola se establece demasiado*de sólo lectura*.

## <a name="continuous-deployment-requirements"></a>Requisitos de implementación continua

Debe tener configurado el origen de la implementación y el código de las funciones en el origen de la implementación de hello antes de configurar la implementación continua. En una implementación de aplicación de la función especificada, cada función reside en un subdirectorio con nombre, donde el nombre del directorio de hello es nombre Hola de función hello.  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a>Configurar la implementación continua
Utilice este procedimiento tooconfigure la implementación continua para una aplicación de función existente. Estos pasos muestran la integración con un repositorio de GitHub, aunque se aplican pasos similares para Visual Studio Team Services u otros servicios de implementación.

1. En la aplicación de la función en hello [portal de Azure](https://portal.azure.com), haga clic en **características de la plataforma** y **opciones de implementación**. 
   
    ![Configurar implementación continua](./media/functions-continuous-deployment/setup-deployment.png)
 
2. A continuación, en hello **implementaciones** hoja haga clic en **el programa de instalación**.
 
    ![Configurar implementación continua](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. Hola **origen de la implementación** hoja, haga clic en **Elegir origen**, a continuación, rellene la información de hello para el origen de implementación elegido y haga clic en **Aceptar**.
   
    ![Elegir origen de la implementación](./media/functions-continuous-deployment/choose-deployment-source.png)

Después de configura una implementación continua, todos los cambios de archivo en el origen de implementación son copiados toohello función aplicación y se desencadena una implementación completa. Cuando se actualizan los archivos de origen de hello, sitio Hola se vuelve a implementar.

## <a name="deployment-options"></a>Opciones de implementación

siguiente Hola se muestran algunos escenarios típicos de implementación:

- [Creación de una implementación de ensayo](#staging)
- [Mover la implementación de toocontinuous de funciones existente](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a>Creación de una implementación de ensayo

Las aplicaciones de función todavía no admiten espacios de implementación. Sin embargo, todavía puede administrar implementaciones de ensayo y producción independientes mediante la integración continua.

Hola tooconfigure de proceso y trabajar con una implementación de ensayo generalmente es similar a esto:

1. Cree dos aplicaciones en función de su suscripción, uno para el código de producción de hello y otro para el almacenamiento provisional. 

2. Cree un origen de la implementación, si aún no tiene uno. En este ejemplo se usa [GitHub].

3. Para la aplicación de función de producción, los pasos de hello completa anterior **configurar la implementación continua** y conjunto Hola implementación bifurcación toohello bifurcación principal de su repositorio de GitHub.
   
    ![Elegir rama de la implementación](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. Repita este paso para la aplicación de la función de almacenamiento provisional de Hola, pero elija Hola rama de ensayo en su lugar en el repositorio de GitHub. Si el origen de la implementación no admite la bifurcación, utilice una carpeta diferente.
    
5. Realizar actualizaciones tooyour código de hello bifurcación o carpeta de almacenamiento provisional, a continuación, comprobar que esos cambios se reflejan en la implementación de ensayo de Hola.

6. Después de probar, combinar los cambios de bifurcación de almacenamiento provisional de hello en la bifurcación principal de Hola. Esta combinación desencadenadores toohello producción función aplicación de la implementación. Si el origen de la implementación no es compatible con bifurcaciones, sobrescriba los archivos de hello en la carpeta de producción de hello con archivos de Hola de Hola carpeta de almacenamiento provisional.

<a name="existing"></a>
### <a name="move-existing-functions-toocontinuous-deployment"></a>Mover la implementación de toocontinuous de funciones existente
Cuando tenga las funciones existentes que ha creado y mantiene en el portal de hello, necesita toodownload sus función archivos de código mediante FTP o hello repositorio Git local para poder configurar la implementación continua como se describió anteriormente. Para hacer esto en hello configuración de servicio de aplicaciones para la aplicación de la función. Después de descargan los archivos, puede cargarlos de origen de la implementación continua de tooyour elegido.

> [!NOTE]
> Después de configurar la integración continua, ya no será capaz de tooedit el origen de los archivos en el portal de funciones de Hola.

- [Configuración de las credenciales de implementación](#credentials)
- [Descarga de archivos mediante FTP](#downftp)
- [Cómo: descargar archivos mediante el repositorio de Git local Hola](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a>Configuración de las credenciales de implementación
Para poder descargar archivos desde la aplicación de la función con FTP o en el repositorio de Git local, debe configurar el sitio de hello tooaccess de credenciales. Las credenciales se establecen en el nivel de aplicación de función hello. Use Hola siguientes pasos le indican las credenciales de la implementación de tooset Hola portal de Azure:

1. En la aplicación de la función en hello [portal de Azure](https://portal.azure.com), haga clic en **características de la plataforma** y **las credenciales de implementación**.
   
    ![Configurar credenciales de implementación locales](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. Escriba un nombre de usuario y una contraseña y haga clic en **Guardar**. Ahora puede usar estos tooaccess las credenciales de la aplicación de la función de FTP o hello repositorio Git integrado.

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a>Descarga de archivos mediante FTP

1. En la aplicación de la función en hello [portal de Azure](https://portal.azure.com), haga clic en **características de la plataforma** y **propiedades**, a continuación, copie los valores de hello para **FTP/implementación usuario**, **Nombre de Host FTP**, y **nombre de Host FTPS**.  

    **Usuario de implementación/FTP** debe especificarse como se muestra en el portal de hello, incluidos el nombre de la aplicación hello, tooprovide contexto adecuado para el servidor FTP de Hola.
   
    ![Obtener la información de implementación](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. Desde el cliente FTP, use información de conexión de Hola que recopiló tooconnect tooyour aplicación y descargar archivos de origen de Hola para sus funciones.

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a>Descarga de archivos mediante el repositorio local de Git

1. En la aplicación de la función en hello [portal de Azure](https://portal.azure.com), haga clic en **características de la plataforma** y **opciones de implementación**. 
   
    ![Configurar implementación continua](./media/functions-continuous-deployment/setup-deployment.png)
 
2. A continuación, en hello **implementaciones** hoja haga clic en **el programa de instalación**.
 
    ![Configurar implementación continua](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. Hola **origen de la implementación** hoja, haga clic en **repositorio de Git Local** y, a continuación, haga clic en **Aceptar**.

3. En **características de la plataforma**, haga clic en **propiedades** y anote el valor de Hola de dirección URL de Git. 
   
    ![Configurar implementación continua](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. Clonar el repositorio de hello en el equipo local mediante un símbolo del sistema compatible con Git o su herramienta preferida de Git. comando de clonación de Git Hello tiene el siguiente aspecto:
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. Capturar los archivos de su clonación toohello de aplicación de función en el equipo local, como en el siguiente ejemplo de Hola:
   
        git pull origin master
   
    Si se le piden, proporcione las [credenciales de implementación configuradas](#credentials).  

[GitHub]: https://github.com/
