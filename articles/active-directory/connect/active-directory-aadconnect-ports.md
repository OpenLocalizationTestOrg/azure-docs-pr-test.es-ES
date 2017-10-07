---
title: "La identidad híbrida requería puertos y protocolos - Azure | Microsoft Docs"
description: "Esta página es una página de referencia técnica para puertos que sean necesario toobe abierto para Azure AD Connect"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: de97b225-ae06-4afc-b2ef-a72a3643255b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 9c62b74b45e7f266e3a55baa2db07a9ff1c9c6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-identity-required-ports-and-protocols"></a>La identidad híbrida requería puertos y protocolos
Hola después de documento es una referencia técnica en hello requerido puertos y protocolos para implementar una solución de identidad híbrida. Utilice Hola después de ilustración y consulte toohello de tabla correspondiente.

![Qué es Azure AD Connect](./media/active-directory-aadconnect-ports/required3.png)

## <a name="table-1---azure-ad-connect-and-on-premises-ad"></a>Tabla 1: Azure AD Connect y AD local
Esta tabla describe Hola puertos y protocolos que son necesarios para la comunicación entre el servidor de Azure AD Connect hello y AD local.

| Protocol | Puertos | Description |
| --- | --- | --- |
| DNS |53 (TCP/UDP) |Búsquedas de DNS en el bosque de destino de Hola. |
| Kerberos |88 (TCP/UDP) |Bosque de AD toohello de autenticación de Kerberos. |
| MS-RPC |135 (TCP/UDP) |Se utiliza durante la configuración inicial del Asistente de Azure AD Connect de hello cuando enlaza toohello AD bosque de Hola y también durante la sincronización de contraseña. |
| LDAP |389 (TCP/UDP) |Se usa para la importación de datos de AD. Los datos se cifran con Kerberos Sign & Seal. |
| RPC | 445 (TCP/UDP) |Utilizando una cuenta de equipo en el bosque de AD Hola de toocreate SSO sin problemas. |
| LDAP/SSL |636 (TCP/UDP) |Se usa para la importación de datos de AD. transferencia de datos de Hello estarán firmada y cifrada. Solo se utiliza si está usando SSL. |
| RPC |49152- 65535 (Puerto RCP alto aleatorio)(TCP/UDP) |Se utiliza durante la configuración inicial de Hola de Azure AD Connect cuando enlaza toohello AD bosques y durante la sincronización de contraseña. Consulte [KB929851](https://support.microsoft.com/kb/929851), [KB832017](https://support.microsoft.com/kb/832017) y [KB224196](https://support.microsoft.com/kb/224196) para más información. |

## <a name="table-2---azure-ad-connect-and-azure-ad"></a>Tabla 2: Azure AD Connect y Azure AD
Esta tabla describen Hola puertos y protocolos que son necesarios para la comunicación entre el servidor de Azure AD Connect hello y Azure AD.

| Protocol | Puertos | Description |
| --- | --- | --- |
| HTTP |80 (TCP/UDP) |Usa certificados SSL de tooverify toodownload CRL (listas de revocación de certificados). |
| HTTPS |443 (TCP/UDP) |Toosynchronize usado con Azure AD. |

Para obtener una lista de direcciones URL e IP direcciones necesita tooopen en el firewall, vea [intervalos de direcciones IP y las direcciones URL de Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

## <a name="table-3---azure-ad-connect-and-ad-fs-federation-serverswap"></a>Tabla 3: Azure AD Connect y servidores de federación AD FS/WAP
Esta tabla describen Hola puertos y protocolos que son necesarios para la comunicación entre el servidor de Azure AD Connect de Hola y servidores de federación/WAP de AD FS.  

| Protocol | Puertos | Description |
| --- | --- | --- |
| HTTP |80 (TCP/UDP) |Usa certificados SSL de tooverify toodownload CRL (listas de revocación de certificados). |
| HTTPS |443 (TCP/UDP) |Toosynchronize usado con Azure AD. |
| WinRM |5985 |Agente de escucha de WinRM |

## <a name="table-4---wap-and-federation-servers"></a>Tabla 4: Servidores de federación y WAP
Esta tabla describen Hola puertos y protocolos que son necesarios para la comunicación entre servidores de federación de Hola y los servidores WAP.

| Protocol | Puertos | Description |
| --- | --- | --- |
| HTTPS |443 (TCP/UDP) |Se usa para autenticación. |

## <a name="table-5---wap-and-users"></a>Tabla 5 - WAP y usuarios
Esta tabla describen Hola puertos y protocolos que son necesarios para la comunicación entre los usuarios y los servidores WAP Hola.

| Protocol | Puertos | Description |
| --- | --- | --- |
| HTTPS |443 (TCP/UDP) |Se usa para la autenticación de dispositivos. |
| TCP |49443 (TCP) |Se usa para la autenticación de certificados. |

## <a name="table-6a--6b---pass-through-authentication-with-single-sign-on-sso-and-password-hash-sync-with-single-sign-on-sso"></a>Tabla 6a y 6b: autenticación de paso a través con inicio de sesión único (SSO) y sincronización de Hash de contraseña con inicio de sesión único (SSO)
Hola las tablas siguientes describe Hola puertos y protocolos que son necesarios para la comunicación entre hello Azure AD Connect y Azure AD.

### <a name="table-6a---pass-through-authentication-with-sso"></a>Tabla 6a: autenticación de paso a través con SSO
|Protocol|Número de puerto|Descripción
| --- | --- | ---
|HTTP|80|Habilita el tráfico HTTP saliente para la validación de seguridad, como SSL. También sea necesario para el conector de Hola de actualización automática capacidad toofunction correctamente.
|HTTPS|443| Habilitar el tráfico HTTPS saliente para operaciones como habilitar y deshabilitar la característica de hello, registrar conectores, descarga las actualizaciones de conector y controlar todas las solicitudes de inicio de sesión de usuario.

Además, Azure AD Connect debe toobe toomake capaz de direct IP conexiones toohello [intervalos IP del centro de datos de Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653).

### <a name="table-6b---password-hash-sync-with-sso"></a>Tabla 6b: sincronización de Hash de contraseña con SSO

|Protocol|Número de puerto|Descripción
| --- | --- | ---
|HTTPS|443| Habilite el registro SSO (sólo es necesario para hello proceso de registro SSO).

Además, Azure AD Connect debe toobe toomake capaz de direct IP conexiones toohello [intervalos IP del centro de datos de Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653). Una vez más, esto solo es necesario para el proceso de registro de hello SSO.

## <a name="table-7a--7b---azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>Tabla 7a y 7b: Agente de Azure AD Connect Health para (AD FS/sincronización) y Azure AD
Hello en las tablas siguientes se describen los puntos de conexión de hello, puertos y protocolos que son necesarios para la comunicación entre agentes de mantenimiento de Azure AD Connect y Azure AD

### <a name="table-7a---ports-and-protocols-for-azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>Tabla 7a: Puertos y protocolos para el agente de Azure AD Connect Health para (AD FS/sincronización) y Azure AD
Esta tabla describen Hola siguiendo los puertos de salida y los protocolos que son necesarios para la comunicación entre agentes de hello Azure AD Connect Health y Azure AD.  

| Protocol | Puertos | Description |
| --- | --- | --- |
| HTTPS |443 (TCP/UDP) |Salida |
| Azure Service Bus |5671 (TCP/UDP) |Salida |

### <a name="7b---endpoints-for-azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>7b: Puntos de conexión para el agente de Azure AD Connect Health para (AD FS/sincronización) y Azure AD
Para obtener una lista de puntos de conexión, consulte [Hola sección de requisitos para el agente de hello Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-agent-install.md#requirements).

