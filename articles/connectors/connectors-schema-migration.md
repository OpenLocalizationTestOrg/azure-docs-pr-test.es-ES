---
title: "aaaHow toomigrate lógica aplicaciones tooschema versión 2015-08-01-vista previa | Documentos de Microsoft"
description: "Puede migrar fácilmente la versión más reciente de esquema de la lógica aplicaciones toohello. Simplemente, siga estos pasos:"
services: logic-apps
documentationcenter: 
author: MSFTMAN
manager: erikre
editor: 
tags: connectors
ms.assetid: 3e177e49-fd69-43e9-9b9b-218abb250c31
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: deonhe
ms.openlocfilehash: c7b42aaec547eddd28b0c649a3c0625047f9f805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-logic-apps-tooschema-version-2015-08-01-preview"></a>¿Cómo toomigrate lógica aplicaciones tooschema versión 2015-08-01-versión preliminar
toomove su lógica aplicaciones toohello nuevo esquema existente, Hola siguientes:  

1. Abra la aplicación lógica en hello portal de Azure  
2. Haga clic en Actualizar esquema:
   
   ![Icono de API][step1]   
   página de esquema de actualización de Hello muestra y proporciona un documento de tooa de vínculo que proporcionan los detalles sobre las mejoras de hello en el nuevo esquema de hello: ![icono de la API][step2]

> [!NOTE]
> Cuando se selecciona **actualizar esquema**, se ejecuta los pasos de migración de Hola automáticamente y se proporcionan salida de código de hello automáticamente. Puede usar este tooupdate la definición, sin embargo, asegúrese de seguir buenas prácticas de codificación como las que se describen en hello **prácticas recomendadas** sección más adelante.
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-toohello-latest-schema-version"></a>Prácticas recomendadas para migrar la versión más reciente de esquema de la lógica aplicaciones toohello:
* Hola copia migrado script tooa nueva lógica de aplicación: no se sobrescriben Hola antiguo uno hasta que haya completado la aplicación migrada hello confirmada y prueba funciona según lo previsto.
* Pruebe la aplicación lógica **antes de** ponerla en producción
* Una vez completada la migración, empieza a actualizar su Hola de lógica aplicaciones toouse [API administradas](apis-list.md) siempre que sea posible. Por ejemplo, puede empezar a utilizar Dropbox v2, en cualquier ocasión que esté utilizando DropBox v1.

## <a name="whats-next"></a>Pasos siguientes
* [Obtenga información acerca de cómo toomanually migrar las aplicaciones lógicas](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






