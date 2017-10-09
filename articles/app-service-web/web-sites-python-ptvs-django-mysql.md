---
title: aaaDjango y MySQL en Azure con Python Tools 2.2 para Visual Studio
description: "Obtenga información acerca de cómo toouse Hola Python Tools para Visual Studio toocreate una aplicación web Django que almacena datos en una instancia de base de datos MySQL y lo implementará tooAzure aplicación del servicio Web de aplicaciones."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1597c391d20c8e8ef629b4e4d05c9eb64c83bffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a>Django y MySQL en Azure con Python Tools 2.2 para Visual Studio
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

En este tutorial, usará [Python Tools para Visual Studio](https://www.visualstudio.com/vs/python) sondea de toocreate una sencilla aplicación web con una de las plantillas de ejemplo de Hola PTVS. Aprenderá cómo toouse un servicio MySQL hospedado en Azure, cómo tooconfigure Hola toouse de aplicación web MySQL y cómo toopublish Hola aplicación web demasiado[aplicaciones de Web del servicio de aplicación de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

> [!NOTE]
> información de Hello contenida en este tutorial también está disponible en hello después de vídeo:
> 
> [PTVS 2.1: Django app with MySQL][video] (PTVS 2.1: aplicación Django con MySQL)
> 
> 

Vea hello [Centro para desarrolladores de Python] para ver más artículos que cubren el desarrollo de aplicaciones de Web del servicio de aplicación de Azure con PTVS mediante Bottle por sí solo, matraz y Django web marcos de trabajo, con los servicios de almacenamiento de tabla de Azure, MySQL y base de datos SQL. Aunque en este artículo se centra en el servicio de aplicaciones, los pasos de hello son similares al desarrollar [servicios en la nube].

## <a name="prerequisites"></a>Requisitos previos
* Visual Studio 2015
* [Python 2.7 de 32 bits] o [Python 3.4 de 32 bits]
* [Python Tools 2.2 para Visual Studio]
* [Python Tools 2.2 para Visual Studio ejemplos VSIX]
* [Azure SDK y herramientas para VS 2015]
* Django 1.9 o posterior

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="create-hello-project"></a>Crear proyecto de hello
En esta sección, va a crear un proyecto de Visual Studio con la utilización de una plantilla de ejemplo. Va a crear un entorno virtual e instalar los paquetes necesarios. Va a crear una base de datos local con sqlite. A continuación, ejecutaremos aplicación hello localmente.

1. En Visual Studio, seleccione **Archivo**, **Nuevo proyecto**.
2. Hola plantillas de proyecto de hello [Python Tools 2.2 para Visual Studio ejemplos VSIX] están disponibles en **Python**, **ejemplos**. Seleccione **proyecto Web de sondeos Django** y haga clic en Aceptar toocreate Hola proyecto.
   
    ![Cuadro de diálogo Nuevo proyecto](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. Es posible que los paquetes externos tooinstall solicitadas. Seleccione **Instalar en un entorno virtual**.
   
    ![Cuadro de diálogo Paquetes externos](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. Seleccione **Python 2.7** o **3.4 de Python** como intérprete base Hola.
   
    ![Cuadro de diálogo Agregar entorno virtual](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. En **el Explorador de soluciones**, haga doble clic en el nodo del proyecto de Hola y seleccione **Python**y, a continuación, seleccione **Django migrar**.  Después, seleccione **Django Create Superuser (Crear superusuario de Django)**.
6. Se abrirá una consola de administración de Django y crear una base de datos de sqlite en la carpeta del proyecto Hola. Siga los mensajes de Hola toocreate un usuario.
7. Confirme que la aplicación hello funciona presionando `F5`.
8. Haga clic en **sesión** de barra de navegación superior de Hola Hola.
   
    ![Barra de navegación de Django](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. Escriba las credenciales de hello para el usuario de Hola que creó al sincronizar base de datos de Hola.
   
    ![Formulario de inicio de sesión](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. Haga clic en **Create Sample Polls**(Crear sondeos de ejemplo).
    
     ![Create Sample Polls](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. Haga clic en un sondeo y vote.
    
     ![Votación en sondeos de ejemplo](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a>Creación de una base de datos MySQL
Para base de datos de hello, creará una base de datos ClearDB MySQL hospedado en Azure.

Como alternativa, puede crear su propia máquina virtual para que se ejecute en Azure y, a continuación, instalar y administrar MySQL por su cuenta.

Siga estos pasos para crear una base de datos con un plan gratuito.

1. Inicie sesión en toohello [Portal de Azure].
2. En la parte superior del panel de navegación de Hola Hola, haga clic en **NEW**, a continuación, haga clic en **datos + almacenamiento**y, a continuación, haga clic en **base de datos MySQL**.
3. Configurar base de datos de MySQL nueva hello mediante la creación de un nuevo grupo de recursos y seleccione la ubicación adecuada de hello para el mismo.
4. Una vez que se crea la base de datos de MySQL de hello, haga clic en **propiedades** en la hoja de la base de datos de Hola.
5. Usar valor Hola copia botón tooput Hola de **cadena de conexión** en Portapapeles Hola.

## <a name="configure-hello-project"></a>Configurar proyecto Hola
En esta sección, configurará la aplicación toouse Hola MySQL base de datos web que acaba de crear. También deberá instalar bases de datos de MySQL de toouse necesarios adicionales paquetes de Python con Django. A continuación, podrá ejecutar aplicación de hello web localmente.

1. En Visual Studio, abra **settings.py**, de hello *ProjectName* carpeta. Pegue temporalmente cadena de conexión de hello en el editor de Hola. cadena de conexión de Hello tiene este formato:
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    Base de datos de cambio Hola predeterminada **motor** toouse MySQL y establezca Hola valores para **nombre**, **usuario**, **contraseña** y  **HOST** de hello **CONNECTIONSTRING**.
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. En el Explorador de soluciones, bajo **entornos de Python**, haga doble clic en el entorno virtual de Hola y seleccione **instalar un paquete de Python**.
3. Instalar el paquete de hello `mysqlclient` con **pip**.
   
    ![Cuadro de diálogo Instalar paquete](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. En **el Explorador de soluciones**, haga doble clic en el nodo del proyecto de Hola y seleccione **Python**y, a continuación, seleccione **Django migrar**.  Después, seleccione **Django Create Superuser (Crear superusuario de Django)**.
   
    Esto creará tablas de hello para la base de datos de MySQL de Hola que creó en la sección anterior de Hola. Siga los mensajes de Hola toocreate un usuario, que no tiene el usuario de hello toomatch en base de datos de sqlite de hello creado en la primera sección de este artículo de Hola.
5. Ejecutar la aplicación hello con `F5`. Sondeos que se crean con **crear sondeos de ejemplo** y se van a serializar datos Hola enviados votando en la base de datos de MySQL de Hola.

## <a name="publish-hello-web-app-tooazure-app-service"></a>Publicar hello web app tooAzure servicio de aplicaciones
Hello Azure SDK para .NET proporciona una manera sencilla de toodeploy su tooAzure de aplicación web servicio de aplicaciones.

1. En **el Explorador de soluciones**, haga doble clic en el nodo del proyecto de Hola y seleccione **publicar**.
   
    ![Cuadro de diálogo Publicación web](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. Haga clic en **Servicio de aplicaciones de Microsoft Azure**.
3. Haga clic en **New** toocreate una nueva aplicación web.
4. Rellene Hola después de campos y haga clic en **crear**:
   
   * **Nombre de aplicación web**
   * **Plan del Servicio de aplicaciones**
   * **Grupos de recursos**
   * **Región**
   * Deje **servidor de base de datos** establecido demasiado**ninguna base de datos**
5. Acepte todos los valores predeterminados y haga clic en **Publicar**.
6. El explorador web abrirá automáticamente aplicaciones web publicadas de toohello. Debería ver el trabajo de aplicación web de hello según lo esperado, con hello **MySQL** base de datos hospedada en Azure.
   
    ![Explorador web](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    ¡Enhorabuena! Se ha publicado correctamente su tooAzure de aplicación web basada en MySQL.

## <a name="next-steps"></a>Pasos siguientes
Siga estos toolearn de vínculos más información acerca de Python Tools para Visual Studio, Django y MySQL.

* [Documentación sobre Python Tools para Visual Studio]
  * [Proyectos web]
  * [Proyectos de servicio en la nube]
  * [Depuración remota en Microsoft Azure]
* [Documentación de Django]
* [MySQL]

Para obtener más información, vea hello [Centro para desarrolladores de Python](/develop/python/).

<!--Link references-->

[Centro para desarrolladores de Python]: /develop/python/
[servicios en la nube]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Portal de Azure]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 para Visual Studio ejemplos VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK y herramientas para VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentación sobre Python Tools para Visual Studio]: http://aka.ms/ptvsdocs
[Depuración remota en Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Proyectos web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Proyectos de servicio en la nube]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentación de Django]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo
