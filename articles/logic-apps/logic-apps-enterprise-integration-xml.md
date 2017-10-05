---
title: Trabajo con mensajes XML en los flujos de trabajo - Azure Logic Apps | Microsoft Docs
description: "Procesar, validar, transformar y enriquecer mensajes XML en aplicaciones lógicas y escenarios empresariales mediante Enterprise Integration Pack"
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
ms.openlocfilehash: 3fec4935f5317be4bf8c9e05f1c24a7c05381b1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a><span data-ttu-id="56fa9-103">Validar y transformar XML, codificar y descodificar archivos planos y enriquecer características de mensajes en aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="56fa9-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span></span>

<span data-ttu-id="56fa9-104">Con las aplicaciones lógicas, tiene la capacidad de procesar los mensajes XML que envía y recibe.</span><span class="sxs-lookup"><span data-stu-id="56fa9-104">Using logic apps, you have the ability to process XML messages that you send and receive.</span></span> <span data-ttu-id="56fa9-105">Esta característica se incluye con Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="56fa9-105">This feature is included with the Enterprise Integration Pack.</span></span> <span data-ttu-id="56fa9-106">Para los usuarios con experiencia en BizTalk Server, Enterprise Integration Pack ofrece funcionalidades similares para transformar y validar los mensajes, trabajar con archivos planos e incluso usar XPath para enriquecer o extraer propiedades específicas de un mensaje.</span><span class="sxs-lookup"><span data-stu-id="56fa9-106">For those users with a BizTalk Server background, the Enterprise Integration Pack gives you similar abilities to transform and validate messages, work with flat files, and even use XPath to enrich or extract specific properties from a message.</span></span> 

<span data-ttu-id="56fa9-107">Para aquellos usuarios que no conocen nada de este espacio, estas características expanden la forma de procesar los mensajes dentro del flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="56fa9-107">For those users who are new to this space, these features expand how you process messages within your workflow.</span></span> <span data-ttu-id="56fa9-108">Por ejemplo, si se encuentra en un escenario de negocio a negocio y trabaja con esquemas XML específicos, puede usar Enterprise Integration Pack para mejorar cómo su empresa procesa estos mensajes.</span><span class="sxs-lookup"><span data-stu-id="56fa9-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use the Enterprise Integration Pack to enhance how your company processes these messages.</span></span> 

<span data-ttu-id="56fa9-109">Enterprise Integration Pack incluye:</span><span class="sxs-lookup"><span data-stu-id="56fa9-109">The Enterprise Integration Pack includes:</span></span> 

* <span data-ttu-id="56fa9-110">[Validación XML](logic-apps-enterprise-integration-xml-validation.md "Información sobre la validación de mensajes XML"): Permite validar un mensaje XML entrante o saliente en un esquema concreto.</span><span class="sxs-lookup"><span data-stu-id="56fa9-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span></span>
* <span data-ttu-id="56fa9-111">[Transformación XML](../logic-apps/logic-apps-enterprise-integration-transform.md "Información sobre las asignaciones y transformaciones de mensajes XML"): Permite convertir o personalizar un mensaje XML basándose en sus requisitos o en los de un asociado.</span><span class="sxs-lookup"><span data-stu-id="56fa9-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or the requirements of a partner.</span></span>
* <span data-ttu-id="56fa9-112">[Codificación y descodificación de archivos sin formato](logic-apps-enterprise-integration-flatfile.md "Información sobre la codificación y descodificación de archivos sin formato"): permiten codificar o descodificar un archivo sin formato.</span><span class="sxs-lookup"><span data-stu-id="56fa9-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span></span> <span data-ttu-id="56fa9-113">Por ejemplo, SAP acepta y envía archivos IDOC en formato de archivo plano.</span><span class="sxs-lookup"><span data-stu-id="56fa9-113">For example, SAP accepts and sends IDOC files in flat file format.</span></span> <span data-ttu-id="56fa9-114">Muchas plataformas de integración crean mensajes XML, incluida Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="56fa9-114">Many integration platforms create XML messages, including Logic Apps.</span></span> <span data-ttu-id="56fa9-115">Por lo tanto, puede crear una aplicación lógica que use el codificador de archivo plano para "convertir" archivos XML en archivos planos.</span><span class="sxs-lookup"><span data-stu-id="56fa9-115">So, you can create a logic app that uses the flat file encoder to "convert" XML files to flat files.</span></span> 
* <span data-ttu-id="56fa9-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx): permite enriquecer un mensaje y extraer propiedades específicas de él.</span><span class="sxs-lookup"><span data-stu-id="56fa9-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from the message.</span></span> <span data-ttu-id="56fa9-117">Las propiedades extraídas se pueden utilizar después para redirigir el mensaje a un destino o un punto de conexión intermediario.</span><span class="sxs-lookup"><span data-stu-id="56fa9-117">You can then use the extracted properties to route the message to a destination, or an intermediary endpoint.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="56fa9-118">Prueba</span><span class="sxs-lookup"><span data-stu-id="56fa9-118">Try it out</span></span>
<span data-ttu-id="56fa9-119">[Implemente una aplicación lógica totalmente operativa](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (ejemplo de GitHub) con las características XML de Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="56fa9-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using the XML features in Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="56fa9-120">Más información</span><span class="sxs-lookup"><span data-stu-id="56fa9-120">Learn more</span></span>
[<span data-ttu-id="56fa9-121">Más información sobre Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="56fa9-121">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Información sobre Enterprise Integration Pack")
