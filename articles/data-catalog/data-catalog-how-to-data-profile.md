---
title: "orígenes de datos de perfil de aaaHow tooData"
description: "Tooarticle cómo resaltar cómo los perfiles de datos de nivel de tabla y columna tooinclude para registrar orígenes de datos en el catálogo de datos de Azure y cómo datos toouse perfiles toounderstand orígenes de datos."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a>Orígenes de datos de perfiles de datos
## <a name="introduction"></a>Introducción
**Catálogo de datos de Microsoft Azure** es un servicio en la nube totalmente administrado que actúa como sistema de registro y de detección de orígenes de datos empresariales. En otras palabras, **el catálogo de datos** es todo acerca de las personas le ayuda a detectar, comprender y usar orígenes de datos, y ayudar a las organizaciones tooget más valor de sus datos existentes. Cuando se registra un origen de datos con **el catálogo de datos**, sus metadatos se copian y se indizan por servicio de hello, pero el caso de hello no termina aquí.

Hola **perfiles de datos** característica de **el catálogo de datos** examina Hola datos desde orígenes de datos admitidos en el catálogo y recopila las estadísticas e información sobre esos datos. Es fácil tooinclude un perfil de sus activos de datos. Al registrar un recurso de datos, elija **incluyen el perfil de datos** en la herramienta de registro de origen de datos de Hola.

## <a name="what-is-data-profiling"></a>¿Qué es la generación de perfiles de datos?
Generación de perfiles de datos examina los datos de Hola Hola origen de datos que se va a registrar y recopila las estadísticas e información sobre esos datos. Durante la detección del origen de datos, estas estadísticas pueden ayudarle a determinar la idoneidad de Hola de hello datos toosolve sus problemas empresariales.

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

Hello orígenes de datos siguientes admiten la generación de perfiles de datos:

* Vistas y tablas de SQL Server (incluidos Almacenamiento de datos SQL y Base de datos SQL de Azure)
* Vistas y tablas de Oracle
* Vistas y tablas de Teradata
* Tablas de Hive

Incluir los perfiles de datos al registrar lo recursos de datos ayuda a los usuarios a responder preguntas acerca de los orígenes de datos, incluidas:

* ¿Puede ser usado toosolve mi problema empresarial?
* ¿Ajustan datos hello tooparticular estándares o patrones?
* ¿Cuáles son algunas de las anomalías de Hola Hola del origen de datos?
* ¿Cuáles son los posibles retos de integración de estos datos en mi aplicación?

> [!NOTE]
> También puede agregar documentación tooan asset toodescribe cómo se pueden integrar datos en una aplicación. Vea [cómo orígenes de datos de toodocument](data-catalog-how-to-documentation.md).
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a>Cómo generar perfiles de datos tooinclude al registrar un origen de datos
Es fácil tooinclude un perfil del origen de datos. Al registrar un origen de datos, en hello **toobe de objetos registrado** el panel del registro del origen de datos de Hola de herramientas, elija **incluyen el perfil de datos**.

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

toolearn Obtenga más información sobre cómo ver los orígenes de datos de tooregister, [cómo orígenes de datos de tooregister](data-catalog-how-to-register.md) y [empezar a trabajar con el catálogo de datos](data-catalog-get-started.md).

## <a name="filtering-on-data-assets-that-include-data-profiles"></a>Filtrado de recursos de datos que incluyen perfiles de datos
toodiscover los activos de datos que incluyen un perfil de datos, puede incluir `has:tableDataProfiles` o `has:columnsDataProfiles` como uno de los términos de búsqueda.

> [!NOTE]
> Seleccionar **incluyen el perfil de datos** en datos Hola herramienta de registro de origen incluye la tabla y la información de perfil de nivel de columna. Sin embargo, hello API de catálogo de datos permite toobe de activos de datos registrado con un solo conjunto de información de perfil incluida.
>
>

## <a name="viewing-data-profile-information"></a>Visualización de la información del perfil de datos
Una vez que encuentre un origen de datos adecuado con un perfil, puede ver detalles del perfil de datos Hola. datos de hello tooview perfil, seleccione un recurso de datos y elija **perfil de datos** en la ventana del portal Hola catálogo de datos.

![](media/data-catalog-data-profile/data-catalog-view.png)

Un perfil de datos del **Catálogo de datos de Azure** muestra la información del perfil de tabla y columna, incluido lo siguiente:

### <a name="object-data-profile"></a>Perfil de datos de objeto
* Número de filas
* Tamaño de la tabla
* Se actualizó por última vez el objeto de Hola

### <a name="column-data-profile"></a>Perfil de datos de columna
* Tipo de datos de columna
* Número de valores distintivos
* Número de filas con valores NULL
* Mínimo, máximo, promedio y desviación estándar para los valores de las columnas

## <a name="summary"></a>Resumen
Datos de generación de perfiles proporciona estadísticas y obtener información sobre registrado toohelp de activos de datos determina la idoneidad de Hola Hola datos toosolve problemas del negocio. Junto con la anotación y documentación de los orígenes de datos, los perfiles de datos pueden dar a los usuarios una comprensión más profunda de los datos.

## <a name="see-also"></a>Otras referencias
* [¿Cómo tooregister los orígenes de datos](data-catalog-how-to-register.md)
* [Introducción al Catálogo de datos de Azure](data-catalog-get-started.md)
