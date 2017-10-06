---
title: "aaaPricing & facturación - Azure Logic Apps | Documentos de Microsoft"
description: "Descubra cómo funcionan los precios y la facturación en Azure Logic Apps."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f8f528f5-51c5-4006-b571-54ef74532f32
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.openlocfilehash: fa10cbbf7657afba7fadb7c76817b7a5e4af7b42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-pricing-model"></a>Modelo de precios de Logic Apps
Aplicaciones lógicas de Azure permite tooscale y ejecutar flujos de trabajo de integración en nube Hola.  Siguiente se muestran los detalles en Hola de facturación y planes de precios para Logic Apps.
## <a name="consumption-pricing"></a>Precios de consumo
Las aplicaciones lógicas recién creadas usan un plan de consumo. Con el modelo de precios de hello Logic Apps consumo, solo se paga por lo que usa.  Las aplicaciones lógicas no se limitan cuando se utiliza un plan de consumo.
Se miden todas las acciones que se ejecutan durante la ejecución de una instancia de aplicación lógica.
### <a name="what-are-action-executions"></a>¿Cuáles son las ejecuciones de acción?
Cada paso en una definición de aplicación lógica es una acción, que incluye a los desencadenadores, pasos de flujo de control como ocurre con las condiciones, los ámbitos, bucles for each, hasta que los bucles, llamadas a acciones de toonative tooconnectors y llamadas.
Los desencadenadores son acciones especiales que están diseñada tooinstantiate una nueva instancia de una aplicación lógica cuando se produce un evento determinado.  Hay varios comportamientos diferentes para los desencadenadores, lo que podrían afectar a cómo se mide la aplicación de la lógica de hello.
* **Desencadenador de sondeo** – este desencadenador sondea continuamente un punto de conexión hasta que recibe un mensaje que cumple los criterios de Hola para crear una instancia de una aplicación de lógica.  intervalo de sondeo de Hello puede configurarse en el desencadenador de Hola Hola diseñador la lógica de aplicación.  Cada solicitud de sondeo, incluso si no crea una instancia de una aplicación lógica, cuenta como una ejecución de acción.
* **Desencadenador de Webhook** – este desencadenador esperará a que un cliente toosend una solicitud en un punto de conexión determinado.  Cada solicitud se envía el punto de conexión de toohello webhook se considera una ejecución de acción. Solicitud de Hola y Hola HTTP Webhook desencadenador son ambos desencadenadores de webhook.
* **Desencadenador de periodicidad** – este desencadenador crea una instancia de aplicación lógica de hello basado en intervalo de periodicidad de hello configurado en el desencadenador de Hola.  Por ejemplo, un desencadenador de periodicidad puede ser configurado toorun cada tres días o incluso cada minuto.

Ejecuciones de desencadenadores pueden verse en la hoja de recursos de aplicaciones lógicas de Hola Hola parte del historial de desencadenador.

Todas las acciones que se ejecutaron, tanto si tuvieron éxito como si no, se miden como ejecuciones de acción.  Acciones que se omitieron debido condición tooa no se cumplen o las acciones que no ejecutan porque la aplicación de lógica de hello termina antes de la finalización no se cuentan como ejecuciones de acción.

Las acciones que se ejecuta dentro de los bucles se cuentan por cada iteración del bucle de Hola.  Por ejemplo, una sola acción en un bucle for each recorrer en iteración una lista de 10 elementos se cuentan como número de Hola de elementos de lista de hello (10) multiplicado por número de Hola de acciones en bucle hello (1) además de uno para la iniciación de Hola de bucle de Hola , que, en este ejemplo, sería (10 * 1) + 1 = 11 ejecuciones de acción.
Si Logic Apps está deshabilitada, no puede tener nuevas instancias iniciadas y, por tanto, mientras las aplicaciones lógicas están deshabilitadas, no se cobrarán.  Tenga en cuenta que después de deshabilitar una aplicación de la lógica puede tardar un poco de tiempo para hello instancias tooquiesce antes de que se deshabilita por completo.
### <a name="integration-account-usage"></a>Uso de la cuenta de integración
Incluido en el uso de consumo es un [cuenta integración](logic-apps-enterprise-integration-create-integration-account.md) de exploración, el desarrollo y con fines de prueba permitiéndole hello toouse [B2B/EDI](logic-apps-enterprise-integration-b2b.md) y [deprocesamientodeXML](logic-apps-enterprise-integration-xml.md)características de lógica de aplicaciones sin ningún costo adicional. Son toocreate capaz de un máximo de una cuenta por cada región y almacenar hasta too10 acuerdos y 25 mapas. Los esquemas, certificados y asociados no tienen ningún límite, y puede cargar tantos como necesite.

Además toohello la inclusión de las cuentas de integración con un consumo, también puede crear integración estándar cuentas sin estos límites y con nuestros SLA de aplicaciones estándar de lógica. Para obtener más información, consulte [Precios de Azure](https://azure.microsoft.com/pricing/details/logic-apps).

## <a name="app-service-plans"></a>Planes del Servicio de aplicaciones
Aplicaciones de lógica que creó anteriormente hace referencia a un Plan de servicio de aplicaciones continúa toobehave como antes. Según el plan de hello elegido, están limitados después de que se superen hello prescritas ejecuciones diarias pero le cobrará el medidor de ejecución de acción de Hola.
Los clientes EA que tienen un Plan de servicio de aplicaciones en su suscripción, que no tiene toobe explícitamente asociada Hola lógica de aplicación, obtener Hola incluyen cantidades beneficio.  Por ejemplo, si tiene un Plan de servicio de aplicaciones estándar en su suscripción de EA y una aplicación de lógica de Hola misma suscripción, a continuación, que no se cobra por 10.000 ejecuciones de acción al día (consulte la siguiente tabla). 

Planes del Servicio de aplicaciones y sus ejecuciones de acción diarias permitidas:
|  | Libre, Compartido o Básico | Estándar | Premium |
| --- | --- | --- | --- |
| Ejecuciones de acción por día |200 |10.000 |50.000 |
### <a name="convert-from-app-service-plan-pricing-tooconsumption"></a>Convertir de precios tooConsumption de Plan de servicio de aplicaciones
toochange una aplicación de lógica que tiene un Plan de servicio de aplicación asociados a él tooa modelo de consumo, remove Hola referencia toohello Plan de servicio de aplicaciones en la definición de aplicación lógica de Hola.  Este cambio puede hacerse con un cmdlet de PowerShell de llamada tooa:`Set-AzureRmLogicApp -ResourceGroupName ‘rgname’ -Name ‘wfname’ –UseConsumptionModel -Force`
## <a name="pricing"></a>Precios
Para obtener información sobre precios, vea [Precios de Logic Apps](https://azure.microsoft.com/pricing/details/logic-apps).

## <a name="next-steps"></a>Pasos siguientes
* [Información general de Logic Apps][whatis]
* [Creación de una nueva aplicación lógica mediante la conexión de servicios de SaaS][create]

[pricing]: https://azure.microsoft.com/pricing/details/logic-apps/
[whatis]: logic-apps-what-are-logic-apps.md
[create]: logic-apps-create-a-logic-app.md

