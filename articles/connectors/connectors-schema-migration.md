---
title: "Migración de aplicaciones lógicas a la versión de esquema 2015-08-01-preview | Microsoft Docs"
description: "Puede migrar fácilmente las aplicaciones lógicas a la última versión de esquema. Simplemente, siga estos pasos:"
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
ms.openlocfilehash: a5a73a9f124e5339b61dbc49021444a208a471f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-migrate-logic-apps-to-schema-version-2015-08-01-preview"></a><span data-ttu-id="b5e3c-104">Migración de aplicaciones lógicas a la versión de esquema 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="b5e3c-104">How to migrate logic apps to schema version 2015-08-01-preview</span></span>
<span data-ttu-id="b5e3c-105">Para mover las aplicaciones lógicas existentes al nuevo esquema, realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b5e3c-105">To move your existing logic apps to the new schema, do the following:</span></span>  

1. <span data-ttu-id="b5e3c-106">Abra la aplicación lógica en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b5e3c-106">Open your logic app in the Azure portal</span></span>  
2. <span data-ttu-id="b5e3c-107">Haga clic en Actualizar esquema:</span><span class="sxs-lookup"><span data-stu-id="b5e3c-107">Click Update Schema:</span></span>
   
   <span data-ttu-id="b5e3c-108">![Icono de API][step1] </span><span class="sxs-lookup"><span data-stu-id="b5e3c-108">![API Icon][step1] </span></span>  
   <span data-ttu-id="b5e3c-109">La página Actualizar esquema aparece y ofrece un vínculo a un documento que proporciona más información acerca de las mejoras del nuevo esquema: ![Icono de API][step2]</span><span class="sxs-lookup"><span data-stu-id="b5e3c-109">The Update Schema page displays and provides a link to a document that provide details on the improvements in the new schema: ![API Icon][step2]</span></span>

> [!NOTE]
> <span data-ttu-id="b5e3c-110">Al seleccionar **Actualizar esquema**, automáticamente se ejecutan los pasos de migración y se le proporciona la salida de código.</span><span class="sxs-lookup"><span data-stu-id="b5e3c-110">When you select **Update Schema**, we automatically run the migration steps and provide the code output for you.</span></span> <span data-ttu-id="b5e3c-111">Con ello puede actualizar la definición, sin embargo, asegúrese de seguir las buenas prácticas de codificación descritas en la sección **Procedimientos recomendados** de más adelante.</span><span class="sxs-lookup"><span data-stu-id="b5e3c-111">You can use this to update your definition, however, ensure you follow good coding practices such as those outlined in the **Best practices** section below.</span></span>
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-to-the-latest-schema-version"></a><span data-ttu-id="b5e3c-112">Procedimientos recomendados al migrar las aplicaciones lógicas a la última versión de esquema:</span><span class="sxs-lookup"><span data-stu-id="b5e3c-112">Best practices when migrating your Logic apps to the latest schema version:</span></span>
* <span data-ttu-id="b5e3c-113">Copie el script migrado a una nueva aplicación lógica: no sobrescriba el antiguo hasta que haya completado las pruebas y confirmado que la aplicación migrada funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="b5e3c-113">Copy the migrated script to a new Logic App - don't overwrite the old one until you've completed your testing and confirmed the migrated app works as expected.</span></span>
* <span data-ttu-id="b5e3c-114">Pruebe la aplicación lógica **antes de** ponerla en producción</span><span class="sxs-lookup"><span data-stu-id="b5e3c-114">Test your Logic app **before** putting in production</span></span>
* <span data-ttu-id="b5e3c-115">Una vez finalizada la migración, comience la actualización de las aplicaciones lógicas para usar las [API administradas](apis-list.md) siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="b5e3c-115">After migration completes, start updating your Logic apps to use the [managed APIs](apis-list.md) where possible.</span></span> <span data-ttu-id="b5e3c-116">Por ejemplo, puede empezar a utilizar Dropbox v2, en cualquier ocasión que esté utilizando DropBox v1.</span><span class="sxs-lookup"><span data-stu-id="b5e3c-116">For example, you can start using Dropbox v2, whereever you are using DropBox v1.</span></span>

## <a name="whats-next"></a><span data-ttu-id="b5e3c-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b5e3c-117">What's next</span></span>
* [<span data-ttu-id="b5e3c-118">Obtenga información sobre cómo migrar las aplicaciones lógicas de forma manual</span><span class="sxs-lookup"><span data-stu-id="b5e3c-118">Learn how to manually migrate your Logic apps</span></span>](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






