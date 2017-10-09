---
title: aaaAdministration y lista de tareas de desarrollo de servicios de BizTalk | Documentos de Microsoft
description: "Ayuda de planeación y de trabajo para implementar Servicios de BizTalk de Azure."
services: biztalk-services
documentationcenter: 
author: msftman
manager: erikre
editor: 
ms.assetid: 0ab70b5b-1a88-4ba5-b329-ec51b785010e
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2016
ms.author: deonhe
ms.openlocfilehash: 544c6b23fcbc2267598b713dbe1626699099d181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="administration-and-development-task-list-in-biztalk-services"></a>Lista de tareas de administración y desarrollo de los Servicios de BizTalk

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="getting-started"></a>Introducción
Cuando se trabaja con los servicios de BizTalk de Microsoft Azure, hay varios locales y tooconsider de componentes en la nube. tooget iniciado, considere la posibilidad de hello siguiendo el flujo del proceso:  

| Paso | Quién es el responsable | Tarea | Vínculos relacionados |
| --- | --- | --- | --- |
| 1. |Administrador |Crear suscripción de Microsoft Azure con una cuenta de Microsoft o una cuenta profesional de hello |[Portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=213885) |
| 2. |Administrador |Cree o aprovisione un servicio de BizTalk. |[Crear un Servicio de BizTalk mediante el portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=302280) |
| 3. |Administrador |Registrarse a usted o registrar la implementación de los Servicios de BizTalk de su empresa |[Registrar y actualizar una implementación de servicio de BizTalk en hello Portal de servicios de BizTalk](https://msdn.microsoft.com/library/azure/hh689837.aspx) |
| 4. |Administrador |Se aplica si la aplicación hello utiliza el sistema de línea de negocio (LOB) de servicio de adaptador de BizTalk tooconnect tooan local o una cola o tema de destino.  Crear Hola Namespace de Bus de servicio de Azure. Asigne a este espacio de nombres, nombre de emisor de Bus de servicio y developer de toohello de valores de clave del emisor de Bus de servicio. |[Crear o modificar un espacio de nombres del servicio de Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md) y [Obtener valores del nombre de emisor y de la clave de emisor](biztalk-issuer-name-issuer-key.md) |
| 5. |Developer |Instalar SDK de Hola y crear Hola proyecto de BizTalk Service en Visual Studio. |[Instalar SDK de Azure BizTalk Services](https://msdn.microsoft.com/library/azure/hh689760.aspx) y [Crear puntos de conexión de mensajería enriquecida en Azure](https://msdn.microsoft.com/library/azure/hh689766.aspx) |
| 6. |Developer |Implementar la tooyour del proyecto de BizTalk Service que BizTalk Service hospedado en Azure. |[Implementar y actualizar Hola proyecto de servicios de BizTalk](https://msdn.microsoft.com/library/azure/hh689881.aspx) |
| 7. |Administrador |Se aplica si está usando EDI.  Puede agregar a asociados y crear acuerdos en hello Portal de servicios de BizTalk de Microsoft Azure. Cuando se crea un acuerdo, puede agregar el puente de Hola o transformaciones creadas por la configuración de un acuerdo para desarrolladores hello toohello. |[Configuración de EDI, AS2 y EDIFACT en el Portal de servicios de BizTalk](https://msdn.microsoft.com/library/azure/hh689853.aspx) |
| 8. |Administrador |Con hello Portal de Azure clásico, supervisar el estado de saludo de su BizTalk Service, incluidas las métricas de rendimiento. |[Servicios de BizTalk: pestañas Panel, Monitor y Escala](http://go.microsoft.com/fwlink/p/?LinkID=302281) |
| 9. |Administrador |Con hello Portal de servicios de BizTalk de Microsoft Azure, administrar los artefactos de Hola que usan los servicios de BizTalk y seguimiento de mensajes conforme son procesados por los archivos de puente de Hola. |[Uso de hello Portal de servicios de BizTalk](https://msdn.microsoft.com/library/azure/dn874043.aspx) |
| 10. |Administrador |Crear un tooback de plan de copia de seguridad de hello BizTalk Service. |[Continuidad empresarial y recuperación ante desastres en Servicios de BizTalk](https://msdn.microsoft.com/library/azure/dn509557.aspx) |

## <a name="next-steps"></a>Pasos siguientes
[Tutoriales y ejemplos](https://msdn.microsoft.com/library/azure/hh689895.aspx)

[Crear proyecto de hello en Visual Studio](https://msdn.microsoft.com/library/azure/hh689811.aspx)

[Instalación del SDK de Servicios de BizTalk de Azure](https://msdn.microsoft.com/library/azure/hh689760.aspx)

## <a name="concepts"></a>Conceptos
[Crear proyecto de hello en Visual Studio](https://msdn.microsoft.com/library/azure/hh689811.aspx)  
[EDI, AS2 y EDIFACT (negocio tooBusiness) de mensajería](https://msdn.microsoft.com/library/azure/hh689898.aspx)  

## <a name="other-resources"></a>Otros recursos
[Agregar puntos de conexión de mensajería de origen, destino y puente](https://msdn.microsoft.com/library/azure/hh689877.aspx)  
[Obtener información y crear transformaciones y mapas de mensajes](https://msdn.microsoft.com/library/azure/hh689905.aspx)  
[Uso de hello servicio de adaptador de BizTalk (BAS)](https://msdn.microsoft.com/library/azure/hh689889.aspx)  
[Servicios de BizTalk de Azure](http://go.microsoft.com/fwlink/p/?LinkID=303664)

