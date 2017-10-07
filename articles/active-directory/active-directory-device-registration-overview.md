---
title: "información general sobre el registro de dispositivo Active Directory aaaAzure | Documentos de Microsoft"
description: "Registro de dispositivos de Azure Active Directory es la base de Hola para escenarios de acceso condicional basado en el dispositivo. Cuando se registra un dispositivo, las disposiciones de registro de dispositivo de Azure Active Directory Hola dispositivo con una identidad que es el dispositivo de hello tooauthenticate usado cuando Hola usuario inicia sesión."
services: active-directory
keywords: registro de dispositivos, habilitar registro de dispositivos, registro de dispositivos y MDM
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 1e92c1a2-01b8-4225-950b-373cd601b035
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: b9846e34fe873d271ebe71cbf8e70c6b4768885b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>Introducción al Registro de dispositivos de Azure Active Directory
Registro de dispositivos de Azure Active Directory es la base de Hola para escenarios de acceso condicional basado en el dispositivo. Cuando se registra un dispositivo, el registro de dispositivos de Azure Active Directory proporciona dispositivo Hola con una identidad que es el dispositivo de hello tooauthenticate usado cuando Hola usuario inicia sesión. dispositivo de Hello autenticado y los atributos de hello de dispositivo de hello, se pueden tooenforce usa directivas de acceso condicional para las aplicaciones que se hospedan en la nube de Hola y local.

Cuando se combina con una solución de management(MDM) de dispositivos móviles como Microsoft Intune, los atributos de dispositivo de hello en Azure Active Directory se actualizan con información adicional sobre el dispositivo de Hola. Esto permite que las reglas de acceso condicional de toocreate que exijan el acceso desde dispositivos toomeet los estándares de seguridad y cumplimiento de normas. Para más información sobre la inscripción de dispositivos de Microsoft Intune, consulte el artículo sobre cómo [inscribir dispositivos para su administración en Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).

## <a name="scenarios-enabled-by-azure-active-directory-device-registration"></a>Escenarios que habilita el registro de dispositivos de Azure Active Directory
El registro de dispositivos de Azure Active Directory incluye compatibilidad con dispositivos iOS, Android y Windows. escenarios de individuales de Hola que utilizan el registro de dispositivos de Azure AD pueden tener compatibilidad con la plataforma y requisitos más específicos. Estos escenarios son los siguientes:

* **Tooapplications de acceso condicional que están hospedados en local**: puede utilizar dispositivos registrados con directivas de acceso para las aplicaciones que están configuradas toouse AD FS con Windows Server 2012 R2. Para obtener más información sobre cómo configurar el acceso condicional localmente, consulte [Configuración del acceso condicional local mediante el registro de dispositivos de Azure Active Directory](active-directory-device-registration-on-premises-setup.md).
* **Acceso condicional para aplicaciones de Office 365 con Microsoft Intune** : los administradores de TI pueden aprovisionar acceso condicional dispositivo directivas toosecure los recursos corporativos, mientras que en hello mismo tiempo permitir que los trabajadores de información en dispositivos compatibles Servicios de hello tooaccess. Para obtener más información, vea [Directivas de dispositivos de acceso condicional para servicios de Office 365](active-directory-conditional-access-device-policies.md).

## <a name="setting-up-azure-active-directory-device-registration"></a>Configuración del registro de dispositivos de Azure Active Directory
Tendrá que tooenable el registro de dispositivos de Azure AD en hello Portal de Azure para que los dispositivos móviles puedan detectar el servicio de hello buscando registros DNS conocidos. Debe configurar DNS de su empresa para que pueden detectar y usar el servicio de hello dispositivos Windows 10, Windows 8.1, Windows 7, iOS y Android.
Puede ver y habilitar o deshabilitar dispositivos registrados con hello Portal del administrador en Azure Active Directory.

> [!NOTE]
> Para obtener instrucciones más recientes sobre cómo ver tooset el registro automático de dispositivos, [cómo toosetup el registro automático de dominio de Windows Unidos a dispositivos con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).
> 
> 

### <a name="enable-azure-active-directory-device-registration-service"></a>Habilitación del servicio de registro de dispositivos de Azure Active Directory
1. Inicie sesión en toohello portal de Microsoft Azure como administrador.
2. En el panel izquierdo de hello, seleccione **Active Directory**.
3. En hello **Directory** ficha, seleccione el directorio.
4. Seleccione hello **configurar** ficha.
5. Desplácese sección toohello denominada **dispositivos**.
6. Seleccione **TODOS** en **LOS USUARIOS PUEDEN UNIR DISPOSITIVOS AL ÁREA DE TRABAJO**.
7. Seleccione el número máximo de Hola de dispositivos que desee tooauthorize por usuario.

> [!NOTE]
> La inscripción en Microsoft Intune o Administración de dispositivos móviles para Office 365 requiere la unión al área de trabajo. Si ha configurado alguno de estos servicios, se selecciona todos y Hola NONE botón está deshabilitado.
> 
> 

De forma predeterminada, la autenticación en dos fases no está habilitada para el servicio de Hola. Aunque se recomienda usar la autenticación en dos fases al registrar un dispositivo.

* Antes de requerir la autenticación en dos fases para este servicio, debe configurar un proveedor de autenticación en dos fases en Azure Active Directory y configurar las cuentas de usuario para la autenticación multifactor, consulte [agregar Multi-factor Authentication Autenticación tooAzure Active Directory](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* Si utiliza AD FS con Windows Server 2012 R2, debe configurar un módulo de autenticación en dos fases en AD FS. Para ello consulte [Utilización de Multi-Factor Authentication con Servicios de federación de Active Directory](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="configure-azure-active-directory-device-registration-discovery"></a>Configuración de la detección del registro de dispositivos de Azure Active Directory
Dispositivos Windows 7 y Windows 8.1 detectarán el servicio de registro de dispositivos de hello mediante la combinación de nombre de cuenta de usuario de hello con un nombre de servidor de registro de dispositivo conocido.

Debe crear un registro DNS CNAME que señala el registro de toohello A asociado con el servicio de registro de dispositivo de Azure Active Directory. Hola registro CNAME debe usar enterpriseregistration de prefijo conocido Hola seguido por el sufijo UPN de hello usado por las cuentas de usuario de hello en su organización. Si su organización usa varios sufijos UPN, deben crearse varios registros CNAME en DNS.

Por ejemplo, si usa dos sufijos UPN en la organización llamada @contoso.com y @region.contoso.com, creará Hola siguientes registros de DNS.

| Entrada | Tipo | Dirección |
| --- | --- | --- |
| enterpriseregistration.contoso.com |CNAME |enterpriseregistration.windows.net |
| enterpriseregistration.region.contoso.com |CNAME |enterpriseregistration.windows.net |

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>Visualización y administración de objetos de dispositivo en Azure Active Directory
1. Desde el portal de administración de Azure de hello, puede ver, bloquear y desbloquear dispositivos. Un dispositivo bloqueado dejará de tener acceso tooapplications que están configurados tooallow solo los dispositivos registrados.
2. Inicie sesión en toohello Portal de Microsoft Azure como administrador.
3. En el panel izquierdo de hello, seleccione **Active Directory**.
4. Seleccione el directorio.
5. Seleccione hello **usuarios** ficha. A continuación, seleccione un usuario tooview sus dispositivos
6. Seleccione hello **dispositivos** ficha.
7. Seleccione **dispositivos registrados** de hello menú desplegable.
8. Aquí puede ver, bloquear o desbloquear usuarios Hola los dispositivos registrados.

## <a name="additional-topics"></a>Otros temas
Puede registrar los dispositivos unidos a un dominio de Windows 7 y Windows 8.1 con el registro de dispositivos de Azure AD. Hola temas siguientes proporciona más información sobre requisitos previos de Hola y el registro de dispositivos de tooconfigure requiere pasos hello en dispositivos con Windows 7 y Windows 8.1.

* [Registro automático de dispositivos en Azure Active Directory para dispositivos Windows unidos a un dominio](active-directory-conditional-access-automatic-device-registration.md)
* [Registro automático de dispositivos en Azure Active Directory para dispositivos Windows 10 unidos a un dominio](active-directory-azureadjoin-devices-group-policy.md)

