---
title: "línea de comandos de AD Java Introducción aaaAzure | Documentos de Microsoft"
description: "¿Cómo toobuild un Java comando aplicación de línea que firma los usuarios de tooaccess una API."
services: active-directory
documentationcenter: java
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 51e1a8f9-6ff0-4643-a350-0ba794e26fd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 9ba1d1e794928a39ca1f091bd0e6eba57ce3d6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-java-command-line-app-tooaccess-an-api-with-azure-ad"></a><span data-ttu-id="83eda-103">Uso de aplicaciones de línea de comandos de Java tooAccess una API con Azure AD</span><span class="sxs-lookup"><span data-stu-id="83eda-103">Using Java Command Line App tooAccess An API with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="83eda-104">Azure AD facilita toooutsource simple y sencilla administración de identidad de su aplicación web, que proporciona un único inicio de sesión y cierre de sesión con unas pocas líneas de código.</span><span class="sxs-lookup"><span data-stu-id="83eda-104">Azure AD makes it simple and straightforward toooutsource your web app's identity management, providing single sign-in and sign-out with only a few lines of code.</span></span>  <span data-ttu-id="83eda-105">En aplicaciones web de Java, puede hacerlo mediante la implementación de Microsoft de hello ADAL4J controlada por la Comunidad.</span><span class="sxs-lookup"><span data-stu-id="83eda-105">In Java web apps, you can accomplish this using Microsoft's implementation of hello community-driven ADAL4J.</span></span>

  <span data-ttu-id="83eda-106">Aquí, usaremos ADAL4J para:</span><span class="sxs-lookup"><span data-stu-id="83eda-106">Here we'll use ADAL4J to:</span></span>

* <span data-ttu-id="83eda-107">Usuario de Hola de inicio de sesión en la aplicación hello mediante Azure AD como proveedor de identidades de Hola.</span><span class="sxs-lookup"><span data-stu-id="83eda-107">Sign hello user into hello app using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="83eda-108">Mostrar información acerca del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="83eda-108">Display some information about hello user.</span></span>
* <span data-ttu-id="83eda-109">Inicio de sesión Hola usuario fuera de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="83eda-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="83eda-110">En Ordenar toodo esto, necesitará:</span><span class="sxs-lookup"><span data-stu-id="83eda-110">In order toodo this, you'll need to:</span></span>

1. <span data-ttu-id="83eda-111">Registro de una aplicación con Azure AD</span><span class="sxs-lookup"><span data-stu-id="83eda-111">Register an application with Azure AD</span></span>
2. <span data-ttu-id="83eda-112">Configurar la biblioteca de ADAL4J aplicación toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="83eda-112">Set up your app toouse hello ADAL4J library.</span></span>
3. <span data-ttu-id="83eda-113">Utilice hello ADAL4J biblioteca tooissue sesión y las solicitudes de cierre de sesión tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="83eda-113">Use hello ADAL4J library tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="83eda-114">Imprimir datos acerca del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="83eda-114">Print out data about hello user.</span></span>

<span data-ttu-id="83eda-115">tooget iniciado, [descargar esqueleto de aplicación Hola](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) o [Descargar ejemplo Hola completado](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="83eda-115">tooget started, [download hello app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) or [download hello completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>  <span data-ttu-id="83eda-116">También necesitará a un inquilino de Azure AD en qué tooregister la aplicación.</span><span class="sxs-lookup"><span data-stu-id="83eda-116">You'll also need an Azure AD tenant in which tooregister your application.</span></span>  <span data-ttu-id="83eda-117">Si aún no tiene uno, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="83eda-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1--register-an-application-with-azure-ad"></a><span data-ttu-id="83eda-118">1.  Registro de una aplicación con Azure AD</span><span class="sxs-lookup"><span data-stu-id="83eda-118">1.  Register an Application with Azure AD</span></span>
<span data-ttu-id="83eda-119">tooenable los usuarios de tooauthenticate aplicación, primero deberá tooregister una nueva aplicación en su inquilino.</span><span class="sxs-lookup"><span data-stu-id="83eda-119">tooenable your app tooauthenticate users, you'll first need tooregister a new application in your tenant.</span></span>

1. <span data-ttu-id="83eda-120">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="83eda-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="83eda-121">En la barra superior de hello, haga clic en su cuenta y en hello **Directory** lista, elija el inquilino de Active Directory de Hola que le gustaría tooregister la aplicación.</span><span class="sxs-lookup"><span data-stu-id="83eda-121">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="83eda-122">Haga clic en **más servicios** en Hola nav izquierda y elija **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="83eda-122">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="83eda-123">Haga clic en **Registros de aplicaciones** y elija **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="83eda-123">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="83eda-124">Siga las indicaciones de Hola y crear un nuevo **aplicación Web o WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="83eda-124">Follow hello prompts and create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="83eda-125">Hola **nombre** de hello aplicación describirá los tooend-usuarios de la aplicación</span><span class="sxs-lookup"><span data-stu-id="83eda-125">hello **name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="83eda-126">Hola **dirección URL de inicio de sesión** es Hola dirección URL base de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="83eda-126">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="83eda-127">valor predeterminado del esqueleto Hello es `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="83eda-127">hello skeleton's default is `http://localhost:8080/adal4jsample/`.</span></span>
6. <span data-ttu-id="83eda-128">Una vez que haya completado el registro, AAD asignará a su aplicación un identificador de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="83eda-128">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="83eda-129">Necesitará este valor en las secciones siguientes de hello, por lo tanto cópiela desde la pestaña de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="83eda-129">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="83eda-130">De hello **configuración** -> **propiedades** página de la aplicación, actualice Hola App ID URI.</span><span class="sxs-lookup"><span data-stu-id="83eda-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="83eda-131">Hola **App ID URI** es un identificador único para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="83eda-131">hello **App ID URI** is a unique identifier for your application.</span></span>  <span data-ttu-id="83eda-132">convención de Hello es toouse `https://<tenant-domain>/<app-name>`, por ejemplo, `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="83eda-132">hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `http://localhost:8080/adal4jsample/`.</span></span>

<span data-ttu-id="83eda-133">Una vez en el portal de hello para la aplicación cree un **clave** de hello **configuración** página de la aplicación y cópiela.</span><span class="sxs-lookup"><span data-stu-id="83eda-133">Once in hello portal for your app create a **Key** from hello **Settings** page for your application and copy it down.</span></span>  <span data-ttu-id="83eda-134">Lo necesitará en breve.</span><span class="sxs-lookup"><span data-stu-id="83eda-134">You will need it shortly.</span></span>

## <a name="2-set-up-your-app-toouse-adal4j-library-and-prerequisites-using-maven"></a><span data-ttu-id="83eda-135">2. Configurar la biblioteca de app toouse ADAL4J y requisitos previos mediante Maven</span><span class="sxs-lookup"><span data-stu-id="83eda-135">2. Set up your app toouse ADAL4J library and prerequisites using Maven</span></span>
<span data-ttu-id="83eda-136">En este caso, vamos a configurar el protocolo de autenticación OpenID Connect de ADAL4J toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="83eda-136">Here, we'll configure ADAL4J toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="83eda-137">ADAL4J ser tooissue usa las solicitudes de inicio de sesión y cierre de sesión, administrar la sesión del usuario de Hola y obtener información acerca del usuario de hello, entre otras cosas.</span><span class="sxs-lookup"><span data-stu-id="83eda-137">ADAL4J will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

* <span data-ttu-id="83eda-138">En el directorio raíz de hello del proyecto, abrir/crear `pom.xml` y busque hello `// TODO: provide dependencies for Maven` y reemplace con hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="83eda-138">In hello root directory of your project, open/create `pom.xml` and locate hello `// TODO: provide dependencies for Maven` and replace with hello following:</span></span>

```Java
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>public-client-adal4j-sample</artifactId>
    <packaging>jar</packaging>
    <version>0.0.1-SNAPSHOT</version>
    <name>public-client-adal4j-sample</name>
    <url>http://maven.apache.org</url>
    <properties>
        <spring.version>3.0.5.RELEASE</spring.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>adal4j</artifactId>
            <version>1.1.2</version>
        </dependency>
        <dependency>
            <groupId>com.nimbusds</groupId>
            <artifactId>oauth2-oidc-sdk</artifactId>
            <version>4.5</version>
        </dependency>
        <dependency>
            <groupId>org.json</groupId>
            <artifactId>json</artifactId>
            <version>20090211</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.0.1</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.7.5</version>
        </dependency>
</dependencies>
    <build>
        <finalName>public-client-adal4j-sample</finalName>
        <plugins>
                <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <version>1.2.1</version>
            <configuration>
                <mainClass>PublicClient</mainClass>
            </configuration>
        </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <executions>
                    <execution>
                        <id>install</id>
                        <phase>install</phase>
                        <goals>
                            <goal>sources</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</artifactId>
                <version>2.5</version>
                <configuration>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
        <artifactId>maven-assembly-plugin</artifactId>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>single</goal>
            </goals>
          </execution>
        </executions>
        <configuration>
          <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
          </descriptorRefs>
        </configuration>
      </plugin>
      <plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-assembly-plugin</artifactId>
  <configuration>
    <archive>
      <manifest>
        <mainClass>PublicClient</mainClass>
      </manifest>
    </archive>
  </configuration>
</plugin>
        </plugins>
    </build>

</project>


```



## <a name="3-create-hello-java-publicclient-file"></a><span data-ttu-id="83eda-139">3. Crear archivo de hello PublicClient de Java</span><span class="sxs-lookup"><span data-stu-id="83eda-139">3. Create hello Java PublicClient file</span></span>
<span data-ttu-id="83eda-140">Como se indicó anteriormente, vamos a usar Hola datos de API Graph tooget sobre Hola usuario registrado.</span><span class="sxs-lookup"><span data-stu-id="83eda-140">As indicated above, we will be using hello Graph API tooget data about hello logged in user.</span></span> <span data-ttu-id="83eda-141">Para este toobe fácil para que podamos debemos crear tanto un toorepresent archivo un **objeto de directorio** un hello toorepresent de archivo individuales y **usuario** para que hello orientado a objetos de Java puede utilizar el modelo.</span><span class="sxs-lookup"><span data-stu-id="83eda-141">For this toobe easy for us we should create both a file toorepresent a **Directory Object** and an individual file toorepresent hello **User** so that hello OO pattern of Java can be used.</span></span>

* <span data-ttu-id="83eda-142">Cree un archivo denominado `DirectoryObject.java` que usaremos toostore datos básicos sobre cualquier DirectoryObject (puede estar libre toouse esto más adelante para todas las consultas de gráfico se pueden hacer).</span><span class="sxs-lookup"><span data-stu-id="83eda-142">Create a file called `DirectoryObject.java` which we will use toostore basic data about any DirectoryObject (you can feel free toouse this later for any other Graph Queries you may do).</span></span> <span data-ttu-id="83eda-143">Puede cortar y pegar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="83eda-143">You can cut/paste this from below:</span></span>

```Java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

import javax.naming.ServiceUnavailableException;

import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;

public class PublicClient {

    private final static String AUTHORITY = "https://login.microsoftonline.com/common/";
    private final static String CLIENT_ID = "2a4da06c-ff07-410d-af8a-542a512f5092";

    public static void main(String args[]) throws Exception {

        try (BufferedReader br = new BufferedReader(new InputStreamReader(
                System.in))) {
            System.out.print("Enter username: ");
            String username = br.readLine();
            System.out.print("Enter password: ");
            String password = br.readLine();

            AuthenticationResult result = getAccessTokenFromUserCredentials(
                    username, password);
            System.out.println("Access Token - " + result.getAccessToken());
            System.out.println("Refresh Token - " + result.getRefreshToken());
            System.out.println("ID Token - " + result.getIdToken());
        }
    }

    private static AuthenticationResult getAccessTokenFromUserCredentials(
            String username, String password) throws Exception {
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(AUTHORITY, false, service);
            Future<AuthenticationResult> future = context.acquireToken(
                    "https://graph.windows.net", CLIENT_ID, username, password,
                    null);
            result = future.get();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;
    }
}


```


## <a name="compile-and-run-hello-sample"></a><span data-ttu-id="83eda-144">Compilar y ejecutar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="83eda-144">Compile and run hello sample</span></span>
<span data-ttu-id="83eda-145">Cambiar atrás en el directorio raíz de tooyour y ejecute hello según comando toobuild hello muestra simplemente ha colocado juntos mediante `maven`.</span><span class="sxs-lookup"><span data-stu-id="83eda-145">Change back out tooyour root directory and run hello following command toobuild hello sample you just put together using `maven`.</span></span> <span data-ttu-id="83eda-146">Se usarán hello `pom.xml` escribió para las dependencias de archivo.</span><span class="sxs-lookup"><span data-stu-id="83eda-146">This will use hello `pom.xml` file you wrote for dependencies.</span></span>

`$ mvn package`

<span data-ttu-id="83eda-147">Ahora debería tener un archivo `adal4jsample.war` en su directorio `/targets`.</span><span class="sxs-lookup"><span data-stu-id="83eda-147">You should now have a `adal4jsample.war` file in your `/targets` directory.</span></span> <span data-ttu-id="83eda-148">Puede implementar en el contenedor de Tomcat y visite la dirección URL de Hola</span><span class="sxs-lookup"><span data-stu-id="83eda-148">You may deploy that in your Tomcat container and visit hello URL</span></span> 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> <span data-ttu-id="83eda-149">Es muy fácil toodeploy una guerra con servidores Tomcat más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="83eda-149">It is very easy toodeploy a WAR with hello latest Tomcat servers.</span></span> <span data-ttu-id="83eda-150">Simplemente vaya demasiado`http://localhost:8080/manager/` y siga las instrucciones de hello acerca de cómo cargar su '' adal4jsample.war' archivo.</span><span class="sxs-lookup"><span data-stu-id="83eda-150">Simply navigate too`http://localhost:8080/manager/` and follow hello instructions on uploading your ``adal4jsample.war\` file.</span></span> <span data-ttu-id="83eda-151">Autodeploy lo hará automáticamente con el punto de conexión correcto Hola.</span><span class="sxs-lookup"><span data-stu-id="83eda-151">It will autodeploy for you with hello correct endpoint.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="83eda-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="83eda-152">Next Steps</span></span>
<span data-ttu-id="83eda-153">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="83eda-153">Congratulations!</span></span> <span data-ttu-id="83eda-154">Ahora tiene una aplicación Java que tiene Hola capacidad tooauthenticate usuarios y en funcionamiento, segura llamar a API Web mediante OAuth 2.0 y obtener información básica acerca del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="83eda-154">You now have a working Java application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="83eda-155">Si no lo ha hecho ya, ahora es Hola tiempo toopopulate el inquilino con algunos usuarios.</span><span class="sxs-lookup"><span data-stu-id="83eda-155">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>

<span data-ttu-id="83eda-156">Como referencia, Hola completado ejemplo (sin los valores de configuración) [se proporciona como .zip aquí](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), o se puede clonar desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="83eda-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

