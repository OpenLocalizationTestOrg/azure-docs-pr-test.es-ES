---
title: "conmutación por error de aaaRegional en la base de datos de Azure Cosmos | Documentos de Microsoft"
description: "Obtenga información sobre el modo en que funciona la conmutación por error manual y automática con Azure Cosmos DB."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 446e2580-ff49-4485-8e53-ae34e08d997f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2fdc7b0e8958d129ab027e4b11193b12961ddae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-regional-failover-for-business-continuity-in-azure-cosmos-db"></a>Conmutación por error regional automática para la continuidad empresarial en Azure Cosmos DB
Base de datos de Azure Cosmos simplifica la distribución global de Hola de los datos mediante totalmente administrados, [cuentas de base de datos de varias regiones](distribute-data-globally.md) que proporcionan desactive contrapartidas entre coherencia, disponibilidad y rendimiento, todos los datos con correspondiente garantías. Las cuentas de COSMOS DB ofrecen alta disponibilidad, las latencias de ms de un dígito, [niveles de coherencia bien definido](consistency-levels.md), transparente conmutación por error regional con las API de hospedaje múltiple y el rendimiento de escala de tooelastically de capacidad de Hola y el almacenamiento todo el mundo de Hola. 

COSMOS DB admite tanto explícita y controlada por directivas las conmutaciones por error que le permiten comportamiento de extremo a otro sistema de hello toocontrol en caso de hello de errores. En este artículo, nos centramos en los siguientes temas:

* Funcionamiento de las conmutaciones por error manuales en Cosmos DB
* Funcionamiento de las conmutaciones por error automáticas en Cosmos DB y efectos del bloqueo de un centro de datos
* Uso de las conmutaciones por error manuales en arquitecturas de aplicación

También obtendrá más información sobre las conmutaciones por error en este vídeo de Azure Friday con Scott Hanselman y el administrador de ingeniería principal Karthik Raman.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

## <a id="ConfigureMultiRegionApplications"></a>Configuración de aplicaciones de varias regiones
Antes de profundizar en los modos de conmutación por error, veremos cómo puede configurar una ventaja de tootake de aplicación de la disponibilidad de varias regiones y ser resistente a errores en la cara de Hola de las conmutaciones por error regional.

* En primer lugar, implemente su aplicación en varias regiones.
* acceso de baja latencia tooensure de cada región de su aplicación se implementa, configurar Hola correspondiente [lista de regiones preferido](https://msdn.microsoft.com/library/microsoft.azure.documents.client.connectionpolicy.preferredlocations.aspx#P:Microsoft.Azure.Documents.Client.ConnectionPolicy.PreferredLocations) para cada región a través de una de hello compatibles SDK.

Hola fragmento siguiente muestra cómo tooinitialize una aplicación de varias regiones. Hola en este caso, la cuenta de base de datos de Azure Cosmos `contoso.documents.azure.com` se configura con dos regiones - oeste de Estados Unidos y Europa del Norte. 

* aplicación Hello se implementa en la región Oeste de Estados Unidos de hello (mediante servicios de aplicaciones de Azure por ejemplo) 
* Configurado con `West US` como primera región preferida Hola de baja latencia lee
* Configurado con `North Europe` como segunda región preferida hello (para lograr alta disponibilidad durante los errores de regionales)

En hello API de documentos, esta configuración es similar a Hola siguiente fragmento de código:

```cs
ConnectionPolicy usConnectionPolicy = new ConnectionPolicy 
{ 
    ConnectionMode = ConnectionMode.Direct,
    ConnectionProtocol = Protocol.Tcp
};

usConnectionPolicy.PreferredLocations.Add(LocationNames.WestUS);
usConnectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

DocumentClient usClient = new DocumentClient(
    new Uri("https://contosodb.documents.azure.com"),
    "memf7qfF89n6KL9vcb7rIQl6tfgZsRt5gY5dh3BIjesarJanYIcg2Edn9uPOUIVwgkAugOb2zUdCR2h0PTtMrA==",
    usConnectionPolicy);
```

aplicación Hello también se implementa en la región de Europa del Norte de hello con orden de Hola de regiones preferidas invertidas. Es decir, región de Europa del Norte Hola se especifica primero para lecturas de latencia baja. A continuación, región del oeste de Estados Unidos de Hola se especifica como segunda región preferida Hola para lograr alta disponibilidad durante errores regionales.

Hello arquitectura diagrama siguiente muestra una implementación de aplicación de varias regiones donde DB Cosmos y aplicación hello son configurado toobe disponible en cuatro regiones geográficas de Azure.  

![Implementación de aplicaciones distribuidas globalmente con Azure Cosmos DB](./media/regional-failover/app-deployment.png)

Ahora, echemos un vistazo a cómo Hola DB Cosmos servicio controla regionales errores a través de las conmutaciones por error automática. 

## <a id="AutomaticFailovers"></a>Conmutaciones por error automáticas
En hello extraño caso de una interrupción regional Azure o la interrupción del centro de datos, base de datos de Cosmos desencadena automáticamente la conmutaciones por error de todas las cuentas de base de datos de Cosmos con presencia en la región de hello afectado. 

**¿Qué ocurre si una región de lectura sufre una interrupción?**

Las cuentas de COSMOS DB con una región de lectura en una de las regiones de hello afectado automáticamente se desconecta de su región de escritura y marcado como sin conexión. Hola Cosmos DB SDK implementan un protocolo de detección regionales que les permita tooautomatically detectar cuándo está disponible una región y redirección lee región disponible de llamadas toohello siguiente en lista de región preferida de Hola. Si ninguna de las regiones de Hola Hola preferido está disponible la lista de regiones, llamadas recurren automáticamente toohello actual región de escritura. Se requiere ningún cambio en la aplicación código toohandle regional las conmutaciones por error. Durante este proceso, garantías de coherencia continúan toobe cumple con la base de datos de Cosmos.

![Errores de la región de lectura en Azure Cosmos DB](./media/regional-failover/read-region-failures.png)

Una vez que la región de hello afectado se recupera de interrupción de hello, se recuperan automáticamente todas las cuentas de Cosmos DB Hola afectado en la región de hello servicio Hola. Cuentas de COSMOS DB que tenía una región de lectura en la región de hello afectado se, a continuación, automáticamente la sincronización con la actual región de escritura y activar en línea. Hola Cosmos DB SDK detectar la disponibilidad de hello de la nueva región de Hola y evaluar si la región de hello debe seleccionarse como región de lectura actual hello en función de lista de región preferida de hello establecida por aplicación Hola. Lecturas posteriores son toohello redirigida recuperada región sin necesidad de cualquier código de aplicación de tooyour de cambios.

**¿Qué ocurre si una región de escritura sufre una interrupción?**

Si región afectada hello es la región de escritura actual de Hola para una cuenta de base de datos de Cosmos determinada, a continuación, región de hello automáticamente marcará como sin conexión. A continuación, se promueve una región alternativa como Hola escribir región cada cuenta de base de datos de Cosmos afectada. Puede controlar completamente orden de selección de región de Hola para las cuentas de base de datos de Cosmos a través del portal de Azure de Hola o [mediante programación](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_FailoverPriorityChange). 

![Prioridades de conmutación por error de Azure Cosmos DB](./media/regional-failover/failover-priorities.png)

Durante la conmutación por error automática, Cosmos DB elige automáticamente la siguiente área de la escritura de Hola para una determinada base de datos de Cosmos cuenta según Hola especifica el orden de prioridad. 

![Errores de la región de escritura en Azure Cosmos DB](./media/regional-failover/write-region-failures.png)

Una vez que la región de hello afectado se recupera de interrupción de hello, se recuperan automáticamente todas las cuentas de Cosmos DB Hola afectado en la región de hello servicio Hola. 

* Las cuentas de COSMOS DB con su región de escritura anterior en la región de hello afectado permanecerá en un modo sin conexión con la disponibilidad de lectura incluso después de la recuperación de Hola de región de Hola. 
* Puede consultar esta región toocompute todas las escrituras no replicadas durante la interrupción de hello mediante la comparación con datos de hello disponibles en la región actual de escritura de Hola. Según las necesidades de saludo de la aplicación, puede realizar la resolución de conflictos o de mezcla y escribir Hola conjunto final de la región actual de escritura de cambios toohello back. 
* Una vez que haya completado combinar los cambios, puede dar región Hola afectado nuevo en línea quitar y volver a agregar cuenta de hello región tooyour Cosmos DB. Una vez que se volvió a región hello, puede configurar como área de escritura de hello mediante la realización de una conmutación por error manual a través del portal de Azure de Hola o [mediante programación](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate).

## <a id="ManualFailovers"></a> Conmutaciones por error manuales

Además tooautomatic las conmutaciones por error, Hola actual escribir región de una cuenta de base de datos de Cosmos determinada puede cambiarse manualmente dinámicamente tooone de hello regiones de lectura existente. Las conmutaciones por error manual se pueden iniciar a través del portal de Azure de Hola o [mediante programación](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate). 

Asegúrese de conmutaciones por error manuales **cero pérdida de datos** y **cero disponibilidad** pérdida y correctamente el estado de escritura de transferencia de hello antiguo escriben región toohello uno nuevo para hello la cuenta de base de datos de Cosmos especificada. Al igual que en la conmutación por error automática, Hola Cosmos DB SDK automáticamente identificadores de escribir región cambia durante las conmutaciones por error manual y garantiza que las llamadas son toohello redirigido automáticamente una nueva área de escritura. Se requiere ningún cambio de código o configuración de la conmutación por error de aplicación toomanage. 

![Conmutaciones por error manuales de Azure Cosmos DB](./media/regional-failover/manual-failovers.png)

Algunos escenarios comunes de Hola donde la conmutación por error manual puede ser útil son:

**Siga el modelo de reloj de Hola**: si las aplicaciones tienen patrones de tráfico de predicción según el tiempo de hello del día de hello, puede cambiar periódicamente Hola escritura estado toohello más activo región geográfica en función de la hora del día en Hola.

**Actualización de servicio**: puede implicar cierto implementación de aplicación distribuida globalmente reenrutamiento región toodifferent de tráfico a través del Administrador de tráfico durante la actualización de servicio planeada. Ahora la implementación de dicha aplicación puede usar conmutación por error manual región de toohello de la estado de tookeep Hola escritura donde habrá tráfico active toobe durante la ventana de actualización de servicio de hello.

**Exploraciones de continuidad empresarial y recuperación ante desastres (BCDR) y alta disponibilidad y recuperación ante desastres (HADR)**: la mayoría de las aplicaciones empresariales incluyen pruebas de continuidad empresarial en su proceso de desarrollo y de lanzamiento. BCDR y las pruebas de HADR es a menudo un paso importante en certificaciones de cumplimiento de normas y garantiza disponibilidad del servicio en caso de hello de interrupciones regionales. Puede probar la preparación BCDR Hola de las aplicaciones que usan DB Cosmos para almacenamiento desencadenar una conmutación por error manual de la cuenta de base de datos de Cosmos o agregando y quitando una región de forma dinámica.

En este artículo, se revisan cómo manuales y automáticas trabajo conmutaciones por error en la base de datos de Cosmos y cómo puede configurar su toobe de cuentas y las aplicaciones de base de datos de Cosmos disponible globalmente. Utilizando el soporte de replicación global de Cosmos DB, puede mejorar la latencia de extremo a extremo y asegurarse de que son altamente disponibles incluso en caso de hello de errores de la región. 

## <a id="NextSteps"></a>Pasos siguientes
* Obtenga información sobre la compatibilidad de Cosmos DB con la [distribución global](distribute-data-globally.md)
* Más información sobre la [coherencia global con Azure Cosmos DB](consistency-levels.md)
* Desarrollo con varias regiones con la [API de DocumentDB](../cosmos-db/tutorial-global-distribution-documentdb.md) de Azure Cosmos DB
* Obtenga información acerca de cómo toobuild [arquitecturas de sistema de escritura de varias regiones](multi-region-writers.md) con documentos de Azure

