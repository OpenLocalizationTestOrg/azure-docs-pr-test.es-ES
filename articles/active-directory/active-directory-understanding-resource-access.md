---
title: acceso a los recursos aaaUnderstanding en Azure | Documentos de Microsoft
description: "Este tema explican conceptos acerca del uso de acceso a recursos de suscripción administradores toocontrol Hola portal completo de Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: 174f1706-b959-4230-9a75-bf651227ebf6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 06b9c4166bdea849faae67cae3146c6c278deb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-resource-access-in-azure"></a>Descripción de acceso a los recursos de Azure
> [!IMPORTANT]
> Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo. Hello Azure portal proporciona [el control de acceso basado en roles](role-based-access-control-configure.md) para recursos de Azure se pueden administrar con mayor precisión.
> 
> 

En octubre de 2013, Hola portal de Azure clásico y las API de administración de servicios se integraron con Azure Active Directory en el marco de trabajo de orden toolay Hola para mejorar la experiencia del usuario de Hola para administrar el acceso a los recursos de tooAzure. Azure Active Directory ya proporciona excelentes funcionalidades, como la administración de usuarios, la sincronización de directorios locales, la autenticación multifactor y el control de acceso a aplicaciones. Naturalmente, también deben estar disponibles para administrar los recursos globales de Azure.

El control de acceso de Azure se inicia desde una perspectiva de facturación. propietario de Hola de una cuenta de Azure, tiene acceso visitando hello [centro de cuentas de Azure](https://account.windowsazure.com/subscriptions), es hello Administrador de cuenta (AA). Las suscripciones son un contenedor para la facturación, pero también actúan como límite de seguridad: cada suscripción tiene un administrador de servicios (SA) que puede agregar, quitar y modificar recursos de Azure en esa suscripción mediante el uso de hello [portal de Azure clásico](https://manage.windowsazure.com/). Hola predeterminado SA de una suscripción nueva es Hola AA, pero Hola AA puede cambiar el SA Hola Hola centro de cuentas de Azure.

<br><br>![Cuentas de Azure][1]

Las suscripciones también tienen una asociación con un directorio. directorio de Hello define un conjunto de usuarios. Estos pueden ser usuarios del trabajo de Hola o la escuela que creó el directorio de Hola o pueden ser usuarios externos (es decir, Accounts de Microsoft). Las suscripciones son accesibles mediante un subconjunto de esos usuarios del directorio que se ha asignado como administrador de servicios (SA) o Coadministrador (CA); Hello solo excepción es que, por razones heredadas, Accounts de Microsoft (anteriormente Windows Live ID) pueden asignarse como SA o CA sin estar presentes en el directorio de Hola.

<br><br>![Control de acceso de Azure][2]

Funcionalidad de hello portal de Azure clásico permite SA que han iniciado sesión con un directorio de Hola de toochange Account de Microsoft que está asociado una suscripción mediante el uso de hello **editar directorio** comando hello **Suscripciones** página **configuración**. Tenga en cuenta que esta operación tiene implicaciones en el control de acceso de Hola de esa suscripción.

> [!NOTE]
> Hola **editar directorio** comando Hola clásico de Azure portal no está disponible toousers que han iniciado sesión con un trabajo o escuela cuenta porque esas cuentas pueden iniciar sesión en solo toohello toowhich de directorio al que pertenecen.
> 
> 

<br><br>![Flujo de inicio de sesión de usuario simple][3]

En un caso simple hello, una organización (por ejemplo, Contoso) se aplicará la facturación y el control de acceso a través de hello al mismo conjunto de suscripciones. Es decir, el directorio de hello toosubscriptions asociados que pertenecen a una sola cuenta de Azure. Cuando el inicio de sesión correcto toohello portal de Azure clásico, los usuarios ven dos colecciones de recursos (representados en color naranja en la ilustración anterior hello):

* Directorios donde existe su cuenta de usuario (con origen o agregada como entidad de seguridad externa). Tenga en cuenta ese directorio de hello usados para el inicio de sesión no es relevante toothis cálculo, por lo que los directorios se muestran siempre independientemente de dónde registran.
* Pueden tener acceso recursos que forman parte de las suscripciones que están asociados con el directorio de hello usados para el inicio de sesión y que Hola usuario (donde sea un SA o CA).

<br><br>![Usuario con varias suscripciones y directorios][4]

Los usuarios con suscripciones en varios directorios tienen Hola capacidad tooswitch Hola contexto actual de hello portal de Azure clásico mediante el uso de filtro de suscripción de Hola. Tras bastidores de hello, esto da como resultado un directorio distinto de tooa de inicio de sesión independiente, pero esto se consigue de forma transparente mediante el inicio de sesión único (SSO).

Operaciones tales como mover recursos entre suscripciones pueden ser más difíciles como resultado de esta vista única del directorio de suscripciones. transferencia de recursos de tooperform hello, es posible que sea necesario toofirst usar hello **editar directorio** comando en la página de suscripciones de hello en **configuración** tooassociate Hola suscripciones toohello mismo directorio .

## <a name="next-steps"></a>Pasos siguientes
* toolearn Obtenga más información sobre cómo los administradores de toochange para una suscripción de Azure, vea [cómo tooadd o cambiar roles de administrador de Azure](../billing/billing-add-change-azure-subscription-administrator.md)
* Para obtener más información sobre cómo Azure Active Directory se relaciona tooyour suscripción de Azure, consulte [se asocian con Azure Active Directory las suscripciones de Azure](active-directory-how-subscriptions-associated-directory.md)
* Para obtener más información acerca de cómo las funciones de tooassign en Azure AD, consulte [asignar roles de administrador en Azure Active Directory](active-directory-assign-admin-roles.md)

<!--Image references-->
[1]: ./media/active-directory-understanding-resource-access/IC707931.png
[2]: ./media/active-directory-understanding-resource-access/IC707932.png
[3]: ./media/active-directory-understanding-resource-access/IC707933.png
[4]: ./media/active-directory-understanding-resource-access/IC707934.png
