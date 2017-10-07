---
title: "aaaEnterprise integración para B2B - Azure Logic Apps | Documentos de Microsoft"
description: "Crear flujos de trabajo de B2B y admite escenarios de integración empresarial para las aplicaciones lógicas con hello paquete de integración empresarial"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: dd517c4d-1701-4247-b83c-183c4d8d8aae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8dc866533110b1d07f51cf446056d2ca5ce869ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a><span data-ttu-id="11159-103">Información general: Escenarios B2B y comunicación con hello paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="11159-103">Overview: B2B scenarios and communication with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="11159-104">Para los flujos de trabajo de negocio a negocio (B2B) y la comunicación sin problemas con aplicaciones de Azure lógica, puede habilitar escenarios de integración de enterprise con la solución basada en la nube de Microsoft, Hola paquete de integración empresarial.</span><span class="sxs-lookup"><span data-stu-id="11159-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, hello Enterprise Integration Pack.</span></span> <span data-ttu-id="11159-105">Las organizaciones pueden intercambiar mensajes electrónicamente, incluso si usan formatos y protocolos diferentes.</span><span class="sxs-lookup"><span data-stu-id="11159-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="11159-106">módulo de Hello transforma diferentes formatos en un formato que pueden interpretar y procesar los sistemas de organizaciones.</span><span class="sxs-lookup"><span data-stu-id="11159-106">hello pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="11159-107">Las organizaciones pueden intercambiar mensajes mediante protocolos estándar del sector, entre ellos [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md) y [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="11159-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="11159-108">También puede proteger los mensajes con cifrado y firmas digitales.</span><span class="sxs-lookup"><span data-stu-id="11159-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="11159-109">Si está familiarizado con BizTalk Server o servicios de BizTalk de Microsoft Azure, las características de integración de Enterprise Hola son toouse fácil porque la mayoría de conceptos son similares.</span><span class="sxs-lookup"><span data-stu-id="11159-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, hello Enterprise Integration features are easy toouse because most concepts are similar.</span></span> <span data-ttu-id="11159-110">Una diferencia importante es que la integración de Enterprise utiliza almacenamiento de Hola de toosimplify de cuentas de integración y la administración de artefactos que se usan en las comunicaciones de B2B.</span><span class="sxs-lookup"><span data-stu-id="11159-110">One major difference is that Enterprise Integration uses integration accounts toosimplify hello storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="11159-111">Hola su arquitectura, que paquete de integración empresarial se basa en "cuentas de integración".</span><span class="sxs-lookup"><span data-stu-id="11159-111">Architecturally, hello Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="11159-112">Estas cuentas son contenedores basados en la nube que almacenan todos sus artefactos, como esquemas, asociados, certificados, mapas y contratos.</span><span class="sxs-lookup"><span data-stu-id="11159-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="11159-113">Puede usar estos toodesign artefactos, implementar y mantener sus aplicaciones B2B y también toobuild B2B flujos de trabajo para las aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="11159-113">You can use these artifacts toodesign, deploy, and maintain your B2B apps and also toobuild B2B workflows for logic apps.</span></span> <span data-ttu-id="11159-114">Pero para poder usar estos artefactos, primero debe vincular la aplicación de la lógica de la cuenta tooyour integración.</span><span class="sxs-lookup"><span data-stu-id="11159-114">But before you can use these artifacts, you must first link your integration account tooyour logic app.</span></span> <span data-ttu-id="11159-115">Después de eso, la aplicación lógica podrá acceder a los artefactos de la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="11159-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="11159-116">¿Por qué se debe utilizar Enterprise Integration Pack?</span><span class="sxs-lookup"><span data-stu-id="11159-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="11159-117">Gracias a Enterprise Integration, podrá almacenar todos los artefactos en un solo lugar: la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="11159-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="11159-118">Puede crear flujos de trabajo de B2B e integrarse con aplicaciones de terceros software como servicio (SaaS), las aplicaciones locales y aplicaciones personalizadas mediante el uso de motor de hello Azure Logic Apps y todos sus conectores.</span><span class="sxs-lookup"><span data-stu-id="11159-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using hello Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="11159-119">Puede crear código personalizado para las aplicaciones lógicas con Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="11159-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-tooget-started-with-enterprise-integration"></a><span data-ttu-id="11159-120">¿Cómo tooget empieza con la integración de enterprise?</span><span class="sxs-lookup"><span data-stu-id="11159-120">How tooget started with enterprise integration?</span></span>

<span data-ttu-id="11159-121">Puede crear y administrar aplicaciones de B2B con hello paquete de integración empresarial a través de hello diseñador la lógica de aplicación Hola **portal de Azure**.</span><span class="sxs-lookup"><span data-stu-id="11159-121">You can build and manage B2B apps with hello Enterprise Integration Pack through hello Logic App Designer in hello **Azure portal**.</span></span> <span data-ttu-id="11159-122">También puede administrar las aplicaciones lógicas con [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Temas de Logic Apps y PowerShell").</span><span class="sxs-lookup"><span data-stu-id="11159-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span></span>

<span data-ttu-id="11159-123">Estos son los pasos de alto nivel de Hola que debe seguir para poder crear aplicaciones en hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="11159-123">Here are hello high-level steps you must take before you can create apps in hello Azure portal:</span></span>

![Imagen de información general](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="11159-125">¿Cuáles son algunos escenarios comunes?</span><span class="sxs-lookup"><span data-stu-id="11159-125">What are some common scenarios?</span></span>

<span data-ttu-id="11159-126">Enterprise Integration Pack admite estos estándares del sector:</span><span class="sxs-lookup"><span data-stu-id="11159-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="11159-127">EDI: intercambio electrónico de datos</span><span class="sxs-lookup"><span data-stu-id="11159-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="11159-128">EAI: integración de aplicaciones empresariales</span><span class="sxs-lookup"><span data-stu-id="11159-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-tooget-started"></a><span data-ttu-id="11159-129">Esto es lo necesita tooget iniciado</span><span class="sxs-lookup"><span data-stu-id="11159-129">Here's what you need tooget started</span></span>

* <span data-ttu-id="11159-130">Tener una suscripción de Azure con una cuenta de integración</span><span class="sxs-lookup"><span data-stu-id="11159-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="11159-131">Visual Studio 2015 toocreate asignaciones y esquemas</span><span class="sxs-lookup"><span data-stu-id="11159-131">Visual Studio 2015 toocreate maps and schemas</span></span>
* [<span data-ttu-id="11159-132">Herramientas de integración de empresas de Aplicaciones Lógicas de Microsoft Azure para la versión 2.0 de Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="11159-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="11159-133">Pruébelo ya</span><span class="sxs-lookup"><span data-stu-id="11159-133">Try it now</span></span>

<span data-ttu-id="11159-134">[Implementación de un envío de AS2 ejemplo totalmente operativo y aplicación lógica de recepción](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) que usa características de hello B2B para las aplicaciones lógicas de Azure.</span><span class="sxs-lookup"><span data-stu-id="11159-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses hello B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="11159-135">Más información</span><span class="sxs-lookup"><span data-stu-id="11159-135">Learn more</span></span>
* [<span data-ttu-id="11159-136">Contratos</span><span class="sxs-lookup"><span data-stu-id="11159-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Información sobre los contratos de Enterprise Integration")
* [<span data-ttu-id="11159-137">Escenarios de negocio (B2B) tooBusiness</span><span class="sxs-lookup"><span data-stu-id="11159-137">Business tooBusiness (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "más información cómo toocreate las aplicaciones lógicas con características de B2B")  
* [<span data-ttu-id="11159-138">Certificados</span><span class="sxs-lookup"><span data-stu-id="11159-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "Información sobre los certificados de Enterprise Integration")
* [<span data-ttu-id="11159-139">Planos de codificación y descodificación de archivo</span><span class="sxs-lookup"><span data-stu-id="11159-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "más información cómo tooencode y descodificar el contenido del archivo sin formato")  
* [<span data-ttu-id="11159-140">Cuentas de Integration</span><span class="sxs-lookup"><span data-stu-id="11159-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "Información acerca de las cuentas de integración")
* [<span data-ttu-id="11159-141">Asignaciones</span><span class="sxs-lookup"><span data-stu-id="11159-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Información sobre las asignaciones de Enterprise Integration")
* [<span data-ttu-id="11159-142">Asociados</span><span class="sxs-lookup"><span data-stu-id="11159-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "Información acerca de los asociados de Enterprise Integration")
* [<span data-ttu-id="11159-143">Esquemas</span><span class="sxs-lookup"><span data-stu-id="11159-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "Información sobre los esquemas de Enterprise Integration")
* [<span data-ttu-id="11159-144">Validación del mensaje XML</span><span class="sxs-lookup"><span data-stu-id="11159-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "Obtenga información acerca de cómo toovalidate XML mensajes a las aplicaciones lógicas")
* [<span data-ttu-id="11159-145">Transformación de XML</span><span class="sxs-lookup"><span data-stu-id="11159-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "Información sobre las asignaciones de Enterprise Integration")
* [<span data-ttu-id="11159-146">Conectores de integración de empresa</span><span class="sxs-lookup"><span data-stu-id="11159-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "Información sobre los conectores de Enterprise Integration Pack")
* [<span data-ttu-id="11159-147">Metadatos de la cuenta de integración</span><span class="sxs-lookup"><span data-stu-id="11159-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "Obtenga más información acerca de los metadatos de la cuenta de integración")
* [<span data-ttu-id="11159-148">Supervisión de mensajes B2B</span><span class="sxs-lookup"><span data-stu-id="11159-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "Más información acerca de la supervisión de mensajes B2B")
* [<span data-ttu-id="11159-149">Seguimiento de mensajes B2B en el Portal de OMS</span><span class="sxs-lookup"><span data-stu-id="11159-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "Más información acerca del seguimiento de mensajes B2B en el Portal de OMS")
