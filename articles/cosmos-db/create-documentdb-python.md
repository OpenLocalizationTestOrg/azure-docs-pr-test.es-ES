---
title: "Azure Cosmos DB: Compilar una aplicación con Python y Hola API de documentos | Documentos de Microsoft"
description: "Presenta un ejemplo de código de Python que puede usar tooconnect tooand consulta Hola API de documentos de base de datos de Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 51c11be2-af6d-425f-a86a-39cbfe61da29
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 05/13/2017
ms.author: mimig
ms.openlocfilehash: e66965ab493c6ef693e88a3767a401d39e1bde2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-hello-azure-portal"></a>Azure Cosmos DB: Compilar una aplicación de API de documentos con Python y Hola portal de Azure

Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft. Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente. 

Este inicio rápido muestra cómo toocreate una cuenta de base de datos de Azure Cosmos, la base de datos de documento y la colección mediante Hola portal de Azure. A continuación, compilar y ejecutar una aplicación de consola compilada en hello [documentos Python API](documentdb-sdk-python.md).

## <a name="prerequisites"></a>Requisitos previos

* Para poder ejecutar este ejemplo, debe tener Hola siguiendo los requisitos previos:
    * [Visual Studio 2015](http://www.visualstudio.com/) o posterior.
    * Herramientas de Python para Visual Studio desde [GitHub](http://microsoft.github.io/PTVS/). En este tutorial se usan las herramientas de Python para VS 2015.
    * Python 2.7 en [python.org](https://www.python.org/downloads/release/python-2712/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Creación de una cuenta de base de datos

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Incorporación de una colección

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Clonar aplicación de ejemplo de Hola

Ahora vamos a clonar una API de documentos de aplicación de github, establezca la cadena de conexión de Hola y ejecútelo. Vea lo fácil que es toowork con datos mediante programación. 

1. Abra una ventana de terminal de git, como git bash, y `cd` tooa directorio de trabajo.  

2. Ejecute hello después de repositorio de ejemplo de comando tooclone Hola. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-hello-code"></a>Revise el código de hello

Vamos a hacer una revisión rápida de lo que sucede en la aplicación hello. Archivo de DocumentDBGetStarted.py de hello abierto y encontrará que estas líneas de código crean Hola recursos de base de datos de Azure Cosmos. 


* Hola DocumentClient se inicializa.

    ```python
    # Initialize hello Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* Se crea una base de datos.

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* Se crea una colección.

    ```python
    # Create collection options
    options = {
        'offerEnableRUPerMinuteThroughput': True,
        'offerVersion': "V2",
        'offerThroughput': 400
    }

    # Create a collection
    collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)
    ```

* Se crean algunos documentos.

    ```python
    # Create some documents
    document1 = client.CreateDocument(collection['_self'],
        { 
            'id': 'server1',
            'Web Site': 0,
            'Cloud Service': 0,
            'Virtual Machine': 0,
            'name': 'some' 
        })
    ```

* Se realiza una consulta con SQL.

    ```python
    # Query them in SQL
    query = { 'query': 'SELECT * FROM server s' }    
            
    options = {} 
    options['enableCrossPartitionQuery'] = True
    options['maxItemCount'] = 2

    result_iterable = client.QueryDocuments(collection['_self'], query, options)
    results = list(result_iterable);

    print(results)
    ```

## <a name="update-your-connection-string"></a>Actualizar la cadena de conexión

Ahora vuelva atrás toohello tooget portal Azure la información de la cadena de conexión y se copia en la aplicación hello.

1. Hola [portal de Azure](http://portal.azure.com/), en la base de datos de Azure Cosmos account, Hola barra de navegación izquierda, haga clic en **claves**y, a continuación, haga clic en **claves de lectura y escritura**. Usará Hola copia botones en hello derecha de hello toocopy de pantalla Hola URI y la clave principal en hello `DocumentDBGetStarted.py` archivo en el paso siguiente de saludo.

    ![Ver y copiar una clave de acceso en hello portal de Azure, hoja de claves](./media/create-documentdb-dotnet/keys.png)

2. Abra Hola `DocumentDBGetStarted.py` archivo. 

3. Copie el valor URI de portal hello (mediante el botón Copiar de Hola) y hacerla Hola valor de clave de punto de conexión de hello en `DocumentDBGetStarted.py`. 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. A continuación, copie el valor de clave principal del portal de Hola y hacerla Hola valo hello `config.MASTERKEY` en `DocumentDBGetStarted.py`. Ahora ha actualizado la aplicación con toda la información de hello debe toocommunicate con base de datos de Azure Cosmos. 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-hello-app"></a>Ejecutar aplicación hello
1. En Visual Studio, haga doble clic en el proyecto de hello en **el Explorador de soluciones**, seleccione el entorno actual de Python de Hola y luego haga clic en.

2. Seleccione Instalar paquete de Python y, después, escriba **pydocumentdb**.

3. Ejecute la aplicación de hello toorun F5. La aplicación se muestra en el explorador. 

Ahora puede volver atrás tooData explorador y vea la consulta, modificar y trabajar con nuevos datos. 

## <a name="review-slas-in-hello-azure-portal"></a>Revise los SLA de hello portal de Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos:

1. En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó. 
2. En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo crear una colección mediante Hola Explorador de datos toocreate una cuenta de base de datos de Azure Cosmos y ejecutar una aplicación. Ahora puede importar la cuenta de base de datos de Cosmos tooyour datos adicionales. 

> [!div class="nextstepaction"]
> [Importar datos en la base de datos de Azure Cosmos para hello API de documentos](import-data.md)


