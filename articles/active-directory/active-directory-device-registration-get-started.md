---
title: "aaaHow tooconfigure el registro automático de dispositivos Unidos a un dominio de Windows con Azure Active Directory | Documentos de Microsoft"
description: "Configurar los dispositivos de Windows Unidos a un dominio, tooregister automática y silenciosa con Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 1d736eba734418231f12e23a8fc1a93405f129c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>Introducción al Registro de dispositivos de Azure Active Directory

Registro de dispositivos de Azure Active Directory es la base de Hola para escenarios de acceso condicional basado en el dispositivo. Cuando se registra un dispositivo, el registro de dispositivos de Azure Active Directory proporciona dispositivo Hola con una identidad que es el dispositivo de hello tooauthenticate usado cuando Hola usuario inicia sesión. dispositivo de Hello autenticado y los atributos de hello de dispositivo de hello, se pueden tooenforce usa directivas de acceso condicional para las aplicaciones que se hospedan en la nube de Hola y local.

Cuando se combina con una solución de management(MDM) de dispositivos móviles como Microsoft Intune, los atributos de dispositivo de hello en Azure Active Directory se actualizan con información adicional sobre el dispositivo de Hola. Esto permite que las reglas de acceso condicional de toocreate que exijan el acceso desde dispositivos toomeet los estándares de seguridad y cumplimiento de normas. Para obtener más información sobre la inscripción de dispositivos de Microsoft Intune, consulte el artículo sobre cómo inscribir dispositivos para su administración en Intune.
Entre los escenarios que posibilita el Registro de dispositivos de Azure Active Directory se encuentra la compatibilidad con dispositivos Windows, iOS y Android. escenarios de individuales de Hola que utilizan el registro de dispositivos de Azure AD pueden tener compatibilidad con la plataforma y requisitos más específicos. 

Estos escenarios son los siguientes:

- **Acceso condicional para aplicaciones de Office 365 con Microsoft Intune:** administradores de TI pueden aprovisionar acceso condicional dispositivo directivas toosecure los recursos corporativos, mientras que en hello mismo tiempo permitir que los trabajadores de información en dispositivos compatibles Servicios de hello tooaccess. Para más información, consulte las directivas de dispositivo de acceso condicional para los servicios de Office 365.

- **Tooapplications de acceso condicional que están hospedados en local:** puede utilizar dispositivos registrados con directivas de acceso para las aplicaciones que están configuradas toouse AD FS con Windows Server 2012 R2. Para obtener más información sobre cómo configurar el acceso condicional localmente, consulte [Configuración del acceso condicional local mediante el registro de dispositivos de Azure Active Directory](active-directory-device-registration-on-premises-setup.md).

## <a name="setting-up-azure-active-directory-device-registration"></a>Configuración del Registro de dispositivos de Azure Active Directory

registro de dispositivos de toosetup, tiene varias opciones:

- Pueden registrar dispositivos cuando AD de tooAzure Unidos a un dominio. Para obtener más información acerca de este tema, se puede obtener más información sobre la configuración de Azure AD Join y Hola necesaria para los usuarios de dominio toojoin Azure AD.

- Cuando los usuarios agregar trabajo o escuela cuentas tooWindows en un dispositivo personal o cuando los dispositivos móviles conectan tooa los recursos de trabajo que requieren el registro, se pueden registrar dispositivos. tooensure esto, debe habilitar el registro de dispositivos de Azure AD en hello Portal de Azure. 

- Los dispositivos se pueden registrar con el registro automático de dispositivos en máquinas tradicionales unidas un dominio. tooensure esto, debe primero el programa de instalación de Azure AD Connect antes de continuar con el registro automático de dispositivos.

Para obtener instrucciones más recientes, consulte [cómo tooconfigure el registro automático de Windows Unidos a dominios dispositivos con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).  
También puede revisar y habilitar o deshabilitar dispositivos registrados con hello Portal del administrador en Azure Active Directory.

## <a name="enable-hello-azure-active-directory-device-registration-service"></a>Habilitar el servicio de registro de dispositivos de Azure Active Directory Hola

**Hola tooenable servicio de registro de dispositivo de Azure Active Directory:**

1.  Inicie sesión en toohello portal de Microsoft Azure como administrador.

2.  En el panel izquierdo de hello, seleccione **Active Directory**.

3.  En la ficha directorio de hello, seleccione el directorio.

4.  Haga clic en **Configurar**.

5.  Desplácese demasiado**dispositivos**.

6.  Seleccione TODO en LOS USUARIOS PUEDEN REGISTRAR SUS DISPOSITIVOS CON AZURE AD.

7.  Seleccione el número máximo de Hola de dispositivos que desee tooauthorize por usuario.

inscripción de Hello con Microsoft Intune o administración de dispositivos móviles para Office 365 requiere el registro del dispositivo. Si configuró alguno de estos servicios, se seleccionará **TODOS** y se deshabilitará el botón **NINGUNO**. Asegúrese de que estén configurados correctamente y que tiene licencias adecuadas de Hola.

De forma predeterminada, la autenticación en dos fases no está habilitada para el servicio de Hola. Aunque se recomienda usar la autenticación en dos fases al registrar un dispositivo.

- Antes de requerir la autenticación en dos fases para este servicio, debe configurar un proveedor de autenticación en dos fases en Azure Active Directory y configurar las cuentas de usuario para la autenticación multifactor, consulte Agregar la autenticación multifactor tooAzure Active Directory

- Si utiliza AD FS con Windows Server 2012 R2, debe configurar un módulo de autenticación en dos fases en AD FS. Para ello consulte Utilización de Multi-Factor Authentication con Servicios de federación de Active Directory.

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>Visualización y administración de objetos de dispositivo en Azure Active Directory

Desde el portal de administración de Azure de hello, puede ver, bloquear y desbloquear dispositivos. Un dispositivo bloqueado dejará de tener acceso tooapplications que están configurados tooallow solo los dispositivos registrados.

**tooview y administrar objetos de dispositivo en Azure Active Directory:**
 
1.  Inicie sesión en toohello portal de Microsoft Azure como administrador.

2.  En el panel izquierdo de hello, seleccione **Active Directory**.

3.  Seleccione el directorio.

4.  Seleccione **Usuarios**. 

5.  Haga clic en usuario de hello para el que desea que los dispositivos de hello toosee.

6.  Seleccione **Dispositivos**.

7.  Seleccione **Dispositivos registrados**.

Ahora, puede revisar, bloquear o desbloquear dispositivos registrados del usuario de Hola.
Dispositivos de Windows 10 que están unidos a un dominio y se registren automáticamente en las instalaciones no aparecen en la ficha de usuarios de Hola. Use toofind de comandos de PowerShell Get-MsolDevice Hola todos los dispositivos de su empresa. 


## <a name="next-steps"></a>Pasos siguientes

toosetup automatizada registro de dispositivos, consulte [cómo tooconfigure el registro automático de Windows Unidos a dominios dispositivos con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).


