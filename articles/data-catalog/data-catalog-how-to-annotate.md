---
title: "orígenes de datos de aaaHow tooannotate | Documentos de Microsoft"
description: "Tooarticle cómo resaltar cómo tooannotate activos de datos en el catálogo de datos, incluidos los nombres descriptivos, etiquetas, descripciones y expertos."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 5a7e6bb2-863c-4eca-b614-1c814920d9ed
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 1d1ef34e3f1ef73cdc65129209d938abe1e36c01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooannotate-data-sources"></a>¿Cómo tooannotate los orígenes de datos
## <a name="introduction"></a>Introducción
**Catálogo de datos de Microsoft Azure** es un servicio en la nube totalmente administrado que actúa como sistema de registro y de detección de orígenes de datos empresariales. En otras palabras, el catálogo de datos es fundamentalmente en ayudar a las personas detectar, comprender y usar orígenes de datos y ayudar a las organizaciones tooget más valor de sus datos existentes. Cuando un origen de datos se registra con el catálogo de datos, sus metadatos se copian y se indizan por servicio de hello, pero el caso de hello no termina aquí. El catálogo de datos permite usuarios tooprovide sus propios metadatos de metadatos descriptivos, como descripciones y etiquetas – toosupplement Hola extraídos de origen de datos de Hola y más comprensibles toomore personas del origen de datos de hello toomake.

## <a name="annotation-and-crowdsourcing"></a>Anotación y micromecenazgo
Todo el mundo tiene una opinión. Y eso es algo bueno.
Data Catalog reconoce que distintos usuarios tienen diferentes perspectivas sobre los orígenes de datos empresariales y que cada una de estas perspectivas puede ser valiosa. Considere la posibilidad de hello siguiendo el escenario:

* el administrador del sistema de Hello sabe contrato de nivel de servicio de Hola para servidores de Hola o servicios de ese origen de datos de Hola de host.
* Administrador de base de datos de Hello sabe copia de seguridad de hello programar para cada base de datos y Hola ventanas de procesamiento de ETL permitidos.
* propietario del sistema Hola sabe proceso hello para el origen de datos de los usuarios toorequest access toohello.
* Administrador de datos de Hello sabe cómo se asignan los activos de Hola y atributos de origen de datos de hello toohello modelo de datos de empresa.
* analista de Hello sabe cómo se usan datos de hello en el contexto de Hola Hola de procesos de negocios que admite.

Cada una de estas perspectivas es importantes y catálogo de datos utiliza un toometadata de enfoque crowdsourcing que permite que cada uno toobe captura y utiliza tooprovide una imagen completa de los orígenes de datos registrados. Mediante el portal del catálogo de datos de hello, cada usuario puede agregar y editar sus propias anotaciones, mientras que se va a anotaciones tooview pueda proporcionadas por otros usuarios.

## <a name="different-types-of-annotations"></a>Distintos tipos de anotaciones
Hola de datos catálogo admite siguientes tipos de anotaciones:

| Anotación | Notas |
| --- | --- |
| Nombre descriptivo |Pueden proporcionar nombres descriptivos en hello datos activos, activos de datos de hello toomake más comprensión. Nombres descriptivos son muy útiles cuando el nombre del objeto de hello subyacente es toousers críptico, abreviada o en caso contrario, no tiene ningún significado. |
| Descripción |Se pueden proporcionar descripciones en el recurso de datos de Hola y atributo / niveles de columna. Las descripciones son anotaciones de texto breve de forma libre que describen la perspectiva del usuario de hello en datos activos de Hola o su uso. |
| Etiquetas (etiquetas de usuario) |Etiquetas pueden proporcionarse en el recurso de datos de Hola y atributo / niveles de columna. Las etiquetas de usuario son las etiquetas definidas por el usuario que pueden ser utilizados toocategorize datos activos o atributos. |
| Etiquetas (etiquetas de glosario) |Etiquetas pueden proporcionarse en el recurso de datos de Hola y atributo / niveles de columna. Etiquetas de glosario son los términos de glosario definidas centralmente que pueden ser utilizados toocategorize datos activos o atributos con una taxonomía empresarial común. Para obtener más información, vea [cómo tooset seguridad Hola glosarios empresariales para etiquetar los rige](data-catalog-how-to-business-glossary.md) |
| Expertos |Pueden proporcionarse expertos en nivel de hello datos activos. Expertos identifican usuarios o grupos con perspectivas expertas en datos de Hola y pueden servir como puntos de contacto para los usuarios que detectar Hola registrar orígenes de datos y tienen alguna pregunta que no se responde en anotaciones existentes Hola. |
| Solicitar acceso |Información de solicitud de acceso puede ser proporcionado en el nivel de activos de datos de Hola. Esta información está destinada a los usuarios que detección un origen de datos que no tienen aún tooaccess de permisos. Los usuarios pueden especificar la dirección de correo electrónico de saludo del usuario de Hola o grupo que concede acceso, Hola dirección URL del proceso de Hola o herramienta que necesite toogain acceso de los usuarios o puede escribir el propio proceso hello como texto. |
| Documentación |Documentación puede ser proporcionada en el nivel de activos de datos de Hola. La documentación sobre recursos es información de texto enriquecido que puede incluir vínculos e imágenes y proporcionar información que no es posible transmitir a través de descripciones y etiquetas. |

## <a name="annotating-multiple-assets"></a>Anotación de varios recursos
Al seleccionar varios activos de datos en el portal del catálogo de datos de hello, los usuarios pueden anotar todos los recursos seleccionados en una sola operación. Las anotaciones se aplican activos tooall seleccionado, lo que tooselect fácil y proporcione una descripción coherente y conjuntos de expertos del mundo y etiquetas para los activos de datos relacionados.

> [!NOTE]
> Etiquetas y expertos también se puede proporcionar cuando la herramienta de registro del origen de registrar activos de datos con datos del catálogo de datos de Hola.
>
>

Al seleccionar varias tablas y vistas, solo las columnas que todos los datos activos se tienen en común seleccionados se mostrará en el portal del catálogo de datos de Hola. Esto permite etiquetas de tooprovide de los usuarios y las descripciones de todas las columnas con el mismo nombre de Hola para todos los recursos seleccionados.

## <a name="annotations-and-discovery"></a>Anotaciones y detección
Al igual que Hola metadatos extraídos del origen de datos de Hola durante el registro se agregan toohello índice de búsqueda de catálogo de datos, también se indizan los metadatos proporcionados por el usuario. Esto significa que no solo hacen anotaciones que sea más fácil para los datos de los usuarios toounderstand Hola descubren, anotaciones también facilitan los usuarios toodiscover Hola anotado con activos de datos mediante una búsqueda con términos de Hola que hacen toothem de sentido.

## <a name="summary"></a>Resumen
Cómo registrar un origen de datos con el catálogo de datos hace que esos datos reconocible copiando metadatos estructurales y descriptivo del origen de datos de hello en hello servicio del catálogo. Una vez que se ha registrado un origen de datos, los usuarios pueden proporcionar anotaciones toomake más fácil toodiscover y entender desde dentro el portal del catálogo de datos de Hola.

## <a name="see-also"></a>Otras referencias
* [Empezar a trabajar con el catálogo de datos de Azure](data-catalog-get-started.md) tutorial para obtener detalles paso a paso acerca de cómo tooannotate los orígenes de datos.
