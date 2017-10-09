---
title: aaaSetting de Azure AD Join para los usuarios | Documentos de Microsoft
description: "Explica cómo pueden configurar los administradores Azure AD Join para el directorio local y el registro de dispositivos."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 60a5aeb11292cb6057ab1065c3ab77e5981d0cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a>Configuración de Azure AD Join en su organización
Antes de configurar Azure Active Directory Join (Azure AD Join), necesita realizar la sincronización de tooeither su directorio local de la nube de los usuarios toohello una copia de seguridad o crear manualmente las cuentas administradas en Azure AD.

Instrucciones detalladas para sincronizar su tooAzure de usuarios local AD se trata en [integrar las identidades locales con Azure Active Directory](active-directory-aadconnect.md).

toomanually crear y administrar los usuarios en Azure AD, consulte demasiado[administración de usuarios en Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).

## <a name="set-up-device-registration"></a>Configuración del registro de dispositivos
1. Inicie sesión en toohello portal de Azure como administrador.
2. En el panel izquierdo de hello, seleccione **Active Directory**.
3. En hello **Directory** ficha, seleccione el directorio.
4. Seleccione hello **configurar** ficha.
5. Vaya toohello **dispositivos** sección.
6. En hello **dispositivos** pestaña, configure Hola siguiente:  
   * **MÁXIMO número de dispositivos por usuario**: seleccione Hola número máximo de dispositivos que puede tener un usuario en Azure AD.  Si un usuario alcanza esta cuota, no estarán tooadd capaz de más dispositivos hasta que se quiten uno o varios de los dispositivos existentes.
   * **REQUERIR la autenticación MULTIFACTOR tooJOIN dispositivos**: establecer si los usuarios están tooprovide necesaria una segunda autenticación factor toojoin su tooAzure dispositivo AD. Para obtener más información acerca de la autenticación multifactor de Azure, consulte [Introducción a la autenticación multifactor Azure en la nube de hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).
   * **Los usuarios pueden dispositivos de combinación de AZURE AD**: seleccione Hola usuarios y grupos que se permiten toojoin dispositivos tooAzure AD.
   * **DISPOSITIVOS Unidos a otros administradores ON AZURE AD**: con Azure AD Premium u Hola Enterprise Mobility Suite (EMS), puede escoger qué usuarios tienen derechos de administrador local toohello dispositivo. De forma predeterminada, a los administradores globales y a los propietarios de dispositivos se les conceden derechos de administrador local.

<center>![Configuración del registro de dispositivos](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png)</center>

Después de configurar Azure AD Join para los usuarios, puede conectar tooAzure AD a través de su empresa o dispositivos personales.

Continuación se muestran tres escenarios de hello puede usar tooenable su tooset a los usuarios de Azure AD Join:

* Los usuarios unir un dispositivo propiedad de la empresa directamente tooAzure AD.
* Toohello de dispositivo de una empresa de unión al dominio de los usuarios de Active Directory local y, después, ampliarla Hola dispositivo tooAzure AD.
* Los usuarios agregar trabajo o escuela cuentas tooWindows en un dispositivo personal

## <a name="additional-information"></a>Información adicional
* [Windows 10 para empresa hello: dispositivos de toouse de formas de trabajo](active-directory-azureadjoin-windows10-devices-overview.md)
* [Extender nube dispositivos de tooWindows 10 capacidades a través de Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Conozca los escenarios de uso de Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Conectar dispositivos Unidos a dominio tooAzure AD para experiencias de Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configuración de Azure AD Join](active-directory-azureadjoin-setup.md)

