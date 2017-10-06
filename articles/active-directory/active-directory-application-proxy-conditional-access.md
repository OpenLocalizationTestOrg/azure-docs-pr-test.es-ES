---
title: aaaConditional acceso local tooon apps - Azure AD | Documentos de Microsoft
description: "Explica cómo tooset el acceso condicional para las aplicaciones se publique toobe acceder de forma remota con el Proxy de aplicación de Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2e97722b-eb4e-4078-b607-9fed210d8a0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7bed25dd4ba17941e77d8c4b2b9ba4edcf0cf597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-conditional-access-in-azure-ad-application-proxy"></a>Trabajo con acceso condicional en el proxy de la aplicación de Azure AD

>[!NOTE]
>En este artículo se aplica toohello portal de Azure clásico, que se va a retirar. Le recomendamos que use hello [portal de Azure](https://portal.azure.com). Hola portal de Azure, las aplicaciones tienen el Proxy de aplicación Hola mismas características de acceso condicional como cualquier otra aplicación de SaaS. toolearn más información sobre el acceso condicional, consulte [empezar a trabajar con el acceso condicional en Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).

Puede configurar el acceso tooapplications de acceso condicional de toogrant de las reglas publicadas mediante el Proxy de aplicación. Esto le permite:

* Exigir la autenticación multifactor por aplicación
* Exigir la autenticación multifactor solo cuando los usuarios no están en el trabajo
* Impedir que los usuarios obtener acceso a la aplicación hello cuando no están en el trabajo

Estas reglas pueden resultar tooall aplicados a los usuarios y grupos o sólo toospecific a los usuarios y grupos. De forma predeterminada los usuarios de tooall que tienen acceso toohello aplicación aplica de regla de Hola. Sin embargo regla hello también puede ser restringido toousers que son miembros de grupos de seguridad especificados.  

Cuando un usuario tiene acceso a una aplicación federada que usa OAuth 2.0, OpenID Connect, SAML o WS-Federation, se evalúan las reglas de acceso. Además, las reglas de acceso se evalúan con OAuth 2.0 y OpenID Connect cuando un token de actualización es tooacquire usa un token de acceso.

## <a name="conditional-access-prerequisites"></a>Requisitos previos de acceso condicional
* Suscripción tooAzure Active Directory Premium
* Un inquilino de Azure Active Directory administrado o federado
* Los inquilinos federados requieren Multi-Factor Authentication (MFA)  
    ![Configurar reglas de acceso - exigir Multi-Factor Authentication](./media/active-directory-application-proxy-conditional-access/application-proxy-conditional-access.png)

## <a name="configure-per-application-multi-factor-authentication"></a>Configuración de Multi-Factor Authentication por aplicación
1. Inicie sesión como administrador en hello portal de Azure clásico.
2. Vaya tooActive directorio y seleccione el directorio de hello en el que desee tooenable Proxy de aplicación.
3. Haga clic en **aplicaciones** y desplácese hacia abajo toohello **reglas de acceso** sección. sección de reglas de acceso de Hello sólo aparece para las aplicaciones publicadas mediante el Proxy de aplicación que utilizan autenticación federada.
4. Habilitar regla Hola seleccionando **habilitar reglas de acceso** demasiado**en**.
5. Especifique Hola usuarios y grupos toowhom Hola se aplican reglas. Hola de uso **Agregar grupo** botón tooselect uno o varios grupos que se aplica la regla de acceso de toowhich Hola. Este cuadro de diálogo también puede ser grupos de tooremove usado seleccionado.  Una vez las reglas de hello toogroups tooapply seleccionado, se aplican las reglas de acceso de hello solo para los usuarios que pertenecen tooone de hello especificada los grupos de seguridad.  

   * comprobar tooexplicitly excluir los grupos de seguridad de la regla de hello, **excepto** y especificar uno o más grupos. Los usuarios que son miembros de un grupo de hello excepto lista no son tooperform requiere la autenticación multifactor.  
   * Si un usuario se ha configurado mediante la característica de la autenticación multifactor por usuario de hello, esta configuración tiene prioridad sobre hello las reglas de la autenticación multifactor de aplicación. Un usuario que se ha configurado para cada usuario la autenticación multifactor es tooperform requiere la autenticación multifactor aunque se haya excluido de las reglas de la aplicación hello la autenticación multifactor. Obtenga más información sobre [Multi-Factor Authentication y la configuración por usuario](../multi-factor-authentication/multi-factor-authentication.md).
6. Seleccione la regla de acceso de hello que desea tooset:

   * **Requerir la autenticación multifactor**: los usuarios aplican reglas de acceso de toowhom son toocomplete requiere la autenticación multifactor antes de acceder a Hola aplicación toowhich Hola regla se aplica.
   * **Requerir la autenticación multifactor fuera del trabajo**: usuarios probando la aplicación de hello tooaccess desde una dirección IP de confianza no estará tooperform requiere la autenticación multifactor. Hola de confianza se pueden configurar intervalos de direcciones IP en la página de configuración de la autenticación multifactor de Hola.
   * **Bloquear el acceso fuera del trabajo**: usuarios probando la aplicación de hello tooaccess desde fuera de la red corporativa no será capaz de tooaccess Hola.

## <a name="configuring-mfa-for-federation-services"></a>Configuración de MFA para servicios de federación
Para los inquilinos federados, puede realizar la autenticación multifactor (MFA) con Azure Active Directory u Hola servidor de AD FS local. De forma predeterminada, MFA se produce en cualquier página hospedada por Azure Active Directory. tooconfigure MFA local, ejecute Windows PowerShell y use Hola – SupportsMFA propiedad tooset Hola módulo Azure AD.

Hello en el ejemplo siguiente se muestra cómo tooenable local MFA mediante el uso de hello [cmdlet Set-MsolDomainFederationSettings](https://msdn.microsoft.com/library/azure/dn194088.aspx) en el inquilino de contoso.com hello:`Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true `

En suma toosetting esta marca, Hola inquilino federado AD FS instancia debe ser configurado tooperform la autenticación multifactor. Siga las instrucciones de Hola para [implementar Microsoft Azure la autenticación multifactor local](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="see-also"></a>Otras referencias
* [Trabajar con las aplicaciones para notificaciones](active-directory-application-proxy-claims-aware-apps.md)
* [Publicar aplicaciones con Proxy de aplicación](active-directory-application-proxy-publish.md)
* [Habilitar el inicio de sesión único](active-directory-application-proxy-sso-using-kcd.md)
* [Publicar aplicaciones mediante su propio nombre de dominio](active-directory-application-proxy-custom-domains.md)

Para obtener las actualizaciones y noticias más recientes de hello, visite hello [blog de Proxy de aplicación](http://blogs.technet.com/b/applicationproxyblog/)
