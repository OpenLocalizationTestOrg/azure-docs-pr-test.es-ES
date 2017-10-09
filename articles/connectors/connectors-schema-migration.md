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
# <a name="how-toomigrate-logic-apps-tooschema-version-2015-08-01-preview"></a><span data-ttu-id="374a7-104">¿Cómo toomigrate lógica aplicaciones tooschema versión 2015-08-01-versión preliminar</span><span class="sxs-lookup"><span data-stu-id="374a7-104">How toomigrate logic apps tooschema version 2015-08-01-preview</span></span>
<span data-ttu-id="374a7-105">toomove su lógica aplicaciones toohello nuevo esquema existente, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="374a7-105">toomove your existing logic apps toohello new schema, do hello following:</span></span>  

1. <span data-ttu-id="374a7-106">Abra la aplicación lógica en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="374a7-106">Open your logic app in hello Azure portal</span></span>  
2. <span data-ttu-id="374a7-107">Haga clic en Actualizar esquema:</span><span class="sxs-lookup"><span data-stu-id="374a7-107">Click Update Schema:</span></span>
   
   <span data-ttu-id="374a7-108">![Icono de API][step1] </span><span class="sxs-lookup"><span data-stu-id="374a7-108">![API Icon][step1] </span></span>  
   <span data-ttu-id="374a7-109">página de esquema de actualización de Hello muestra y proporciona un documento de tooa de vínculo que proporcionan los detalles sobre las mejoras de hello en el nuevo esquema de hello: ![icono de la API][step2]</span><span class="sxs-lookup"><span data-stu-id="374a7-109">hello Update Schema page displays and provides a link tooa document that provide details on hello improvements in hello new schema: ![API Icon][step2]</span></span>

> [!NOTE]
> <span data-ttu-id="374a7-110">Cuando se selecciona **actualizar esquema**, se ejecuta los pasos de migración de Hola automáticamente y se proporcionan salida de código de hello automáticamente.</span><span class="sxs-lookup"><span data-stu-id="374a7-110">When you select **Update Schema**, we automatically run hello migration steps and provide hello code output for you.</span></span> <span data-ttu-id="374a7-111">Puede usar este tooupdate la definición, sin embargo, asegúrese de seguir buenas prácticas de codificación como las que se describen en hello **prácticas recomendadas** sección más adelante.</span><span class="sxs-lookup"><span data-stu-id="374a7-111">You can use this tooupdate your definition, however, ensure you follow good coding practices such as those outlined in hello **Best practices** section below.</span></span>
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-toohello-latest-schema-version"></a><span data-ttu-id="374a7-112">Prácticas recomendadas para migrar la versión más reciente de esquema de la lógica aplicaciones toohello:</span><span class="sxs-lookup"><span data-stu-id="374a7-112">Best practices when migrating your Logic apps toohello latest schema version:</span></span>
* <span data-ttu-id="374a7-113">Hola copia migrado script tooa nueva lógica de aplicación: no se sobrescriben Hola antiguo uno hasta que haya completado la aplicación migrada hello confirmada y prueba funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="374a7-113">Copy hello migrated script tooa new Logic App - don't overwrite hello old one until you've completed your testing and confirmed hello migrated app works as expected.</span></span>
* <span data-ttu-id="374a7-114">Pruebe la aplicación lógica **antes de** ponerla en producción</span><span class="sxs-lookup"><span data-stu-id="374a7-114">Test your Logic app **before** putting in production</span></span>
* <span data-ttu-id="374a7-115">Una vez completada la migración, empieza a actualizar su Hola de lógica aplicaciones toouse [API administradas](apis-list.md) siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="374a7-115">After migration completes, start updating your Logic apps toouse hello [managed APIs](apis-list.md) where possible.</span></span> <span data-ttu-id="374a7-116">Por ejemplo, puede empezar a utilizar Dropbox v2, en cualquier ocasión que esté utilizando DropBox v1.</span><span class="sxs-lookup"><span data-stu-id="374a7-116">For example, you can start using Dropbox v2, whereever you are using DropBox v1.</span></span>

## <a name="whats-next"></a><span data-ttu-id="374a7-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="374a7-117">What's next</span></span>
* [<span data-ttu-id="374a7-118">Obtenga información acerca de cómo toomanually migrar las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="374a7-118">Learn how toomanually migrate your Logic apps</span></span>](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






