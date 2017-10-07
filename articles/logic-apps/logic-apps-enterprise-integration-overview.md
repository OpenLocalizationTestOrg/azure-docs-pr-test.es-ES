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
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a>Información general: Escenarios B2B y comunicación con hello paquete de integración empresarial

Para los flujos de trabajo de negocio a negocio (B2B) y la comunicación sin problemas con aplicaciones de Azure lógica, puede habilitar escenarios de integración de enterprise con la solución basada en la nube de Microsoft, Hola paquete de integración empresarial. Las organizaciones pueden intercambiar mensajes electrónicamente, incluso si usan formatos y protocolos diferentes. módulo de Hello transforma diferentes formatos en un formato que pueden interpretar y procesar los sistemas de organizaciones. Las organizaciones pueden intercambiar mensajes mediante protocolos estándar del sector, entre ellos [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md) y [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md). También puede proteger los mensajes con cifrado y firmas digitales.

Si está familiarizado con BizTalk Server o servicios de BizTalk de Microsoft Azure, las características de integración de Enterprise Hola son toouse fácil porque la mayoría de conceptos son similares. Una diferencia importante es que la integración de Enterprise utiliza almacenamiento de Hola de toosimplify de cuentas de integración y la administración de artefactos que se usan en las comunicaciones de B2B. 

Hola su arquitectura, que paquete de integración empresarial se basa en "cuentas de integración". Estas cuentas son contenedores basados en la nube que almacenan todos sus artefactos, como esquemas, asociados, certificados, mapas y contratos. Puede usar estos toodesign artefactos, implementar y mantener sus aplicaciones B2B y también toobuild B2B flujos de trabajo para las aplicaciones lógicas. Pero para poder usar estos artefactos, primero debe vincular la aplicación de la lógica de la cuenta tooyour integración. Después de eso, la aplicación lógica podrá acceder a los artefactos de la cuenta de integración.

## <a name="why-should-you-use-enterprise-integration"></a>¿Por qué se debe utilizar Enterprise Integration Pack?

* Gracias a Enterprise Integration, podrá almacenar todos los artefactos en un solo lugar: la cuenta de integración.
* Puede crear flujos de trabajo de B2B e integrarse con aplicaciones de terceros software como servicio (SaaS), las aplicaciones locales y aplicaciones personalizadas mediante el uso de motor de hello Azure Logic Apps y todos sus conectores.
* Puede crear código personalizado para las aplicaciones lógicas con Azure Functions.

## <a name="how-tooget-started-with-enterprise-integration"></a>¿Cómo tooget empieza con la integración de enterprise?

Puede crear y administrar aplicaciones de B2B con hello paquete de integración empresarial a través de hello diseñador la lógica de aplicación Hola **portal de Azure**. También puede administrar las aplicaciones lógicas con [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Temas de Logic Apps y PowerShell").

Estos son los pasos de alto nivel de Hola que debe seguir para poder crear aplicaciones en hello portal de Azure:

![Imagen de información general](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a>¿Cuáles son algunos escenarios comunes?

Enterprise Integration Pack admite estos estándares del sector:

* EDI: intercambio electrónico de datos
* EAI: integración de aplicaciones empresariales

## <a name="heres-what-you-need-tooget-started"></a>Esto es lo necesita tooget iniciado

* Tener una suscripción de Azure con una cuenta de integración
* Visual Studio 2015 toocreate asignaciones y esquemas
* [Herramientas de integración de empresas de Aplicaciones Lógicas de Microsoft Azure para la versión 2.0 de Visual Studio 2015](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a>Pruébelo ya

[Implementación de un envío de AS2 ejemplo totalmente operativo y aplicación lógica de recepción](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) que usa características de hello B2B para las aplicaciones lógicas de Azure.

## <a name="learn-more"></a>Más información
* [Contratos](../logic-apps/logic-apps-enterprise-integration-agreements.md "Información sobre los contratos de Enterprise Integration")
* [Escenarios de negocio (B2B) tooBusiness](../logic-apps/logic-apps-enterprise-integration-b2b.md "más información cómo toocreate las aplicaciones lógicas con características de B2B")  
* [Certificados](logic-apps-enterprise-integration-certificates.md "Información sobre los certificados de Enterprise Integration")
* [Planos de codificación y descodificación de archivo](logic-apps-enterprise-integration-flatfile.md "más información cómo tooencode y descodificar el contenido del archivo sin formato")  
* [Cuentas de Integration](../logic-apps/logic-apps-enterprise-integration-accounts.md "Información acerca de las cuentas de integración")
* [Asignaciones](../logic-apps/logic-apps-enterprise-integration-maps.md "Información sobre las asignaciones de Enterprise Integration")
* [Asociados](logic-apps-enterprise-integration-partners.md "Información acerca de los asociados de Enterprise Integration")
* [Esquemas](logic-apps-enterprise-integration-schemas.md "Información sobre los esquemas de Enterprise Integration")
* [Validación del mensaje XML](logic-apps-enterprise-integration-xml.md "Obtenga información acerca de cómo toovalidate XML mensajes a las aplicaciones lógicas")
* [Transformación de XML](logic-apps-enterprise-integration-transform.md "Información sobre las asignaciones de Enterprise Integration")
* [Conectores de integración de empresa](../connectors/apis-list.md "Información sobre los conectores de Enterprise Integration Pack")
* [Metadatos de la cuenta de integración](../logic-apps/logic-apps-enterprise-integration-metadata.md "Obtenga más información acerca de los metadatos de la cuenta de integración")
* [Supervisión de mensajes B2B](logic-apps-monitor-b2b-message.md "Más información acerca de la supervisión de mensajes B2B")
* [Seguimiento de mensajes B2B en el Portal de OMS](logic-apps-track-b2b-messages-omsportal.md "Más información acerca del seguimiento de mensajes B2B en el Portal de OMS")

