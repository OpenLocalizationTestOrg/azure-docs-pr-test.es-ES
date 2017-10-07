---
title: Directrices para aplicaciones aaaBranding | Documentos de Microsoft
description: "Obtener una guía de recursos orientados a toodeveloper para Azure Active Directory"
services: active-directory
documentationcenter: dev-center-name
author: skwan
manager: mbaldwin
editor: 
ms.assetid: 72f4e464-1352-4a49-a18f-c37f58e7d5c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: skwan
ms.custom: aaddev
ms.openlocfilehash: e43f884c736a0dcb2e6e51293962ef1e2636ad70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="branding-guidelines-for-applications"></a>Directrices de personalización de marca para aplicaciones
Este tema describen Hola marca directrices que se debe usar al desarrollar aplicaciones con Azure Active Directory (Azure AD). Estas instrucciones le ayudarán a dirigir a los clientes cuando lo deseen toouse su trabajo o cuenta educativa, administrada en Azure AD o su cuenta personal de aplicación tooyour registrarse e iniciar sesión.

## <a name="personal-accounts-vs-work-or-school-accounts-from-microsoft"></a>Cuentas personales frente a cuentas profesionales o educativas de Microsoft
Microsoft administra dos tipos de cuentas de usuario:

* **Cuentas personales** (anteriormente conocidas como Windows Live ID). Estas cuentas representan la relación de hello entre *individuales* a los usuarios y Microsoft y usan los dispositivos de consumo tooaccess y servicios de Microsoft. Estas cuentas están pensadas para un uso personal.
* **Cuentas profesionales o educativas.**  Estas cuentas las administra Microsoft en nombre de las organizaciones que usan Azure Active Directory. Estas cuentas son toosign utilizado en tooOffice 365 y otros servicios empresariales de Microsoft.

Microsoft suelen ser cuentas profesionales o educativas asignada a los usuarios de tooend (empleados, estudiantes, empleados federales) por las organizaciones (empresa, escuela, organismo gubernamental). Estas cuentas están que bien administrados directamente en la nube de hello, en la plataforma de hello Azure AD o sincronizado tooAzure AD desde un directorio local, como Windows Server Active Directory. Microsoft es hello *custodia* de trabajo de Hola o escolares, pero Hola cuentas posee y controladas por organización Hola.

## <a name="referring-tooazure-ad-accounts-in-your-application"></a>Cuentas de tooAzure AD que hace referencia en la aplicación
Microsoft no expone los usuarios finales toohello Azure o nombres de marca de Active Directory de Hola y que no debería hacerlo.

* Una vez que los usuarios inician sesión, debe usar el nombre y el logotipo tanto como sea posible de la organización de Hola. Esto es mejor que usar términos genéricos como "la organización".
* Cuando los usuarios no inician sesión, debe hacer referencia a las cuentas de tootheir como "trabajo o escolares" y use hello tooconvey de logotipo de Microsoft que estas cuentas estén administradas por Microsoft. No utilice términos como "cuenta de la empresa", "cuenta empresarial" ni "cuenta corporativa", ya que estos crearían confusión entre los usuarios.

## <a name="user-account-pictogram"></a>Pictograma de una cuenta de usuario
En una versión anterior de estas directrices, se recomendaba usar un pictograma con un "distintivo azul". En función de los comentarios de usuario o el desarrollador, te recomendamos que ahora uses Hola de logotipo de Microsoft de hello en su lugar. Esto le ayudará a los usuarios saber que puede volver a usar cuenta de hello que usa con Office 365 u otro toosign de servicios empresariales de Microsoft en tooyour aplicación.

## <a name="signing-up-and-signing-in-with-azure-ad"></a>Inscripción e inicio de sesión con Azure AD
La aplicación puede presentar las rutas de acceso independientes para registrarse e iniciar sesión y hello las secciones siguientes proporciona guías visuales para ambos escenarios.

**Si la aplicación admite el inicio de sesión de usuario final (p. ej. libre tootrial o freemium modelo)**: puede mostrar un **inicio de sesión** botón que permite a los usuarios tooaccess la aplicación con su cuenta profesional o su cuenta personal. Azure AD mostrará un saludo de símbolo del sistema de consentimiento la primera vez que accedan a la aplicación.

**Si su aplicación requiere permisos que solo los administradores pueden otorgar o requiere licencias para organizaciones**: debe separar la adquisición de administrador del inicio de sesión como usuario. Hola **"obtener esta aplicación" botón** se redirigir administradores toosign en, a continuación, pídale toogrant consentimiento en nombre de los usuarios de su organización. Esto ha Hola ventaja adicional de suprimir los usuarios finales consentimiento indicaciones tooyour aplicación.

## <a name="visual-guidance-for-app-acquisition"></a>Guía visual para la adquisición de la aplicación
El vínculo "obtener la aplicación hello" debe redirigir toohello Azure AD conceder acceso de usuario de hello (autorización) página, tooallow tooauthorize de administrador de una organización su toohave de aplicación tener acceso a datos de la organización tootheir hospedado por Microsoft. Obtener más información sobre cómo se tratan toorequest acceso Hola [integración de aplicaciones con Azure Active Directory](active-directory-integrating-applications.md) artículo.

Después de Admins. del consentimiento tooyour aplicación, pueden elegir tooadd, experiencia de iniciador de aplicación de Office 365 de los usuarios de tootheir (accesible desde para gofres Hola y de [https://portal.office.com/myapps](https://portal.office.com/myapps)). Si desea tooadvertise esta capacidad, puede usar términos como "Agregar esta organización de tooyour aplicación" y mostrar un botón parecido a esto:

![Tipos de aplicaciones y escenarios](./media/active-directory-branding-guidelines/add-to-my-org.png)

Sin embargo, se recomienda que escriba un texto explicativo en lugar de confiar en los botones. Por ejemplo:

> *Si ya usa Office 365 u otro servicio de negocio de Microsoft, simplemente puede conceder < your_app_name > acceso tooyour datos de la organización. Esto permitirá que su tooaccess < your_app_name > de los usuarios con sus cuentas de trabajo existentes.*
> 
> 

## <a name="visual-guidance-for-sign-in"></a>Guía visual para el inicio de sesión
La aplicación debe aparecer un inicio de sesión en el botón que redirija a los usuarios toohello inicio de sesión de punto de conexión que corresponde protocolo toohello usar toointegrate con Azure AD. Hola siguiente sección proporciona información sobre el aspecto que debería ese botón.

### <a name="pictogram-and-sign-in-with-microsoft"></a>Pictograma e Iniciar sesión en Microsoft
'S asociación Hola del logotipo de Microsoft de Hola y los términos de "Inicio de sesión en con Microsoft" hello que representa exclusivamente a Azure AD entre otros proveedores de identidad que puede admitir la aplicación. Si no tiene espacio suficiente para "Inicio de sesión en con Microsoft", es aceptar tooshorten demasiado "iniciar sesión".

![Tipos de aplicaciones y escenarios](./media/active-directory-branding-guidelines/sign-in-with-microsoft-light.png)

![Tipos de aplicaciones y escenarios](./media/active-directory-branding-guidelines/sign-in-light.png)

También puede utilizar una combinación de colores oscuro para los botones de Hola.

![Tipos de aplicaciones y escenarios](./media/active-directory-branding-guidelines/sign-in-with-microsoft-dark.png)

![Tipos de aplicaciones y escenarios](./media/active-directory-branding-guidelines/sign-in-dark.png)

## <a name="branding-dos-and-donts"></a>Personalización de marca: qué se debe hacer y qué no
**HACER** usar "cuenta profesional o educativa" en combinación con los usuarios finales del tooprovide una explicación adicional toohelp de Hola "Inicio de sesión en con Microsoft" botón reconocer si pueden usarla. **NO USE** otros términos como "cuenta empresarial", "cuenta de negocio" o "cuenta corporativa".

**No:** no use “Office 365 ID” ni “Azure ID”. Office 365 también es nombre Hola de un consumidor de la oferta de Microsoft que no usa Azure AD para la autenticación.

**No** alter logotipo de Microsoft de Hola.

**No** exponer toohello Active Directory o Azure marcas de los usuarios finales. Sin embargo, es aceptar toouse estos términos con los desarrolladores, los profesionales de TI y administradores.

## <a name="navigation-dos-and-donts"></a>Navegación: qué se debe hacer y qué no
**HACER** proporcionan una manera para los usuarios toosign out y cambiar la cuenta de usuario de tooanother. La mayoría de los usuarios tiene una sola cuenta personal de Microsoft, Facebook, Google o Twitter, pero pueden estar asociados con varias organizaciones. Próximamente se admitirá el inicio de sesión simultáneo para varios usuarios.

