---
title: aplicaciones web aaaCreating con matraz en Azure
description: "Un tutorial que le presenta toorunning una aplicación web de Python en Azure."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: b7f4ca3a-0b52-4108-90a7-f7e07ac73da0
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/20/2016
ms.author: huvalo
ms.openlocfilehash: 3362047b3106b4380b5971e47cbd8042d38a792b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a>Creación de aplicaciones web con Flask en Azure
Este tutorial describe cómo tooget comenzó a ejecutarse Python en [aplicaciones de Web del servicio de aplicación de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).  Aplicaciones web ofrece hospedaje gratuito limitado y una implementación rápida. Además, ahora también se puede usar Python.  Medida que crezca su aplicación, puede cambiar toopaid de hospedaje y también se puede integrar con todos Hola otros servicios de Azure.

Se creará una aplicación con el marco de trabajo de hello matraz web (vea versiones alternativas de este tutorial para [Django](web-sites-python-create-deploy-django-app.md) y [Bottle](web-sites-python-create-deploy-bottle-app.md)).  Se crear sitio Web de Hola de hello Galería de Azure, configure la implementación de Git y clonar el repositorio de hello localmente.  A continuación, se ejecuta la aplicación hello localmente, realizar cambios, confirmar e insertarlas tooAzure.  Hola tutorial se muestra cómo toodo de Windows o Mac y Linux.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="prerequisites"></a>Requisitos previos
* Windows, Mac o Linux
* Python 2.7 o 3.4
* setuptools, pip, virtualenv (solo en Python 2.7)
* Git
* [Python Tools para Visual Studio][Python Tools para Visual Studio] (PTVS)- Nota: Esto es opcional

**Nota:**la publicación TFS no se admite actualmente para los proyectos de Python.

### <a name="windows"></a>Windows
Si aún no tiene Python 2.7 o 3.4 instalado (32 bits), se recomienda instalar [Azure SDK para Python 2.7] o [Azure SDK para Python 3.4] mediante el instalador de plataforma web.  Esto instala la versión de 32 bits de Hola de Python, setuptools, pip, virtualenv, etcetera (32-bit Python es lo que se instala en equipos de host de Azure de hello).  También puede obtener Python en [python.org].

Para Git, recomendamos [Git para Windows] o [GitHub para Windows].  Si utiliza Visual Studio, puede usar soporte técnico de Git de hello integrado.

También se recomienda instalar [Python Tools 2.2 para Visual Studio].  Esto es opcional, pero si tiene [Visual Studio], incluidos Hola liberar Visual Studio Community 2013 o Visual Studio Express 2013 para Web, a continuación, esto le proporcionará un excelente IDE de Python.

### <a name="maclinux"></a>Mac o Linux:
Debe tener Python y Git instalados, pero asegúrese de que tiene Python 2.7 o 3.4.

## <a name="web-app-create-on-hello-azure-portal"></a>Crear aplicación Web en hello Portal de Azure
primer paso para crear la aplicación Hello es toocreate hello web app mediante hello [Portal de Azure](https://portal.azure.com). 

1. Inicie sesión en hello Portal de Azure y haga clic en hello **NEW** botón en la esquina izquierda inferior de Hola. 
2. Haga clic en **Web y móvil**.
3. En el cuadro de búsqueda de hello, escriba "python".
4. En los resultados de la búsqueda de hello, seleccione **matraz**, a continuación, haga clic en **crear**.
5. Configurar aplicación de matraz nueva hello, como la creación de un nuevo plan de servicio de aplicaciones y un nuevo grupo de recursos para él. A continuación, haga clic en **Crear**.
6. Configurar la publicación de Git de la aplicación web recién creado siguiendo las instrucciones de hello en [tooAzure servicio de aplicaciones de la implementación de Git Local](app-service-deploy-local-git.md).

## <a name="application-overview"></a>Información general de la aplicación
### <a name="git-repository-contents"></a>Contenido del repositorio de Git
Esta es una visión general de los archivos de Hola que encontrará en el repositorio de Git inicial hello, que se podrá clonar en la sección siguiente de Hola.

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

Orígenes principales de la aplicación hello.  Consta de tres páginas (índice, acerca de, contacto) con un diseño principal.  El contenido estático y los scripts incluyen bootstrap, jquery, modernizr y respond.

    \runserver.py

Compatibilidad con servidor de desarrollo local. Use esta aplicación de hello toorun localmente.

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

Archivos de proyecto para su uso con [Python Tools para Visual Studio].

    \ptvs_virtualenv_proxy.py

Proxy IIS para entornos virtuales y compatibilidad con la depuración remota de PTVS.

    \requirements.txt

Paquetes externos necesarios para esta aplicación. script de implementación de Hola pip paquetes de Hola de instalación incluidos en este archivo.

    \web.2.7.config
    \web.3.4.config

Archivos de configuración de IIS.  script de implementación de Hello usará web.x.y.config adecuado de Hola y copiar como web.config.

### <a name="optional-files---customizing-deployment"></a>Archivos opcionales - Implementación de personalización
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>Archivos opcionales - Tiempo de ejecución de Python
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>Archivos adicionales en el servidor
Algunos archivos existen en el servidor de hello pero no se agregan toohello repositorio de git.  Estos se crean mediante el script de implementación de Hola.

    \web.config

Archivo de configuración de IIS.  Se crea desde web.x.y.config en cada implementación.

    \env\

Entorno virtual de Python.  Si aún no existe un entorno virtual compatible en la aplicación hello, creados durante la implementación.  Paquetes incluidos en requirements.txt son pip instalado, pero pip omitirá la instalación si ya se han instalado paquetes de saludo.

Hello 3 secciones describen cómo tooproceed con hello web desarrollo de aplicaciones en 3 entornos diferentes:

* Windows, con Python Tools para Visual Studio
* Windows, con línea de comandos
* Mac/Linux, con línea de comandos

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>Desarrollo de aplicaciones web: Windows, Python Tools para Visual Studio
### <a name="clone-hello-repository"></a>Repositorio de Hola de clon
En primer lugar, clonar el repositorio de hello mediante dirección URL de hello proporcionada en hello Portal de Azure. Para obtener más información, consulte [tooAzure servicio de aplicaciones de la implementación de Git Local](app-service-deploy-local-git.md).

Hola abrir archivo de solución (.sln) que se incluye en la raíz de hello del repositorio de Hola.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a>Creación de un entorno virtual
Ahora vamos a crear un entorno virtual para el desarrollo local.  Haga clic con el botón secundario en **Entornos de Python** y elija **Agregar entorno virtual...**

* Asegúrese de que nombre hello del entorno de hello es `env`.
* Seleccione intérprete base Hola.  Asegúrese de que toouse Hola la misma versión de Python que está seleccionada para la aplicación web (en runtime.txt o hello **configuración de la aplicación** hoja de la aplicación web en hello Portal de Azure).
* Asegúrese de que esté marcada Hola opción toodownload e instalar los paquetes.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

Haga clic en **Crear**.  Esto se crear entorno virtual de hello e instalar las dependencias en requirements.txt.

### <a name="run-using-development-server"></a>Ejecución con el servidor de desarrollo
Presione F5 toostart depuración y el explorador web abrirá automáticamente página toohello que se ejecuta localmente.

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

Puede establecer puntos de interrupción en orígenes de hello, las ventanas de inspección de uso hello, etcetera.  Vea hello [Python Tools para la documentación de Visual Studio] para obtener más información sobre Hola distintas características.

### <a name="make-changes"></a>Realización de cambios
Ahora puede experimentar realizando cambios toohello aplicación orígenes o plantillas.

Después de haberlo probado los cambios, confirmarlos toohello repositorio de Git:

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a>Instalación de más paquetes
La aplicación puede tener otras dependencias, aparte de Python y Flask.

Puede instalar paquetes adicionales con pip.  tooinstall un paquete, haga doble clic en entorno virtual de Hola y seleccione **instalar un paquete de Python**.

Por ejemplo, tooinstall hello Azure SDK para Python, que proporciona acceso tooAzure almacenamiento, bus de servicio y otros servicios de Azure, escriba `azure`:

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

Haga doble clic en el entorno virtual de Hola y seleccione **generar requirements.txt** tooupdate requirements.txt.

A continuación, confirmar el repositorio de Git de hello cambios toorequirements.txt toohello.

### <a name="deploy-tooazure"></a>Implementar tooAzure
tootrigger una implementación, haga clic en **sincronización** o **Push**.  La sincronización realiza una inserción y una extracción.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

primera implementación de Hello tardará algún tiempo, tal y como se va a crear un entorno virtual, paquetes de instalación, etcetera.

Visual Studio no muestra el progreso de Hola de implementación de Hola.  Si desea que la salida de hello tooreview, vea la sección Hola en [solución de problemas - implementación](#troubleshooting-deployment).

Examinar los cambios de toohello tooview de dirección URL de Azure.

## <a name="web-app-development---windows---command-line"></a>Desarrollo de aplicaciones web - Windows - Línea de comandos
### <a name="clone-hello-repository"></a>Repositorio de Hola de clon
En primer lugar, clonar el repositorio de hello mediante dirección URL de hello proporcionada en hello Portal de Azure y agregar hello Azure repositorio como un control remoto. Para obtener más información, consulte [tooAzure servicio de aplicaciones de la implementación de Git Local](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Creación de un entorno virtual
Vamos a crear un nuevo entorno virtual para fines de desarrollo (no lo agregue toohello repositorio).  Los entornos virtuales de Python no son reubicables, por lo que cada desarrollador que trabaja en la aplicación hello creará su propias localmente.

Asegúrese de que toouse Hola la misma versión de Python que está seleccionada para la aplicación web (en runtime.txt o hello **configuración de la aplicación** hoja de la aplicación web en hello Portal de Azure).

Para Python 2.7:

    c:\python27\python.exe -m virtualenv env

Para Python 3.4:

    c:\python34\python.exe -m venv env

Instale los paquetes externos requeridos por la aplicación. Puede usar el archivo de requirements.txt de hello en raíz de Hola de paquetes de saludo repositorio tooinstall hello en su entorno virtual:

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a>Ejecución con el servidor de desarrollo
Puede iniciar la aplicación hello en un servidor de desarrollo con hello siguiente comando:

    env\scripts\python runserver.py

consola de Hola mostrará la dirección URL de Hola y escucha servidor hello de puertos:

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

A continuación, abra la dirección URL toothat del explorador web.

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a>Realización de cambios
Ahora puede experimentar realizando cambios toohello aplicación orígenes o plantillas.

Después de haberlo probado los cambios, confirmarlos toohello repositorio de Git:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Instalación de más paquetes
La aplicación puede tener otras dependencias, aparte de Python y Flask.

Puede instalar paquetes adicionales con pip.  Por ejemplo, tooinstall hello Azure SDK para Python, que proporciona acceso tooAzure almacenamiento, bus de servicio y otros servicios de Azure, escriba:

    env\scripts\pip install azure

Asegúrese de que requirements.txt tooupdate:

    env\scripts\pip freeze > requirements.txt

Confirmar cambios de hello:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>Implementar tooAzure
una implementación de tootrigger, Hola de inserción cambia tooAzure:

    git push azure master

Se obtiene un resultado de hello del script de implementación de hello, incluida la creación del entorno virtual, instalación de paquetes, la creación del archivo web.config.

Examinar los cambios de toohello tooview de dirección URL de Azure.

## <a name="web-app-development---maclinux---command-line"></a>Desarrollo de aplicaciones web: Mac/Linux - Línea de comandos
### <a name="clone-hello-repository"></a>Repositorio de Hola de clon
En primer lugar, clonar el repositorio de hello mediante dirección URL de hello proporcionada en hello Portal de Azure y agregar hello Azure repositorio como un control remoto. Para obtener más información, consulte [tooAzure servicio de aplicaciones de la implementación de Git Local](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Creación de un entorno virtual
Vamos a crear un nuevo entorno virtual para fines de desarrollo (no lo agregue toohello repositorio).  Los entornos virtuales de Python no son reubicables, por lo que cada desarrollador que trabaja en la aplicación hello creará su propias localmente.

Asegúrese de que toouse Hola la misma versión de Python que está seleccionada para la aplicación web (en runtime.txt o hello **configuración de la aplicación** hoja de la aplicación web en hello Portal de Azure).

Para Python 2.7:

    python -m virtualenv env

Para Python 3.4:

    python -m venv env
o pyvenv env

Instale los paquetes externos requeridos por la aplicación. Puede usar el archivo de requirements.txt de hello en raíz de Hola de paquetes de saludo repositorio tooinstall hello en su entorno virtual:

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a>Ejecución con el servidor de desarrollo
Puede iniciar la aplicación hello en un servidor de desarrollo con hello siguiente comando:

    env/bin/python runserver.py

consola de Hola mostrará la dirección URL de Hola y escucha servidor hello de puertos:

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

A continuación, abra la dirección URL toothat del explorador web.

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a>Realización de cambios
Ahora puede experimentar realizando cambios toohello aplicación orígenes o plantillas.

Después de haberlo probado los cambios, confirmarlos toohello repositorio de Git:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Instalación de más paquetes
La aplicación puede tener otras dependencias, aparte de Python y Flask.

Puede instalar paquetes adicionales con pip.  Por ejemplo, tooinstall hello Azure SDK para Python, que proporciona acceso tooAzure almacenamiento, bus de servicio y otros servicios de Azure, escriba:

    env/bin/pip install azure

Asegúrese de que requirements.txt tooupdate:

    env/bin/pip freeze > requirements.txt

Confirmar cambios de hello:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>Implementar tooAzure
una implementación de tootrigger, Hola de inserción cambia tooAzure:

    git push azure master

Se obtiene un resultado de hello del script de implementación de hello, incluida la creación del entorno virtual, instalación de paquetes, la creación del archivo web.config.

Examinar los cambios de toohello tooview de dirección URL de Azure.

## <a name="troubleshooting---package-installation"></a>Solución de problemas - Instalación de un paquete
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Solución de problemas - Entorno virtual
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>Pasos siguientes
Siga estos toolearn de vínculos más sobre matraz y Python Tools para Visual Studio: 

* [Documentación de Flask]
* [Python Tools para la documentación de Visual Studio]

Para obtener información sobre el uso de Almacenamiento de tablas de Azure y MongoDB:

* [Flask y MongoDB en Azure con Python Tools para Visual Studio]
* [Flask y Almacenamiento de tablas de Azure en Azure con Python Tools para Visual Studio]

Para obtener más información, vea también hello [Centro para desarrolladores de Python](/develop/python/).

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Flask y MongoDB en Azure con Python Tools para Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure
[Flask y Almacenamiento de tablas de Azure en Azure con Python Tools para Visual Studio]: web-sites-python-ptvs-flask-table-storage.md

<!--External Link references-->
[Azure SDK para Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[Azure SDK para Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git para Windows]: http://msysgit.github.io/
[GitHub para Windows]: https://windows.github.com/
[Python Tools para Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[Python Tools para la documentación de Visual Studio]: http://aka.ms/ptvsdocs
[Documentación de Flask]: http://flask.pocoo.org/ 

