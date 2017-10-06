---
title: "Azure Cosmos DB: Compilación de una aplicación web con la autenticación de Xamarin y Facebook | Microsoft Docs"
description: "Presenta un ejemplo de código de .NET puede usar tooconnect tooand consultar la base de datos de Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 5f71dddd2b2f5bd117e481c96c17915fc58d2119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a>Azure Cosmos DB: Compilación de una aplicación web con la autenticación de .NET, Xamarin y Facebook

Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft. Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente. 

Este inicio rápido muestra cómo toocreate una cuenta de base de datos de Azure Cosmos, la base de datos de documento y la colección mediante Hola portal de Azure. A continuación, podrá compilar e implementar una aplicación de web de lista de tareas integrada en hello [API de .NET de DocumentDB](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/)y motor de autorización de base de datos de Azure Cosmos Hola. aplicación de web de lista de tareas de Hello implementa un patrón de datos por el usuario que permite toologin de los usuarios mediante Facebook Auth y administrar sus propios elementos de toodo.

## <a name="prerequisites"></a>Requisitos previos

Si aún no tiene Visual Studio de 2017 instalado, puede descargar y usar hello **libre** [2017 Community Edition de Visual Studio](https://www.visualstudio.com/downloads/). Asegúrese de que habilitar **desarrollo Azure** durante la instalación de Visual Studio Hola.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Creación de una cuenta de base de datos

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Incorporación de una colección

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Clonar aplicación de ejemplo de Hola

Ahora vamos a clonar una API de documentos de aplicación de github, establezca la cadena de conexión de Hola y ejecútelo. Podrá ver lo fácil que es toowork con datos mediante programación. 

1. Abra una ventana de terminal de git, como git bash, y `cd` tooa directorio de trabajo.  

2. Ejecute hello después de repositorio de ejemplo de comando tooclone Hola. 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. A continuación, abra el archivo DocumentDBTodo.sln de hello de carpeta de samples/xamarin/UserItems/xamarin.forms de hello en Visual Studio. 

## <a name="review-hello-code"></a>Revise el código de hello

contiene el código de Hello en la carpeta de hello Xamarin:

* Aplicación de Xamarin. aplicación Hello almacena elementos de lista de tareas del usuario de hello en una colección con particiones denominada UserItems.
* Resource token broker API. Un recurso de base de datos de Azure Cosmos de toobroker simple de ASP.NET Web API tokens toohello registrado en los usuarios de la aplicación hello. Tokens de recursos son tokens de acceso de corta duración que brindan aplicación hello Hola acceso toohello registrado en los datos del usuario.

Hola autenticación y flujo de datos se muestra en el siguiente diagrama de Hola.

* Hola UserItems colección se crea con la clave de partición de hello ' / userid'. Especificar que una clave de partición para una colección permite tooscale de base de datos de Azure Cosmos infinitamente como número de Hola de usuarios y elementos aumenta de tamaño.
* aplicación de Xamarin Hello permite toologin a los usuarios con credenciales de Facebook.
* aplicación de Xamarin Hello usa tooauthenticate de token de acceso de Facebook con API de ResourceTokenBroker
* broker de token de recurso de Hello API autentica mediante la característica de autenticación de servicio de la aplicación de solicitud de Hola y solicita un token de recurso de base de datos de Azure Cosmos con documentos de tooall de acceso de lectura/escritura compartir la clave de partición del usuario autenticado de Hola.
* Broker de token de recurso devuelve aplicación de cliente de hello recursos toohello símbolo (token).
* aplicación Hello tiene acceso a elementos de tareas del usuario de hello mediante el token de recurso de Hola.

![Aplicación de tareas pendientes con datos de ejemplo](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a>Actualizar la cadena de conexión

Ahora vuelva atrás toohello tooget portal Azure la información de la cadena de conexión y se copia en la aplicación hello.

1. Hola [portal de Azure](http://portal.azure.com/), en la base de datos de Azure Cosmos account, Hola barra de navegación izquierda, haga clic en **claves**y, a continuación, haga clic en **claves de lectura y escritura**. Deberá usar botones de copia de hello en hello derecha de hello toocopy de pantalla Hola URI y la clave principal en el archivo Web.config de hello en el paso siguiente de saludo.

    ![Ver y copiar una clave de acceso en hello portal de Azure, hoja de claves](./media/create-documentdb-xamarin-dotnet/keys.png)

2. En 2017 de Visual Studio, abra el archivo Web.config de hello en la carpeta de azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker de Hola. 

3. Copie el valor URI de portal hello (mediante el botón Copiar de Hola) y hacerla Hola valo accountUrl hello en el archivo Web.config. 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. A continuación, copie el valor de clave principal del portal de Hola y hacerla Hola valo hello accountKey en Web.congif. 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

Ahora ha actualizado la aplicación con toda la información de hello debe toocommunicate con base de datos de Azure Cosmos. 

## <a name="build-and-deploy-hello-web-app"></a>Compilar e implementar la aplicación web de hello

1. Hola portal de Azure, crear a un servicio de aplicación sitio Web toohost Hola recursos token broker API.
2. En hello portal de Azure, abra la hoja de configuración de la aplicación hello del agente de token de recurso de hello sitio Web de API de. Rellene Hola después de la configuración de la aplicación:

    * accountUrl - URL hello de la cuenta de base de datos de Azure Cosmos desde la pestaña de claves de saludo de la cuenta de base de datos de Azure Cosmos.
    * accountKey - clave maestra de la cuenta de la base de datos de Azure Cosmos Hola desde la pestaña de claves de saludo de la cuenta de base de datos de Azure Cosmos.
    * databaseId y collectionId de la base de datos y de la colección creadas

3. Publicar hello ResourceTokenBroker solución tooyour creado sitio Web.

4. Abra el proyecto de Xamarin hello y navegue tooTodoItemManager.cs. Rellene los valores de hello para accountURL, collectionId, databaseId, así como resourceTokenBrokerURL como dirección url base https de hello para el sitio Web de broker de token de recurso de Hola.

5. Hola completa [cómo tooconfigure su inicio de sesión de servicio de aplicaciones aplicación toouse Facebook](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) toosetup tutorial autenticación de Facebook y configurar el sitio Web de ResourceTokenBroker Hola.

    Ejecute la aplicación de Xamarin hello.

## <a name="review-slas-in-hello-azure-portal"></a>Revise los SLA de hello portal de Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos: 

1. En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que acaba de crear. 
2. En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo crear una colección mediante Hola Explorador de datos, toocreate una cuenta de base de datos de Azure Cosmos y compilar e implementar una aplicación de Xamarin. Ahora puede importar la cuenta de base de datos de Cosmos tooyour datos adicionales. 

> [!div class="nextstepaction"]
> [Importación de datos a Azure Cosmos DB](import-data.md)
