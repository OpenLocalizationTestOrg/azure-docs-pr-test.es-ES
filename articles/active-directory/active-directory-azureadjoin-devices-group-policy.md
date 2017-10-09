---
title: experimenta aaaConnect dispositivos Unidos a dominio tooAzure AD para Windows 10 | Documentos de Microsoft
description: "Explica cómo los administradores pueden configurar la red de empresa de directiva de grupo tooenable dispositivos toobe toohello Unidos a un dominio."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a>Conectar dispositivos Unidos a dominio tooAzure AD para experiencias de Windows 10
Unión a un dominio es organizaciones de forma tradicional de hello han conectado dispositivos para el trabajo de hello en los últimos 15 años y mucho más. Ha habilitado toosign de usuarios en los dispositivos tootheir mediante el uso de su trabajo de Windows Server Active Directory (Active Directory) o escolares y permitido toofully de TI administran estos dispositivos. Las organizaciones suelen basarse en métodos tooprovision dispositivos toousers de creación de imágenes y generalmente se utiliza System Center Configuration Manager (SCCM) o directiva de grupo toomanage ellos.


Unión a un dominio de Windows 10 proporciona Hola después ventajas después de conectar dispositivos tooAzure Active Directory (Azure AD):

* Inicio de sesión (SSO) tooAzure AD recursos individuales desde cualquier lugar
* Obtener acceso a enterprise toohello tienda Windows mediante el uso de trabajo o escuela cuentas (no requerida ninguna cuenta de Microsoft)
* Movilidad de las configuraciones de usuario conforme a la empresa entre dispositivos que usan cuentas profesionales o educativas (sin necesidad de una cuenta Microsoft)
* Autenticación segura y práctico inicio de sesión para cuentas profesionales o educativas con Windows Hello para empresas y Windows Hello
* Capacidad toorestrict acceso solo toodevices que cumplen con la configuración de directiva de grupo de organización de dispositivo

## <a name="prerequisites"></a>Requisitos previos
Unión a un dominio continúa toobe útil. Sin embargo, los beneficios de hello Azure AD tooget de SSO, itinerancia de configuración con o cuentas, educativas y tener acceso a almacén tooWindows con trabajo cuentas profesionales o educativas, necesitará Hola siguientes:

* Suscripción de Azure AD
* Azure AD Connect tooextend hello tooAzure directory AD local
* Directiva que ha establecido tooconnect dispositivos Unidos a dominio tooAzure AD
* Compilación de Windows 10 (compilación 10551 o posterior) en los dispositivos.

tooenable Windows Hello para empresas y Windows Hello, también necesitará siguiente hello:

- **Infraestructura de clave pública (PKI)** para la emisión de certificados de usuario.

- **Rama actual de System Center Configuration Manager** -necesita tooinstall versión 1606 o superior.  
Para más información, consulte: 
    - [Documentación de System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx)
    - [Blog del equipo de System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [Configuración de Windows Hello para empresas en System Center Configuration Manager](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

Como un requisito de implementación de PKI toohello alternativo, puede hacer siguiente hello:

* Tener algunos controladores de dominio con los Servicios de dominio de Active Directory para Windows Server 2016.

tooenable acceso condicional, puede crear configuraciones de directiva de grupo que permitir que los dispositivos Unidos a un toodomain de acceso con sin implementaciones adicionales. toomanage control de acceso basado en cumplimiento de dispositivo de hello, necesitará la siguiente hello:

* Rama actual de System Center Configuration Manager (1606 o posterior) para escenarios de Windows Hello para empresas

## <a name="deployment-instructions"></a>Instrucciones de implementación

toodeploy, siga los pasos de hello enumerados en [cómo tooconfigure el registro automático de Windows Unidos a dominios dispositivos con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="next-step"></a>Paso siguiente
* [Windows 10 para empresa hello: dispositivos de toouse de formas de trabajo](active-directory-azureadjoin-windows10-devices-overview.md)
* [Extender nube dispositivos de tooWindows 10 capacidades a través de Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Conozca los escenarios de uso de Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Conectar dispositivos Unidos a dominio tooAzure AD para experiencias de Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configuración de Azure AD Join](active-directory-azureadjoin-setup.md)

