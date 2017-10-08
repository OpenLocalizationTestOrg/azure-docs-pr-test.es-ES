---
title: aaaDjango y base de datos de SQL en Azure con Python Tools 2.2 para Visual Studio
description: "Obtenga información acerca de cómo toouse Hola Python Tools para Visual Studio toocreate una aplicación web Django que almacena datos en una instancia de base de datos SQL e impleméntela tooAzure aplicación del servicio Web de aplicaciones."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a>Django y Base de datos SQL en Azure con Python Tools 2.2 para Visual Studio
En este tutorial, usaremos [Python Tools para Visual Studio] sondea de toocreate una sencilla aplicación web con una de las plantillas de ejemplo de Hola PTVS. Este tutorial también se encuentra disponible como [vídeo](https://www.youtube.com/watch?v=ZwcoGcIeHF4).

Obtendrá información sobre cómo toouse una base de datos SQL hospeda en Azure, cómo tooconfigure Hola toouse de aplicación web a una base de datos SQL y cómo toopublish Hola aplicación web demasiado[aplicaciones de Web del servicio de aplicación de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

Vea hello [Centro para desarrolladores de Python] para ver más artículos que cubren el desarrollo de aplicaciones de Web del servicio de aplicación de Azure con PTVS mediante Bottle por sí solo, matraz y Django web marcos de trabajo, con los servicios de almacenamiento de tabla de Azure, MySQL y base de datos SQL. Aunque en este artículo se centra en el servicio de aplicaciones, los pasos de hello son similares al desarrollar [servicios en la nube].

## <a name="prerequisites"></a>Requisitos previos
* Visual Studio 2015
* [Python 2.7 de 32 bits]
* [Python Tools 2.2 para Visual Studio]
* [Python Tools 2.2 para Visual Studio ejemplos VSIX]
* [Azure SDK y herramientas para VS 2015]
* Django 1.9 o posterior

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
>
>

## <a name="create-hello-project"></a>Crear proyecto de hello
En esta sección, vamos a crear un proyecto de Visual Studio con la utilización de una plantilla de ejemplo. Vamos a crear un entorno virtual e instalar los paquetes necesarios. Vamos a crear una base de datos local con sqlite. A continuación, ejecutaremos aplicación web de hello localmente.

1. En Visual Studio, seleccione **Archivo**, **Nuevo proyecto**.
2. Hola plantillas de proyecto de hello [Python Tools 2.2 para Visual Studio ejemplos VSIX] están disponibles en **Python**, **ejemplos**. Seleccione **proyecto Web de sondeos Django** y haga clic en Aceptar toocreate Hola proyecto.

     ![Cuadro de diálogo Nuevo proyecto](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. Es posible que los paquetes externos tooinstall solicitadas. Seleccione **Instalar en un entorno virtual**.

     ![Cuadro de diálogo Paquetes externos](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. Seleccione **Python 2.7** como intérprete base Hola.

     ![Cuadro de diálogo Agregar entorno virtual](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. En **el Explorador de soluciones**, haga doble clic en el nodo del proyecto de Hola y seleccione **Python**y, a continuación, seleccione **Django migrar**.  Después, seleccione **Django Create Superuser (Crear superusuario de Django)**.
6. Se abrirá una consola de administración de Django y crear una base de datos de sqlite en la carpeta del proyecto Hola. Siga los mensajes de Hola toocreate un usuario.
7. Confirme que la aplicación hello funciona presionando <kbd>F5</kbd>.
8. Haga clic en **sesión** de barra de navegación superior de Hola Hola.

     ![Explorador web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. Escriba las credenciales de hello para el usuario de Hola que creó al sincronizar base de datos de Hola.

     ![Explorador web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. Haga clic en **Create Sample Polls**(Crear sondeos de ejemplo).

      ![Explorador web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. Haga clic en un sondeo y vote.

      ![Explorador web](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a>una Base de datos SQL
Para la base de datos de hello, vamos a crear una base de datos de SQL Azure.

Siga estos pasos para crear una base de datos.

1. Inicie sesión en hello [Portal de Azure].
2. En la parte inferior de hello del panel de navegación de hello, haga clic en **nuevo**. A continuación, haga clic en **Datos y almacenamiento** > **SQL Database**.
3. Configurar Hola nueva base de datos de SQL mediante la creación de un nuevo grupo de recursos y seleccione Hola ubicación adecuada para él.
4. Una vez creada la base de datos SQL de hello, haga clic en **abierta en Visual Studio** en la hoja de la base de datos de Hola.
5. Haga clic en **Configurar el firewall**.
6. Hola **configuración de Firewall** hoja, agregar una regla de firewall con **IP inicial** y **IP final** establecer toohello de dirección IP pública de su equipo de desarrollo. Haga clic en **Guardar**.

   Esto permitirá que el servidor de base de datos de toohello de las conexiones desde el equipo de desarrollo.
7. En la hoja de la base de datos de hello, haga clic en **propiedades**, a continuación, haga clic en **mostrar cadenas de conexión de base de datos**.
8. Usar valor Hola copia botón tooput Hola de **ADO.NET** en Portapapeles Hola.

## <a name="configure-hello-project"></a>Configurar proyecto Hola
En esta sección, vamos a configurar nuestro web app toouse Hola base de datos SQL que acabamos de crear. También vamos a instalar bases de datos SQL de toouse necesarios adicionales paquetes de Python con Django. A continuación, ejecutaremos aplicación web de hello localmente.

1. En Visual Studio, abra **settings.py**, de hello *ProjectName* carpeta. Pegue temporalmente cadena de conexión de hello en el editor de Hola. cadena de conexión de Hello tiene este formato:

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

Editar definición de Hola de `DATABASES` valores de hello toouse indicados anteriormente.

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. En el Explorador de soluciones, bajo **entornos de Python**, haga doble clic en el entorno virtual de Hola y seleccione **instalar un paquete de Python**.
2. Instalar el paquete de hello `pyodbc` con **pip**.

     ![Cuadro de diálogo Instalar paquete de Python](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. Instalar el paquete de hello `django-pyodbc-azure` con **pip**.

     ![Cuadro de diálogo Instalar paquete de Python](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. En **el Explorador de soluciones**, haga doble clic en el nodo del proyecto de Hola y seleccione **Python**y, a continuación, seleccione **Django migrar**.  Después, seleccione **Django Create Superuser (Crear superusuario de Django)**.

   Esto creará tablas de Hola para base de datos SQL de hello que hemos creado en la sección anterior de Hola. Siga los mensajes de Hola toocreate un usuario, que no tiene el usuario de hello toomatch en base de datos de sqlite de hello creado en la primera sección de Hola.
5. Ejecutar la aplicación hello con `F5`. Sondeos que se crean con **crear sondeos de ejemplo** y se van a serializar datos Hola enviados votando en la base de datos SQL de Hola.

## <a name="publish-hello-web-app-tooazure-app-service"></a>Publicar hello web app tooAzure servicio de aplicaciones
Hello Azure SDK para .NET proporciona un toodeploy fácilmente su tooAzure de aplicación web de web aplicación del servicio de aplicaciones Web.

1. En **el Explorador de soluciones**, haga doble clic en el nodo del proyecto de Hola y seleccione **publicar**.

     ![Cuadro de diálogo Publicación web](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. Haga clic en **Aplicaciones web de Microsoft Azure**.
3. Haga clic en **New** toocreate una nueva aplicación web.
4. Rellene Hola después de campos y haga clic en **crear**.

   * **Nombre de aplicación web**
   * **Plan del Servicio de aplicaciones**
   * **Grupos de recursos**
   * **Región**
   * Deje **servidor de base de datos** establecido demasiado**ninguna base de datos**
5. Acepte todos los valores predeterminados y haga clic en **Publicar**.
6. El explorador web abrirá automáticamente aplicaciones web publicadas de toohello. Debería ver el trabajo de aplicación web de hello según lo esperado, con hello **SQL** base de datos hospedada en Azure.

   ¡Enhorabuena!

     ![Explorador web](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a>Pasos siguientes
Siga estos toolearn de vínculos más información acerca de Python Tools para Visual Studio, Django y base de datos SQL.

* [Documentación sobre Python Tools para Visual Studio]
  * [Proyectos web]
  * [Proyectos de servicio en la nube]
  * [Depuración remota en Microsoft Azure]
* [Documentación de Django]
* [Base de datos SQL]

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Centro para desarrolladores de Python]: /develop/python/
[servicios en la nube]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Portal de Azure]: https://portal.azure.com
[Python Tools para Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 para Visual Studio ejemplos VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK y herramientas para VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Documentación sobre Python Tools para Visual Studio]: http://aka.ms/ptvsdocs
[Depuración remota en Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Proyectos web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Proyectos de servicio en la nube]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentación de Django]: https://www.djangoproject.com/
[Base de datos SQL]: /documentation/services/sql-database/
