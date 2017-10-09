---
title: aaaAzure acceso condicional para aplicaciones de SaaS | Documentos de Microsoft
description: "Acceso condicional en Azure AD permite el acceso de tooblock de capacidad de Hola y se tooconfigure según la aplicación de la autenticación multifactor reglas de acceso para los usuarios no en una red de confianza. "
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 69748014c0c8e266ba66562980c784aba4c68d80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-conditional-access"></a>Introducción al acceso condicional de Azure Active Directory
El acceso condicional de Azure Active Directory a las aplicaciones [SaaS](https://azure.microsoft.com/overview/what-is-saas/) y a las aplicaciones conectadas a Azure AD le permite configurar el acceso condicional en función del grupo, la ubicación y la confidencialidad de la aplicación. 

Con el acceso condicional basado en la confidencialidad de la aplicación, puede establecer reglas de acceso de autenticación multifactor (MFA) por aplicación. MFA por aplicación proporciona acceso de tooblock de capacidad de Hola para los usuarios que no están en una red de confianza. Puede aplicar MFA reglas tooall usuarios a los que se asignan toohello aplicación, o solo para los usuarios dentro de los grupos de seguridad especificados.  Los usuarios pueden excluirse de obligatoriedad de MFA de hello si tienen acceso aplicación hello desde una dirección IP que está dentro de la red de la organización de Hola.

Estas funcionalidades estarán disponibles toocustomers que ha adquirido una licencia de Azure Active Directory Premium.

## <a name="scenario-prerequisites"></a>Requisitos previos de escenario
* Licencia de Azure Active Directory Premium
* Inquilino de Azure Active Directory federado o administrado
* Para los inquilinos federados, es necesario que la autenticación multifactor esté habilitada.

## <a name="configure-per-application-access-rules"></a>Configuración de las reglas de acceso por aplicación
Esta sección describe cómo tooconfigure según la aplicación tener acceso a las reglas.

1. Inicie sesión en toohello Azure portal clásico con una cuenta que sea un administrador global para Azure AD.
2. En el panel izquierdo de hello, seleccione **Active Directory**.
3. En la ficha directorio de hello, seleccione el directorio.
4. Seleccione hello **aplicaciones** ficha.
5. Aplicación Hola SELECT que Hola regla se establecerá para.
6. Seleccione hello **configurar** ficha.
7. Desplácese hacia abajo de la sección de reglas de acceso de toohello. Seleccione la regla de acceso deseado Hola.
8. Especifique los usuarios de Hola Hola regla se aplicará a.
9. Habilitar directiva de hello seleccionando **habilitado toobe en**.

## <a name="understanding-access-rules"></a>Descripción de las reglas de acceso
En esta sección se ofrece una descripción detallada de las reglas de acceso de hello admitidos Hola acceso condicional de aplicación de Azure.

### <a name="specifying-hello-users-hello-access-rules-apply-to"></a>Especificar los usuarios de Hola Hola acceso reglas se aplican a
De forma predeterminada aplicará por directiva de hello tooall usuarios que tienen acceso toohello aplicación. Sin embargo, también puede restringir hello toousers de directiva que son miembros de hello especificadas los grupos de seguridad. Hola **Agregar grupo** botón está tooselect usa uno o más grupos del cuadro de diálogo de selección de grupo de Hola que Hola regla de acceso se aplicarán a. Este cuadro de diálogo también puede ser grupos de tooremove usado seleccionado. Una vez las reglas de hello tooGroups tooapply seleccionada, solo se aplicarán las reglas de acceso de Hola para los usuarios que pertenezcan tooone de hello especificada los grupos de seguridad.

Grupos de seguridad pueden también explícitamente excluirse de la directiva de hello seleccionando hello **excepto** opción y especifique uno o varios grupos. Los usuarios que sean miembros de un grupo de hello **excepto** lista no será el requisito de la autenticación multifactor de asunto toohello, incluso si son miembros de un grupo de esa regla de acceso de Hola se aplica a.
regla de acceso de Hola que se muestra a continuación requerirá todos los usuarios de hello administradores grupo toouse la autenticación multifactor al obtener acceso a la aplicación hello.

![Configuración de reglas de acceso condicional con MFA](./media/active-directory-conditional-access-azuread-connected-apps/conditionalaccess-saas-apps.png)

## <a name="conditional-access-rules-with-mfa"></a>Reglas de acceso condicional con MFA
Si un usuario se ha configurado mediante la característica de la autenticación multifactor por usuario de hello, esta configuración de usuario de hello combinará con las reglas de la autenticación multifactor de Hola de aplicación hello. Esto significa que un usuario que se ha configurado para la autenticación de multifactor por usuario estará tooperform requiere la autenticación multifactor aunque se haya excluido de las reglas de la autenticación multifactor de aplicación Hola. Obtenga más información sobre Multi-Factor Authentication y la configuración por usuario.

### <a name="access-rule-options"></a>Opciones de reglas de acceso
se admite Hola siguientes opciones:

* **Requerir la autenticación multifactor**: usuarios de hello aplican reglas de acceso de toowhom hello, podrán toocomplete requiere la autenticación multifactor antes de obtener acceso a la aplicación hello que Hola directiva se aplica a.
* **Requerir la autenticación multifactor fuera del trabajo**: un usuario que procede de una dirección IP de confianza no estará tooperform requiere la autenticación multifactor. Hola de confianza se pueden configurar intervalos de direcciones IP en la página de configuración de la autenticación multifactor de Hola.
* **Bloquear acceso fuera del trabajo**: se bloqueará a los usuarios que no procedan de una dirección IP de confianza. Hola de confianza se pueden configurar intervalos de direcciones IP en la página de configuración de la autenticación multifactor de Hola.

### <a name="setting-rule-status"></a>Configuración del estado de la regla
Estado de la regla de acceso permite activar o desactivar la reglas de Hola. Cuando hello las reglas de acceso están desactivadas, no se aplica el requisito de la autenticación multifactor de Hola.

### <a name="access-rule-evaluation"></a>Evaluación de la regla de acceso
Cuando un usuario tiene acceso a una aplicación federada que usa OAuth 2.0, OpenID Connect, SAML o WS-Federation, se evalúan las reglas de acceso. Además, las reglas de acceso se evalúan cuando hello OAuth 2.0 y OpenID Connect utilizan un tooacquire de símbolo (token) de la actualización de un token de acceso. Si se produce un error en la evaluación de la directiva cuando se usa un token de actualización, Hola error **concesión_no_válida** se devolverán, esto indica que necesita de usuario de hello toore-autenticar toohello cliente.

### <a name="configure-federation-services-tooprovide-multi-factor-authentication"></a>Configurar federación servicios tooprovide la autenticación multifactor
Para los inquilinos federados, MFA puede realizarse mediante Azure Active Directory u Hola servidor de AD FS local.

De forma predeterminada, MFA se producirá en una página hospedada por Azure Active Directory. Hola tooconfigure MFA local, **– SupportsMFA** propiedad debe establecerse demasiado**true** en Azure Active Directory mediante el módulo de hello Azure AD para Windows PowerShell.

Hello en el ejemplo siguiente se muestra cómo tooenable local MFA mediante el uso de hello [cmdlet Set-MsolDomainFederationSettings](https://msdn.microsoft.com/library/azure/dn194088.aspx) en el inquilino de contoso.com hello:

    Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true

En suma toosetting esta marca, Hola inquilino federado AD FS instancia debe ser configurado tooperform la autenticación multifactor. Siga las instrucciones de Hola para [implementar la autenticación multifactor Azure local](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="related-articles"></a>Artículos relacionados
* [Proteger el acceso tooOffice 365 y otras aplicaciones conectadas tooAzure Active Directory](active-directory-conditional-access.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)

