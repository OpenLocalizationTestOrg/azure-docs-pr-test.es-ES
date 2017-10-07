---
title: "conceptos de la cuadrícula de eventos de aaaAzure"
description: Describe Azure Event Grid y sus conceptos. Define varios componentes clave de Event Grid.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/10/2017
ms.author: babanisa
ms.openlocfilehash: bb86381330fd2d6d2769167ec1953f0d5c28af85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="concepts-in-azure-event-grid"></a>Concepts de Azure Event Grid

Hola conceptos principales en la cuadrícula de eventos de Azure son:

## <a name="events"></a>Eventos

Un evento es la cantidad más pequeña de Hola de información que describe totalmente algo que ha producido en el sistema de Hola.  Cada evento tiene información comunes como: origen de evento de hello, eventos de tiempo de hello tuvo lugar y el identificador único.  Todos los eventos también tengan la información específica que es solo toohello relevantes de evento específico. Por ejemplo, un evento sobre un nuevo archivo se crea en el almacenamiento de Azure contiene detalles sobre el archivo hello, como el valor de lastTimeModified Hola. O bien, un evento sobre un reinicio de máquina virtual contiene el nombre de Hola de máquina virtual de hello y el motivo de Hola de reinicio.

## <a name="event-sourcespublishers"></a>Orígenes/publicadores de eventos

Un origen de eventos es donde ocurre el evento Hola. Por ejemplo, el almacenamiento de Azure es origen de eventos de Hola de blob creado eventos. Tejido de Azure VM es origen de eventos de Hola para eventos de máquina virtual. Orígenes de eventos son responsables de la publicación de eventos tooEvent cuadrícula.

## <a name="topics"></a>Temas

Los publicadores clasifican los eventos en temas. tema de Hello incluye un punto de conexión donde publisher Hola envíe los eventos. toorespond toocertain tipos de eventos, los suscriptores decidir qué toosubscribe temas a. Temas también proporcionan un esquema de eventos para que los suscriptores puedan detectar cómo tooconsume Hola eventos adecuadamente.

Los temas del sistema son temas integrados que ofrecen los servicios de Azure. Los temas personalizados son temas de terceros y de aplicación.

## <a name="event-subscriptions"></a>Suscripciones a eventos

Una suscripción indica a Event Grid los eventos sobre un tema que a un suscriptor le interesa recibir.  Una suscripción también contiene información sobre cómo se deben entregar los eventos toohello suscriptor.

## <a name="event-handlers"></a>Controladores de eventos

Desde una perspectiva de la cuadrícula de eventos, un controlador de eventos es lugar de Hola dónde se envían eventos de Hola. controlador de Hello usa algunos eventos de Hola de tooprocess acción adicional.  Event Grid admite varios tipos de suscriptor. Según el tipo de Hola de suscriptor, cuadrícula de eventos sigue entrega de hello tooguarantee de diferentes mecanismos de evento Hola.  Para los controladores de eventos de webhook HTTP, evento de Hola se vuelve a intentar hasta que el controlador de hello devuelve un código de estado `200 – OK`. Para cola de almacenamiento de Azure, se reintentan eventos Hola hasta que inserción de mensaje de Hola toosuccessfully capaz de proceso en cola Hola Hola servicio cola.

## <a name="filters"></a>Filtros

Cuando se suscriba tooa tema, puede filtrar los eventos de Hola que se envían toohello extremo. Puede filtrar por tipo de evento o por patrón de asunto. Para más información, vea [Esquema de suscripción de Event Grid](subscription-creation-schema.md).

## <a name="security"></a>Seguridad

Evento proporciona seguridad para la suscripción tootopics así como temas de publicación. Cuando se suscriba, debe tener los permisos adecuados en el recurso de Hola o tema. Al publicar, debe tener un token de SAS o autenticación de claves tema Hola. Para más información, vea [Event Grid security and authentication](security-authentication.md) (Seguridad y autenticación de Event Grid).

## <a name="failed-delivery"></a>Error de entrega

Cuando la cuadrícula de eventos no se puede confirmar que se ha recibido un evento de punto de conexión del suscriptor de hello, redelivers evento Hola. Para más información, vea [Entrega y reintento de entrega de mensajes de Event Grid](delivery-and-retry.md).

## <a name="next-steps"></a>Pasos siguientes

* Para una cuadrícula de introducción tooEvent, consulte [acerca de la cuadrícula de eventos](overview.md).
* tooquickly Introducción al uso de la cuadrícula de eventos, vea [ruta y crear eventos personalizados con la cuadrícula de eventos de Azure](custom-event-quickstart.md).
