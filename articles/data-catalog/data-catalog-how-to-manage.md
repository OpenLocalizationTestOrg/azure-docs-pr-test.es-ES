---
title: "aaaManage activos de datos en el catálogo de datos de Azure | Documentos de Microsoft"
description: "artículo de Hello destaca cómo toocontrol visibilidad y la propiedad de activos de datos registran en el catálogo de datos."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 48a634b92d7da19c32c9e551f295eec257f54f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a>Administración de recursos de datos en Azure Data Catalog
## <a name="introduction"></a>Introducción
Catálogo de datos de Azure está diseñado para la detección de origen de datos, por lo que puede detectar fácilmente y comprender los orígenes de datos de hello necesita tooperform análisis y tomar decisiones. Estas capacidades de detección tener mayor impacto de hello cuando usted y otros usuarios pueden buscar y comprender la gama más amplia de Hola de orígenes de datos disponibles. Con estos elementos en mente, comportamiento predeterminado de hello del catálogo de datos es para todos los datos registrados orígenes toobe visible tooand reconocible por todos los usuarios del catálogo.

El catálogo de datos no le otorga acceso a los datos de toohello propio. Acceso a datos se controla mediante el propietario de Hola Hola del origen de datos. Con el catálogo de datos, puede detectar los orígenes de datos y ver los metadatos de Hola que son orígenes de toohello relacionados que están registrados en el catálogo de Hola.

Puede haber casos, sin embargo, en los orígenes de datos solo deberían resultar toospecific visible a los usuarios o toomembers de grupos específicos. En estos escenarios, los usuarios pueden tomar posesión de los activos de datos registrado en el catálogo de hello y, a continuación, controlar la visibilidad de Hola de activos de Hola que poseen.

> [!NOTE]
> funcionalidad de Hello descrita en este artículo solo está disponible en hello edición estándar de catálogo de datos de Azure. Hello edición gratuita no proporciona funciones para la propiedad y para restringir la visibilidad de recurso de datos.
>
>

## <a name="manage-ownership-of-data-assets"></a>Administración de la propiedad de los recursos de datos
De forma predeterminada, los activos de datos que están registrados en Data Catalog no tienen propietario. Cualquier usuario con permiso tooaccess Hola del catálogo puede detectar y anotar estos activos. Los usuarios pueden tomar posesión de activos de datos no poseído y, a continuación, limitar la visibilidad de Hola de activos de Hola que poseen.

Cuando es propiedad de un recurso de datos en el catálogo de datos, solo los usuarios que estén autorizados a los propietarios de hello pueden detectar asset hello y ver sus metadatos, y sólo los propietarios de hello pueden eliminar el recurso de Hola desde el catálogo de Hola.

> [!NOTE]
> Propiedad de catálogo de datos afecta a solo los metadatos de Hola que se almacenan en el catálogo de Hola. Propiedad no confiere ningún permiso en el origen de datos subyacente de Hola.
>
>

### <a name="take-ownership"></a>Toma de posesión
Los usuarios pueden tomar posesión de activos de datos seleccionando hello **Take Ownership** opción en el portal del catálogo de datos de Hola. No hay permisos especiales son tootake requiere la propiedad de un recurso de datos no poseído. Cualquier usuario puede tomar posesión de un recurso de datos sin propietario.

### <a name="add-owners-and-co-owners"></a>Adición de propietarios y copropietarios
Si un recurso de datos ya tiene propietario, los demás usuarios simplemente no podrán tomar posesión del mismo. Un propietario ya existente debe agregarles como copropietarios. Cualquier propietario puede agregar más usuarios o grupos de seguridad como copropietarios.

> [!NOTE]
> Es al menos dos usuarios como propietarios de un toohave de prácticas recomendada para cualquier propiedad de recurso de datos.
>
>

### <a name="remove-owners"></a>Eliminación de propietarios
Al igual que un propietario de recursos puede agregar copropietarios, cualquier propietario de recursos puede quitar a un copropietario.

Un propietario del recurso que se quita de él o su propio como un propietario no podrá administrar activos de Hola. Si el propietario del recurso de hello quita le o su propio como un propietario y no hay ningún otros los copropietarios, asset Hola revierte tooan no poseído estado.

## <a name="control-visibility"></a>Control de la visibilidad
Los propietarios del recurso de datos pueden controlar la visibilidad de Hola Hola de activos de datos que poseen. visibilidad de toorestrict como valor predeterminado de hello, donde Hola a todos los usuarios pueden detectar el catálogo de datos y ver datos activos, el propietario del recurso de hello puede alternar configuración de visibilidad de Hola de **todos** demasiado**propietarios y usuarios de estas** en Propiedades de Hola de activos de Hola. Los propietarios pueden después agregar usuarios y grupos de seguridad específicos.

> [!NOTE]
> Siempre que sea posible, deben asignarse permisos de propiedad y la visibilidad de activos toosecurity grupos y no tooindividual a los usuarios.
>
>

## <a name="catalog-administrators"></a>Administradores del Catálogo
Los administradores del catálogo de datos son implícitamente los copropietarios de todos los activos en el catálogo de Hola. Los propietarios de activos no pueden quitar la visibilidad de los administradores y los administradores pueden administrar la visibilidad de todos los activos de datos en el catálogo de Hola y propiedad.

## <a name="summary"></a>Resumen
Hola catálogo de datos crowdsourcing modelo toometadata y los datos activos detección permite que todos los catálogos a los usuarios toocontribute y detectar. Hola edición estándar de catálogo de datos está diseñado para la propiedad y la administración de visibilidad de hello toolimit y el uso de activos de datos específicos.
