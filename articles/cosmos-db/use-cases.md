---
title: aaaCommon usar casos y escenarios de base de datos de Azure Cosmos | Documentos de Microsoft
description: "Obtenga información acerca de la parte superior de hello cinco casos de uso para la base de datos de Azure Cosmos: generado por el usuario contenido, el registro de eventos, datos del catálogo, datos de las preferencias de usuario y Internet de las cosas (IoT)."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: eca68a58-1a8c-4851-8cf8-6e4d2b889905
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: mimig
ms.openlocfilehash: 115a418e7b18d5033c4d7e64591bf302aea0190b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="common-azure-cosmos-db-use-cases"></a>Casos de uso comunes de Azure Cosmos DB
En este artículo se proporciona información general acerca de varios casos de uso comunes de Azure Cosmos DB.  recomendaciones de Hello en este artículo servir como punto de partida a medida que desarrolla la aplicación con la base de datos de Cosmos.   

Después de leer este artículo, podrá hello tooanswer pueda siguientes preguntas: 

* ¿Qué casos de uso comunes de hello para la base de datos de Azure Cosmos?
* ¿Cuáles son las ventajas de hello del uso de base de datos de Azure Cosmos para las aplicaciones comerciales?
* ¿Cuáles son las ventajas de Hola de usar base de datos de Azure Cosmos como un almacén de datos para los sistemas de Internet de las cosas (IoT)?
* ¿Cuáles son las ventajas de hello del uso de base de datos de Azure Cosmos para aplicaciones web y móviles?

## <a name="introduction"></a>Introducción
[Azure Cosmos DB](../cosmos-db/introduction.md) es un servicio de base de datos de distribución global de Microsoft. servicio Hello está diseñada tooallow clientes tooelastically (y de forma independiente) escalar el almacenamiento y rendimiento a través de cualquier número de regiones geográficas. Base de datos de Azure Cosmos es Hola primer servicio de base de datos distribuidos globalmente en hello mercado toooffer hoy completa [contratos de nivel de servicio](https://azure.microsoft.com/support/legal/sla/cosmos-db/) que abarca el rendimiento, latencia, disponibilidad y coherencia. 

proyecto de base de datos de Azure Cosmos Hola inició en 2011 como "Proyecto Florence" tooaddress developer dolor puntos que se enfrentan grandes aplicaciones de escala de Internet en Microsoft. Observar que estos problemas no son aplicaciones del único tooMicrosoft, decidimos toomake base de datos de Azure Cosmos tooexternal disponible con carácter general a los desarrolladores de 2015 en forma de Hola de [Azure DocumentDB](https://azure.microsoft.com/blog/documentdb-moving-to-general-availability/). servicio de Hello es omnipresentes internamente en Microsoft y es uno de los servicios de más rápido crecimiento de Hola utilizados por los desarrolladores de Azure en externamente. 

Azure Cosmos DB es una base de datos con varios modelos y de distribución global que se usa en una amplia variedad de aplicaciones y casos de uso. Es una buena elección para cualquier [sin servidor](http://azure.com/serverless) aplicación que necesita tiempos de respuesta de pedido de milisegundo baja y necesita tooscale rápidamente y global. Admite varios modelos de datos (clave-valor, documentos, grafos y columnas) y muchas API para acceso de datos, entre las que se incluyen [MongoDB](mongodb-introduction.md), [DocumentDB SQL](documentdb-introduction.md), [Gremlin](graph-introduction.md) y [Azure Tables](table-introduction.md) de forma nativa y de forma extensible. 

Hola algunos atributos de base de datos de Azure Cosmos que hacen que sea ideal para aplicaciones de alto rendimiento con ambición global son.

* Azure Cosmos DB crea de forma nativa particiones para sus datos a fin de ofrecer una alta disponibilidad y escalabilidad. Azure Cosmos DB garantiza un 99,99 % de disponibilidad, rendimiento, baja latencia y coherencia.
* Azure Cosmos DB cuenta con almacenamiento respaldado por SSD con tiempos de respuesta con una reducida latencia, de milisegundos.
* La compatibilidad de Azure Cosmos DB con niveles de coherencia, como eventual, prefijo coherente, sesión y obsolescencia entrelazada, permite disfrutar de una flexibilidad completa y una excelente relación precio-rendimiento. Ningún servicio de base de datos ofrece la flexibilidad que ofrece Azure Cosmos DB en la coherencia de niveles. 
* Azure Cosmos DB presenta un modelo de precios flexible e idóneo para los datos que mide el almacenamiento y el rendimiento por separado.
* Modelo de rendimiento reservados de Azure DB Cosmos permite toothink en cuanto al número de lecturas/escrituras en lugar de CPU/memoria y e/s por segundo de hello subyacente de hardware.
* Diseño le permite del Azure Cosmos base de datos de que escalar los volúmenes de solicitud de toomassive Hola orden de trillones de solicitudes al día.

Estos atributos son beneficiosos en web, móvil, juegos y aplicaciones de IoT que necesitan tiempos de respuesta baja y necesitan toohandle grandes cantidades de lecturas y escrituras.

## <a name="iot-and-telematics"></a>IoT y telemáticas
A menudo, los casos de uso de IoT comparten algunos patrones en el modo de ingerir, procesar y almacenar datos.  En primer lugar, estos sistemas deben tooingest ráfagas de datos de sensores de dispositivo de varias configuraciones regionales. A continuación, estos sistemas procesan y analizar información en tiempo real de transmisión por secuencias datos tooderive. datos de Hello están, a continuación, archivado toocold almacenamiento para el análisis por lotes. Microsoft Azure ofrece sofisticados servicios que pueden aplicarse a los casos de uso de IoT, incluidos Azure Cosmos DB, Azure Event Hubs, Azure Stream Analytics, Azure Notification Hub, Azure Machine Learning, Azure HDInsight y PowerBI. 

![Arquitectura de referencia de IoT de Azure Cosmos DB](./media/use-cases/iot.png)

Las ráfagas de datos pueden ser asumidas por los Centros de eventos de Azure, ya que ofrecen una ingesta de datos de alto rendimiento con baja latencia. Datos ingeridos que necesita toobe procesado para obtener información en tiempo real pueden ser dirigida tooAzure análisis de transmisiones de análisis en tiempo real. Los datos pueden cargarse en Azure Cosmos DB para realizar consultas ad hoc. Una vez que se cargan datos de hello en la base de datos de Azure Cosmos, datos de hello están listo toobe consultada. Además, los datos nuevos y cambios tooexisting datos se pueden leer en fuente de cambio. Cambiar fuente es un persistente, anexe solo cambia de registro que almacena las colecciones de tooCosmos DB en orden secuencial. Hola que todos los datos o simplemente cambios toodata en la base de datos de Azure Cosmos puede usarse como datos de referencia como parte del análisis en tiempo real. Además, además se pueden refinados y procesados por conexión tooHDInsight de datos de base de datos de Azure Cosmos para trabajos de Pig, Hive o asignación y reducción datos.  Datos refinados, a continuación, se cargan tooAzure back-DB Cosmos para crear informes.   

Para una solución de IoT de ejemplo con base de datos de Azure Cosmos, EventHubs y Storm, vea hello [repositorio de ejemplos de aluvión de hdinsight en GitHub](https://github.com/hdinsight/hdinsight-storm-examples/).

Para obtener más información sobre las ofertas de IoT de Azure, consulte [crear Hola Internet de las cosas Your](http://www.microsoft.com/server-cloud/internet-of-things.aspx). 

## <a name="retail-and-marketing"></a>Minoristas y marketing
Base de datos de Azure Cosmos se utiliza habitualmente en plataformas de comercio electrónico de Microsoft, que se ejecutan de la tienda de Windows hello y XBox Live. También se utiliza en el sector minorista de Hola para almacenar los datos del catálogo y de evento de origen en las canalizaciones de procesamiento de pedidos.

Entre los escenarios de uso de los datos de catálogo se encuentra el almacenamiento y la consulta de un conjunto de atributos para entidades como personas, lugares y productos. Algunos ejemplos de datos de catálogo son las cuentas de usuario, los catálogos de productos, los registros de dispositivo IoT y los sistemas de lista de materiales. Atributos de estos datos pueden variar y pueden cambiar con requisitos de la aplicación de tiempo toofit.

Piense por ejemplo en un catálogo de productos para un proveedor de piezas para vehículos. Todos los elementos pueden tener sus propios atributos en suma toohello los atributos comunes que comparten todas las partes. Además, los atributos de una parte específica pueden cambiar Hola tras año cuando se publica un nuevo modelo. Azure Cosmos DB admite esquemas flexibles y datos jerárquicos, y por ello es adecuado para almacenar los datos del catálogo de productos.

![Arquitectura de referencia del catálogo de minoristas de Azure Cosmos DB](./media/use-cases/product-catalog.png)

Base de datos de Azure Cosmos se suele utilizar para eventos subcontratación toopower arquitecturas de orientada a eventos mediante su [Cambiar fuente](change-feed.md) funcionalidad. fuente de cambio de Hello proporciona microservicios siguen en la cadena Hola tooreliably de capacidad y los inserta incrementalmente de lectura y las actualizaciones (por ejemplo, eventos desordenados) están tooan base de datos de Azure Cosmos. Esta funcionalidad puede ser aprovechado tooprovide un evento persistente se almacenan como un agente de mensajes para los eventos de cambio de estado y flujo de trabajo del procesamiento de orden de unidad entre muchos microservicios (que se puede implementar como [funciones de Azure sin servidor](http://azure.com/serverless)).

![Arquitectura de referencia para la ordenación de las canalizaciones de Azure Cosmos DB](./media/use-cases/event-sourcing.png)

Además, los datos almacenados en Azure Cosmos DB pueden integrarse con HDInsight para el análisis de macrodatos a través de trabajos de Apache Spark. Para obtener detalles sobre Hola conector Spark para base de datos de Azure Cosmos, consulte [ejecutar un trabajo de Spark con base de datos de Cosmos y HDInsight](spark-connector.md).

## <a name="gaming"></a>Juegos
nivel de base de datos de Hello es un componente fundamental de las aplicaciones de juegos. Los juegos más modernos realizan el procesamiento de gráficos en los clientes móviles/consola, pero se basan en hello en la nube toodeliver personalizado y contenido personalizado, como estadísticas de juego, integración de redes sociales y tablas de líderes de puntuaciones máximas. A menudo, los juegos requieren latencias de milisegundo solo para las lecturas y escribe tooprovide una experiencia de juego fomentar la participación. Una base de datos de juego necesita toobe rápido y ser capaz de toohandle picos masivos en velocidad de solicitudes durante inicia juego nuevos y actualizaciones de características.

Base de datos de Azure Cosmos es usado por juegos como [Hola recorrer muertos: tierra del n "hombre"](https://azure.microsoft.com/blog/the-walking-dead-no-mans-land-game-soars-to-1-with-azure-documentdb/) por [juegos siguiente](http://www.nextgames.com/), y [Halo 5: tutores](https://azure.microsoft.com/blog/how-halo-5-guardians-implemented-social-gameplay-using-azure-documentdb/). Base de datos de Azure Cosmos proporciona siguiente Hola beneficia a los desarrolladores de toogame:

* Base de datos de Azure Cosmos permite toobe rendimiento escalada hacia arriba o abajo de forma elástica. Esto permite actualizar el perfil y estadísticas entre docenas de toohandle de juegos toomillions de jugadores simultáneas mediante la realización de una sola llamada API.
* Azure admite la base de datos de Cosmos milisegundo las lecturas y escrituras toohelp evitar los retrasos durante el juego.
* La indexación automática de Azure Cosmos DB permite filtrar por varias propiedades distintas en tiempo real (por ejemplo, ubicar a jugadores por sus identificadores internos de jugador o de Game Center, Facebook o Google, o bien consultar según la pertenencia del jugador a un gremio). Esto es posible sin crear una infraestructura compleja de indexación o particionamiento.
* Características sociales, incluidos los mensajes de chat en juego, pertenencias a grupos de Reproductor guild, desafíos completados, tablas de líderes de puntuaciones máximas y gráficos sociales son tooimplement más fácil con un esquema flexible.
* Azure DB Cosmos como un administrado plataforma como-servicio (PaaS) el programa de instalación mínima y tooallow de trabajo de administración necesarios para iteración rápido y reducir toomarket de tiempo.

![Arquitectura de referencia de juegos de Azure Cosmos DB](./media/use-cases/gaming.png)

## <a name="web-and-mobile-applications"></a>Aplicaciones web y móviles
Azure Cosmos DB se usa normalmente en aplicaciones web y móviles y sirve para modelar interacciones sociales, para la integración con servicios de terceros y para la creación de experiencias personalizadas enriquecidas. Hola Cosmos DB SDK puede ser compilación usado completas aplicaciones de iOS y Android mediante Hola popular [Xamarin framework](mobile-apps-with-xamarin.md).  

### <a name="social-applications"></a>Aplicaciones sociales
Un caso de uso común para la base de datos de Azure Cosmos es toostore y consulta de contenido generado por los usuarios (UGC) para web, aplicaciones móviles y sociales multimedia. Algunos ejemplos de contenido generado por usuarios son las sesiones de chat, los tweets, las entradas de blog, las valoraciones y los comentarios. Hola UGC en aplicaciones de medios sociales suele ser una combinación de texto sin formato, propiedades, etiquetas y las relaciones que no están limitadas por estructura rígida. Contenido, como chats, comentarios y publicaciones pueden almacenarse en la base de datos de Cosmos sin necesidad de niveles de asignación de objeto complejo toorelational o transformaciones.  Propiedades de datos se pueden agregar o modifican fácilmente toomatch requisitos según los desarrolladores iteración sobre el código de la aplicación hello, por tanto, promover el desarrollo rápido.  

Las aplicaciones que se integran con las redes sociales de terceros deben responder toochanging esquemas de estas redes. Como se indizan automáticamente los datos de forma predeterminada en la base de datos de Cosmos, los datos son toobe listo consultado en cualquier momento. Por lo tanto, estas aplicaciones tienen las proyecciones de hello flexibilidad tooretrieve según sus necesidades respectivas.

Muchas de las aplicaciones sociales de hello ejecutan a escala global y pueden ofrecer los patrones de uso impredecible. Flexibilidad para escalar el almacén de datos de hello es esencial, ya que escala de nivel de aplicación Hola toomatch demanda de uso.  Es posible escalar horizontalmente mediante la adición de particiones de datos adicionales a una cuenta de Cosmos DB.  Además, también puede crear cuentas adicionales de Cosmos DB en varias regiones. Para ver la disponibilidad del servicio de Cosmos DB por regiones, consulte [Regiones de Azure](https://azure.microsoft.com/regions/#services).

![Arquitectura de referencia de aplicaciones web de Azure Cosmos DB](./media/use-cases/apps-with-global-reach.png)

### <a name="personalization"></a>Personalización
En la actualidad, las aplicaciones modernas incluyen experiencias y vistas complejas. Se trata normalmente dinámicos y la restauración toouser preferencias o humor y las necesidades de personalización de marca. Por lo tanto, las aplicaciones necesitan toobe tooretrieve pueda personalizar configuración toorender eficazmente los elementos de interfaz de usuario y experiencias rápidamente. 

JSON, un formato compatible con la base de datos de Cosmos, es un datos de diseño de interfaz de usuario de toorepresent formato efectivos solo no es ligera; sin embargo, también puede interpretar fácilmente mediante JavaScript. Cosmos DB ofrece niveles de coherencia ajustables que permiten lecturas rápidas con escrituras de baja latencia. Por lo tanto, almacenar datos de diseño de interfaz de usuario incluida la configuración personalizada como documentos JSON en la base de datos de Cosmos es un medio eficaz tooget estos datos a través de conexión de Hola.

![Arquitectura de referencia de aplicaciones web de Azure Cosmos DB](./media/use-cases/personalization.png)

## <a name="next-steps"></a>Pasos siguientes
tooget a trabajar con la base de datos de Azure Cosmos, siga nuestro [rápidas](create-documentdb-dotnet.md), que le guían por la creación de una cuenta e Introducción a base de datos de Cosmos. 

O bien, si desea más información acerca de los clientes que usan DB Cosmos tooread, hello historias de clientes siguientes están disponibles:

* [Jet.com](https://jet.com). Challenger de comercio electrónico ojos Hola primer lugar, se ejecuta en la nube de Microsoft hello, aprovecha Cosmos DB en una escala global.
* [Asos.com](http://www.asos.com/). Asos.com es una tienda británica en línea de moda y artículos de belleza. Dirigida principalmente a adultos jóvenes, Asos vende más de 850 marcas, además de su propia gama de vestuario y accesorios.
* [Toyota](https://www.toyota.com/). Toyota Motor Corporation es un fabricante de automóviles japonés. Toyota usó Cosmos DB para una aplicación de IoT a nivel mundial.
* [Citrix](https://customers.microsoft.com/story/citrix). Citrix desarrolla una solución de inicio de sesión único con Azure Service Fabric y Azure Cosmos DB
* [TEXA](https://customers.microsoft.com/story/texaspa) La revolucionaria solución IoT de TEXA para propietarios de vehículos permite ahorrar tiempo, dinero y combustible... y posiblemente salvar vidas.
* [Domino's Pizza](https://www.dominos.com). Domino's Pizza Inc. es una cadena de pizzerías de Estados Unidos.
* [Johnson Controls](http://www.johnsoncontrols.com). Johnson Controls es un líder en tecnología diversificada y de varios sectores a nivel mundial, con una gran variedad de clientes en más de 150 países.
* [Microsoft Windows, Universal Store, Azure IoT Hub, Xbox Live y otros servicios a escala de Internet](https://azure.microsoft.com/blog/how-azure-documentdb-planet-scale-nosql-helps-run-microsoft-s-own-businesses/). Cómo Microsoft compila de forma masiva servicios escalables con Azure Cosmos DB.
* [Equipo de Datos y análisis de Microsoft](https://customers.microsoft.com/story/microsoftdataandanalytics). El equipo de Datos y análisis de Microsoft alcanza una colección de macrodatos a escala mundial con Azure Cosmos DB
* [Sulekha.com](https://customers.microsoft.com/story/sulekha-uses-azure-documentdb-to-connect-customers-and-businesses-across-india). Sulekha usa la base de datos de Azure Cosmos tooconnect clientes y las empresas en India.
* [NewOrbit](https://customers.microsoft.com/story/neworbit-takes-flight-with-azure-documentdb). NewOrbit alza el vuelo con Azure Cosmos DB.
* [Affinio](https://customers.microsoft.com/doclink/affinio-switches-from-aws-to-azure-documentdb-to-harness-social-data-at-scale). Affinio cambia del AWS tooAzure Cosmos DB tooharness sociales datos a escala.
* [Next Games](https://azure.microsoft.com//blog/the-walking-dead-no-mans-land-game-soars-to-1-with-azure-documentdb/). Hola fallidos de paseo: N Man popular terrenos juego se eleva demasiado #1 compatible con base de datos de Azure Cosmos.
* [Halo](https://azure.microsoft.com/blog/how-halo-5-guardians-implemented-social-gameplay-using-azure-documentdb/). How Halo 5 implemented social gameplay using Azure Cosmos DB (Halo 5 usa Azure Cosmos DB para implementar el juego social).
* [Galería de Cortana Analytics](https://azure.microsoft.com/blog/cortana-analytics-gallery-a-scalable-community-site-built-on-azure-documentdb/). Galería de Cortana Analytics: un sitio de la comunidad escalable basado en Azure Cosmos DB.
* [Breeze](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18602). Integrador líder del sector ofrece a empresas multinacionales perspectivas globales en minutos con tecnologías en la nube flexibles.
* [News Republic](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18639). Agregar inteligencia toohello noticias tooprovide información con el propósito de ciudadanos involucrados. 
* [SGS International](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18653). Para el color coherente en todo el mundo de hello las principales marcas activan tooSGS. Y SGS resulta tooAzure.
* [Telenor](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18608). Líder mundial Telenor usa toomove de hello en la nube con una velocidad de Hola de un inicio. 
* [XOMNI](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18667). almacén de Hola de ejecuciones futuras de hello en flujo fácil hello y búsqueda rápido de datos.
* [Nucleo](https://customers.microsoft.com/story/azure-based-software-platform-breaks-down-barriers-bet). Esta plataforma de software basada en Azure rompe las barreras que existen entre las empresas y los clientes.
* [Weka](https://customers.microsoft.com/story/weka-smart-fridge-improves-vaccine-management-so-more-people-can-be-protected-against-diseases). Smart-Fridge de Weka mejora la administración de vacunas de forma que más gente puede protegerse contra enfermedades.
* [Orange Tribes](https://customers.microsoft.com/story/theres-more-to-that-food-app-than-meets-the-eye-or-the-mouth). No hay más aplicaciones de alimentos toothat que cumple los ojos de Hola o boca Hola.
* [Real Madrid](https://customers.microsoft.com/story/real-madrid-brings-the-stadium-closer-to-450-million-f). Madrid real pone hello más cerca de millones ventiladores de too450 estadio mundo Hola con hello Microsoft Cloud.
* [Tuku](https://customers.microsoft.com/story/tuku-makes-car-buying-fun-with-help-from-azure-services). TUKU hace que comprar un vehículo sea una experiencia divertida gracias a los servicios de Azure.
