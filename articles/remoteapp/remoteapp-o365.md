---
title: aaaUsing Office con Azure RemoteApp | Documentos de Microsoft
description: "Obtenga información sobre cómo funcionan juntos Office y Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: f1773baf-8aa1-423c-a2f9-e4679e0463d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d065c1a0a2191c9e2e405264a835cecf791d6ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-office-with-azure-remoteapp"></a>Uso de Office con Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Tiene dos opciones para hospedar aplicaciones de Office en Azure RemoteApp: Office 365 ProPlus u Office 2013 Professional Plus Trial.

**¿Sabía que tenemos un nuevo artículo mejor que pronto reemplazará a este? Extraer del repositorio [cómo toouse la suscripción a Office 365 con Azure RemoteApp](remoteapp-officesubscription.md). Incluye toda la información de hello que necesita para poder usar Office 365 + Azure RemoteApp.**

## <a name="office-365-proplus"></a>Office 365 ProPlus
Puede crear una colección de RemoteApp mediante Office 365 ProPlus imagen de plantilla Hola. Esta opción le permite tooextend su tooRemoteApp de servicio de Office 365. Debe disponer de un plan de suscripción existente y los usuarios deben tener licencia para hello servicio Office 365 ProPlus, tanto de forma independiente o a través de los planes de servicio de hello Office 365.

RemoteApp es compatible con la activación en equipos compartidos de Office 365. Al habilitar la activación del equipo compartido y usar hello [herramienta de implementación de Office](http://www.microsoft.com/download/details.aspx?id=36778) para la instalación, Office 365 ProPlus instala sin que se va a activar. Cuando un usuario inicia sesión en una colección que contiene Office 365, Office comprueba toosee si se ha proporcionado el usuario de Hola para Office 365 ProPlus. Si es así, Office temporalmente activa Office 365 ProPlus - esta activación continúa hasta que signos de los usuarios fuera de servicio de Hola.

toouse Office 365 compartido activación del equipo, deberá toocreate un [plantilla personalizada](remoteapp-create-custom-image.md) y, después de instalar Office 365 ProPlus [estas instrucciones](https://technet.microsoft.com/library/dn782858.aspx).

Puede administrar las licencias de Office 365 de los usuarios en hello [Portal de administración de Office 365](https://portal.office365.com/). Obtenga más información sobre [Planes de servicios de Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).  

## <a name="office-2013-professional-plus-trial"></a>Office 2013 Professional Plus Trial
Durante una prueba de 30 días de RemoteApp, puede utilizar toocreate de imagen de plantilla Hola Office 2013 Professional Plus (prueba) una colección de RemoteApp. Puede asignar usuarios toothis colección prueba mediante sus cuentas de trabajo de Azure Active Directory o cuentas de Microsoft. No se requieren suscripciones adicionales.

Esto es una buena opción tookick hello las cubiertas y hacerse una idea buena de Office en RemoteApp. Sin embargo, esta opción está pensada solo para su evaluación y prueba. Las colecciones de RemoteApp creadas mediante imagen de plantilla de hello Office 2013 Professional Plus (prueba) no pueden ser el modo de transición tooproduction y se deshabilitará al final de hello del período de prueba de Hola.

## <a name="switching-from-trial-tooproduction"></a>Cambio de prueba tooproduction
Cuando se inicia la prueba gratuita de 30 días, una nota en hello RemoteApp sección del portal de hello le indicará cuánto tiempo han dejado de evaluación de hello antes de que necesites tooa tootransition cuenta de pago. Puede activar el modo de tooproduction de cuenta y el conmutador mediante el vínculo de hello en esta nota.

Al activar su cuenta, esto afectará a todas las colecciones de RemoteApp de hello en su cuenta.

* Las colecciones que se ejecutan con Windows Server 2012 R2 de Hola o imágenes de plantilla de Office 365 ProPlus Hola realizará la transición tooproduction sin problemas. Todos los datos de usuario y configuración, incluidas las sesiones en curso, permanecerán intactos.
* Si cargó imágenes de plantilla personalizadas, las colecciones que usen esas imágenes también pasarán sin problemas.
* imagen de plantilla de Hello Office 2013 Professional Plus (prueba) está pensado para evaluación únicamente. Colecciones que se ejecuten con esta imagen de plantilla no pueden ser tooproduction transición. Se pondrán en estado "deshabilitado".

Si no se pasa tooproduction modo vencimiento de saludo de la versión de prueba, se deshabilitará las colecciones de RemoteApp. No se preocupe: la configuración y los datos de los usuarios se guardan para otro 90 días, por lo que todavía se puede activar el modo de tooproduction de servicio y el conmutador sin pérdida de datos.

