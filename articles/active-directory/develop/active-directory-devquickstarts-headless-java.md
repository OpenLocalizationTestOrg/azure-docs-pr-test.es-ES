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
# <a name="using-java-command-line-app-tooaccess-an-api-with-azure-ad"></a>Uso de aplicaciones de línea de comandos de Java tooAccess una API con Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure AD facilita toooutsource simple y sencilla administración de identidad de su aplicación web, que proporciona un único inicio de sesión y cierre de sesión con unas pocas líneas de código.  En aplicaciones web de Java, puede hacerlo mediante la implementación de Microsoft de hello ADAL4J controlada por la Comunidad.

  Aquí, usaremos ADAL4J para:

* Usuario de Hola de inicio de sesión en la aplicación hello mediante Azure AD como proveedor de identidades de Hola.
* Mostrar información acerca del usuario de Hola.
* Inicio de sesión Hola usuario fuera de la aplicación hello.

En Ordenar toodo esto, necesitará:

1. Registro de una aplicación con Azure AD
2. Configurar la biblioteca de ADAL4J aplicación toouse Hola.
3. Utilice hello ADAL4J biblioteca tooissue sesión y las solicitudes de cierre de sesión tooAzure AD.
4. Imprimir datos acerca del usuario de Hola.

tooget iniciado, [descargar esqueleto de aplicación Hola](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) o [Descargar ejemplo Hola completado](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).  También necesitará a un inquilino de Azure AD en qué tooregister la aplicación.  Si aún no tiene uno, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).

## <a name="1--register-an-application-with-azure-ad"></a>1.  Registro de una aplicación con Azure AD
tooenable los usuarios de tooauthenticate aplicación, primero deberá tooregister una nueva aplicación en su inquilino.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En la barra superior de hello, haga clic en su cuenta y en hello **Directory** lista, elija el inquilino de Active Directory de Hola que le gustaría tooregister la aplicación.
3. Haga clic en **más servicios** en Hola nav izquierda y elija **Azure Active Directory**.
4. Haga clic en **Registros de aplicaciones** y elija **Agregar**.
5. Siga las indicaciones de Hola y crear un nuevo **aplicación Web o WebAPI**.
  * Hola **nombre** de hello aplicación describirá los tooend-usuarios de la aplicación
  * Hola **dirección URL de inicio de sesión** es Hola dirección URL base de la aplicación.  valor predeterminado del esqueleto Hello es `http://localhost:8080/adal4jsample/`.
6. Una vez que haya completado el registro, AAD asignará a su aplicación un identificador de aplicación único.  Necesitará este valor en las secciones siguientes de hello, por lo tanto cópiela desde la pestaña de la aplicación hello.
7. De hello **configuración** -> **propiedades** página de la aplicación, actualice Hola App ID URI. Hola **App ID URI** es un identificador único para la aplicación.  convención de Hello es toouse `https://<tenant-domain>/<app-name>`, por ejemplo, `http://localhost:8080/adal4jsample/`.

Una vez en el portal de hello para la aplicación cree un **clave** de hello **configuración** página de la aplicación y cópiela.  Lo necesitará en breve.

## <a name="2-set-up-your-app-toouse-adal4j-library-and-prerequisites-using-maven"></a>2. Configurar la biblioteca de app toouse ADAL4J y requisitos previos mediante Maven
En este caso, vamos a configurar el protocolo de autenticación OpenID Connect de ADAL4J toouse Hola.  ADAL4J ser tooissue usa las solicitudes de inicio de sesión y cierre de sesión, administrar la sesión del usuario de Hola y obtener información acerca del usuario de hello, entre otras cosas.

* En el directorio raíz de hello del proyecto, abrir/crear `pom.xml` y busque hello `// TODO: provide dependencies for Maven` y reemplace con hello siguiente:

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



## <a name="3-create-hello-java-publicclient-file"></a>3. Crear archivo de hello PublicClient de Java
Como se indicó anteriormente, vamos a usar Hola datos de API Graph tooget sobre Hola usuario registrado. Para este toobe fácil para que podamos debemos crear tanto un toorepresent archivo un **objeto de directorio** un hello toorepresent de archivo individuales y **usuario** para que hello orientado a objetos de Java puede utilizar el modelo.

* Cree un archivo denominado `DirectoryObject.java` que usaremos toostore datos básicos sobre cualquier DirectoryObject (puede estar libre toouse esto más adelante para todas las consultas de gráfico se pueden hacer). Puede cortar y pegar lo siguiente:

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


## <a name="compile-and-run-hello-sample"></a>Compilar y ejecutar el ejemplo hello
Cambiar atrás en el directorio raíz de tooyour y ejecute hello según comando toobuild hello muestra simplemente ha colocado juntos mediante `maven`. Se usarán hello `pom.xml` escribió para las dependencias de archivo.

`$ mvn package`

Ahora debería tener un archivo `adal4jsample.war` en su directorio `/targets`. Puede implementar en el contenedor de Tomcat y visite la dirección URL de Hola 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> Es muy fácil toodeploy una guerra con servidores Tomcat más recientes de Hola. Simplemente vaya demasiado`http://localhost:8080/manager/` y siga las instrucciones de hello acerca de cómo cargar su '' adal4jsample.war' archivo. Autodeploy lo hará automáticamente con el punto de conexión correcto Hola.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
¡Enhorabuena! Ahora tiene una aplicación Java que tiene Hola capacidad tooauthenticate usuarios y en funcionamiento, segura llamar a API Web mediante OAuth 2.0 y obtener información básica acerca del usuario de Hola.  Si no lo ha hecho ya, ahora es Hola tiempo toopopulate el inquilino con algunos usuarios.

Como referencia, Hola completado ejemplo (sin los valores de configuración) [se proporciona como .zip aquí](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), o se puede clonar desde GitHub:

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

