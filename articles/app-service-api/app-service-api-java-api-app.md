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
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a><span data-ttu-id="49181-103">Compilación e implementación de una aplicación de API de Java en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="49181-103">Build and deploy a Java API app in Azure App Service</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="49181-104">Este tutorial se muestra cómo una aplicación Java toocreate e implementar aplicaciones de API de servicio tooAzure aplicación mediante [GIT].</span><span class="sxs-lookup"><span data-stu-id="49181-104">This tutorial shows how toocreate a Java application and deploy it tooAzure App Service API Apps using [Git].</span></span> <span data-ttu-id="49181-105">instrucciones de Hello en este tutorial se pueden aplicar en cualquier sistema operativo que sea capaz de ejecutar Java.</span><span class="sxs-lookup"><span data-stu-id="49181-105">hello instructions in this tutorial can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="49181-106">código de Hello en este tutorial se basa en [Maven].</span><span class="sxs-lookup"><span data-stu-id="49181-106">hello code in this tutorial is built using [Maven].</span></span> <span data-ttu-id="49181-107">[JAX RS] es toocreate usado hello servicio RESTful y se genera basándose en hello [Swagger] especificaciones de metadatos con hello [Swagger Editor].</span><span class="sxs-lookup"><span data-stu-id="49181-107">[Jax-RS] is used toocreate hello RESTful Service, and is generated based on hello [Swagger] metadata specification using hello [Swagger Editor].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49181-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="49181-108">Prerequisites</span></span>
1. <span data-ttu-id="49181-109">[Kit para desarrolladores de Java 8]\(o posterior)</span><span class="sxs-lookup"><span data-stu-id="49181-109">[Java Developer's Kit 8] \(or later)</span></span>
2. <span data-ttu-id="49181-110">[Maven] instalado en el equipo de desarrollo</span><span class="sxs-lookup"><span data-stu-id="49181-110">[Maven] installed on your development machine</span></span>
3. <span data-ttu-id="49181-111">[GIT] instalado en el equipo de desarrollo</span><span class="sxs-lookup"><span data-stu-id="49181-111">[Git] installed on your development machine</span></span>
4. <span data-ttu-id="49181-112">Un pago o [evaluación gratuita] suscripción demasiado[Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="49181-112">A paid or [free trial] subscription too[Microsoft Azure]</span></span>
5. <span data-ttu-id="49181-113">Una aplicación de prueba HTTP como [Postman]</span><span class="sxs-lookup"><span data-stu-id="49181-113">An HTTP test application like [Postman]</span></span>

## <a name="scaffold-hello-api-using-swaggerio"></a><span data-ttu-id="49181-114">API de hello scaffold usando Swagger.IO</span><span class="sxs-lookup"><span data-stu-id="49181-114">Scaffold hello API using Swagger.IO</span></span>
<span data-ttu-id="49181-115">Con editor de hello swagger.io en línea, puede escribir código de Swagger JSON o YAML que representa la estructura de saludo de la API.</span><span class="sxs-lookup"><span data-stu-id="49181-115">Using hello swagger.io online editor, you can enter Swagger JSON or YAML code representing hello structure of your API.</span></span> <span data-ttu-id="49181-116">Una vez que tenga el área expuesta en la API de hello diseñado, puede exportar el código para una amplia variedad de plataformas y marcos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="49181-116">Once you have hello API surface area designed, you can export code for a variety of platforms and frameworks.</span></span> <span data-ttu-id="49181-117">En la siguiente sección hello, código de hello scaffolding será funcionalidad ficticia tooinclude modificado.</span><span class="sxs-lookup"><span data-stu-id="49181-117">In hello next section, hello scaffolded code will be modified tooinclude mock functionality.</span></span> 

<span data-ttu-id="49181-118">En esta demostración se iniciará con un cuerpo JSON de Swagger que pegará en el editor de swagger.io hello, que, a continuación, usa toogenerate código estará uso de RS JAX tooaccess un punto de conexión de API de REST.</span><span class="sxs-lookup"><span data-stu-id="49181-118">This demonstration will begin with a Swagger JSON body that you will paste into hello swagger.io editor, which will then be used toogenerate code making use of JAX-RS tooaccess a REST API endpoint.</span></span> <span data-ttu-id="49181-119">A continuación, edite datos simulados de hello scaffolding código tooreturn, simulando una API de REST que se crea a partir de un mecanismo de persistencia de datos.</span><span class="sxs-lookup"><span data-stu-id="49181-119">Then, you'll edit hello scaffolded code tooreturn mock data, simulating a REST API built atop a data persistence mechanism.</span></span>  

1. <span data-ttu-id="49181-120">Copie Hola después de Portapapeles de Swagger JSON código tooyour:</span><span class="sxs-lookup"><span data-stu-id="49181-120">Copy hello following Swagger JSON code tooyour clipboard:</span></span>
   
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
2. <span data-ttu-id="49181-121">Navegue toohello [Editor en línea Swagger].</span><span class="sxs-lookup"><span data-stu-id="49181-121">Navigate toohello [Online Swagger Editor].</span></span> <span data-ttu-id="49181-122">Una vez allí, haga clic en hello **archivo -> Pegar JSON** elemento de menú.</span><span class="sxs-lookup"><span data-stu-id="49181-122">Once there, click hello **File -> Paste JSON** menu item.</span></span>
   
    ![Elemento de menú Pegar JSON][paste-json]
3. <span data-ttu-id="49181-124">Pegue en hello contactos lista API Swagger JSON que copió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="49181-124">Paste in hello Contacts List API Swagger JSON you copied earlier.</span></span> 
   
    ![Pegado de código JSON en Swagger][pasted-swagger]
4. <span data-ttu-id="49181-126">Ver las páginas de documentación de Hola y resumen de la API representados en el editor de Hola.</span><span class="sxs-lookup"><span data-stu-id="49181-126">View hello documentation pages and API summary rendered in hello editor.</span></span> 
   
    ![Ver documentos generados de Swagger][view-swagger-generated-docs]
5. <span data-ttu-id="49181-128">Seleccione hello **generar Server -> JAX RS** menú opción tooscaffold Hola código del lado servidor edite posterior implementación ficticia de tooadd.</span><span class="sxs-lookup"><span data-stu-id="49181-128">Select hello **Generate Server -> JAX-RS** menu option tooscaffold hello server-side code you'll edit later tooadd mock implementation.</span></span> 
   
    ![Generar elemento de menú de código][generate-code-menu-item]
   
    <span data-ttu-id="49181-130">Una vez que se genera código de hello, deberá proporcionar un toodownload de archivo ZIP.</span><span class="sxs-lookup"><span data-stu-id="49181-130">Once hello code is generated, you'll be provided a ZIP file toodownload.</span></span> <span data-ttu-id="49181-131">Este archivo contiene código de hello scaffolding generador de código de Swagger de Hola y todos los asociados generación scripts.</span><span class="sxs-lookup"><span data-stu-id="49181-131">This file contains hello code scaffolded by hello Swagger code generator and all associated build scripts.</span></span> <span data-ttu-id="49181-132">Descomprima el directorio de tooa toda la biblioteca de hello en la estación de trabajo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="49181-132">Unzip hello entire library tooa directory on your development workstation.</span></span> 

## <a name="edit-hello-code-tooadd-api-implementation"></a><span data-ttu-id="49181-133">Editar código de hello tooadd implementación de la API</span><span class="sxs-lookup"><span data-stu-id="49181-133">Edit hello Code tooadd API Implementation</span></span>
<span data-ttu-id="49181-134">En esta sección, reemplazará la implementación del hello Swagger código generado lado servidor con el código personalizado.</span><span class="sxs-lookup"><span data-stu-id="49181-134">In this section, you'll replace hello Swagger-generated code's server-side implementation with your custom code.</span></span> <span data-ttu-id="49181-135">nuevo código de Hello devolverá a un cliente que realiza la llamada de ArrayList de contacto entidades toohello.</span><span class="sxs-lookup"><span data-stu-id="49181-135">hello new code will return an ArrayList of Contact entities toohello calling client.</span></span> 

1. <span data-ttu-id="49181-136">Hola abierto *Contact.java* archivo de modelo, que se encuentra en hello *src/gen/java/e/s/swagger/modelo* carpeta, con [código de Visual Studio] o su editor de texto que prefiera.</span><span class="sxs-lookup"><span data-stu-id="49181-136">Open hello *Contact.java* model file, which is located in hello *src/gen/java/io/swagger/model* folder, using [Visual Studio Code] or your favorite text editor.</span></span> 
   
    ![Abrir archivo de modelo de contacto][open-contact-model-file]
2. <span data-ttu-id="49181-138">Agregar Hola después constructor dentro de hello **póngase en contacto con** clase.</span><span class="sxs-lookup"><span data-stu-id="49181-138">Add hello following constructor within hello **Contact** class.</span></span> 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. <span data-ttu-id="49181-139">Hola abierto *ContactsApiServiceImpl.java* archivo de implementación de servicio, que se encuentra en hello *src/principal/java/e/s/swagger/api/impl* carpeta, con [código de Visual Studio]o su editor de texto que prefiera.</span><span class="sxs-lookup"><span data-stu-id="49181-139">Open hello *ContactsApiServiceImpl.java* service implementation file, which is located in hello *src/main/java/io/swagger/api/impl* folder, using [Visual Studio Code] or your favorite text editor.</span></span>
   
    ![Abrir archivo de código de servicio de contacto][open-contact-service-code-file]
4. <span data-ttu-id="49181-141">Sobrescribir el código de hello en el archivo hello con esta nueva tooadd de código un código de servicio de implementación ficticia toohello.</span><span class="sxs-lookup"><span data-stu-id="49181-141">Overwrite hello code in hello file with this new code tooadd a mock implementation toohello service code.</span></span> 
   
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
5. <span data-ttu-id="49181-142">Abra un símbolo del sistema y cambie la carpeta de raíz de toohello del directorio de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="49181-142">Open a command prompt and change directory toohello root folder of your application.</span></span>
6. <span data-ttu-id="49181-143">Ejecute hello sigue Maven comando toobuild Hola código y ejecutarlo mediante el servidor de aplicaciones de Jetty Hola localmente.</span><span class="sxs-lookup"><span data-stu-id="49181-143">Execute hello following Maven command toobuild hello code and run it using hello Jetty app server locally.</span></span> 
   
        mvn package jetty:run
7. <span data-ttu-id="49181-144">Debería ver la ventana de comandos de hello reflejar que Jetty ha iniciado el código en el puerto 8080.</span><span class="sxs-lookup"><span data-stu-id="49181-144">You should see hello command window reflect that Jetty has started your code on port 8080.</span></span> 
   
    ![Abrir archivo de código de servicio de contacto][run-jetty-war]
8. <span data-ttu-id="49181-146">Use [Postman] método toomake una API de solicitud toohello "obtener todos los contactos" en http://localhost: 8080/api/contactos.</span><span class="sxs-lookup"><span data-stu-id="49181-146">Use [Postman] toomake a request toohello "get all contacts" API method at http://localhost:8080/api/contacts.</span></span>
   
    ![Hola llamada API de contactos][calling-contacts-api]
9. <span data-ttu-id="49181-148">Use [Postman] toomake una API de "obtener un contacto específico" de solicitud toohello método ubicado en http://localhost: 8080/api/contactos/2.</span><span class="sxs-lookup"><span data-stu-id="49181-148">Use [Postman] toomake a request toohello "get specific contact" API method located at http://localhost:8080/api/contacts/2.</span></span>
   
    ![Hola llamada API de contactos][calling-specific-contact-api]
10. <span data-ttu-id="49181-150">Por último, crear archivo WAR de Java (archivo Web) de hello ejecutando Hola siguiente comando de Maven en la consola.</span><span class="sxs-lookup"><span data-stu-id="49181-150">Finally, build hello Java WAR (Web ARchive) file by executing hello following Maven command in your console.</span></span> 
    
         mvn package war:war
11. <span data-ttu-id="49181-151">Una vez que se compila el archivo WAR de hello, se colocarán en hello **destino** carpeta.</span><span class="sxs-lookup"><span data-stu-id="49181-151">Once hello WAR file is built, it will be placed into hello **target** folder.</span></span> <span data-ttu-id="49181-152">Suba hello **destino** carpeta y cambie el nombre Hola archivo WAR demasiado**ROOT.war**.</span><span class="sxs-lookup"><span data-stu-id="49181-152">Navigate into hello **target** folder and rename hello WAR file too**ROOT.war**.</span></span> <span data-ttu-id="49181-153">(Asegúrese de que el uso de mayúsculas de hello coincide con este formato).</span><span class="sxs-lookup"><span data-stu-id="49181-153">(Make sure hello capitalization matches this format).</span></span>
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. <span data-ttu-id="49181-154">Por último, ejecute los siguientes comandos de la carpeta raíz de hello de la aplicación toocreate de Hola un **implementar** toodeploy Hola WAR de carpeta toouse tooAzure de archivos.</span><span class="sxs-lookup"><span data-stu-id="49181-154">Finally, execute hello following commands from hello root folder of your application toocreate a **deploy** folder toouse toodeploy hello WAR file tooAzure.</span></span> 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a><span data-ttu-id="49181-155">Publicar Hola salida tooAzure servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="49181-155">Publish hello output tooAzure App Service</span></span>
<span data-ttu-id="49181-156">En esta sección que aprenderá cómo toocreate una App API nueva con hello Portal de Azure, preparar esa API App para hospedar aplicaciones de Java e implementar Hola recién creado WAR archivo tooAzure toorun de servicio de aplicaciones su App API nueva.</span><span class="sxs-lookup"><span data-stu-id="49181-156">In this section you'll learn how toocreate a new API App using hello Azure Portal, prepare that API App for hosting Java applications, and deploy hello newly-created WAR file tooAzure App Service toorun your new API App.</span></span> 

1. <span data-ttu-id="49181-157">Crear una nueva aplicación de API en hello [portal de Azure], haciendo clic en hello **nuevo -> Web + Mobile -> aplicación de API** elemento de menú, introduzca los detalles de la aplicación y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="49181-157">Create a new API app in hello [Azure portal], by clicking hello **New -> Web + Mobile -> API app** menu item, entering your app details, and then clicking **Create**.</span></span>
   
    ![Crear una nueva aplicación de API][create-api-app]
2. <span data-ttu-id="49181-159">Una vez creada la aplicación de API, abra la aplicación **configuración** hoja y, a continuación, haga clic en hello **configuración de la aplicación** elemento de menú.</span><span class="sxs-lookup"><span data-stu-id="49181-159">Once your API app has been created, open your app's **Settings** blade, and then click hello **Application settings** menu item.</span></span> <span data-ttu-id="49181-160">Seleccione Hola últimas versiones de Java de opciones disponibles de hello, a continuación, seleccione Hola Tomcat más reciente de hello **contenedor Web** menú y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="49181-160">Select hello latest Java versions from hello available options, then select hello latest Tomcat from hello **Web container** menu, and then click **Save**.</span></span>
   
    ![Configurar Java Hola hoja API App][set-up-java]
3. <span data-ttu-id="49181-162">Haga clic en hello **las credenciales de implementación** menú de configuración de elemento y proporcione un nombre de usuario y una contraseña que se va toouse para publicar archivos tooyour API App.</span><span class="sxs-lookup"><span data-stu-id="49181-162">Click hello **Deployment credentials** settings menu item, and provide a username and password you wish toouse for publishing files tooyour API App.</span></span> 
   
    ![Configurar credenciales de implementación][deployment-credentials]
4. <span data-ttu-id="49181-164">Haga clic en hello **origen de la implementación** elemento de menú de configuración.</span><span class="sxs-lookup"><span data-stu-id="49181-164">Click hello **Deployment source** settings menu item.</span></span> <span data-ttu-id="49181-165">Una vez allí, haga clic en hello **Elegir origen** button, seleccione hello **repositorio de Git Local** opción y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="49181-165">Once there, click hello **Choose source** button, select hello **Local Git Repository** option, and then click **OK**.</span></span> <span data-ttu-id="49181-166">Se crea un repositorio de Git que se ejecuta en Azure, que tiene una asociación con la aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="49181-166">This will create a Git repository running in Azure, that has an association with your API App.</span></span> <span data-ttu-id="49181-167">Cada vez que se confirma código toohello *maestro* rama del repositorio Git, el código se publicará en la instancia API App en ejecución en vivo.</span><span class="sxs-lookup"><span data-stu-id="49181-167">Each time you commit code toohello *master* branch of your Git repository, your code will be published into your live running API App instance.</span></span> 
   
    ![Configurar un nuevo repositorio de Git local][select-git-repo]
5. <span data-ttu-id="49181-169">Copie tooyour Portapapeles de hello nuevo repositorio Git dirección URL.</span><span class="sxs-lookup"><span data-stu-id="49181-169">Copy hello new Git repository's URL tooyour clipboard.</span></span> <span data-ttu-id="49181-170">Guárdela, será importante dentro de poco.</span><span class="sxs-lookup"><span data-stu-id="49181-170">Save this as it will be important in a moment.</span></span> 
   
    ![Configurar un nuevo repositorio de Git para la aplicación][copy-git-repo-url]
6. <span data-ttu-id="49181-172">Inserción Hola WAR archivo toohello online repositorio de GIT.</span><span class="sxs-lookup"><span data-stu-id="49181-172">Git push hello WAR file toohello online repository.</span></span> <span data-ttu-id="49181-173">toodo, suba hello **implementar** carpeta que creó anteriormente para que fácilmente puede confirmar código de hello arriba repositorio de toohello que se ejecutan en el servicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="49181-173">toodo this, navigate into hello **deploy** folder you created earlier so that you can easily commit hello code up toohello repository running in your App Service.</span></span> <span data-ttu-id="49181-174">Una vez está en la ventana de la consola de Hola y navega en carpeta Hola donde se encuentra, carpeta de aplicaciones Web de hello emitir Hola siguiendo Git comandos toolaunch Hola proceso y lanzar una implementación.</span><span class="sxs-lookup"><span data-stu-id="49181-174">Once you're in hello console window and navigated into hello folder where hello webapps folder is located, issue hello following Git commands toolaunch hello process and fire off a deployment.</span></span> 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    <span data-ttu-id="49181-175">Una vez que se emite hello **inserción** solicitud, se le preguntará para contraseña de Hola que creó anteriormente para las credenciales de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="49181-175">Once you issue hello **push** request, you'll be asked for hello password you created for hello deployment credential earlier.</span></span> <span data-ttu-id="49181-176">Después de escribir sus credenciales, debería ver la pantalla de portal que Hola actualización se implementó.</span><span class="sxs-lookup"><span data-stu-id="49181-176">After you enter your credentials, you should see your portal display that hello update was deployed.</span></span>
7. <span data-ttu-id="49181-177">Si usa una vez más Postman toohit Hola había implementado recién App API ejecutando en el servicio de aplicación de Azure, verá que el comportamiento de hello es coherente y que ahora está devolviendo datos de contacto según lo previsto y utilizando un código sencillo cambios toohello Swagger.io scaffolding código Java.</span><span class="sxs-lookup"><span data-stu-id="49181-177">If you once again use Postman toohit hello newly-deployed API App running in Azure App Service, you'll see that hello behavior is consistent and that now it is returning contact data as expected, and using simple code changes toohello Swagger.io scaffolded Java code.</span></span> 
   
    ![Uso de la API de REST de contactos de Java activa en Azure][postman-calling-azure-contacts]

## <a name="next-steps"></a><span data-ttu-id="49181-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="49181-179">Next steps</span></span>
<span data-ttu-id="49181-180">En este artículo, eran capaz de toostart con un archivo Swagger JSON y algún código de Java con scaffolding obtenido desde el editor de Swagger.io Hola.</span><span class="sxs-lookup"><span data-stu-id="49181-180">In this article, you were able toostart with a Swagger JSON file and some scaffolded Java code obtained from hello Swagger.io editor.</span></span> <span data-ttu-id="49181-181">A partir de ahí, algunos sencillos cambios y un proceso de implementación de Git han dado lugar a que tengamos una aplicación de API funcional escrita en Java.</span><span class="sxs-lookup"><span data-stu-id="49181-181">From there, your simple changes and a Git deploy process resulted in having a functional API app written in Java.</span></span> <span data-ttu-id="49181-182">tutorial de Hello siguiente muestra cómo demasiado[utilicen las aplicaciones de API de los clientes de JavaScript, mediante CORS][App Service API CORS].</span><span class="sxs-lookup"><span data-stu-id="49181-182">hello next tutorial shows how too[consume API apps from JavaScript clients, using CORS][App Service API CORS].</span></span> <span data-ttu-id="49181-183">Los tutoriales posteriores en Hola serie mostrar cómo tooimplement autenticación y autorización.</span><span class="sxs-lookup"><span data-stu-id="49181-183">Later tutorials in hello series show how tooimplement authentication and authorization.</span></span>

<span data-ttu-id="49181-184">toobuild en este ejemplo, se puede obtener más información acerca de hello [Storage SDK para Java] blobs de toopersist Hola JSON.</span><span class="sxs-lookup"><span data-stu-id="49181-184">toobuild on this sample, you can learn more about hello [Storage SDK for Java] toopersist hello JSON blobs.</span></span> <span data-ttu-id="49181-185">O bien, puede usar hello [SDK de Java de base de datos de documentos] toosave su tooAzure de datos de contacto base de datos del documento.</span><span class="sxs-lookup"><span data-stu-id="49181-185">Or, you could use hello [Document DB Java SDK] toosave your Contact data tooAzure Document DB.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="49181-186">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="49181-186">See Also</span></span>
<span data-ttu-id="49181-187">Para más información sobre el uso de Azure con Java, visite [Azure para desarrolladores de Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="49181-187">For more information about using Azure with Java, visit [Azure for Java developers](/java/azure).</span></span>

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
