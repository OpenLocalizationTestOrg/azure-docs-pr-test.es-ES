---
title: aaaCustomizing asignaciones de atributos de AD de Azure | Documentos de Microsoft
description: "Averigüe qué asignaciones de atributos para las aplicaciones SaaS en Azure Active Directory cómo puede modificarlas tooaddress su empresa necesita."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14db5303f06fc8df3b07a0a8b75713312e71bbfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a>Personalización de asignaciones de atributos de aprovisionamiento de usuarios para aplicaciones SaaS en Azure Active Directory de usuarios
Microsoft Azure AD proporciona compatibilidad con aplicaciones de SaaS toothird terceros como Salesforce, Google Apps y otros de aprovisionamiento de usuarios. Si tiene usuarios de aprovisionamiento de una aplicación de SaaS de terceros habilitada, Hola Portal de administración de Azure controla sus valores de atributo en forma de una configuración conocida como "asignación de atributos".

Hay un conjunto preconfigurado de asignaciones de atributos entre los objetos de usuario de Azure AD y los objetos de usuario de cada aplicación SaaS. Algunas aplicaciones administran otros tipos de objetos, como grupos o contactos. <br> 
 Puede personalizar asignaciones de atributo predeterminadas Hola según las necesidades del negocio tooyour. Esto significa que puede cambiar o eliminar asignaciones de atributos existentes o crear nuevas asignaciones de atributos.

En el portal de Azure AD hello, puede tener acceso a esta característica haciendo clic en un **asignaciones** configuración bajo **Provisioning** en hello **administrar** sección de un  **Aplicación empresarial**.


![Salesforce][5] 

Al hacer clic en un **asignaciones** configuración, se abrirá Hola relacionados con **asignación de atributos** hoja.  
No hay asignaciones de atributos que son requeridas por un toofunction de aplicación de SaaS correctamente. Para los atributos necesarios, Hola **eliminar** característica no está disponible.


![Salesforce][6]  

En el ejemplo de Hola anterior, puede ver que hello **nombre de usuario** atributo de un objeto administrado en Salesforce se rellena con hello **userPrincipalName** valor de hello vincula el objeto de Active Directory de Azure.

Puede personalizar las **asignaciones de atributos** existentes haciendo clic en una asignación. Se abrirá hello **Editar atributo** hoja.

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a>Información sobre los tipos de asignación de atributos
Con asignaciones de atributos, puede controlar cómo se rellenan los atributos en una aplicación SaaS de terceros. Se admiten cuatro tipos de asignaciones diferentes:

* **Direct** : atributo de destino de Hola se rellena con el valor de Hola de un atributo del objeto vinculado Hola en Azure AD.
* **Constante** : atributo de destino de Hola se rellena con una cadena específica que se ha especificado.
* **Expresión** -atributo de destino de Hola se rellena según el resultado de hello de una expresión de tipo de secuencia de comandos. 
  Para más información, consulte [Escritura de expresiones para la asignación de atributos en Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).
* **Ninguno** -Hola atributo de destino se deja sin modificar. Sin embargo, si el atributo de destino de hello está vacío, se rellena con el valor predeterminado de Hola que especifique.

En los tipos de asignación de suma toothese cuatro atributos básicos, asignaciones de atributo personalizadas admiten concepto de Hola de opcional **predeterminado** valor de asignación. asignación de valor predeterminado de Hello garantiza que un atributo de destino se rellena con un valor si no hay ningún valor en Azure AD ni en el objeto de destino de Hola. configuración más común de Hello es tooleave este en blanco.


## <a name="understanding-attribute-mapping-properties"></a>Información sobre las propiedades de asignación de atributos

En la sección anterior de hello, ya han sido propiedad de tipo de asignación de atributo toohello se ha introducido.
En la propiedad toothis de adición, asignaciones de atributos también admiten Hola siguientes atributos:

- **Atributo de origen** -atributo de usuario de Hola Hola sistema de origen (p. ej.: Azure Active Directory).
- **Atributo de destino** : atributo de usuario de hello en el sistema de destino de hello (p. ej.: ServiceNow).
- **Coincide con los objetos mediante este atributo** : si no se debe usar esta asignación toouniquely identificar a los usuarios entre los sistemas de origen y destino de Hola. Normalmente se establece en hello userPrincipalName o atributo de correo en Azure AD, que suele ser asignada tooa campo de nombre de usuario en una aplicación de destino.
- **Precedencia de coincidencia**: se pueden establecer varios atributos coincidentes. Si hay varios, se evalúan en orden de hello definido por este campo. En el momento en que se encuentre una coincidencia, no se evaluarán más atributos coincidentes.
- **Aplicar esta asignación**
    - **Siempre**: esta asignación se aplica a las acciones de creación y actualización de usuarios
    - **Solo durante la creación**: esta asignación se aplica solo a las acciones de creación de usuarios


## <a name="what-you-should-know"></a>Qué debería saber

Microsoft Azure AD proporciona una implementación eficaz de un proceso de sincronización. En un entorno inicializado, sólo los objetos que requieren actualizaciones se procesan durante un ciclo de sincronización. Actualizar asignaciones de atributos tiene un impacto en el rendimiento de Hola de un ciclo de sincronización. Una configuración de asignación de actualización toohello atributo requiere vuelven a evaluar todas las toobe de objetos administrados. Es un mejor práctica tookeep Hola número recomendado de asignaciones de atributos de cambios consecutivos tooyour como mínimo.

## <a name="next-steps"></a>Pasos siguientes

* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [Automatizar aplicaciones del usuario aprovisionamiento o desaprovisionamiento tooSaaS](active-directory-saas-app-provisioning.md)
* [Escritura de expresiones para la asignación de atributos](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Filtros de ámbito para el aprovisionamiento de usuario](active-directory-saas-scoping-filters.md)
* [Uso de SCIM tooenable el aprovisionamiento automático de usuarios y grupos de Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Notificaciones de aprovisionamiento de cuentas](active-directory-saas-account-provisioning-notifications.md)
* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

