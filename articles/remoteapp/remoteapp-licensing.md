---
title: licencias de RemoteApp aaaAzure | Documentos de Microsoft
description: "Obtenga información sobre cómo funcionan las licencias en RemoteApp de Azure."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: ff8ebd20-61a1-4f10-87a6-234a170534c9
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dfa808a65ea6b1a78bf74f3daddb9a84e186eebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-licensing-work-in-azure-remoteapp"></a>¿Cómo funciona la concesión de licencias de RemoteApp de Azure?
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Por lo que ha configurado el servicio de Azure RemoteApp, creado las plantillas y aplicaciones toopublish listo tooyour usuarios. Pero sigue siendo una toofigure lo último out: Administrador de licencias. ¿Simplemente cómo funciona la licencia de RemoteApp y para las aplicaciones de hello que compartir a través de RemoteApp?

RemoteApp no requiere licencias de Windows ni licencias de acceso de cliente (CAL) de Escritorio remoto. La suscripción se encarga de hello lado RemoteApp propio. (Consulte detalles de Hola de hello [planes de precios](https://azure.microsoft.com/pricing/details/remoteapp).)

Si utiliza una de las imágenes de Hola que se incluye en su suscripción, puede compartir cualquiera de las aplicaciones de hello instaladas en dicha imagen sin necesidad de una licencia independiente. Por ejemplo, si utiliza la colección toobuild de imagen de plantilla de Windows Server 2012 R2 de hello, puede compartir System Center Endpoint Protection con los usuarios. Hello solo excepciones toothis regla son Office 365 ProPlus, lo que requiere una suscripción independiente, y Office 2013, que no se puede compartir en una colección de producción.

Si desea toouse Hola Office 365 imagen de la plantilla que se incluye con RemoteApp, debe tener un *existente* plan de Office 365 ProPlus. Hola que mismo puede decirse de cualquier aplicación de Office 365 que publica mediante una plantilla personalizada. Necesitará tooactivate Hola aplicaciones con su propia suscripción. Lo mismo ocurre con las suscripciones de prueba y de pago. Si desea toouse imagen de plantilla de Office 365 Hola durante la prueba de hello, *y ya no tiene ninguna suscripción*, ir a página de toohello Office 365 demasiado[registrarse](https://go.microsoft.com/fwlink/p/?LinkID=403802) para una suscripción de prueba. Consulte [¿Cómo funcionan conjuntamente RemoteApp y Office?](remoteapp-o365.md) para obtener más información.

Si, durante el período de prueba de hello, no desea suscripción de prueba de tooget Office 365, use Hola Office 2013 Professional Plus imagen de la plantilla que se incluye con RemoteApp. Esta imagen de plantilla solo puede usarse durante 30 días y no se puede convertir en una colección de pago.

Para otras aplicaciones, debe toomake Asegúrese de que tiene la aplicación Hola de hello licencia tooshare.

Esto tiene sentido, ¿no? Puede publicar cualquier aplicación que tienen derecho legalmente tooshare. Y deberá toomake que es realmente titulada "tooshare los programas.

Tenga en cuenta que no puede usar un contrato de licencia por volumen ni una licencia CAL en una colección en la nube. Se *puede* usar una aplicación de tooactivate de contrato de licencia por volumen en su colección híbrida (salvo Office). Solo tiene tooinstall en la plantilla de la imagen de hello medios de licencias por volumen. Siga Hola información de licencias de hello aplicación proveedor tooinstall en un entorno de escritorio remoto.

