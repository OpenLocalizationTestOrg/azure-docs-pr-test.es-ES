---
title: "Tutorial de Azure Cosmos DB: Creación, consulta y recorrido en la consola de Gremlin de Apache TinkerPops | Microsoft Docs"
description: "Un toocreates de inicio rápido de base de datos de Azure Cosmos vértices, bordes y las consultas que utilizan API Graph de Azure Cosmos DB Hola."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: terminal
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: denlee
ms.openlocfilehash: 9de64c97fec89c45cecba9e14214db472ec76f57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-query-and-traverse-a-graph-in-hello-gremlin-console"></a>Azure Cosmos DB: Crear, consultar y recorrer un gráfico en la consola de hello Gremlin

Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft. Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente. 

Este inicio rápido muestra cómo toocreate una cuenta de base de datos de Azure Cosmos, la base de datos y el gráfico (contenedor) utilizando Hola portal de Azure y, a continuación, use hello [Gremlin consola](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) de [TinkerPop Apache](http://tinkerpop.apache.org) toowork con Datos de API (versión preliminar) del gráfico. En este tutorial, crear y consultar los vértices y bordes, actualizando una propiedad de vértices, consultar los vértices, recorren el gráfico de Hola y quitar un vértice.

![BD de Cosmos Azure de consola de Apache Gremlin Hola](./media/create-graph-gremlin-console/gremlin-console.png)

consola de Hello Gremlin es Groovy/Java basados y se ejecuta en Linux, Mac y Windows. Puede descargarlo en hello [TinkerPop Apache sitio](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).

## <a name="prerequisites"></a>Requisitos previos

Necesitará toohave un toocreate de suscripción de Azure una cuenta de base de datos de Azure Cosmos para este tutorial rápido.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

También necesita hello tooinstall [Gremlin consola](http://tinkerpop.apache.org/). Use la versión 3.2.5 o posterior.

## <a name="create-a-database-account"></a>Creación de una cuenta de base de datos

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Agregar un grafo

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a id="ConnectAppService"></a>Conectar el servicio de aplicación tooyour
1. Antes de iniciar Hola Gremlin consola, crear o modificar el archivo de configuración de secure.yaml remoto de hello en el directorio de apache-tinkerpop-gremlin-console-3.2.5/conf Hola.
2. Rellene sus configuraciones *host*, *puerto*, *nombre de usuario*, *contraseña*, *connectionPool* y *serializador*:

    Configuración|Valor sugerido|Descripción
    ---|---|---
    hosts|[***.graphs.azure.com]|Ver la captura de pantalla siguiente. Se trata de valor de URI Gremlin de hello en la página de información general de Hola de hello portal de Azure, entre corchetes, con finales Hola: 443 / quitado.<br><br>Este valor también puede obtenerse de la pestaña de claves de hello, utilizando el valor URI de hello quitar https://, cambiar toographs de documentos y quitando finales Hola: 443 /.
    puerto|443|Establecer too443.
    nombre de usuario|*Su nombre de usuario*|Hola recursos de formulario de hello `/dbs/<db>/colls/<coll>` donde `<db>` es el nombre de la base de datos y `<coll>` es el nombre de la colección.
    Contraseña|*La clave principal*| Ver la segunda captura de pantalla más adelante. Se trata de la clave principal, que puede recuperar de la página de claves de Hola de portal de Azure, en el cuadro de la clave principal de Hola Hola. Use el botón de copiar de hello lado izquierdo de hello del valor de hello cuadro toocopy Hola.
    connectionPool|{enableSsl: true}|La configuración del grupo de conexiones para SSL.
    serializer|{ className:org.apache.tinkerpop.gremlin.<br>driver.ser.GraphSONMessageSerializerV1d0,<br> config: { serializeResultToString: true }}|Establezca el valor de toothis y eliminar cualquier `\n` saltos de línea cuando se pegue en el valor de Hola.

    Para el valor de hosts de hello, copie hello **Gremlin URI** valor de hello **Introducción** página: ![visualizar y copiar valor de URI Gremlin de hello en la página de información general de Hola Hola portal de Azure](./media/create-graph-gremlin-console/gremlin-uri.png)

    Para el valor de la contraseña de hello, copiar hello **clave principal** de hello **claves** página: ![visualizar y copiar las claves de la clave principal en hello portal de Azure, página](./media/create-graph-gremlin-console/keys.png)


3. En el terminal, ejecute `bin/gremlin.bat` o `bin/gremlin.sh` toostart hello [Gremlin consola](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).
4. En el terminal, ejecute `:remote connect tinkerpop.server conf/remote-secure.yaml` servicio de aplicaciones de tooconnect tooyour.

    > [!TIP]
    > Si recibe el error hello `No appenders could be found for logger` Asegúrese de que actualiza el valor de serializador de hello en archivo de hello secure.yaml remoto tal como se describe en el paso 2. 

Estupendo. Ahora que hemos terminado el programa de instalación de hello, puede empezar a ejecutar algunos comandos de la consola.

Probemos un comando count() sencillo. Escriba Hola siguiente en la consola de hello en el símbolo del sistema de hello:
```
:> g.V().count()
```

> [!TIP]
> ¿Hola aviso `:>` que precede a hello `g.V().count()` texto? 
>
> Esto forma parte del comando hello que necesita tootype. Es importante cuando utiliza la consola de Gremlin hello, con la base de datos de Azure Cosmos.  
>
> Si se omite este `:>` prefijo indica el comando de hello localmente, de hello consola tooexecute a menudo en un gráfico en memoria.
> Mediante este `:>` indica Hola consola tooexecute un comando remoto, en este caso, en la base de datos de Cosmos (ya sea emulador de localhost hello, o una > instancia de Azure).


## <a name="create-vertices-and-edges"></a>Crear vértices y bordes

Comencemos agregando cinco vértices de personas para *Thomas*, *Mary Kay*, *Robin*, *Ben* y *Jack*.

Entrada (Thomas):

```
:> g.addV('person').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44).property('userid', 1)
```

Salida:

```
==>[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d,label:person,type:vertex,properties:[firstName:[[id:f02a749f-b67c-4016-850e-910242d68953,value:Thomas]],lastName:[[id:f5fa3126-8818-4fda-88b0-9bb55145ce5c,value:Andersen]],age:[[id:f6390f9c-e563-433e-acbf-25627628016e,value:44]],userid:[[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d|userid,value:1]]]]
```
Entrada (Mary Kay):

```
:> g.addV('person').property('firstName', 'Mary Kay').property('lastName', 'Andersen').property('age', 39).property('userid', 2)

```

Salida:

```
==>[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e,label:person,type:vertex,properties:[firstName:[[id:ea0604f8-14ee-4513-a48a-1734a1f28dc0,value:Mary Kay]],lastName:[[id:86d3bba5-fd60-4856-9396-c195ef7d7f4b,value:Andersen]],age:[[id:bc81b78d-30c4-4e03-8f40-50f72eb5f6da,value:39]],userid:[[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e|userid,value:2]]]]

```

Entrada (Robin):

```
:> g.addV('person').property('firstName', 'Robin').property('lastName', 'Wakefield').property('userid', 3)
```

Salida:

```
==>[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e,label:person,type:vertex,properties:[firstName:[[id:ec65f078-7a43-4cbe-bc06-e50f2640dc4e,value:Robin]],lastName:[[id:a3937d07-0e88-45d3-a442-26fcdfb042ce,value:Wakefield]],userid:[[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e|userid,value:3]]]]
```

Entrada (Ben):

```
:> g.addV('person').property('firstName', 'Ben').property('lastName', 'Miller').property('userid', 4)

```

Salida:

```
==>[id:ee86b670-4d24-4966-9a39-30529284b66f,label:person,type:vertex,properties:[firstName:[[id:a632469b-30fc-4157-840c-b80260871e9a,value:Ben]],lastName:[[id:4a08d307-0719-47c6-84ae-1b0b06630928,value:Miller]],userid:[[id:ee86b670-4d24-4966-9a39-30529284b66f|userid,value:4]]]]
```

Entrada (Jack):

```
:> g.addV('person').property('firstName', 'Jack').property('lastName', 'Connor').property('userid', 5)
```

Salida:

```
==>[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469,label:person,type:vertex,properties:[firstName:[[id:4250824e-4b72-417f-af98-8034aa15559f,value:Jack]],lastName:[[id:44c1d5e1-a831-480a-bf94-5167d133549e,value:Connor]],userid:[[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469|userid,value:5]]]]
```


Después, vamos a agregar bordes a las relaciones entre estas personas.

Entrada (Thomas -> Mary Kay):

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Mary Kay'))
```

Salida:

```
==>[id:c12bf9fb-96a1-4cb7-a3f8-431e196e702f,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:0d1fa428-780c-49a5-bd3a-a68d96391d5c,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

Entrada (Thomas -> Robin):

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Robin'))
```

Salida:

```
==>[id:58319bdd-1d3e-4f17-a106-0ddf18719d15,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:3e324073-ccfc-4ae1-8675-d450858ca116,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

Entrada (Robin -> Ben):

```
:> g.V().hasLabel('person').has('firstName', 'Robin').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Ben'))
```

Salida:

```
==>[id:889c4d3c-549e-4d35-bc21-a3d1bfa11e00,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:40fd641d-546e-412a-abcc-58fe53891aab,outV:3e324073-ccfc-4ae1-8675-d450858ca116]
```

## <a name="update-a-vertex"></a>Actualizar un vértice

Vamos a actualizar hello *Thomas* vértice con una nueva era de *45*.

Entrada:
```
:> g.V().hasLabel('person').has('firstName', 'Thomas').property('age', 45)
```
Salida:

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

## <a name="query-your-graph"></a>Consultar el grafo

Ahora, vamos a ejecutar una variedad de consultas en su grafo.

En primer lugar, vamos a intentarlo una consulta con una filtro tooreturn únicamente las personas que son más de 40 años de antigüedad.

Entrada (consulta de filtro):

```
:> g.V().hasLabel('person').has('age', gt(40))
```

Salida:

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

A continuación, vamos a Hola nombre de proyecto para las personas de Hola que sean más antiguos que 40 años de antigüedad.

Entrada (filtro + consulta de proyección):

```
:> g.V().hasLabel('person').has('age', gt(40)).values('firstName')
```

Salida:

```
==>Thomas
```

## <a name="traverse-your-graph"></a>Recorrer el grafo

Vamos a recorrer Hola gráfico tooreturn todos amigos de Thomas.

Entrada (amigos de Thomas):

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person')
```

Salida: 

```
==>[id:f04bc00b-cb56-46c4-a3bb-a5870c42f7ff,label:person,type:vertex,properties:[firstName:[[id:14feedec-b070-444e-b544-62be15c7167c,value:Mary Kay]],lastName:[[id:107ab421-7208-45d4-b969-bbc54481992a,value:Andersen]],age:[[id:4b08d6e4-58f5-45df-8e69-6b790b692e0a,value:39]]]]
==>[id:91605c63-4988-4b60-9a30-5144719ae326,label:person,type:vertex,properties:[firstName:[[id:f760e0e6-652a-481a-92b0-1767d9bf372e,value:Robin]],lastName:[[id:352a4caa-bad6-47e3-a7dc-90ff342cf870,value:Wakefield]]]]
```

A continuación, vamos a la capa siguiente de Hola de vértices. Recorrer Hola gráfico tooreturn todos los amigos de Hola de amigos de Thomas.

Entrada (amigos de los amigos de Thomas):

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```
Salida:

```
==>[id:a801a0cb-ee85-44ee-a502-271685ef212e,label:person,type:vertex,properties:[firstName:[[id:b9489902-d29a-4673-8c09-c2b3fe7f8b94,value:Ben]],lastName:[[id:e084f933-9a4b-4dbc-8273-f0171265cf1d,value:Miller]]]]
```

## <a name="drop-a-vertex"></a>Quitar un vértice

Vamos a eliminar ahora un vértice de base de datos de gráfico de Hola.

Entrada (quitar vértice de Jack):

```
:> g.V().hasLabel('person').has('firstName', 'Jack').drop()
```

## <a name="clear-your-graph"></a>Borrar el grafo

Por último, vamos a limpiar la base de datos de Hola de todos los vértices y bordes.

Entrada:

```
:> g.E().drop()
:> g.V().drop()
```

¡Enhorabuena! Ha finalizado este tutorial de API Graph de Azure Cosmos DB.

## <a name="review-slas-in-hello-azure-portal"></a>Revise los SLA de hello portal de Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos:  

1. En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó. 
2. En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo toocreate una cuenta de base de datos de Azure Cosmos, crear un gráfico utilizando Hola Explorador de datos, crear vértices y bordes y recorrer el gráfico mediante la consola de Gremlin Hola. Ahora puede crear consultas más complejas e implementar con Gremlin una lógica eficaz de recorrido del grafo. 

> [!div class="nextstepaction"]
> [Consulta mediante Gremlin](tutorial-query-graph.md)
