---
title: "aplicaciones web de tecnologías de origen aaaOpen preguntas más frecuentes de Azure | Documentos de Microsoft"
description: "Obtener toofrequently respuestas preguntas más frecuentes acerca de las tecnologías de código abierto en función de las aplicaciones Web de Hola de servicio de aplicaciones de Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a>Preguntas más frecuentes sobre tecnologías de código abierto para Web Apps en Azure

Este artículo tiene toofrequently respuestas preguntas frecuentes (P+f) sobre los problemas con las tecnologías de código abierto para hello [característica de las aplicaciones Web de servicio de aplicaciones de Azure](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a>Mi base de datos ClearDB está inactiva. ¿Cómo se resuelve este problema?

Si tiene algún problema relacionado con la base de datos, póngase en contacto con el [soporte técnico de ClearDB](https://www.cleardb.com/developers/help/support). 

Para respuestas toocommon preguntas sobre ClearDB, consulte [ClearDB preguntas más frecuentes sobre](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a>¿Por qué no aparece mi base de datos ClearDB en el portal de hello?

Si crea una base de datos ClearDB en hello [portal de Azure](http://portal.azure.com/), base de datos de hello no aparece en hello [portal de Azure clásico](http://manage.windowsazure.com/). toowork resolver este problema, puede vincular manualmente la aplicación web de toohello de base de datos.

De forma similar, si crea una base de datos ClearDB en hello [portal de Azure clásico](http://manage.windowsazure.com/), no podrá ver la base de datos en hello [portal de Azure](http://portal.azure.com/). En este caso, no existe ninguna solución alternativa. 

Para obtener más información, vea [P+F sobre bases de datos MySQL ClearDB con Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a>¿Por qué no se ha migrado mi base de datos ClearDB durante la migración de mi suscripción?

Al realizar una migración de recursos entre suscripciones, se aplican algunas limitaciones. Una base de datos MySQL ClearDB es un servicio de terceros y no se migra durante la migración de la suscripción de Azure.

Si no administra la migración de saludo de la base de datos de MySQL antes de migrar los recursos de Azure, la base de datos ClearDB MySQL podría no estar disponible. tooavoid esto, en primer lugar, migrar manualmente la base de datos ClearDB y, a continuación, migrar Hola suscripción de Azure para su aplicación web.

Para obtener más información, vea [P+F sobre bases de datos MySQL ClearDB con Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a>¿Cómo activar PHP registro de problemas PHP tootroubleshoot?

tooturn registro PHP:

1. Inicie sesión en tooyour [sitio Web de Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
2. En el menú superior de hello, seleccione **consola de depuración** > **CMD**.
3. Seleccione hello **sitio** carpeta.
4. Seleccione hello **wwwroot** carpeta.
5. Seleccione hello  **+**  icono y, a continuación, seleccione **nuevo archivo**.
6. Establecer nombre de archivo de hello demasiado**. user.ini**.
7. Seleccione a continuación el icono de lápiz Hola demasiado**. user.ini**.
8. En el archivo hello, agregue este código:`log_errors=on`
9. Seleccione **Guardar**.
10. Seleccione a continuación el icono de lápiz Hola demasiado**wp-config.php**.
11. Cambiar Hola texto toohello siguiente código:
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. Hola portal de Azure, en el menú de aplicación web de hello, reinicie la aplicación web.

Para obtener más información, vea [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/) (Habilitar los registros de errores de WordPress).

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a>¿Cómo se pueden registrar errores de aplicaciones de Python en las aplicaciones hospedadas en App Service?

errores de aplicación de Python toocapture:

1. Hola portal de Azure, en la aplicación web, seleccione **configuración**.
2. En hello **configuración** ficha, seleccione **configuración de la aplicación**.
3. En **configuración de la aplicación**, escriba Hola siguiendo el par clave/valor:
    * Clave: WSGI_LOG
    * Valor: D:\home\site\wwwroot\logs.txt (escriba el nombre de archivo que elija)

Ahora debería ver los errores en el archivo de logs.txt hello en la carpeta wwwroot de Hola.

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a>¿Cómo se cambia la versión de Hola de hello aplicación Node.js que se hospeda en el servicio de aplicaciones?

versión de hello toochange de hello aplicación Node.js, puede usar uno de hello siguientes opciones:

*   Hola portal de Azure, use **configuración de la aplicación**.
    1. Hola portal de Azure, vaya tooyour web app.
    2. En hello **configuración** hoja, seleccione **configuración de la aplicación**.
    3. En **configuración de la aplicación**, puede incluir WEBSITE_NODE_DEFAULT_VERSION como clave de Hola y Hola versión de Node.js que desee como valor de Hola.
    4. Vaya tooyour [consola Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
    5. toocheck Hola versión Node.js, escriba el siguiente comando de hello:  
   ```
   node -v
   ```
*   Modifique el archivo de hello iisnode.yml. Versión de Node.js Hola variación en el archivo de hello iisnode.yml solo establece entorno en tiempo de ejecución de Hola que iisnode utiliza. Su cmd Kudu y otros seguir usan la versión Node.js de Hola que se establece en **configuración de la aplicación** Hola portal de Azure.

    tooset hello iisnode.yml manualmente, cree un archivo de iisnode.yml en la carpeta raíz de aplicación. En el archivo de hello, incluya Hola después de línea:
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   Establecer archivo de hello iisnode.yml mediante package.json durante la implementación de control de código fuente.
    Hola proceso de implementación del control de origen de Azure implica Hola pasos:
    1. Mueve la aplicación de toohello contenido web de Azure.
    2. Crea un script de implementación predeterminado, si no hay uno (deploy.cmd, archivos de implementación.) en la carpeta raíz de hello web app.
    3. Ejecuta un script de implementación en el que crea un archivo iisnode.yml si mencionan versión Node.js de hello en el archivo de hello package.json > motor de`"engines": {"node": "5.9.1","npm": "3.7.3"}`
    4. archivo de Hello iisnode.yml tiene Hola después de la línea de código:
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a>Aparece el mensaje de Hola "Error al establecer una conexión de base de datos" en mi aplicación WordPress que se hospeda en el servicio de aplicaciones. ¿Cómo se soluciona este problema?

Si ve este error en la aplicación de Azure WordPress, tooenable php_errors.log y debug.log, pasos de hello completa se detallan en [registros de errores de WordPress habilitar](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).

Cuando se habilitan los registros de hello, reproducir el error de hello y, a continuación, comprobar Hola registros toosee si se está quedando sin conexiones:
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

Si ve este error en los archivos debug.log o php_errors.log, la aplicación supera el número Hola de conexiones. Si está hospedando en ClearDB, compruebe el número de Hola de conexiones que están disponibles en su [plan de servicio](https://www.cleardb.com/pricing.view).

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a>¿Cómo se puede depurar una aplicación Node.js hospedada en App Service?

1.  Vaya tooyour [consola Kudu](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).
2.  Carpeta de registros de aplicación de vaya tooyour (D:\home\LogFiles\Application).
3.  En el archivo de logging_errors.txt hello, busque el contenido.

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a>¿Cómo se instalan módulos nativos de Python en una aplicación web de App Service o una aplicación de API?

Algunos paquetes podrían no instalarse si se usa pip en Azure. paquete de Hello podría no estar disponible en el índice del paquete Python Hola o un compilador puede ser necesario (un compilador no está disponible en el equipo de Hola que se ejecuta la aplicación web de hello en servicio de aplicaciones). Para obtener información sobre cómo instalar módulos nativos en aplicaciones web de App Service y aplicaciones de API, vea [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/) (Instalar módulos de Python en App Service).

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a>¿Cómo implementar un tooApp de aplicación Django servicio mediante Git y Hola nueva versión de Python

Para obtener información acerca de cómo instalar Django, consulte [implementar un tooApp de aplicación Django servicio](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).

## <a name="where-are-hello-tomcat-log-files-located"></a>¿Dónde están los archivos de registro de Tomcat Hola ubicados?

En Azure Marketplace e implementaciones personalizadas:

* Ubicación de la carpeta: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs
* Archivos de interés:
    * catalina.*aaaa-mm-dd*.log
    * host-manager.*aaaa-mm-dd*.log
    * localhost.*aaaa-mm-dd*.log
    * manager.*aaaa-mm-dd*.log
    * site_access_log.*aaaa-mm-dd*.log


Para implementaciones de **configuración de la aplicación** en el portal:

* Ubicación de la carpeta: D:\home\LogFiles
* Archivos de interés:
    * catalina.*aaaa-mm-dd*.log
    * host-manager.*aaaa-mm-dd*.log
    * localhost.*aaaa-mm-dd*.log
    * manager.*aaaa-mm-dd*.log
    * site_access_log.*aaaa-mm-dd*.log

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a>¿Cómo se solucionan los errores de conexión de JDBC Driver?

Puede aparecer Hola sigue mensaje en los registros de Tomcat:

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

error de Hola tooresolve:

1. Hola sqljdbc*.jar archivo se quitará la carpeta de aplicación/lib.
2. Si usas Hola Tomcat o Azure Marketplace Tomcat servidor web personalizado, copie esta carpeta .jar archivo toohello Tomcat "lib".
3. Si va a habilitar Java de Hola portal de Azure (seleccione **Java 1.8** > **servidor de Tomcat**), archivo de copia hello sqljdbc.* jar en carpeta Hola aplicación tooyour paralelas. A continuación, agregue Hola classpath el archivo web.config de configuración toohello siguiente:

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a>¿Por qué veo errores cuando intente archivos de registro en vivo de toocopy?

Si trata de archivos de registro en vivo de toocopy para una aplicación de Java (por ejemplo, Tomcat), puede aparecer este error FTP:

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

mensaje de error de Hello puede variar en función de cliente hello FTP.

Todas las aplicaciones de Java tienen este problema de bloqueo. Kudu sólo admite la descarga de este archivo mientras se está ejecutando la aplicación hello.

Detener aplicación hello permite el acceso FTP archivos toothese.

Otra solución alternativa es toowrite un trabajo Web que se ejecuta según una programación y copia estas tooa otro directorio de archivos. Para un proyecto de ejemplo, vea hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) proyecto.

## <a name="where-do-i-find-hello-log-files-for-jetty"></a>¿Dónde se puede encontrar los archivos de registro de hello para Jetty?

Marketplace y las implementaciones personalizadas, archivo de registro de hello radica en carpeta de D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs Hola. Tenga en cuenta que la ubicación de la carpeta de hello depende de versión Hola de Jetty que usa. Por ejemplo, la ruta de acceso de hello proporcionada aquí sirve de Jetty 9.1.2. Busque jetty_*AAAA_MM_DD*.stderrout.log.

Para implementaciones de configuración de la aplicación de portal, archivo de registro de hello está en D:\home\LogFiles. Busque jetty_*AAAA_MM_DD*.stderrout.log.

## <a name="can-i-send-email-from-my-azure-web-app"></a>¿Puedo enviar correo electrónico desde la aplicación web de Azure?

App Service no tiene una característica integrada de correo electrónico. Para conocer algunas alternativas adecuadas para enviar correo electrónico desde la aplicación, vea este [debate de Stack Overflow](http://stackoverflow.com/questions/17666161/sending-email-from-azure).

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a>¿Por qué mi sitio de WordPress tooanother dirección URL de redireccionamiento?

Si recientemente ha migrado tooAzure, WordPress podría redirigir la dirección URL del dominio antiguo toohello. Esto se debe a una configuración de base de datos de MySQL Hola.

WordPress amigo + es una extensión de sitio de Azure que puede usar la dirección URL de redirección de hello tooupdate directamente en la base de datos de Hola. Para obtener más información sobre el uso de WordPress Buddy+, vea [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Herramientas de WordPress y migración de MySQL con WordPress Buddy+).

O bien, si prefiere toomanually actualización dirección URL de redirección hello mediante consultas SQL o PHPMyAdmin, consulte [WordPress: redirigir la dirección URL de toowrong](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a>¿Cómo se cambia la contraseña de inicio de sesión de WordPress?

Si ha olvidado su contraseña de inicio de sesión de WordPress, puede usar WordPress amigo + tooupdate lo. tooreset su contraseña, instalación Hola WordPress amigo + extensión de sitio de Azure y pasos de hello completa, a continuación, se describen en [WordPress herramientas y la migración de MySQL con WordPress amigo +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a>No se puede iniciar sesión en tooWordPress. ¿Cómo se resuelve este problema?

Si está bloqueado y no puede entrar en WordPress después de instalar recientemente un complemento, dicho complemento podría ser defectuoso. WordPress Buddy+ es una extensión de sitio de Azure que permite deshabilitar complementos en WordPress. Para obtener más información, vea [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Herramientas de WordPress y migración de MySQL con WordPress Buddy+).

## <a name="how-do-i-migrate-my-wordpress-database"></a>¿Cómo puedo migrar mi base de datos de WordPress?

Tiene varias opciones para migrar bases de datos de MySQL de Hola que es el sitio Web de WordPress tooyour conectado:

* Los desarrolladores: Hola de uso [símbolo del sistema o PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)
* Los usuarios que no son desarrolladores deben usar [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).

## <a name="how-do-i-help-make-wordpress-more-secure"></a>¿Cómo puedo conseguir que WordPress sea más seguro?

toolearn sobre prácticas recomendadas de seguridad para WordPress, vea [las prácticas recomendadas para la seguridad de WordPress en Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a>Estoy tratando de toouse PHPMyAdmin y aparece el mensaje de Hola "Acceso denegado". ¿Cómo se resuelve este problema?

Puede experimentar este problema si la característica de hello MySQL en la aplicación no se está ejecutando todavía en esta instancia de servicio de aplicaciones. tooresolve Hola problema, intente tooaccess su sitio Web. Esto inicia procesos Hola necesario, por ejemplo el proceso de hello en la aplicación de MySQL. tooverify que MySQL que se está ejecutando en la aplicación, en el Explorador de proceso, asegúrese de que mysqld.exe se muestra en los procesos de Hola.

Después de asegurarse de que se está ejecutando en la aplicación de MySQL, intente toouse PHPMyAdmin.

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a>Obtengo un error 403 de HTTP cuando intente tooimport o exportar mi base de datos de MySQL en la aplicación mediante PHPMyadmin. ¿Cómo se resuelve este problema?

Si usa una versión antigua de Chrome, podría tratarse de un problema conocido. problema de hello tooresolve, versión más reciente de actualización tooa de Chrome. Intentar usar un explorador diferente, como Internet Explorer o Edge, donde hello problema no ocurre.
