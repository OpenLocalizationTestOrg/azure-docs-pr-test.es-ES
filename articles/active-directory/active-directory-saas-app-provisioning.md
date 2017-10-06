---
title: "aaaAutomated SaaS aplicación aprovisionamiento de usuarios en Azure AD | Documentos de Microsoft"
description: "Un toohow de introducción que se puede utilizar Azure AD tooautomatically provisión, desaprovisionar y actualizar continuamente las cuentas de usuario en varias aplicaciones de SaaS de terceros."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 58c5fa2d-bb33-4fba-8742-4441adf2cb62
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: curtand
ms.openlocfilehash: a1f3ecdd513e2b603f8ad9901e9f551b3b982b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automate-user-provisioning-and-deprovisioning-toosaas-applications-with-azure-active-directory"></a>Automatizar usuario aprovisionamiento y desaprovisionamiento rápidos tooSaaS aplicaciones con Azure Active Directory
## <a name="what-is-automated-user-provisioning-for-saas-apps"></a>¿Qué es el aprovisionamiento automático de usuarios para aplicaciones SaaS?
Azure Active Directory (Azure AD) permite la creación de hello tooautomate, mantenimiento y eliminación de identidades de usuario en la nube ([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) aplicaciones como Dropbox, Salesforce, ServiceNow y mucho más.

**A continuación se muestran algunos ejemplos de lo que esta característica le permite toodo:**

* Crea automáticamente nuevas cuentas en hello aplicaciones SaaS correctas para los usuarios nuevos cuando se unan a su equipo.
* Desactivar automáticamente las cuentas de aplicaciones SaaS cuando los usuarios dejan inevitablemente equipo Hola.
* Asegúrese de que las identidades de hello en las aplicaciones de SaaS se mantengan actualizados toodate según los cambios en el directorio de Hola.
* Aprovisionar objetos de no usuario, como los grupos de aplicaciones de tooSaaS que las admiten.

**Aprovisionamiento automático de usuarios, también incluye Hola siguiente funcionalidad:**

* Hola identidades existentes de capacidad toomatch entre Azure AD y las aplicaciones de SaaS.
* Opciones de personalización toohelp Azure AD ajusta configuraciones actuales de Hola Hola de aplicaciones de SaaS que su organización está usando actualmente.
* Alertas de correo electrónico opcionales para errores de aprovisionamiento.
* Informes y la actividad toohelp de registros con la supervisión y solución de problemas.

## <a name="why-use-automated-provisioning"></a>¿Por qué usar el aprovisionamiento automático?
Las razones habituales por las que se debe usar esta característica son:

* los costos de hello tooavoid, ineficiencias y error humano asociado con los procesos de aprovisionamiento manual.
* toosecure de su organización mediante la eliminación al instante las identidades de los usuarios de clave aplicaciones SaaS cuando abandonan la organización de Hola.
* tooeasily importar un número de cargas masivas de usuarios en una aplicación SaaS en particular.
* comodidad de hello tooenjoy de tener la solución de aprovisionamiento funcionar solo con hello mismas directivas de acceso de aplicación que definiera para Azure AD Single Sign-On.

## <a name="frequently-asked-questions"></a>Preguntas frecuentes
**¿La frecuencia con Azure AD escribe aplicaciones de SaaS de toohello de cambios de directorio?**

Azure AD comprueba los cambios cada cinco minutos de tooten. Si la aplicación de SaaS hello devuelve varios errores (como en el caso de hello de credenciales de administrador no válido), Azure AD ralentice gradualmente su tooonce de tooup de frecuencia al día hasta que se solucionen los errores de Hola.

**¿Durante cuánto tiempo tardará tooprovision Mis usuarios?**

Cambios incrementales se lleven a cabo casi al instante pero si está tratando de tooprovision la mayoría de su directorio, depende del número de Hola de usuarios y grupos que tiene. Los directorios pequeños tardan sólo unos minutos, los medianos pueden tardar varios minutos y los directorios muy grandes pueden tardar varias horas.

**¿Cómo puedo realizar un seguimiento de progreso de Hola de trabajo de aprovisionamiento actual de hello?**

Puede revisar Hola informe de aprovisionamiento de cuentas en la sección de informes de Hola de su directorio. Otra opción es pestaña de panel de hello toovisit de hello aplicación SaaS que va a aprovisionar para y busque en la sección de "Estado de integración" cerca de la parte inferior de Hola de página de Hola Hola.

**¿Cómo se sabe si los usuarios no pueden tooget aprovisionado correctamente?**

Al final de Hola de hello aprovisionamiento Asistente de configuración no existe es un notificaciones de tooemail toosubscribe de opción para el aprovisionamiento de errores. También puede comprobar hello toosee de informe de errores de aprovisionamiento de los usuarios que no pudo toobe aprovisionado y por qué.

**¿Azure AD puede escribir los cambios del directorio de hello SaaS aplicación back-toohello?**

Para la mayoría de las aplicaciones de SaaS, el aprovisionamiento es solo de salida, lo que significa que se escriben los usuarios de aplicación de toohello del directorio de hello y cambios de la aplicación hello no se pueden volver a escribir toohello directory. Para [Workday](https://msdn.microsoft.com/library/azure/dn762434.aspx), sin embargo, el aprovisionamiento es sólo de entrada, lo que significa que los que los usuarios se importan en el directorio de Hola desde jornada laboral, y del mismo modo, cambios en el directorio de hello no obtener reescriben a jornada laboral.

**¿Cómo puedo enviar del equipo de ingeniería toohello comentarios?**

Póngase en contacto con nosotros a través de hello [foro de comentarios de Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/).

## <a name="how-does-automated-provisioning-work"></a>¿Cómo funciona el aprovisionamiento automático?
Azure AD proporciona a usuarios tooSaaS aplicaciones mediante la conexión de puntos de conexión de tooprovisioning proporcionados por cada proveedor de la aplicación. Estos puntos de conexión permiten a Azure AD tooprogrammatically crear, actualizar y quitar usuarios. A continuación se muestra una breve descripción de hello pasos diferentes que Azure AD toma tooautomate aprovisionamiento.

1. Cuando se habilita el aprovisionamiento de una aplicación para hello primera vez, se realiza Hola siguientes acciones:
   * Azure AD intentará toomatch todos los usuarios existentes en la aplicación de SaaS hello con sus identidades correspondientes en el directorio de Hola. Cuando se asocia un usuario, *no* se habilitan automáticamente para el inicio de sesión único. En orden para una aplicación de usuario toohave acceso toohello, debe haber asignado explícitamente toohello aplicación en Azure AD, ya sea directamente o a través de la pertenencia a grupos.
   * Si ya ha especificado qué usuarios deben asignarse toohello aplicación, y si se produce un error en Azure AD toofind cuentas existentes para los usuarios, Azure AD ofrece nuevas cuentas para ellos en la aplicación hello.
2. Una vez que se ha completado la sincronización inicial de hello como se describió anteriormente, Azure AD comprobará cada 10 minutos para hello siguientes cambios:
   * Si se han asignado a los usuarios nuevos para aplicación toohello (ya sea directamente o a través de la pertenencia a grupos), entonces estarán aprovisionar una nueva cuenta en la aplicación de SaaS hello.
   * Si se ha quitado el acceso de un usuario, su cuenta de aplicación de SaaS hello se marcará como deshabilitado (nunca totalmente eliminan usuarios, que le protege contra la pérdida de datos en caso de hello de una configuración incorrecta).
   * Si un usuario se ha asignado recientemente toohello aplicación y ya tenían una cuenta de hello aplicación SaaS, que cuenta se marcará como habilitado y, algunas propiedades de usuario pueden actualizarse si están obsoletas toohello comparados directorio.
   * Si ha cambiado la información del usuario (por ejemplo, número de teléfono, ubicación de oficina, etcetera) en el directorio de hello, esa información también se actualizará en hello aplicación SaaS.

Para obtener más información sobre cómo se asignan los atributos entre Azure AD y la aplicación de SaaS, consulte el artículo de hello en [personalizar las asignaciones de atributo](active-directory-saas-customizing-attribute-mappings.md).

## <a name="list-of-apps-that-support-automated-user-provisioning"></a>Lista de aplicaciones que admiten el aprovisionamiento automático de usuarios
Las aplicaciones de "Destacado" hello en Galería de aplicaciones de Azure AD de Hola de admitan el aprovisionamiento automático de usuarios. [lista de Hola de aplicaciones destacadas puede verse a continuación.](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)

En orden para un aplicación toosupport automatizadas aprovisionamiento de usuario, primero debe proporcionar Hola los extremos necesarios que permiten la creación de programas externos tooautomate hello, mantenimiento y eliminación de usuarios. Por lo tanto, no todas las aplicaciones SaaS son compatibles con esta característica. Para las aplicaciones que lo admiten, equipo de ingeniería de Azure AD de Hola a continuación ser capaz de toobuild un aprovisionamiento toothose de conector de aplicaciones, y este trabajo es ordenada por nivel de necesidades de Hola de clientes actuales y potenciales.

ingeniería de hello Azure AD toocontact equipo toorequest aprovisionamiento proporciona compatibilidad para aplicaciones adicionales, envíe un mensaje a través de hello [foro de comentarios de Azure Active Directory](https://feedback.azure.com/forums/374982-azure-active-directory-application-requests/category/172035-user-provisioning).

## <a name="related-articles"></a>Artículos relacionados
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [Personalización de asignaciones de atributos para el aprovisionamiento de usuarios](active-directory-saas-customizing-attribute-mappings.md)
* [Escritura de expresiones para asignaciones de atributos](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Filtros de ámbito para el aprovisionamiento de usuario](active-directory-saas-scoping-filters.md)
* [Uso de SCIM tooenable el aprovisionamiento automático de usuarios y grupos de Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Notificaciones de aprovisionamiento de cuentas](active-directory-saas-account-provisioning-notifications.md)
* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones SaaS](active-directory-saas-tutorial-list.md)

