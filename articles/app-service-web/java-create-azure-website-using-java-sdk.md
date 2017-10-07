---
title: "aaaCreate una aplicación Web en el servicio de aplicaciones de Azure con hello Azure SDK para Java"
description: "Obtenga información acerca de cómo toocreate una aplicación Web de servicio de aplicaciones de Azure mediante programación con hello Azure SDK para Java."
tags: azure-classic-portal
services: app-service-web
documentationcenter: Java
author: donntrenton
manager: erikre
editor: jimbe
ms.assetid: 8954c456-1275-4d57-aff4-ca7d6374b71e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/25/2016
ms.author: v-donntr
ms.openlocfilehash: 42ba86b7fbb5668b3675198d0c5bb454525f706b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-hello-azure-sdk-for-java"></a>Crear una aplicación Web en el servicio de aplicación de Azure con hello Azure SDK para Java
<!-- Azure Active Directory workflow is not yet available on hello Azure Portal -->

## <a name="overview"></a>Información general
Este tutorial muestra cómo toocreate un SDK de Azure para aplicaciones de Java que crea una aplicación Web en [servicio de aplicaciones de Azure][Azure App Service], a continuación, implemente un tooit de aplicación. Consta de dos partes:

* Parte 1 explica cómo toobuild una aplicación Java crea una aplicación web.
* Parte 2 se muestra cómo toocreate un JSP simple "Hola mundo" aplicación y, a continuación, use un FTP cliente toodeploy código tooApp servicio.

## <a name="prerequisites"></a>Requisitos previos
### <a name="software-installations"></a>Instalaciones de software
Hola AzureWebDemo código de la aplicación en este artículo se escribió con SDK de Java de Azure 0.7.0, que se puede instalar con hello [instalador de plataforma Web] [ Web Platform Installer] (WPI). Además, compruebe que toouse hello más reciente de versión hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]. Después de instalar el SDK de hello, actualizar las dependencias de hello en el proyecto de Eclipse ejecutando **Actualizar índice** en **repositorios de Maven**, a continuación, vuelva a agregar la versión más reciente de Hola de cada paquete en hello  **Dependencias** ventana. Puede comprobar la versión de Hola del software instalado en Eclipse haciendo clic en **Ayuda > detalles de la instalación**; debe haber Hola al menos siguientes versiones:

* Paquete para bibliotecas de Microsoft Azure para Java 0.7.0.20150309
* IDE de Eclipse para desarrolladores de Java EE 4.4.2.20150219

### <a name="create-and-configure-cloud-resources-in-azure"></a>Creación y configuración de recursos en la nube en Azure
Antes de comenzar este procedimiento, es necesario toohave una suscripción activa de Azure y configurar un valor predeterminado de Active Directory (AD) en Azure.

### <a name="create-an-active-directory-ad-in-azure"></a>Creación de un Active Directory (AD) en Azure
Si no tiene ya un Active Directory (AD) en su suscripción de Azure, inicie sesión en hello [portal de Azure clásico] [ Azure classic portal] con tu cuenta de Microsoft. Si tiene varias suscripciones, haga clic en **suscripciones** y directorio de hello seleccione predeterminado para la suscripción de Hola que desee toouse para este proyecto. A continuación, haga clic en **aplicar** tooswitch toothat vista de la suscripción.

1. Seleccione **Active Directory** desde el menú de Hola a la izquierda. Haga clic en **Nuevo > Directorio > Creación personalizada**.
2. En **Agregar directorio**, elija **Crear nuevo directorio**.
3. En **Nombre**, escriba un nombre para el directorio.
4. En **Dominio**, escriba un nombre de dominio. Se trata de un nombre de dominio básico que se incluye de forma predeterminada con el directorio; tiene forma de hello `<domain_name>.onmicrosoft.com`. Puede asignarle un nombre basado en el nombre del directorio de hello u otro nombre de dominio que posee. Más adelante, puede agregar otro nombre de dominio que ya use su organización.
5. En **País o región**, elija la configuración regional que corresponda.

Para obtener más información sobre AD, consulte [¿Qué es un directorio de Azure AD?][What is an Azure AD directory]

### <a name="create-a-management-certificate-for-azure"></a>Creación de un certificado de administración para Azure
Hello Azure SDK para Java utiliza tooauthenticate de certificados de administración con las suscripciones de Azure. Se trata de usar una aplicación cliente que utiliza hello tooact de API de administración de servicios en nombre de recursos de la suscripción de hello suscripción propietario toomanage tooauthenticate los certificados X.509 v3.

código de Hello en este procedimiento utiliza un certificado autofirmado tooauthenticate de Azure. Para este procedimiento, se necesita un certificado de toocreate y cargarlo toohello [portal de Azure clásico] [ Azure classic portal] con antelación. Esto implica Hola pasos:

* Generar un archivo PFX que represente el certificado de cliente y guardarlo localmente.
* Generar un certificado de administración (archivo .cer) del archivo PFX de Hola.
* Cargar Hola CER archivo tooyour suscripción de Azure.
* Convertir archivo PFX de hello en el almacén JKS, dado que Java utiliza ese tooauthenticate formato mediante certificados.
* Escribir código de autenticación de la aplicación hello, que hace referencia el archivo de almacén JKS local toohello.

Al completar este procedimiento, certificado CER de hello residirá en la suscripción de Azure y certificado de almacén JKS Hola residirá en la unidad local. Para obtener más información sobre la administración de certificados, consulte [Crear y cargar un certificado de administración para Azure][Create and Upload a Management Certificate for Azure].

#### <a name="create-a-certificate"></a>Creación de un certificado
toocreate su propio certificado autofirmado, abra una consola de comandos en el sistema operativo y ejecute hello siga los comandos.

> **Nota:** equipo hello en el que se ejecuta este comando debe tener Hola JDK instalado. Además, la Hola ruta de acceso toohello keytool depende de la ubicación de Hola de instalación de JDK Hola. Para obtener más información, consulte [clave y la herramienta de administración de certificados (keytool)] [ Key and Certificate Management Tool (keytool)] en documentos de hello Java en línea.
> 
> 

archivo .pfx de toocreate hello:

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

archivo .cer de toocreate hello:

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

donde:

* `<java-install-dir>`es el directorio de toohello de ruta de acceso de hello en el que se instaló Java.
* `<keystore-id>`es el identificador de entrada del almacén de claves de hello (por ejemplo, `AzureRemoteAccess`).
* `<cert-store-dir>`es Hola ruta de acceso toohello directorio en el que desea que los certificados de toostore (por ejemplo `C:/Certificates`).
* `<cert-file-name>`es el nombre de Hola Hola del archivo de certificado (por ejemplo `AzureWebDemoCert`).
* `<password>`es la contraseña Hola elige tooprotect Hola certificado; debe ser al menos 6 caracteres. Se puede optar por no escribir ninguna contraseña, aunque no se recomienda.
* `<dname>`es Hola nombre distintivo X.500 toobe asociado con el alias y se utiliza como emisor de Hola y los campos de sujeto de certificado autofirmado Hola.

Para obtener más información, consulte [Crear y cargar un certificado de administración para Azure][Create and Upload a Management Certificate for Azure].

#### <a name="upload-hello-certificate"></a>Cargar certificado Hola
tooupload tooAzure de un certificado autofirmado, vaya toohello **configuración** página portal clásico de hello, haga clic en hello **certificados de administración** ficha. Haga clic en **cargar** final Hola de hello página y navegar toohello ubicación del archivo CER Hola creado.

#### <a name="convert-hello-pfx-file-into-jks"></a>Convertir archivo PFX de hello en el almacén JKS
Hola de línea de comandos de Windows (que se ejecuta como administrador), cd toohello directorio que contiene Hola certificados y ejecute hello siguiente comando, donde `<java-install-dir>` es el directorio de hello en el que instaló Java en el equipo:

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. Cuando se le solicite, escriba la contraseña del almacén de claves de destino de hello; se trata de contraseña de hello para el archivo de almacén JKS hello.
2. Cuando se le solicite, escriba la contraseña del almacén de claves de origen de hello; se trata de una contraseña de Hola que especificó para el archivo PFX de Hola.

las dos contraseñas de Hello no tiene toobe Hola igual. Se puede optar por no escribir ninguna contraseña, aunque no se recomienda.

## <a name="build-a-web-app-creation-application"></a>Compilación de una aplicación para crear aplicaciones web
### <a name="create-hello-eclipse-workspace-and-maven-project"></a>Crear Hola área de trabajo de Eclipse y proyectos de Maven
En esta sección se creará un área de trabajo y un proyecto de Maven para la aplicación de creación de aplicaciones de web hello, denominado AzureWebDemo.

1. Cree un nuevo proyecto de Maven. Haga clic en **File (Archivo) > New (Nuevo) > Maven Project (Proyecto de Maven)**. En **New Maven Project** (Nuevo proyecto de Maven), elija **Create a simple project** (Crear proyecto sencillo) y, a continuación, elija **Use default workspace location** (Usar ubicación de espacio de trabajo predeterminada).
2. En la segunda página de Hola de **Maven proyecto**, especifique Hola siguiente:
   
   * Group ID (Identificador del grupo): `com.<username>.azure.webdemo`
   * Artifact ID (Identificador de artefacto): AzureWebDemo
   * Version (Versión): 0.0.1-SNAPSHOT
   * Packaging (Empaquetado): jar
   * Name (Nombre): AzureWebDemo
     
     Haga clic en **Finalizar**
3. Abra el archivo de pom.xml del nuevo proyecto de hello en el Explorador de proyectos. Seleccione hello **dependencias** ficha. Como se trata de un nuevo proyecto, todavía no se muestra ningún paquete.
4. Ver los repositorios de Maven Hola abierto. **Haga clic en Window (Ventana) &gt; Show View (Mostrar vista) &gt; Other (Otro) &gt; Maven &gt; Maven Repositories (Repositorios de Maven)** y luego en **OK** (Aceptar). Hola **Maven repositorios** vista aparecerá en parte inferior de Hola de hello IDE.
5. Abra **repositorios globales**, contextual hello **central** repositorio y seleccione **volver a generar índice**.
   
    ![][1]
   
    Este paso puede tardar varios minutos, según la velocidad de saludo de la conexión. Cuando se vuelve a generar el índice de hello, debería ver paquetes de Microsoft Azure de hello en hello **central** repositorio de Maven.
6. En **Dependencies** (Dependencias), haga clic en **Add** (Agregar). En **Enter Group ID...** (Especificar identificador de grupo), escriba `azure-management`. Seleccionar paquetes de saludo para administración de la base y la administración de aplicaciones Web de servicio de aplicación:
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > **Nota:** si va a actualizar las dependencias de hello después de una nueva versión de lanzamiento, necesita toore-agregar cada una de las dependencias de hello en esta lista.
   > Tras hacer clic en **agregar** y seleccione cada dependencia, ésta aparece con el nuevo número de versión Hola Hola **dependencias** lista.
   > 
   > 

Haga clic en **Aceptar**. Hola paquetes de Azure, a continuación, aparecen en hello **dependencias** lista.

### <a name="writing-java-code-toocreate-a-web-app-by-calling-hello-azure-sdk"></a>Escribir código Java tooCreate una aplicación Web que realiza la llamada hello Azure SDK
A continuación, escribir código de hello que llama a las API de hello Azure SDK para hello de Java toocreate aplicación de servicio de aplicaciones web.

1. Crear un código de punto de entrada principal de Java clase toocontain Hola. En el Explorador de proyectos, haga doble clic en el nodo del proyecto de Hola y seleccione **nuevo > clase**.
2. En **nueva clase de Java**, el nombre de clase hello `WebCreator` y comprobar hello **principal de void estático público** casilla de verificación. selecciones de Hello deberían aparecer como sigue:
   
    ![][2]
3. Haga clic en **Finalizar** archivo de Hello WebCreator.java aparece en el Explorador de proyectos.

### <a name="calling-hello-azure-api-toocreate-an-app-service-web-app"></a>Al llamar a hello Azure API tooCreate una aplicación de servicio de aplicaciones Web
#### <a name="add-necessary-imports"></a>Adición de las importaciones necesarias
En WebCreator.java, agregue Hola siguiendo las importaciones; estas importaciones proporcionan acceso tooclasses en hello las bibliotecas de administración para utilizar las API de Azure:

    // General imports
    import java.net.URI;
    import java.util.ArrayList;

    // Imports for Exceptions
    import java.io.IOException;
    import java.net.URISyntaxException;
    import javax.xml.parsers.ParserConfigurationException;
    import com.microsoft.windowsazure.exception.ServiceException;
    import org.xml.sax.SAXException;

    // Imports for Azure App Service management configuration
    import com.microsoft.windowsazure.Configuration;
    import com.microsoft.windowsazure.management.configuration.ManagementConfiguration;

    // Service management imports for App Service Web Apps creation
    import com.microsoft.windowsazure.management.websites.*;
    import com.microsoft.windowsazure.management.websites.models.*;

    // Imports for authentication
    import com.microsoft.windowsazure.core.utils.KeyStoreType;


#### <a name="define-hello-main-entry-point-class"></a>Definir la clase de punto de entrada principal de hello
Porque Hola de hello AzureWebDemo aplicación sirve toocreate una aplicación de servicio de aplicaciones Web, name clase principal de Hola para esta aplicación `WebAppCreator`. Esta clase proporciona código de punto de entrada principal de Hola que llama la aplicación web de hello API de administración de servicios de Azure toocreate Hola.

Agregar Hola siguiendo las definiciones de parámetro para la aplicación web de hello y espacio Web. Necesitará tooprovide su propia información de identificador y el certificado de suscripción de Azure.

    public class WebAppCreator {

        // Parameter definitions used for authentication.
        private static String uri = "https://management.core.windows.net/";
        private static String subscriptionId = "<subscription-id>";
        private static String keyStoreLocation = "<certificate-store-path>";
        private static String keyStorePassword = "<certificate-password>";

        // Define web app parameter values.
        private static String webAppName = "WebDemoWebApp";
        private static String domainName = ".azurewebsites.net";
        private static String webSpaceName = WebSpaceNames.WESTUSWEBSPACE;
        private static String appServicePlanName = "WebDemoAppServicePlan";

donde:

* `<subscription-id>`es el Id. de suscripción de Azure de hello en el que desea que el recurso de Hola de toocreate.
* `<certificate-store-path>`es la ruta de acceso y nombre de archivo toohello almacén JKS archivo hello en el directorio de almacén de certificados local. Por ejemplo, `C:/Certificates/CertificateName.jks` para Linux y `C:\Certificates\CertificateName.jks` para Windows.
* `<certificate-password>`es la contraseña de Hola que especificó cuando creó el certificado del almacén JKS.
* `webAppName`puede ser cualquier nombre que elija; Este procedimiento utiliza el nombre de hello `WebDemoWebApp`. nombre de dominio completo de Hello es hello `webAppName` con hello `domainName` anexado, por lo que en este caso dominio completo de hello es `webdemowebapp.azurewebsites.net`.
* `domainName` debe especificarse del modo indicado anteriormente.
* `webSpaceName`debe ser uno de los valores de hello definidos en hello [WebSpaceNames] [ WebSpaceNames] clase.
* `appServicePlanName` debe especificarse del modo indicado anteriormente.

> **Nota:** cada vez que se ejecuta esta aplicación, necesita toochange Hola valo `webAppName` y `appServicePlanName` (o eliminar la aplicación web de hello en hello Portal de Azure) antes de ejecutar de nuevo la aplicación hello. En caso contrario, se producirá un error la ejecución porque hello mismo recurso ya existe en Azure.
> 
> 

#### <a name="define-hello-web-creation-method"></a>Definir el método de creación de hello web
A continuación, defina una aplicación web de método toocreate Hola. Este método, `createWebApp`, especifica los parámetros de Hola de hello web app y espacio Web Hola. También crea y configura el cliente de administración de aplicaciones Web de servicio de aplicación hello, que se define por hello [WebSiteManagementClient] [ WebSiteManagementClient] objeto. cliente de administración de Hello es clave toocreating las aplicaciones Web. Proporciona servicios web RESTful que permiten a las aplicaciones toomanage aplicaciones web (realizar operaciones como crear, update y delete) mediante una llamada a la API de administración de servicios de Hola.

    private static void createWebApp() throws Exception {

        // Specify configuration settings for hello App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path toohello JKS file
            keyStorePassword,  // Password for hello JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create hello App Service Web Apps management client toocall Azure APIs
        // and pass it hello App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for hello web app with hello specified parameters.
        WebHostingPlanCreateParameters appServicePlanParams = new WebHostingPlanCreateParameters();
        appServicePlanParams.setName(appServicePlanName);
        appServicePlanParams.setSKU(SkuOptions.Free);
        webAppManagementClient.getWebHostingPlansOperations().create(webSpaceName, appServicePlanParams);

        // Set webspace parameters.
        WebSiteCreateParameters.WebSpaceDetails webSpaceDetails = new WebSiteCreateParameters.WebSpaceDetails();
        webSpaceDetails.setGeoRegion(GeoRegionNames.WESTUS);
        webSpaceDetails.setPlan(WebSpacePlanNames.VIRTUALDEDICATEDPLAN);
        webSpaceDetails.setName(webSpaceName);

        // Set web app parameters.
        // Note that hello server farm name takes hello Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define hello web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create hello web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output hello HTTP status code of hello response; 200 indicates hello request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output hello name of hello web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

código de Hello dará como resultado de estado HTTP Hola de respuesta de Hola que indica éxito o error y si se realiza correctamente, dará como resultado el nombre de Hola de hello creado la aplicación web.

#### <a name="define-hello-main-method"></a>Definir el método main() de Hola
Proporcionar código del método main() Hola esa aplicación web de llamadas createWebApp() toocreate Hola.

Por último, efectúe una llamada a `createWebApp` desde `main`:

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-hello-application-and-verify-web-app-creation"></a>Ejecutar la aplicación hello y comprobar la creación de aplicaciones web
tooverify que se ejecuta la aplicación, haga clic en **ejecutar > ejecutar**. Cuando complete la ejecución de aplicación hello, debería ver Hola después de salida en la consola de Eclipse hello:

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

Inicie sesión en el portal de Azure clásico de Hola y haga clic en **aplicaciones Web**. aplicación web nueva de Hello debe aparecer en la lista de aplicaciones Web de hello dentro de unos minutos.

## <a name="deploying-an-application-toohello-web-app"></a>Implementar una aplicación Web de aplicación toohello
Después de que han ejecutado AzureWebDemo y creó Hola nueva aplicación web, inicie sesión en el portal clásico de hello, haga clic en **aplicaciones Web**y seleccione **WebDemoWebApp** en hello **aplicaciones Web** lista. En la página del panel de la aplicación de hello web, haga clic en **examinar** (o haga clic en la dirección URL de hello, `webdemowebapp.azurewebsites.net`) toonavigate tooit. Verá una página de marcador de posición en blanco, porque no hay contenido ha sido publicado toohello web app aún.

A continuación creará una aplicación "Hello World" e implementar toohello web app.

### <a name="create-a-jsp-hello-world-application"></a>Creación de una aplicación Hello World en JSP
#### <a name="create-hello-application"></a>Crear aplicación hello
En toodemonstrate orden cómo Hola toodeploy web toohello aplicación, siga el procedimiento muestra cómo toocreate una sencilla aplicación de Java de "Hello World" y la carga toohello aplicación Web de aplicación de servicio que creó la aplicación.

1. Haga clic en **File (Archivo) > New (Nuevo) > Dynamic Web Project (Proyecto web dinámico)**. Asígnele el nombre `JSPHello`. No es necesario toochange ninguna otra configuración de este cuadro de diálogo. Haga clic en **Finalizar**
   
    ![][3]
2. En el Explorador de proyectos, expanda hello **JSPHello** proyecto de equipo y haga clic en **WebContent**, a continuación, haga clic en **nuevo > archivo JSP**. En el cuadro de diálogo de nuevo archivo JSP hello, nombre hello nuevo archivo `index.jsp`. Haga clic en **Siguiente**.
3. Hola **Select JSP Template** cuadro de diálogo, seleccione **New JSP File (html)** y haga clic en **finalizar**.
4. En el archivo index.jsp agregar Hola después el código de hello `<head>` y `<body>` etiquetar secciones:
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, hello time is <%= date %> 
        </body>

#### <a name="run-hello-hello-world-application-in-localhost"></a>Ejecutar la aplicación hello World Hello en localhost
Antes de ejecutar esta aplicación, necesita tooconfigure algunas propiedades.

1. Menú contextual hello **JSPHello** de proyecto y seleccione **propiedades**.
2. Hola **propiedades** diálogo: seleccione **Java Build Path**, seleccione hello **ordenar y exportar** ficha, comprobación de **JRE biblioteca del sistema**, a continuación, haga clic en **Una** toomove se toohello superior de la lista de Hola.
   
    ![][4]
3. También en hello **propiedades** diálogo: seleccione **tiempos de ejecución de destino** y haga clic en **nuevo**.
4. Hola **nuevo entorno de tiempo de ejecución de servidor** cuadro de diálogo, seleccione un servidor como **Apache Tomcat v7.0** y haga clic en **siguiente**. Hola **servidor de Tomcat** cuadro de diálogo, establezca **nombre** demasiado`Apache Tomcat v7.0`y establezca **directorio de instalación de Tomcat** directorio toohello en el que instaló la versión de Hola de Servidor de Tomcat que desee toouse.
   
    ![][5]
   
    Haga clic en **Finalizar**
5. A continuación, devolver toohello **tiempos de ejecución de destino** página de hello **propiedades** cuadro de diálogo. Elija **Apache Tomcat v7.0** y haga clic en **OK** (Aceptar).
   
    ![][6]
6. Hola Eclipse **ejecutar** menú, haga clic en **ejecutar**. Hola **ejecución** cuadro de diálogo, seleccione **ejecutar en el servidor**. Hola **ejecutar en el servidor** cuadro de diálogo, seleccione **Tomcat v7.0 Server**:
   
    ![][7]
   
    Haga clic en **Finalizar**
7. Hola cuando ejecuta la aplicación, debería ver Hola **JSPHello** página aparecen en una ventana de localhost en Eclipse (`http://localhost:8080/JSPHello/`), mostrar Hola siguiente mensaje:
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-hello-application-as-a-war"></a>Exportar aplicación hello como una guerra
Exportar archivos de proyecto de hello web como un archivo web (WAR) para que pueda implementar toohello web app. Hello siguientes archivos de proyecto web residen en hello WebContent carpeta:

    META-INF
    WEB-INF
    index.jsp

1. Haga clic en carpeta de hello WebContent y seleccione **exportar**.
2. Hola **Exportar seleccione** cuadro de diálogo, haga clic en **Web > WAR** de archivos, a continuación, haga clic en **siguiente**.
3. Hola **exportar WAR** cuadro de diálogo, seleccione el directorio de src de hello en el proyecto actual de hello e incluir nombre de Hola de archivo WAR de hello final Hola. Por ejemplo:
   
    `<project-path>/JSPHello/src/JSPHello.war`

Para obtener más información sobre cómo implementar archivos WAR, consulte [agregar una tooAzure de aplicación de Java aplicación del servicio de aplicaciones Web](web-sites-java-add-app.md).

### <a name="deploying-hello-hello-world-application-using-ftp"></a>Implementar Hola Hola mundo aplicación mediante FTP
Seleccione una aplicación de terceros FTP cliente toopublish Hola. Este procedimiento describe dos opciones: consola de Kudu Hola integrada en Azure; y FileZilla, una herramienta muy usada con una interfaz de usuario adecuada, gráfica.

> **Nota:** Hola Kit de herramientas de Azure para Eclipse es compatible con cuentas de implementación de toostorage y servicios en la nube, pero no admite actualmente las aplicaciones de tooweb de implementación. Puede implementar toostorage cuentas y servicios mediante un proyecto de implementación de Azure como se describe en la nube [crear una aplicación Hello World de Azure en Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), pero no a las aplicaciones tooweb. Utilizar otros métodos, como FTP o GitHub tootransfer archivos tooyour aplicación web.
> 
> **Nota:** no se recomienda usar FTP desde la línea de comandos de Windows hello (Hola de línea de comandos FTP.EXE utilidad que se incluye con Windows). Los clientes FTP que utilicen FTP activo, por ejemplo, FTP.EXE, a menudo no toowork a través de firewalls. FTP activo especifica una dirección interna basado en LAN, servidor FTP toowhich probablemente se producirá un error tooconnect.
> 
> 

Para obtener más información sobre la aplicación del servicio de aplicaciones web de implementación tooan mediante FTP, vea Hola temas siguientes:

* [Implementación mediante una utilidad FTP](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a>Configurar credenciales de implementación
Asegúrese de que ha ejecutado hello **AzureWebDemo** aplicación toocreate una aplicación web. Transferirá ubicación toothis de archivos.

1. Inicie sesión en el portal clásico de Hola y haga clic en **aplicaciones Web**. Asegúrese de que **WebDemoWebApp** aparece en la lista de Hola de aplicaciones web y asegúrese de que se está ejecutando. Haga clic en **WebDemoWebApp** tooopen su **panel** página.
2. En hello **panel** página, en **vista rápida**, haga clic en **configurar las credenciales de implementación** (si ya tiene las credenciales de implementación, éste lee  **Restablecer las credenciales de implementación**).
   
    Credenciales de implementación asociadas con una cuenta de Microsoft. Deberá toospecify un nombre de usuario y la contraseña que se puede usar toodeploy mediante Git y FTP. Puede usar estas aplicaciones web de credenciales toodeploy tooany en todas las suscripciones de Azure asociadas a su cuenta de Microsoft. Proporcione las credenciales de implementación de Git y FTP en el cuadro de diálogo de hello y el nombre de usuario de registro hello y una contraseña para un uso futuro.

#### <a name="get-ftp-connection-information"></a>Obtención de la información de conexión para FTP
toouse FTP toodeploy aplicación archivos toohello que acaba de crear aplicación web, necesitará información de conexión de tooobtain. Hay dos maneras de obtener información de conexión de tooobtain. Una manera es la aplicación web de toovisit hello **panel** página; hello otra manera es perfil de publicación de la aplicación web de toodownload Hola. perfil de publicación de Hello es un archivo XML que proporciona información como credenciales de inicio de sesión y el nombre de host FTP para las aplicaciones web en el servicio de aplicaciones de Azure. Puede usar esta aplicación toodeploy tooany web de nombre de usuario y contraseña en todas las suscripciones asociadas con hello cuenta de Azure, no solo este uno.

información de conexión de tooobtain FTP de hoja de la aplicación web Hola Hola [Portal de Azure][Azure Portal]:

1. En **Essentials**, busque y copie hello **nombre de host FTP**. Esto es un URI similar demasiado`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.
2. En **Essentials**, busque y copie **FTP/Nombre de usuario de implementación**. Esto provocará que el formulario de hello *webappname\deployment-username*; por ejemplo `WebDemoWebApp\deployer77`.

perfil de publicación de información de conexión de FTP tooobtain de hello:

1. En la hoja de la aplicación de hello web, haga clic en **Get perfil de publicación**. Se descargará una unidad local de .publishsettings archivo tooyour.
2. Abra el archivo .publishsettings de hello en un editor XML o editor de texto y busque hello `<publishProfile>` que contiene el elemento `publishMethod="FTP"`. Debería ser similar Hola siguiente:
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. Tenga en cuenta esa aplicación de web hello `publishProfile` configuración asignar configuración de administrador del sitio FileZilla toohello como sigue:

* `publishUrl`se Hola igual **nombre de host FTP**, Hola valor establecido en **Host**.
* `publishMethod="FTP"`significa que se establece **protocolo** demasiado**FTP: protocolo de transferencia de archivos**, y **cifrado** demasiado**usar FTP sin formato**.
* `userName`y `userPWD` son claves para hello valores reales de nombre de usuario y la contraseña que especificó al restablecer credenciales de implementación de Hola. `userName`se Hola igual **implementación / FTP usuario**. Se asignan demasiado**usuario** y **contraseña** en FileZilla.
* `ftpPassiveMode="True"`significa que ese sitio Hola FTP utiliza a transferencia FTP pasivo; Seleccione **pasivo** en hello **configuración de transferencia** ficha.

#### <a name="configure-hello-web-app-toohost-a-java-application"></a>Configurar la aplicación Web de hello toohost una aplicación de Java
Antes de publicar la aplicación hello, tendrá que toochange algunos valores de configuración para que hello aplicación web puede hospedar una aplicación Java.

1. En el portal clásico de hello, vaya toohello web app **panel** página y haga clic en **configurar**. En hello **configurar** página, especifique Hola después de la configuración.
2. En **versión de Java** Hola predeterminado es **desactivar**; seleccione versión de Java de hello destine su aplicación; por ejemplo 1.7.0_51. Después de hacer esto, también Asegúrese de que **contenedor Web** se establece la versión de tooa de servidor de Tomcat.
3. En **documentos predeterminados**, agregue index.jsp y moverlo hacia arriba de la parte superior de toohello de lista de Hola. (archivo de saludo predeterminado para las aplicaciones web es hostingstart.html).
4. Haga clic en **Guardar**.

#### <a name="publish-your-application-using-kudu"></a>Publicación de la aplicación mediante Kudu
Aplicación de una manera toopublish hello es hello toouse que kudu depurar consola integrada en Azure. Kudu se conoce toobe estable y coherente con la aplicación del servicio de aplicaciones Web y el servidor de Tomcat. Tener acceso a la consola de hello para la aplicación web de hello examinando la dirección URL de tooa de hello siguiendo el formato:

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. Para este procedimiento, consola de hello Kudu se encuentra en hello después de la dirección URL; Busque la ubicación de toothis:
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. En el menú superior de hello, seleccione **consola Depurar > CMD**.
3. En la línea de comandos de consola de hello, navegue demasiado`/site/wwwroot` (o haga clic en `site`, a continuación, `wwwroot` en la vista de directorio de hello al principio de Hola de página de hello):
   
    `cd /site/wwwroot`
4. Después de especificar un valor en **Versión de Java**, el servidor de Tomcat debe crear un directorio de aplicaciones web. En la línea de comandos de consola de hello, desplácese toohello directorio de aplicaciones Web:
   
    `mkdir webapps`
   
    `cd webapps`
5. Arrastre JSPHello.war de `<project-path>/JSPHello/src/` y colóquelo en la vista de directorio de hello Kudu en `/site/wwwroot/webapps`. No lo arrastre toohello "Arrastre aquí tooupload y zip" área, porque descomprímalo Tomcat.
   
   ![][8]

En JSPHello.war primera aparece en el área de directorio de Hola por sí solo:

  ![][9]

En poco tiempo (probablemente menos de 5 minutos) servidor de Tomcat se descomprima el archivo WAR de hello en un directorio JSPHello desempaquetado. Haga clic en hello raíz directory toosee si se ha descomprimido index.jsp y se copiarán allí. Si es así, vaya toosee de directorio de aplicaciones Web toohello atrás si Hola desempaqueta JSPHello se ha creado el directorio. Si no ve estos elementos, espere y repita el procedimiento.

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a>Publicación de la aplicación mediante FileZilla (opcional)
Otra herramienta que puede usar la aplicación de hello toopublish es FileZilla, un cliente FTP de otros fabricantes popular con una interfaz de usuario adecuada, gráfico. Puede descargar e instalar FileZilla desde [http://filezilla-project.org/](http://filezilla-project.org/) en caso de que no lo tenga. Para obtener más información sobre el uso de cliente hello, vea hello [FileZilla documentación](https://wiki.filezilla-project.org/Documentation) y esta entrada de blog en [los clientes FTP - parte 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).

1. En FileZilla, haga clic en **Archivo > Gestor de sitios**.
2. Hola **Site Manager** cuadro de diálogo, haga clic en **nuevo sitio**. Aparecerá un nuevo sitio FTP en blanco en **Seleccionar entrada** preguntar tooprovide un nombre. Para este procedimiento, asígnele el nombre `AzureWebDemo-FTP`.
   
    En hello **General** ficha, especifique Hola después de configuración:
   
   * **Host:** ENTRAR hello **nombre de Host FTP** que copió desde el panel de Hola.
   * **Puerto:** (dejarlo en blanco, tal y como se trata de una transferencia de pasivo y servidor hello determinará Hola puerto toouse.)
   * **Protocolo:** FTP - Protocolo de Transferencia de Archivos
   * **Cifrado:** Use plain FTP (Usar FTP sin formato)
   * **Modo de acceso:** Normal
   * **Usuario:** ENTRAR Hola implementación / FTP de usuario que ha copiado en el panel de Hola. Se trata de hello nombre de usuario FTP completo, que tiene formato de hello *webappname\username*.
   * **Contraseña:** escriba la contraseña de Hola que especificó al configurar las credenciales de implementación de Hola.
     
     En hello **configuración de transferencia** ficha, seleccione **pasivo**.
3. Haga clic en **Conectar**. Si es correcta, consola del FileZilla se mostrará un `Status: Connected` mensaje y emitir un `LIST` comando contenido del directorio toolist Hola.
4. Hola **Local** el panel de sitio, directorio de origen de hello seleccione en qué archivo de JSPHello.war hello reside; ruta de acceso de hello será similar siguiente toohello:
   
    `<project-path>/JSPHello/src/`
5. Hola **remoto** panel sitio, la carpeta de destino de hello select. Implementará Hola WAR archivo toohello `webapps` directorio en la raíz de la aplicación hello web. Navegue demasiado`/site/wwwroot`, haga doble clic en `wwwroot`y seleccione **crear directorio**. Directorio de nombres de hello `webapps` y escriba ese directorio.
6. Transferir JSPHello.war demasiado`/site/wwwroot/webapps`. Seleccione JSPHello.war en hello **Local** lista de archivos, haga doble clic en él y seleccione **cargar**. Deberá mostrarse en `/site/wwwroot/webapps`.
7. Una vez copiado el directorio de aplicaciones Web de JSPHello.war toohello, automáticamente se desempaquetar el servidor de Tomcat (Descomprimir) Hola archivos en archivo WAR de hello. Aunque el servidor de Tomcat comienza a desempaquetar casi de inmediato, es posible que tarde mucho tiempo (posiblemente horas) para hello tooappear de archivos de cliente de hello FTP.

#### <a name="run-hello-hello-world-application-on-hello-web-app"></a>Ejecutar aplicación hello Hello World en hello aplicación Web
1. Una vez que haya cargado el archivo WAR de hello y comprobar que el servidor de Tomcat ha creado un desempaquetados `JSPHello` directory, examinar demasiado`http://webdemowebapp.azurewebsites.net/JSPHello` aplicación de hello toorun.
   
   > **Nota:** si hace clic en **examinar** desde portal clásico de hello, podría obtener página Web predeterminada de hello, que dice "esta aplicación web de Java según se creó correctamente." Podría tener página Web de hello toorefresh en orden tooview Hola salida de la aplicación en lugar de la página Web predeterminada de Hola.
   > 
   > 
2. Cuando se ejecuta la aplicación hello, verá una página web con hello después de salida:
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a>Limpieza de los recursos de Azure
Este procedimiento crea una aplicación web de Servicio de aplicaciones. Se le facturará para el recurso de hello mientras existe. A menos que piense toocontinue con hello web app para pruebas o desarrollo, debería considerar detener o eliminarlo. Una aplicación web detenida generará un gasto pequeño, pero podrá volver a iniciarla en cualquier momento. Eliminar una aplicación web, borra todos los datos que se ha cargado tooit.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

[1]: ./media/java-create-azure-website-using-java-sdk/eclipse-maven-repositories-rebuild-index.png
[2]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-java-class.png
[3]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-dynamic-web-project.png
[4]: ./media/java-create-azure-website-using-java-sdk/eclipse-java-build-path.png
[5]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-tomcat-server.png
[6]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-properties-page.png
[7]: ./media/java-create-azure-website-using-java-sdk/eclipse-run-on-server.png
[8]: ./media/java-create-azure-website-using-java-sdk/kudu-console-drag-drop.png
[9]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-1.png
[10]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-2.png


[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Platform Installer]: http://go.microsoft.com/fwlink/?LinkID=252838
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh690946.aspx
[Azure classic portal]: https://manage.windowsazure.com
[What is an Azure AD directory]: http://technet.microsoft.com/library/jj573650.aspx
[Create and Upload a Management Certificate for Azure]: ../cloud-services/cloud-services-certs-create.md
[Key and Certificate Management Tool (keytool)]: http://docs.oracle.com/javase/6/docs/technotes/tools/windows/keytool.html
[WebSiteManagementClient]: http://azure.github.io/azure-sdk-for-java/com/microsoft/azure/management/websites/WebSiteManagementClient.html
[WebSpaceNames]: http://dl.windowsazure.com/javadoc/com/microsoft/windowsazure/management/websites/models/WebSpaceNames.html
[Azure Portal]: https://portal.azure.com
