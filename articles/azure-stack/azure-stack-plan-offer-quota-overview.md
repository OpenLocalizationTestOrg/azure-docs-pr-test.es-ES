---
title: "Introducción al plan, oferta, cuota y suscripción pila aaaAzure | Documentos de Microsoft"
description: Como un operador en la nube, deseo toounderstand que planes de pila de Azure, ofertas, cuotas y las suscripciones.
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 3dc92e5c-c004-49db-9a94-783f1f798b98
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/22/2017
ms.author: erikje
ms.openlocfilehash: 67f5bcfda221473b1f397668e2a3186b80d6f43c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="plan-offer-quota-and-subscription-overview"></a>Introducción a los planes, ofertas, cuotas y suscripciones

Azure Stack le permite proporcionar una amplia variedad de servicios, como máquinas virtuales, bases de datos SQL Server, SharePoint, Exchange e incluso [elementos de Azure Marketplace](azure-stack-marketplace-azure-items.md). Como operador de nube, debe configurar y entregar esos servicios en Azure Stack por medio de planes, ofertas y cuotas.

Las ofertas contienen uno o varios planes y cada plan incluye uno o varios servicios. Al crear planes y combinarlos en diferentes ofertas, puede controlar:
- los servicio y los recursos a los que pueden acceder los usuarios
- cantidad de Hola de esos recursos que los usuarios podrán consumir
- Qué regiones tienen acceso a recursos de toohello

Al ofrecer un servicio, seguirá estos pasos de alto nivel:

1. Agregar un servicio que desea que los usuarios de tooyour toodeliver.
2. Crear un plan que contenga uno o varios servicios. Al crear un plan, se seleccione o cree cuotas que definen los límites de recursos de Hola de cada servicio en el plan de Hola.
3. Crear una oferta que contenga uno o varios planes (incluidos los planes base y planes complementarios opcionales).

Después de haber creado la oferta de hello, los usuarios pueden suscribirse proporciona los recursos y servicios de Hola de tooaccess de tooit. Los usuarios pueden suscribirse tooas ofrece muchos como deseen. Hello siguiente diagrama muestra un ejemplo sencillo de un usuario que se ha suscrito tootwo ofertas. Cada oferta tiene un plan o dos, y cada plan le da acceso tooservices.

![](media/azure-stack-key-features/image4.png)

## <a name="plans"></a>Planes

Los planes son agrupaciones de uno o varios servicios. Como un operador en la nube, le [crear planes de](azure-stack-create-plan.md) toooffer tooyour usuarios. A su vez, los usuarios suscriben tooyour ofertas toouse Hola planes y servicios que se incluyen. Al crear los planes, realizar tooset seguro de las cuotas, definir los planes de base y considere incluir planes de complemento opcional.

### <a name="quotas"></a>Cuotas

toohelp administrar la capacidad de la nube, seleccione o cree una cuota para cada servicio en un plan. Las cuotas de definen los límites de recursos superior de Hola que puede aprovisionar o utilizar una suscripción de usuario. Por ejemplo, una cuota puede permitir un toocreate usuario las máquinas virtuales de toofive. Las cuotas pueden limitar una variedad de recursos, como máquinas virtuales, RAM y límites de CPU.

Las cuotas se pueden configurar por región. Por ejemplo, un plan que contiene servicios de proceso de la Región A podría tener una cuota de dos máquinas virtuales, 4 GB de RAM y 10 núcleos de CPU. En el Kit de desarrollo de la pila de Azure, solo una región de hello (denominado *local*) está disponible.

### <a name="base-plan"></a>Plan base

Al crear una oferta, Administrador de servicios de hello puede incluir un plan de base. Estos planes base se incluyen de forma predeterminada cuando un usuario suscribe toothat oferta. Cuando un usuario se suscribe, tienen proveedores de recursos de acceso tooall Hola especificados en esos planes base (con las cuotas correspondientes de hello).

### <a name="add-on-plans"></a>Planes complementarios

También puede incluir planes complementarios opcionales en una oferta. Planes de complemento no se incluyen de forma predeterminada en la suscripción de Hola. Planes de complemento son planes adicionales (con cuotas) disponibles en una oferta que un suscriptor puede agregar suscripciones de tootheir. Por ejemplo, puede ofrecer un plan base con recursos limitados para una versión de prueba y un plan de complemento con toocustomers recursos más importantes que decidir tooadopt Hola servicio.

## <a name="offers"></a>Ofertas

Ofertas son grupos de uno o varios planes que cree para que los usuarios pueden suscribirse toothem. Por ejemplo, la Oferta Alfa puede incluir el Plan A (que contiene un conjunto de servicios Compute Services) y el Plan B (que contiene un conjunto de servicios de almacenamiento y Network Services). 

Cuando se [crear una oferta](azure-stack-create-offer.md), debe incluir al menos un plan de base, pero también puede crear planes de complemento que los usuarios pueden agregar suscripción tootheir.


## <a name="subscriptions"></a>Suscripciones

Una suscripción es la forma en que los inquilinos acceden a las ofertas. Si es un operador en la nube en un proveedor de servicios, los usuarios (inquilinos) compran sus servicios suscribiéndose tooyour ofertas. Si es un operador en la nube en una organización, los usuarios (empleados) pueden suscribirse a servicios toohello que ofrecen sin pagar. Cada combinación de un usuario con una oferta es una suscripción única. Por lo tanto, un usuario puede tener suscripciones toomultiple ofertas, pero cada suscripción aplica tooonly una oferta. Planes y ofertas, cuotas se aplican solo tooeach de suscripción único, no se puede compartir entre suscripciones. Cada recurso que crea un usuario está asociado a una suscripción.


### <a name="default-provider-subscription"></a>Suscripción de proveedor predeterminada

Hola suscripción de proveedor predeterminado se crea automáticamente cuando se implementa Hola Kit de desarrollo de pila de Azure. Esta suscripción puede ser usado toomanage pila de Azure, implementar más proveedores de recursos y crear planes y ofrece a los usuarios. Para la seguridad y licencias de motivos, no debe ser aplicaciones y cargas de trabajo de cliente toorun utilizado. 

## <a name="next-steps"></a>Pasos siguientes

[Creación de un plan](azure-stack-create-plan.md)
