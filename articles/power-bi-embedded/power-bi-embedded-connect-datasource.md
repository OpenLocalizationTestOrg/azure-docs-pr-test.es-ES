---
title: Microsoft Power BI Embedded - Conectarse a un origen de datos
description: "Power BI Embedded, conectarse a orígenes de datos"
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
ms.openlocfilehash: 9f614bbc63eae788aa52132c8f0e42ad8963559a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-a-data-source"></a>Conectarse a un origen de datos
Con **Power BI Embedded**, puede insertar informes en su propia aplicación. Cuando inserta un informe de Power BI en su aplicación, el informe se conecta a los datos subyacentes **importando** una copia de los datos o **conectándose directamente** al origen de datos mediante **DirectQuery**.

Estas son las diferencias entre usar **Importación** y **DirectQuery**.

| Importar | DirectQuery |
| --- | --- |
| Las tablas, columnas *y datos* se importan o se copian en el conjunto de datos del informe. Para ver los cambios que se han producido en los datos subyacentes, debe actualizar o importar de nuevo un conjunto de datos actual completo. |Solo las *tablas y columnas* se importan o se copian en el conjunto de datos del informe. Siempre verá los datos más actuales. |

Con Power BI incrustado, en este momento se puede usar DirectQuery con orígenes de datos de nube, pero no en orígenes de datos locales.

> [!NOTE]
> No se admite la puerta de enlace de datos local con Power BI Embedded en este momento. Esto significa que no se puede usar DirectQuery con orígenes de datos locales.

## <a name="supported-data-sources"></a>Orígenes de datos admitidos

**DirectQuery**
* Base de datos SQL de Azure
* Almacenamiento de datos SQL de Azure

**Importaciónación**

Puede realizar la importación mediante todos los orígenes de datos disponibles en Power BI Desktop. **No** podrá actualizar dichos datos en Power BI Embedded. Tendrá que cargar los cambios en el archivo PBIX en Power BI Embedded. Esto se debe a que no hay ninguna puerta de enlace disponible. 

## <a name="benefits-of-using-directquery"></a>Ventajas del uso de DirectQuery
Existen dos ventajas principales al usar **DirectQuery**:

* **DirectQuery** le permite crear visualizaciones sobre conjuntos de datos muy grandes, cuando, de otro modo, sería inviable importar por primera vez todos los datos.
* Los cambios en los datos subyacentes pueden requerir una actualización de datos, y para algunos informes, la necesidad de mostrar los datos actuales puede requerir grandes transferencias de datos, haciendo inviable la reimportación de datos. Por el contrario, los informes de **DirectQuery** siempre usan datos actuales.

## <a name="limitations-of-directquery"></a>Limitaciones de DirectQuery
   Existen algunas limitaciones al usar **DirectQuery**:

* Todas las tablas deben proceder de una base de datos única.
* Si la consulta es demasiado compleja, se producirá un error. Para solucionar el error debe refactorizar la consulta, de forma que sea menos compleja. Si la consulta debe ser compleja, deberá importar los datos en lugar de usar **DirectQuery**.
* El filtrado de relación se limita a una dirección única, en lugar de a ambas direcciones.
* No puede cambiar el tipo de datos de una columna.
* De forma predeterminada, las limitaciones se colocan en expresiones DAX permitidas en las medidas. Consulte [DirectQuery y medidas](#measures).

<a name="measures"/>

## <a name="directquery-and-measures"></a>DirectQuery y medidas
Para asegurarse de que las consultas que se envían al origen de datos subyacente tienen un rendimiento adecuado, se imponen limitaciones en las medidas. Al usar **Power BI Desktop**, los usuarios avanzados pueden elegir derivar esta limitación eligiendo **Archivo > Opciones y configuración > Opciones**. En el cuadro de diálogo **Opciones**, elija **DirectQuery** y seleccione la opción **Permitir medidas sin restricciones en el modo DirectQuery**. Cuando se selecciona esta opción, se puede usar cualquier expresión DAX que sea válida para una medida. Sin embargo, los usuarios deben tener en cuenta que algunas expresiones que se ejecutan correctamente cuando se importan los datos, pueden provocar consultas muy lentas en el origen de back-end del modo **DirectQuery** . 

## <a name="see-also"></a>Otras referencias
* [Introducción a Microsoft Power BI Embedded](power-bi-embedded-get-started.md)
* [Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

¿Tiene más preguntas? [Pruebe la comunidad de Power BI](http://community.powerbi.com/)

