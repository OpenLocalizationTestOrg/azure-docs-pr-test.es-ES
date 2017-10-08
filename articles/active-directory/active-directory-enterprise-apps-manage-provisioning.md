---
title: "aaaUser aprovisionamiento de administración para aplicaciones empresariales en hello Azure Active Directory | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage usuario aprovisionamiento de cuentas para las aplicaciones de empresa con hello Azure Active Directory"
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: 34ac4028-a5aa-40d9-a93b-0db4e0abd793
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.openlocfilehash: a613f844c8f51e04b92e62b488313a78ab85f7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-user-account-provisioning-for-enterprise-apps-in-hello-azure-portal"></a>Administración de aplicaciones empresariales en hello portal de Azure de aprovisionamiento de cuentas de usuario
Este artículo se describe cómo hello toouse [portal de Azure](https://portal.azure.com) categoría de cuentas de usuario automática de toomanage aprovisionamiento y cancelación del aprovisionamiento de aplicaciones compatibles con él, especialmente los que se han agregado de Hola "destacadas" Hola [Galería de aplicaciones de Azure Active Directory](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery). toolearn más información sobre el aprovisionamiento de cuentas de usuario automática y cómo funciona, consulte [tooSaaS automatizar el aprovisionamiento de usuarios y desaprovisionamiento aplicaciones con Azure Active Directory](active-directory-saas-app-provisioning.md).

## <a name="finding-your-apps-in-hello-portal"></a>Buscar las aplicaciones de portal de Hola
Todas las aplicaciones que están configuradas para inicio de sesión único en un directorio, un administrador de directorio mediante hello [Galería de aplicaciones de Azure Active Directory](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery), se pueden ver y administrar en hello [portal de Azure](https://portal.azure.com). las aplicaciones de Hello pueden encontrarse en hello **más servicios** &gt; **aplicaciones empresariales** sección del portal de Hola de. Las aplicaciones empresariales son aplicaciones que se implementan y se usan dentro de su organización.

![Hoja Aplicaciones empresariales][0]

Seleccionar hello **todas las aplicaciones** en vínculo Hola izquierda muestra una lista de todas las aplicaciones que se han configurado, incluidas las aplicaciones que se agregan desde la Galería de Hola. Al seleccionar una aplicación carga la hoja de recursos de Hola para esa aplicación, donde se pueden ver informes para que la aplicación y se pueden administrar diversas opciones de configuración.

Configuración de aprovisionamiento de la cuenta de usuario puede administrarse mediante la selección **Provisioning** Hola izquierda.

![Hoja Recursos de aplicación][1]

## <a name="provisioning-modes"></a>Modos de aprovisionamiento
Hola **Provisioning** hoja comienza con un **modo** menú, que muestra qué modos de aprovisionamiento son compatibles con una aplicación empresarial y les permite toobe configurado. Hola las opciones disponibles incluyen:

* **Automática** -esta opción aparece si Azure AD admite el aprovisionamiento automático basado en la API o la cancelación del aprovisionamiento de aplicación de toothis de cuentas de usuario. Al seleccionar este modo muestra una interfaz que se orienta a los administradores a través de la configuración de administración de usuarios de la aplicación de Azure AD tooconnect toohello API y la creación de asignaciones de cuentas y los flujos de trabajo que definen cómo deberían fluir los datos de la cuenta de usuario entre Azure AD y aplicación Hello y administrar servicio de aprovisionamiento de Azure AD Hola.
* **Manual** -esta opción estará disponible si Azure AD no admite el aprovisionamiento automático de aplicaciones de toothis de cuentas de usuario. Esta opción significa que los registros de cuenta de usuario almacenados en la aplicación hello deben administrarse mediante un proceso externo, basándose en las capacidades de administración y aprovisionamiento de la usuario de hello aplicación (que puede incluir aprovisionamiento Just SAML).

## <a name="configuring-automatic-user-account-provisioning"></a>Configuración del aprovisionamiento automático de cuentas de usuario
Seleccionar hello **automática** opción muestra una pantalla que se divide en cuatro secciones:

### <a name="admin-credentials"></a>Credenciales de administrador
Esto es donde se especifican las credenciales de hello necesarias para la API de administración de usuario de la aplicación de Azure AD tooconnect toohello. requerido una entrada de Hello depende de la aplicación hello. toolearn sobre los tipos de credencial de Hola y requisitos para aplicaciones específicas, consulte hello [tutorial de configuración para esa aplicación específica](active-directory-saas-app-provisioning.md#list-of-apps-that-support-automated-user-provisioning).

Seleccionar hello **Probar conexión** botón permite que las credenciales de hello tootest haciendo que Azure AD intente tooconnect toohello aplicación de aprovisionamiento de la aplicación mediante las credenciales de hello proporcionado.

### <a name="mappings"></a>Asignaciones
Esto es donde los administradores pueden ver y editar el flujo de atributos de usuario entre Azure AD y aplicación de destino de hello, cuando se aprovisiona o se actualizan las cuentas de usuario.

Hay un conjunto preconfigurado de asignaciones entre los objetos de usuario de Azure AD y los objetos de usuario de cada aplicación SaaS. Algunas aplicaciones administran otros tipos de objetos, como grupos o contactos. Selección de una de estas asignaciones de tabla de hello muestra a editor de asignación de hello toohello derecha, donde puede ver y personalizar.

![Hoja Recursos de aplicación][2]

Las personalizaciones compatibles incluyen:

* Habilitar y deshabilitar asignaciones para objetos específicos, como el objeto de usuario de la aplicación de hello Azure AD usuario objeto toohello SaaS.
* Editar fluyan de los atributos del objeto de usuario de la aplicación del toohello del objeto de usuario del hello Azure AD. Para más información sobre la asignación de atributos, consulte la sección [Información sobre los tipos de asignaciones de atributos](active-directory-saas-customizing-attribute-mappings.md#understanding-attribute-mapping-types).
* Hola filtro aprovisionamiento de las acciones que lleva a cabo en hello Azure AD dirigió a aplicación. En lugar de tener que Azure AD totalmente-sincronizar objetos, puede limitar las acciones de hello llevadas a cabo. Por ejemplo, si solo se selecciona **Actualizar**, Azure AD únicamente actualiza las cuentas de usuario existentes en una aplicación y no crea otras nuevas. Si solo se selecciona **Crear**, Azure únicamente crea nuevas cuentas de usuario, pero no actualiza los existentes. Esta característica permite a los administradores toocreate diferentes asignaciones de cuenta de los flujos de trabajo de creación y actualización.

### <a name="settings"></a>Settings
Esta sección permite administradores toostart y Hola detener servicio de aprovisionamiento de Azure AD para aplicación hello seleccionado, así como Hola opcionalmente desactive el aprovisionamiento de caché y reinicie el servicio de Hola.

Si el aprovisionamiento está habilitado para hello primera vez para una aplicación, activar servicio Hola cambiando hello **estado de aprovisionamiento** demasiado**en**. Esto hace que tooperform de servicio de aprovisionamiento de hello Azure AD una sincronización inicial, que lee los usuarios de hello asignados en hello **usuarios y grupos** sección, las consultas de aplicación de destino de Hola para ellos y, a continuación, realiza el aprovisionamiento de Hola las acciones definidas en hello Azure AD **asignaciones** sección. Durante este proceso, Hola aprovisionamiento del servicio almacena los datos almacenados en caché sobre qué cuentas de usuario que se está administrando, por lo que las cuentas no administrados dentro de las aplicaciones de destino de Hola que estaban nunca en el ámbito de asignación no se ven afectadas por las operaciones de la cancelación del aprovisionamiento. Después de hello la sincronización inicial, Hola aprovisionamiento del servicio automáticamente sincroniza objetos de usuario y de grupo en un intervalo de diez minutos.

Hola cambiante **estado de aprovisionamiento** demasiado**desactivar** simplemente pausas Hola aprovisionamiento del servicio. En este estado, Azure no crear, actualizar o quitar los objetos de grupo o usuario en la aplicación hello. Cambiar tooon de espera de estado de hello hace Hola servicio toopick donde se quedó.

Seleccionar hello **borrar el estado actual y reiniciar la sincronización** casilla de verificación y guardar se detiene Hola servicio de aprovisionamiento, volcados de hello en caché datos acerca de qué cuentas de Azure AD está administrando, reinician los servicios de Hola y realiza Hola nuevo en la sincronización inicial. Esta opción permite administradores toostart Hola proceso de implementación de aprovisionamiento de nuevo.

### <a name="synchronization-details"></a>Detalles de la sincronización
En esta sección se proporcionan detalles de suma sobre operación Hola de hello aprovisionamiento del servicio, incluido el servicio de aprovisionamiento de Hola Hola tiempos de primera y última ejecutó en la aplicación hello y cuántos de los objetos de usuario y de grupo que se van a administrar.

Se proporcionan vínculos toohello **informe de actividad de aprovisionamiento**, lo que proporciona un registro de todos los usuarios y los grupos creados, actualizado y eliminado entre AD de Azure y aplicación de destino de Hola y toohello **error de aprovisionamiento informe** que proporciona más mensajes de error de usuario y los objetos de grupo de ese error toobe leer, crear, actualizar o quitar. 

##<a name="feedback"></a>Comentarios

Esperamos que le guste su experiencia de Azure AD. Tenga procedentes de comentarios de Hola! Publique sus comentarios y sugerencias para la mejora en hello **Portal de administración de** sección de nuestro [foro de comentarios](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).  Se esté emocionados acerca de cómo crear nuevos y estupendos todos los días y usar su tooshape de instrucciones y definir qué compilar después.


[0]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-blade.PNG
[1]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-provisioning.PNG
[2]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-provisioning-mapping.PNG
