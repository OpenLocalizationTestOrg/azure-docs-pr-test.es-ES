---
title: temas de tendencias de aaaTwitter con Apache Storm en HDInsight | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Trident toocreate una topología de Apache Storm que determina los temas tendencias en Twitter basado en hashtags."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 63b280ea-5c07-4dc8-a35f-dccf5a96ba93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/14/2017
ms.author: larryfr
ms.openlocfilehash: 0281b495d10833c63868b36856c96369b139c553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a>Determinación de las tendencias de Twitter con Apache Storm en HDInsight

Obtenga información acerca de cómo toouse Trident toocreate una topología de Storm que determina tendencias temas (etiquetas de hash) en Twitter.

Trident es una abstracción de alto nivel que ofrece herramientas como uniones, agregaciones, agrupaciones, funciones y filtros. Además, Trident agrega primitivas para realizar el procesamiento incremental, con estado. ejemplo de Hola usado en este documento es una topología de Trident con un pitorro personalizado y una función. También usa varias funciones integradas disponibles en Trident.

## <a name="requirements"></a>Requisitos

* <a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Hello JDK 1.8 y Java</a>

* <a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a>

* <a href="http://git-scm.com/" target="_blank">Git</a>

* Una cuenta de desarrollador de Twitter

## <a name="download-hello-project"></a>Descargar proyecto Hola

Usar hello después tooclone Hola proyecto de código de forma local.

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a>Descripción de la topología de Hola

Hola siguiente diagrama se muestra de cómo fluyen los datos a través de esta topología:

![Topología](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> Este diagrama es una vista simplificada de topología de Hola. Varias instancias de componentes de Hola se distribuyen en nodos de hello en clúster de Hola.


Hola código Trident que implementa la topología de hello es como sigue:

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

Este código realiza Hola siguientes acciones:

1. Crea una secuencia de pitorro Hola. pitorro Hola recupera tweets de Twitter y los filtros de palabras clave específicas (amor, música y coffee en este ejemplo).

2. HashtagExtractor, una función personalizada, es tooextract usa hash etiquetas de cada tweet. Hola hash distinguen flujo toohello emitido.

3. secuencia de Hello es había agrupado por etiqueta de hash y pasa tooan agregador. Este agregador crea un recuento de cuántas veces se ha repetido cada hashtag. Estos datos se conservan en memoria. Por último, se genera una nueva secuencia que contiene la etiqueta de hash de Hola y recuento de Hola.

4. Hola **FirstN** ensamblado es tooreturn aplicado solo Hola 10 valores más altos, tomando como base el campo de recuento de Hola.

> [!NOTE]
> Para obtener más información sobre cómo trabajar con Trident, vea hello [Introducción a la API de Trident](http://storm.apache.org/releases/current/Trident-API-Overview.html) documento.

### <a name="hello-spout"></a>pitorro Hola

pitorro Hello, **TwitterSpout**, usa [Twitter4j](http://twitter4j.org/en/) tooretrieve tweets de Twitter. Se crea un filtro para palabras hello __le encanta__, **música**, y **café**. Tweets entrantes (status) que coinciden con el filtro de Hola se almacenan en una cola bloqueo vinculada. Por último, elementos se saca de la cola de Hola y genera la topología de toohello.

### <a name="hello-hashtagextractor"></a>Hola HashtagExtractor

etiquetas de hash tooextract, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) es tooretrieve usado todas las etiquetas de hash que se encuentran en tweet Hola. Estos artículos pasan a secuencia toohello emitido.

## <a name="configure-twitter"></a>Configuración de Twitter

Usar hello siguiendo los pasos tooregister una nueva aplicación de Twitter y obtener tooread de necesita la información del token de acceso y el consumidor Hola de Twitter:

1. Vaya demasiado[aplicaciones Twitter](https://apps.twitter.com) y haga clic en hello **crear nueva aplicación** botón. Al rellenar el formulario de hello, deje hello **dirección URL de devolución de llamada** campo vacío.

2. Cuando se crea la aplicación hello, haga clic en hello **claves y Tokens de acceso** ficha.

3. Hola copia **clave de consumidor** y **secreto de consumidor** información.

4. En hello parte inferior de la página de hello, seleccione **crear mi token de acceso** si no existen tokens. Cuando se han creado los tokens de hello, Hola copia **Token de acceso** y **secreto del Token de acceso** información.

5. Hola **TwitterSpoutTopology** proyecto Hola clonado anteriormente, abra **resources/twitter4j.properties** de archivos, agregar información de Hola que recopiló en los pasos anteriores de hello y, a continuación, guarde el archivo hello .

## <a name="build-hello-topology"></a>Crear topología de Hola

Usar hello siguiendo el proyecto de código toobuild hello:

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a>Topología de Hola de prueba

Usar hello después topología localmente de comando tootest hello:

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

Una vez iniciada la topología de hello, debería ver información de depuración que contiene el hash de hello etiquetas y recuentos de emitido por la topología de Hola. salida de Hello debe aparecer toohello similar siguiente texto:

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha probado localmente la topología de hello, descubrir cómo toodeploy Hola topología: [implementar y administrar topologías de Apache Storm en HDInsight](hdinsight-storm-deploy-monitor-topology.md).

También es posible que interesa Hola Storm temas siguientes:

* [Desarrollo de las topologías de Java para Storm en HDInsight con Maven](hdinsight-storm-develop-java-topology.md)
* [Desarrollo de las topologías de C# para Storm en HDInsight con Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

Para obtener más ejemplos de Storm para HDInsight:

* [Topologías de ejemplo para Storm en HDInsight](hdinsight-storm-example-topology.md)

