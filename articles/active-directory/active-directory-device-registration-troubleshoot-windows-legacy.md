---
title: "aaaTroubleshooting Hola el registro automático de dominio de Azure AD los equipos Unidos para clientes de nivel inferior de Windows | Documentos de Microsoft"
description: "Solución de problemas de registro automático de Hola de dominio de Azure AD los equipos Unidos para clientes de nivel inferior de Windows."
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
ms.openlocfilehash: 84fe666576f13de09d1eaa5692517d45a4dbeebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a>Solución de problemas de registro automático de dominio unido equipos tooAzure AD para clientes de nivel inferior de Windows 

Este tema es aplicable toohello solo después de los clientes: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Para Windows 10 o Windows Server 2016, consulte [solución de problemas de registro automático de dominio unido equipos tooAzure AD – Windows 10 y Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).

En este tema se da por supuesto que ha configurado el registro automático de dispositivos Unidos a un dominio como se ha descrito en se describe en [cómo tooconfigure el registro automático de Windows Unidos a dominios dispositivos con Azure Active Directory](active-directory-device-registration-get-started.md).
 
Este tema proporciona instrucciones sobre cómo tooresolve posibles problemas de solución de problemas.  
Algunos toonote cosas para resultados correcta: 

- El registro de estos clientes en Azure AD se realiza por usuario/dispositivo. Por ejemplo: si jdoe y jharnett iniciado sesión en el dispositivo toothis, se crea un registro independiente (DeviceID) para cada uno de estos usuarios en la ficha de información de usuario de Hola.  

- Es el registro de estos clientes fuera del cuadro de hello tootry configurado en el inicio de sesión o bloquear/desbloquear y podría haber un retraso de 5 minutos que esto se desencadena mediante una tarea de programador de tareas. 

- Una nueva instalación de sistema operativo de Hola o anular el registro manual y volver a registrar, puede crear un nuevo registro en Azure AD y dará como resultado varias entradas en la ficha de información de usuario de Hola Hola portal de Azure. 


## <a name="step-1-retrieve-hello-registration-status"></a>Paso 1: Recuperar el estado de registro de hello 

**estado de registro de hello tooverify:**  

1. Hola abrir símbolo del sistema como administrador 

2. Escriba `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`

Este comando muestra un cuadro de diálogo que le proporciona más detalles acerca del estado de unión Hola.

![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a>Paso 2: Evaluar el estado de registro de hello 

Si la combinación de hello no fue correcta, cuadro de diálogo de Hola proporciona detalles sobre el problema de Hola que se ha producido.

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
  
**Hola las causas más comunes para un registro de errores son:** 

- El equipo no está en la red interna de la organización de Hola o una VPN sin conexión tooan local controlador de dominio de AD.

- Se registran en el equipo de tooyour con una cuenta de equipo local. 

- Problemas de configuración de servicio: 

  - Hello servidor de federación ha sido configurado toosupport **WIAORMULTIAUTHN**. 

  - No hay ningún objeto de punto de conexión de servicio que señala el nombre de dominio verificado de tooyour en Azure AD en bosque de AD de Hola que pertenece el equipo de Hola a.

  - Un usuario ha alcanzado el límite de Hola de dispositivos. Consulte Introducción al Registro de dispositivos de Azure Active Directory.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información, vea hello [registro automático de dispositivos preguntas más frecuentes](active-directory-device-registration-faq.md) 
