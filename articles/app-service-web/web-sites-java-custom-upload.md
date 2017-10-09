---
title: "aaaUpload una aplicación tooAzure personalizada de Java web"
description: "Este tutorial muestra cómo tooupload personalizadas de Java web tooAzure aplicaciones Web de aplicación de servicio de aplicación."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: eb2ccd83-e5c6-444e-a0fc-08fd5cc8326c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 0cb4a682bb25d86ff08bfd03628c89795c58451e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-java-web-app-tooazure"></a>Cargar una aplicación tooAzure personalizada de Java web
Este tema explica cómo tooupload personalizadas de Java web app demasiado[servicio de aplicaciones de Azure] aplicaciones Web. Incluye información que se aplica también algunos ejemplos de aplicaciones específicas o aplicación web y sitio Web de Java de tooany.

Tenga en cuenta que Azure proporciona un medio para crear aplicaciones web de Java utilizando la UI de configuración del Portal de Azure de Hola y Hola Azure Marketplace, tal como se documenta en [crear una aplicación web de Java en el servicio de aplicación de Azure](web-sites-java-get-started.md). Este tutorial es para los escenarios en los que no desee UI de configuración del Portal de Azure toouse Hola o hello Azure Marketplace.  

## <a name="configuration-guidelines"></a>Directrices de configuración
siguiente Hola describe la configuración de hello esperado para aplicaciones de web personalizadas de Java en Azure.

* puerto HTTP de Hello usado por hello proceso de Java se asigna dinámicamente.  proceso de Hello debe usar el puerto de Hola de variable de entorno de hello `HTTP_PLATFORM_PORT`.
* Puertos todos escuchan distinto de escucha HTTP único Hola debe deshabilitarse.  En Tomcat, que incluye Hola apagado, HTTPS y AJP puertos.
* los contenedores de Hello debe toobe configurado para el tráfico de IPv4 únicamente.
* Hola **inicio** comando para necesidades de aplicación hello toobe establecidos en configuración de Hola.
* Las aplicaciones que requieren el permiso de escritura de directorios con necesitan toobe ubicado en el directorio de contenido de la aplicación hello web de Azure, que es **D:\home**.  variable de entorno de Hello `HOME` hace referencia a tooD:\home.  

Puede establecer variables de entorno según sea necesario en el archivo web.config de Hola.

## <a name="webconfig-httpplatform-configuration"></a>Configuración de web.config httpPlatform
Hello siguiente información describe hello **httpplatform en** formato en el archivo web.config.

**arguments** (valor predeterminado=""). Argumentos toohello ejecutable o script especificado en hello **processPath** configuración.

Ejemplos (que se muestran con **processPath** incluido):

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


**processPath** -toohello de ruta de acceso ejecutable o script que se iniciará un proceso de escucha las solicitudes HTTP.

Ejemplos:

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

**rapidFailsPerMinute** (valor predeterminado=10). Número de veces especificado en el proceso de hello **processPath** se permite toocrash por minuto. Si se supera este límite, **HttpPlatformHandler** dejará de iniciar el proceso de hello para el resto de Hola de minuto de Hola.

**requestTimeout** (valor predeterminado="00:02:00"). Duración para la que **HttpPlatformHandler** va a esperar una respuesta del proceso de hello escuchando en `%HTTP_PLATFORM_PORT%`.

**startupRetryCount** (valor predeterminado=10). Número de veces que **HttpPlatformHandler** tratará de proceso de hello toolaunch especificado en **processPath**. Consulte **startupTimeLimit** para obtener más detalles.

**startupTimeLimit** (valor predeterminado=10 segundos). Duración para la que **HttpPlatformHandler** esperará Hola ejecutable o script toostart un proceso escuchando en el puerto de Hola.  Si se supera este límite de tiempo, **HttpPlatformHandler** realizarán terminar el proceso de hello e intentarán toolaunch vuelva a **startupRetryCount** veces.

**stdoutLogEnabled** (valor predeterminado="true"). Si es true, **stdout** y **stderr** proceso de hello especificado en hello **processPath** valor será archivo toohello redirigida especificado en  **stdoutLogFile** (consulte **stdoutLogFile** sección).

**stdoutLogFile** (valor predeterminado="d:\home\LogFiles\httpPlatformStdout.log"). Ruta de acceso absoluta del archivo para el que **stdout** y **stderr** de proceso de hello especificado en **processPath** se registrarán.

> [!NOTE]
> `%HTTP_PLATFORM_PORT%`es un marcador de posición especial que necesita ya sea como parte de toospecified **argumentos** o como parte del programa Hola a **httpplatform en** **environmentVariables** lista. Esto se reemplazará por un puerto generado internamente por **HttpPlatformHandler** para que el proceso de hello especificado por **processPath** puede escuchar en este puerto.
> 
> 

## <a name="deployment"></a>Implementación
Las aplicaciones web en función de Java pueden implementarse fácilmente a través de la mayoría de hello que mismo significa que se usa con las aplicaciones web de Internet Information Services (IIS) en función de Hola.  FTP, Git y Kudu se admite como mecanismos de implementación, tal y como se Hola capacidad SCM integrada para las aplicaciones web. WebDeploy funciona como un protocolo; sin embargo, debido a que Java no está desarrollado en Visual Studio, WebDeploy no se adapta a los casos de uso de la implementación de una aplicación web de Java.

## <a name="application-configuration-examples"></a>Ejemplos de configuración de aplicaciones
Para hello después hello, un archivo web.config y aplicaciones, configuración de la aplicación se proporciona como ejemplos tooshow cómo tooenable la aplicación de Java en las aplicaciones de servicio Web de aplicación.

### <a name="tomcat"></a>Tomcat
Aunque hay dos variaciones en Tomcat que se proporcionan con la aplicación del servicio de aplicaciones Web, sigue siendo instancias específicas de tooupload bastante posible del cliente. A continuación se muestra un ejemplo de una instalación de Tomcat con una máquina virtual Java (JVM) diferente.

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat" 
            arguments="">
          <environmentVariables>
            <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
            <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\bin\tomcat" />
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default too%programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

En el lado de Tomcat hello, hay algunos cambios de configuración que necesitan toobe realizado. Hola server.xml necesita tooset toobe editar:

* Puerto de apagado = -1
* Puerto del conector HTTP = {port.http}
* Dirección del conector HTTP = "127.0.0.1"
* Convierta en comentarios los conectores HTTPS y AJP
* configuración de IPv4 de Hello también puede establecerse en el archivo catalina.properties de hello donde puede agregar`java.net.preferIPv4Stack=true`

Las llamadas Direct3D no se admiten en Aplicaciones web del Servicio de aplicaciones. toodisable, agregue Hola después de opción de Java debe hacer la aplicación tales llamadas:`-Dsun.java2d.d3d=false`

### <a name="jetty"></a>Jetty
Como es el caso de hello de Tomcat, los clientes pueden cargar sus propias instancias de Jetty. En caso de hello de ejecución instalación completa de Hola de Jetty, configuración de hello tendría un aspecto similar al siguiente:

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httppPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe" 
             arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP_PLATFORM_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"
            startupTimeLimit="20"
          startupRetryCount="10"
          stdoutLogEnabled="true">
        </httpPlatform>
      </system.webServer>
    </configuration>

configuración de Jetty Hello necesita toobe cambiado en hello start.ini tooset `java.net.preferIPv4Stack=true`.

### <a name="springboot"></a>Springboot
En orden tooget una aplicación Springboot ejecutan necesita tooupload el archivo JAR o guerra y agregue Hola siguiente el archivo web.config. archivo web.config de Hello entra en la carpeta wwwroot de Hola. En el archivo web.config de hello ajustar archivo JAR de hello argumentos toopoint tooyour, Hola siguiente el archivo JAR de ejemplo Hola se encuentra en carpeta así de hello wwwroot.  

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
            arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\my-web-project.jar&quot;">
        </httpPlatform>
      </system.webServer>
    </configuration>


### <a name="hudson"></a>Hudson
Nuestras pruebas utiliza Hola war Hudson 3.1.2 y Hola instancia predeterminada de Tomcat 7.0.50 pero sin ocupar cosas de tooset de interfaz de usuario de Hola.  Dado que Hudson es una herramienta de compilación de software, es aconsejable tooinstall en dedicado instancias donde hello **AlwaysOn** indicador puede establecerse en la aplicación web de Hola.

1. En el directorio raíz de la aplicación web, es decir, **d:\home\site\wwwroot**, cree un directorio **webapps** (si todavía no existe) y coloque Hudson.war en **d:\home\site\wwwroot\webapps**.
2. Descargue apache maven 3.0.5 (compatible con Hudson) y colóquelo en **d:\home\site\wwwroot**.
3. Crear el archivo web.config en **d:\home\site\wwwroot** y pegar Hola siguiendo en su contenido:
   
        <?xml version="1.0" encoding="UTF-8"?>
        <configuration>
          <system.webServer>
            <handlers>
              <add name="httppPlatformHandler" path="*" verb="*" 
        modules="httpPlatformHandler" resourceType="Unspecified" />
            </handlers>
            <httpPlatform processPath="%AZURE_TOMCAT7_HOME%\bin\startup.bat"
        startupTimeLimit="20"
        startupRetryCount="10">
        <environmentVariables>
          <environmentVariable name="HUDSON_HOME" 
        value="%HOME%\site\wwwroot\hudson_home" />
          <environmentVariable name="JAVA_OPTS" 
        value="-Djava.net.preferIPv4Stack=true -Duser.home=%HOME%/site/wwwroot/user_home -Dhudson.DNSMultiCast.disabled=true" />
        </environmentVariables>            
            </httpPlatform>
          </system.webServer>
        </configuration>
   
    En este momento hello web app puede ser reiniciado tootake Hola cambios.  Conectar toohttp://yourwebapp/hudson toostart Hudson.
4. Una vez Hudson configura a sí mismo, debería ver Hola después de pantalla:
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. Hola de acceso a la página de configuración de Hudson: haga clic en **administrar Hudson**y, a continuación, haga clic en **configurar el sistema**.
6. Configurar Hola JDK tal y como se muestra a continuación:
   
    ![Configuración de Hudson](./media/web-sites-java-custom-upload/hudson2.png)
7. Configure Maven como se muestra a continuación:
   
    ![Configuración de Maven](./media/web-sites-java-custom-upload/maven.png)
8. Guardar la configuración de Hola. Hudson debe estar ahora configurado y listo para su uso.

Para obtener información adicional sobre Hudson, consulte [http://hudson-ci.org](http://hudson-ci.org).

### <a name="liferay"></a>Liferay
Liferay es compatible con Aplicaciones web del Servicio de aplicaciones. Puesto que Liferay puede requerir bastante memoria, aplicación web de hello debe toorun en un trabajo dedicado mediano o grande, lo que puede proporcionar suficiente memoria. Liferay también ocupa varias toostart minutos. Por esta razón, se recomienda configurar aplicación web de hello demasiado**siempre en**.  

Con Liferay 6.1.2 que Community Edition GA3 agrupadas Tomcat, hello siguientes archivos se modificaron después de descargar Liferay:

**Server.xml**

* Cambiar apagado puerto demasiado-1.
* Cambiar también el conector HTTP`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`
* Comente el conector AJP Hola.

Hola **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** carpeta, cree un archivo denominado **ext.properties portal**. Este archivo debe toocontain una sola línea, como se muestra aquí:

    liferay.home=%HOME%/site/wwwroot/liferay

Hello en el mismo nivel de directorio como carpeta de tomcat 7.0.40 hello, cree un archivo denominado **web.config** con hello siguen contenido:

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
    <add name="httpPlatformHandler" path="*" verb="*"
         modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\tomcat-7.0.40\bin\catalina.bat" 
                      arguments="run" 
                      startupTimeLimit="10" 
                      requestTimeout="00:10:00" 
                      stdoutLogEnabled="true">
          <environmentVariables>
      <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
      <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\tomcat-7.0.40" />
            <environmentVariable name="JRE_HOME" value="D:\Program Files\Java\jdk1.7.0_51" /> 
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

En hello **httpplatform en** bloquear, hello **requestTimeout** se establece demasiado "00:10:00".  Puede reducirse pero, a continuación, estás toosee es probable que algunos errores de tiempo de espera mientras se arranque Liferay.  Si se cambia este valor, Hola **connectionTimeout** en tomcat hello también se puede modificar server.xml.  

Cabe mencionar que varariable de entorno de hello JRE_HOME se especifica en hello anteriormente web.config toopoint toohello JDK de 64 bits. valor predeterminado de Hello es 32 bits, pero como Liferay puede necesitar niveles altos de memoria, se recomienda toouse Hola JDK de 64 bits.

Después de que realice estos cambios, reinicie la aplicación web que ejecuta Liferay y, a continuación, abra http://yourwebapp. Hola Liferay portal está disponible desde la raíz de aplicación web de Hola. 

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre Liferay, consulte [http://www.liferay.com](http://www.liferay.com).

Para más información sobre Java, visite [Azure para desarrolladores de Java](/java/azure).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[servicio de aplicaciones de Azure]: http://go.microsoft.com/fwlink/?LinkId=529714
