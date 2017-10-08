---
title: "Autenticación de paso a través de Azure AD: inicio rápido | Microsoft Docs"
description: "Este artículo describe cómo tooget se inicia con la autenticación de paso a través de Azure Active Directory (Azure AD)."
services: active-directory
keywords: "Autenticación de paso a través de Azure AD Connect, instalación de Active Directory, componentes necesarios para Azure AD, SSO, inicio de sesión único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: billmath
ms.openlocfilehash: d6d0f85fe144cf36cc94676f6592d37988b20647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-quick-start"></a>Autenticación de paso a través de Azure Active Directory: inicio rápido

## <a name="how-toodeploy-azure-ad-pass-through-authentication"></a>¿Cómo toodeploy autenticación de paso a través de Azure AD

Autenticación de paso a través de Azure Active Directory (Azure AD) permite la toosign usuarios tooboth en local y aplicaciones basadas en la nube mediante Hola mismas contraseñas. Los usuarios inician sesión mediante la validación de sus contraseñas directamente en la instancia de Active Directory local.

>[!IMPORTANT]
>La autenticación de paso a través de Azure AD se encuentra actualmente en versión preliminar. Si ha estado usando esta característica a través de la vista previa, debe asegurarse de que actualizar las versiones preliminares de agentes de autenticación de hello utilizando instrucciones Hola proporcionadas [aquí](./active-directory-aadconnect-pass-through-authentication-upgrade-preview-authentication-agents.md).

Necesita toofollow estos toodeploy autenticación de paso a través de instrucciones:

## <a name="step-1-check-prerequisites"></a>Paso 1: Comprobación de los requisitos previos

Asegúrese de que Hola siguiendo los requisitos previos están en su lugar:

### <a name="on-hello-azure-active-directory-admin-center"></a>En el centro de administración de Azure Active Directory Hola

1. Cree una cuenta de administrador global solo en la nube en el inquilino de Azure AD. De esta manera, puede administrar configuración de hello del inquilino de los servicios locales falla o se dejan de estar disponibles. Información acerca de la [incorporación de una cuenta de administrador global que está solo en la nube](../active-directory-users-create-azure-portal.md). Este paso es tooensure crítico que no quedar bloqueado de su inquilino.
2. Agregue uno o varios [nombres de dominio personalizado](../active-directory-add-domain.md) inquilino tooyour Azure AD. Los usuarios inician sesión con uno de estos nombres de dominio.

### <a name="in-your-on-premises-environment"></a>En el entorno local

1. Identificar un servidor que ejecuta Windows Server 2012 R2 o posterior en qué toorun de Azure AD Connect. Agregar bosque toohello misma instancia de AD del servidor de hello como usuarios de hello cuyas contraseñas necesitan toobe validado.
2. Instalar hello [versión más reciente de Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) en servidor hello identificado en el paso anterior. Si ya dispone de ejecución de Azure AD Connect, asegúrese de que la versión hello es 1.1.557.0 o posterior.
3. Identificar un servidor adicional que se ejecuta Windows Server 2012 R2 o posterior en qué toorun un agente de autenticación independiente. la versión del agente de autenticación Hola necesita toobe 1.5.193.0 o una versión posterior. Este servidor es necesario tooensure alta disponibilidad de las solicitudes de inicio de sesión. Agregar bosque toohello misma instancia de AD del servidor de hello como usuarios de hello cuyas contraseñas necesitan toobe validado.
4. Si hay un firewall entre los servidores y Azure AD, deberá hello tooconfigure siguientes elementos:
   - Asegúrese de que los agentes de autenticación puede realiza **saliente** solicita tooAzure AD sobre Hola siguientes puertos:
   
   | Número de puerto | Cómo se usa |
   | --- | --- |
   | **80** | Descarga de revocación de certificados (CRL) enumera al validar el certificado SSL de Hola |
   | **443** | Toda la comunicación saliente con nuestro servicio |
   
   Si el firewall aplica las reglas según los usuarios toooriginating, abra estos puertos para el tráfico de servicios de Windows que se ejecutan como servicio de red.
   - Si el firewall o proxy permite crear listas blancas con DNS, las conexiones de la lista blanca de direcciones demasiado**\*. msappproxy.net** y  **\*. servicebus.windows.net**. Si no es así, permitir el acceso demasiado[intervalos de direcciones IP del centro de datos de Azure](https://www.microsoft.com/download/details.aspx?id=41653), que se actualiza semanalmente.
   - Los agentes de autenticación necesitan tener acceso demasiado**login.windows.net** y **login.microsoftonline.com** para el registro inicial, abra el firewall para dichas direcciones así.
   - Para la validación de certificado, desbloquear hello las siguientes direcciones URL: **mscrl.microsoft.com:80**, **crl.microsoft.com:80**, **ocsp.msocsp.com:80** y  **www.Microsoft.com:80**. Estas direcciones URL se utilizan para la validación de certificados con otros productos de Microsoft, por lo que es posible que estas direcciones URL estén bloqueadas.

## <a name="step-2-enable-exchange-activesync-support-optional"></a>Paso 2: Habilitación de la compatibilidad con Exchange ActiveSync (opcional)

Siga estos tooenable instrucciones del soporte técnico de Exchange ActiveSync:

1. Use [Exchange PowerShell](https://technet.microsoft.com/library/mt587043(v=exchg.150).aspx) hello toorun siguiente comando:
```
Get-OrganizationConfig | fl per*
```

2. Comprobar valor Hola de hello `PerTenantSwitchToESTSEnabled` configuración. Si el valor de hello es **true**, su inquilino está configurado correctamente: suele ser el caso de hello para la mayoría de los clientes. Si el valor de hello es **false**, ejecute hello comando siguiente:
```
Set-OrganizationConfig -PerTenantSwitchToESTSEnabled:$true
```

3. Compruebe que el valor de Hola Hola `PerTenantSwitchToESTSEnabled` configuración ahora se establece demasiado**true**. Espere una hora antes de mover toohello siguiente paso.

Si encuentra algún problema durante este paso, consulte la [guía de solución de problemas](active-directory-aadconnect-troubleshoot-pass-through-authentication.md#exchange-activesync-configuration-issues) para más información.

## <a name="step-3-enable-hello-feature"></a>Paso 3: Habilitar la característica de Hola

La autenticación de paso a través se puede habilitar por medio de [Azure AD Connect](active-directory-aadconnect.md).

>[!IMPORTANT]
>Autenticación de paso a través puede habilitarse en el servidor principal o de ensayo de hello Azure AD Connect. Se recomienda encarecidamente habilitarlo desde el servidor principal de Hola.

Si va a instalar Azure AD Connect para hello primera vez, elija hello [ruta de acceso de instalación personalizada](active-directory-aadconnect-get-started-custom.md). En hello **inicio de sesión de usuario** página, elija **autenticación de paso a través** como Hola inicio de sesión en el método. Cuando se finaliza correctamente, se instala un agente de autenticación de paso a través en hello mismo servidor que Azure AD Connect. Además, la característica de autenticación de paso a través de hello está habilitada en su inquilino de.

![Azure AD Connect: inicio de sesión de usuario](./media/active-directory-aadconnect-sso/sso3.png)

Si ya ha instalado Azure AD Connect (con hello [instalación rápida](active-directory-aadconnect-get-started-express.md) o hello [instalación personalizada](active-directory-aadconnect-get-started-custom.md) ruta de acceso), seleccione **página de inicio de sesión de usuario de cambio** en Azure AD Conectarse y haga clic en **siguiente**. A continuación, seleccione **autenticación de paso a través** como Hola inicio de sesión en el método. Cuando se finaliza correctamente, se instala un agente de autenticación de paso a través en hello mismo servidor que la característica de Azure AD Connect y Hola está habilitado en el inquilino.

![Azure AD Connect: Change user sign-in page (Cambiar página de inicio de sesión del usuario)](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

>[!IMPORTANT]
>La autenticación de paso a través es una característica de nivel de inquilino. Activación de afecta a iniciar sesión para los usuarios a través de _todos los_ Hola administra dominios en su inquilino. Si cambia de tooPass mediante autenticación de AD FS, se recomienda que espere al menos 12 horas antes de apagar la infraestructura de AD FS, este tiempo de espera es tooensure que los usuarios pueden mantener sesión tooExchange ActiveSync durante la transición.

## <a name="step-4-test-hello-feature"></a>Paso 4: Probar la característica de Hola

Siga estos tooverify de instrucciones que se ha habilitado la autenticación de paso a través correctamente:

1. Inicie sesión en toohello [centro de administración de Azure Active Directory](https://aad.portal.azure.com) con credenciales de administrador Global de hello para el inquilino.
2. Seleccione **Azure Active Directory** en el panel de navegación izquierdo Hola.
3. Seleccione **Azure AD Connect**.
4. Compruebe que hello **autenticación de paso a través** característica se muestra como **habilitado**.
5. Seleccione **Autenticación de paso a través**. Esta hoja enumera los servidores de Hola donde están instalados los agentes de autenticación.

![Centro de administración de Azure Active Directory: hoja de Azure AD Connect](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Centro de administración de Azure Active Directory: hoja de Autenticación de paso a través](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

En esta fase, los usuarios de todos los dominios administrados del inquilino pueden iniciar sesión con la autenticación de paso a través. Sin embargo, los usuarios de dominios federados seguir toosign en con los servicios de federación de Active Directory (AD FS) u otro proveedor de federación que se ha configurado previamente. Si convierte un dominio de toomanaged federada, todos los usuarios del dominio iniciar automáticamente el inicio de sesión mediante autenticación de paso a través. Característica de autenticación de paso a través de hello no afectan a los usuarios solo en la nube.

## <a name="step-5-ensure-high-availability"></a>Paso 5: Garantía de alta disponibilidad

Si tiene previsto toodeploy autenticación de paso a través en un entorno de producción, debe instalar un agente de autenticación independiente. Instale este segundo agente de autenticación en un servidor _otros_ de Hola un funcionamiento Azure AD Connect y Hola primer agente de autenticación. Esta configuración proporciona alta disponibilidad de las solicitudes de inicio de sesión. Siga estos toodeploy instrucciones un agente de autenticación independiente:

1. **Descargar Hola la versión más reciente del agente de autenticación de hello (versiones 1.5.193.0 o una versión posterior)**: inicie sesión en toohello [centro de administración de Azure Active Directory](https://aad.portal.azure.com) con credenciales de administrador Global de su inquilino.
2. Seleccione **Azure Active Directory** en el panel de navegación izquierdo Hola.
3. Seleccione **Azure AD Connect** y después **Autenticación de paso a través**. Seleccione **Descargar agente**.
4. Haga clic en hello **Aceptar términos & Descargar** botón.
5. **Instale Hola la versión más reciente del agente de autenticación de Hola**: Hola de ejecución ejecutable descargado en hello anterior paso. Proporcione las credenciales de administrador global de su inquilino cuando se le solicite.

![Centro de administración de Azure Active Directory: botón Download Authentication Agent (Descargar agente de autenticación)](./media/active-directory-aadconnect-pass-through-authentication/pta9.png)

![Centro de administración de Azure Active Directory: hoja Descargar agente](./media/active-directory-aadconnect-pass-through-authentication/pta10.png)

>[!NOTE]
>También puede descargar Hola agente de autenticación de [aquí](https://aka.ms/getauthagent). Asegúrese de que revise y acepte Hola Authentication Agent [las condiciones del servicio](https://aka.ms/authagenteula) _antes de_ instalarla.

## <a name="next-steps"></a>Pasos siguientes
- [**Limitaciones actuales**](active-directory-aadconnect-pass-through-authentication-current-limitations.md): esta funcionalidad actualmente está en su versión preliminar. Obtenga información sobre los escenarios que se admiten y los que no.
- [**Profundización técnica**](active-directory-aadconnect-pass-through-authentication-how-it-works.md): descripción del funcionamiento de esta característica.
- [**Preguntas más frecuentes** ](active-directory-aadconnect-pass-through-authentication-faq.md) -responde toofrequently preguntas más frecuentes.
- [**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Obtenga información acerca de cómo emite tooresolve común con la característica de Hola.
- [**SSO de conexión directa de Azure AD**](active-directory-aadconnect-sso.md): obtenga más información sobre esta característica complementaria.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para rellenar solicitudes de características nuevas.
