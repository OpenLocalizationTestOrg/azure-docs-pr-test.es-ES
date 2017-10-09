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
# <a name="upload-a-custom-java-web-app-tooazure"></a><span data-ttu-id="14731-103">Cargar una aplicación tooAzure personalizada de Java web</span><span class="sxs-lookup"><span data-stu-id="14731-103">Upload a custom Java web app tooAzure</span></span>
<span data-ttu-id="14731-104">Este tema explica cómo tooupload personalizadas de Java web app demasiado[servicio de aplicaciones de Azure] aplicaciones Web.</span><span class="sxs-lookup"><span data-stu-id="14731-104">This topic explains how tooupload a custom Java web app too[Azure App Service] Web Apps.</span></span> <span data-ttu-id="14731-105">Incluye información que se aplica también algunos ejemplos de aplicaciones específicas o aplicación web y sitio Web de Java de tooany.</span><span class="sxs-lookup"><span data-stu-id="14731-105">Included is information that applies tooany Java website or web app, and also some examples for specific applications.</span></span>

<span data-ttu-id="14731-106">Tenga en cuenta que Azure proporciona un medio para crear aplicaciones web de Java utilizando la UI de configuración del Portal de Azure de Hola y Hola Azure Marketplace, tal como se documenta en [crear una aplicación web de Java en el servicio de aplicación de Azure](web-sites-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="14731-106">Note that Azure provides a means for creating Java web apps using hello Azure Portal's configuration UI, and hello Azure Marketplace, as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md).</span></span> <span data-ttu-id="14731-107">Este tutorial es para los escenarios en los que no desee UI de configuración del Portal de Azure toouse Hola o hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="14731-107">This tutorial is for scenarios in which you do not want toouse hello Azure Portal configuration UI or hello Azure Marketplace.</span></span>  

## <a name="configuration-guidelines"></a><span data-ttu-id="14731-108">Directrices de configuración</span><span class="sxs-lookup"><span data-stu-id="14731-108">Configuration guidelines</span></span>
<span data-ttu-id="14731-109">siguiente Hola describe la configuración de hello esperado para aplicaciones de web personalizadas de Java en Azure.</span><span class="sxs-lookup"><span data-stu-id="14731-109">hello following describes hello settings expected for custom Java web apps on Azure.</span></span>

* <span data-ttu-id="14731-110">puerto HTTP de Hello usado por hello proceso de Java se asigna dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="14731-110">hello HTTP port used by hello Java process is dynamically assigned.</span></span>  <span data-ttu-id="14731-111">proceso de Hello debe usar el puerto de Hola de variable de entorno de hello `HTTP_PLATFORM_PORT`.</span><span class="sxs-lookup"><span data-stu-id="14731-111">hello process must use hello port from hello environment variable `HTTP_PLATFORM_PORT`.</span></span>
* <span data-ttu-id="14731-112">Puertos todos escuchan distinto de escucha HTTP único Hola debe deshabilitarse.</span><span class="sxs-lookup"><span data-stu-id="14731-112">All listen ports other than hello single HTTP listener should be disabled.</span></span>  <span data-ttu-id="14731-113">En Tomcat, que incluye Hola apagado, HTTPS y AJP puertos.</span><span class="sxs-lookup"><span data-stu-id="14731-113">In Tomcat, that includes hello shutdown, HTTPS, and AJP ports.</span></span>
* <span data-ttu-id="14731-114">los contenedores de Hello debe toobe configurado para el tráfico de IPv4 únicamente.</span><span class="sxs-lookup"><span data-stu-id="14731-114">hello container needs toobe configured for IPv4 traffic only.</span></span>
* <span data-ttu-id="14731-115">Hola **inicio** comando para necesidades de aplicación hello toobe establecidos en configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="14731-115">hello **startup** command for hello application needs toobe set in hello configuration.</span></span>
* <span data-ttu-id="14731-116">Las aplicaciones que requieren el permiso de escritura de directorios con necesitan toobe ubicado en el directorio de contenido de la aplicación hello web de Azure, que es **D:\home**.</span><span class="sxs-lookup"><span data-stu-id="14731-116">Applications that require directories with write permission need toobe located in hello Azure web app's content directory,  which is **D:\home**.</span></span>  <span data-ttu-id="14731-117">variable de entorno de Hello `HOME` hace referencia a tooD:\home.</span><span class="sxs-lookup"><span data-stu-id="14731-117">hello environmental variable `HOME` refers tooD:\home.</span></span>  

<span data-ttu-id="14731-118">Puede establecer variables de entorno según sea necesario en el archivo web.config de Hola.</span><span class="sxs-lookup"><span data-stu-id="14731-118">You can set environment variables as required in hello web.config file.</span></span>

## <a name="webconfig-httpplatform-configuration"></a><span data-ttu-id="14731-119">Configuración de web.config httpPlatform</span><span class="sxs-lookup"><span data-stu-id="14731-119">web.config httpPlatform configuration</span></span>
<span data-ttu-id="14731-120">Hello siguiente información describe hello **httpplatform en** formato en el archivo web.config.</span><span class="sxs-lookup"><span data-stu-id="14731-120">hello following information describes hello **httpPlatform** format within web.config.</span></span>

<span data-ttu-id="14731-121">**arguments** (valor predeterminado="").</span><span class="sxs-lookup"><span data-stu-id="14731-121">**arguments** (Default="").</span></span> <span data-ttu-id="14731-122">Argumentos toohello ejecutable o script especificado en hello **processPath** configuración.</span><span class="sxs-lookup"><span data-stu-id="14731-122">Arguments toohello executable or script specified in hello **processPath** setting.</span></span>

<span data-ttu-id="14731-123">Ejemplos (que se muestran con **processPath** incluido):</span><span class="sxs-lookup"><span data-stu-id="14731-123">Examples (shown with **processPath** included):</span></span>

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


<span data-ttu-id="14731-124">**processPath** -toohello de ruta de acceso ejecutable o script que se iniciará un proceso de escucha las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="14731-124">**processPath** - Path toohello executable or script that will launch a process listening for HTTP requests.</span></span>

<span data-ttu-id="14731-125">Ejemplos:</span><span class="sxs-lookup"><span data-stu-id="14731-125">Examples:</span></span>

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

<span data-ttu-id="14731-126">**rapidFailsPerMinute** (valor predeterminado=10). Número de veces especificado en el proceso de hello **processPath** se permite toocrash por minuto.</span><span class="sxs-lookup"><span data-stu-id="14731-126">**rapidFailsPerMinute** (Default=10.) Number of times hello process specified in **processPath** is allowed toocrash per minute.</span></span> <span data-ttu-id="14731-127">Si se supera este límite, **HttpPlatformHandler** dejará de iniciar el proceso de hello para el resto de Hola de minuto de Hola.</span><span class="sxs-lookup"><span data-stu-id="14731-127">If this limit is exceeded, **HttpPlatformHandler** will stop launching hello process for hello remainder of hello minute.</span></span>

<span data-ttu-id="14731-128">**requestTimeout** (valor predeterminado="00:02:00"). Duración para la que **HttpPlatformHandler** va a esperar una respuesta del proceso de hello escuchando en `%HTTP_PLATFORM_PORT%`.</span><span class="sxs-lookup"><span data-stu-id="14731-128">**requestTimeout** (Default="00:02:00".) Duration for which **HttpPlatformHandler** will wait for a response from hello process listening on `%HTTP_PLATFORM_PORT%`.</span></span>

<span data-ttu-id="14731-129">**startupRetryCount** (valor predeterminado=10). Número de veces que **HttpPlatformHandler** tratará de proceso de hello toolaunch especificado en **processPath**.</span><span class="sxs-lookup"><span data-stu-id="14731-129">**startupRetryCount** (Default=10.) Number of times **HttpPlatformHandler** will try toolaunch hello process specified in **processPath**.</span></span> <span data-ttu-id="14731-130">Consulte **startupTimeLimit** para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="14731-130">See **startupTimeLimit** for more details.</span></span>

<span data-ttu-id="14731-131">**startupTimeLimit** (valor predeterminado=10 segundos). Duración para la que **HttpPlatformHandler** esperará Hola ejecutable o script toostart un proceso escuchando en el puerto de Hola.</span><span class="sxs-lookup"><span data-stu-id="14731-131">**startupTimeLimit** (Default=10 seconds.) Duration for which **HttpPlatformHandler** will wait for hello executable/script toostart a process listening on hello port.</span></span>  <span data-ttu-id="14731-132">Si se supera este límite de tiempo, **HttpPlatformHandler** realizarán terminar el proceso de hello e intentarán toolaunch vuelva a **startupRetryCount** veces.</span><span class="sxs-lookup"><span data-stu-id="14731-132">If this time limit is exceeded, **HttpPlatformHandler** will kill hello process and try toolaunch it again **startupRetryCount** times.</span></span>

<span data-ttu-id="14731-133">**stdoutLogEnabled** (valor predeterminado="true"). Si es true, **stdout** y **stderr** proceso de hello especificado en hello **processPath** valor será archivo toohello redirigida especificado en  **stdoutLogFile** (consulte **stdoutLogFile** sección).</span><span class="sxs-lookup"><span data-stu-id="14731-133">**stdoutLogEnabled** (Default="true".) If true, **stdout** and **stderr** for hello process specified in hello **processPath** setting will be redirected toohello file specified in **stdoutLogFile** (see **stdoutLogFile** section).</span></span>

<span data-ttu-id="14731-134">**stdoutLogFile** (valor predeterminado="d:\home\LogFiles\httpPlatformStdout.log"). Ruta de acceso absoluta del archivo para el que **stdout** y **stderr** de proceso de hello especificado en **processPath** se registrarán.</span><span class="sxs-lookup"><span data-stu-id="14731-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Absolute file path for which **stdout** and **stderr** from hello process specified in **processPath** will be logged.</span></span>

> [!NOTE]
> <span data-ttu-id="14731-135">`%HTTP_PLATFORM_PORT%`es un marcador de posición especial que necesita ya sea como parte de toospecified **argumentos** o como parte del programa Hola a **httpplatform en** **environmentVariables** lista.</span><span class="sxs-lookup"><span data-stu-id="14731-135">`%HTTP_PLATFORM_PORT%` is a special placeholder which needs toospecified either as part of **arguments** or as part of hello **httpPlatform** **environmentVariables** list.</span></span> <span data-ttu-id="14731-136">Esto se reemplazará por un puerto generado internamente por **HttpPlatformHandler** para que el proceso de hello especificado por **processPath** puede escuchar en este puerto.</span><span class="sxs-lookup"><span data-stu-id="14731-136">This will be replaced by an internally generated port by **HttpPlatformHandler** so that hello process specified by **processPath** can listen on this port.</span></span>
> 
> 

## <a name="deployment"></a><span data-ttu-id="14731-137">Implementación</span><span class="sxs-lookup"><span data-stu-id="14731-137">Deployment</span></span>
<span data-ttu-id="14731-138">Las aplicaciones web en función de Java pueden implementarse fácilmente a través de la mayoría de hello que mismo significa que se usa con las aplicaciones web de Internet Information Services (IIS) en función de Hola.</span><span class="sxs-lookup"><span data-stu-id="14731-138">Java based web apps can be deployed easily through most of hello same means that are used with hello Internet Information Services (IIS) based web applications.</span></span>  <span data-ttu-id="14731-139">FTP, Git y Kudu se admite como mecanismos de implementación, tal y como se Hola capacidad SCM integrada para las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="14731-139">FTP, Git and Kudu are all supported as deployment mechanisms, as is hello integrated SCM capability for web apps.</span></span> <span data-ttu-id="14731-140">WebDeploy funciona como un protocolo; sin embargo, debido a que Java no está desarrollado en Visual Studio, WebDeploy no se adapta a los casos de uso de la implementación de una aplicación web de Java.</span><span class="sxs-lookup"><span data-stu-id="14731-140">WebDeploy works as a protocol, however, as Java is not developed in Visual Studio, WebDeploy does not fit with Java web app deployment use cases.</span></span>

## <a name="application-configuration-examples"></a><span data-ttu-id="14731-141">Ejemplos de configuración de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="14731-141">Application configuration Examples</span></span>
<span data-ttu-id="14731-142">Para hello después hello, un archivo web.config y aplicaciones, configuración de la aplicación se proporciona como ejemplos tooshow cómo tooenable la aplicación de Java en las aplicaciones de servicio Web de aplicación.</span><span class="sxs-lookup"><span data-stu-id="14731-142">For hello following applications, a web.config file and hello application configuration is provided as examples tooshow how tooenable your Java application on App Service Web Apps.</span></span>

### <a name="tomcat"></a><span data-ttu-id="14731-143">Tomcat</span><span class="sxs-lookup"><span data-stu-id="14731-143">Tomcat</span></span>
<span data-ttu-id="14731-144">Aunque hay dos variaciones en Tomcat que se proporcionan con la aplicación del servicio de aplicaciones Web, sigue siendo instancias específicas de tooupload bastante posible del cliente.</span><span class="sxs-lookup"><span data-stu-id="14731-144">While there are two variations on Tomcat that are supplied with App Service Web Apps, it is still quite possible tooupload customer specific instances.</span></span> <span data-ttu-id="14731-145">A continuación se muestra un ejemplo de una instalación de Tomcat con una máquina virtual Java (JVM) diferente.</span><span class="sxs-lookup"><span data-stu-id="14731-145">Below is an example of an install of Tomcat with a different Java Virtual Machine (JVM).</span></span>

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

<span data-ttu-id="14731-146">En el lado de Tomcat hello, hay algunos cambios de configuración que necesitan toobe realizado.</span><span class="sxs-lookup"><span data-stu-id="14731-146">On hello Tomcat side, there are a few configuration changes that need toobe made.</span></span> <span data-ttu-id="14731-147">Hola server.xml necesita tooset toobe editar:</span><span class="sxs-lookup"><span data-stu-id="14731-147">hello server.xml needs toobe edited tooset:</span></span>

* <span data-ttu-id="14731-148">Puerto de apagado = -1</span><span class="sxs-lookup"><span data-stu-id="14731-148">Shutdown port = -1</span></span>
* <span data-ttu-id="14731-149">Puerto del conector HTTP = {port.http}</span><span class="sxs-lookup"><span data-stu-id="14731-149">HTTP connector port = ${port.http}</span></span>
* <span data-ttu-id="14731-150">Dirección del conector HTTP = "127.0.0.1"</span><span class="sxs-lookup"><span data-stu-id="14731-150">HTTP connector address = "127.0.0.1"</span></span>
* <span data-ttu-id="14731-151">Convierta en comentarios los conectores HTTPS y AJP</span><span class="sxs-lookup"><span data-stu-id="14731-151">Comment out HTTPS and AJP connectors</span></span>
* <span data-ttu-id="14731-152">configuración de IPv4 de Hello también puede establecerse en el archivo catalina.properties de hello donde puede agregar`java.net.preferIPv4Stack=true`</span><span class="sxs-lookup"><span data-stu-id="14731-152">hello IPv4 setting can also be set in hello catalina.properties file where you can add     `java.net.preferIPv4Stack=true`</span></span>

<span data-ttu-id="14731-153">Las llamadas Direct3D no se admiten en Aplicaciones web del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="14731-153">Direct3d calls are not supported on App Service Web Apps.</span></span> <span data-ttu-id="14731-154">toodisable, agregue Hola después de opción de Java debe hacer la aplicación tales llamadas:`-Dsun.java2d.d3d=false`</span><span class="sxs-lookup"><span data-stu-id="14731-154">toodisable those, add hello following Java option should your application make such calls: `-Dsun.java2d.d3d=false`</span></span>

### <a name="jetty"></a><span data-ttu-id="14731-155">Jetty</span><span class="sxs-lookup"><span data-stu-id="14731-155">Jetty</span></span>
<span data-ttu-id="14731-156">Como es el caso de hello de Tomcat, los clientes pueden cargar sus propias instancias de Jetty.</span><span class="sxs-lookup"><span data-stu-id="14731-156">As is hello case for Tomcat, customers can upload their own instances for Jetty.</span></span> <span data-ttu-id="14731-157">En caso de hello de ejecución instalación completa de Hola de Jetty, configuración de hello tendría un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="14731-157">In hello case of running hello full install of Jetty, hello configuration would look like this:</span></span>

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

<span data-ttu-id="14731-158">configuración de Jetty Hello necesita toobe cambiado en hello start.ini tooset `java.net.preferIPv4Stack=true`.</span><span class="sxs-lookup"><span data-stu-id="14731-158">hello Jetty configuration needs toobe changed in hello start.ini tooset `java.net.preferIPv4Stack=true`.</span></span>

### <a name="springboot"></a><span data-ttu-id="14731-159">Springboot</span><span class="sxs-lookup"><span data-stu-id="14731-159">Springboot</span></span>
<span data-ttu-id="14731-160">En orden tooget una aplicación Springboot ejecutan necesita tooupload el archivo JAR o guerra y agregue Hola siguiente el archivo web.config.</span><span class="sxs-lookup"><span data-stu-id="14731-160">In order tooget a Springboot application running you need tooupload your JAR or WAR file and add hello following web.config file.</span></span> <span data-ttu-id="14731-161">archivo web.config de Hello entra en la carpeta wwwroot de Hola.</span><span class="sxs-lookup"><span data-stu-id="14731-161">hello web.config file goes into hello wwwroot folder.</span></span> <span data-ttu-id="14731-162">En el archivo web.config de hello ajustar archivo JAR de hello argumentos toopoint tooyour, Hola siguiente el archivo JAR de ejemplo Hola se encuentra en carpeta así de hello wwwroot.</span><span class="sxs-lookup"><span data-stu-id="14731-162">In hello web.config adjust hello arguments toopoint tooyour JAR file, in hello following example hello JAR file is located in hello wwwroot folder as well.</span></span>  

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


### <a name="hudson"></a><span data-ttu-id="14731-163">Hudson</span><span class="sxs-lookup"><span data-stu-id="14731-163">Hudson</span></span>
<span data-ttu-id="14731-164">Nuestras pruebas utiliza Hola war Hudson 3.1.2 y Hola instancia predeterminada de Tomcat 7.0.50 pero sin ocupar cosas de tooset de interfaz de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="14731-164">Our test used hello Hudson 3.1.2 war and hello default Tomcat 7.0.50 instance but without using hello UI tooset things up.</span></span>  <span data-ttu-id="14731-165">Dado que Hudson es una herramienta de compilación de software, es aconsejable tooinstall en dedicado instancias donde hello **AlwaysOn** indicador puede establecerse en la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="14731-165">Because Hudson is a software build tool, it is advised tooinstall it on dedicated instances where hello **AlwaysOn** flag can be set on hello web app.</span></span>

1. <span data-ttu-id="14731-166">En el directorio raíz de la aplicación web, es decir, **d:\home\site\wwwroot**, cree un directorio **webapps** (si todavía no existe) y coloque Hudson.war en **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="14731-166">In your web app’s root directory, i.e., **d:\home\site\wwwroot**, create a **webapps** directory (if not already present), and place Hudson.war in **d:\home\site\wwwroot\webapps**.</span></span>
2. <span data-ttu-id="14731-167">Descargue apache maven 3.0.5 (compatible con Hudson) y colóquelo en **d:\home\site\wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="14731-167">Download apache maven 3.0.5 (compatible with Hudson) and place it in **d:\home\site\wwwroot**.</span></span>
3. <span data-ttu-id="14731-168">Crear el archivo web.config en **d:\home\site\wwwroot** y pegar Hola siguiendo en su contenido:</span><span class="sxs-lookup"><span data-stu-id="14731-168">Create web.config in **d:\home\site\wwwroot** and paste hello following contents in it:</span></span>
   
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
   
    <span data-ttu-id="14731-169">En este momento hello web app puede ser reiniciado tootake Hola cambios.</span><span class="sxs-lookup"><span data-stu-id="14731-169">At this point hello web app can be restarted tootake hello changes.</span></span>  <span data-ttu-id="14731-170">Conectar toohttp://yourwebapp/hudson toostart Hudson.</span><span class="sxs-lookup"><span data-stu-id="14731-170">Connect toohttp://yourwebapp/hudson toostart Hudson.</span></span>
4. <span data-ttu-id="14731-171">Una vez Hudson configura a sí mismo, debería ver Hola después de pantalla:</span><span class="sxs-lookup"><span data-stu-id="14731-171">After Hudson configures itself, you should see hello following screen:</span></span>
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. <span data-ttu-id="14731-173">Hola de acceso a la página de configuración de Hudson: haga clic en **administrar Hudson**y, a continuación, haga clic en **configurar el sistema**.</span><span class="sxs-lookup"><span data-stu-id="14731-173">Access hello Hudson configuration page: Click **Manage Hudson**, and then click **Configure System**.</span></span>
6. <span data-ttu-id="14731-174">Configurar Hola JDK tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="14731-174">Configure hello JDK as shown below:</span></span>
   
    ![Configuración de Hudson](./media/web-sites-java-custom-upload/hudson2.png)
7. <span data-ttu-id="14731-176">Configure Maven como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="14731-176">Configure Maven as shown below:</span></span>
   
    ![Configuración de Maven](./media/web-sites-java-custom-upload/maven.png)
8. <span data-ttu-id="14731-178">Guardar la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="14731-178">Save hello settings.</span></span> <span data-ttu-id="14731-179">Hudson debe estar ahora configurado y listo para su uso.</span><span class="sxs-lookup"><span data-stu-id="14731-179">Hudson should now be configured and ready for use.</span></span>

<span data-ttu-id="14731-180">Para obtener información adicional sobre Hudson, consulte [http://hudson-ci.org](http://hudson-ci.org).</span><span class="sxs-lookup"><span data-stu-id="14731-180">For additional information on Hudson, see [http://hudson-ci.org](http://hudson-ci.org).</span></span>

### <a name="liferay"></a><span data-ttu-id="14731-181">Liferay</span><span class="sxs-lookup"><span data-stu-id="14731-181">Liferay</span></span>
<span data-ttu-id="14731-182">Liferay es compatible con Aplicaciones web del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="14731-182">Liferay is supported on App Service Web Apps.</span></span> <span data-ttu-id="14731-183">Puesto que Liferay puede requerir bastante memoria, aplicación web de hello debe toorun en un trabajo dedicado mediano o grande, lo que puede proporcionar suficiente memoria.</span><span class="sxs-lookup"><span data-stu-id="14731-183">Since Liferay can require significant memory, hello web app needs toorun on a medium or large dedicated worker, which can provide enough memory.</span></span> <span data-ttu-id="14731-184">Liferay también ocupa varias toostart minutos.</span><span class="sxs-lookup"><span data-stu-id="14731-184">Liferay also takes several minutes toostart up.</span></span> <span data-ttu-id="14731-185">Por esta razón, se recomienda configurar aplicación web de hello demasiado**siempre en**.</span><span class="sxs-lookup"><span data-stu-id="14731-185">For that reason, it is recommended that you set hello web app too**Always On**.</span></span>  

<span data-ttu-id="14731-186">Con Liferay 6.1.2 que Community Edition GA3 agrupadas Tomcat, hello siguientes archivos se modificaron después de descargar Liferay:</span><span class="sxs-lookup"><span data-stu-id="14731-186">Using Liferay 6.1.2 Community Edition GA3 bundled with Tomcat, hello following files were edited after downloading Liferay:</span></span>

<span data-ttu-id="14731-187">**Server.xml**</span><span class="sxs-lookup"><span data-stu-id="14731-187">**Server.xml**</span></span>

* <span data-ttu-id="14731-188">Cambiar apagado puerto demasiado-1.</span><span class="sxs-lookup"><span data-stu-id="14731-188">Change Shutdown port too-1.</span></span>
* <span data-ttu-id="14731-189">Cambiar también el conector HTTP`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span><span class="sxs-lookup"><span data-stu-id="14731-189">Change HTTP connector too       `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span></span>
* <span data-ttu-id="14731-190">Comente el conector AJP Hola.</span><span class="sxs-lookup"><span data-stu-id="14731-190">Comment out hello AJP connector.</span></span>

<span data-ttu-id="14731-191">Hola **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** carpeta, cree un archivo denominado **ext.properties portal**.</span><span class="sxs-lookup"><span data-stu-id="14731-191">In hello **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folder, create a file named **portal-ext.properties**.</span></span> <span data-ttu-id="14731-192">Este archivo debe toocontain una sola línea, como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="14731-192">This file needs toocontain one line, as shown here:</span></span>

    liferay.home=%HOME%/site/wwwroot/liferay

<span data-ttu-id="14731-193">Hello en el mismo nivel de directorio como carpeta de tomcat 7.0.40 hello, cree un archivo denominado **web.config** con hello siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="14731-193">At hello same directory level as hello tomcat-7.0.40 folder, create a file named **web.config** with hello following content:</span></span>

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

<span data-ttu-id="14731-194">En hello **httpplatform en** bloquear, hello **requestTimeout** se establece demasiado "00:10:00".</span><span class="sxs-lookup"><span data-stu-id="14731-194">Under hello **httpPlatform** block, hello **requestTimeout** is set too“00:10:00”.</span></span>  <span data-ttu-id="14731-195">Puede reducirse pero, a continuación, estás toosee es probable que algunos errores de tiempo de espera mientras se arranque Liferay.</span><span class="sxs-lookup"><span data-stu-id="14731-195">It can be reduced but then you are likely toosee some timeout errors while Liferay is bootstrapping.</span></span>  <span data-ttu-id="14731-196">Si se cambia este valor, Hola **connectionTimeout** en tomcat hello también se puede modificar server.xml.</span><span class="sxs-lookup"><span data-stu-id="14731-196">If this value is changed, then hello **connectionTimeout** in hello tomcat server.xml should also be modified.</span></span>  

<span data-ttu-id="14731-197">Cabe mencionar que varariable de entorno de hello JRE_HOME se especifica en hello anteriormente web.config toopoint toohello JDK de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="14731-197">It is worth noting that hello JRE_HOME environnment varariable is specified in hello above web.config toopoint toohello 64-bit JDK.</span></span> <span data-ttu-id="14731-198">valor predeterminado de Hello es 32 bits, pero como Liferay puede necesitar niveles altos de memoria, se recomienda toouse Hola JDK de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="14731-198">hello default is 32-bit, but since Liferay may require high levels of memory, it is recommended toouse hello 64-bit JDK.</span></span>

<span data-ttu-id="14731-199">Después de que realice estos cambios, reinicie la aplicación web que ejecuta Liferay y, a continuación, abra http://yourwebapp.</span><span class="sxs-lookup"><span data-stu-id="14731-199">Once you make these changes, restart your web app running Liferay, Then, open http://yourwebapp.</span></span> <span data-ttu-id="14731-200">Hola Liferay portal está disponible desde la raíz de aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="14731-200">hello Liferay portal is available from hello web app root.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="14731-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="14731-201">Next steps</span></span>
<span data-ttu-id="14731-202">Para obtener más información sobre Liferay, consulte [http://www.liferay.com](http://www.liferay.com).</span><span class="sxs-lookup"><span data-stu-id="14731-202">For more information about Liferay, see [http://www.liferay.com](http://www.liferay.com).</span></span>

<span data-ttu-id="14731-203">Para más información sobre Java, visite [Azure para desarrolladores de Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="14731-203">For more information about Java, visit [Azure for Java developers](/java/azure).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[servicio de aplicaciones de Azure]: http://go.microsoft.com/fwlink/?LinkId=529714
