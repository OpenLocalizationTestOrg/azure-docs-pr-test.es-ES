---
title: Informes de acceso y uso para Azure MFA | Microsoft Docs
description: "Aquí se describe cómo utilizar la característica de informes de Azure Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: curtand
ms.assetid: 3f6b33c4-04c8-47d4-aecb-aa39a61c4189
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: f76e726c6a67de4b0472c0e97f9e72c31c14c4f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a>Informes en Azure Multi-Factor Authentication
Azure Multi-Factor Authentication proporciona varios tipos de informes que usted o su organización pueden usar. Estos informes son accesibles a través del Portal de administración de Multi-Factor Authentication. La siguiente es una lista de los informes disponibles:

| Informe | Descripción |
|:--- |:--- |
| Uso |Los informes de uso muestran información sobre el uso general, resúmenes y detalles de usuario. |
| Estado del servidor |Este informe muestra el estado de los Servidores Multi-Factor Authentication asociados a su cuenta. |
| Historial de usuarios bloqueados |Estos informes muestran el historial de solicitudes para bloquear o desbloquear a los usuarios. |
| Historial de usuarios omitidos |Muestra el historial de solicitudes para omitir Multi-Factor Authentication para el número de teléfono de un usuario. |
| Alerta de fraude |Muestra un historial de las alertas de fraude enviadas durante el intervalo de fechas especificado. |
| En cola |Enumera los informes en cola para su procesamiento y su estado. Cuando el informe se haya completado, se proporciona un vínculo para descargar o ver el informe. |

## <a name="view-reports"></a>Ver informes
1. Inicie sesión en el [Portal de Azure clásico](https://manage.windowsazure.com).
2. En la parte izquierda, seleccione Active Directory.
3. Siga una de estas dos opciones, dependiendo de si usa proveedores de autenticación:
   * **Opción 1**: haga clic en la pestaña Proveedores de autenticación multifactor. Seleccione el proveedor de autenticación multifactor y haga clic en el botón **Administrar** de la parte inferior.
   * **Opción 2**: seleccione el directorio y haga clic en la pestaña **Configurar**. En la sección de autenticación multifactor, seleccione **Administrar configuración del servicio**. En la parte inferior de la página Configuración del servicio MFA, haga clic en el vínculo Ir al portal.
4. En el Portal de administración de Azure Multi-Factor Authentication, seleccione el tipo de informe que desea en la sección **Ver un informe** en el panel de navegación izquierdo.

<center>![Nube](./media/multi-factor-authentication-manage-reports/report.png)</center>


**Recursos adicionales**

* [Para los usuarios](end-user/multi-factor-authentication-end-user.md)
* [Azure Multi-Factor Authenticaton en MSDN](https://msdn.microsoft.com/library/azure/dn249471.aspx)
