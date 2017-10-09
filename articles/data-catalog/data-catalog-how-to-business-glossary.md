---
title: "aaaSet los glosarios empresariales de Hola para etiquetar los controlada en el catálogo de datos de Azure | Documentos de Microsoft"
description: "Cómo tooarticle Glosario de negocio de hello resaltado en el catálogo de datos para definir y utilizar un tootag de vocabulario empresarial común registrado activos de datos."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: b3d63dbe-1ae7-499f-bc46-42124e950cd6
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: c9adf663bd08ac3c0c7b5d3551e6af409fe69ebc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-business-glossary-for-governed-tagging"></a>Configurar glosarios empresariales de Hola para rige etiquetado
## <a name="introduction"></a>Introducción
Catálogo de datos de Azure habilita la detección de origen de datos, por lo que puede detectar fácilmente y comprender los orígenes de datos de Hola que necesita tooperform análisis y tomar decisiones. Estas capacidades convierten mayor impacto de hello cuando se puede encontrar y entender la gama más amplia de Hola de orígenes de datos disponibles.

Una característica del Catálogo de datos que promueve una mejor comprensión de los datos de recursos es el etiquetado. Mediante el uso de etiquetado, puede asociar palabras clave a un recurso o una columna, que a su vez resulta más fácil de activos de hello toodiscover a través de la búsqueda o la exploración. Etiquetado también más ayuda a comprender fácilmente el contexto de Hola y el propósito del activo de Hola.

Sin embargo, el etiquetado a veces puede causar problemas por sí mismo. Estos son algunos ejemplos de los problemas que puede presentar el etiquetado:

* Hola el uso de las abreviaturas en algunos activos y texto expandido en otras versiones. Esta incoherencia afecta negativamente al detección Hola de activos, aunque el intento de hello era activos de hello tootag con hello misma etiqueta.
* Posibles variaciones de significado en función del contexto. Por ejemplo, una etiqueta denominada *ingresos* en un cliente, conjunto de datos podría significar ingresos por cliente, pero hello misma etiqueta en un conjunto de datos de ventas trimestral, podría significar ingresos trimestrales para empresa Hola.  

toohelp resolver éstos y otros desafíos similares, el catálogo de datos incluye un glosario empresarial.

Mediante el uso de glosario de hello catálogo de datos empresariales, una organización puede documentar términos empresariales clave y su toocreate definiciones un vocabulario empresarial común. Este control permite coherencia en el uso de datos a través de la organización de Hola. Después de define un término de glosario empresarial de hello, que puede asignarse a tooa datos activos en el catálogo de Hola. Este enfoque, *rige etiquetado*, es Hola mismo enfoque como el etiquetado.

## <a name="glossary-availability-and-privileges"></a>Disponibilidad del glosario y privilegios
Glosario de Hello empresarial solo está disponible en hello edición estándar de catálogo de datos de Azure. Hello edición gratuita de catálogo de datos no incluye un glosario, y no proporciona funciones para etiquetar los controlados.

Puede tener acceso a los glosarios empresariales de Hola a través de hello **glosario** opción en el menú de navegación del portal del catálogo de datos de Hola.  

![Obtener acceso a los glosarios empresariales de Hola](./media/data-catalog-how-to-business-glossary/01-portal-menu.png)

Los administradores del catálogo de datos y los miembros de glosario de hello rol de los administradores pueden crear, editar y eliminar Glosario de términos de glosario empresarial de Hola. Todos los usuarios del catálogo de datos pueden ver definiciones de términos de Hola y activos de etiqueta con términos de glosario.

![Adición de nuevo término de glosario](./media/data-catalog-how-to-business-glossary/02-new-term.png)

## <a name="creating-glossary-terms"></a>Creación de términos de glosario
Los administradores del catálogo de datos y los administradores de glosario pueden crear términos del glosario haciendo clic en hello **nuevo término** botón. Cada término de glosario contiene Hola siguientes campos:

* Una definición de negocios durante el período de Hola
* Una descripción que captura Hola pensado reglas de uso o business de activos de Hola o columna
* Una lista de las partes interesadas que sabe hello más acerca de los términos de Hola
* término primario de Hello, que define la jerarquía de hello en qué Hola se organiza término

## <a name="glossary-term-hierarchies"></a>Jerarquías de términos de glosario
Mediante el uso de glosario de hello catálogo de datos empresariales, una organización puede describir su vocabulario empresarial como una jerarquía de términos y puede crear una clasificación de los términos que represente mejor su taxonomía de negocios.

Cada término debe ser único en un nivel determinado de jerarquía. No se permiten nombres duplicados. No hay ningún toohello limitar el número de niveles en una jerarquía, pero una jerarquía es a menudo más comprensible cuando hay tres niveles o menos.

uso de Hola de jerarquías en glosarios empresariales de hello es opcional. Dejando Hola campo primario por el término en blanco para los términos del glosario crea una lista plana (sin jerarquía) de términos en Glosario de Hola.  

## <a name="tagging-assets-with-glossary-terms"></a>Etiquetado de recursos con los términos del glosario
Después de definir los términos del glosario en el catálogo de hello, experiencia de Hola de etiquetado de activos es Glosario de hello toosearch optimizado como un usuario escribe una etiqueta. portal del catálogo de datos de Hello muestra una lista de búsqueda de coincidencias toochoose de términos de glosario de. Si el usuario de hello selecciona un término de glosario de lista de hello, se agrega el término de hello toohello asset como una etiqueta (también denominada una etiqueta de glosario). Hello usuario también puede elegir toocreate una nueva etiqueta escribiendo un término que no esté en hello Glosario (también denominada una etiqueta de usuario).

![Recurso de datos etiquetados con una etiqueta de usuario y dos etiquetas de glosario](./media/data-catalog-how-to-business-glossary/03-tagged-asset.png)

> [!NOTE]
> Usuario distinguen Hola solo tipo de etiqueta es compatible con Hola edición gratuita de catálogo de datos.
>
>

### <a name="hover-behavior-on-tags"></a>Comportamiento al mantener el puntero en las etiquetas
En el portal del catálogo de datos de hello, Hola dos tipos de etiquetas son comportamientos de desplazamiento diferentes visualmente distintos y se presente. Cuando mantenga el mouse sobre una etiqueta de usuario, puede ver el texto de etiqueta de Hola y Hola o varios usuarios que hayan agregado etiqueta Hola. Cuando mantenga el mouse sobre una etiqueta de glosario, también ver definición de Hola de término de glosario de Hola y una vínculo tooopen Hola business glosario tooview Hola definición completa de términos de Hola.

### <a name="search-filters-for-tags"></a>Filtros de búsqueda de etiquetas
Se pueden realizar búsquedas tanto en las etiquetas de glosario como en las de usuario y se pueden aplicar como filtros en una búsqueda.

## <a name="summary"></a>Resumen
Mediante el uso de glosario empresarial de hello en el catálogo de datos de Azure y Hola rige etiquetado permite, puede identificar, administrar e incluye los activos de datos de una manera coherente. Glosario de Hello empresarial puede promover aprendizaje de vocabulario empresarial de hello los miembros de la organización. Glosario de Hello también admite la captura de metadatos significativo, lo que simplifica la comprensión y detección de activos.

## <a name="next-steps"></a>Pasos siguientes
* [Documentación de API de REST para las operaciones del glosario empresarial](https://msdn.microsoft.com/library/mt708855.aspx)
