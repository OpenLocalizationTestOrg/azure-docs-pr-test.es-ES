---
title: "aaaWindows autenticación y el servidor de MFA de Azure | Documentos de Microsoft"
description: "Se trata de una página de autenticación multifactor de Azure de Hola que te ayudará a implementar la autenticación de Windows y el servidor de autenticación multifactor de Azure."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a>Servidor de Autenticación de Windows y Azure Multi-Factor Authentication
Utilice sección de autenticación de Windows hello de hello tooenable de servidor de autenticación multifactor de Azure y configurar la autenticación de Windows para las aplicaciones. Antes de configurar la autenticación de Windows, tenga Hola lista en la cuenta siguiente:

* Después de la instalación, reinicie hello Azure la autenticación multifactor para el efecto de tootake de servicios de Terminal Server.
* Si se comprueba 'Coincidencia de usuario requieren la autenticación multifactor Azure' y no está en la lista de usuarios de hello, no será capaz de toolog en la máquina de hello después del reinicio.
* Direcciones IP depende de si aplicación hello puede proporcionar la dirección IP del cliente con la autenticación de Hola Hola de confianza. Actualmente solo se admite Terminal Services.  

> [!NOTE]
> Esta característica no está admitida toosecure Terminal Services en Windows Server 2012 R2.

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a>toosecure una aplicación con la autenticación de Windows, siguiendo el procedimiento de Hola de uso.
1. Haga clic en icono de autenticación de Windows hello Hola servidor Azure Multi-factor Authentication.
   ![Autenticación de Windows](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)
2. Comprobar hello **habilitar la autenticación de Windows** casilla de verificación. De forma predeterminada, esta casilla está desmarcada.
3. pestaña de aplicaciones de Hello permite Hola administrador tooconfigure una o más aplicaciones para la autenticación de Windows.
4. Seleccione un servidor o una aplicación: especifique si el servidor o la aplicación hello está habilitada. Haga clic en **Aceptar**.
5. Haga clic en **Agregar...**
6. pestaña de IP de confianza de Hello permite tooskip Azure Multi-factor Authentication para sesiones de Windows que se originan de direcciones IP específicas. Por ejemplo, si los empleados usan la aplicación hello desde office hello y desde casa, puede decidir que no desea que sus teléfonos suenen para Azure Multi-factor Authentication mientras se encuentran en office Hola. Para ello, especificaría subred de la oficina de hello como entrada de IP de confianza.
7. Haga clic en **Agregar...**
8. Seleccione **IP única** si desea que tooskip una única dirección IP.
9. Seleccione **intervalo de IP** si desea que tooskip todo un intervalo de IP. Ejemplo 10.63.193.1-10.63.193.100.
10. Seleccione **subred** si desea que toospecify un intervalo de direcciones IP mediante la notación de subred. Escriba Hola dirección IP inicial y seleccione Hola máscara de red adecuada de la lista desplegable de Hola.
11. Haga clic en **Aceptar**.

## <a name="next-steps"></a>Pasos siguientes

- [Configuración de dispositivos de VPN de terceros para el servidor Azure MFA](multi-factor-authentication-advanced-vpn-configurations.md)

- [Aumentar la infraestructura de autenticación existente con hello extensión NPS para Azure MFA](multi-factor-authentication-nps-extension.md)
