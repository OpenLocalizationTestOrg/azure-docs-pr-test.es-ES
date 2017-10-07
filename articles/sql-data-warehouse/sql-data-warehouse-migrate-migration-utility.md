---
title: "Migración: Utilidad de migración de Data Warehouse | Microsoft Docs"
description: Migrar tooSQL almacenamiento de datos.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 4d7ad981-ef31-4513-b337-50bdc4709c09
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: c89909883fb42b0b04dd87a9973e5ee3e30d8f0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-warehouse-migration-utility-preview"></a>Utilidad de migración de Almacenamiento de datos (vista previa)
> [!div class="op_single_selector"]
> * [Descargar la utilidad de migración][Download Migration Utility]
> 
> 

Hola utilidad de migración de almacenamiento de datos es que una herramienta diseñada toomigrate esquema y los datos de SQL Server y base de datos de SQL Azure tooAzure almacenamiento de datos SQL. Durante la migración de esquema, herramienta de hello asigna automáticamente el esquema correspondiente de Hola de toodestination de origen. Después de que se ha migrado el esquema de hello, herramientas de hello proporciona datos de toomove de opción de hello con scripts generados automáticamente.

Además tooschema y migración de datos, esta herramienta le proporciona Hola informes de compatibilidad de toogenerate opción que resumen las incompatibilidades entre las instancias de origen y de destino de Hola que impedirían que simplifica la migración.

## <a name="get-started"></a>Primeros pasos
Como requisito previo para la instalación, deberá scripts de migración de toorun de utilidad de línea de comandos de BCP de Hola y el informe de compatibilidad de Office tooview Hola. Después de iniciar Hola ejecutable que se descarga, será tooaccept solicitada CLUF estándar antes de que se instalará la herramienta Hola.

Además, toorun hello Utiliy de migración, se necesita Hola uno los siguientes permisos de base de datos de Hola que se está viendo toomigrate: CREATE DATABASE, ALTER ANY DATABASE o VIEW ANY DEFINITION.

### <a name="launching-hello-tool-and-connecting"></a>Herramienta de Hola y la conexión
Instalar herramienta de Hola de inicio, haga clic en el icono del escritorio Hola que aparece post. Al abrir la herramienta de hello, se le pedirá con una página de conexión inicial donde puede elegir el origen y destino para la herramienta de migración de Hola. En este momento se admiten SQL Server y Base de datos SQL de Azure como orígenes y Almacenamiento de datos SQL como destino. Después de seleccionar esta opción se pide a servidor de origen de tooconnect tooyour rellenando en nombre del servidor y autenticación y, a continuación, haga clic en 'Conectar'.

Después de autenticar, herramienta de hello mostrará una lista de bases de datos que se encuentran en el servidor de Hola que están conectados a. Puede comenzar la migración de hello seleccionando una base de datos que le gustaría toomigrate y, a continuación, haga clic en 'Migrar seleccionado'.

## <a name="migration-report"></a>Informe de migración
Al seleccionar 'Comprobar la compatibilidad de base de datos' en la herramienta de hello generará un informe que resume todas las incompatibilidades de objeto de base de datos de hello solicitado toomigrate. Puede encontrar una lista más amplia de algunas Hola funcionalidad de SQL Server que no está presente en el almacén de datos de SQL en nuestro [documentación sobre migración][migration documentation]. Cuando se genera el informe de hello será capaz de toosave y el informe de hello abierto en Excel.

Tenga en cuenta que al generar el esquema de migración de hello, mayoría de los problemas identificado como 'Object' se ajustará en migración inmediata de tooallow de orden de los datos. Revise Hola cambios tooensure no desea toomake más ajustes antes de aplicar el esquema de Hola.

## <a name="migrate-schema"></a>Migración del esquema
Después de conectarse, seleccionar esquema de migrar generará un script de migración de esquema para las tablas de hello seleccionado. Esta estructura de Hola de puertos de secuencia de comandos de tabla de hello, asigna los formularios compatibles de toomore de tipos de datos incompatibles y crea esquema y las credenciales de seguridad si esto se indica por usuario de hello en configuración de la migración de Hola. Este código puede ejecutarse en la instancia de almacenamiento de datos SQL de hello como destinada, guarda el archivo tooa, copia tooyour Portapapeles o incluso editar en línea antes de realizar otra acción.  

Como se indicó anteriormente, cuando la migración de Hola de revisión de esquema cambia ese Hola herramienta ha realizado en orden tooensure que comprende todas ellas.  

## <a name="migrate-data"></a>Migración de los datos
Haciendo clic en la opción de "Datos migrar" hello puede generar scripts BCP que se moverán los archivos de datos primer tooflat en el servidor, y, a continuación, directamente en el almacén de datos de SQL. Se recomienda este proceso para mover pequeñas cantidades de datos y, como los reintentos no están integrados y pueden producirse errores si se produce una pérdida de conexión de red de Hola. En Ordenar toorun esto, necesitará una utilidad de línea de comandos toohave Hola BCP instalado y ya se debe haber creado esquema Hola para datos de Hola.

Después de que se ha rellenado parámetros Hola superiores que simplemente necesita tooclick ejecutar migración y se generará un conjunto de dos paquetes tooyour la ubicación especificada. Ejecute el archivo de exportación de hello datos de pedidos tooexport desde el origen de la migración a archivos sin formato y ejecute el archivo de importación de hello en orden tooimport los datos en almacenamiento de datos de SQL.

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha migrado algunos datos, consulte cómo demasiado[desarrollar][develop].

<!--Image references-->

<!--Article references-->
[migration documentation]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md

<!--Other Web references--> 
[Download Migration Utility]: https://migrhoststorage.blob.core.windows.net/sqldwsample/DataWarehouseMigrationUtility.zip
