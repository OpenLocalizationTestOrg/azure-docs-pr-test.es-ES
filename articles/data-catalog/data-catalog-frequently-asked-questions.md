---
title: "Catálogo de datos de preguntas más frecuentes aaaAzure | Documentos de Microsoft"
description: "Preguntas más frecuentes sobre el Catálogo de datos de Azure, incluidas las funciones de detección de origen de datos, anotación y administración."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 5c7e209a-458c-4bb4-96bb-7ed178f9528a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 03f9f4b801640b2e14232c62c8fc168e42e2c393
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-frequently-asked-questions"></a>Preguntas frecuentes sobre el Catálogo de datos de Azure
Este artículo proporciona respuestas toofrequently más frecuentes tiene preguntas relacionadas con el servicio de catálogo de datos de Azure toohello.

## <a name="what-is-azure-data-catalog"></a>¿Qué es Azure Data Catalog?
Data Catalog es un servicio totalmente administrado, hospedado en Microsoft Azure, que actúa como sistema de registro y detección de orígenes de datos empresariales. Con el catálogo de datos, cualquier usuario, los científicos de toodata analistas y desarrolladores, puede registrar, detectar, comprender y consumir orígenes de datos.

## <a name="what-customer-challenges-does-it-solve"></a>¿Qué problemas de los clientes soluciona?
Direcciones de datos de catálogo Hola retos de detección de origen de datos y "datos oscuros" para que los usuarios pueden detectar y entender los orígenes de datos empresariales.

## <a name="what-are-its-target-audiences"></a>¿Cuáles son sus audiencias de destino?
Data Catalog está diseñado tanto para usuarios técnicos como para no técnicos, entre los que se incluyen:

* Los desarrolladores de datos y profesionales de BI y análisis: personas que son responsables de generar los datos y análisis de contenido para que otros lo tooconsume.
* Los administradores de datos: personas que tengan conocimiento de hello sobre Hola datos, lo que significa y cómo es toobe previsto usar.
* Los consumidores de datos: las personas que necesita tooeasily de toobe capaz de detectar, comprender y conectar datos toohello necesitan toodo su trabajo, utilizando la herramienta de Hola de su elección.
* Central TI: personas que necesitan toomake cientos de orígenes de datos reconocible por los usuarios empresariales, y que necesitan supervisión toomaintain sobre cómo se usa datos y por quién.

## <a name="what-is-its-availability-by-region"></a>¿Cuál es su disponibilidad por región?
Servicios de datos de catálogo están actualmente disponibles en hello después de centros de datos:

* Oeste de EE. UU.
* Este de EE. UU.
* Europa occidental
* Europa del Norte
* Australia Oriental
* Sudeste asiático

## <a name="what-are-its-limits-on-hello-number-of-data-assets"></a>¿Cuáles son sus límites del número de Hola de activos de datos?
Hola edición gratuita de catálogo de datos es too5 limitado, activos de datos registrados 000.

Hola edición estándar de catálogo de datos admite la too100, 000 recursos de datos registrados.

## <a name="what-are-its-supported-data-source-and-asset-types"></a>¿Cuáles son los tipos de recursos y orígenes de datos que admite?
Para ver una lista de orígenes de datos admitidos actualmente, consulte los [DSR de Data Catalog](data-catalog-dsr.md).

## <a name="how-do-i-request-support-for-another-data-source"></a>¿Cómo solicito soporte técnico para otro origen de datos?
toosubmit cuentan con las solicitudes y otros comentarios, vaya toohello [foro del catálogo de datos de Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="how-do-i-get-started-with-data-catalog"></a>¿Cómo empiezo a usar Data Catalog?
Hola tooget de mejor manera iniciado es yendo demasiado[cómo empezar a usar el catálogo de datos](data-catalog-get-started.md). Este artículo es una introducción to-end capacidades de hello en el servicio de Hola.

## <a name="how-do-i-register-my-data"></a>¿Cómo registro mis datos?
tooregister los datos en el catálogo de datos:
1. En portal del catálogo de datos de Azure hello, Hola **publicar** área, la herramienta de registro de inicio Hola el catálogo de datos. 
2. Hola catálogo de datos de publicación de aplicación, inicie sesión con hello igual credenciales que use tooaccess Hola portal del catálogo de datos.
3. Seleccionar origen de datos de Hola y determinados recursos de Hola que desea tooregister.

## <a name="what-properties-does-it-extract-for-data-assets-that-are-registered"></a>¿Qué propiedades extrae de los recursos de datos que se registran?
propiedades específicas de Hello difieren de origen de toodata de origen de datos pero, en general, Hola servicio de publicación del catálogo de datos extrae Hola siguiente información:

* Nombre de recurso
* Tipo de recurso
* Descripción de activos
* Nombres de columna o atributo
* Tipos de datos de columna o atributo
* Descripción de la columna o atributo

> [!IMPORTANT]
> Registrar activos de datos con el catálogo de datos no se mueva o copie los datos toohello en la nube. Registrar activos desde un origen de datos copias Hola tooAzure de metadatos de activos, pero los datos de hello permanecen en la ubicación de origen de datos existente de Hola. regla de toothis de excepción de Hello está si elige un perfil de datos o de registros de la vista previa de tooupload al registrar los activos de Hola. Al incluir una vista previa, una too20 registros se copian desde cada activo y almacena como una instantánea en el catálogo de datos. Al incluir un perfil de datos, información de agregado se calcula y se incluyen en los metadatos de Hola que se almacenan en el catálogo de Hola. Agregar información puede incluir Hola tamaño de las tablas, Hola porcentaje de valores null por columna, o hello mínimo, máximo y promedio valores para las columnas. 
>
>

> [!NOTE]
> Para orígenes de datos, como SQL Server Analysis Services que tienen una primera clase **descripción** propiedad, Hola catálogo de datos de publicación de aplicación extrae ese valor de propiedad. Para bases de datos relacionales de SQL Server, que carecen de una primera clase **descripción** propiedad, Hola aplicación de publicación en el catálogo de datos extrae el valor de Hola de hello **ms_description** propiedad extendida para los objetos y columnas. Para más información, consulte [Usar propiedades extendidas en objetos de base de datos](https://technet.microsoft.com/library/ms190243%28v=sql.105%29.aspx).
>
>

## <a name="how-long-should-it-take-for-newly-registered-assets-tooappear-in-hello-catalog"></a>¿Cuánto tiempo debe llevar para tooappear activos recién registrado en el catálogo de hello?
Después de registrar activos con el catálogo de datos, puede haber un período de 5 segundos too10 antes de que aparezcan en el portal del catálogo de datos de Hola.

## <a name="how-do-i-annotate-and-enrich-hello-metadata-for-my-registered-data-assets"></a>¿Cómo se puede anotar y enriquecer los metadatos de Hola para mi activos de datos registrada?
metadatos de tooprovide de manera más sencilla de Hola para recursos registrados es tooselect Hola activo en el portal del catálogo de datos de hello y, a continuación, escriba los valores de hello en el panel de propiedades de Hola o panel de esquema para el objeto seleccionado de Hola.

También puede proporcionar algunos metadatos, como etiquetas y expertos durante el proceso de registro de hello. los valores de Hello que proporcionar en el servicio de publicación del catálogo de datos de hello aplican activos tooall va a registrar en ese momento. Hola tooview registrado recientemente objetos en el portal de hello para la anotación adicional, seleccione hello **Portal de vista** botón en la pantalla de bienvenida final del programa Hola a aplicación de publicación en el catálogo de datos.

## <a name="how-do-i-delete-my-registered-data-objects"></a>¿Cómo elimino los objetos de datos registrados?
Puede eliminar un objeto de catálogo de datos seleccionando el objeto de hello en el portal de hello y, a continuación, haga clic en hello **eliminar** botón. Quitar objetos de hello quita los metadatos del catálogo de datos pero no afecta al origen de datos subyacente de Hola.

## <a name="what-is-an-expert"></a>¿Qué es un experto?
Un experto es una persona que tiene una perspectiva informada acerca de un objeto de datos. Un objeto puede tener varios expertos. Un experto no necesita toobe Hola "propietario" de un objeto, pero simplemente alguien que sabe cómo datos Hola pueden y debe utilizarse.

## <a name="how-do-i-share-information-with-hello-data-catalog-team-if-i-encounter-problems"></a>¿Cómo compartir información con el equipo del catálogo de datos de hello si producen problemas?
problemas de tooreport, compartir información y hacer preguntas, vaya toohello [foro del catálogo de datos de Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="does-hello-catalog-work-with-another-data-source-that-im-interested-in"></a>¿Hola trabajo de catálogo con otro origen de datos que me interesa?
Estamos trabajando activamente para agregar más tooData de orígenes de datos catálogo. Si desea toosee admite un origen de datos específico, sugieren (o el soporte técnico de voz si ya se han sugerido) por van toohello [foro del catálogo de datos de Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="how-is-azure-data-catalog-related-toohello-data-catalog-in-power-bi-for-office-365"></a>¿Cómo es el catálogo de datos relacionados con toohello catálogo de datos en Power BI para Office 365?
El catálogo de datos se puede considerar como una evolución del catálogo de datos en Power BI Hola. A partir de primavera de 2017, el catálogo de datos es tooenable usado Hola uso compartido y la detección de las consultas en Excel 2016 y Power Query para Excel. Capacidades del catálogo de datos de Excel están disponibles toousers con licencias de Power BI Pro.

## <a name="what-permissions-do-i-need-tooregister-assets-with-data-catalog"></a>¿Qué permisos necesito tooregister activos con el catálogo de datos?
herramienta de registro de catálogo de datos de hello toorun, necesita permisos en el origen de datos de Hola que le permite tooread Hola metadatos de origen de Hola. tooalso incluye una vista previa, debe tener permisos que permitan que tooread de datos de Hola de objetos de Hola que se va a registrar.

## <a name="will-data-catalog-be-made-available-for-on-premises-deployment-as-well"></a>¿Estará Data Catalog disponible también para las implementaciones locales?
El catálogo de datos es un servicio de nube que puede trabajar con toodeliver de orígenes de datos en la nube y local de una solución de detección del origen de datos híbrida. No está prevista para una versión de Hola servicio catálogo de datos que se ejecuta en local.

## <a name="can-i-extract-more-or-richer-metadata-from-hello-data-sources-i-register"></a>¿Se puede extraer metadatos de un o más de orígenes de datos de hello que puedo registrar?
Estamos trabajando activamente las capacidades de hello tooexpand del catálogo de datos. Si desea extraer del origen de datos de Hola durante el registro de metadatos adicionales toohave, sugerir (ni voto para él, si ya se han sugerido) en hello [foro del catálogo de datos de Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409). Hola futuras, permitiremos que a terceros tooadd nuevos tipos de orígenes de datos a través de una API de extensibilidad.

## <a name="how-do-i-restrict-hello-visibility-of-registered-data-assets-so-that-only-certain-people-can-discover-them"></a>¿Cómo se restringe visibilidad Hola de activos de datos registrada, para que sólo determinadas personas puedan detectar ellos?
Seleccione los activos de datos de Hola Hola catálogo de datos y, a continuación, haga clic en hello **Take Ownership** botón. Los propietarios de activos de datos en el catálogo de datos pueden cambiar la visibilidad de hello tooeither configuración Permitir Hola de toodiscover todos los usuarios activos de propiedad o restringir a los usuarios de toospecific de visibilidad.

## <a name="how-do-i-update-hello-registration-for-a-data-asset-so-that-changes-in-hello-data-source-are-reflected-in-hello-catalog"></a>¿Cómo actualizar el registro de hello para un recurso de datos para que los cambios en el origen de datos de Hola se reflejan en el catálogo de hello?
tooupdate Hola metadatos para los activos de datos que ya están registrados en el catálogo de hello, basta con volver a registrar origen de datos de Hola que contiene los activos de Hola. Los cambios en el origen de datos de hello, como columnas que se agregan o quitan en tablas o vistas, se actualizan en el catálogo de hello, pero se conservan las anotaciones proporcionadas por los usuarios.

## <a name="my-question-isnt-answered-here-where-can-i-go-for-answers"></a>No encuentro ninguna respuesta a mi pregunta. ¿Dónde puedo encontrarla?
Vaya toohello [foro del catálogo de datos de Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409). Las preguntas formuladas ahí tendrán respuesta aquí.
