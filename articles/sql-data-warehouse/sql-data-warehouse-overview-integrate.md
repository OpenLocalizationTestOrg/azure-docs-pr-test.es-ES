---
title: aaaBuild soluciones integradas con almacenamiento de datos SQL | Documentos de Microsoft
description: 'Herramientas y asociados con soluciones que se integran con Almacenamiento de datos SQL. '
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: e2dc8f3f-10e3-4589-a4e2-50c67dfcf67f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: c8a4202dd84305bea4e4c2faf0e4791d026e794f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a>Aprovechamiento de otros servicios con Almacenamiento de datos SQL
Además tooits las funcionalidades básicas, almacenamiento de datos de SQL permite a los usuarios tooleverage muchas de Hola otros servicios en Azure junto con él.  En concreto, le hemos llevado actualmente toodeeply integrar con los siguientes Hola de pasos:

* Power BI
* Factoría de datos de Azure
* Aprendizaje automático de Azure
* Análisis de transmisiones de Azure

Estamos trabajando tooconnect con más servicios a través de hello ecosistema de Azure.

## <a name="power-bi"></a>Power BI
Integración de Power BI permite la capacidad de proceso de hello tooleverage de almacenamiento de datos de SQL con los informes dinámicos de Hola y la visualización de Power BI. La integración de Power BI actualmente incluye:

* **Conexión directa**: una conexión más avanzada con aplicación de lógica en Almacenamiento de datos SQL.  Esto proporciona un análisis más rápido a mayor escala.
* **Abrir en Power BI**: botón 'Abrir en Power BI' hello pasa información de instancia tooPower BI, lo que permite una conexión más sencilla.

Vea [integrar con Power BI](sql-data-warehouse-integrate-power-bi.md) o hello [documentación de Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) para obtener más información.

## <a name="azure-data-factory"></a>Azure Data Factory
Factoría de datos de Azure ofrece a los usuarios un toocreate de plataforma administrada que canalizaciones complejas de extracción y carga.  La integración del almacenamiento de datos de SQL con Data Factory de Azure incluye siguiente de hello:

* **Procedimientos almacenados**: coordinar la ejecución de Hola de procedimientos almacenados en almacenamiento de datos de SQL.
* **Copia**: datos de uso ADF toomove en almacenamiento de datos de SQL.  Esta operación puede utilizar el mecanismo de movimiento de datos estándar de ADF o PolyBase en hello cubre. 

Vea [integración con Data Factory de Azure](sql-data-warehouse-integrate-azure-data-factory.md) o hello [documentación de Data Factory de Azure](https://azure.microsoft.com/documentation/services/data-factory/) para obtener más información.

## <a name="azure-machine-learning"></a>Aprendizaje automático de Azure
Aprendizaje automático de Azure es un servicio de análisis totalmente administrado que permite a los usuarios aprovechar un gran conjunto de herramientas de predicción de modelos intrincados toocreate.  Almacenamiento de datos de SQL se admite como un origen y un destino para estos modelos con hello después funcionalidad:

* **Lectura de datos:** producir modelos a escala usando T-SQL en Almacenamiento de datos SQL.
* **Datos de escritura:** confirmar los cambios de cualquier modelo de realizar copias de tooSQL almacenamiento de datos.

Vea [integrar con aprendizaje automático de Azure](sql-data-warehouse-integrate-azure-machine-learning.md) o hello [documentación de aprendizaje automático de Azure](https://azure.microsoft.com/services/machine-learning/) para obtener más información.

## <a name="azure-stream-analytics"></a>Análisis de transmisiones de Azure
Análisis de transmisores de Azure es una infraestructura compleja y totalmente administrada para el procesamiento y consumo de datos de eventos generados por el Centro de eventos de Azure.  Integración con el almacenamiento de datos de SQL permite streaming toobe datos eficazmente procesa y almacenan junto con datos relacionales, lo que permite un poco más, más análisis avanzado.  

* **Salida del trabajo:** salida de envío de análisis de transmisiones directamente trabajos tooSQL almacenamiento de datos.

Vea [integrar con análisis de transmisiones de Azure](sql-data-warehouse-integrate-azure-stream-analytics.md) o hello [documentación de análisis de transmisiones de Azure](https://azure.microsoft.com/documentation/services/stream-analytics/) para obtener más información.

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop/

[Azure Data Factory]: sql-data-warehouse-integrate-azure-data-factory.md
[Azure Machine Learning]: sql-data-warehouse-integrate-azure-machine-learning.md
[Azure Stream Analytics]: sql-data-warehouse-integrate-azure-stream-analytics.md
[Power BI]: sql-data-warehouse-integrate-power-bi.md
[Partners]: sql-data-warehouse-partner-business-intelligence.md

<!--MSDN references-->

<!--Other Web references-->
