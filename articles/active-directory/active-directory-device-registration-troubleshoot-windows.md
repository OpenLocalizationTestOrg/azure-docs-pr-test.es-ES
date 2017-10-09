---
title: "equipos Unidos de aaaTroubleshooting Hola el registro automático de dominio de Azure AD para Windows 10 y Windows Server 2016 | Documentos de Microsoft"
description: "Solución de problemas de registro automático de Hola de dominio de Azure AD los equipos Unidos para Windows 10 y Windows Server 2016."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 3795323ce9392368b412b3e1208868431e59a74b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a>Solución de problemas de registro automático de dominio unido equipos tooAzure AD – Windows 10 y Windows Server 2016

Este tema es aplicable toohello después de los clientes:

-   Windows 10
-   Windows Server 2016

Para otros clientes de Windows, vea [solución de problemas de registro automático de dominio unido equipos tooAzure AD para clientes de nivel inferior de Windows](active-directory-device-registration-troubleshoot-windows-legacy.md).

En este tema se da por supuesto que ha configurado el registro automático de dispositivos Unidos a un dominio como se ha descrito en se describe en [cómo tooconfigure el registro automático de Windows Unidos a dominios dispositivos con Azure Active Directory](active-directory-device-registration-get-started.md) Hola de toosupport los escenarios siguientes:

- [Acceso condicional basado en dispositivos](active-directory-conditional-access-automatic-device-registration-setup.md)

- [Perfiles móviles de empresa](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello para empresas](active-directory-azureadjoin-passport-deployment.md)


Este documento proporciona instrucciones para solucionar problemas sobre cómo tooresolve posibles problemas. 

Hello el registro se admite en Windows hello actualizar 10 de noviembre de 2015 y versiones posteriores.  
Se recomienda usar actualización de aniversario de Hola para habilitar escenarios de hello anteriores.

## <a name="step-1-retrieve-hello-registration-status"></a>Paso 1: Recuperar el estado de registro de hello 

**estado de registro de hello tooretrieve:**

1. Abra el símbolo del sistema de hello como administrador.

2. Escriba **dsregcmd /status**



    +----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+
    
        AzureAdJoined : YES
     EnterpriseJoined: Ningún Id. de dispositivo: huella digital de 5820fbe9-60c8-43b0-bb11-44aee233e4e7: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected de proveedor de cifrado de la plataforma de Microsoft: Sí KeySignTest:: debe ejecutar con permisos elevados tootest.
                  Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO
    
    +----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES



## <a name="step-2-evaluate-hello-registration-status"></a>Paso 2: Evaluar el estado de registro de hello 

Revise Hola después de campos y asegúrese de que tienen valores de hello esperados:

### <a name="azureadjoined--yes"></a>AzureAdJoined : YES  

Este campo muestra si el dispositivo de hello está registrado con Azure AD. Si el valor de Hola se muestra como "NO", el registro no ha terminado. 

**Causas posibles:**

- Error de autenticación del equipo de hello para el registro.

- Hay un proxy HTTP en la organización de Hola que no se puede detectar por equipo Hola

- equipo de Hello no puede establecer comunicación con Azure AD para la autenticación o DRS de Azure para el registro

- Hello equipo no esté en la red interna de la organización de Hola o en VPN con la línea de visión directa tooan controlador de dominio de AD local.

- Si el equipo de hello tiene un TPM, puede estar en mal estado.

- Puede haber un error de configuración en los servicios indicados en el documento de Hola que necesitará tooverify nuevo. Los ejemplos comunes son:

    - El servidor de federación no tiene habilitados los puntos de conexión de WS-Trust.

    - Es posible que el servidor de federación no pueda permitir la autenticación de entrada de equipos de la red mediante la autenticación integrada de Windows.

    - No hay ningún objeto de punto de conexión de servicio que señala el nombre de dominio verificado de tooyour en Azure AD en bosque de AD de Hola que pertenece el equipo de Hola a

---

### <a name="domainjoined--yes"></a>DomainJoined : YES  

Este campo muestra si el dispositivo de hello es tooan unido a Active Directory local o no. Si el valor de hello muestra como **n**, dispositivo hello no se registran automáticamente con Azure AD. Comprobar primero que toohello de combinaciones de dispositivo de hello en Active Directory local antes de que se puede registrar con Azure AD. Si desea unir el equipo tooAzure AD de hello directamente, vaya tooLearn acerca de las capacidades de Azure Active Directory Join.

---

### <a name="workplacejoined--no"></a>WorkplaceJoined : NO  

Este campo muestra si el dispositivo de hello está registrado con Azure AD, sino como un dispositivo personal (marcado como 'Unido al área de trabajo'). Si este valor debería aparecer como "NO" para un equipo unido a un dominio registrado con Azure AD, sin embargo si muestra como Sí significa que una cuenta profesional o educativa fue agregado toohello anterior equipo al completarse el registro. En este caso la cuenta de hello se omitirá si utiliza la versión de actualización de aniversario de Hola de Windows 10 (1607 cuando ejecuta el comando WinVer de hello en Hola "Run" ventana o una ventana de símbolo del sistema).

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet : YES y AzureADPrt : YES
  
Estos campos muestran que autentica correctamente ese usuario hello tooAzure AD tras iniciar sesión en el dispositivo toohello. Si muestra "NO" siguiente hello las causas posibles es:

- Clave de almacenamiento incorrecto (STK) de TPM asociado Hola dispositivo tras el registro (comprobación de Hola KeySignTest mientras se ejecuta con privilegios elevados).

- Id. de inicio de sesión alternativo

- No se ha encontrado el proxy HTTP

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información, vea hello [registro automático de dispositivos preguntas más frecuentes](active-directory-device-registration-faq.md) 
