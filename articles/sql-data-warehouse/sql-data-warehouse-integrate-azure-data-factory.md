---
title: aaaUse Data Factory de Azure con almacenamiento de datos SQL | Documentos de Microsoft
description: "Sugerencias para usar Factoría de datos de Azure (ADF) con Almacenamiento de datos SQL para el desarrollo de soluciones."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 492de762-c7a2-4cdb-943f-3135230e94f1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d40a547830f9681504253d39ae3066800a955c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a>Uso de Factoría de datos de Azure con Almacenamiento de datos SQL
Factoría de datos de Azure proporciona un método completamente administrado para orquestar la transferencia de Hola de datos y la ejecución de procedimientos almacenados de almacenamiento de datos de SQL.  Esto le permitirá toomore fácilmente instalación y programación extraer transformación y carga (ETL) procedimientos complejos con almacenamiento de datos de SQL. Para obtener una descripción más completa de Data Factory de Azure, vea hello [documentación de Data Factory de Azure][Azure Data Factory documentation].

## <a name="data-movement"></a>Movimiento de datos
Factoría de datos de Azure permite el movimiento entre orígenes locales y los distintos servicios de Azure.  Integración general y actual con Data Factory de Azure admite tooand de movimiento de datos de hello ubicaciones siguientes:

* Almacenamiento de blobs de Azure
* Base de datos SQL de Azure
* SQL Server local
* SQL Server en IaaS

Para obtener información sobre cómo tooset los datos de una actividad de copia [copiar los datos con Data Factory de Azure][Copy data with Azure Data Factory]

## <a name="stored-procedures"></a>Procedimientos almacenados
 Hola igual forma se puede utilizar tooschedule la transferencia de datos, puede Data Factory de Azure también puede tooorchestrate usado Hola ejecución de procedimientos almacenados.  Esto permite más compleja toobe canalizaciones creado y extiende capacidad tooleverage Hola potencia de cálculo del generador de datos de Azure de almacenamiento de datos SQL.

## <a name="next-steps"></a>Pasos siguientes
Para obtener información general sobre la integración, consulte la [información general de la integración de SQL Data Warehouse][SQL Data Warehouse integration overview].
Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de Almacenamiento de datos SQL][SQL Data Warehouse development overview].

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

