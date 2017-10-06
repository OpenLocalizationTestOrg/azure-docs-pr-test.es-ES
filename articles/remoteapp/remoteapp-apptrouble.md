---
title: "aaaAzure solución de problemas de conexión de RemoteApp - errores de inicio y conexión de la aplicación | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tootroubleshoot emite con iniciar y conectarse tooapplications en Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e5cf7171-d1c2-4053-a38b-5af7821305e1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e51d480c9d3fa1f2076f95b63c7a8cd2f6956a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a>Solución de problemas de Azure RemoteApp: errores de inicio y conexión de la aplicación
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Las aplicaciones hospedadas en Azure RemoteApp pueden fallar toolaunch por diferentes motivos. Este artículo describen varias razones y mensajes de error a los usuarios podrían recibir al intentar toolaunch aplicaciones. También se incluyen los errores de conexión. (Pero en este artículo no se describen los problemas al iniciar sesión en el cliente de Azure RemoteApp hello).  

Siga leyendo para obtener información acerca de los mensajes de error comunes debido a errores de inicio y conexión tooapp.

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a>Estamos realizando la configuración... Inténtelo de nuevo en 10 minutos.
Este error significa que Azure RemoteApp está reduciendo la necesidad de capacidad de hello toomeet de los usuarios. En segundo plano de hello más instancias de máquina virtual de RemoteApp de Azure se están creando las necesidades de capacidad de los usuarios toohandle Hola. Normalmente, esto tarda aproximadamente cinco minutos pero puede tardar hasta too10 minutos. En ocasiones, no se produce lo suficientemente rápido y se necesitan recursos inmediatamente. Por ejemplo, un escenario de 9 AM donde muchos usuarios necesitan toouse su aplicación en Azure RemoteAppn en hello mismo tiempo. Si esto ocurre tooyou podemos habilitar **modo capacidad** en hello back-end. toodo este abra una incidencia de soporte técnico de Azure. Ser cierta tooinclude su identificador de suscripción en la solicitud de saludo.  

![Estamos realizando la configuración](./media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-tooyour-applications-please-re-launch-your-application"></a>Podría no la reconexión automática tooyour aplicaciones, por favor, vuelva a iniciar la aplicación
Este mensaje de error a menudo se ve si usara RemoteApp de Azure y, a continuación, coloque su toosleep PC más de 4 horas y, a continuación, reactivó su PC y hello Azure RemoteApp cliente intento tooauto volver a conectarse y se ha superado el tiempo de espera.  Indicar a los usuarios toonavigate toohello atrás aplicación e intente tooopen desde el cliente de Azure RemoteApp Hola.

![Podría no la reconexión automática tooyour aplicaciones](./media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-hello-temp-profile"></a>Problemas con el perfil temporal Hola
Este error se produce cuando el perfil de usuario (disco de perfil de usuario) no pudo toomount y usuario Hola recibe un perfil temporal.  Los administradores deben navegar por colección toohello Hola portal de Azure y, a continuación, vaya toohello **sesiones** pestaña e intente demasiado**cerrar sesión** usuario Hola. Esto fuerza un registro completo fuera de sesión de usuario de hello - a continuación tiene una aplicación Hola usuario intento toolaunch nuevo. Si se produce un error, póngase en contacto con el soporte técnico de Azure.

## <a name="azure-remoteapp-has-stopped-working"></a>Azure RemoteApp ha dejado de funcionar
Este mensaje de error significa cliente de Azure RemoteApp hello tiene un problema y necesita toobe reiniciar. Indicar a los usuarios tooclose: seleccione **cerrar programa** y, a continuación, vuelva a iniciar el cliente de Azure RemoteApp Hola.  Si el problema de hello sigue abierto e incidencia de soporte técnico de Azure.

![Azure RemoteApp ha dejado de funcionar](./media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-hello-connection-or-contact-your-system-administrator"></a>Se produjo un error mientras Conexión a Escritorio remoto trataba de obtener acceso a este recurso. Vuelva a intentar la conexión de Hola o póngase en contacto con el administrador del sistema
Se trata de un mensaje de error genérico: póngase en contacto con el soporte técnico de Azure para que podamos investigarlo. 

![Mensaje genérico de Azure RemoteApp](./media/remoteapp-apptrouble/ra-apptrouble4.png) 

