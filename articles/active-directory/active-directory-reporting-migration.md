---
title: los informes de actividad de aaaFind de hello portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo se notifica toofind actividad de Azure Active Directory en hello portal de Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a>Buscar informes de actividad en hello portal de Azure

Si va a mover de hello Azure toohello portal clásico de portal de Azure, obtendrá un nuevo aspecto en registros de actividad de Azure Active Directory (Azure AD). En una encuesta reciente [entrada de blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), explicamos cómo puede ver registros de actividad en el contexto de hello del recurso de saludo está trabajando en hello portal de Azure. En este artículo se describe cómo toofind informa que usó en el portal de Azure clásico en el portal de Azure Hola Hola.

## <a name="whats-new"></a>Novedades

Informes en el portal de Azure clásico Hola se dividen en categorías:

1.  Informes de seguridad
2.  Informes de actividad
3.  Informes de aplicaciones integradas

### <a name="activity-and-integrated-app-reports"></a>Informes de actividad y de aplicaciones integradas

Para generación de informes basada en contexto en hello portal de Azure, los informes existentes se combinan en una sola vista. Una única API subyacente proporciona Hola datos toohello vista.

toosee esta vista, en hello **Azure Active Directory** hoja, en **actividad**, seleccione **registros de auditoría**.

![Registros de auditoría](./media/active-directory-reporting-migration/482.png "Registros de auditoría")

Hola siguientes informes está consolidado en esta vista:

-   Informe de auditoría
-   Actividad de restablecimiento de contraseña
-   Actividad de registro de restablecimiento de contraseñas
-   Actividad de los grupos de autoservicio
-   Cambios de nombre de grupo de Office365
-   Actividad de aprovisionamiento de cuentas
-   Estado de la sustitución de contraseña
-   Errores de aprovisionamiento de cuentas


Hola informes de uso de la aplicación se ha mejorado y se incluye en hello **inicios de sesión** vista. toosee esta vista, en hello **Azure Active Directory** hoja, en **actividad**, seleccione **inicios de sesión**.

![Vista de inicios de sesión](./media/active-directory-reporting-migration/483.png "Vista de inicios de sesión")

Hola **inicios de sesión** vista incluye todos los inicios de sesión. Puede utilizar esta información de uso de aplicaciones de tooget de información. También puede ver información de uso de la aplicación Hola **aplicaciones empresariales** información general, en hello **administrar** sección.

![Aplicaciones empresariales](./media/active-directory-reporting-migration/484.png "Aplicaciones empresariales")

## <a name="access-a-specific-report"></a>Acceso a un informe específico

Aunque Hola portal de Azure ofrece una vista única, también puede buscar en informes específicos.

### <a name="audit-logs"></a>Registros de auditoría

Comentarios de respuesta toocustomer, Hola portal de Azure, puede usar avanzadas filtrado tooaccess Hola de datos que desee. Es un filtro que se puede usar un *categoría de actividad*, que enumeran Hola diferentes tipos de actividad registra en Azure AD. toonarrow toowhat de resultados que está buscando, puede seleccionar una categoría.

Por ejemplo, si está interesado en los restablecimientos de contraseña de tooself servicio relacionado de actividades, puede elegir hello **administración de contraseñas de autoservicio** categoría. categorías de Hello que verá se basan en recursos de hello en que si está trabajando.  

![Opciones de la categoría en la página de registros de auditoría de filtro de hello](./media/active-directory-reporting-migration/06.png "opciones de la categoría en la página de registros de auditoría de filtro de Hola")

Las categorías de actividad incluyen:

- Core Directory (Directorio principal)
- Self-service Password Management (Administración de contraseñas de autorservicio)
- Self-service Group Management (Administración de grupos de autoservicio)
- Account Provisioning (Aprovisionamiento de cuentas)

### <a name="application-usage"></a>Uso de la aplicación

tooview los detalles sobre el uso de la aplicación para todas las aplicaciones o para una sola aplicación en **actividad**, seleccione **inicios de sesión**. resultados de hello toonarrow, puede filtrar por nombre de usuario o nombre de la aplicación.

![Página Filtrar eventos de inicio de sesión](./media/active-directory-reporting-migration/07.png "Página Filtrar eventos de inicio de sesión")

### <a name="security-reports"></a>Informes de seguridad

#### <a name="azure-ad-anomalous-activity-reports"></a>Informes de actividades anómalas de Azure AD

Seguridad de Azure AD actividad anómala informes desde el portal de Azure clásico Hola han sido tooprovide consolidado a una, vista central. Esta vista muestra todos los eventos de riesgo relacionados con la seguridad que Azure AD puede detectar e informar.

Hello en la tabla siguiente enumera los tipos de eventos de riesgo correspondientes en hello portal de Azure e informes de seguridad de actividad anómala de hello Azure AD.

| Informe de actividad anómala de Azure AD |  Tipo de evento de riesgo de Identity Protection|
| :--- | :--- |
| Usuarios con credenciales perdidas | Credenciales con fugas |
| Actividad de inicio de sesión irregular | Viaje imposible tooatypical ubicaciones |
| Inicios de sesión desde dispositivos posiblemente infectados | Inicios de sesión desde dispositivos infectados|
| Inicios de sesión desde orígenes desconocidos | Inicios de sesión desde direcciones IP anónimas |
| Inicios de sesión desde direcciones IP con actividad sospechosa | Inicios de sesión desde direcciones IP con actividad sospechosa |
| - | Inicios de sesión desde ubicaciones desconocidas |

Hola después de seguridad de la actividad anómala de Azure AD informa que no se incluyen como eventos de riesgo en hello portal de Azure:

* Inicios de sesión tras varios errores
* Inicios de sesión desde varias ubicaciones geográficas

Estos informes siguen estando disponibles en el portal de Azure clásico hello, pero dejará de utilizarse en algún momento futuro Hola.

Para más información, consulte [Eventos de riesgo de Azure Active Directory](active-directory-identity-protection-risk-events.md).  


#### <a name="detected-risk-events"></a>Eventos de riesgo detectados

Hola portal de Azure, puede tener acceso a informes acerca de los eventos de riesgo detectados en hello **Azure Active Directory** hoja, en **seguridad**. Se realiza el seguimiento de eventos de riesgo detectados en hello después de informes:   

- Usuarios en riesgo
- Inicios de sesión no seguros

![Informes de seguridad](./media/active-directory-reporting-migration/04.png "Informes de seguridad")

Para más información sobre los informes de seguridad, consulte:

- [Usuarios de informes de seguridad de riesgo en el portal de Azure Active Directory Hola](active-directory-reporting-security-user-at-risk.md)
- [Riesgo informe de inicios de sesión en el portal de Azure Active Directory Hola](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a>Informes de actividad en hello portal de Azure clásico frente a Hola portal de Azure

tabla de Hello en esta sección enumeran los informes existentes en hello portal de Azure clásico. También se describe cómo puede obtener Hola la misma información en hello portal de Azure.

tooview todos los datos, en Hola de auditoría **Azure Active Directory** hoja, en **actividad**, vaya demasiado**registros de auditoría**.

![Registros de auditoría](./media/active-directory-reporting-migration/61.png "Registros de auditoría")

| Portal de Azure clásico                 | toofind Hola portal de Azure                                                         |
| ---                                  | ---                                                                        |
| Registros de auditoría                           | Para **Categoría de actividad**, seleccione **Directorio principal**.                       |
| Actividad de restablecimiento de contraseña              | Para **Categoría de actividad**, seleccione **Administración de contraseñas de autoservicio**. |
| Actividad de registro de restablecimiento de contraseñas | Para **Categoría de actividad**, seleccione **Administración de contraseñas de autoservicio**.     |
| Actividad de los grupos de autoservicio         | Para **Categoría de actividad**, seleccione **Administración de grupos de autoservicio**.        |
| Actividad de aprovisionamiento de cuentas        | Para **Categoría de actividad**, seleccione **Aprovisionamiento de usuarios de la cuenta**.         |
| Estado de la sustitución de contraseña             | En **Categoría de actividad**, seleccione **Sustitución automática de contraseñas de aplicación**.      |
| Errores de aprovisionamiento de cuentas          | Para **Categoría de actividad**, seleccione **Aprovisionamiento de usuarios de la cuenta**.        |
| Cambios de nombre de grupo de Office365         | Para **Categoría de actividad**, seleccione **Administración de contraseñas de autoservicio**. Para **Tipo de recurso de actividad**, seleccione **Grupo**. Para **Origen de la actividad**, seleccione **Grupos de O365**.|

Hola tooview **uso de la aplicación** informes en hello **Azure Active Directory** hoja, en **administrar**, seleccione **aplicaciones empresariales**y, a continuación, seleccione **inicios de sesión**.


![Informe Inicios de sesión de aplicaciones empresariales](./media/active-directory-reporting-migration/199.png "Informe Inicios de sesión de aplicaciones empresariales")

## <a name="next-steps"></a>Pasos siguientes

Para obtener información general de informes, vea hello [reporting de Azure Active Directory](active-directory-reporting-azure-portal.md).
