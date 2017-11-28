---
title: "Carga de una aplicación web de Java personalizada en Azure"
description: "En este tutorial se muestra cómo cargar una aplicación web de Java personalizada en Aplicaciones web del Servicio de aplicaciones de Azure."
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
ms.openlocfilehash: 9c8f9ee7780859f7640ac82d6ebce85082170ad7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="upload-a-custom-java-web-app-to-azure"></a><span data-ttu-id="7e0af-103">Carga de una aplicación web de Java personalizada en Azure</span><span class="sxs-lookup"><span data-stu-id="7e0af-103">Upload a custom Java web app to Azure</span></span>
<span data-ttu-id="7e0af-104">En este tema se explica cómo cargar una aplicación web de Java personalizada en Aplicaciones web del [Servicio de aplicaciones de Azure] .</span><span class="sxs-lookup"><span data-stu-id="7e0af-104">This topic explains how to upload a custom Java web app to [Azure App Service] Web Apps.</span></span> <span data-ttu-id="7e0af-105">Se incluye información que se aplica a cualquier aplicación web o sitio web de Java, así como algunos ejemplos de aplicaciones específicas.</span><span class="sxs-lookup"><span data-stu-id="7e0af-105">Included is information that applies to any Java website or web app, and also some examples for specific applications.</span></span>

<span data-ttu-id="7e0af-106">Tenga en cuenta que Azure permite crear aplicaciones web de Java con la interfaz de usuario de configuración del Portal de Azure y Azure Marketplace, tal y como se documenta en [Creación de una aplicación web de Java en Servicio de aplicaciones de Azure](web-sites-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7e0af-106">Note that Azure provides a means for creating Java web apps using the Azure Portal's configuration UI, and the Azure Marketplace, as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md).</span></span> <span data-ttu-id="7e0af-107">Este tutorial se destina a escenarios en los que no desea usar la interfaz de usuario de configuración del Portal de Azure ni Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="7e0af-107">This tutorial is for scenarios in which you do not want to use the Azure Portal configuration UI or the Azure Marketplace.</span></span>  

## <a name="configuration-guidelines"></a><span data-ttu-id="7e0af-108">Directrices de configuración</span><span class="sxs-lookup"><span data-stu-id="7e0af-108">Configuration guidelines</span></span>
<span data-ttu-id="7e0af-109">A continuación se describe la configuración esperada para las aplicaciones web de Java personalizadas en Azure.</span><span class="sxs-lookup"><span data-stu-id="7e0af-109">The following describes the settings expected for custom Java web apps on Azure.</span></span>

* <span data-ttu-id="7e0af-110">El puerto HTTP que utiliza el proceso de Java se asigna de manera dinámica.</span><span class="sxs-lookup"><span data-stu-id="7e0af-110">The HTTP port used by the Java process is dynamically assigned.</span></span>  <span data-ttu-id="7e0af-111">El proceso debe utilizar el puerto de la variable de entorno `HTTP_PLATFORM_PORT`.</span><span class="sxs-lookup"><span data-stu-id="7e0af-111">The process must use the port from the environment variable `HTTP_PLATFORM_PORT`.</span></span>
* <span data-ttu-id="7e0af-112">Se deben deshabilitar todos los puertos de escucha aparte del agente de escucha simple HTTP.</span><span class="sxs-lookup"><span data-stu-id="7e0af-112">All listen ports other than the single HTTP listener should be disabled.</span></span>  <span data-ttu-id="7e0af-113">En Tomcat, ello incluye los puertos de apagado, HTTPS y AJP.</span><span class="sxs-lookup"><span data-stu-id="7e0af-113">In Tomcat, that includes the shutdown, HTTPS, and AJP ports.</span></span>
* <span data-ttu-id="7e0af-114">El contenedor debe estar configurado solo para el tráfico IPv4.</span><span class="sxs-lookup"><span data-stu-id="7e0af-114">The container needs to be configured for IPv4 traffic only.</span></span>
* <span data-ttu-id="7e0af-115">En la configuración se debe establecer el comando **startup** para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7e0af-115">The **startup** command for the application needs to be set in the configuration.</span></span>
* <span data-ttu-id="7e0af-116">Las aplicaciones que requieren directorios con permiso de escritura tienen que estar ubicadas en el directorio de contenido de la aplicación web de Azure, que es **D:\home**.</span><span class="sxs-lookup"><span data-stu-id="7e0af-116">Applications that require directories with write permission need to be located in the Azure web app's content directory,  which is **D:\home**.</span></span>  <span data-ttu-id="7e0af-117">La variable de entorno `HOME` hace referencia a D:\home.</span><span class="sxs-lookup"><span data-stu-id="7e0af-117">The environmental variable `HOME` refers to D:\home.</span></span>  

<span data-ttu-id="7e0af-118">Puede establecer las variables de entorno como se requiere en el archivo web.config.</span><span class="sxs-lookup"><span data-stu-id="7e0af-118">You can set environment variables as required in the web.config file.</span></span>

## <a name="webconfig-httpplatform-configuration"></a><span data-ttu-id="7e0af-119">Configuración de web.config httpPlatform</span><span class="sxs-lookup"><span data-stu-id="7e0af-119">web.config httpPlatform configuration</span></span>
<span data-ttu-id="7e0af-120">La siguiente información describe el formato **httpPlatform** dentro de web.config.</span><span class="sxs-lookup"><span data-stu-id="7e0af-120">The following information describes the **httpPlatform** format within web.config.</span></span>

<span data-ttu-id="7e0af-121">**arguments** (valor predeterminado="").</span><span class="sxs-lookup"><span data-stu-id="7e0af-121">**arguments** (Default="").</span></span> <span data-ttu-id="7e0af-122">Argumentos para el ejecutable o script especificado en la configuración de **processPath** .</span><span class="sxs-lookup"><span data-stu-id="7e0af-122">Arguments to the executable or script specified in the **processPath** setting.</span></span>

<span data-ttu-id="7e0af-123">Ejemplos (que se muestran con **processPath** incluido):</span><span class="sxs-lookup"><span data-stu-id="7e0af-123">Examples (shown with **processPath** included):</span></span>

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


<span data-ttu-id="7e0af-124">**processPath** : ruta de acceso al ejecutable o script que iniciará un proceso de escucha de las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="7e0af-124">**processPath** - Path to the executable or script that will launch a process listening for HTTP requests.</span></span>

<span data-ttu-id="7e0af-125">Ejemplos:</span><span class="sxs-lookup"><span data-stu-id="7e0af-125">Examples:</span></span>

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

<span data-ttu-id="7e0af-126">**rapidFailsPerMinute** (valor predeterminado=10). Número de veces que se permite que el proceso especificado en **processPath** se bloquee por minuto.</span><span class="sxs-lookup"><span data-stu-id="7e0af-126">**rapidFailsPerMinute** (Default=10.) Number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="7e0af-127">Si se supera este límite, **HttpPlatformHandler** detendrá el inicio del proceso durante el resto del minuto.</span><span class="sxs-lookup"><span data-stu-id="7e0af-127">If this limit is exceeded, **HttpPlatformHandler** will stop launching the process for the remainder of the minute.</span></span>

<span data-ttu-id="7e0af-128">**requestTimeout** (valor predeterminado="00:02:00"). Tiempo durante el cual **HttpPlatformHandler** esperará una respuesta del proceso de escucha en `%HTTP_PLATFORM_PORT%`.</span><span class="sxs-lookup"><span data-stu-id="7e0af-128">**requestTimeout** (Default="00:02:00".) Duration for which **HttpPlatformHandler** will wait for a response from the process listening on `%HTTP_PLATFORM_PORT%`.</span></span>

<span data-ttu-id="7e0af-129">**startupRetryCount** (valor predeterminado=10). Número de veces que **HttpPlatformHandler** intentará iniciar el proceso especificado en **processPath**.</span><span class="sxs-lookup"><span data-stu-id="7e0af-129">**startupRetryCount** (Default=10.) Number of times **HttpPlatformHandler** will try to launch the process specified in **processPath**.</span></span> <span data-ttu-id="7e0af-130">Consulte **startupTimeLimit** para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="7e0af-130">See **startupTimeLimit** for more details.</span></span>

<span data-ttu-id="7e0af-131">**startupTimeLimit** (valor predeterminado=10 segundos). Tiempo durante el cual **HttpPlatformHandler** esperará a que el ejecutable/script inicie un proceso que escucha en el puerto.</span><span class="sxs-lookup"><span data-stu-id="7e0af-131">**startupTimeLimit** (Default=10 seconds.) Duration for which **HttpPlatformHandler** will wait for the executable/script to start a process listening on the port.</span></span>  <span data-ttu-id="7e0af-132">Si se supera este límite de tiempo, **HttpPlatformHandler** cerrará el proceso e intentará volver a iniciarlo **startupRetryCount** veces.</span><span class="sxs-lookup"><span data-stu-id="7e0af-132">If this time limit is exceeded, **HttpPlatformHandler** will kill the process and try to launch it again **startupRetryCount** times.</span></span>

<span data-ttu-id="7e0af-133">**stdoutLogEnabled** (valor predeterminado="true"). Si el valor es true, **stdout** y **stderr** para el proceso especificado en la configuración **processPath** serán redirigidos al archivo especificado en **stdoutLogFile** (consulte la sección **stdoutLogFile**).</span><span class="sxs-lookup"><span data-stu-id="7e0af-133">**stdoutLogEnabled** (Default="true".) If true, **stdout** and **stderr** for the process specified in the **processPath** setting will be redirected to the file specified in **stdoutLogFile** (see **stdoutLogFile** section).</span></span>

<span data-ttu-id="7e0af-134">**stdoutLogFile** (valor predeterminado="d:\home\LogFiles\httpPlatformStdout.log"). Ruta de acceso absoluta del archivo por el cual se registrarán **stdout** y **stderr** desde el proceso especificado en **processPath**.</span><span class="sxs-lookup"><span data-stu-id="7e0af-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Absolute file path for which **stdout** and **stderr** from the process specified in **processPath** will be logged.</span></span>

> [!NOTE]
> <span data-ttu-id="7e0af-135">`%HTTP_PLATFORM_PORT%` es un marcador de posición especial que se debe especificar como parte de los **argumentos** o como parte de la lista **environmentVariables** de **httpPlatform**.</span><span class="sxs-lookup"><span data-stu-id="7e0af-135">`%HTTP_PLATFORM_PORT%` is a special placeholder which needs to specified either as part of **arguments** or as part of the **httpPlatform** **environmentVariables** list.</span></span> <span data-ttu-id="7e0af-136">Esto se reemplazará por un puerto generado internamente mediante **HttpPlatformHandler** de modo que el proceso que se especifica en **processPath** pueda escuchar en este puerto.</span><span class="sxs-lookup"><span data-stu-id="7e0af-136">This will be replaced by an internally generated port by **HttpPlatformHandler** so that the process specified by **processPath** can listen on this port.</span></span>
> 
> 

## <a name="deployment"></a><span data-ttu-id="7e0af-137">Implementación</span><span class="sxs-lookup"><span data-stu-id="7e0af-137">Deployment</span></span>
<span data-ttu-id="7e0af-138">Las aplicaciones web basadas ​​en Java se pueden implementar fácilmente a través de la mayoría de los mismos medios que se utilizan con las aplicaciones web basadas en Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="7e0af-138">Java based web apps can be deployed easily through most of the same means that are used with the Internet Information Services (IIS) based web applications.</span></span>  <span data-ttu-id="7e0af-139">FTP, Git y Kudu son todas compatibles como mecanismos de implementación, así como la funcionalidad de SCM integrada para las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="7e0af-139">FTP, Git and Kudu are all supported as deployment mechanisms, as is the integrated SCM capability for web apps.</span></span> <span data-ttu-id="7e0af-140">WebDeploy funciona como un protocolo; sin embargo, debido a que Java no está desarrollado en Visual Studio, WebDeploy no se adapta a los casos de uso de la implementación de una aplicación web de Java.</span><span class="sxs-lookup"><span data-stu-id="7e0af-140">WebDeploy works as a protocol, however, as Java is not developed in Visual Studio, WebDeploy does not fit with Java web app deployment use cases.</span></span>

## <a name="application-configuration-examples"></a><span data-ttu-id="7e0af-141">Ejemplos de configuración de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7e0af-141">Application configuration Examples</span></span>
<span data-ttu-id="7e0af-142">Para las siguientes aplicaciones, se proporciona un archivo web.config y la configuración de la aplicación como ejemplos para mostrar cómo habilitar la aplicación Java en Aplicaciones web del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7e0af-142">For the following applications, a web.config file and the application configuration is provided as examples to show how to enable your Java application on App Service Web Apps.</span></span>

### <a name="tomcat"></a><span data-ttu-id="7e0af-143">Tomcat</span><span class="sxs-lookup"><span data-stu-id="7e0af-143">Tomcat</span></span>
<span data-ttu-id="7e0af-144">Si bien hay dos variaciones en Tomcat que se suministran con Aplicaciones web del Servicio de aplicaciones, todavía es posible cargar las instancias específicas de los clientes.</span><span class="sxs-lookup"><span data-stu-id="7e0af-144">While there are two variations on Tomcat that are supplied with App Service Web Apps, it is still quite possible to upload customer specific instances.</span></span> <span data-ttu-id="7e0af-145">A continuación se muestra un ejemplo de una instalación de Tomcat con una máquina virtual Java (JVM) diferente.</span><span class="sxs-lookup"><span data-stu-id="7e0af-145">Below is an example of an install of Tomcat with a different Java Virtual Machine (JVM).</span></span>

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
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default to %programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="7e0af-146">Por el lado de Tomcat, es necesario realizar algunos cambios en la configuración.</span><span class="sxs-lookup"><span data-stu-id="7e0af-146">On the Tomcat side, there are a few configuration changes that need to be made.</span></span> <span data-ttu-id="7e0af-147">Se debe editar server.xml para establecer:</span><span class="sxs-lookup"><span data-stu-id="7e0af-147">The server.xml needs to be edited to set:</span></span>

* <span data-ttu-id="7e0af-148">Puerto de apagado = -1</span><span class="sxs-lookup"><span data-stu-id="7e0af-148">Shutdown port = -1</span></span>
* <span data-ttu-id="7e0af-149">Puerto del conector HTTP = {port.http}</span><span class="sxs-lookup"><span data-stu-id="7e0af-149">HTTP connector port = ${port.http}</span></span>
* <span data-ttu-id="7e0af-150">Dirección del conector HTTP = "127.0.0.1"</span><span class="sxs-lookup"><span data-stu-id="7e0af-150">HTTP connector address = "127.0.0.1"</span></span>
* <span data-ttu-id="7e0af-151">Convierta en comentarios los conectores HTTPS y AJP</span><span class="sxs-lookup"><span data-stu-id="7e0af-151">Comment out HTTPS and AJP connectors</span></span>
* <span data-ttu-id="7e0af-152">La configuración de IPv4 también se puede configurar en el archivo catalina.properties donde se puede agregar `java.net.preferIPv4Stack=true`</span><span class="sxs-lookup"><span data-stu-id="7e0af-152">The IPv4 setting can also be set in the catalina.properties file where you can add     `java.net.preferIPv4Stack=true`</span></span>

<span data-ttu-id="7e0af-153">Las llamadas Direct3D no se admiten en Aplicaciones web del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7e0af-153">Direct3d calls are not supported on App Service Web Apps.</span></span> <span data-ttu-id="7e0af-154">Para deshabilitarlas, agregue la siguiente opción de Java si la aplicación realiza llamadas de ese tipo: `-Dsun.java2d.d3d=false`</span><span class="sxs-lookup"><span data-stu-id="7e0af-154">To disable those, add the following Java option should your application make such calls: `-Dsun.java2d.d3d=false`</span></span>

### <a name="jetty"></a><span data-ttu-id="7e0af-155">Jetty</span><span class="sxs-lookup"><span data-stu-id="7e0af-155">Jetty</span></span>
<span data-ttu-id="7e0af-156">Como es el caso de Tomcat, los clientes pueden cargar sus propias instancias de Jetty.</span><span class="sxs-lookup"><span data-stu-id="7e0af-156">As is the case for Tomcat, customers can upload their own instances for Jetty.</span></span> <span data-ttu-id="7e0af-157">En el caso de ejecutar la instalación completa de Jetty, la configuración sería similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="7e0af-157">In the case of running the full install of Jetty, the configuration would look like this:</span></span>

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

<span data-ttu-id="7e0af-158">La configuración de Jetty necesita cambiarse en el archivo start.ini para establecer `java.net.preferIPv4Stack=true`.</span><span class="sxs-lookup"><span data-stu-id="7e0af-158">The Jetty configuration needs to be changed in the start.ini to set `java.net.preferIPv4Stack=true`.</span></span>

### <a name="springboot"></a><span data-ttu-id="7e0af-159">Springboot</span><span class="sxs-lookup"><span data-stu-id="7e0af-159">Springboot</span></span>
<span data-ttu-id="7e0af-160">Para obtener una aplicación Springboot en ejecución necesita cargar el archivo JAR o WAR y agregar el siguiente archivo web.config.</span><span class="sxs-lookup"><span data-stu-id="7e0af-160">In order to get a Springboot application running you need to upload your JAR or WAR file and add the following web.config file.</span></span> <span data-ttu-id="7e0af-161">El archivo web.config se coloca en la carpeta wwwroot.</span><span class="sxs-lookup"><span data-stu-id="7e0af-161">The web.config file goes into the wwwroot folder.</span></span> <span data-ttu-id="7e0af-162">En el archivo web.config, ajuste los argumentos para apuntar al archivo JAR. En el ejemplo siguiente el archivo JAR también se encuentra en la carpeta wwwroot.</span><span class="sxs-lookup"><span data-stu-id="7e0af-162">In the web.config adjust the arguments to point to your JAR file, in the following example the JAR file is located in the wwwroot folder as well.</span></span>  

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


### <a name="hudson"></a><span data-ttu-id="7e0af-163">Hudson</span><span class="sxs-lookup"><span data-stu-id="7e0af-163">Hudson</span></span>
<span data-ttu-id="7e0af-164">Nuestra prueba utilizó war de Hudson 3.1.2 y la instancia predeterminada de Tomcat 7.0.50, pero sin utilizar la interfaz de usuario para realizar la configuración.</span><span class="sxs-lookup"><span data-stu-id="7e0af-164">Our test used the Hudson 3.1.2 war and the default Tomcat 7.0.50 instance but without using the UI to set things up.</span></span>  <span data-ttu-id="7e0af-165">Debido a que Hudson es una herramienta de compilación de software, se recomienda instalarla en instancias dedicadas donde la marca **AlwaysOn** se pueda configurar en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="7e0af-165">Because Hudson is a software build tool, it is advised to install it on dedicated instances where the **AlwaysOn** flag can be set on the web app.</span></span>

1. <span data-ttu-id="7e0af-166">En el directorio raíz de la aplicación web, es decir, **d:\home\site\wwwroot**, cree un directorio **webapps** (si todavía no existe) y coloque Hudson.war en **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="7e0af-166">In your web app’s root directory, i.e., **d:\home\site\wwwroot**, create a **webapps** directory (if not already present), and place Hudson.war in **d:\home\site\wwwroot\webapps**.</span></span>
2. <span data-ttu-id="7e0af-167">Descargue apache maven 3.0.5 (compatible con Hudson) y colóquelo en **d:\home\site\wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="7e0af-167">Download apache maven 3.0.5 (compatible with Hudson) and place it in **d:\home\site\wwwroot**.</span></span>
3. <span data-ttu-id="7e0af-168">Cree web.config en **d:\home\site\wwwroot** y pegue el siguiente contenido en él:</span><span class="sxs-lookup"><span data-stu-id="7e0af-168">Create web.config in **d:\home\site\wwwroot** and paste the following contents in it:</span></span>
   
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
   
    <span data-ttu-id="7e0af-169">En este punto, se puede reiniciar la aplicación web para que los cambios surtan efecto.</span><span class="sxs-lookup"><span data-stu-id="7e0af-169">At this point the web app can be restarted to take the changes.</span></span>  <span data-ttu-id="7e0af-170">Conéctese con http://yourwebapp/hudson para iniciar Hudson.</span><span class="sxs-lookup"><span data-stu-id="7e0af-170">Connect to http://yourwebapp/hudson to start Hudson.</span></span>
4. <span data-ttu-id="7e0af-171">Cuando Hudson se haya configurado, debería ver la siguiente pantalla:</span><span class="sxs-lookup"><span data-stu-id="7e0af-171">After Hudson configures itself, you should see the following screen:</span></span>
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. <span data-ttu-id="7e0af-173">Obtenga acceso a la página de configuración de Hudson: haga clic en **Manage Hudson** (Administrar Hudson) y, continuación, en **Configure System** (Configurar sistema).</span><span class="sxs-lookup"><span data-stu-id="7e0af-173">Access the Hudson configuration page: Click **Manage Hudson**, and then click **Configure System**.</span></span>
6. <span data-ttu-id="7e0af-174">Configure el JDK como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="7e0af-174">Configure the JDK as shown below:</span></span>
   
    ![Configuración de Hudson](./media/web-sites-java-custom-upload/hudson2.png)
7. <span data-ttu-id="7e0af-176">Configure Maven como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="7e0af-176">Configure Maven as shown below:</span></span>
   
    ![Configuración de Maven](./media/web-sites-java-custom-upload/maven.png)
8. <span data-ttu-id="7e0af-178">Guarde la configuración</span><span class="sxs-lookup"><span data-stu-id="7e0af-178">Save the settings.</span></span> <span data-ttu-id="7e0af-179">Hudson debe estar ahora configurado y listo para su uso.</span><span class="sxs-lookup"><span data-stu-id="7e0af-179">Hudson should now be configured and ready for use.</span></span>

<span data-ttu-id="7e0af-180">Para obtener información adicional sobre Hudson, consulte [http://hudson-ci.org](http://hudson-ci.org).</span><span class="sxs-lookup"><span data-stu-id="7e0af-180">For additional information on Hudson, see [http://hudson-ci.org](http://hudson-ci.org).</span></span>

### <a name="liferay"></a><span data-ttu-id="7e0af-181">Liferay</span><span class="sxs-lookup"><span data-stu-id="7e0af-181">Liferay</span></span>
<span data-ttu-id="7e0af-182">Liferay es compatible con Aplicaciones web del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7e0af-182">Liferay is supported on App Service Web Apps.</span></span> <span data-ttu-id="7e0af-183">Debido a que Liferay puede requerir una importante cantidad de memoria, la aplicación web necesita ejecutarse en un trabajo dedicado mediano o grande, que puede proporcionar suficiente memoria.</span><span class="sxs-lookup"><span data-stu-id="7e0af-183">Since Liferay can require significant memory, the web app needs to run on a medium or large dedicated worker, which can provide enough memory.</span></span> <span data-ttu-id="7e0af-184">Liferay también tarda varios minutos en iniciarse.</span><span class="sxs-lookup"><span data-stu-id="7e0af-184">Liferay also takes several minutes to start up.</span></span> <span data-ttu-id="7e0af-185">Por esa razón, se recomienda que configure el sitio en **Always On**.</span><span class="sxs-lookup"><span data-stu-id="7e0af-185">For that reason, it is recommended that you set the web app to **Always On**.</span></span>  

<span data-ttu-id="7e0af-186">Con Liferay 6.1.2 Community Edition GA3 incluido con Tomcat, se editaron los siguientes archivos después de descargar Liferay:</span><span class="sxs-lookup"><span data-stu-id="7e0af-186">Using Liferay 6.1.2 Community Edition GA3 bundled with Tomcat, the following files were edited after downloading Liferay:</span></span>

<span data-ttu-id="7e0af-187">**Server.xml**</span><span class="sxs-lookup"><span data-stu-id="7e0af-187">**Server.xml**</span></span>

* <span data-ttu-id="7e0af-188">Cambie el puerto de apagado a -1.</span><span class="sxs-lookup"><span data-stu-id="7e0af-188">Change Shutdown port to -1.</span></span>
* <span data-ttu-id="7e0af-189">Cambie el conector HTTP a `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span><span class="sxs-lookup"><span data-stu-id="7e0af-189">Change HTTP connector to       `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span></span>
* <span data-ttu-id="7e0af-190">Comente el conector AJP.</span><span class="sxs-lookup"><span data-stu-id="7e0af-190">Comment out the AJP connector.</span></span>

<span data-ttu-id="7e0af-191">En la carpeta **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes**, cree un archivo llamado **portal-ext.properties**.</span><span class="sxs-lookup"><span data-stu-id="7e0af-191">In the **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folder, create a file named **portal-ext.properties**.</span></span> <span data-ttu-id="7e0af-192">Este archivo debe contener una línea, como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="7e0af-192">This file needs to contain one line, as shown here:</span></span>

    liferay.home=%HOME%/site/wwwroot/liferay

<span data-ttu-id="7e0af-193">En el mismo nivel de directorio que la carpeta tomcat-7.0.40, cree un archivo llamado **web.config** con el contenido siguiente:</span><span class="sxs-lookup"><span data-stu-id="7e0af-193">At the same directory level as the tomcat-7.0.40 folder, create a file named **web.config** with the following content:</span></span>

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

<span data-ttu-id="7e0af-194">En el bloque **httpPlatform**, **requestTimeout** se establece en "00:10:00".</span><span class="sxs-lookup"><span data-stu-id="7e0af-194">Under the **httpPlatform** block, the **requestTimeout** is set to “00:10:00”.</span></span>  <span data-ttu-id="7e0af-195">Se puede reducir, pero entonces es probable se vean algunos errores de tiempo de espera mientras Liferay arranca.</span><span class="sxs-lookup"><span data-stu-id="7e0af-195">It can be reduced but then you are likely to see some timeout errors while Liferay is bootstrapping.</span></span>  <span data-ttu-id="7e0af-196">Si se cambia este valor, se debe modificar también **connectionTimeout** en el archivo server.xml de tomcat.</span><span class="sxs-lookup"><span data-stu-id="7e0af-196">If this value is changed, then the **connectionTimeout** in the tomcat server.xml should also be modified.</span></span>  

<span data-ttu-id="7e0af-197">Vale la pena señalar que la variable de entorno JRE_HOME se especifica en web.config anterior para apuntar a la JDK de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="7e0af-197">It is worth noting that the JRE_HOME environnment varariable is specified in the above web.config to point to the 64-bit JDK.</span></span> <span data-ttu-id="7e0af-198">El valor predeterminado es 32 bits, pero debido a que Liferay puede requerir altos niveles de memoria, se recomienda utilizar el JDK de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="7e0af-198">The default is 32-bit, but since Liferay may require high levels of memory, it is recommended to use the 64-bit JDK.</span></span>

<span data-ttu-id="7e0af-199">Después de que realice estos cambios, reinicie la aplicación web que ejecuta Liferay y, a continuación, abra http://yourwebapp.</span><span class="sxs-lookup"><span data-stu-id="7e0af-199">Once you make these changes, restart your web app running Liferay, Then, open http://yourwebapp.</span></span> <span data-ttu-id="7e0af-200">El portal de Liferay está disponible en la raíz de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="7e0af-200">The Liferay portal is available from the web app root.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7e0af-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7e0af-201">Next steps</span></span>
<span data-ttu-id="7e0af-202">Para obtener más información sobre Liferay, consulte [http://www.liferay.com](http://www.liferay.com).</span><span class="sxs-lookup"><span data-stu-id="7e0af-202">For more information about Liferay, see [http://www.liferay.com](http://www.liferay.com).</span></span>

<span data-ttu-id="7e0af-203">Para más información sobre Java, visite [Azure para desarrolladores de Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="7e0af-203">For more information about Java, visit [Azure for Java developers](/java/azure).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[Servicio de aplicaciones de Azure]: http://go.microsoft.com/fwlink/?LinkId=529714
