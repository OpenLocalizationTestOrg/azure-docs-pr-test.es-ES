---
title: "aaaMove datos tooan base de datos de SQL de Azure para el aprendizaje automático de Azure | Documentos de Microsoft"
description: Crear tabla de SQL y cargar datos tooSQL tabla
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 50f8b862-4d32-44b2-a1e2-4fbc8024acaa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: b33ef836f42c17a56794baf763281e9998b16bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooan-azure-sql-database-for-azure-machine-learning"></a>Mover datos tooan base de datos de SQL Azure para el aprendizaje automático de Azure
Este tema describen las opciones de Hola para mover datos de archivos planos (formatos CSV o TSV) o de datos almacenados en una base de datos de SQL Azure del tooan de SQL Server local. Estas tareas para mover datos en la nube toohello forman parte de hello proceso de ciencia de datos de equipo.

Para un tema que describe las opciones de Hola para móvil tooan de datos local de SQL Server para el aprendizaje automático, consulte [mover datos tooSQL Server en una máquina virtual de Azure](machine-learning-data-science-move-sql-server-virtual-machine.md).

siguiente Hello **menú** vincula tootopics que describen cómo tooingest datos en entornos de destino donde se pueden almacenar y procesar durante datos Hola Hola proceso de ciencia de datos de equipo (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Hello siguiente tabla resume las opciones de Hola para mover datos tooan base de datos de SQL Azure.

| <b>ORIGEN</b> | <b>DESTINO: Base de datos SQL de Azure</b> |
| --- | --- |
| <b>Archivo plano (formatos CSV o TSV)</b> |<a href="#bulk-insert-sql-query">Consulta SQL de inserción masiva |
| <b>SQL Server local</b> |1. <a href="#export-flat-file">Exportar archivo tooFlat<br> 2. <a href="#insert-tables-bcp">Asistente para migración de base de datos de SQL<br> 3. <a href="#db-migration">Copia de seguridad y restauración de una base de datos<br> 4. <a href="#adf">Factoría de datos de Azure |

## <a name="prereqs"></a>Requisitos previos
procedimientos de Hello descritos aquí requieren que tenga:

* Una **suscripción de Azure**. Si no tiene una suscripción, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Una **cuenta de almacenamiento de Azure**. Usar una cuenta de almacenamiento de Azure para almacenar datos de hello en este tutorial. Si no tiene una cuenta de almacenamiento de Azure, vea hello [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artículo. Una vez haya creado la cuenta de almacenamiento de hello, necesita tooobtain Hola cuenta clave usa el almacenamiento de información de tooaccess Hola. Consulte [Administración de la cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Acceso tooan **base de datos de SQL Azure**. Si debe configurar una base de datos de SQL Azure, [Introducción a la base de datos de SQL de Microsoft Azure](../sql-database/sql-database-get-started.md) proporciona información acerca de cómo tooprovision una nueva instancia de una base de datos de SQL Azure.
* **Azure PowerShell** instalado y configurado de forma local. Para obtener instrucciones, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

**Datos**: procesos de migración de Hola se muestran con hello [conjunto de datos de Nueva York Taxi](http://chriswhong.com/open-data/foil_nyc_taxi/). contiene información sobre los datos de ida y vuelta y ferias Hello NYC Taxi dataset y está disponible en el almacenamiento de blobs de Azure: [NYC Taxi datos](http://www.andresmh.com/nyctaxitrips/). En [Descripción del conjunto de datos de carreras de taxi de Nueva York](machine-learning-data-science-process-sql-walkthrough.md#dataset), se proporciona un ejemplo y una descripción de estos archivos.

Puede adaptar Hola procedimientos tooa aquí descrito conjunto de sus propios datos, o bien, siga los pasos de hello tal como se describe mediante el uso de hello NYC Taxi conjunto de datos. Hola tooupload NYC Taxi conjunto de datos en la base de datos de SQL Server local, siga procedimiento Hola descrito en [importar masivamente datos en la base de datos de SQL Server](machine-learning-data-science-process-sql-walkthrough.md#dbload). Estas instrucciones son para un servidor de SQL Server en una máquina Virtual de Azure, pero Hola procedimiento Hola para cargar toohello local de SQL Server es igual.

## <a name="file-to-azure-sql-database"></a>Migración de datos de una base de datos de archivo plano origen tooan SQL Azure
Datos de archivos sin formato (con formato CSV o TSV) pueden ser movida tooan de base de datos de SQL Azure usando una consulta de SQL de inserción masiva.

### <a name="bulk-insert-sql-query"></a> Consulta SQL de inserción masiva
pasos de Hola para procedimiento almacenado Hola con hello consulta de SQL de inserción masiva son similar toothose tratado en secciones de Hola para mover datos desde un tooSQL de origen de archivo sin formato Server en una máquina virtual de Azure. Para detalles, vea [Consulta SQL de inserción masiva](machine-learning-data-science-move-sql-server-virtual-machine.md#insert-tables-bulkquery).

## <a name="sql-on-prem-to-sazure-sql-database"></a>Migración de datos de la base de datos local SQL Server tooan SQL Azure
Si los datos de origen de Hola se almacenan en un servidor local de SQL, existen varias posibilidades de base de datos de SQL Azure de tooan mover datos de hello:

1. [Exportar archivo tooFlat](#export-flat-file)
2. [Asistente para migración de Base de datos SQL](#insert-tables-bcp)
3. [Copia de seguridad y restauración de una base de datos](#db-migration)
4. [Factoría de datos de Azure](#adf)

pasos para los tres primeros Hola Hola son muy similares secciones de toothose en [mover datos tooSQL Server en una máquina virtual de Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) que abarcan los mismos procedimientos. Secciones correspondientes de vínculos toohello en ese tema se proporcionan en hello siguiendo las instrucciones.

### <a name="export-flat-file"></a>Exportar archivo tooFlat
pasos de Hola para este exportar el archivo sin formato de tooa son similar toothose cubierto en [exportar tooFlat archivo](machine-learning-data-science-move-sql-server-virtual-machine.md#export-flat-file).

### <a name="insert-tables-bcp"></a>Asistente para migración de Base de datos SQL
pasos para utilizar Hola Asistente para migración de base de datos de SQL Hello son similar toothose cubierto en [Asistente para migración de base de datos de SQL](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-migration).

### <a name="db-migration"></a>Copia de seguridad y restauración de una base de datos
pasos de Hello para el uso de la base de datos realice una copia y restauración son similar toothose cubierto en [base de datos copia de seguridad y restaurar](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-backup).

### <a name="adf"></a>Factoría de datos de Azure
procedimiento de Hola para mover datos tooan Azure base de datos SQL con el generador de datos de Azure (ADF) se proporciona en el tema de hello [mover datos desde un servidor SQL local tooSQL Azure con Data Factory de Azure](machine-learning-data-science-move-sql-azure-adf.md). Este tema muestra cómo toomove datos desde una base de datos de SQL Server local tooan SQL Azure base de datos a través de almacenamiento de blobs de Azure con ADF.

Considere el uso de ADF cuando continuamente migra toobe de necesidades de datos en un escenario híbrido que tiene acceso tanto de forma local y recursos de la nube y cuando se lleva a cabo o necesitan datos de hello toobe modificar ni lógica de negocios agregó tooit cuando se están migrando. ADF permite Hola de programación y la supervisión de trabajos mediante scripts sencillos de JSON que administran el movimiento de Hola de datos de forma periódica. La ADF también tiene otras capacidades como la compatibilidad con operaciones complejas.
