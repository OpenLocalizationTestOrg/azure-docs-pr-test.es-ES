---
title: "Compilación e implementación de una aplicación de API de Java en el Servicio de aplicaciones de Azure"
description: "Aprenda a crear un paquete de aplicación de API de Java y a implementarlo en el Servicio de aplicaciones de Azure."
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
ms.openlocfilehash: e38c540071cb49b0177e79178566d72ecb5f8886
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a><span data-ttu-id="27943-103">Compilación e implementación de una aplicación de API de Java en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="27943-103">Build and deploy a Java API app in Azure App Service</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="27943-104">En este tutorial se muestra cómo crear una aplicación de Java e implementarla en las aplicaciones de API del Servicio de aplicaciones de Azure mediante [Git].</span><span class="sxs-lookup"><span data-stu-id="27943-104">This tutorial shows how to create a Java application and deploy it to Azure App Service API Apps using [Git].</span></span> <span data-ttu-id="27943-105">Las instrucciones que se indican en este tutorial se pueden seguir en cualquier sistema operativo que sea capaz de ejecutar Java.</span><span class="sxs-lookup"><span data-stu-id="27943-105">The instructions in this tutorial can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="27943-106">El código de este tutorial está compilado mediante [Maven].</span><span class="sxs-lookup"><span data-stu-id="27943-106">The code in this tutorial is built using [Maven].</span></span> <span data-ttu-id="27943-107">[Jax-RS] se utiliza para crear el servicio RESTful y se genera a partir de la especificación de metadatos de [Swagger] mediante el [Editor de Swagger].</span><span class="sxs-lookup"><span data-stu-id="27943-107">[Jax-RS] is used to create the RESTful Service, and is generated based on the [Swagger] metadata specification using the [Swagger Editor].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27943-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="27943-108">Prerequisites</span></span>
1. <span data-ttu-id="27943-109">[Kit para desarrolladores de Java 8] \(o posterior)</span><span class="sxs-lookup"><span data-stu-id="27943-109">[Java Developer's Kit 8] \(or later)</span></span>
2. <span data-ttu-id="27943-110">[Maven] instalado en el equipo de desarrollo</span><span class="sxs-lookup"><span data-stu-id="27943-110">[Maven] installed on your development machine</span></span>
3. <span data-ttu-id="27943-111">[Git] instalado en el equipo de desarrollo</span><span class="sxs-lookup"><span data-stu-id="27943-111">[Git] installed on your development machine</span></span>
4. <span data-ttu-id="27943-112">Una suscripción de [evaluación gratuita] o de pago a [Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="27943-112">A paid or [free trial] subscription to [Microsoft Azure]</span></span>
5. <span data-ttu-id="27943-113">Una aplicación de prueba HTTP como [Postman]</span><span class="sxs-lookup"><span data-stu-id="27943-113">An HTTP test application like [Postman]</span></span>

## <a name="scaffold-the-api-using-swaggerio"></a><span data-ttu-id="27943-114">Aplicación de la técnica scaffolding a la API mediante Swagger.IO</span><span class="sxs-lookup"><span data-stu-id="27943-114">Scaffold the API using Swagger.IO</span></span>
<span data-ttu-id="27943-115">Con el editor en línea de swagger.io, puede escribir código JSON o YAML de Swagger que representa la estructura de su API.</span><span class="sxs-lookup"><span data-stu-id="27943-115">Using the swagger.io online editor, you can enter Swagger JSON or YAML code representing the structure of your API.</span></span> <span data-ttu-id="27943-116">Cuando haya diseñado el área de superficie de API, puede exportar el código en una diversidad de plataformas y marcos.</span><span class="sxs-lookup"><span data-stu-id="27943-116">Once you have the API surface area designed, you can export code for a variety of platforms and frameworks.</span></span> <span data-ttu-id="27943-117">En la siguiente sección se modificará el código con scaffold para incluir la funcionalidad de simulacro.</span><span class="sxs-lookup"><span data-stu-id="27943-117">In the next section, the scaffolded code will be modified to include mock functionality.</span></span> 

<span data-ttu-id="27943-118">Esta demostración comenzará con un cuerpo JSON de Swagger que se pegará en el editor de swagger.io, que luego se utilizará para generar código mediante el uso de JAX-RS para acceder a un punto de conexión de API de REST.</span><span class="sxs-lookup"><span data-stu-id="27943-118">This demonstration will begin with a Swagger JSON body that you will paste into the swagger.io editor, which will then be used to generate code making use of JAX-RS to access a REST API endpoint.</span></span> <span data-ttu-id="27943-119">A continuación, modificará el código con scaffold para devolver datos ficticios y simular una API de REST creada sobre un mecanismo de persistencia de datos.</span><span class="sxs-lookup"><span data-stu-id="27943-119">Then, you'll edit the scaffolded code to return mock data, simulating a REST API built atop a data persistence mechanism.</span></span>  

1. <span data-ttu-id="27943-120">Copie el siguiente código JSON de Swagger en el Portapapeles:</span><span class="sxs-lookup"><span data-stu-id="27943-120">Copy the following Swagger JSON code to your clipboard:</span></span>
   
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
2. <span data-ttu-id="27943-121">Vaya al [editor en línea de Swagger].</span><span class="sxs-lookup"><span data-stu-id="27943-121">Navigate to the [Online Swagger Editor].</span></span> <span data-ttu-id="27943-122">Una vez allí, haga clic en el elemento de menú **Archivo -> Pegar JSON**.</span><span class="sxs-lookup"><span data-stu-id="27943-122">Once there, click the **File -> Paste JSON** menu item.</span></span>
   
    ![Elemento de menú Pegar JSON][paste-json]
3. <span data-ttu-id="27943-124">Pegue el código JSON de Swagger de lista de contactos que copió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="27943-124">Paste in the Contacts List API Swagger JSON you copied earlier.</span></span> 
   
    ![Pegado de código JSON en Swagger][pasted-swagger]
4. <span data-ttu-id="27943-126">Vea las páginas de documentación y el resumen de la API representado en el editor.</span><span class="sxs-lookup"><span data-stu-id="27943-126">View the documentation pages and API summary rendered in the editor.</span></span> 
   
    ![Ver documentos generados de Swagger][view-swagger-generated-docs]
5. <span data-ttu-id="27943-128">Seleccione la opción de menú **Generar servidor -> JAX RS** para aplicar la técnica scaffolding al código del lado servidor que modificará más adelante para agregar la implementación ficticia.</span><span class="sxs-lookup"><span data-stu-id="27943-128">Select the **Generate Server -> JAX-RS** menu option to scaffold the server-side code you'll edit later to add mock implementation.</span></span> 
   
    ![Generar elemento de menú de código][generate-code-menu-item]
   
    <span data-ttu-id="27943-130">Una vez que se genere el código, se le proporcionará un archivo ZIP para descargar.</span><span class="sxs-lookup"><span data-stu-id="27943-130">Once the code is generated, you'll be provided a ZIP file to download.</span></span> <span data-ttu-id="27943-131">Este archivo contiene el código al que el generador de código de Swagger le ha aplicado la técnica scaffolding y todos los scripts de compilación asociados.</span><span class="sxs-lookup"><span data-stu-id="27943-131">This file contains the code scaffolded by the Swagger code generator and all associated build scripts.</span></span> <span data-ttu-id="27943-132">Descomprima la biblioteca completa en un directorio de su estación de trabajo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="27943-132">Unzip the entire library to a directory on your development workstation.</span></span> 

## <a name="edit-the-code-to-add-api-implementation"></a><span data-ttu-id="27943-133">Edición del código para agregar la implementación de API</span><span class="sxs-lookup"><span data-stu-id="27943-133">Edit the Code to add API Implementation</span></span>
<span data-ttu-id="27943-134">En esta sección va a reemplazar la implementación en el lado servidor del código generado por Swagger con el código personalizado.</span><span class="sxs-lookup"><span data-stu-id="27943-134">In this section, you'll replace the Swagger-generated code's server-side implementation with your custom code.</span></span> <span data-ttu-id="27943-135">El nuevo código devolverá una listaDeMatrices de entidades de contactos para el cliente que realiza la llamada.</span><span class="sxs-lookup"><span data-stu-id="27943-135">The new code will return an ArrayList of Contact entities to the calling client.</span></span> 

1. <span data-ttu-id="27943-136">Abra el archivo de modelo *Contact.java*, ubicado en la carpeta *src/gen/java/io/swagger/model*, mediante [código de Visual Studio] o en el editor de texto de su elección.</span><span class="sxs-lookup"><span data-stu-id="27943-136">Open the *Contact.java* model file, which is located in the *src/gen/java/io/swagger/model* folder, using [Visual Studio Code] or your favorite text editor.</span></span> 
   
    ![Abrir archivo de modelo de contacto][open-contact-model-file]
2. <span data-ttu-id="27943-138">Agregue el siguiente constructor a la clase **Contact**.</span><span class="sxs-lookup"><span data-stu-id="27943-138">Add the following constructor within the **Contact** class.</span></span> 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. <span data-ttu-id="27943-139">Abra el archivo de implementación del servicio *ContactsApiServiceImpl.java*, ubicado en la carpeta *src/main/java/io/swagger/api/impl*, mediante [código de Visual Studio] o en el editor de texto de su elección.</span><span class="sxs-lookup"><span data-stu-id="27943-139">Open the *ContactsApiServiceImpl.java* service implementation file, which is located in the *src/main/java/io/swagger/api/impl* folder, using [Visual Studio Code] or your favorite text editor.</span></span>
   
    ![Abrir archivo de código de servicio de contacto][open-contact-service-code-file]
4. <span data-ttu-id="27943-141">Sobrescriba el código del archivo con este nuevo código para agregar una implementación ficticia al código de servicio.</span><span class="sxs-lookup"><span data-stu-id="27943-141">Overwrite the code in the file with this new code to add a mock implementation to the service code.</span></span> 
   
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
5. <span data-ttu-id="27943-142">Abra un símbolo del sistema y cambie el directorio a la carpeta raíz de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="27943-142">Open a command prompt and change directory to the root folder of your application.</span></span>
6. <span data-ttu-id="27943-143">Ejecute el siguiente comando de Maven para compilar el código y ejecutarlo localmente mediante el servidor de aplicaciones de Jetty.</span><span class="sxs-lookup"><span data-stu-id="27943-143">Execute the following Maven command to build the code and run it using the Jetty app server locally.</span></span> 
   
        mvn package jetty:run
7. <span data-ttu-id="27943-144">Debería ver que la ventana de comandos refleja que Jetty ha iniciado el código en el puerto 8080.</span><span class="sxs-lookup"><span data-stu-id="27943-144">You should see the command window reflect that Jetty has started your code on port 8080.</span></span> 
   
    ![Abrir archivo de código de servicio de contacto][run-jetty-war]
8. <span data-ttu-id="27943-146">Utilice [Postman] para realizar una solicitud al método de API "obtener todos los contactos" en http://localhost:8080/api/contacts.</span><span class="sxs-lookup"><span data-stu-id="27943-146">Use [Postman] to make a request to the "get all contacts" API method at http://localhost:8080/api/contacts.</span></span>
   
    ![Llamar a la API de contactos][calling-contacts-api]
9. <span data-ttu-id="27943-148">Utilice [Postman] para realizar una solicitud al método de API "obtener contacto específico" ubicado en http://localhost:8080/api/contacts/2.</span><span class="sxs-lookup"><span data-stu-id="27943-148">Use [Postman] to make a request to the "get specific contact" API method located at http://localhost:8080/api/contacts/2.</span></span>
   
    ![Llamar a la API de contactos][calling-specific-contact-api]
10. <span data-ttu-id="27943-150">Por último, compile el archivo WAR de Java (archivo Web) ejecutando el siguiente comando de Maven en la consola.</span><span class="sxs-lookup"><span data-stu-id="27943-150">Finally, build the Java WAR (Web ARchive) file by executing the following Maven command in your console.</span></span> 
    
         mvn package war:war
11. <span data-ttu-id="27943-151">Una vez creado el archivo WAR, se colocará en la carpeta **target** .</span><span class="sxs-lookup"><span data-stu-id="27943-151">Once the WAR file is built, it will be placed into the **target** folder.</span></span> <span data-ttu-id="27943-152">Vaya a la carpeta de **destino** y cambie el nombre del archivo WAR por **ROOT.war**.</span><span class="sxs-lookup"><span data-stu-id="27943-152">Navigate into the **target** folder and rename the WAR file to **ROOT.war**.</span></span> <span data-ttu-id="27943-153">(Asegúrese de que las mayúsculas y minúsculas coinciden con este formato).</span><span class="sxs-lookup"><span data-stu-id="27943-153">(Make sure the capitalization matches this format).</span></span>
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. <span data-ttu-id="27943-154">Por último, ejecute los siguientes comandos desde la carpeta raíz de la aplicación para crear una carpeta **deploy** que va a utilizar para implementar el archivo WAR en Azure.</span><span class="sxs-lookup"><span data-stu-id="27943-154">Finally, execute the following commands from the root folder of your application to create a **deploy** folder to use to deploy the WAR file to Azure.</span></span> 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-the-output-to-azure-app-service"></a><span data-ttu-id="27943-155">Publicación del resultado en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="27943-155">Publish the output to Azure App Service</span></span>
<span data-ttu-id="27943-156">En esta sección aprenderá a crear una nueva aplicación de API mediante el Portal de Azure, a prepararla para hospedar aplicaciones Java y a implementar el archivo WAR recién creado en el Servicio de aplicaciones de Azure para ejecutar la nueva aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="27943-156">In this section you'll learn how to create a new API App using the Azure Portal, prepare that API App for hosting Java applications, and deploy the newly-created WAR file to Azure App Service to run your new API App.</span></span> 

1. <span data-ttu-id="27943-157">Cree una nueva aplicación de API en [Azure Portal]; para ello, haga clic en el elemento de menú **Nuevo -> Web y móvil -> Aplicación de API**, escriba los detalles de la aplicación y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="27943-157">Create a new API app in the [Azure portal], by clicking the **New -> Web + Mobile -> API app** menu item, entering your app details, and then clicking **Create**.</span></span>
   
    ![Crear una nueva aplicación de API][create-api-app]
2. <span data-ttu-id="27943-159">Una vez creada la aplicación de API, abra la hoja **Configuración** de la aplicación y, después, haga clic en el elemento de menú **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="27943-159">Once your API app has been created, open your app's **Settings** blade, and then click the **Application settings** menu item.</span></span> <span data-ttu-id="27943-160">Seleccione las últimas versiones de Java entre las opciones disponibles, seleccione la aplicación Tomcat más reciente en el menú **Contenedor web** y después haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="27943-160">Select the latest Java versions from the available options, then select the latest Tomcat from the **Web container** menu, and then click **Save**.</span></span>
   
    ![Configurar Java en la hoja de aplicaciones de API][set-up-java]
3. <span data-ttu-id="27943-162">Haga clic en el elemento **Credenciales de implementación** del menú de configuración y especifique el nombre de usuario y la contraseña que desee usar para publicar archivos en una aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="27943-162">Click the **Deployment credentials** settings menu item, and provide a username and password you wish to use for publishing files to your API App.</span></span> 
   
    ![Configurar credenciales de implementación][deployment-credentials]
4. <span data-ttu-id="27943-164">Haga clic en el elemento de menú de configuración **Origen de implementación** .</span><span class="sxs-lookup"><span data-stu-id="27943-164">Click the **Deployment source** settings menu item.</span></span> <span data-ttu-id="27943-165">Una vez allí, haga clic en el botón **Elegir origen**, seleccione la opción **Repositorio de Git local** y después haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="27943-165">Once there, click the **Choose source** button, select the **Local Git Repository** option, and then click **OK**.</span></span> <span data-ttu-id="27943-166">Se crea un repositorio de Git que se ejecuta en Azure, que tiene una asociación con la aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="27943-166">This will create a Git repository running in Azure, that has an association with your API App.</span></span> <span data-ttu-id="27943-167">Cada vez que confirme el código en la bifurcación *principal* del repositorio de Git, el código se publicará en la instancia de aplicación de API en ejecución activa.</span><span class="sxs-lookup"><span data-stu-id="27943-167">Each time you commit code to the *master* branch of your Git repository, your code will be published into your live running API App instance.</span></span> 
   
    ![Configurar un nuevo repositorio de Git local][select-git-repo]
5. <span data-ttu-id="27943-169">Copie la nueva URL del repositorio de Git en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="27943-169">Copy the new Git repository's URL to your clipboard.</span></span> <span data-ttu-id="27943-170">Guárdela, será importante dentro de poco.</span><span class="sxs-lookup"><span data-stu-id="27943-170">Save this as it will be important in a moment.</span></span> 
   
    ![Configurar un nuevo repositorio de Git para la aplicación][copy-git-repo-url]
6. <span data-ttu-id="27943-172">Realice la operación de inserción de Git del archivo WAR en el repositorio en línea.</span><span class="sxs-lookup"><span data-stu-id="27943-172">Git push the WAR file to the online repository.</span></span> <span data-ttu-id="27943-173">Para ello, vaya a la carpeta **deploy** que creó anteriormente para que pueda confirmar fácilmente el código hasta el repositorio que se ejecuta en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="27943-173">To do this, navigate into the **deploy** folder you created earlier so that you can easily commit the code up to the repository running in your App Service.</span></span> <span data-ttu-id="27943-174">Una vez que esté en la ventana de la consola y que haya ido a la carpeta donde se encuentra la carpeta de aplicaciones web, emita los siguientes comandos de Git para iniciar el proceso y lanzar una implementación.</span><span class="sxs-lookup"><span data-stu-id="27943-174">Once you're in the console window and navigated into the folder where the webapps folder is located, issue the following Git commands to launch the process and fire off a deployment.</span></span> 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    <span data-ttu-id="27943-175">Después de emitir la solicitud **push** , se le pedirá la contraseña que creó anteriormente para la credencial de la implementación.</span><span class="sxs-lookup"><span data-stu-id="27943-175">Once you issue the **push** request, you'll be asked for the password you created for the deployment credential earlier.</span></span> <span data-ttu-id="27943-176">Después de escribir las credenciales, verá que en el portal se muestra que la implementación se ha llevado a cabo.</span><span class="sxs-lookup"><span data-stu-id="27943-176">After you enter your credentials, you should see your portal display that the update was deployed.</span></span>
7. <span data-ttu-id="27943-177">Si utiliza nuevamente Postman para llegar a la aplicación de API recién implementada que se ejecuta en el Servicio de aplicaciones de Azure, verá que el comportamiento es coherente y que ahora se devuelven los datos de contacto, y todo ello mediante sencillos cambios en el código Java con scaffold Swagger.io.</span><span class="sxs-lookup"><span data-stu-id="27943-177">If you once again use Postman to hit the newly-deployed API App running in Azure App Service, you'll see that the behavior is consistent and that now it is returning contact data as expected, and using simple code changes to the Swagger.io scaffolded Java code.</span></span> 
   
    ![Uso de la API de REST de contactos de Java activa en Azure][postman-calling-azure-contacts]

## <a name="next-steps"></a><span data-ttu-id="27943-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="27943-179">Next steps</span></span>
<span data-ttu-id="27943-180">En este artículo ha sido capaz de comenzar con un archivo JSON de Swagger y algún código Java con scaffold obtenido con el editor de Swagger.io.</span><span class="sxs-lookup"><span data-stu-id="27943-180">In this article, you were able to start with a Swagger JSON file and some scaffolded Java code obtained from the Swagger.io editor.</span></span> <span data-ttu-id="27943-181">A partir de ahí, algunos sencillos cambios y un proceso de implementación de Git han dado lugar a que tengamos una aplicación de API funcional escrita en Java.</span><span class="sxs-lookup"><span data-stu-id="27943-181">From there, your simple changes and a Git deploy process resulted in having a functional API app written in Java.</span></span> <span data-ttu-id="27943-182">El siguiente tutorial muestra cómo [consumir aplicaciones de API desde clientes JavaScript mediante CORS][App Service API CORS].</span><span class="sxs-lookup"><span data-stu-id="27943-182">The next tutorial shows how to [consume API apps from JavaScript clients, using CORS][App Service API CORS].</span></span> <span data-ttu-id="27943-183">Otros tutoriales de la serie muestran cómo implementar la autenticación y autorización.</span><span class="sxs-lookup"><span data-stu-id="27943-183">Later tutorials in the series show how to implement authentication and authorization.</span></span>

<span data-ttu-id="27943-184">Para sacar más partido a este ejemplo, aprenda más sobre el [SDK de almacenamiento para Java] para conservar los blobs de JSON.</span><span class="sxs-lookup"><span data-stu-id="27943-184">To build on this sample, you can learn more about the [Storage SDK for Java] to persist the JSON blobs.</span></span> <span data-ttu-id="27943-185">O bien, puede usar el [SDK de Java de DocumentDB] para guardar los datos de contacto en Azure DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="27943-185">Or, you could use the [Document DB Java SDK] to save your Contact data to Azure Document DB.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="27943-186">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="27943-186">See Also</span></span>
<span data-ttu-id="27943-187">Para más información sobre el uso de Azure con Java, visite [Azure para desarrolladores de Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="27943-187">For more information about using Azure with Java, visit [Azure for Java developers](/java/azure).</span></span>

<!-- URL List -->

[App Service API CORS]: app-service-api-cors-consume-javascript.md
[Azure Portal]: https://portal.azure.com/
[SDK de Java de DocumentDB]: ../documentdb/documentdb-java-application.md
[evaluación gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: http://www.git-scm.com/
[Azure Java Developer Center]: /develop/java/
[Kit para desarrolladores de Java 8]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[Jax-RS]: https://jax-rs-spec.java.net/
[Maven]: https://maven.apache.org/
[Microsoft Azure]: https://azure.microsoft.com/
[editor en línea de Swagger]: http://editor2.swagger.io/
[Postman]: https://www.getpostman.com/
[SDK de almacenamiento para Java]:../storage/blobs/storage-java-how-to-use-blob-storage.md
[Swagger]: http://swagger.io/
[Editor de Swagger]: http://editor.swagger.io/
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
