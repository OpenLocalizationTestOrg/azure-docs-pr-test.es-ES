---
title: las notificaciones de aprovisionamiento de aaaAccount | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooensure que se le notifica de problemas relacionados con toouser de aprovisionamiento que requieren su atención al habilitar las notificaciones de aprovisionamiento de cuentas."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a637aac7-f06b-48ef-a66d-639835a8edec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: e33d1dd806fff43fc96f843a9dcddd7375d2e3c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="account-provisioning-notifications"></a>Notificaciones de aprovisionamiento de cuentas
Con el aprovisionamiento de usuarios, puede automatizar el proceso Hola de administración de usuarios en aplicaciones de SaaS de terceros. <br>
Aunque esto es un proceso automatizado, la interacción con este proceso es de tootime de tiempo necesario. <br>
Esto sucede, por ejemplo Hola, cuando la contraseña de Hola de cuenta de hello tooexchange datos se han configurado con una tercera aplicación expiró de SaaS de terceros. 

Al habilitar las notificaciones de aprovisionamiento de cuentas, puede asegurarse de que se le notifica de aprovisionamiento toouser relacionado de los problemas que requieren su atención.

Puede activar o desactivar las notificaciones de aprovisionamiento de cuentas como  parte de la configuración de aprovisionamiento de usuarios de aplicaciones SaaS de terceros.

![Aprovisionamiento de usuarios][1] 

tooactivate las notificaciones de aprovisionamiento de cuentas, seleccione Hola casilla correspondiente en hello **confirmación** página de diálogo y, a continuación, alias de correo electrónico de tipo hello del destinatario de Hola.

![Notificaciones de aprovisionamiento de cuentas][2]

Puede especificar una lista de distribución como destinatario; Sin embargo, es importante toonote que correo electrónico de notificación de hello contiene tooreports vínculos que solo están accesibles para los administradores de hello Azure AD.

Si tiene habilitadas las notificaciones de aprovisionamiento de cuentas, recibirá correos electrónicos sobre los problemas críticos que están relacionado toouser aprovisionamiento. Sin embargo, tooavoid una sobrecarga de correo electrónico, sólo recibirá un correo electrónico de notificación al día para cada SaaS está habilitado el correo electrónico de notificación de aplicación Hola para.

## <a name="related-articles"></a>Artículos relacionados
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [Automatizar aplicaciones del usuario aprovisionamiento o desaprovisionamiento tooSaaS](active-directory-saas-app-provisioning.md)
* [Personalización de asignaciones de atributos para el aprovisionamiento de usuarios](active-directory-saas-customizing-attribute-mappings.md)
* [Escritura de expresiones para asignaciones de atributos](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Filtros de ámbito para el aprovisionamiento de usuario](active-directory-saas-scoping-filters.md)
* [Uso de SCIM tooenable el aprovisionamiento automático de usuarios y grupos de Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-account-provisioning-notifications/ic766307.png
[2]: ./media/active-directory-saas-account-provisioning-notifications/ic766308.png
