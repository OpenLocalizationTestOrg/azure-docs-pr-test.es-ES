---
title: "Azure AD Connect: solución de problemas de inicio de sesión único de conexión directa | Microsoft Docs"
description: "Este tema se describe cómo tootroubleshoot Azure Active Directory sin problemas Single Sign-On (SSO sin problemas de Azure AD)."
services: active-directory
keywords: "qué es Azure AD Connect, instalar Active Directory, componentes necesarios para Azure AD, SSO, inicio de sesión único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: f1c1c11522f22d5bc742c126fff483c5b06e1f06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-seamless-single-sign-on"></a>Solución de problemas de inicio de sesión único de conexión directa de Azure Active Directory

Este artículo sirve de ayuda para encontrar información acerca de cómo solucionar los problemas comunes relativos al inicio de sesión único de conexión directa de Azure AD.

## <a name="known-issues"></a>Problemas conocidos

- Si va a sincronizar treinta bosques de AD o más, no se puede habilitar SSO de conexión directa mediante Azure AD Connect. Como alternativa, también puede [habilitar manualmente](#manual-reset-of-azure-ad-seamless-sso) característica hello en el inquilino.
- Agregar Azure AD servicio las direcciones URL (https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net) toohello "zona Sitios de confianza" en lugar de la zona de "intranet Local" hello **impide que los usuarios iniciar sesión en**.
- SSO de conexión directa no funciona en modo de exploración privada en Firefox y Edge. Y también en Internet Explorer cuando se activa el modo de protección mejorada.

>[!IMPORTANT]
>Se recientemente revierten compatibilidad con borde tooinvestigate problemas detectados por el cliente.

## <a name="check-status-of-hello-feature"></a>Comprobar el estado de la característica de Hola

Asegúrese de que esa característica de SSO sin problemas de hello sigue siendo **habilitado** en su inquilino. Puede comprobar el estado por van toohello **Azure AD Connect** hoja en hello [centro de administración de Azure Active Directory](https://aad.portal.azure.com/).

![Centro de administración de Azure Active Directory: hoja de Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>Motivos del error de inicio de sesión en el centro de administración de Azure Active Directory Hola

Un toostart lo ideal, solución de problemas de inicio de sesión de usuario con SSO sin problemas es toolook en hello [informe actividad de inicio de sesión](../active-directory-reporting-activity-sign-ins.md) en hello [centro de administración de Azure Active Directory](https://aad.portal.azure.com/).

![Centro de administración de Azure Active Directory: informe de inicios de sesión](./media/active-directory-aadconnect-sso/sso9.png)

Navegue demasiado**Azure Active Directory** -> **inicios de sesión** en hello [centro de administración de Azure Active Directory](https://aad.portal.azure.com/) y haga clic en la actividad de inicio de sesión de un usuario específico. Busque hello **código de ERROR de inicio de sesión** campo. Valor de Hola de asignación de ese motivo del error tooa campo y la resolución mediante hello en la tabla siguiente:

|Código de error de inicio de sesión|Motivo del error de inicio de sesión|Resolución
| --- | --- | ---
| 81001 | El vale de Kerberos del usuario es demasiado grande. | Reduzca la pertenencia a grupos del usuario e inténtelo de nuevo.
| 81002 | Vale de Kerberos del usuario no se puede toovalidate. | Vela la [Lista de comprobación de solución de problemas](#troubleshooting-checklist).
| 81003 | Vale de Kerberos del usuario no se puede toovalidate. | Vela la [Lista de comprobación de solución de problemas](#troubleshooting-checklist).
| 81004 | Error al intentar la autenticación Kerberos. | Vela la [Lista de comprobación de solución de problemas](#troubleshooting-checklist).
| 81008 | Vale de Kerberos del usuario no se puede toovalidate. | Vela la [Lista de comprobación de solución de problemas](#troubleshooting-checklist).
| 81009 | "Vale de Kerberos del usuario no se puede toovalidate. | Vela la [Lista de comprobación de solución de problemas](#troubleshooting-checklist).
| 81010 | No se pudo SSO sin problemas porque el vale de Kerberos del usuario de hello ha expirado o no es válido. | El usuario necesita toosign en desde un dispositivo unido al dominio dentro de su red corporativa.
| 81011 | Objeto de usuario de toofind no se puede basado en la información de vale de Kerberos del usuario de Hola. | Utilice la información de usuario de Azure AD Connect toosynchronize en Azure AD.
| 81012 | usuario de Hello intentar toosign en tooAzure AD es diferente de usuario Hola iniciado sesión en el dispositivo de Hola. | Inicie sesión desde un dispositivo diferente.
| 81013 | Objeto de usuario de toofind no se puede basado en la información de vale de Kerberos del usuario de Hola. |Utilice la información de usuario de Azure AD Connect toosynchronize en Azure AD. 

## <a name="troubleshooting-checklist"></a>Lista de comprobación de solución de problemas

Usar hello problemas de lista de comprobación tootroubleshoot SSO sin problemas siguientes:

- Compruebe si está habilitada la característica de SSO sin problemas de hello en Azure AD Connect. Si no se puede habilitar la característica de hello (por ejemplo, debido a puerto tooa bloqueado), asegúrese de que tiene todos los hello [requisitos previos](active-directory-aadconnect-sso-quick-start.md#step-1-check-prerequisites) en su lugar.
- Compruebe si ambas estos Azure AD direcciones URL (https://autologon.microsoftazuread-sso.com y https://aadg.windows.net.nsatc.net) forman parte de la configuración del usuario de hello de la zona de Intranet.
- Asegúrese de dispositivos corporativos hello es AD de toohello Unidos a un dominio.
- Asegúrese de que se registra usuario hello en dispositivo toohello con una cuenta de dominio de AD.
- Asegúrese de que cuenta de usuario de hello es de un bosque de AD que ha sido SSO sin problemas configurada.
- Asegúrese de hello dispositivo está conectado en red corporativa de Hola.
- Asegúrese de que hora del dispositivo de hello está sincronizada con hello Active Directory y controladores de dominio hello y es inferior a cinco minutos entre sí.
- Lista los vales de Kerberos existentes en dispositivo de hello mediante hello **klist** comando desde un símbolo del sistema. Compruebe si emite vales para hello `AZUREADSSOACCT` cuenta de equipo están presentes. Los vales de Kerberos de los usuarios suelen ser válidos durante 12 horas. Puede tener una configuración diferente en Active Directory.
- Purgar los vales de Kerberos existentes de dispositivo de hello mediante hello **klist purge** comando e inténtelo de nuevo.
- toodetermine si hay problemas relacionados con JavaScript, revisar los registros de la consola de hello del explorador de hello (bajo "Developer Tools").
- Hola de revisión [controlador de dominio registra](#domain-controller-logs) así.

### <a name="domain-controller-logs"></a>Registros de controlador de dominio

Si está habilitada la auditoría de acciones correctas en el controlador de dominio, a continuación, cada vez que un usuario inicia sesión con SSO sin problemas una entrada de seguridad se registra en el registro de eventos de Hola. Puede encontrar estos eventos de seguridad con hello después de consulta (busque el evento **4769** asociado a la cuenta de equipo de hello **AzureADSSOAcc$**):

```
    <QueryList>
      <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ServiceName'] and (Data='AZUREADSSOACC$')]]</Select>
      </Query>
    </QueryList>
```

## <a name="manual-reset-of-hello-feature"></a>Restablecimiento manual de la característica de Hola

Si la solución de problemas no le ha ayudado, puede restablecer manualmente la característica de hello en el inquilino. Siga estos pasos en el servidor local de Hola donde se ejecuta Azure AD Connect:

### <a name="step-1-import-hello-seamless-sso-powershell-module"></a>Paso 1: Importar el módulo de PowerShell de SSO sin problemas de Hola

1. En primer lugar, descargar e instalar hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).
2. A continuación, descargue e instale hello [módulo de Azure Active Directory de 64 bits para Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Navegue toohello `%programfiles%\Microsoft Azure Active Directory Connect` carpeta.
4. Módulo de PowerShell de SSO sin problemas de importación Hola con este comando: `Import-Module .\AzureADSSO.psd1`.

### <a name="step-2-get-hello-list-of-ad-forests-on-which-seamless-sso-has-been-enabled"></a>Paso 2: Obtener lista de Hola de bosques de AD en el que se ha habilitado el SSO sin problemas

1. Ejecute PowerShell como administrador. En PowerShell, llame a `New-AzureADSSOAuthenticationContext`. Cuando se le solicite, escriba las credenciales de administrador global de su inquilino.
2. Llame a `Get-AzureADSSOStatus`. Este comando proporciona que Hola lista de los bosques de AD (vistazo a la lista de dominios"hello") en que se ha habilitado esta característica.

### <a name="step-3-disable-seamless-sso-for-each-ad-forest-that-it-was-set-it-up-on"></a>Paso 3: Deshabilitación del SSO de conexión directa para cada bosque de AD en el que esté configurado

1. Llame a `$creds = Get-Credential`. Cuando se le solicite, escriba las credenciales de administrador de dominio de hello para el bosque de AD que vayan Hola.
2. Llame a `Disable-AzureADSSOForest -OnPremCredentials $creds`. Este comando quita hello `AZUREADSSOACCT` cuenta de equipo de hello localmente el controlador de dominio para este bosque de AD específico.
3. Repita Hola pasos para cada bosque de AD que haya configurado la característica de hello en anteriores.

### <a name="step-4-enable-seamless-sso-for-each-ad-forest"></a>Paso 4: Habilitación de SSO de conexión directa para cada bosque de AD

1. Llame a `Enable-AzureADSSOForest`. Cuando se le solicite, escriba las credenciales de administrador de dominio de hello para el bosque de AD que vayan Hola.
2. Repita Hola pasos para cada bosque de AD que desee tooset la característica de hello en anteriores.

### <a name="step-5-enable-hello-feature-on-your-tenant"></a>Paso 5. Habilitar característica de hello en el inquilino

Llame a `Enable-AzureADSSO` y el tipo en "true" en hello `Enable: ` tooturn símbolo del sistema en la característica de hello en el inquilino.
