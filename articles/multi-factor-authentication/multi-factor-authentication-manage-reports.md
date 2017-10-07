---
title: informes de uso y aaaAccess para MFA de Azure | Documentos de Microsoft
description: "Describe cómo toouse Hola característica de la autenticación multifactor Azure - informes."
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
ms.openlocfilehash: ae7ccceca4968d7ec7cf0cb1cf9e041d9997c840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a>Informes en Azure Multi-Factor Authentication
Azure Multi-Factor Authentication proporciona varios tipos de informes que usted o su organización pueden usar. Estos informes pueden obtenerse a través de hello Portal de administración de autenticación multifactor. Hola mostramos una lista de los informes disponibles de hello:

| Informe | Descripción |
|:--- |:--- |
| Uso |información de visualización de informes de uso de Hello en los detalles del usuario, el uso general y resumen de usuario. |
| Estado del servidor |Este informe muestra el estado de Hola de servidores de autenticación multifactor asociadas a su cuenta. |
| Historial de usuarios bloqueados |Estos informes muestran Hola historial de solicitudes tooblock o desbloquear usuarios. |
| Historial de usuarios omitidos |Muestra el historial de Hola de solicitudes toobypass la autenticación multifactor para el número de teléfono del usuario. |
| Alerta de fraude |Muestra un historial de alertas de fraude enviadas durante el intervalo de fechas de hello especificado. |
| En cola |Enumera los informes en cola para su procesamiento y su estado. Cuando haya terminado el informe de hello, se proporciona un informe de Hola de toodownload o la vista de vínculo. |

## <a name="view-reports"></a>Ver informes
1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Hola izquierda, seleccione Active Directory.
3. Siga una de estas dos opciones, dependiendo de si usa proveedores de autenticación:
   * **Opción 1**: haga clic en la ficha de proveedores de autenticación multifactor de Hola. Seleccione el proveedor de MFA y haga clic en hello **administrar** situado en la parte inferior de Hola.
   * **Opción 2**: seleccione el directorio y vaya toohello **configurar** ficha. En la sección de la autenticación multifactor de hello, seleccione **administrar la configuración del servicio**. En parte inferior de Hola de página de configuración del servicio de MFA de hello, haga clic en hello Go toohello portal vínculo.
4. Hola Portal de administración de autenticación multifactor de Azure, seleccione el tipo de Hola de informe que desee en hello **ver un informe** sección Hola barra de navegación izquierda.

<center>![Nube](./media/multi-factor-authentication-manage-reports/report.png)</center>


**Recursos adicionales**

* [Para los usuarios](end-user/multi-factor-authentication-end-user.md)
* [Azure Multi-Factor Authenticaton en MSDN](https://msdn.microsoft.com/library/azure/dn249471.aspx)
