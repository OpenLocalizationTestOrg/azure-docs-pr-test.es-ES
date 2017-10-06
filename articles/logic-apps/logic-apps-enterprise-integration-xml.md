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
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a>Validar y transformar XML, codificar y descodificar archivos planos y enriquecer características de mensajes en aplicaciones lógicas

Con las aplicaciones lógicas, tiene Hola capacidad tooprocess XML los mensajes que envían y reciben. Esta característica se incluye con hello paquete de integración empresarial. Para los usuarios con un fondo de BizTalk Server, Hola paquete de integración empresarial ofrece tootransform de capacidades similares y validar los mensajes, trabajar con archivos sin formato e incluso usar XPath tooenrich o extraer propiedades específicas de un mensaje. 

Para aquellos usuarios que son el nuevo espacio de toothis, estas características expande la forma de procesar los mensajes dentro de su flujo de trabajo. Por ejemplo, si se encuentra en un escenario de negocio a negocio y trabajar con esquemas XML específicos, puede utilizar tooenhance de paquete de integración empresarial Hola cómo su empresa procesa estos mensajes. 

Hello paquete de integración empresarial incluye: 

* [Validación XML](logic-apps-enterprise-integration-xml-validation.md "Información sobre la validación de mensajes XML"): Permite validar un mensaje XML entrante o saliente en un esquema concreto.
* [Transformación XML](../logic-apps/logic-apps-enterprise-integration-transform.md "más información acerca de las transformaciones de mensajes XML y mapas") : convertir o personalizar un mensaje XML en función de sus requisitos, o de Hola de un asociado.
* [Codificación y descodificación de archivos sin formato](logic-apps-enterprise-integration-flatfile.md "Información sobre la codificación y descodificación de archivos sin formato"): permiten codificar o descodificar un archivo sin formato. Por ejemplo, SAP acepta y envía archivos IDOC en formato de archivo plano. Muchas plataformas de integración crean mensajes XML, incluida Logic Apps. Por lo tanto, puede crear una aplicación de lógica que utiliza Hola archivos planos codificador demasiado "convierta" tooflat de archivos XML. 
* [XPath](https://msdn.microsoft.com/library/mt643789.aspx) : enriquecer un mensaje y extraer propiedades específicas de mensaje de bienvenida. Puede usar Hola extrae propiedades tooroute Hola mensaje tooa destino o un extremo intermediario.

## <a name="try-it-out"></a>Prueba
[Implementar una aplicación totalmente operativa lógica ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (ejemplo de GitHub) mediante las características XML de hello en las aplicaciones lógicas de Azure.

## <a name="learn-more"></a>Más información
[Obtener más información sobre Hola paquete de integración empresarial](../logic-apps/logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial")
