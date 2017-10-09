---
title: "aaaHow tooconfigure usuario aprovisionar la aplicación de la Galería de Azure AD tooan | Documentos de Microsoft"
description: "Cómo configurar rápidamente cuenta de usuario enriquecida de aprovisionamiento y desaprovisionamiento rápidos tooapplications ya aparece en la Galería de aplicaciones de Azure AD Hola"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2c28e59a3ac8f221ed93b2f6b0b1221f7604af23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-user-provisioning-tooan-azure-ad-gallery-application"></a>Cómo aprovisionar la aplicación de la Galería de Azure AD tooan de usuario de tooconfigure

*Aprovisionamiento de cuentas de usuario* Hola consisten en crear, actualizar o deshabilitar registros de cuenta de usuario en el almacén de perfiles de usuario local de la aplicación. La mayoría en la nube y aplicaciones SaaS almacenan Hola roles de los usuarios y los permisos en su propio almacén de perfiles de usuario local, y es la presencia de un registro de usuario en su almacén local *necesario* para toowork único de inicio de sesión y el acceso.

Hola portal de Azure, Hola **Provisioning** ficha Panel de navegación izquierdo de Hola para una aplicación empresarial, se muestran los modos de aprovisionamiento se admiten para esa aplicación. Puede ser uno de dos valores:

## <a name="configuring-an-application-for-manual-provisioning"></a>Configuración de una aplicación para el aprovisionamiento manual

*Manual* aprovisionamiento significa que las cuentas de usuario se deben crear manualmente utilizando los métodos de hello proporcionados por esa aplicación. Esto podría suponer iniciar sesión en un portal administrativo para esa aplicación y agregar usuarios mediante una interfaz de usuario basada en Web. O bien, podría tener que cargar una hoja de cálculo con los detalles de las cuentas de usuario, mediante un mecanismo proporcionado por esa aplicación. Consulte la documentación de hello proporcionados por aplicación hello, o una aplicación Hola póngase en contacto con mecanismos de desarrollador toodetermine wat están disponibles.

Si Manual es el modo solo Hola se muestra para una aplicación determinada, significa que ningún conector de aprovisionamiento de Azure AD automática aún se ha creado para la aplicación hello. O bien, significa aplicación hello no soporte Hola usuario son un requisito previo API de administración de en qué toobuild un conector de aprovisionamiento automatizado.

Si desea recibir soporte técnico de toorequest para el aprovisionamiento automático para una aplicación determinada, puede rellenar una solicitud en <http://aka.ms/aadapprequest>.

## <a name="configuring-an-application-for-automatic-provisioning"></a>Configuración de una aplicación para el aprovisionamiento automático

*Automático* significa que se ha desarrollado un conector de aprovisionamiento de Azure AD para esta aplicación. Para obtener más información sobre hello Azure AD de aprovisionamiento de servicio y cómo funciona, consulte [tooSaaS automatizar el aprovisionamiento de usuarios y desaprovisionamiento aplicaciones con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).

Para obtener más información sobre cómo ver usuarios específicos de tooprovision y la aplicación de tooan grupos [administración de aprovisionamiento de cuentas de usuario para aplicaciones empresariales](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).

Hola tooenable necesarios pasos real y configurar el aprovisionamiento automático varían dependiendo de la aplicación hello.

>[!NOTE]
>Debe empezar por buscar Hola toosetting específico tutorial de instalación de aprovisionamiento para la aplicación y después esos pasos tooconfigure aplicación hello y Azure AD toocreate Hola conexión aprovisionamiento. 
>
>

Tutoriales de aplicación pueden encontrarse en [lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).

Una tooconsider importante al configurar el aprovisionamiento puede tooreview y configurar asignaciones de atributos de Hola y flujos de trabajo que definen qué flujo de propiedades de usuario (o grupo) de la aplicación de Azure AD toohello. Esto incluye el establecimiento de Hola "hacer coincidir la propiedad" que ser usado toouniquely identificar y asociar los usuarios/grupos entre sistemas de hello dos. Para más información acerca de este proceso importante.

## <a name="next-steps"></a>Pasos siguientes
[Personalización de asignaciones de atributos de aprovisionamiento de usuarios para aplicaciones SaaS en Azure Active Directory de usuarios](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

