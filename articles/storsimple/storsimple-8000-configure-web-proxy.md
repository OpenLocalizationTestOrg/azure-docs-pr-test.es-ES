---
title: aaaSet el proxy web para el dispositivo de la serie StorSimple 8000 | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Windows PowerShell para StorSimple tooconfigure web configuración del proxy para el dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: 
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: alkohli
ms.openlocfilehash: ed34ff400df66a5f1950c21d5298b41acc538cca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-proxy-for-your-storsimple-device"></a>Configurar el proxy web para el dispositivo StorSimple

## <a name="overview"></a>Información general

Este tutorial se describe cómo toouse Windows PowerShell para StorSimple tooconfigure y vista web configuración del proxy para el dispositivo StorSimple. configuración del proxy web Hola se utiliza por dispositivo de StorSimple de hello al comunicarse con hello nube. Un servidor proxy web es tooadd usado otro nivel de seguridad, filtrar el contenido, almacenar en caché tooease requisitos de ancho de banda o incluso ayudar con el análisis.

Guía de Hello en este tutorial aplica solo tooStorSimple 8000 series dispositivos físicos. Configuración del proxy Web no se admite en hello aparato de nube de StorSimple (8010 y 8020).

El proxy web es una configuración _opcional_ de su dispositivo StorSimple. Puede configurar el proxy web solo a través de Windows PowerShell para StorSimple. configuración de Hello es un proceso de dos pasos como se indica a continuación:

1. Configurar la configuración de proxy web a través del Asistente para la instalación de Hola o Windows PowerShell para los cmdlets de StorSimple.
2. A continuación, habilitar a Hola configurado configuración del proxy web a través de Windows PowerShell para StorSimple cmdlets.

Una vez completada la configuración del proxy web hello, puede ver configuración del proxy web Hola configurado en el servicio de administrador de dispositivos de Microsoft Azure StorSimple Hola y Hola Windows PowerShell para StorSimple.

Después de leer este tutorial, podrá:

* Configurar el proxy web mediante el asistente para instalación y los cmdlets.
* Habilitar el proxy web mediante cmdlets.
* Ver la configuración de proxy web en hello portal de Azure.
* Solución de errores durante la configuración del proxy web.


## <a name="configure-web-proxy-via-windows-powershell-for-storsimple"></a>Configurar el proxy web a través de Windows PowerShell para StorSimple

Use cualquiera de hello después de la configuración del proxy web tooconfigure:

* Tooguide del Asistente para la instalación le guían a través de los pasos de configuración de Hola.
* Los cmdlets de Windows PowerShell para StorSimple

Cada uno de estos métodos se explica en las secciones siguientes de Hola.

## <a name="configure-web-proxy-via-hello-setup-wizard"></a>Configurar a proxy web a través del Asistente para la instalación de Hola

Utilice tooguide Asistente Hola el programa de instalación que le guían a través de hello los pasos de configuración del proxy web. Realizar Hola después de proxy web de tooconfigure de pasos en el dispositivo.

#### <a name="tooconfigure-web-proxy-via-hello-setup-wizard"></a>proxy web de tooconfigure a través del Asistente para la instalación de Hola

1. En el menú de consola serie de hello, elija la opción 1, **iniciar sesión con acceso completo** y proporcionar hello **contraseña de administrador de dispositivo**. Escriba lo siguiente Hola comando toostart una sesión del Asistente para la instalación:
   
    `Invoke-HcsSetupWizard`
2. Si se trata de hello primera vez que ha utilizado el Asistente para la instalación de hello para el registro de dispositivos, debe tooconfigure todas las configuraciones de red de hello necesario hasta llegar a la configuración del proxy web Hola. Si el dispositivo ya está registrado, acepte todos los ajustes de red de hello configurado hasta llegar a la configuración del proxy web Hola. Asistente para instalación de hello, cuando tooconfigure solicitada web configuración de proxy, escriba **Sí**.
3. Para hello **URL de Proxy Web**, especifique la dirección IP de Hola u Hola nombre de dominio completo (FQDN) de la web proxy hello y servidor número de puerto TCP que quiere que su toouse dispositivo al comunicarse con hello nube. Usar hello siguiendo el formato:
   
    `http://<IP address or FQDN of hello web proxy server>:<TCP port number>`
   
    De manera predeterminada, se especifica el número de puerto TCP 8080.
4. Elija el tipo de autenticación hello **NTLM**, **básica**, o **ninguno**. Basic es autenticación menos segura de hello para la configuración del servidor proxy Hola. NT LAN Manager (NTLM) es un protocolo de autenticación compleja y muy seguro que usa un sistema de mensajería de tres vías (a veces incluso cuatro si se requiere integridad adicional) tooauthenticate un usuario. autenticación de Hello predeterminado es NTLM. Para obtener más información, consulte autenticación [Básica](http://hc.apache.org/httpclient-3.x/authentication.html) y [NTLM](http://hc.apache.org/httpclient-3.x/authentication.html). 
   
   > [!IMPORTANT]
   > **Hola servicio Administrador de dispositivos de StorSimple, gráficos de supervisión de dispositivos de hello no funcionan cuando básica o la autenticación NTLM está habilitada en la configuración de servidor proxy de hello de dispositivo de Hola. Para hello toowork de gráficos de supervisión, debe tooensure que la autenticación se establece tooNONE.**
  
5. Si ha habilitado la autenticación de hello, proporcionar un **nombre de usuario de Proxy Web** y un **contraseña del Proxy Web**. También necesitará tooconfirm Hola contraseña.
   
    ![Configurar el proxy web en el dispositivo StorSimple 1](./media/storsimple-configure-web-proxy/IC751830.png)

Si va a registrar el dispositivo para hello primera vez, continúe con el registro de hello. Si ya se ha registrado el dispositivo, se cierra el Asistente de Hola. configuración de Hello configurado se guarda.

El proxy web ya está habilitado. Puede omitir hello [habilitar el proxy web](#enable-web-proxy) paso a paso y vaya directamente demasiado[ver configuración de proxy web en el portal de Azure hello](#view-web-proxy-settings-in-the-azure-portal).

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple-cmdlets"></a>Configurar el proxy web mediante Windows PowerShell para StorSimple

Una configuración de proxy web de forma alternativa tooconfigure es a través de hello Windows PowerShell para StorSimple cmdlets. Realizar Hola después de proxy de pasos tooconfigure web.

#### <a name="tooconfigure-web-proxy-via-cmdlets"></a>proxy de web de tooconfigure a través de los cmdlets
1. En el menú de consola serie de hello, elija la opción 1, **iniciar sesión con acceso completo**. Cuando se le solicite, proporcione hello **contraseña de administrador de dispositivo**. contraseña de Hello predeterminada es `Password1`.
2. En hello símbolo del sistema, escriba:
   
    `Set-HcsWebProxy -Authentication NTLM -ConnectionURI "<http://<IP address or FQDN of web proxy server>:<TCP port number>" -Username "<Username for web proxy server>"`
   
    Proporcione y confirme la contraseña de hello cuando se le solicite.
   
    ![Configurar el proxy web en el dispositivo StorSimple 3](./media/storsimple-configure-web-proxy/IC751831.png)

proxy de Hello web ya está configurado y necesita toobe habilitado.

## <a name="enable-web-proxy"></a>Habilitar el proxy web

El proxy web está deshabilitado de manera predeterminada. Después de configurar opciones de proxy web de hello en el dispositivo StorSimple, usar hello Windows PowerShell para la configuración de proxy web de StorSimple tooenable Hola.

> [!NOTE]
> **Este paso no es necesario si utiliza al proxy web tooconfigure de hello instalación asistente. El proxy web se habilita automáticamente de manera predeterminada después de una sesión del asistente de configuración.**


Lleve a cabo Hola siguiendo los pasos indicados en Windows PowerShell para el proxy web de StorSimple tooenable en el dispositivo:

#### <a name="tooenable-web-proxy"></a>proxy web de tooenable
1. En el menú de consola serie de hello, elija la opción 1, **iniciar sesión con acceso completo**. Cuando se le solicite, proporcione hello **contraseña de administrador de dispositivo**. contraseña de Hello predeterminada es `Password1`.
2. En hello símbolo del sistema, escriba:
   
    `Enable-HcsWebProxy`
   
    Ahora ya ha habilitado la configuración del proxy web hello en el dispositivo StorSimple.
   
    ![Configurar el proxy web en el dispositivo StorSimple 4](./media/storsimple-configure-web-proxy/IC751832.png)

## <a name="view-web-proxy-settings-in-hello-azure-portal"></a>Ver la configuración de proxy web en hello portal de Azure

configuración del proxy web Hola se configura a través de la interfaz de Windows PowerShell de hello y no se pueden cambiar en el portal de Hola. Sin embargo, puede ver los valores configurados en el portal de Hola. Realizar Hola después de proxy de pasos tooview web.

#### <a name="tooview-web-proxy-settings"></a>configuración del proxy web tooview
1. Navegue demasiado**servicio de administrador de dispositivos de StorSimple > dispositivos**. Seleccione y haga clic en un dispositivo y, a continuación, vaya demasiado**configuración del dispositivo > red**.

    ![Haga clic en Red](./media/storsimple-8000-configure-web-proxy/view-web-proxy-1.png)

2. Hola **configuración de red** hoja, haga clic en hello **proxy Web** icono.

    ![Haga clic en Proxy web](./media/storsimple-8000-configure-web-proxy/view-web-proxy-2.png)

3. Hola **proxy Web** hoja, configuración del proxy web revisión Hola configurado en el dispositivo StorSimple.
   
    ![Ver la configuración de proxy web](./media/storsimple-8000-configure-web-proxy/view-web-proxy-3.png)


## <a name="errors-during-web-proxy-configuration"></a>Errores durante la configuración del proxy web

Si la configuración del proxy web hello no está configurados correctamente, mensajes de error son usuario toohello mostrada en Windows PowerShell para StorSimple. Hello en la tabla siguiente explica algunos de estos mensajes de error, sus causas probables y acciones recomendadas.

| Nº de serie | Código de error HRESULT | Posible causa principal | Acción recomendada |
|:--- |:--- |:--- |:--- |
| 1. |0x80070001 |Comando se ejecuta desde el controlador pasivo hello y no es capaz de toocommunicate con controlador activo Hola. |Ejecute el comando de hello en controlador activo Hola. toorun comando de Hola desde el controlador pasivo hello, debe corregir conectividad de Hola desde el controlador pasivo tooactive. Si no hay conectividad, debe ponerse en contacto con el soporte técnico de Microsoft. |
| 2. |0x800710dd - identificador de la operación de hello no es válido |StorSimple Cloud Appliance no admite la configuración de proxy. |StorSimple Cloud Appliance no admite la configuración de proxy. La misma solo puede establecerse en un dispositivo StorSimple físico. |
| 3. |0x80070057 - Parámetro no válido |Uno de los parámetros de hello proporcionados para la configuración de proxy de hello no es válido. |Hola URI no se proporciona en el formato correcto. Usar hello siguiendo el formato:`http://<IP address or FQDN of hello web proxy server>:<TCP port number>` |
| 4. |0x800706ba - Servidor RPC no disponible |causa de Hello es uno de los siguientes de hello:</br></br>El clúster no está activo. </br></br>El servicio de ruta de datos no se está ejecutando.</br></br>Hola comando se ejecuta desde el controlador pasivo y no es capaz de toocommunicate con controlador activo Hola. |Participar tooensure Microsoft Support que Hola clúster está activo y se está ejecutando el servicio de ruta de datos.</br></br>Ejecute el comando de Hola desde el controlador activo Hola. Si desea toorun Hola comando desde el controlador pasivo hello, debe asegurarse de que ese controlador pasivo Hola puede comunicarse con el controlador activo Hola. Si no hay conectividad, debe ponerse en contacto con el soporte técnico de Microsoft. |
| 5. |0X800706be - Llamada RPC con errores |El clúster está inactivo. |Participar tooensure Microsoft Support que Hola clúster está activo. |
| 6. |0x8007138f - Recurso de clúster no encontrado |El recurso de clúster del servicio de plataforma no se encuentra. Esto puede ocurrir cuando la instalación de hello no era correcto. |Puede que necesite tooperform una restablecimiento de fábrica en el dispositivo. Puede que necesite toocreate un recurso de la plataforma. Póngase en contacto con el servicio de soporte técnico de Microsoft para conocer los pasos siguientes. |
| 7. |0x8007138c - El recurso de clúster no está en línea |Los recursos de clúster de ruta de datos o plataforma no están en línea. |Contacto toohelp Microsoft Support Asegúrese de que el recurso del servicio de plataforma y la ruta de datos de hello estén en línea. |

> [!NOTE]
> * Hola por encima de la lista de mensajes de error no es exhaustiva.
> * No se mostrará la configuración de proxy de errores relacionados tooweb Hola portal de Azure en el servicio de administrador de dispositivos de StorSimple. Si hay un problema con el proxy web una vez finalizada la configuración de hello, estado del dispositivo Hola cambiará demasiado**Offline** en portal clásico de Hola. |

## <a name="next-steps"></a>Pasos siguientes
* Si experimenta problemas al implementar el dispositivo o la configuración de proxy web, consulte demasiado[solucionar problemas de la implementación de dispositivo de StorSimple](storsimple-troubleshoot-deployment.md).
* toolearn cómo ir demasiado toouse Hola servicio de administrador de dispositivos de StorSimple,[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

