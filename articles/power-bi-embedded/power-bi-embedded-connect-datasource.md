---
title: "aaaMicrosoft Power BI Embedded - origen de datos de conexión tooa"
description: "Power BI Embedded, conectar orígenes toodata"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a>Conectar el origen de datos de tooa
Con **Power BI Embedded**, puede insertar informes en su propia aplicación. Al incrustar un informe de Power BI en su aplicación, conecta toohello subyacente datos por informe de hello **importar** una copia de datos de Hola o por **conectar directamente** toohello origen de datos mediante  **DirectQuery**.

Estas son Hola diferencias entre el uso de **importación** y **DirectQuery**.

| Importación | DirectQuery |
| --- | --- |
| Tablas, columnas, *y datos* se importan o copian en el conjunto de datos del informe de Hola. toosee cambia datos subyacente toohello se produjo, debe actualizar o importar un completo actual conjunto de datos nuevo. |Solo *tablas y columnas* se importan o copian en el conjunto de datos del informe de Hola. Siempre verá los datos más actualizados de Hola. |

Con Power BI incrustado, en este momento se puede usar DirectQuery con orígenes de datos de nube, pero no en orígenes de datos locales.

> [!NOTE]
> Hello puerta de enlace de datos local no es compatible con Power BI Embedded en este momento. Esto significa que no se puede usar DirectQuery con orígenes de datos locales.

## <a name="supported-data-sources"></a>Orígenes de datos admitidos

**DirectQuery**
* Base de datos SQL de Azure
* Almacenamiento de datos SQL de Azure

**Importaciónación**

Puede importar usando el máximo de orígenes de datos disponibles de hello en Power BI Desktop. Que se van a **no** ser capaz de toorefresh esos datos en Power BI Embedded. Tendrá cambios tooupload tooyour PBIX archivo tooPower BI Embedded. Esto es debido a toono puerta de enlace disponible. 

## <a name="benefits-of-using-directquery"></a>Ventajas del uso de DirectQuery
Existen dos ventajas principales al usar **DirectQuery**:

* **DirectQuery** permite crear visualizaciones con conjuntos de datos muy grandes, donde lo contrario sería imposible toofirst importación todos Hola datos.
* Datos subyacentes cambian pueden requerir una actualización de datos, y en algunos informes, hello necesitan datos actuales de toodisplay puede requerir grandes transferencias de datos, realizar imposible volver a importar datos. Por el contrario, los informes de **DirectQuery** siempre usan datos actuales.

## <a name="limitations-of-directquery"></a>Limitaciones de DirectQuery
   Hay algunas de las limitaciones toousing **DirectQuery**:

* Todas las tablas deben proceder de una base de datos única.
* Si consulta hello es demasiado compleja, se producirá un error. error de hello tooremedy debe refactorizar consulta Hola por lo que es menos complejo. Si consulta Hola debe ser compleja, será necesario tooimport datos de hello en lugar de usar **DirectQuery**.
* El filtrado de relaciones es una dirección única tooa limitada, en lugar de ambas direcciones.
* No se puede cambiar el tipo de datos de Hola de una columna.
* De forma predeterminada, las limitaciones se colocan en expresiones DAX permitidas en las medidas. Consulte [DirectQuery y medidas](#measures).

<a name="measures"/>

## <a name="directquery-and-measures"></a>DirectQuery y medidas
las consultas de tooensure enviadas toohello origen de datos subyacente tengan un rendimiento aceptable, se aplican limitaciones en medidas. Cuando se usa **Power BI Desktop**avanzadas los usuarios pueden elegir toobypass esta limitación eligiendo **archivo > Opciones y configuración > opciones**. Hola **opciones** cuadro de diálogo, elija **DirectQuery**y seleccione la opción de hello **permitir medidas sin restricciones en el modo DirectQuery**. Cuando se selecciona esta opción, se puede usar cualquier expresión DAX que sea válida para una medida. Los usuarios deben tener en cuenta; Sin embargo, que algunas expresiones que funcionan muy bien cuando se importan datos de hello penada back-end de consultas muy lentas toohello de origen en **DirectQuery** modo. 

## <a name="see-also"></a>Otras referencias
* [Introducción a Microsoft Power BI Embedded](power-bi-embedded-get-started.md)
* [Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

¿Tiene más preguntas? [Intente Hola Comunidad de Power BI](http://community.powerbi.com/)

