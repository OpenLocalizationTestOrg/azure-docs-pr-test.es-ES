---
title: "orígenes de aaaHow tooconnect toodata | Documentos de Microsoft"
description: "Tooarticle cómo resaltar cómo tooconnect toodata orígenes detectan con el catálogo de datos de Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 4e6b27a5-cf75-4012-b88c-333c1fe638e8
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 01d659510c8e67c1238ed488f4eebf511aab7217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-toodata-sources"></a>Cómo tooconnect toodata orígenes
## <a name="introduction"></a>Introducción
**Catálogo de datos de Microsoft Azure** es un servicio en la nube totalmente administrado que actúa como sistema de registro y de detección de orígenes de datos empresariales. En otras palabras, **el catálogo de datos** es todo acerca de las personas le ayuda a detectar, comprender y usar orígenes de datos, y ayudar a las organizaciones tooget más valor de sus datos existentes. Un aspecto clave de este escenario usa Hola origen de datos: una vez que un usuario detecta una datos y entiende su propósito, Hola siguiente paso es tooput del origen de datos de toohello tooconnect su toouse de datos.

## <a name="data-source-locations"></a>Ubicaciones de orígenes de datos
Durante el registro del origen de datos, **el catálogo de datos** recibe metadatos sobre el origen de datos de Hola. Estos metadatos incluyen detalles de Hola de ubicación del origen de datos de Hola. Hola detalles de ubicación de hello varían de origen de toodata de origen de datos, pero siempre contendrá hello tooconnect de información necesaria. Por ejemplo, ubicación de Hola para una tabla de SQL Server incluye el nombre del servidor de hello, nombre de base de datos, nombre de esquema y nombre de tabla, mientras la ubicación de Hola para un informe de SQL Server Reporting Services incluye el nombre del servidor de Hola y el informe de toohello de ruta de acceso de Hola. Otros tipos de orígenes de datos tendrá ubicaciones que reflejan la estructura de Hola y capacidades del sistema de origen de Hola.

## <a name="integrated-client-tools"></a>Herramientas de cliente integradas
el origen de datos para tooa el más sencillo tooconnect manera Hello es hello toouse "abrir en..." menú de hello **el catálogo de datos** portal. Este menú muestra una lista de opciones para conectarse toohello activos de datos seleccionado.
Cuando se usa la vista en mosaico predeterminado hello, este menú está disponible en Hola cada mosaico.

 ![Abriendo una tabla de SQL Server en Excel del icono de hello datos activos](./media/data-catalog-how-to-connect/data-catalog-how-to-connect1.png)

Cuando se usa la vista de lista de hello, menú Hola está disponible en barra de búsqueda de hello en parte superior de Hola de ventana del portal Hola.

 ![Abrir un informe de SQL Server Reporting Services en el Administrador de informes de la barra de búsqueda de Hola](./media/data-catalog-how-to-connect/data-catalog-how-to-connect2.png)

## <a name="supported-client-applications"></a>Aplicaciones de cliente admitidas
Cuando se usa Hola "abrir en..." orígenes de menú para los datos en el portal del catálogo de datos de Azure de hello, aplicación de cliente correcto de hello debe instalarse en el equipo cliente de Hola.

| Abrir en la aplicación | Extensión de archivo o protocolo | Versiones de aplicación admitidas |
| --- | --- | --- |
| Excel |.odc |Excel 2010 o posterior |
| Excel (primeros 1000) |.odc |Excel 2010 o posterior |
| Power Query |.xlsx |Instalado Excel 2016 o Excel 2010 o Excel 2013 con hello Power Query para el complemento de Excel |
| Power BI Desktop |.pbix |Power BI Desktop de julio de 2016 o posterior |
| SQL Server Data Tools |vsweb:// |Visual Studio 2013 Update 4 o posterior con las herramientas de SQL Server instaladas |
| Administrador de informes |http:// |Consulte los [requisitos del explorador para SQL Server Reporting Services](https://technet.microsoft.com/en-us/library/ms156511.aspx) |

## <a name="your-data-your-tools"></a>Sus propios datos y herramientas
Opciones de Hello disponibles en el menú de hello dependerán de tipo hello de datos activos actualmente seleccionado. Por supuesto, no todas las herramientas posibles se incluirán en hello "abrir en..." menú, pero es el origen de datos de toohello tooconnect fácil mediante cualquier herramienta de cliente. Cuando se selecciona un recurso de datos en hello **el catálogo de datos** portal, se muestra en el panel de propiedades de hello ubicación completa Hola.

 ![Información de conexión de una tabla de SQL Server](./media/data-catalog-how-to-connect/data-catalog-how-to-connect3.png)

información de conexión de Hello detalles se diferenciarán del tipo de origen de toodata del tipo de origen de datos, pero la información de hello incluido en el portal de hello, tendrá todo lo que necesita el origen de datos de tooconnect toohello en cualquier herramienta de cliente. Los usuarios pueden copiar los detalles de la conexión de Hola Hola orígenes de datos que han descubierto mediante **el catálogo de datos**, lo que les toowork con datos de hello en la herramienta de elección.

## <a name="connecting-and-data-source-permissions"></a>Permisos de origen de datos y conexión
Aunque **el catálogo de datos** hace que los orígenes de datos access reconocible, datos toohello propio permanecen bajo el control de hello del propietario del origen de datos de Hola o administrador. Detección de un origen de datos en **el catálogo de datos** no conceder a un usuario los permisos tooaccess Hola propio origen de datos.

toomake que es más fácil para los usuarios que detección un datos de origen pero no tiene permiso tooaccess sus datos, los usuarios pueden proporcionar información en hello propiedad solicitar acceso al anotar un origen de datos. Se presenta la información proporcionada aquí, incluidos el proceso de toohello vínculos o punto de contacto para obtener acceso al código fuente de datos – junto con información de ubicación de origen de datos de hello en el portal de Hola.

 ![Información de conexión con las instrucciones de solicitud de acceso proporcionadas](./media/data-catalog-how-to-connect/data-catalog-how-to-connect4.png)

## <a name="summary"></a>Resumen
Cómo registrar un origen de datos con **el catálogo de datos** hace que los datos sean reconocibles copiando metadatos estructurales y descriptivo del origen de datos de hello en hello servicio del catálogo. Una vez que un origen de datos se ha registrado y detectados, los usuarios pueden conectarse a origen de datos de toohello de hello **el catálogo de datos** portal "abrir en..." " o con las herramientas de datos que prefieran.

## <a name="see-also"></a>Otras referencias
* [Empezar a trabajar con el catálogo de datos de Azure](data-catalog-get-started.md) tutorial para obtener detalles paso a paso acerca de cómo tooconnect toodata orígenes.
