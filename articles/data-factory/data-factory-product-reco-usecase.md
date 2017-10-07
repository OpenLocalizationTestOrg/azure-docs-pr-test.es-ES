---
title: "aaaData caso de uso de fábrica - las recomendaciones del producto"
description: "Obtenga información acerca de un caso de uso que se implementan mediante Factoría de datos de Azure junto con otros servicios."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6f1523c7-46c3-4b8d-9ed6-b847ae5ec4ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: d7912965fe4762d64e8ca3c28381ea6187f36631
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---product-recommendations"></a>Caso de uso: recomendaciones de productos
Factoría de datos de Azure es uno de los muchos servicios que se utilizan tooimplement Hola Suite de inteligencia de Cortana de aceleradores de soluciones.  Consulte la página [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics) para más información sobre este conjunto de aplicaciones. En este documento se describe un caso de uso común que los usuarios de Azure ya resolvieron e implementaron mediante Data Factory de Azure y otros servicios del componente Cortana Intelligence.

## <a name="scenario"></a>Escenario
Tiendas en línea normalmente desea tooentice sus productos de toopurchase de los clientes por mostrándoles productos que están probablemente toobe interesa y, por tanto, probablemente toobuy. tooaccomplish, tiendas en línea necesitan toocustomize experiencia en línea de los usuarios mediante el uso de las recomendaciones del producto personalizado para ese usuario específico. Estas recomendaciones personalizadas son toobe realizada en función de sus datos históricos y actuales compra comportamiento, información del producto, acaban de introducir las marcas y los datos de segmentación de producto y de cliente.  Además, pueden ofrecer recomendaciones de producto de hello usuario basadas en el análisis del comportamiento de uso general de todos sus usuarios combinada.

objetivo de Hola de estos distribuidores es toooptimize para las conversiones de usuario haga clic en para venta y disfrutar de los ingresos por ventas superior.  Para conseguirlo, se proporcionan recomendaciones de productos contextuales, basadas en el comportamiento en función de los intereses y las acciones del cliente. En este caso de uso, usamos tiendas en línea como un ejemplo de empresas que quieran toooptimize para sus clientes. Sin embargo, estos principios aplican business tooany que desea tooengage sus clientes alrededor de sus productos y servicios y mejoran la experiencia de compra de sus clientes con las recomendaciones del producto personalizado.

## <a name="challenges"></a>Desafíos
Existen muchos desafíos que se enfrentan los minoristas en línea al tratar de tooimplement este tipo de caso de uso. 

En primer lugar, se deben ingestión los datos de diferentes tamaños y formas de varios orígenes de datos, tanto de forma local y en la nube de Hola. Estos datos incluyen datos de productos, datos de comportamiento del cliente históricos y datos de usuario como usuario de hello examina el punto de venta en línea de saludo. 

En segundo lugar, las recomendaciones de productos personalizadas deben calcularse y predecirse de forma razonable y precisa. Además tooproduct, marca y datos de comportamiento y el explorador del cliente, tiendas en línea también necesitan tooinclude comentarios de los clientes en los últimos toofactor de compras en la determinación de Hola de recomendadas de producto de Hola para usuario Hola. 

En tercer lugar, recomendaciones de Hola deben toohello inmediatamente entrega usuario tooprovide una exploración sin problemas y la experiencia de compra y proporcionará recomendaciones de hello más reciente y relevante. 

Por último, los minoristas necesitan eficacia de hello toomeasure de su enfoque al realizar un seguimiento global subida y ventas cruzadas éxitos de ventas de conversión de haga clic en y ajuste tootheir recomendaciones para el futuro.

## <a name="solution-overview"></a>Información general de la solución
Este caso práctico de ejemplo fue resuelto e implementado por usuarios reales de Azure Data Factory y otros servicios del componente Cortana Intelligence, como [HDInsight](https://azure.microsoft.com/services/hdinsight/) y [Power BI](https://powerbi.microsoft.com/).

comerciante en línea Hello utiliza un almacén de blobs de Azure, un servidor local de SQL, base de datos de SQL Azure y un puesto de datos relacionales como sus opciones de almacenamiento de datos a lo largo de flujo de trabajo de Hola.  almacén de blobs de Hello contiene información del cliente, datos de comportamiento del cliente y datos de la información de producto. información de producto de Hello datos incluyen información de marca de producto y un catálogo de productos almacena localmente en el almacén de datos SQL. 

Todos los datos de Hola se combinan y se pasa a un recomendaciones toodeliver personalizada del sistema de recomendación producto según intereses del cliente y las acciones de mientras el usuario de Hola examina los productos en el catálogo de hello en el sitio Web de Hola. los clientes de Hello también ver productos que están relacionados con el producto toohello está mirando basado en general patrones de uso del sitio Web que no están relacionado tooany un usuario.

![diagrama del caso de uso](./media/data-factory-product-reco-usecase/diagram-1.png)

Gigabytes web sin formato de archivos de registro se generan cada día del sitio Web del distribuidor de hello en línea como archivos semiestructurados. Hola archivos de registro de web sin formato e información del catálogo de customer y product hello es ingestión con regularidad en un almacenamiento de blobs de Azure mediante el movimiento de datos implementadas globalmente del generador de datos como un servicio. archivos de registro sin procesar de Hola de día de Hola se particionan (por año y mes) en almacenamiento de blobs para almacenamiento a largo plazo.  [HDInsight de Azure](https://azure.microsoft.com/services/hdinsight/) son toopartition usado Hola los archivos de registro sin procesar blob Hola almacén y el proceso registros Hola ingerida a escala mediante scripts de Hive y Pig. Hola registros web con particiones están de datos, a continuación, hello tooextract procesado necesario entradas para una recomendación sistema toogenerate Hola personalizada producto recomendaciones de aprendizaje automático.

sistema de recomendación que se usa para el aprendizaje automático de hello en este ejemplo Hello es una plataforma de recomendación de aprendizaje de automático de código abierto [Mahout Apache](http://mahout.apache.org/).  Cualquier [aprendizaje automático de Azure](https://azure.microsoft.com/services/machine-learning/) o modelos personalizados pueden ser aplicados toohello escenario.  modelo de Mahout de Hello es toopredict usado Hola similitud entre elementos en el sitio Web de hello basado en patrones de uso general y recomendaciones de hello personalizada toogenerate en función de usuario individual de Hola.

Por último, conjunto de resultados de Hola de recomendaciones de productos personalizados es tooa movida relacional data mart para el consumo por sitio Web del distribuidor Hola.  conjunto de resultados de Hello también podría tener acceso directamente desde almacenamiento de blobs por otra aplicación o movido tooadditional almacenes para otros consumidores y casos de uso.

## <a name="benefits"></a>Ventajas
Al optimizar su estrategia de recomendación de producto y alinearse con los objetivos empresariales, solución de hello cumple del comerciante en línea hello comercialización y objetivos de marketing. Además, se toooperationalize capaz y administración el flujo de trabajo de hello productos recomendación de una manera eficaz, confiable y rentable. enfoque Hola hecho muy fácil para ellos tooupdate su modelo y ajustar su efectividad basado en medidas de Hola de aciertos de conversión de haga clic en ventas. Mediante el uso de Data Factory de Azure, se puede tooabandon su administración de recursos de nube manual de un proceso lento y costoso y mover la administración de recursos de nube tooon a petición. Por lo tanto, se puede toosave tiempo y dinero y reduce su implementación en tiempo de toosolution. Estado operativo y las vistas del linaje de datos se convirtió en toovisualize fácil y solucionar problemas con la supervisión de hello intuitiva factoría de datos y la administración disponible en hello portal de Azure de la interfaz de usuario. Su solución ahora puede programar y administrar para que termine de datos se genera y se entregan toousers forma confiable y datos y las dependencias de procesamiento se administran automáticamente sin intervención humana.

Al proporcionar esta experiencia de compra personalizada, hello comerciante en línea crea un cliente más competitivo, fomentar la participación experimentar y, por tanto, aumentar la satisfacción del cliente de ventas y general.

