---
title: "aaaUse caso, la generación de perfiles de cliente"
description: "Obtenga información acerca de cómo Data Factory de Azure es clientes de juegos de tooprofile de flujo de trabajo (canalización) de toocreate usa una orientadas a datos."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: e07d55cf-8051-4203-9966-bdfa1035104b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 47f5e77242366c80cce2a2db65e3c696505b3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---customer-profiling"></a>Caso de uso - Generación de perfiles de clientes
Factoría de datos de Azure es uno de los muchos servicios que se utilizan tooimplement Hola Suite de inteligencia de Cortana de aceleradores de soluciones.  Para más información sobre Cortana Intelligence, visite [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics)(conjunto de aplicaciones de Cortana Intelligence). En este documento, describimos una toohelp de casos de uso sencillo comenzar a comprender cómo Data Factory de Azure puede resolver problemas comunes de análisis.

## <a name="scenario"></a>Escenario
Contoso es una empresa de juegos que crea juegos para varias plataformas: consolas de juegos, dispositivos portátiles y PC. Como reproductores de reproducir estos juegos, se genera gran volumen de datos del registro que realiza un seguimiento Hola patrones de uso, estilo de juegos y las preferencias del usuario de Hola.  Cuando se combina con demográfica, regional, y datos de productos, Contoso puede llevar a cabo análisis tooguide estas acerca de cómo los reproductores tooenhance experimentan y establecerlas como destino para las actualizaciones y en juego las compras. 

Objetivo de Contoso es oportunidades de ventas arriba-venta cruzada tooidentify basadas en el historial de juegos de Hola de sus reproductores y agregar atractivas crecimiento del negocio de toodrive de características y proporcionan una mejor toocustomers experiencia. Para este caso de uso, usamos una empresa de juegos como ejemplo de empresa. compañía de Hello desea toooptimize sus juegos en función de comportamiento de los jugadores. Estos principios aplican business tooany que desea tooengage sus clientes alrededor de sus productos y servicios y mejoran la experiencia de sus clientes.

En esta solución, Contoso desea que la eficacia de hello tooevaluate de una campaña de marketing que ha lanzado recientemente. Se iniciar con registros de juegos sin procesar de hello, proceso y enriquecen ellos con los datos de ubicación geográfica, combinarlos con datos de referencia de anuncios y, por último cópielos en impacto de una base de datos de SQL Azure tooanalyze Hola la campaña.

## <a name="deploy-solution"></a>Implementación de la solución
Todo lo que necesita tooaccess y pruebe este caso de uso simple es un [suscripción de Azure](https://azure.microsoft.com/pricing/free-trial/), [cuenta de almacenamiento Blob de Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)y un [base de datos de SQL Azure](../sql-database/sql-database-get-started.md). Implementar el cliente hello generación de perfiles de canalización de hello **canalizaciones de ejemplo** de mosaico en la página principal de saludo de la factoría de datos.

1. Cree una factoría de datos o abra una. Vea [copiar los datos de almacenamiento de blobs tooSQL con factoría de datos de la base de datos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para pasos toocreate una factoría de datos.
2. Hola **factoría de datos** hoja de factoría de datos de hello, haga clic en hello **ejemplo canalizaciones** icono.

    ![Icono Canalizaciones de ejemplo](./media/data-factory-samples/SamplePipelinesTile.png)
3. Hola **ejemplo canalizaciones** hoja, haga clic en hello **cliente de generación de perfiles** que desea toodeploy.

    ![Hoja Canalizaciones de ejemplo](./media/data-factory-samples/SampleTile.png)
4. Especificar opciones de configuración de ejemplo de Hola. Por ejemplo, el nombre de la cuenta de Azure Storage y la clave, el nombre del servidor de SQL Azure, la base de datos, el identificador de usuario y la contraseña.

    ![Hoja de ejemplo](./media/data-factory-samples/SampleBlade.png)
5. Una vez que haya en la especificación de opciones de configuración de hello, haga clic en **crear** toocreate/implementar Hola canalizaciones de ejemplo y utilizadas por las canalizaciones de hello services/tablas vinculadas.
6. Ver el estado de Hola de implementación en mosaico de ejemplo de Hola que hizo clic anteriormente hello **ejemplo canalizaciones** hoja.

    ![Estado de implementación](./media/data-factory-samples/DeploymentStatus.png)
7. Cuando vea hello **implementación se realizó correctamente** mensaje en mosaico Hola de ejemplo de Hola, cerrar hello **ejemplo canalizaciones** hoja.  
8. En **factoría de datos** hoja, verá que se agregan los servicios vinculados, conjuntos de datos y las canalizaciones tooyour factoría de datos.  

    ![Hoja de la Factoría de datos](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="solution-overview"></a>Información general de la solución
Este caso de uso sencillo puede utilizarse como un ejemplo de cómo puede usar tooingest Data Factory de Azure, preparar, transformar, analizar y publicar los datos.

![Flujo de trabajo de un extremo a otro](./media/data-factory-customer-profiling-usecase/EndToEndWorkflow.png)

Esta ilustración muestra cómo las canalizaciones de datos de hello aparecen en hello portal de Azure después de que se han implementado.

1. Hola **PartitionGameLogsPipeline** lee los eventos de juego sin procesar de hello del almacenamiento de blobs y crea particiones basadas en el año, mes y día.
2. Hola **EnrichGameLogsPipeline** combina eventos juegos con particiones con datos de referencia de código de replicación geográfica y enriquecer datos hello mediante la asignación de IP direcciones toohello correspondientes ubicaciones geográficas.
3. Hola **AnalyzeMarketingCampaignPipeline** canalización usa datos de hello enriquecido y lo procesa con hello publicidad datos toocreate Hola resultado final que contiene la eficacia de la campaña de marketing.

En este ejemplo, factoría de datos es tooorchestrate usa actividades que copian los datos de entrada, transformación y procesamiento de datos de Hola y Hola datos final tooan base de datos de SQL Azure de salida.  También puede visualizar red Hola de canalizaciones de datos, administrarlos y supervisar su estado de hello interfaz de usuario.

## <a name="benefits"></a>Ventajas
Al optimizar sus análisis de perfil de usuario y alinearse con los objetivos empresariales, empresa juegos es los patrones de uso recopilar tooquickly pueda y analizar Hola efectividad de sus campañas de marketing.

