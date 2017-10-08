---
title: "aaaBuild e implementar una aplicación de API de Java en el servicio de aplicación de Azure"
description: "Obtenga información acerca de cómo una aplicación de API de Java toocreate empaquetar e implementar tooAzure servicio de aplicaciones."
services: app-service\api
documentationcenter: java
author: rmcmurray
manager: erikre
editor: tdykstra
ms.assetid: 8d21ba5f-fc57-4269-bc8f-2fcab936ec22
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: get-started-article
ms.date: 04/25/2017
ms.author: rachelap;robmcm
ms.openlocfilehash: a4056fec870b1c4bed8ee14bb0e748b3ee89b9e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a>Compilación e implementación de una aplicación de API de Java en el Servicio de aplicaciones de Azure
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

Este tutorial se muestra cómo una aplicación Java toocreate e implementar aplicaciones de API de servicio tooAzure aplicación mediante [GIT]. instrucciones de Hello en este tutorial se pueden aplicar en cualquier sistema operativo que sea capaz de ejecutar Java. código de Hello en este tutorial se basa en [Maven]. [JAX RS] es toocreate usado hello servicio RESTful y se genera basándose en hello [Swagger] especificaciones de metadatos con hello [Swagger Editor].

## <a name="prerequisites"></a>Requisitos previos
1. [Kit para desarrolladores de Java 8]\(o posterior)
2. [Maven] instalado en el equipo de desarrollo
3. [GIT] instalado en el equipo de desarrollo
4. Un pago o [evaluación gratuita] suscripción demasiado[Microsoft Azure]
5. Una aplicación de prueba HTTP como [Postman]

## <a name="scaffold-hello-api-using-swaggerio"></a>API de hello scaffold usando Swagger.IO
Con editor de hello swagger.io en línea, puede escribir código de Swagger JSON o YAML que representa la estructura de saludo de la API. Una vez que tenga el área expuesta en la API de hello diseñado, puede exportar el código para una amplia variedad de plataformas y marcos de trabajo. En la siguiente sección hello, código de hello scaffolding será funcionalidad ficticia tooinclude modificado. 

En esta demostración se iniciará con un cuerpo JSON de Swagger que pegará en el editor de swagger.io hello, que, a continuación, usa toogenerate código estará uso de RS JAX tooaccess un punto de conexión de API de REST. A continuación, edite datos simulados de hello scaffolding código tooreturn, simulando una API de REST que se crea a partir de un mecanismo de persistencia de datos.  

1. Copie Hola después de Portapapeles de Swagger JSON código tooyour:
   
        {
            "swagger": "2.0",
            "info": {
                "version": "v1",
                "title": "Contact List",
                "description": "A Contact list API based on Swagger and built using Java"
            },
            "host": "localhost",
            "schemes": [
                "http",
                "https"
            ],
            "basePath": "/api",
            "paths": {
                "/contacts": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_get",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                },
                "/contacts/{id}": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_getById",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "parameters": [
                            {
                                "name": "id",
                                "in": "path",
                                "required": true,
                                "type": "integer",
                                "format": "int32"
                            }
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                }
            },
            "definitions": {
                "Contact": {
                    "type": "object",
                    "properties": {
                        "Id": {
                            "format": "int32",
                            "type": "integer"
                        },
                        "Name": {
                            "type": "string"
                        },
                        "EmailAddress": {
                            "type": "string"
                        }
                    }
                }
            }
        }
2. Navegue toohello [Editor en línea Swagger]. Una vez allí, haga clic en hello **archivo -> Pegar JSON** elemento de menú.
   
    ![Elemento de menú Pegar JSON][paste-json]
3. Pegue en hello contactos lista API Swagger JSON que copió anteriormente. 
   
    ![Pegado de código JSON en Swagger][pasted-swagger]
4. Ver las páginas de documentación de Hola y resumen de la API representados en el editor de Hola. 
   
    ![Ver documentos generados de Swagger][view-swagger-generated-docs]
5. Seleccione hello **generar Server -> JAX RS** menú opción tooscaffold Hola código del lado servidor edite posterior implementación ficticia de tooadd. 
   
    ![Generar elemento de menú de código][generate-code-menu-item]
   
    Una vez que se genera código de hello, deberá proporcionar un toodownload de archivo ZIP. Este archivo contiene código de hello scaffolding generador de código de Swagger de Hola y todos los asociados generación scripts. Descomprima el directorio de tooa toda la biblioteca de hello en la estación de trabajo de desarrollo. 

## <a name="edit-hello-code-tooadd-api-implementation"></a>Editar código de hello tooadd implementación de la API
En esta sección, reemplazará la implementación del hello Swagger código generado lado servidor con el código personalizado. nuevo código de Hello devolverá a un cliente que realiza la llamada de ArrayList de contacto entidades toohello. 

1. Hola abierto *Contact.java* archivo de modelo, que se encuentra en hello *src/gen/java/e/s/swagger/modelo* carpeta, con [código de Visual Studio] o su editor de texto que prefiera. 
   
    ![Abrir archivo de modelo de contacto][open-contact-model-file]
2. Agregar Hola después constructor dentro de hello **póngase en contacto con** clase. 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. Hola abierto *ContactsApiServiceImpl.java* archivo de implementación de servicio, que se encuentra en hello *src/principal/java/e/s/swagger/api/impl* carpeta, con [código de Visual Studio]o su editor de texto que prefiera.
   
    ![Abrir archivo de código de servicio de contacto][open-contact-service-code-file]
4. Sobrescribir el código de hello en el archivo hello con esta nueva tooadd de código un código de servicio de implementación ficticia toohello. 
   
        package io.swagger.api.impl;
   
        import io.swagger.api.*;
        
        import io.swagger.model.Contact;
        import java.util.*;
        import io.swagger.api.NotFoundException;
               
        import javax.ws.rs.core.Response;
        import javax.ws.rs.core.SecurityContext;
   
        @javax.annotation.Generated(value = "class io.swagger.codegen.languages.JaxRSServerCodegen", date = "2015-11-24T21:54:11.648Z")
        public class ContactsApiServiceImpl extends ContactsApiService {
   
            private ArrayList<Contact> loadContacts()
            {
                ArrayList<Contact> list = new ArrayList<Contact>();
                list.add(new Contact(1, "Barney Poland", "barney@contoso.com"));
                list.add(new Contact(2, "Lacy Barrera", "lacy@contoso.com"));
                list.add(new Contact(3, "Lora Riggs", "lora@contoso.com"));
                return list;
            }
   
            @Override
            public Response contactsGet(SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                return Response.ok().entity(list).build();
                }
   
            @Override
            public Response contactsGetById(Integer id, SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                Contact ret = null;
   
                for(int i=0; i<list.size(); i++)
                {
                    if(list.get(i).getId() == id)
                        {
                            ret = list.get(i);
                        }
                }
                return Response.ok().entity(ret).build();
            }
        }
5. Abra un símbolo del sistema y cambie la carpeta de raíz de toohello del directorio de la aplicación.
6. Ejecute hello sigue Maven comando toobuild Hola código y ejecutarlo mediante el servidor de aplicaciones de Jetty Hola localmente. 
   
        mvn package jetty:run
7. Debería ver la ventana de comandos de hello reflejar que Jetty ha iniciado el código en el puerto 8080. 
   
    ![Abrir archivo de código de servicio de contacto][run-jetty-war]
8. Use [Postman] método toomake una API de solicitud toohello "obtener todos los contactos" en http://localhost: 8080/api/contactos.
   
    ![Hola llamada API de contactos][calling-contacts-api]
9. Use [Postman] toomake una API de "obtener un contacto específico" de solicitud toohello método ubicado en http://localhost: 8080/api/contactos/2.
   
    ![Hola llamada API de contactos][calling-specific-contact-api]
10. Por último, crear archivo WAR de Java (archivo Web) de hello ejecutando Hola siguiente comando de Maven en la consola. 
    
         mvn package war:war
11. Una vez que se compila el archivo WAR de hello, se colocarán en hello **destino** carpeta. Suba hello **destino** carpeta y cambie el nombre Hola archivo WAR demasiado**ROOT.war**. (Asegúrese de que el uso de mayúsculas de hello coincide con este formato).
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. Por último, ejecute los siguientes comandos de la carpeta raíz de hello de la aplicación toocreate de Hola un **implementar** toodeploy Hola WAR de carpeta toouse tooAzure de archivos. 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a>Publicar Hola salida tooAzure servicio de aplicaciones
En esta sección que aprenderá cómo toocreate una App API nueva con hello Portal de Azure, preparar esa API App para hospedar aplicaciones de Java e implementar Hola recién creado WAR archivo tooAzure toorun de servicio de aplicaciones su App API nueva. 

1. Crear una nueva aplicación de API en hello [portal de Azure], haciendo clic en hello **nuevo -> Web + Mobile -> aplicación de API** elemento de menú, introduzca los detalles de la aplicación y, a continuación, haga clic en **crear**.
   
    ![Crear una nueva aplicación de API][create-api-app]
2. Una vez creada la aplicación de API, abra la aplicación **configuración** hoja y, a continuación, haga clic en hello **configuración de la aplicación** elemento de menú. Seleccione Hola últimas versiones de Java de opciones disponibles de hello, a continuación, seleccione Hola Tomcat más reciente de hello **contenedor Web** menú y, a continuación, haga clic en **guardar**.
   
    ![Configurar Java Hola hoja API App][set-up-java]
3. Haga clic en hello **las credenciales de implementación** menú de configuración de elemento y proporcione un nombre de usuario y una contraseña que se va toouse para publicar archivos tooyour API App. 
   
    ![Configurar credenciales de implementación][deployment-credentials]
4. Haga clic en hello **origen de la implementación** elemento de menú de configuración. Una vez allí, haga clic en hello **Elegir origen** button, seleccione hello **repositorio de Git Local** opción y, a continuación, haga clic en **Aceptar**. Se crea un repositorio de Git que se ejecuta en Azure, que tiene una asociación con la aplicación de API. Cada vez que se confirma código toohello *maestro* rama del repositorio Git, el código se publicará en la instancia API App en ejecución en vivo. 
   
    ![Configurar un nuevo repositorio de Git local][select-git-repo]
5. Copie tooyour Portapapeles de hello nuevo repositorio Git dirección URL. Guárdela, será importante dentro de poco. 
   
    ![Configurar un nuevo repositorio de Git para la aplicación][copy-git-repo-url]
6. Inserción Hola WAR archivo toohello online repositorio de GIT. toodo, suba hello **implementar** carpeta que creó anteriormente para que fácilmente puede confirmar código de hello arriba repositorio de toohello que se ejecutan en el servicio de aplicación. Una vez está en la ventana de la consola de Hola y navega en carpeta Hola donde se encuentra, carpeta de aplicaciones Web de hello emitir Hola siguiendo Git comandos toolaunch Hola proceso y lanzar una implementación. 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    Una vez que se emite hello **inserción** solicitud, se le preguntará para contraseña de Hola que creó anteriormente para las credenciales de implementación de Hola. Después de escribir sus credenciales, debería ver la pantalla de portal que Hola actualización se implementó.
7. Si usa una vez más Postman toohit Hola había implementado recién App API ejecutando en el servicio de aplicación de Azure, verá que el comportamiento de hello es coherente y que ahora está devolviendo datos de contacto según lo previsto y utilizando un código sencillo cambios toohello Swagger.io scaffolding código Java. 
   
    ![Uso de la API de REST de contactos de Java activa en Azure][postman-calling-azure-contacts]

## <a name="next-steps"></a>Pasos siguientes
En este artículo, eran capaz de toostart con un archivo Swagger JSON y algún código de Java con scaffolding obtenido desde el editor de Swagger.io Hola. A partir de ahí, algunos sencillos cambios y un proceso de implementación de Git han dado lugar a que tengamos una aplicación de API funcional escrita en Java. tutorial de Hello siguiente muestra cómo demasiado[utilicen las aplicaciones de API de los clientes de JavaScript, mediante CORS][App Service API CORS]. Los tutoriales posteriores en Hola serie mostrar cómo tooimplement autenticación y autorización.

toobuild en este ejemplo, se puede obtener más información acerca de hello [Storage SDK para Java] blobs de toopersist Hola JSON. O bien, puede usar hello [SDK de Java de base de datos de documentos] toosave su tooAzure de datos de contacto base de datos del documento. 

<a name="see-also"></a>

## <a name="see-also"></a>Otras referencias
Para más información sobre el uso de Azure con Java, visite [Azure para desarrolladores de Java](/java/azure).

<!-- URL List -->

[App Service API CORS]: app-service-api-cors-consume-javascript.md
[portal de Azure]: https://portal.azure.com/
[SDK de Java de base de datos de documentos]: ../documentdb/documentdb-java-application.md
[evaluación gratuita]: https://azure.microsoft.com/pricing/free-trial/
[GIT]: http://www.git-scm.com/
[Azure Java Developer Center]: /develop/java/
[Kit para desarrolladores de Java 8]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[JAX RS]: https://jax-rs-spec.java.net/
[Maven]: https://maven.apache.org/
[Microsoft Azure]: https://azure.microsoft.com/
[Editor en línea Swagger]: http://editor2.swagger.io/
[Postman]: https://www.getpostman.com/
[Storage SDK para Java]:../storage/blobs/storage-java-how-to-use-blob-storage.md
[Swagger]: http://swagger.io/
[Swagger Editor]: http://editor.swagger.io/
[código de Visual Studio]: https://code.visualstudio.com

<!-- IMG List -->

[paste-json]: ./media/app-service-api-java-api-app/paste-json.png
[pasted-swagger]: ./media/app-service-api-java-api-app/pasted-swagger.png
[view-swagger-generated-docs]: ./media/app-service-api-java-api-app/view-swagger-generated-docs.png
[generate-code-menu-item]: ./media/app-service-api-java-api-app/generate-code-menu-item.png
[open-contact-model-file]: ./media/app-service-api-java-api-app/open-contact-model-file.png
[open-contact-service-code-file]: ./media/app-service-api-java-api-app/open-contact-service-code-file.png
[run-jetty-war]: ./media/app-service-api-java-api-app/run-jetty-war.png
[calling-contacts-api]: ./media/app-service-api-java-api-app/calling-contacts-api.png
[calling-specific-contact-api]: ./media/app-service-api-java-api-app/calling-specific-contact-api.png
[create-api-app]: ./media/app-service-api-java-api-app/create-api-app.png
[set-up-java]: ./media/app-service-api-java-api-app/set-up-java.png
[deployment-credentials]: ./media/app-service-api-java-api-app/deployment-credentials.png
[select-git-repo]: ./media/app-service-api-java-api-app/select-git-repo.png
[copy-git-repo-url]: ./media/app-service-api-java-api-app/copy-git-repo-url.png
[postman-calling-azure-contacts]: ./media/app-service-api-java-api-app/postman-calling-azure-contacts.png
