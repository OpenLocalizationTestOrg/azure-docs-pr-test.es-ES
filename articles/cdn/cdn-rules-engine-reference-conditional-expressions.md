---
title: expresiones condicionales de motor de reglas de aaaAzure CDN | Documentos de Microsoft
description: "Documentación de referencia sobre las condiciones y características de coincidencia del motor de reglas de la red CDN de Azure."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 39d0754c34a577f77ca87b6fd92e2b6a9e4ff8fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a><span data-ttu-id="f10bc-103">Expresiones condicionales del motor de reglas de la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="f10bc-103">Azure CDN rules engine conditional expressions</span></span>
<span data-ttu-id="f10bc-104">Este tema enumeran las descripciones detalladas de hello expresiones condicionales del red de entrega de contenido (CDN) para Azure [motor de reglas de](cdn-rules-engine.md).</span><span class="sxs-lookup"><span data-stu-id="f10bc-104">This topic lists detailed descriptions of hello Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="f10bc-105">primera parte de una regla de Hello es hello expresión condicional.</span><span class="sxs-lookup"><span data-stu-id="f10bc-105">hello first part of a rule is hello Conditional Expression.</span></span>

<span data-ttu-id="f10bc-106">Expresión condicional</span><span class="sxs-lookup"><span data-stu-id="f10bc-106">Conditional Expression</span></span> | <span data-ttu-id="f10bc-107">Descripción</span><span class="sxs-lookup"><span data-stu-id="f10bc-107">Description</span></span>
-----------------------|-------------
<span data-ttu-id="f10bc-108">IF</span><span class="sxs-lookup"><span data-stu-id="f10bc-108">IF</span></span> | <span data-ttu-id="f10bc-109">Una expresión IF siempre es una parte de la primera instrucción de hello en una regla.</span><span class="sxs-lookup"><span data-stu-id="f10bc-109">An IF expression is always a part of hello first statement in a rule.</span></span> <span data-ttu-id="f10bc-110">Al igual que las demás expresiones condicionales, esta instrucción IF debe asociarse a una coincidencia.</span><span class="sxs-lookup"><span data-stu-id="f10bc-110">Like all other conditional expressions, this IF statement must be associated with a match.</span></span> <span data-ttu-id="f10bc-111">Si no se han definido ningún expresiones condicionales adicionales, esta coincidencia determina criterio Hola que debe cumplirse antes de que un conjunto de características puede ser solicitud tooa aplicada.</span><span class="sxs-lookup"><span data-stu-id="f10bc-111">If no additional conditional expressions are defined, then this match determines hello criterion that must be met before a set of features may be applied tooa request.</span></span>
<span data-ttu-id="f10bc-112">AND IF</span><span class="sxs-lookup"><span data-stu-id="f10bc-112">AND IF</span></span> | <span data-ttu-id="f10bc-113">Una expresión si y solo puede agregarse después de hello siguientes tipos de expresiones condicional: IF, y si.</span><span class="sxs-lookup"><span data-stu-id="f10bc-113">An AND IF expression may only be added after hello following types of conditional expressions:IF,AND IF.</span></span> <span data-ttu-id="f10bc-114">Indica que hay otra condición que debe cumplirse para instrucción IF inicial de Hola.</span><span class="sxs-lookup"><span data-stu-id="f10bc-114">It indicates that there is another condition that must be met for hello initial IF statement.</span></span>
<span data-ttu-id="f10bc-115">ELSE IF</span><span class="sxs-lookup"><span data-stu-id="f10bc-115">ELSE IF</span></span>| <span data-ttu-id="f10bc-116">Una expresión o si especifica una condición alternativa que debe cumplirse antes de que realiza un conjunto de características específicas toothis instrucción ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="f10bc-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific toothis ELSE IF statement takes place.</span></span> <span data-ttu-id="f10bc-117">presencia de Hola de una instrucción ELSE IF indica final hello de la instrucción anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="f10bc-117">hello presence of an ELSE IF statement indicates hello end of hello previous statement.</span></span> <span data-ttu-id="f10bc-118">expresión condicional solo Hola que se puede colocar después de una instrucción ELSE IF es otra instrucción ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="f10bc-118">hello only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span></span> <span data-ttu-id="f10bc-119">Esto significa que una instrucción IF ELSE solo puede ser toospecify usa una única condición adicional que tiene toobe cumplen.</span><span class="sxs-lookup"><span data-stu-id="f10bc-119">This means that an ELSE IF statement may only be used toospecify a single additional condition that has toobe met.</span></span>

<span data-ttu-id="f10bc-120">**Ejemplo**: ![Condición de coincidencia de red CDN](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span><span class="sxs-lookup"><span data-stu-id="f10bc-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span></span>

 > [!TIP]
   > <span data-ttu-id="f10bc-121">Una regla subsiguientes puede invalidar las acciones de hello especificadas por una regla anterior.</span><span class="sxs-lookup"><span data-stu-id="f10bc-121">A subsequent rule may override hello actions specified by a previous rule.</span></span> <span data-ttu-id="f10bc-122">Ejemplo: Una regla de detección de todo protege todas las solicitudes a través de la autenticación basada en token.</span><span class="sxs-lookup"><span data-stu-id="f10bc-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span></span> <span data-ttu-id="f10bc-123">Se puede crear otra regla justo debajo de ella toomake una excepción para ciertos tipos de solicitudes.</span><span class="sxs-lookup"><span data-stu-id="f10bc-123">Another rule may be created directly below it toomake an exception for certain types of requests.</span></span>

### <a name="next-steps"></a><span data-ttu-id="f10bc-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f10bc-124">Next steps</span></span>
* [<span data-ttu-id="f10bc-125">Información general de la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="f10bc-125">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="f10bc-126">Referencia del motor de reglas</span><span class="sxs-lookup"><span data-stu-id="f10bc-126">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="f10bc-127">Condiciones de coincidencia del motor de reglas</span><span class="sxs-lookup"><span data-stu-id="f10bc-127">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="f10bc-128">Funciones del motor de reglas</span><span class="sxs-lookup"><span data-stu-id="f10bc-128">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="f10bc-129">Invalidar el comportamiento HTTP predeterminado mediante el motor de reglas de Hola</span><span class="sxs-lookup"><span data-stu-id="f10bc-129">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
