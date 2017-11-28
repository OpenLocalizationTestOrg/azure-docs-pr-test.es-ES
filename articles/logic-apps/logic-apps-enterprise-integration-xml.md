---
title: "los mensajes de aaaWorking con XML en los flujos de trabajo: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Procesar, validar, transformar y enriquecer XML mensajes en las aplicaciones lógicas y el uso de negocios tooscenarios Hola paquete de integración empresarial"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 47672dc4-1caa-44e5-b8cb-68ec3a76b7dc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 02/27/2017
ms.author: LADocs; mandia
ms.openlocfilehash: f90ae89fef0a4bd17286adbce398e573940bb790
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a><span data-ttu-id="3f004-103">Validar y transformar XML, codificar y descodificar archivos planos y enriquecer características de mensajes en aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="3f004-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span></span>

<span data-ttu-id="3f004-104">Con las aplicaciones lógicas, tiene Hola capacidad tooprocess XML los mensajes que envían y reciben.</span><span class="sxs-lookup"><span data-stu-id="3f004-104">Using logic apps, you have hello ability tooprocess XML messages that you send and receive.</span></span> <span data-ttu-id="3f004-105">Esta característica se incluye con hello paquete de integración empresarial.</span><span class="sxs-lookup"><span data-stu-id="3f004-105">This feature is included with hello Enterprise Integration Pack.</span></span> <span data-ttu-id="3f004-106">Para los usuarios con un fondo de BizTalk Server, Hola paquete de integración empresarial ofrece tootransform de capacidades similares y validar los mensajes, trabajar con archivos sin formato e incluso usar XPath tooenrich o extraer propiedades específicas de un mensaje.</span><span class="sxs-lookup"><span data-stu-id="3f004-106">For those users with a BizTalk Server background, hello Enterprise Integration Pack gives you similar abilities tootransform and validate messages, work with flat files, and even use XPath tooenrich or extract specific properties from a message.</span></span> 

<span data-ttu-id="3f004-107">Para aquellos usuarios que son el nuevo espacio de toothis, estas características expande la forma de procesar los mensajes dentro de su flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3f004-107">For those users who are new toothis space, these features expand how you process messages within your workflow.</span></span> <span data-ttu-id="3f004-108">Por ejemplo, si se encuentra en un escenario de negocio a negocio y trabajar con esquemas XML específicos, puede utilizar tooenhance de paquete de integración empresarial Hola cómo su empresa procesa estos mensajes.</span><span class="sxs-lookup"><span data-stu-id="3f004-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use hello Enterprise Integration Pack tooenhance how your company processes these messages.</span></span> 

<span data-ttu-id="3f004-109">Hello paquete de integración empresarial incluye:</span><span class="sxs-lookup"><span data-stu-id="3f004-109">hello Enterprise Integration Pack includes:</span></span> 

* <span data-ttu-id="3f004-110">[Validación XML](logic-apps-enterprise-integration-xml-validation.md "Información sobre la validación de mensajes XML"): Permite validar un mensaje XML entrante o saliente en un esquema concreto.</span><span class="sxs-lookup"><span data-stu-id="3f004-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span></span>
* <span data-ttu-id="3f004-111">[Transformación XML](../logic-apps/logic-apps-enterprise-integration-transform.md "más información acerca de las transformaciones de mensajes XML y mapas") : convertir o personalizar un mensaje XML en función de sus requisitos, o de Hola de un asociado.</span><span class="sxs-lookup"><span data-stu-id="3f004-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or hello requirements of a partner.</span></span>
* <span data-ttu-id="3f004-112">[Codificación y descodificación de archivos sin formato](logic-apps-enterprise-integration-flatfile.md "Información sobre la codificación y descodificación de archivos sin formato"): permiten codificar o descodificar un archivo sin formato.</span><span class="sxs-lookup"><span data-stu-id="3f004-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span></span> <span data-ttu-id="3f004-113">Por ejemplo, SAP acepta y envía archivos IDOC en formato de archivo plano.</span><span class="sxs-lookup"><span data-stu-id="3f004-113">For example, SAP accepts and sends IDOC files in flat file format.</span></span> <span data-ttu-id="3f004-114">Muchas plataformas de integración crean mensajes XML, incluida Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="3f004-114">Many integration platforms create XML messages, including Logic Apps.</span></span> <span data-ttu-id="3f004-115">Por lo tanto, puede crear una aplicación de lógica que utiliza Hola archivos planos codificador demasiado "convierta" tooflat de archivos XML.</span><span class="sxs-lookup"><span data-stu-id="3f004-115">So, you can create a logic app that uses hello flat file encoder too"convert" XML files tooflat files.</span></span> 
* <span data-ttu-id="3f004-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) : enriquecer un mensaje y extraer propiedades específicas de mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="3f004-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from hello message.</span></span> <span data-ttu-id="3f004-117">Puede usar Hola extrae propiedades tooroute Hola mensaje tooa destino o un extremo intermediario.</span><span class="sxs-lookup"><span data-stu-id="3f004-117">You can then use hello extracted properties tooroute hello message tooa destination, or an intermediary endpoint.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="3f004-118">Prueba</span><span class="sxs-lookup"><span data-stu-id="3f004-118">Try it out</span></span>
<span data-ttu-id="3f004-119">[Implementar una aplicación totalmente operativa lógica ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (ejemplo de GitHub) mediante las características XML de hello en las aplicaciones lógicas de Azure.</span><span class="sxs-lookup"><span data-stu-id="3f004-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using hello XML features in Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="3f004-120">Más información</span><span class="sxs-lookup"><span data-stu-id="3f004-120">Learn more</span></span>
[<span data-ttu-id="3f004-121">Obtener más información sobre Hola paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="3f004-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial")
