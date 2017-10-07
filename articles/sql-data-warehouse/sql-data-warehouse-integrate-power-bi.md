---
title: aaaUse Power BI con almacenamiento de datos SQL | Documentos de Microsoft
description: Sugerencias para usar Power BI con Almacenamiento de datos SQL de Azure para el desarrollo de soluciones.
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: a3a347493d07af6824a561567f05894cfe3c0471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a>Uso de Power BI con Almacenamiento de datos SQL
Al igual que con la base de datos de SQL Azure, en la conexión directa de SQL datos de almacenamiento permite aplicación lógica del usuario tooleverage eficaz junto con capacidades de análisis de Hola de Power BI.  Con conexión directa, las consultas se envían tooyour back-almacenamiento de datos de SQL Azure en tiempo real como explorar datos Hola.  Esto, combinado con una escala de hello del almacén de datos de SQL, permite a los usuarios de informes dinámicos toocreate en minutos con terabytes de datos.  Además, la introducción de Hola de hello abierto en el botón de Power BI permite a los usuarios toodirectly conectar Power BI tootheir almacenamiento de datos SQL sin recopilar información de otras partes de Azure.

Cuando use Conexión directa, tenga en cuenta lo siguiente:

* Especifique el nombre del servidor de acceso completa de hello cuando se conecte (consulte a continuación para obtener más detalles)
* Garantizar las reglas de firewall se configuran la base de datos de Hola demasiado "permitan el acceso tooAzure services".
* Cada acción, como seleccionar una columna o agregar un filtro directamente consultará el almacenamiento de datos de Hola
* Iconos se actualizan aproximadamente cada 15 minutos (no es necesario actualización toobe programado)
* La sección de Preguntas y respuestas no está disponible para los conjuntos de datos de Conexión directa.
* Los cambios de esquema no se seleccionan automáticamente.
* Todas las consultas de conexión directa agotarán el tiempo de espera al cabo de 2 minutos.

Estas restricciones y notas pueden cambiar mientras seguimos tooimprove Hola experiencias. Hola tooconnect de pasos se detallan a continuación.  

## <a name="using-hello-open-in-power-bi-button"></a>Utilizando el botón 'Abrir en Power BI' hello
Hola toomove de manera más sencilla entre el almacenamiento de datos SQL y Power BI es con hello abierto en el botón de Power BI. Este botón permite tooseamlessly empezar a crear nuevos paneles en Power BI.  

1. tooget inició navegar por instancia de almacenamiento de datos SQL de tooyour Hola Portal clásico de Azure.
2. Haga clic en el botón 'Abrir en Power BI' hello.
3. Si no es capaz de toosign en directamente, o si no tiene una cuenta de Power BI, necesitará toosign en.  
4. Se le dirigirá toohello página de conexión de almacenamiento de datos SQL, con información de Hola desde el almacenamiento de datos de SQL se ha rellenado previamente.
5. Después de escribir sus credenciales será tooyour conectados de forma continua de almacenamiento de datos SQL.

## <a name="connecting-through-hello-power-bi-portal"></a>Conexión a través del portal de Power BI Hola
En suma toousing Hola abierto en el botón de Power BI a los usuarios también pueden conectar tootheir almacenamiento de datos SQL a través de hello Portal de Power BI.

1. Haga clic en obtener datos en parte inferior de Hola Hola del panel de exploración.
2. Seleccione "Bases de datos".
3. Una vez en la página de bases de datos de hello, seleccione "Almacenamiento de datos de SQL Azure" y, a continuación, haga clic en 'Conectar'.
4. Escriba la información de conexión necesaria de Hola.  El nombre del servidor y el nombre de la base de datos pueden encontrarse en hello Portal de Azure.
5. Se le dirigirá volver toohello la página principal de Power BI y después de la conexión se realiza una nueva entrada en 'Conjuntos de datos' aparecerá con el nombre de saludo de la instancia.  
6. Puede hacer clic en hello nuevo conjunto de datos tooexplore todos Hola tablas y vistas en la base de datos. Si selecciona una columna enviará un origen de toohello espera de consulta, creará dinámicamente el objeto visual. Estos objetos visuales pueden guardarse en un informe nuevo y anclarse de nuevo panel tooyour.

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
