---
title: "aaaHow toocomplete una revisión de acceso | Documentos de Microsoft"
description: "Después de que ha iniciado una revisión de acceso en Azure AD Privileged Identity Management, obtenga información acerca de cómo toocomplete y ver resultados de Hola"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a>¿Cómo toocomplete un acceso Revise en Azure AD Privileged Identity Management
Los administradores de roles con privilegios pueden revisar el acceso con privilegios cuando se [ha iniciado una revisión de seguridad](active-directory-privileged-identity-management-how-to-start-security-review.md). Azure AD Privileged Identity Management (PIM) enviará automáticamente un correo electrónico preguntar a los usuarios tooreview su acceso. Si un usuario no obtuvo un correo electrónico, se pueden enviar instrucciones de hello [cómo tooperform una revisión de seguridad](active-directory-privileged-identity-management-how-to-perform-security-review.md).

Después de período de revisión de seguridad de Hola o todos los usuarios de hello han terminado su revisar automáticamente, siga los pasos de hello en esta revisión del artículo toomanage hello y ver resultados de Hola.

## <a name="manage-security-reviews"></a>Administración de las revisiones de seguridad
1. Vaya toohello [portal de Azure](https://portal.azure.com/) y seleccione hello **Azure AD Privileged Identity Management** aplicación en el panel.
2. Seleccione hello **acceder a las revisiones** sección del panel de Hola.
3. Seleccione la revisión de acceso de Hola que desea toomanage.

En la hoja de detalle de revisión de hello acceso hay un número opciones para administrar esa revisión.

![Botones de revisión de acceso de PIM: captura de pantalla][1]

### <a name="remind"></a>Recuerde
Si una revisión de acceso está configurada para que los usuarios de hello revisar por sí mismos, Hola **avisar** botón envía una notificación. 

### <a name="stop"></a>Detención
Todas las revisiones de acceso tienen una fecha de finalización, pero puede usar hello **detener** botón toofinish cuanto antes. Si los usuarios aún no ha revisado Llegados a este punto, no será capaz de tooafter detener revisión Hola. No se puede reiniciar una revisión después de que se ha detenido.

### <a name="apply"></a>Aplicar
Una vez completada una revisión de acceso, ya sea porque se alcanza la fecha de finalización de Hola o se detuvo manualmente, Hola **aplicar** botón implementa el resultado de hello de revisión de Hola. Si se denegó el acceso de un usuario en revisión hello, este es el paso de Hola que se quitará la asignación de rol.  

### <a name="export"></a>Exportación
Si desea tooapply resultados de Hola Hola revisión de seguridad manualmente, puede exportar revisión Hola. Hola **exportar** botón iniciará la descarga de un archivo CSV. Puede administrar los resultados de hello en Excel u otros programas que se abren los archivos CSV.

### <a name="delete"></a>Eliminar
Si no está interesado en hello revisar todas aún más, elimínelo. Hola **eliminar** botón quita revisión Hola Hola aplicación PIM.

> [!IMPORTANT]
> No se recibe una advertencia antes de que se produce una eliminación, por tanto, asegúrese de que desea toodelete que revisar. 

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
