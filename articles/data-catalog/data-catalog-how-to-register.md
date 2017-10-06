---
title: "aaaRegister orígenes de datos en el catálogo de datos de Azure | Documentos de Microsoft"
description: "Este artículo destaca cómo extraen tooregister orígenes de datos en el catálogo de datos, incluidos los campos de metadatos de Hola durante el registro."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: bab89906-186f-4d35-9ffd-61b1d903905d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: efc8a852ddc9fb4bbacc7b0280477bd47814936f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-sources-in-azure-data-catalog"></a>Registro de orígenes de datos en Azure Data Catalog
## <a name="introduction"></a>Introducción
Azure Data Catalog es un servicio en la nube totalmente administrado que actúa como sistema de registro y de detección para orígenes de datos empresariales. En otras palabras, Data Catalog ayuda a los usuarios a detectar, comprender y usar orígenes de datos, así como a las organizaciones a obtener un mayor valor de sus datos. Hola primer paso toomaking un origen de datos puede detectar a través del catálogo de datos es tooregister ese origen de datos.

## <a name="register-data-sources"></a>Registrar orígenes de datos
Registro es Hola proceso de extracción de metadatos del origen de datos de Hola y copia esa toohello datos servicio catálogo de datos. Hola datos permanecen donde se encuentra actualmente y permanece bajo control de Hola de administradores de Hola y directivas del sistema actual Hola.

Hola tooregister un origen de datos siguientes:
1. En el portal del catálogo de datos de Azure hello, inicie la herramienta de registro de origen de datos de catálogo de datos de Hola. 
2. Inicie sesión con su cuenta profesional o educativa con hello mismo credenciales de Azure Active Directory que usan toosign en toohello portal.
3. Seleccione el origen de datos de Hola que desee tooregister.

Para obtener información paso a paso, vea hello [empezar a trabajar con el catálogo de datos de Azure](data-catalog-get-started.md) tutorial.

Después de que ha registrado el origen de datos de hello, catálogo Hola realiza un seguimiento de su ubicación y sus metadatos de índices. Los usuarios pueden buscar, examinar, detectar el origen de datos de hello y, a continuación, usar su tooit de tooconnect de ubicación mediante la aplicación hello o herramienta de su elección.

## <a name="supported-data-sources"></a>Orígenes de datos admitidos
Para ver una lista de orígenes de datos admitidos actualmente, consulte los [DSR de Data Catalog](data-catalog-dsr.md).

## <a name="structural-metadata"></a>Metadatos estructurales
Al registrar un origen de datos, la herramienta de registro de hello extrae información sobre la estructura de Hola de objetos de Hola que seleccione. Esta información es metadatos estructurales tooas que se hace referencia.

Para todos los objetos, estos metadatos estructurales incluyen la ubicación del objeto de hello, para que los usuarios detección Hola datos pueden utilizar ese objeto de información de toohello tooconnect en herramientas de cliente de Hola de su elección. Entre otros metadatos estructurales se incluyen el nombre y tipo del objeto, así como el nombre de atributo/columna y el tipo de datos.

## <a name="descriptive-metadata"></a>Metadatos descriptivos
Además toohello principales metadatos estructurales que se extraen del origen de datos de hello, herramienta de registro de origen de datos de hello extrae metadatos descriptivos. Para SQL Server Analysis Services y SQL Server Reporting Services, estos metadatos se toma de propiedades de descripción de hello expuestas por estos servicios. Para SQL Server, valores que se proporcionan con ms hello\_se extrae la descripción de la propiedad extendida. Para la base de datos de Oracle, Hola origen de datos registro herramienta extrae Hola comentarios columna de Hola a todos\_ficha\_ver comentarios.

En suma toohello metadatos descriptivos que se extraen del origen de datos de hello, los usuarios pueden especificar metadatos descriptivos mediante el uso de la herramienta de registro de origen de datos de Hola. Los usuarios pueden agregar etiquetas y pueden identificar a expertos para objetos de Hola que se va a registrar. Todos estos metadatos descriptivos son copian toohello servicio de catálogo de datos junto con los metadatos estructurales de Hola.

## <a name="include-previews"></a>Inclusión de vistas previas
De forma predeterminada, solo los metadatos se extraen de orígenes de datos y copian toohello servicio catálogo de datos, pero comprender que un origen de datos a menudo es más fácil si puede ver un ejemplo de datos de Hola que contiene.

Mediante la herramienta de registro de hello catálogo de datos de origen de datos, puede incluir una vista previa de instantánea de datos de hello en cada tabla y la vista que está registrada. Si elige vistas previas de tooinclude durante el registro, la herramienta de registro de hello incluye too20 registros de cada tabla y vista. A continuación, se copia esta instantánea toohello catálogo junto con los metadatos de hello estructural y descriptivo.

> [!NOTE]
> Las tablas anchas que tienen un gran número de columnas pueden tener menos de 20 registros incluidos en la vista previa.
>
>

## <a name="include-data-profiles"></a>Inclusión de los perfiles de datos
Tal y como vistas previas incluidas pueden proporcionar el contexto valiosa para los usuarios que buscan orígenes de datos en el catálogo de datos, incluido un perfil de datos puede ser más fácil de orígenes de datos de toounderstand detectado.

Mediante la herramienta de registro de hello catálogo de datos de origen de datos, puede incluir un perfil de datos para cada tabla y la vista que está registrada. Si decide tooinclude un perfil de datos durante el registro, la herramienta de registro de hello incluye estadísticas acumuladas sobre los datos de hello en cada tabla o vista, incluidos:

* número de Hola de filas y el tamaño de los datos de hello en el objeto de Hola.
* fecha de Hello para la actualización más reciente de Hola de datos de Hola y el esquema de objeto de Hola.
* número de Hola de registros null y valores distintos para las columnas.
* Hola mínimo, máximo, Media y desviación estándar de valores para las columnas.

A continuación, se copian estas estadísticas toohello catálogo junto con los metadatos de hello estructural y descriptivo.

> [!NOTE]
> Las columnas de texto y fecha no incluyen las estadísticas de promedio o desviación estándar en su perfil de datos.
>
>

## <a name="update-registrations"></a>Actualización de registros
Cómo registrar un origen de datos facilita detectable en el catálogo de datos al utilizar metadatos de Hola y opcional preview extraído durante el registro. Si el origen de datos de hello debe toobe actualizado en el catálogo de hello (por ejemplo, si Hola esquema de un objeto ha cambiado, se deben incluidas las tablas que se excluyeron originalmente o desea tooupdate Hola datos que se incluyen en las vistas previas de Hola), herramienta de registro de origen de datos de Hola se puede volver a ejecutar.

Al volver a registrar un origen de datos ya registrado se realiza una operación de combinación "upsert": los objetos existentes se actualizan al tiempo que los nuevos objetos se crean. Se conservan los metadatos proporcionados por los usuarios a través del portal del catálogo de datos de Hola.

## <a name="summary"></a>Resumen
Porque copia metadatos descriptivos y estructural de un servicio de catálogo de toohello de origen de datos, registrar el origen de datos de hello en el catálogo de datos hace que toodiscover sea más fácil de hello datos y comprender. Después de haber registrado el origen de datos de hello, puede anotar, administrar y descubrir mediante el portal del catálogo de datos de Hola.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre el registro de orígenes de datos, vea hello [empezar a trabajar con el catálogo de datos de Azure](data-catalog-get-started.md) tutorial.
