---
title: aaaManaging aplicaciones con Azure Active Directory | Documentos de Microsoft
description: "Este beneficios de Hola de artículo de la integración de Azure Active Directory con su local, en la nube y aplicaciones SaaS."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 95b96f10-2d5c-4b78-8af8-d3657a24140f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 0016f8b433e101d8a150bc6d9be3931851578241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-applications-with-azure-active-directory"></a>Administración de aplicaciones con Azure Active Directory
Más allá de flujo de trabajo real de Hola o contenido, las empresas tienen dos requisitos básicos para todas las aplicaciones:

1. productividad tooincrease, las aplicaciones deben tener toodiscover fácil y acceso
2. tooenable seguridad y gobernanza, organización Hola necesita un control y supervisión de quién puede y realmente tiene acceso a cada aplicación

En Hola mundo de aplicaciones de nube mejor esto puede lograrse mediante identidad toocontrol "*que se permite toodo lo*".

En la terminología informática:

* *Que* se conoce como *identidad* -Hola administración de usuarios y grupos
* *¿Qué* se conoce como *administración de accesos* : Hola administración de acceso a los recursos tooprotected

Ambos componentes juntos se conocen como *identidad y administración de acceso (IAM)*, que se define por hello [Gartner](http://www.gartner.com/it-glossary/identity-and-access-management-iam) grupo como "*Hola en materia de seguridad que permite derecha Hola recursos adecuados Hola de individuos tooaccess en hello derecha veces por motivos de derecho de hello*".

Bien, ¿cuál es el problema de hello? Si IAM *no se administra* en un solo lugar con una solución integrada:

* Los administradores de identidad tienen tooindividually crear y actualizar cuentas de usuario en todas las aplicaciones por separado, una actividad de un proceso lento y redundante.
* Los usuarios tienen toomemorize varias credenciales tooaccess hello las aplicaciones que necesitan toowork con. Como resultado, los usuarios suelen toowrite sus contraseñas o usar otras soluciones de administración de contraseñas que presenta otros riesgos de seguridad de datos.
* Actividades redundantes, lleva mucho tiempo reducen la cantidad de Hola de tiempo que los usuarios y los administradores trabajan en las actividades de negocio que aumentar la rentabilidad de su empresa.

De modo que, ¿qué impide normalmente a las organizaciones adoptar soluciones IAM integradas?

* Soluciones más técnicas se basan en plataformas de software que necesitan toobe implementado y adaptado por cada organización para sus propias aplicaciones.
* Las aplicaciones de nube a menudo se adoptan a un ritmo más rápido del que las organizaciones de TI pueden integrarse con las soluciones IAM existentes.
* Seguridad y herramientas de supervisión requieren personalización e integración tooachieve completa E2E escenarios adicionales.

## <a name="azure-active-directory-integrated-with-applications"></a>Azure Active Directory integrado con las aplicaciones
Azure Active Directory es la solución completa de identidad como servicio (IDaaS) de Microsoft que:

* Habilita la IAM como un servicio en la nube. 
* Proporciona administración de acceso central, inicio de sesión único (SSO) y creación de informes. 
* Admite la administración de acceso integrado para [miles de aplicaciones](https://azure.microsoft.com/marketplace/active-directory/) en Galería de aplicaciones de hello, incluyendo Salesforce, Google Apps, Box, Concur e. 

Con Azure Active Directory, todas las aplicaciones que publique la aplicación por los socios y los clientes (business o consumidor) tienen Hola mismas capacidades de administración de identidades y acceso.<br> Esto permite toosignificantly reducir los costos operativos.

¿Qué ocurre si necesita una aplicación que todavía no figura en la Galería de aplicaciones de hello tooimplement? Aunque esto es un poco más lento que la configuración de SSO para aplicaciones de la Galería de aplicaciones de Hola, Azure AD proporciona un asistente que le ayudará con la configuración de Hola.

valor de Hola de Azure AD va más allá de "solo" aplicaciones en la nube. También puede utilizarlo con aplicaciones locales al proporcionar acceso remoto seguro. Con el acceso remoto seguro, podrá eliminar Hola Hola necesario para las redes privadas virtuales u otras implementaciones de administración de acceso remoto tradicionales.

Al proporcionar administración de acceso central y el inicio de sesión único (SSO) para todas las aplicaciones, Azure AD proporciona soluciones hello toohello problemas de seguridad y productividad de datos principal.

* Los usuarios pueden tener acceso a varias aplicaciones con un inicio de sesión que proporciona más tooincome tiempo empresariales o generar actividades de operaciones realizadas.
* Los administradores de identidad pueden administrar tooapplications de acceso en un solo lugar.

beneficio de Hello para el usuario de Hola y de su empresa es obvio. Echemos un vistazo más de cerca en ventajas de Hola para un administrador de identidades y la organización de Hola.

## <a name="integrated-application-benefits"></a>Ventajas de aplicaciones integradas
Hola proceso SSO consta de dos pasos:

* Autenticación, proceso de Hola de validación de identidad del usuario de Hola.
* Autorización, Hola tooenable de decisión o bloquear el acceso a recursos de tooa con una directiva de acceso.

Al utilizar aplicaciones de Azure AD toomanage y habilitar SSO:

* La autenticación se realiza en (por ejemplo, AD) local o la cuenta de Azure AD del usuario de Hola.
* Autorización se ejecuta en hello Azure AD protección y asignación de directiva asegurándose de experiencia del usuario final coherente y Habilitar asignación tooadd, ubicaciones y las condiciones MFA en cualquier aplicación, independientemente de sus capacidades internas.

Es importante toounderstand que Hola autorización de manera Hola está aplicado en la aplicación de destino de hello varía en función de la aplicación hello se integró con Azure AD.

* **Aplicaciones integradas previamente por el proveedor de servicios**, como Office 365 y Azure. Se trata de aplicaciones integradas directamente en Azure AD y que dependen de él para sus funcionalidades completas de administración de identidades y acceso. Las aplicaciones de Access toothese se habilita a través de la emisión de información y el símbolo (token) de directorio.
* **Aplicaciones integradas previamente por Microsoft y aplicaciones personalizadas**. Son aplicaciones de nube independientes que dependen de un directorio de aplicaciones interno y pueden funcionar con independencia de Azure AD. Las aplicaciones de Access toothese está habilitado mediante la emisión de una cuenta de aplicación de aplicación específico credencial asignada tooan. Según las capacidades de aplicación Hola, credencial Hola puede ser un símbolo (token) de federación o el nombre de usuario y la contraseña de una cuenta que se haya proporcionado anteriormente en la aplicación hello.
* **Aplicaciones locales** aplicaciones publican a través de proxy de aplicación hello Azure AD principalmente habilitar las aplicaciones de access tooon local. Estas aplicaciones se basan en un directorio local central, como Windows Server Active Directory. Las aplicaciones de Access toothese está habilitado mediante la activación de usuario final de hello proxy toodeliver Hola aplicación toohello contenido respetando Hola local sesión requisito al mismo tiempo.

Por ejemplo, si un usuario une a su organización, debe toocreate una cuenta de usuario de hello en Azure AD para operaciones de inicio de sesión principal de Hola. Si este usuario necesita acceso tooa administrar aplicaciones, como Salesforce, también necesitará toocreate una cuenta para este usuario en Salesforce y vincúlela trabajo SSO de toomake de toohello cuenta de Azure. Cuando Hola alguien deja la empresa, es aconsejable toodelete Hola cuenta de Azure AD y todas las cuentas de homólogo Hola almacenes IAM de aplicaciones de Hola Hola usuario tenía acceso a.

## <a name="access-detection"></a>Detección de acceso
En las empresas modernas, los departamentos de TI a menudo no son conscientes de las aplicaciones de nube de Hola que se utilizan. De forma conjunta con Cloud App Discovery, Azure AD proporciona una solución toodetect estas aplicaciones.

## <a name="account-management"></a>Administración de cuentas
Tradicionalmente, administra cuentas en hello diversas aplicaciones es un proceso manual realizado por TI o compatible con el personal de organización de Hola. Azure AD automatiza completamente la administración de cuentas en todas las aplicaciones integradas del proveedor de servicios y en esas aplicaciones previamente integradas por Microsoft que admiten el aprovisionamiento automático de usuarios o SAML JIT.

## <a name="automated-user-provisioning"></a>Aprovisionamiento automático de usuarios
Algunas aplicaciones proporcionan interfaces de automatización para la creación y eliminación (o desactivación) de cuentas. Si un proveedor ofrece esta interfaz, Azure Active Directory hace uso de ella. Esto reduce los costos operativos dado que las tareas administrativas se realizan automáticamente y mejora la seguridad de Hola de su entorno ya que reduce la posibilidad de Hola de acceso no autorizado.

## <a name="access-management"></a>administración de acceso
Con Azure AD puede administrar acceso a tooapplications mediante individuales o regla controlada por las asignaciones. También puede delegar el acceso a administración toohello personas en hello organización garantizar Hola mejor supervisión y reducir la carga de Hola de departamento de soporte técnico.

## <a name="on-premises-applications"></a>Aplicaciones locales
Hola integrada en el proxy de aplicación permite toopublish experiencia con las ventajas de hello y aplicación de nube modernas de acceso de los usuarios de tooyour de aplicaciones local resultante en ambas coherente de supervisión de Azure AD, los informes y capacidades de seguridad .

## <a name="reporting-and-monitoring"></a>Creación de informes y supervisión
Azure AD proporciona y capacidades que permiten tooknow quién tiene acceso tooapplications y cuando realmente utilizan ellos de supervisión e informes previamente integradas.

## <a name="related-capabilities"></a>Funcionalidades relacionadas
Con Azure AD puede proteger las aplicaciones con directivas de acceso granular y MFA previamente integrada. toolearn más sobre Azure MFA, consulte [Azure MFA](https://azure.microsoft.com/services/multi-factor-authentication/).

## <a name="getting-started"></a>Introducción
tooget a integrar aplicaciones con Azure AD, eche un vistazo a hello [Guía de introducción de integración de Azure Active Directory con las aplicaciones obtener](active-directory-integrating-applications-getting-started.md).

## <a name="see-also"></a>Otras referencias
[Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)

