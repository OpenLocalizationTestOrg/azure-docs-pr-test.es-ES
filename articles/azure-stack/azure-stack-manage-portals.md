---
title: los portales de administrador y usuario de hello aaaUsing en pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de las diferencias de hello entre portales de administrador y usuario de hello en la pila de Azure."
services: azure-stack
documentationcenter: 
author: twooley
manager: byronr
editor: 
ms.assetid: 02c7ff03-874e-4951-b591-28166b7a7a79
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: twooley
ms.openlocfilehash: 5e940749917e4aade26483a79bcc238346bf94f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-administrator-and-user-portals-in-azure-stack"></a>Uso de portales de administrador y usuario de hello en la pila de Azure

Hay dos portales de pila de Azure; Hola portal de administrador y usuario hello (también denominada hello tooas *inquilino* portal). portales de Hola se basan en instancias independientes del Administrador de recursos de Azure.

tabla Hola siguiente muestra cómo tooconnect toohello portales y los puntos de conexión del Administrador de tooResource en un entorno de Kit de desarrollo de pila de Azure.

|  Portal | URL del portal | URL del punto de conexión de Resource Manager |   
| -------- | ------------- | ------- |  
| Administrador | https://adminportal.local.azurestack.external  | https://adminmanagement.local.azurestack.external  |  
| Usuario | https://portal.local.azurestack.external | https://management.local.azurestack.external  |
| | |

## <a name="hello-administrator-portal"></a>portal de administración de Hola

portal de administrador de Hello permite a una nube operador tooperform administrativo y operativo las tareas. Un operador de nube puede hacer cosas como las siguientes:
* Supervisar el estado y las alertas.
* Administrar la capacidad.
* rellenar marketplace Hola
* Crear planes y ofertas.
* Crear suscripciones para los inquilinos.

Un operador de nube también puede crear recursos, como máquinas virtuales, redes virtuales y cuentas de almacenamiento.

 ![portal de administración de Hola](media/azure-stack-manage-portals/image1.png)

 ## <a name="hello-user-portal"></a>portal de usuarios de Hola

 portal de usuarios de Hello no proporciona acceso tooany de capacidades de hello administrativos u operativos del portal de administrador de Hola. En el portal de usuarios de hello, un usuario puede suscribirse toopublic ofertas y usar servicios de Hola que están disponibles a través de dichas ofertas.

  ![portal de usuarios de Hola](media/azure-stack-manage-portals/image2.png)
 
 ## <a name="subscription-behavior"></a>Comportamiento de la suscripción
 
 Asegúrese de que comprende Hola siguiendo las diferencias entre el comportamiento de suscripción en los portales de hello dos.

 Portal de administración:
* Hay solo una suscripción que está disponible en el portal del Administrador de Hola. Esta suscripción es hello *suscripción de proveedor predeterminado*. No se puede agregar cualquier otras suscripciones para su uso en el portal del Administrador de Hola.
* Como un operador en la nube, puede agregar suscripciones para los usuarios (incluido usted) en el portal del Administrador de Hola. Los usuarios (incluido usted) pueden tener acceso y usar estas suscripciones desde el portal de usuarios de Hola.

  >[!NOTE]
  Debido a la separación de Azure Resource Manager hello, las suscripciones no se transfieren entre portales. Por ejemplo, si como un operador en la nube inicia sesión en el portal de usuarios de toohello, no se puede tener acceso a Hola suscripción de proveedor predeterminado. Por lo tanto, no tiene acceso a las funciones administrativas de tooany. Puede crear suscripciones para sí mismo a partir de ofertas públicas, pero se le considerará un usuario inquilino.

Portal de usuarios:
* En el portal de usuarios de hello, una cuenta puede tener varias suscripciones.

  >[!NOTE]
  En el entorno de kit de desarrollo hello, si un usuario inquilino pertenece toohello mismo directorio como operador de nube de hello, no se podrá iniciar sesión en toohello portal del administrador. Sin embargo, no se puede tener acceso a cualquiera de las funciones administrativas de Hola. Además, no se agregan las suscripciones o acceso ofrece realizadas toothem disponible en el portal de usuarios de Hola.

## <a name="next-steps"></a>Pasos siguientes

[Conectar tooAzure pila](azure-stack-connect-azure-stack.md)

[Administración de regiones en Azure Stack](azure-stack-region-management.md)
