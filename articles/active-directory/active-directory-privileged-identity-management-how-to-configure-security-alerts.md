---
title: alertas de seguridad de aaaHow tooconfigure | Documentos de Microsoft
description: "Obtenga información acerca de cómo las alertas de seguridad tooconfigure de extensión de Privileged Identity Management de Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4e0c911a-36c6-42a0-8f79-a01c03d2d04f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 1b3c4a7d36fa3f81bb3fe2574d675fdf0ab34909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-security-alerts-in-azure-ad-privileged-identity-management"></a>¿Cómo tooconfigure security muestra una alerta en Azure AD Privileged Identity Management
## <a name="security-alerts"></a>Alertas de seguridad
Privileged Identity Management (PIM) de Azure genera alertas cuando existen actividades sospechosas o no seguras en su entorno. Cuando se desencadene una alerta, muestra en el panel PIM Hola. Seleccione Hola alerta toosee un informe que enumera Hola usuarios o roles que desencadenó la alerta de Hola.

![Alertas de seguridad del panel de PIM: captura de pantalla][1]

| Alerta | Desencadenador | Recomendación |
| --- | --- | --- |
| **Se están asignando roles fuera de PIM** |Un administrador asignó permanentemente rol tooa, fuera de la interfaz PIM Hola. |Revise la nueva asignación de roles Hola. Dado que otros servicios solo pueden asignar a los administradores permanentes, cambiar, tooan elegible asignación si es necesario. |
| **Se están activando roles con demasiada frecuencia** |Se han producido demasiados Reactivaciones de hello mismo rol en tiempo de hello permitido en la configuración de Hola. |Póngase en contacto con hello usuario toosee ¿por qué activó el rol de hello tantas veces. Tiempo de hello quizás límite es demasiado corto para ellos toocomplete sus tareas, o quizás que usas scripts tooautomatically activar un rol. |
| **No se necesita la autenticación multifactor para la activación de los roles** |Hay funciones sin MFA habilitada en la configuración de Hola. |Se requiere MFA para los roles de hello con más altos privilegiada, pero recomendamos encarecidamente que habilite MFA para la activación de todos los roles. |
| **Los administradores no están usando sus roles con privilegios** |Hay administradores aptos que no han activado sus roles recientemente. |Iniciar un acceso revisión toodetermine Hola a los usuarios que no necesitan acceso. |
| **Demasiados administradores globales** |Hay más administradores globales de lo que se recomienda. |Si tiene un gran número de administradores globales, es probable que los usuarios estén obteniendo más permisos de los que necesitan. Mover a los usuarios que no requiere herramientas con privilegios roles, o realizar algunas de ellas aptos para su rol de hello en lugar de asignados permanentemente. |

## <a name="configure-security-alert-settings"></a>Configuración de alertas de seguridad
Puede personalizar algunas de las alertas de seguridad de hello en PIM toowork con el entorno y los objetivos de seguridad. Siga estos hoja de configuración de pasos tooreach hello:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) y seleccione hello **Azure AD Privileged Identity Management** icono de panel de Hola.
2. Seleccione **Roles con privilegios administrados** > **Configuración** > **Configuración de alertas**.
   
    ![Navegar por la configuración de alertas toosecurity][2]

### <a name="roles-are-being-activated-too-frequently-alert"></a>Alerta "Los roles se están activando con demasiada frecuencia"
Esta alerta se activa si un usuario activa Hola mismo rol con privilegios varias veces en un período especificado. Puede configurar ambos número de hello y período de tiempo de Hola de activaciones.

* **Período de tiempo de renovación de activación**: especificar en días, horas, minutos y la segunda vez Hola período que desea toouse tootrack sospechosa renovaciones.
* **Número de renovaciones de activación**: especificar Hola número de activaciones de too100 2, que tener en cuenta que alerta, en período de tiempo de Hola que eligió. Puede cambiar esta configuración mediante el control deslizante de hello móvil o escribiendo un número en el cuadro de texto de Hola.

### <a name="there-are-too-many-global-administrators-alert"></a>Alerta "Demasiados administradores globales"
El PIM desencadena esta alerta si se cumplen dos criterios diferentes, y puede configurar ambos. En primer lugar, deberá tooreach un umbral determinado de administradores globales. En segundo lugar, un porcentaje determinado de las asignaciones de roles totales deben ser administradores globales. Si solo se cumple una de estas medidas, alerta de hello no aparece.  

* **Número mínimo de administradores globales**: especificar Hola número de administradores globales, de 2 too100, tenga en cuenta una cantidad no segura.
* **Porcentaje de administradores globales**: especifique el porcentaje de Hola de los administradores que son administradores globales, de 0% too100%, que no es segura en su entorno.

### <a name="administrators-arent-using-their-privileged-roles-alert"></a>Alerta "Los administradores no están usando sus roles con privilegios"
Esta alerta se desencadena si un usuario pasa un cierto tiempo sin activar un rol.

* **Número de días**: especifique Hola número de días, de 0 too100, que un usuario puede ejecutarse sin activar un rol.

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_dash.png
[2]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_settings.png
