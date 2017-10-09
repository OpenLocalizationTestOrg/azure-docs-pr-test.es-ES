---
title: los niveles de rendimiento aaaDocumentDB API | Documentos de Microsoft
description: "Obtenga información acerca de cómo los niveles de rendimiento de API de documentos le permiten tooreserve rendimiento en una base por contenedor."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 7dc21c71-47e2-4e06-aa21-e84af52866f4
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 716bc11ae238dbb0feebf004ed8d5f8a7515ec6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="retiring-hello-s1-s2-and-s3-performance-levels"></a>Retirar los niveles de rendimiento Hola S1, S2 y S3

> [!IMPORTANT] 
> Hola S1, S2 y S3 niveles de rendimiento descritos en este artículo se ha retirado y ya no están disponibles para las nuevas cuentas de API de documentos.
>

En este artículo se proporciona información general de los niveles de rendimiento S1, S2 y S3 y explica cómo colecciones de Hola que usen estos niveles de rendimiento se incluirá las colecciones de partición toosingle migrados en el 1 de agosto de 2017. Después de leer este artículo, podrá hello tooanswer pueda siguientes preguntas:

- [¿Por qué rendimiento S1, S2 y S3 de hello niveles han ido retirando?](#why-retired)
- [¿Cómo colecciones de una sola partición y con particiones se comparan toohello S1, S2, S3 los niveles de rendimiento?](#compare)
- [¿Qué necesita toodo tooensure sin interrupciones, tener acceso a datos de toomy?](#uninterrupted-access)
- [¿Cómo cambiará Mi colección después de la migración de hello?](#collection-change)
- [¿Cómo cambiará mi facturación después de que deseo que las colecciones de partición toosingle migrados?](#billing-change)
- [¿Qué ocurre si necesito más de 10 GB de almacenamiento?](#more-storage-needed)
- [¿Se puede cambiar entre los niveles de rendimiento de hello S1, S2 y S3 antes del 1 de agosto de 2017?](#change-before)
- [¿Cómo puedo saber cuándo ha migrado mi colección?](#when-migrated)
- [¿Cómo migrar de hello S1, S2, S3 rendimiento niveles toosingle las colecciones de partición en mi propio?](#migrate-diy)
- [¿Cómo me afecta si soy un cliente de EA?](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-hello-s1-s2-and-s3-performance-levels-being-retired"></a>¿Por qué rendimiento S1, S2 y S3 de hello niveles han ido retirando?

niveles de rendimiento S1, S2 y S3 Hola hacerlo no ofrece Hola una gran flexibilidad que ofrece colecciones de API de documentos. Con hello S1, S2, S3 los niveles de rendimiento, la capacidad de rendimiento y almacenamiento de ambos Hola previamente se establecieron y no ofrecía elasticidad. Azure DB Cosmos ahora ofrece Hola capacidad toocustomize su rendimiento y almacenamiento, que ofrece mucha más flexibilidad en su tooscale capacidad según cambien sus necesidades.

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-toohello-s1-s2-s3-performance-levels"></a>¿Cómo colecciones de una sola partición y con particiones se comparan toohello S1, S2, S3 los niveles de rendimiento?

Hello en la tabla siguiente compara las opciones de rendimiento y almacenamiento de hello disponibles en las colecciones de partición única, las colecciones particionadas y S1, S2, S3 los niveles de rendimiento. Este es un ejemplo para la región Este de EE. UU. - 2:

|   |Colección con particiones|Colección de partición única|S1|S2|S3|
|---|---|---|---|---|---|
|Rendimiento máximo|Ilimitado|10 000 RU/s|250 RU/s|1000 RU/s|2500 RU/s|
|Rendimiento mínimo|2500 RU/s|400 RU/s|250 RU/s|1000 RU/s|2500 RU/s|
|Almacenamiento máximo|Ilimitado|10 GB|10 GB|10 GB|10 GB|
|Precio (mensual)|Rendimiento: 6 USD / 100 RU/s<br><br>Almacenamiento: 0,25 USD/GB|Rendimiento: 6 USD / 100 RU/s<br><br>Almacenamiento: 0,25 USD/GB|25 USD|50 USD|100 USD|

¿Es un cliente de EA? Si es así, consulte [¿Cómo me afecta si soy un cliente de EA?](#ea-customer)

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-toodo-tooensure-uninterrupted-access-toomy-data"></a>¿Qué necesita toodo tooensure sin interrupciones, tener acceso a datos de toomy?

Nada, Cosmos DB controla la migración de Hola para usted. Si tiene una colección de S1, S2 o S3, la colección actual será la colección de una sola partición de tooa migrados en el 31 de julio de 2017. 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-hello-migration"></a>¿Cómo cambiará Mi colección después de la migración de hello?

Si tiene una colección de S1, es posible que tooa migrados de colección de una sola partición con rendimiento de 400 RU/s. 400 RU/s es el rendimiento más bajo de hello disponible con colecciones de una sola partición. Sin embargo, costo de Hola de 400 RU/s en una colección de una sola partición es aproximadamente Hola igual a la se pagan con la colección de S1 de Hola y RU 250/s, por lo que no va a pagar de Hola extra 150 tooyou de RU/s disponibles.

Si tiene una colección de S2, es posible que tooa migrados de colección de una sola partición con 1 K RU/s. No podrá ver ningún nivel de rendimiento de tooyour de cambio.

Si tiene una colección de S3, es posible que tooa migrados colección de una sola partición con 2,5 K RU/s. No podrá ver ningún nivel de rendimiento de tooyour de cambio.

En cada uno de estos casos, después de migra la colección, se ser capaz de toocustomize su nivel de rendimiento o ampliarlo arriba o abajo como usuarios de tooyour de acceso de baja latencia tooprovide necesarios. nivel de rendimiento de hello toochange después de migra la colección, solo tiene que abrir su cuenta de base de datos de Cosmos Hola portal de Azure, haga clic en la escala, elija la colección y, a continuación, ajustar el nivel de rendimiento de hello, tal y como se muestra en la siguiente captura de pantalla de hello:

![¿Cómo tooscale rendimiento en Hola portal de Azure](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-toohello-single-partition-collections"></a>¿Cómo cambiará mi facturación después soy colecciones de partición únicas toohello migrados?

Suponiendo que tiene 10 colecciones de S1, 1 GB de almacenamiento para cada uno, en la región Este de EE. de hello, y migrar estas 10 colecciones de una única partición de S1 colecciones too10 en 400 RU/seg. (nivel mínimo de hello). Su factura será como se indica a continuación si mantiene colecciones de partición única 10 Hola durante un mes completo:

![Cómo comparan la S1 precios para 10 colecciones de colecciones de too10 con precios para una colección de una única partición](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a>¿Qué ocurre si necesito más de 10 GB de almacenamiento?

Si dispone de una colección con un nivel de rendimiento S1, S2 o S3 o tiene una colección de una sola partición, todos los cuales tienen 10 GB de almacenamiento disponible, se puede utilizar toomigrate de herramienta de migración de datos de base de datos de Cosmos Hola su tooa de datos con particiones colección con prácticamente almacenamiento ilimitado. Para obtener información acerca de las ventajas de Hola de una colección con particiones, vea [particiones y ajuste de escala en la base de datos de Azure Cosmos](documentdb-partition-data.md). Para obtener información acerca de cómo toomigrate sus, S1, S2, S3 o colección de tooa particionado de colección de una sola partición, vea [migrar de colecciones de partición único toopartitioned](documentdb-partition-data.md#migrating-from-single-partition). 

<a name="change-before"></a>

## <a name="can-i-change-between-hello-s1-s2-and-s3-performance-levels-before-august-1-2017"></a>¿Se puede cambiar entre los niveles de rendimiento de hello S1, S2 y S3 antes del 1 de agosto de 2017?

Solo las cuentas existentes con rendimiento S1, S2 y S3 se capaz de toochange y modificar los niveles de nivel de rendimiento a través del portal de Hola o mediante programación. El 1 de agosto de 2017 Hola S1, S2, y los niveles de rendimiento S3 dejará de estar disponibles. Si cambia de la colección de una sola partición tooa S1, S3 o S3, no puede devolver toohello los niveles de rendimiento S1, S2 o S3.

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a>¿Cómo puedo saber cuándo ha migrado mi colección?

migración de Hola se producirá en el 31 de julio de 2017. Si tiene una colección que usa Hola S1, S2 o S3 los niveles de rendimiento, equipo de base de datos de Cosmos Hola pondremos en contacto contigo por correo electrónico antes de migración de hello tiene lugar. Una vez completada, migración de hello en el 1 de agosto de 2017 hello Azure portal mostrará que la colección utiliza precios estándar.

![¿Cómo tooconfirm la colección ha migrado toohello de tarifa estándar](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-hello-s1-s2-s3-performance-levels-toosingle-partition-collections-on-my-own"></a>¿Cómo migrar de hello S1, S2, S3 rendimiento niveles toosingle las colecciones de partición en mi propio?

Puede migrar de hello S1, S2, y las colecciones de partición toosingle con hello portal de Azure de niveles de rendimiento de S3 o mediante programación. Puede hacer esto en su propia antes toobenefit el 1 de agosto de opciones de rendimiento flexible de hello disponibles con colecciones de partición únicas o Migraremos las colecciones para usted en el 31 de julio de 2017.

**colecciones de partición de toosingle toomigrate mediante Hola portal de Azure**

1. Hola [ **portal de Azure**](https://portal.azure.com), haga clic en **base de datos de Azure Cosmos**, a continuación, seleccione toomodify de cuenta de base de datos de Cosmos Hola. 
 
    Si **base de datos de Azure Cosmos** no está en Hola Jumpbar, haga clic en >, desplácese demasiado**bases de datos**, seleccione **base de datos de Azure Cosmos**y, a continuación, seleccione la cuenta de DocumentDB de Hola.  

2. En el menú de recursos de hello, en **contenedores**, haga clic en **escala**, seleccione hello toomodify de colección de lista desplegable de hello y, a continuación, haga clic en **tarifa**. Las cuentas con un rendimiento predefinido tienen un plan de tarifa de S1, S2 o S3.  Hola **elegir el nivel de precios** hoja, haga clic en **estándar** toochange definido por el toouser rendimiento y, a continuación, haga clic en **seleccione** toosave el cambio.

    ![Captura de pantalla de hoja de configuración de hello, que muestra dónde toochange Hola valor de rendimiento](./media/performance-levels/change-performance-set-thoughput.png)

3. En hello **escala** hoja, hello **tarifa** cambia demasiado**estándar** hello y **(RU/s) de rendimiento** cuadro se muestra con un valor predeterminado de 400. Rendimiento de hello conjunto entre 400 y 10.000 [unidades de solicitud ](request-units.md) /segundo (RU/s). Hola **factura mensual estimado** final Hola de hello página actualiza automáticamente tooprovide una estimación de costo mensual de Hola. 

    >[!IMPORTANT] 
    > Una vez que guarde los cambios y mover el nivel de precios estándar toohello, no puede revertir toohello los niveles de rendimiento S1, S2 o S3.

4. Haga clic en **guardar** toosave los cambios.

    Si cree que necesita más rendimiento (superior a 10 000 RU/s) o espacio de almacenamiento (mayor que 10 GB), puede crear una colección con particiones. toomigrate una colección de tooa particiones de colección de una sola partición, vea [migrar de colecciones de partición único toopartitioned](documentdb-partition-data.md#migrating-from-single-partition).

    > [!NOTE]
    > Cambiar de S1, S2 o S3 tooStandard puede tardar minutos too2.
    > 
    > 

**colecciones de partición de toosingle toomigrate mediante Hola SDK para .NET**

Otra opción para cambiar los niveles de rendimiento de las colecciones es a través de nuestros SDK. Esta sección solo incluyen cambiar el rendimiento de la colección con el nivel nuestro [API de .NET de DocumentDB](documentdb-sdk-dotnet.md), pero el proceso de hello es similar para nuestro otros SDK.

Este es un fragmento de código para cambiar too5 de rendimiento de recopilación de hello, 000 unidades de solicitud por segundo:
    
```C#
    //Fetch hello resource toobe updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set hello throughput too5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes toohello database by replacing hello original resource
    await client.ReplaceOfferAsync(offer);
```

Visite [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) tooview otros ejemplos y obtener más información sobre nuestros métodos de oferta:

* [**ReadOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [**ReadOffersFeedAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [**ReplaceOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [**CreateOfferQuery**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a>¿Cómo me afecta si soy un cliente de EA?

Los clientes EA será precio protegido hasta el final de Hola de su contrato actual.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información sobre precios y administrar datos con la base de datos de Azure Cosmos explorar estos recursos:

1.  [Partición de datos en Cosmos DB](documentdb-partition-data.md). Comprender la diferencia de hello entre el contenedor de una sola partición y contenedores con particiones, así como sugerencias sobre cómo implementar una partición tooscale estrategia sin problemas.
2.  [Precios de Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/). Obtenga información sobre el costo de Hola de aprovisionamiento de rendimiento y consumo de almacenamiento.
3.  [Unidades de solicitud](request-units.md). Comprender el consumo de Hola de rendimiento para los tipos de operación diferente, consulta de lectura, escritura, por ejemplo.
