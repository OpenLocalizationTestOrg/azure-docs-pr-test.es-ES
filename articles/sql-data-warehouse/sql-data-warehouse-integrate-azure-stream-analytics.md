---
title: "Análisis de transmisiones de Azure con el almacenamiento de datos de SQL aaaUse | Documentos de Microsoft"
description: "Sugerencias para usar Análisis de transmisiones de Azure con Almacenamiento de datos SQL de Azure para el desarrollo de soluciones."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1278197a6764864124fd92fc672de00b83ec343f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a>Uso de Análisis de transmisiones de Azure con Almacenamiento de datos SQL
Análisis de transmisiones de Azure es un servicio completamente administrado, lo que proporciona el procesamiento de eventos complejos de baja latencia, alta disponibilidad y escalable en transmisión de datos en la nube de Hola. Aprenderá los conceptos básicos de hello leyendo [Introducción tooAzure análisis de transmisiones][Introduction tooAzure Stream Analytics]. A continuación, aprenderá cómo toocreate una solución end-to-end con análisis de transmisiones siguiendo Hola [Introducción al uso de análisis de transmisiones de Azure] [ Get started using Azure Stream Analytics] tutorial.

En este artículo, aprenderá cómo toouse el almacenamiento de datos de SQL Azure base de datos como un receptor de salida para los trabajos de análisis de secuencia.

## <a name="prerequisites"></a>Requisitos previos
En primer lugar, recorra Hola siguiendo los pasos de hello [Introducción al uso de análisis de transmisiones de Azure] [ Get started using Azure Stream Analytics] tutorial.  

1. Creación de una entrada de Centro de eventos
2. Configuración e inicio de la aplicación del generador de eventos
3. Aprovisionamiento de un trabajo de Stream Analytics
4. Especificación de una consulta y entrada de trabajo

Luego cree una base de datos de Almacenamiento de datos SQL de Azure.

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a>Especifique la salida de trabajo: base de datos de Almacenamiento de datos SQL de Azure.
### <a name="step-1"></a>Paso 1
En el trabajo de análisis de transmisiones, haga clic en **salida** de arriba Hola de página de hello y, a continuación, haga clic en **agregar salida**.

### <a name="step-2"></a>Paso 2
Seleccione Base de datos SQL y haga clic en Siguiente.

![][add-output]

### <a name="step-3"></a>Paso 3
Escriba Hola después los valores en la página siguiente de hello:

* *Alias de salida*: escriba un nombre descriptivo para esta salida de trabajo.
* *Suscripción*:
  * Si la base de datos de almacenamiento de datos de SQL está en hello misma suscripción que el trabajo de análisis de transmisiones de hello, seleccione Usar base de datos SQL de la suscripción actual.
  * Si la base de datos está en una suscripción diferente, seleccione Usar la base de datos SQL de otra suscripción.
* *Base de datos*: especifique Hola nombre de una base de datos de destino.
* *Nombre del servidor*: especificar Hola nombre del servidor de base de datos de Hola que acaba de especificar. Ya puede utilizarla hello toofind de Portal de Azure clásico.

![][server-name]

* *Nombre de usuario*: especifique Hola de nombre de usuario de una cuenta que tenga permisos de escritura para la base de datos de Hola.
* *Contraseña*: proporcionar contraseña Hola Hola cuenta de usuario especificada.
* *Tabla*: especifique el nombre de Hola de tabla de destino de hello en la base de datos de Hola.

![][add-database]

### <a name="step-4"></a>Paso 4
Haga clic en tooadd de botón de comprobación de hello esta salida del trabajo y tooverify que análisis de transmisiones puede conectar correctamente la base de datos de toohello.

![][test-connection]

Cuando se realiza correctamente la base de datos de hello conexión toohello, verá una notificación en la parte inferior de hello del portal de Hola. Puede hacer clic en Probar conexión en base de datos de hello inferior tootest Hola conexión toohello.

## <a name="next-steps"></a>Pasos siguientes
Para obtener información general sobre la integración, consulte la [información general de la integración de SQL Data Warehouse][SQL Data Warehouse integration overview].

Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de Almacenamiento de datos SQL][SQL Data Warehouse development overview].

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction tooAzure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
