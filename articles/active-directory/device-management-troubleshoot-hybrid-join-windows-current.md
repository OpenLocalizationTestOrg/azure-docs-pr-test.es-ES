---
title: "aaaTroubleshooting híbrido Azure Active Directory unido a dispositivos Windows 10 y Windows Server 2016 | Documentos de Microsoft"
description: "Solución de problemas de dispositivos híbridos de Windows 10 y Windows Server 2016 unidos a Azure Active Directory"
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc252d1d0684d6632694afc8a367327794228c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a>Solución de problemas de dispositivos híbridos de Windows 10 y Windows Server 2016 unidos a Azure Active Directory 

Este tema es aplicable toohello después de los clientes:

-   Windows 10
-   Windows Server 2016

Para otros clientes Windows, consulte [Solución de problemas de dispositivos híbridos de nivel inferior unidos a Azure Active Directory](device-management-troubleshoot-hybrid-join-windows-legacy.md).

En este tema se da por supuesto que tiene [dispositivos Unidos a un híbrido configurado Azure Active Directory](device-management-hybrid-azuread-joined-devices-setup.md) hello toosupport los escenarios siguientes:

- Acceso condicional basado en dispositivos

- [Perfiles móviles de empresa](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello para empresas](active-directory-azureadjoin-passport-deployment.md)


Este documento proporciona instrucciones para solucionar problemas sobre cómo tooresolve posibles problemas. 


Actualizar de 10 de noviembre de 2015 para Windows 10 y Windows Server 2016, híbrida Hola de admite la combinación de Azure Active Directory Windows y versiones posteriores. Se recomienda usar la actualización de aniversario de Hola.

## <a name="step-1-retrieve-hello-join-status"></a>Paso 1: Recuperar el estado de combinación de Hola 

**estado de combinación de Hola tooretrieve:**

1. Hola abrir símbolo del sistema como administrador

2. Escriba **dsregcmd /status**



    +----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+
    
        AzureAdJoined: YES
     EnterpriseJoined: Ningún Id. de dispositivo: huella digital de 5820fbe9-60c8-43b0-bb11-44aee233e4e7: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected de proveedor de cifrado de la plataforma de Microsoft: Sí KeySignTest:: debe ejecutar con permisos elevados tootest.
                  Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO
    
    +----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES



## <a name="step-2-evaluate-hello-join-status"></a>Paso 2: Evaluar el estado de combinación de Hola 

Revise Hola después de campos y asegúrese de que tienen valores de hello esperados:

### <a name="azureadjoined--yes"></a>AzureAdJoined : YES  

Este campo indica si el dispositivo de Hola se une con Azure AD. Si el valor de hello es **n**, Hola tooAzure combinación AD no se ha completado todavía. 

**Causas posibles:**

- Error de autenticación del equipo de hello para la combinación.

- Hay un proxy HTTP en la organización de Hola que no se puede detectar por equipo Hola

- Hola equipo no puede comunicarse con tooauthenticate de Azure AD o Azure DRS para el registro

- Hello equipo no esté en la red interna de la organización de Hola o en VPN con la línea de visión directa tooan controlador de dominio de AD local.

- Si el equipo de hello tiene un TPM, puede estar en mal estado.

- Puede haber un error de configuración en servicios de hello indicados en el documento de Hola que necesitará tooverify nuevo. Los ejemplos comunes son:

    - El servidor de federación no tiene habilitados los puntos de conexión de WS-Trust.

    - Es posible que el servidor de federación no permita la autenticación de entrada de equipos de la red mediante la autenticación integrada de Windows.

    - No hay ningún objeto de punto de conexión de servicio que señala el nombre de dominio verificado de tooyour en Azure AD en bosque de AD de Hola que pertenece el equipo de Hola a

---

### <a name="domainjoined--yes"></a>DomainJoined : YES  

Este campo indica si se une el dispositivo de hello tooan en Active Directory local o no. Si el valor de hello es **n**, dispositivo hello no puede realizar una combinación de híbrida Azure AD.  

---

### <a name="workplacejoined--no"></a>WorkplaceJoined : NO  

Este campo indica si el dispositivo de hello está registrado con Azure AD como un dispositivo personal (marcados como *al área de trabajo*). Este valor debe ser **NO** para un equipo unido a un dominio que esté también unido a Azure AD híbrido. Si el valor de hello es **Sí**, una cuenta profesional o educativa agregó finalización toohello anterior de combinación de hello híbrida Azure AD. En este caso, la cuenta de hello se omite cuando se usa la versión de actualización de aniversario de Hola de Windows 10 (1607).

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet : YES y AzureADPrt : YES
  
Estos campos indican si el usuario de hello autenticó correctamente tooAzure AD cuando inicien sesión en el dispositivo toohello. Si hay valores de hello **n**, podría ser debido:

- Clave de almacenamiento incorrecto (STK) de TPM asociado Hola dispositivo tras el registro (comprobación de Hola KeySignTest mientras se ejecuta con privilegios elevados).

- Id. de inicio de sesión alternativo

- No se ha encontrado el proxy HTTP

## <a name="next-steps"></a>Pasos siguientes

Si tiene preguntas, consulte hello [preguntas más frecuentes sobre la administración de dispositivos](device-management-faq.md) 
