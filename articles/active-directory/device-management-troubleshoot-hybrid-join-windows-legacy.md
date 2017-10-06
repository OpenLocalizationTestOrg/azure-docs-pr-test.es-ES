---
title: "aaaTroubleshooting híbrido Azure Active Directory unido a dispositivos de nivel inferior | Documentos de Microsoft"
description: "Solución de problemas de dispositivos híbridos de nivel inferior unidos a Azure Active Directory"
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
ms.openlocfilehash: edd56b89579fac6b427732902284ad9c568b87b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a>Solución de problemas de dispositivos híbridos de nivel inferior unidos a Azure Active Directory 

Este tema es aplicable toohello solo después de dispositivos: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Para Windows 10 o Windows Server 2016, consulte [Solución de problemas de dispositivos híbridos de Windows 10 y Windows Server 2016 unidos a Azure Active Directory](device-management-troubleshoot-hybrid-join-windows-current.md).

En este tema se da por supuesto que tiene [dispositivos Unidos a un híbrido configurado Azure Active Directory](device-management-hybrid-azuread-joined-devices-setup.md) hello toosupport los escenarios siguientes:

- Acceso condicional basado en dispositivos

- [Perfiles móviles de empresa](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello para empresas](active-directory-azureadjoin-passport-deployment.md) 





Este tema proporciona instrucciones sobre cómo tooresolve posibles problemas de solución de problemas.  

**Qué debería saber:** 

- número máximo de Hola de dispositivos por usuario está centrado en los dispositivos. Por ejemplo, si *jdoe* y *jharnett* dispositivo de inicio de sesión tooa, se crea un registro independiente (DeviceID) para cada uno de ellos en hello **usuario** ficha información.  

- Hola registro inicial / combinación de dispositivos es tooperform configurado un intento de inicio de sesión o bloquear / desbloquear. Podría haber un retraso de 5 minutos desencadenado por una tarea de programador de tareas. 

- Una reinstalación del sistema operativo de Hola o un manual unregister y vuelva a registrar pueden crear un nuevo registro en Azure AD y da como resultado varias entradas en la ficha de información de usuario de hello en Hola portal de Azure. 


## <a name="step-1-retrieve-hello-registration-status"></a>Paso 1: Recuperar el estado de registro de hello 

**estado de registro de hello tooverify:**  

1. Hola abrir símbolo del sistema como administrador 

2. Escriba `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`

Este comando muestra un cuadro de diálogo que le proporciona más detalles acerca del estado de unión Hola.

![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a>Paso 2: Evaluar el estado de unión de Azure AD de hello híbrida 

Si la combinación de Azure AD de hello híbrida no fue correcta, cuadro de diálogo de hello proporciona detalles sobre el problema de Hola que se ha producido.

**Hola los problemas más comunes son:**

- Una configuración incorrecta de AD FS o Azure AD

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- No está registrado como un usuario de dominio

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- Se ha alcanzado una cuota

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- Hola el servicio no responde 

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

También puede encontrar información de estado de hello en el registro de eventos de hello en **aplicaciones y servicios Log\Microsoft-unión**.
  
**Hola las causas más comunes para una combinación de Azure AD errores híbrida son:** 

- El equipo no está en la red interna de la organización de Hola o una VPN sin conexión tooan local controlador de dominio de AD.

- Se registran en el equipo de tooyour con una cuenta de equipo local. 

- Problemas de configuración de servicio: 

  - Hello servidor de federación ha sido configurado toosupport **WIAORMULTIAUTHN**. 

  - No hay ningún objeto de punto de conexión de servicio que señala el nombre de dominio verificado de tooyour en Azure AD en bosque de AD de Hola que pertenece el equipo de Hola a.

  - Un usuario ha alcanzado el límite de Hola de dispositivos. 

## <a name="next-steps"></a>Pasos siguientes

Si tiene preguntas, consulte hello [preguntas más frecuentes sobre la administración de dispositivos](device-management-faq.md)  
