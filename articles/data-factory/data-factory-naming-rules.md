---
title: "aaaRules para asignar nombres a las entidades de la factoría de datos de Azure | Documentos de Microsoft"
description: "Describe las reglas de nomenclatura para las entidades de Factoría de datos."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 98c5fc5fc932b72b65894afad438b4dc321c8aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---naming-rules"></a>Azure Data Factory: reglas de nomenclatura
Hello en la tabla siguiente proporciona las reglas de nomenclatura para los artefactos de la factoría de datos.

| Nombre | Exclusividad del nombre | Comprobaciones de validación |
|:--- |:--- |:--- |
| Factoría de datos |Único en Microsoft Azure. Nombres distinguen mayúsculas de minúsculas, es decir, `MyDF` y `mydf` consulte toohello misma factoría de datos. |<ul><li>Cada factoría de datos es una suscripción a Azure tooexactly relacionados.</li><li>Nombres de objeto deben comenzar con una letra o un número y pueden contener solo letras, números y caracteres de guión (-) Hola.</li><li>Los caracteres de guión (-) debe estar inmediatamente precedidos y seguidos por una letra o un número. No se permiten guiones consecutivos en los nombres de contenedor.</li><li>El nombre puede tener entre 3 y 63 caracteres.</li></ul> |
| Servicios, tablas o canalizaciones vinculados |Único en una factoría de datos. Los nombres no distinguen mayúsculas de minúsculas. |<ul><li>Número máximo de caracteres incluido en un nombre de tabla: 260.</li><li>Los nombres de objeto deben empezar con una letra, un número o un carácter de subrayado (_).</li><li>No se permiten los caracteres siguientes: “.”, “+”, “?”, “/”, “<”, ”>”,”*”,”%”,”&”,”:”,”\\”</li></ul> |
| Grupo de recursos |Único en Microsoft Azure. Los nombres no distinguen mayúsculas de minúsculas. |<ul><li>Número máximo de caracteres: 1000.</li><li>Nombre puede contener letras, dígitos, hello y los caracteres siguientes: "-", "_",","y"."</li></ul> |

