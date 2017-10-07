---
title: "problemas de implementación de StorSimple aaaTroubleshoot | Documentos de Microsoft"
description: "Describe cómo toodiagnose y corrección de errores que se producen cuando se implementa en primer lugar StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: f8352eaa-193c-42d1-8818-0b8e02d8485d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 9a31a3cfb3be577500b226c2bc8172dd8664bad9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storsimple-device-deployment-issues"></a>Solución de problemas de implementación de dispositivos de StorSimple
## <a name="overview"></a>Información general
Este artículo proporciona instrucciones útiles para la solución de problemas relacionados con la implementación de Microsoft Azure StorSimple. Describe los problemas comunes, causas posibles y toohelp pasos recomendados que resolver problemas que pueden experimentar al configurar StorSimple. Esta información aplica tooboth dispositivo físico de hello StorSimple local y el dispositivo virtual StorSimple Hola.

> [!NOTE]
> Problemas relacionados con la configuración del dispositivo que pueda enfrentar pueden producirse al implementar dispositivos Hola para hello primera vez o se pueden producir más adelante, cuando el dispositivo de hello esté operativo. Este artículo se centra en la solución de problemas relacionados con la implementación por primera vez. tootroubleshoot un dispositivo operativo, vaya demasiado[solucionar problemas del dispositivo operativa](storsimple-troubleshoot-operational-device.md).
> 
> 

Este artículo también describe las herramientas de Hola para solucionar problemas en implementaciones de StorSimple y proporciona un ejemplo paso a paso para solucionar problemas.

## <a name="first-time-deployment-issues"></a>Problemas de implementación por primera vez
Si experimenta un problema al implementar el dispositivo para hello primera vez, tenga en cuenta Hola siguiente:

* Si está solucionando un dispositivo físico, asegúrese de que se ha instalado y configurado como se describe en hardware de hello [instalar el dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md) o [instalar su dispositivo 8600 StorSimple](storsimple-8600-hardware-installation.md).
* Compruebe los requisitos previos para la implementación. Asegúrese de que tiene toda la información de hello descrita en hello [lista de comprobación de configuración de implementación](storsimple-deployment-walkthrough.md#deployment-configuration-checklist).
* Revise Hola notas de la versión de StorSimple toosee si se describe el problema de Hola. notas de la versión de Hola incluyen soluciones para problemas de instalación conocidos. 

Durante la implementación de dispositivo, hello más comunes problemas a que los usuarios cara se producen cuando se ejecuta Asistente para la instalación de Hola y cuando registran dispositivo hello mediante Windows PowerShell para StorSimple. (Usa Windows PowerShell para StorSimple tooregister y configura el dispositivo de StorSimple. Para obtener más información sobre el registro de dispositivos, consulte [Paso 3: Configurar y registrar el dispositivo mediante Windows PowerShell para StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)).

Hola siguientes secciones puede ayudarle a resolver los problemas que encuentre al configurar el dispositivo de StorSimple de Hola para hello primera vez.

## <a name="first-time-setup-wizard-process"></a>Proceso del Asistente para instalación por primera vez
Hola pasos resume proceso del Asistente para instalación Hola. Para obtener información detallada de la configuración, consulte cómo [Implementar el dispositivo StorSimple local](storsimple-deployment-walkthrough.md).

1. Ejecute hello [Invoke-HcsSetupWizard](https://technet.microsoft.com/library/dn688135.aspx) cmdlet toostart Hola Asistente para la instalación que le guiará a través de hello restantes pasos. 
2. Configurar red hello: Asistente para la instalación de hello le permite configurar opciones de red para la interfaz de red 0 datos hello en el dispositivo StorSimple. Estas opciones incluyen siguiente de hello:
   * Virtuales IP (VIP), máscara de subred y puerta de enlace: Hola [Set-HcsNetInterface](https://technet.microsoft.com/library/dn688161.aspx) cmdlet se ejecuta en segundo plano de Hola. Dirección IP de hello, máscara de subred y puerta de enlace para la interfaz de red 0 de datos de Hola configura en el dispositivo StorSimple.
   * Servidor DNS principal: Hola [Set-HcsDnsClientServerAddress](https://technet.microsoft.com/library/dn688172.aspx) cmdlet se ejecuta en segundo plano de Hola. Configura valores de DNS de hello para la solución StorSimple.
   * Servidor NTP: Hola [Set-HcsNtpClientServerAddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet se ejecuta en segundo plano de Hola. Establece Hola configuración de servidor NTP para su solución de StorSimple.
   * Opcional proxy web: hello [Set-HcsWebProxy](https://technet.microsoft.com/library/dn688154.aspx) cmdlet se ejecuta en segundo plano de Hola. Establece y permite la configuración de proxy web de hello para la solución StorSimple.
3. Configurar contraseñas de hello: Hola siguiente paso es tooset Administrador de dispositivos y las contraseñas de administrador de instantáneas StorSimple. Si ejecuta Update 1, no podrá tooset requiere la contraseña de administrador de instantáneas StorSimple Hola.
   
   * contraseña del Administrador de dispositivos de Hello es toolog usado en el dispositivo de tooyour. es la contraseña predeterminada del dispositivo de Hello **Password1**.
   * contraseña de administrador de instantáneas StorSimple de Hello es necesaria cuando configura un administrador de instantáneas StorSimple toouse de dispositivo. Debe toofirst establecer contraseña de hello en el Asistente para la instalación de hello y, a continuación, puede establecer y cambiar de hello el servicio StorSimple Manager. Esta contraseña autentica el dispositivo de hello con el Administrador de instantáneas de StorSimple.
     
     > [!IMPORTANT]
     > Las contraseñas se recopilan antes del registro, pero solo se aplican cuando se haya registrado correctamente el dispositivo de Hola. Si se produce un error tooapply una contraseña, se podrá solicitadas toosupply contraseña de Hola de nuevo hasta que Hola requiere contraseñas (que cumplan los requisitos de complejidad de Hola) se recopilan.
     > 
     > 
4. Registrar el dispositivo de hello: Hola último paso es el dispositivo de hello tooregister con servicio de StorSimple Manager Hola ejecuta en Microsoft Azure. registro de Hello requiere demasiado[obtener clave de registro del servicio de hello](storsimple-manage-service.md#get-the-service-registration-key) de Hola portal de Azure clásico y se proporciona en el Asistente para la instalación de Hola. Después de que se ha registrado correctamente el dispositivo de hello, una clave de cifrado de datos de servicio se proporciona tooyou. Asegúrese de que tookeep el cifrado de clave en una ubicación segura ya que será necesario tooregister todos los dispositivos subsiguientes con el servicio de Hola.

## <a name="common-errors-during-device-deployment"></a>Errores comunes durante la implementación de dispositivos
¡Hola siguientes tablas lista Hola los errores comunes que pueden surgir cuando se:

* Configure la red de hello necesario.
* Configurar opciones de proxy web opcional Hola.
* Configurar el administrador del dispositivo de Hola y las contraseñas de administrador de instantáneas StorSimple. 
* Registrar el dispositivo Hola. 

## <a name="errors-during-hello-required-network-settings"></a>Errores durante la configuración de red de hello necesario
| No. | Mensaje de error | Causas posibles | Acción recomendada |
| --- | --- | --- | --- |
| 1 |Invoke-HcsSetupWizard: Sólo se puede ejecutar este comando en el controlador activo Hola. |Configuración se estaba realizando en el controlador pasivo Hola. |Ejecute este comando desde el controlador activo Hola. Para obtener más información, consulte [Identificación de un controlador activo en el dispositivo](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device). |
| 2 |Invoke-HcsSetupWizard: El dispositivo no está listo. |Hay problemas con la conectividad de red de hello en DATA 0. |Compruebe la conectividad de red físico de hello en DATA 0. |
| 3 |Invoke-HcsSetupWizard: Hay un conflicto de dirección IP con otro sistema de red de hello (excepción de HRESULT: 0x80070263). |dirección IP de Hello proporcionada para DATA 0 ya estaba en uso por otro sistema. |Indique una dirección IP nueva que no esté en uso. |
| 4 |Invoke-HcsSetupWizard: Error en un recurso de clúster (excepción de HRESULT: 0x800713AE). |VIP duplicada. IP de Hello proporcionado ya está en uso. |Indique una dirección IP nueva que no esté en uso. |
| 5 |Invoke-HcsSetupWizard: Dirección IPv4 no válida. |dirección IP de Hola se proporciona en un formato incorrecto. |Compruebe el formato de Hola y proporcione la dirección IP de nuevo. Para obtener más información, consulte [Direcciones Ipv4][1]. |
| 6 |Invoke-HcsSetupWizard: Dirección IPv6 no válida. |dirección IP de Hola se proporciona en un formato incorrecto. |Compruebe el formato de Hola y proporcione la dirección IP de nuevo. Para obtener más información, consulte [Direcciones Ipv6][2]. |
| 7 |Invoke-HcsSetupWizard: Hay no hay más extremos disponibles desde el asignador de extremos de Hola. (Excepción de HRESULT: 0x800706D9). |funcionalidad de clústeres de Hello no funciona. |[Póngase en contacto con el servicio de soporte técnico de Microsoft](storsimple-contact-microsoft-support.md) para conocer los pasos siguientes. |

## <a name="errors-during-hello-optional-web-proxy-settings"></a>Errores durante la configuración del proxy web opcional Hola
| No. | Mensaje de error | Causas posibles | Acción recomendada |
| --- | --- | --- | --- |
| 1 |Invoke-HcsSetupWizard: Parámetro no válido (excepción de HRESULT: 0x80070057) |Uno de los parámetros de hello proporcionados para la configuración de proxy de hello no es válido. |Hola URI no se proporciona en el formato correcto de saludo. Hola de uso siguiente formato: http://*<IP address or FQDN of hello web proxy server>*:*<TCP port number>* |
| 2 |Invoke-HcsSetupWizard: Servidor RPC no disponible (excepción de HRESULT: 0x800706ba) |causa de Hello es uno de los siguientes de hello:<ol><li>clúster de Hello no está activo.</li><li>el controlador pasivo Hello no puede comunicarse con el controlador activo de Hola y Hola comando se ejecuta desde el controlador pasivo.</li></ol> |Dependiendo de la causa raíz de hello:<ol><li>[Póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) toomake seguro de ese clúster Hola está activo.</li><li>Ejecute el comando de Hola desde el controlador activo Hola. Si desea toorun Hola comando desde el controlador pasivo hello, deberá tooensure ese controlador pasivo Hola puede comunicarse con el controlador activo Hola. Necesitará demasiado[póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) si la conectividad está rota.</li></ol> |
| 3 |Invoke-HcsSetupWizard: Error en la llamada RPC (excepción de HRESULT: 0x800706be) |El clúster está inactivo. |[Póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) toomake seguro de ese clúster Hola está activo. |
| 4 |Invoke-HcsSetupWizard: El recurso de clúster no se encontró (excepción de HRESULT: 0x8007138f). |no se encuentra el recurso de clúster de Hola. Esto puede ocurrir cuando la instalación de hello no era correcta. |Puede que tenga la configuración predeterminada de fábrica de toohello de dispositivo de tooreset Hola. [Póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) toocreate un recurso de clúster. |
| 5 |Invoke-HcsSetupWizard: El recurso de clúster no está en línea (excepción de HRESULT: 0x8007138c). |Los recursos de clúster no están en línea. |[Póngase en contacto con el servicio de soporte técnico de Microsoft](storsimple-contact-microsoft-support.md) para conocer los pasos siguientes. |

## <a name="errors-related-toodevice-administrator-and-storsimple-snapshot-manager-passwords"></a>Errores relacionados con Administrador de toodevice y las contraseñas de administrador de instantáneas StorSimple
contraseña del Administrador de dispositivos de Hello predeterminada es **Password1**. Esta contraseña expira tras Hola primer inicio de sesión; por lo tanto, necesitará toochange del Asistente de instalación de toouse Hola se. Debe proporcionar una nueva contraseña de administrador de dispositivos al registrar dispositivo Hola para hello primera vez. 

Si utiliza el software de administrador de instantáneas StorSimple Hola ejecutando en hello Windows Server host toomanage Hola dispositivo, también debe proporcionar una contraseña de administrador de instantáneas StorSimple durante el registro por primera vez. 

Asegúrese de que las contraseñas cumplan Hola según los requisitos:

* La contraseña del administrador de dispositivos debe tener entre 8 y 15 caracteres.
* La contraseña de StorSimple Snapshot Manager debe tener 14 o 15 caracteres.
* Las contraseñas deben contener 3 de hello siguientes 4 tipos de caracteres: minúsculas, mayúsculas, numéricos y especiales. 
* La contraseña no se puede ser Hola igual que Hola últimas 24 contraseñas.

Además, tenga en cuenta que las contraseñas expiran cada año y se puede cambiar sólo después de registrar correctamente el dispositivo de Hola. Si se produce un error en el registro de hello por cualquier motivo, no se cambiará las contraseñas de Hola. Para obtener más información sobre el Administrador de dispositivos y las contraseñas de administrador de instantáneas de StorSimple, vaya demasiado[uso Hola toochange de servicio de administrador de StorSimple las contraseñas de StorSimple](storsimple-change-passwords.md).

Puede encontrar uno o varios de los siguientes errores al configurar el Administrador de dispositivos de Hola y las contraseñas de administrador de instantáneas StorSimple de Hola.

| No. | Mensaje de error | Acción recomendada |
| --- | --- | --- |
| 1 |contraseña de Hello supera la longitud máxima de Hola. |Utilice una contraseña que cumpla estos requisitos:<ul><li>La contraseña de administrador del dispositivo debe tener entre 8 y 15 caracteres.</li><li>La contraseña de StorSimple Snapshot Manager debe tener 14 o 15 caracteres.</li></ul> |
| 2 |Hola contraseña no cumple longitud Hola necesario. |Utilice una contraseña que cumpla estos requisitos:<ul><li>La contraseña de administrador del dispositivo debe tener entre 8 y 15 caracteres.</li><li>La contraseña de StorSimple Snapshot Manager debe tener 14 o 15 caracteres.</lu></ul> |
| 3 |contraseña de Hello debe contener caracteres en minúsculas. |Las contraseñas deben contener 3 de hello siguientes 4 tipos de caracteres: minúsculas, mayúsculas, numéricos y especiales. Asegúrese de que la contraseña cumple estos requisitos. |
| 4 |contraseña de Hello debe contener caracteres numéricos. |Las contraseñas deben contener 3 de hello siguientes 4 tipos de caracteres: minúsculas, mayúsculas, numéricos y especiales. Asegúrese de que la contraseña cumple estos requisitos. |
| 5 |contraseña de Hello debe contener caracteres especiales. |Las contraseñas deben contener 3 de hello siguientes 4 tipos de caracteres: minúsculas, mayúsculas, numéricos y especiales. Asegúrese de que la contraseña cumple estos requisitos. |
| 6 |Hello contraseña debe contener 3 de hello siguientes 4 tipos de caracteres: mayúsculas, minúsculas, numéricos y especiales. |La contraseña no contiene tipos de hello necesaria de caracteres. Asegúrese de que la contraseña cumple estos requisitos. |
| 7 |El parámetro no coincide con la confirmación. |Asegúrese de que la contraseña cumple todos los requisitos y de que la ha escrito correctamente. |
| 8 |La contraseña no puede coincidir con valor predeterminado de Hola. |es la contraseña predeterminada de Hello *Password1*. Debe toochange esta contraseña después de iniciar sesión para hello primera vez. |
| 9 |contraseña de Hola que ha escrito no coincide con la contraseña del dispositivo Hola. Vuelva a escribir contraseña de Hola. |Compruebe la contraseña de Hola y escríbala de nuevo. |

Las contraseñas se recopilan antes de dispositivo de hello está registrado, pero se aplican solo después de un registro correcto. flujo de trabajo de recuperación de contraseña de Hello requiere hello toobe de dispositivo registrado. 

> [!IMPORTANT]
> En general, si un intento de tooapply una contraseña produce un error, a continuación, software de hello intenta repetidamente contraseña de hello toocollect hasta que se realiza correctamente. En raras ocasiones, no se puede aplicar la contraseña de Hola. En esta situación, puede registrar el dispositivo de Hola y continuar, sin embargo no se cambiarán las contraseñas de Hola. No recibirá ninguna indicación de que no se cambió la contraseña de toowhich: contraseña de administrador de dispositivos de Hola o la contraseña de administrador de instantáneas StorSimple Hola. Si se produce esta situación, se recomienda que cambie ambas contraseñas.
> 
> 

Puede restablecer las contraseñas de Hola Hola portal de Azure clásico a través de hello el servicio StorSimple Manager. Para obtener más información, consulte: 

* [Cambiar contraseña de administrador de dispositivo de hello](storsimple-change-passwords.md#change-the-device-administrator-password).
* [Cambiar contraseña de administrador de instantáneas StorSimple hello](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password).

## <a name="errors-during-device-registration"></a>Errores durante el registro de dispositivos
Usar el servicio de StorSimple Manager Hola ejecutando en el dispositivo de Microsoft Azure tooregister Hola. Podrían surgir uno o varios de hello problemas siguientes durante el registro de dispositivo.

| No. | Mensaje de error | Causas posibles | Acción recomendada |
| --- | --- | --- | --- |
| 1 |Error 350027 al dispositivo de hello tooregister con hello StorSimple Manager. | |Espere unos minutos y vuelva a intentar la operación de Hola de nuevo. Si persiste el problema de hello, [póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md). |
| 2 |Error 350013: Hubo un error en el registro de dispositivos de Hola. Esto puede ser debido tooincorrect clave de registro del servicio. | |Vuelva a registrar Hola dispositivo con la clave de registro del servicio correcta Hola. Para obtener más información, vea [clave de registro del servicio de Get hello.](storsimple-manage-service.md#get-the-service-registration-key) |
| 3 |Error 350063: Autenticación tooStorSimple servicio Manager pasado pero no se pudo registrar. Vuelva a intentar la operación de hello más tarde. |Este error indica que ha pasado la autenticación con ACS pero Hola register llamada realizada toohello servicio no ha podido. Esto puede deberse a un problema de red esporádico. |Si el problema de hello persiste, [póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md). |
| 4 |Error 350049: Hola podría no tener acceso al servicio durante el registro. |Cuando se realizan llamadas de hello toohello servicio, se recibe una excepción web. En algunos casos, esto puede solucionarse volviendo a intentar la operación de hello más tarde. |Compruebe su dirección IP y el nombre DNS y, a continuación, vuelva a intentar la operación de Hola. Si persiste el problema de hello, [póngase en contacto con Microsoft Support.](storsimple-contact-microsoft-support.md) |
| 5 |Error 350031: Hola dispositivo ya está registrado. | |No es necesaria ninguna acción. |
| 6 |Error 350016: Error de registro de dispositivo. | |Asegúrese de que la clave de registro de hello es correcta. |
| 7 |Invoke-HcsSetupWizard: Se ha producido un error al registrar el dispositivo; Esto puede ser debido tooincorrect dirección IP o nombre DNS. Compruebe la configuración de red y vuelva a intentarlo. Si persiste el problema de hello, [póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md). (Error 350050) |Asegúrese de que el dispositivo puede hacer ping Hola fuera de la red. Si no tiene red toooutside de conectividad, registro de hello puede producir este error. Este error puede ser una combinación de uno o más de hello siguientes:<ul><li>IP incorrecta</li><li>Subred incorrecta</li><li>Puerta de enlace incorrecta</li><li>Configuración DNS incorrecta</li></ul> |Consulte los pasos de Hola de hello [ejemplo paso a paso de solución de problemas](#step-by-step-storsimple-troubleshooting-example). |
| 8 |Invoke-HcsSetupWizard: error en la operación actual de hello debido tooan error de servicio interno [0x1FBE2]. Vuelva a intentar operación hello más tarde. Si persiste el problema de hello, póngase en contacto con Microsoft Support. |Se trata de un error genérico que se produce para todos los errores invisibles de usuario del servicio o del agente. razón más común de Hello puede ser el que error de autenticación Hola ACS. Una posible causa de error de hello es que hay problemas con la configuración del servidor NTP hello y hora Hola dispositivo no está configurado correctamente. |Corrija la hora de hello (si hay problemas) y, a continuación, vuelva a intentar la operación de registro de hello. Si usas zona de horaria Hola Set-HcsSystem - zona horaria comando tooadjust hello, poner en mayúsculas todas las palabras de la zona horaria de hello (por ejemplo "hora estándar del Pacífico").  Si persiste este problema, [póngase en contacto con el servicio de soporte técnico de Microsoft](storsimple-contact-microsoft-support.md) para conocer los pasos siguientes. |
| 9 |Advertencia: No se pudo activar el dispositivo de Hola. Las contraseñas del administrador de dispositivos y de StorSimple Snapshot Manager no han cambiado. |Si se produce un error en el registro de Hola, Administrador de dispositivos de Hola y las contraseñas de administrador de instantáneas de StorSimple no cambian. | |

## <a name="tools-for-troubleshooting-storsimple-deployments"></a>Herramientas para solucionar problemas en implementaciones de StorSimple
StorSimple incluye varias herramientas que puede usar tootroubleshoot la solución StorSimple. Entre ellos se incluyen los siguientes:

* Paquetes de soporte y registros de dispositivo 
* Cmdlets diseñados específicamente para la solución de problemas 

## <a name="support-packages-and-device-logs-available-for-troubleshooting"></a>Paquetes de soporte y registros de dispositivo disponibles para la solución de problemas
Un paquete de soporte contiene todos los registros pertinentes Hola que pueden ayudar equipo de Microsoft Support de Hola a solucionar problemas de dispositivos. Puede usar Windows PowerShell para StorSimple toogenerate un paquete de soporte cifrado que, a continuación, puede compartir con el personal de soporte técnico.

### <a name="tooview-hello-logs-or-hello-contents-of-hello-support-package"></a>registros de hello tooview o contenido de Hola Hola del paquete de soporte
1. Usar Windows PowerShell para StorSimple toogenerate un paquete de soporte técnico como se describe en [crear y administrar un paquete de soporte](storsimple-create-manage-support-package.md).
2. Descargar hello [secuencia de comandos de descifrado](https://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localmente en el equipo cliente.
3. Utilícelo [procedimiento paso a paso](storsimple-create-manage-support-package.md#edit-a-support-package) paquete de soporte técnico de hello tooopen y descifrar.
4. Hola descifra el paquete de soporte técnico de los registros están en formato etw/etvx. Puede realizar Hola siguiendo los pasos tooview estos archivos en el Visor de eventos de Windows:
   
   1. Ejecute hello **eventvwr** comando en el cliente Windows. Esto iniciará Hola Visor de eventos.
   2. Hola **acciones** panel, haga clic en **Abrir registro guardado** y archivos de registro de punto de toohello en formato etvx/etw (paquete de soporte de hello). Ahora puede ver el archivo hello. Después de abrir el archivo hello, puede haga clic en y guarde el archivo hello como texto.
      
      > [!IMPORTANT]
      > También puede usar hello **Get-WinEvent** cmdlet tooopen estos archivos en Windows PowerShell. Para obtener más información, consulte [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx) Hola documentación de referencia de cmdlet de Windows PowerShell.
      > 
      > 
5. Al abrir registros de hello en el Visor de eventos, busque Hola después de registros que contienen la configuración del dispositivo relacionadas toohello problemas:
   
   * hcs_pfconfig/registro operativo
   * hcs_pfconfig/registro de configuración
6. En los archivos de registro de hello, buscar cadenas cmdlets relacionados toohello llamado por el Asistente para la instalación de Hola. Consulte [Proceso del Asistente para instalación por primera vez](#first-time-setup-wizard-process) para obtener una lista de estos cmdlets. 
7. Si no es capaz de toofigure a causa de Hola de problema de hello, también puede [póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) para los pasos siguientes. Hola de uso de los pasos de [crear una solicitud de soporte técnico](storsimple-contact-microsoft-support.md#create-a-support-request) cuando póngase en contacto con Microsoft Support para obtener ayuda.

## <a name="cmdlets-available-for-troubleshooting"></a>Cmdlets disponibles para solucionar problemas
Usar hello siguientes errores de conectividad de toodetect de cmdlets de Windows PowerShell.

* `Get-NetAdapter`: Use este cmdlet toodetect el estado del Hola de interfaces de red. 
* `Test-Connection`: Use este cmdlet toocheck Hola conectividad dentro y fuera de la red de Hola.
* `Test-HcsmConnection`: Use este cmdlet toocheck la conectividad de Hola de un dispositivo registrado correctamente.

Si se ejecuta Update 1 en el dispositivo StorSimple, Hola siguientes cmdlets de diagnóstico también está disponible.

* `Sync-HcsTime`: Se usa esta hora del dispositivo cmdlet toodisplay y forzar una sincronización de hora con el servidor NTP Hola.
* `Enable-HcsPing`y `Disable-HcsPing`: usar estas interfaces de red cmdlets tooallow Hola hosts tooping hello en el dispositivo de StorSimple. De forma predeterminada, interfaces de red de StorSimple de hello no responder las solicitudes de tooping.
* `Trace-HcsRoute`: use este cmdlet como una herramienta de seguimiento de ruta. Envía el enrutador de tooeach de paquetes en el destino final de hello forma tooa durante un período de tiempo y, a continuación, calcula los resultados basándose en los paquetes de saludo devueltos en cada salto. Puesto que `Trace-HcsRoute` muestra el grado de Hola de pérdida de paquetes en un enrutador determinado o un vínculo, puede determinar qué enrutadores o vínculos podrían estar causando problemas en la red. 
* `Get-HcsRoutingTable`: Use este cmdlet toodisplay Hola local tabla de enrutamiento IP.

## <a name="troubleshoot-with-hello-get-netadapter-cmdlet"></a>Solucionar problemas con el cmdlet Get-NetAdapter de Hola
Cuando configura las interfaces de red para una implementación de dispositivo por primera vez, el estado del hardware de hello no está disponible en hello UI del servicio StorSimple Manager porque el dispositivo de hello no se ha registrado con el servicio de Hola. Además, página de estado de Hardware de hello puede no refleje correctamente estado hello de dispositivo de hello, especialmente si hay problemas que afectan a la sincronización del servicio. En estas situaciones, puede usar hello `Get-NetAdapter` cmdlet toodetermine Hola condición y estado de las interfaces de red.

### <a name="toosee-a-list-of-all-hello-network-adapters-on-your-device"></a>toosee una lista de todos los adaptadores de red de hello en el dispositivo
1. Inicie Windows PowerShell para StorSimple y escriba `Get-NetAdapter`. 
2. Usar la salida de hello de hello `Get-NetAdapter` hello siguiendo las directrices toounderstand y cmdlet Hola estado de la interfaz de red.
   
   * Si la interfaz de hello está habilitado y funciona correctamente, Hola **ifIndex** estado se muestra como **seguridad**.
   * Si la interfaz de hello es correcto pero no está conectado físicamente (mediante un cable de red), Hola **ifIndex** se muestra como **deshabilitado**.
   * Si la interfaz de hello es correcto pero no se ha habilitado, Hola **ifIndex** estado se muestra como **NotPresent**.
   * Si no existe interfaz hello, no aparece en esta lista. Hola UI del servicio StorSimple Manager seguirá mostrando esta interfaz en un estado de error.

Para obtener más información acerca de cómo toouse este cmdlet, vaya demasiado[GetNetAdapter](https://technet.microsoft.com/library/jj130867.aspx) Hola referencia de cmdlet de Windows PowerShell. 

Hello las secciones siguientes muestran ejemplos de la salida de hello `Get-NetAdapter` cmdlet. 

 En estos ejemplos, controlador 0 fue el controlador pasivo hello y se configuró como sigue:

* DATA 0, DATA 1, DATA 2 y red de DATA 3 existían interfaces en el dispositivo de Hola.
* DATA 4 y tarjetas de interfaz de red de DATA 5 no estaban presentes; por lo tanto, no aparecen en la salida de hello.
* La interfaz DATA 0 estaba habilitada.

Controlador 1 era controlador activo de Hola y se configuró como sigue:

* DATA 0, DATA 1, DATA 2, DATA 3, DATA 4 y red de DATA 5 existían interfaces en el dispositivo de Hola.
* La interfaz DATA 0 estaba habilitada.

**Ejemplo de salida: controlador 0**

Hola aquí te mostramos salida Hola desde el controlador 0 (Hola el controlador pasivo). DATA 1, DATA 2 y DATA 3 no están conectadas. DATA 4 y DATA 5 no aparecen porque no están presentes en el dispositivo de Hola. 

     Controller0>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter #2     17       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter        14       NotPresent
     Ethernet 2           HCS VNIC                                    13       Up
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up


**Ejemplo de salida: controlador 1**

Hola aquí te mostramos salida Hola desde el controlador 1 (controlador activo hello). Solo Hola DATA 0 se configura la interfaz de red de dispositivo de Hola y trabajar.

     Controller1>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter        18       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter #2     19       NotPresent
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up
     Ethernet 2           HCS VNIC                                    13       Up
     DATA5                Intel(R) Gigabit ET Dual Port Server...     14       NotPresent
     DATA4                Intel(R) Gigabit ET Dual Port Serv...#2     17       NotPresent


## <a name="troubleshoot-with-hello-test-connection-cmdlet"></a>Solucionar problemas con el cmdlet Test-Connection de Hola
Puede usar hello `Test-Connection` toodetermine cmdlet si su dispositivo de StorSimple puede conectarse toohello fuera de la red. Si todos los parámetros de red de hello, incluidos Hola DNS, están configurados correctamente en el Asistente para la instalación de hello, puede usar hello `Test-Connection` cmdlet tooping una dirección conocida fuera de la red de hello, por ejemplo, outlook.com. 

Debe habilitar problemas de conectividad de ping tootroubleshoot con este cmdlet si ping está deshabilitado.

Vea Hola siguientes ejemplos de salida de hello `Test-Connection` cmdlet. 

> [!NOTE]
> En el primer ejemplo de Hola, dispositivo Hola se configura con un DNS incorrecto. En el segundo ejemplo de Hola, Hola DNS es correcta.
> 
> 

**Ejemplo de salida: DNS incorrecto**

En el siguiente ejemplo de Hola, no hay ningún resultado para direcciones IPV4 e IPV6 de hello, que indica que Hola que DNS no se ha resuelto. Esto significa que no hay ningún toohello conectividad fuera de la red y un DNS correcto necesita toobe proporcionado. 

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com

**Ejemplo de salida: DNS correcto**

En el siguiente ejemplo de Hola, Hola DNS devuelve Hola una dirección IPV4, que indica que Hola que DNS está configurado correctamente. Esto confirma que hay conectividad toohello fuera de la red. 

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194

## <a name="troubleshoot-with-hello-test-hcsmconnection-cmdlet"></a>Solucionar problemas con el cmdlet Test-HcsmConnection de Hola
Hola de uso `Test-HcsmConnection` cmdlet para un dispositivo que ya está conectado tooand registrado con el servicio StorSimple Manager. Este cmdlet le ayuda a comprobar la conectividad de hello entre un dispositivo registrado y Hola correspondiente servicio StorSimple Manager. Puede ejecutar este comando en Windows PowerShell para StorSimple. 

### <a name="toorun-hello-test-hcsmconnection-cmdlet"></a>cmdlet de hello Test-HcsmConnection toorun
1. Asegúrese de que ese dispositivo Hola está registrado.
2. Comprobar el estado del dispositivo de Hola. Si se desactiva el dispositivo de hello, en modo de mantenimiento o sin conexión, pueden aparecer Hola siguientes errores: 
   
   * ErrorCode.CiSDeviceDecommissioned: indica que ese dispositivo Hola está desactivado.
   * ErrorCode.DeviceNotReady: indica que ese dispositivo Hola está en modo de mantenimiento.
   * ErrorCode.DeviceNotReady: indica que el dispositivo hello no está en línea.
3. Compruebe que el servicio StorSimple Manager Hola se está ejecutando (use hello [Get-ClusterResource](https://technet.microsoft.com/library/ee461004.aspx) cmdlet). Si no se está ejecutando el servicio de hello, pueden aparecer Hola siguientes errores:
   
   * ErrorCode.CiSApplianceAgentNotOnline
   * ErrorCode.CisPowershellScriptHcsError: indica que se produjo una excepción al ejecutar Get-ClusterResource.
4. Compruebe el token de servicio de Control de acceso (ACS) de Hola. Si produce una excepción web, es posible resultado de hello de un problema de puerta de enlace, una autenticación de proxy que faltan, un DNS incorrecto o un error de autenticación. Puede aparecer Hola siguientes errores:
   
   * ErrorCode.CiSApplianceGateway: indica una excepción de HttpStatusCode.BadGateway: servicio de resolución de nombres de hello no pudo resolver el nombre de host de Hola. 
   * ErrorCode.CiSApplianceProxy: indica una excepción de HttpStatusCode.ProxyAuthenticationRequired, con (código de estado HTTP 407): Hola cliente no pudo autenticar con el servidor de proxy de Hola. 
   * ErrorCode.CiSApplianceDNSError: indica una excepción de WebExceptionStatus.NameResolutionFailure: servicio de resolución de nombres de hello no pudo resolver el nombre de host de Hola.
   * ErrorCode.CiSApplianceACSError: indica que Hola servicio devolvió un error de autenticación, pero no hay conectividad.
     
     Si no se produce una excepción web, compruebe el elemento ErrorCode.CiSApplianceFailure. Esto indica un error de ese dispositivo Hola.
5. Compruebe la conectividad de servicio de nube de Hola. Si el servicio de hello inicia una excepción web, podría ver Hola siguientes errores:
   
   * ErrorCode.CiSApplianceGateway: indica una excepción de HttpStatusCode.BadGateway: un servidor proxy intermedio recibió una solicitud incorrecta de otro proxy o de servidor original de Hola.
   * ErrorCode.CiSApplianceProxy: indica una excepción de HttpStatusCode.ProxyAuthenticationRequired, con (código de estado HTTP 407): Hola cliente no pudo autenticar con el servidor de proxy de Hola. 
   * ErrorCode.CiSApplianceDNSError: indica una excepción de WebExceptionStatus.NameResolutionFailure: servicio de resolución de nombres de hello no pudo resolver el nombre de host de Hola.
   * ErrorCode.CiSApplianceACSError: indica que Hola servicio devolvió un error de autenticación, pero no hay conectividad.
     
     Si no se produce una excepción web, compruebe el elemento ErrorCode.CiSApplianceSaasServiceError. Esto indica un problema con el servicio StorSimple Manager Hola.
6. Compruebe la conectividad del Bus de servicio de Azure. ErrorCode.cisapplianceservicebuserror: indica que el dispositivo hello no puede conectarse toohello Bus de servicio.

Hola archivos de registro CiSCommandletLog0Curr.errlog y cisagentsvc0curr.errlog encontrará más información, como los detalles de la excepción. 

Para obtener más información acerca de cómo toouse Hola cmdlet, vaya demasiado[Test-HcsmConnection](https://technet.microsoft.com/library/dn715782.aspx) en Windows PowerShell Hola documentación de referencia.

> [!IMPORTANT]
> Puede ejecutar este cmdlet para hello activo y el controlador pasivo Hola. 
> 
> 

Vea Hola siguientes ejemplos de salida de hello `Test-HcsmConnection` cmdlet. 

**Ejemplo de salida: dispositivo registrado correctamente mediante la versión de StorSimple (julio de 2014)**

Hola primer ejemplo corresponde a un dispositivo que se ha registrado correctamente con el servicio StorSimple Manager hello y no tiene ningún problema de conectividad. 

     Controller1>Test-HcsmConnection -verbose
     Checking device state  ... Success.
     Device registered successfully
     Checking device authentication.  ... This operation will take few minutes toocomplete....
     Checking device authentication.  ... Success.
     Checking connectivity from device tooStorSimple Manager service.  ... This operation will take few minutes toocomplete....
     Checking connectivity from device tooStorSimple Manager service.  ... Success.
     Checking connectivity from StorSimple Manager service tooStorSimple device. .... Success.
     Controller1>

**Ejemplo de salida: dispositivo registrado correctamente mediante la actualización número 1 de StorSimple**

Si se ejecuta Update 1 en el dispositivo StorSimple, no necesitará toorun con el modificador verbose Hola.

      Controller1>Test-HcsmConnection

      Checking device registration state  ... Success
      Device registered successfully

      Checking primary NTP server [time.windows.com] ... Success

      Checking web proxy  ... NOT SET

      Checking primary IPv4 DNS server [10.222.118.154] ... Success
      Checking primary IPv6 DNS server  ... NOT SET
      Checking secondary IPv4 DNS server [10.222.120.24] ... Success
      Checking secondary IPv6 DNS server  ... NOT SET

      Checking device online  ... Success

      Checking device authentication  ... This will take a few minutes.
      Checking device authentication  ... Success

      Checking connectivity from device tooservice  ... This will take a few minutes.

      Checking connectivity from device tooservice  ... Success

      Checking connectivity from service toodevice  ... Success

      Checking connectivity tooMicrosoft Update servers  ... Success
      Controller1>

**Ejemplo de salida: dispositivo sin conexión que ejecuta la versión de StorSimple (julio de 2014)**

Este ejemplo es de un dispositivo que tiene un estado de **Offline** Hola portal de Azure clásico.

     Checking device state: Success 
     Device is registered successfully 
     Checking connectivity from device tooSaaS.. Failure

dispositivo de Hello no pudo conectarse usando la configuración del proxy web actual Hola. Podría tratarse de un problema con la configuración del proxy web Hola o un problema de conectividad de red. En este caso, debe asegurarse de que la configuración del proxy web es correcta y de que los servidores proxy web están en línea y accesibles. 

## <a name="troubleshoot-with-hello-sync-hcstime-cmdlet"></a>Solucionar problemas con el cmdlet de sincronización HcsTime Hola
Use esta hora del dispositivo cmdlet toodisplay Hola. Si la hora del dispositivo hello tiene un desfase con el servidor NTP hello, a continuación, puede usar este cmdlet tooforce-sincronizar la hora de hello con el servidor NTP. Si el desplazamiento de hello entre dispositivos de Hola y el servidor NTP es mayor que 5 minutos, aparecerá una advertencia. Si el desplazamiento de hello supera los 15 minutos, se desconectará dispositivo Hola. Todavía se puede usar este tooforce cmdlet una sincronización de hora. Sin embargo, si el desplazamiento de hello supera los 15 horas, a continuación, no será capaz de tooforce-sincronizar la hora de Hola y se mostrará un mensaje de error.

**Salida de ejemplo: sincronización de hora forzada mediante Sync-HcsTime**

     Controller0>Sync-HcsTime
     hello current device time is 4/24/2015 4:05:40 PM UTC.

     Time difference between NTP server and appliance is 00.0824069 seconds. Do you want tooresync time with NTP server?
     [Y] Yes [N] No (Default is "Y"): Y
     Controller0>

## <a name="troubleshoot-with-hello-enable-hcsping-and-disable-hcsping-cmdlets"></a>Solucionar problemas con los cmdlets de hello HcsPing habilitar y deshabilitar HcsPing
Use estos tooensure de cmdlets que interfaces de red de hello en el dispositivo responden las solicitudes de ping de tooICMP. De forma predeterminada interfaces de red de StorSimple de hello no responder las solicitudes de tooping. Con este cmdlet es hello tooknow de manera más fácil si el dispositivo está en línea y accesible.  

**Salida de ejemplo: Enable-HcsPing y Disable-HcsPing**

     Controller0>
     Controller0>Enable-HcsPing
     Successfully enabled ping.
     Controller0>
     Controller0>
     Controller0>Disable-HcsPing
     Successfully disabled ping.
     Controller0>

## <a name="troubleshoot-with-hello-trace-hcsroute-cmdlet"></a>Solucionar problemas con hello HcsRoute seguimiento cmdlet
Use este cmdlet como una herramienta de seguimiento de ruta. Envía el enrutador de tooeach de paquetes en el destino final de hello forma tooa durante un período de tiempo y, a continuación, calcula los resultados basándose en los paquetes de saludo devueltos en cada salto. Dado que hello muestra grado de Hola de pérdida de paquetes en un determinado vínculo o enrutador, puedes establecer claramente qué enrutadores o vínculos podrían estar causando problemas en la red.

**Salida de ejemplo que muestra cómo tootrace Hola ruta de un paquete con seguimiento HcsRoute**

     Controller0>Trace-HcsRoute -Target 10.126.174.25

     Tracing route toocontoso.com [10.126.174.25]
     over a maximum of 30 hops:
       0  HCSNode0 [10.126.173.90]
       1  contoso.com [10.126.174.25]

     Computing statistics for 25 seconds...
                 Source tooHere   This Node/Link
     Hop  RTT    Lost/Sent = Pct  Lost/Sent = Pct  Address
       0                                           HCSNode0 [10.126.173.90]
                                     0/ 100 =  0%   |
       1    0ms     0/ 100 =  0%     0/ 100 =  0%  contoso.com
      [10.126.174.25]

     Trace complete.

## <a name="troubleshoot-with-hello-get-hcsroutingtable-cmdlet"></a>Solucionar problemas con el cmdlet Get-HcsRoutingTable de Hola
Use esta tabla de enrutamiento de cmdlet tooview hello para el dispositivo StorSimple. Una tabla de enrutamiento es un conjunto de reglas que le pueden ayudar a determinar hacia dónde se dirigen los paquetes de datos transmitidos a través de una red de protocolo de Internet (IP). 

tabla de enrutamiento Hello muestra interfaces hello y puerta de enlace que rutas Hola datos toohello hello especificado redes. También ofrece la métrica de enrutamiento de Hola que es responsable de la decisión de Hola para hello tooreach de ruta de acceso que un destino concreto. Hola inferior Hola enrutamiento métrica, Hola Hola preferencia mayor. 

Por ejemplo, si tiene 2 interfaces de red, DATA 2 y DATA 3, toohello conectado Internet. Si la métrica de enrutamiento de Hola para DATA 2 y DATA 3 es 15 y 261 respectivamente, DATA 2 con la métrica de enrutamiento inferior hello es interfaz preferida de hello usa tooreach Hola Internet.

Si se ejecuta Update 1 en el dispositivo StorSimple, su interfaz de red 0 de datos tiene preferencia más alto de hello para el tráfico de nube de Hola. Esto significa que incluso si no hay otras interfaces habilitadas para la nube, tráfico de la nube de hello debería enrutarse a través de DATA 0. 

Si ejecuta hello `Get-HcsRoutingTable` cmdlet sin especificar ningún parámetro (como Hola siguiente ejemplo se muestra), Hola cmdlet mostrará las tablas de enrutamiento IPv4 e IPv6. Como alternativa, puede especificar `Get-HcsRoutingTable -IPv4` o `Get-HcsRoutingTable -IPv6` tooget una tabla de enrutamiento relevante.

      Controller0>
      Controller0>Get-HcsRoutingTable
      ===========================================================================
      Interface List
       14...00 50 cc 79 63 40 ......Intel(R) 82574L Gigabit Network Connection
       12...02 9a 0a 5b 98 1f ......Microsoft Failover Cluster Virtual Adapter
       13...28 18 78 bc 4b 85 ......HCS VNIC
        1...........................Software Loopback Interface 1
       21...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
       22...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #3
      ===========================================================================

      IPv4 Route Table
      ===========================================================================
      Active Routes:
      Network Destination        Netmask          Gateway       Interface  Metric
                0.0.0.0          0.0.0.0  192.168.111.100  192.168.111.101     15
              127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
              127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
        127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
            169.254.0.0      255.255.0.0         On-link     169.254.1.235    261
          169.254.1.235  255.255.255.255         On-link     169.254.1.235    261
        169.254.255.255  255.255.255.255         On-link     169.254.1.235    261
          192.168.111.0    255.255.255.0         On-link   192.168.111.101    266
        192.168.111.101  255.255.255.255         On-link   192.168.111.101    266
        192.168.111.255  255.255.255.255         On-link   192.168.111.101    266
              224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
              224.0.0.0        240.0.0.0         On-link     169.254.1.235    261
              224.0.0.0        240.0.0.0         On-link   192.168.111.101    266
        255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        255.255.255.255  255.255.255.255         On-link     169.254.1.235    261
        255.255.255.255  255.255.255.255         On-link   192.168.111.101    266
      ===========================================================================
      Persistent Routes:
        Network Address          Netmask  Gateway Address  Metric
                0.0.0.0          0.0.0.0  192.168.111.100       5
      ===========================================================================

      IPv6 Route Table
      ===========================================================================
      Active Routes:
       If Metric Network Destination      Gateway
        1    306 ::1/128                  On-link
       13    276 fd99:4c5b:5525:d80b::/64 On-link
       13    276 fd99:4c5b:5525:d80b::1/128
                                          On-link
       13    276 fd99:4c5b:5525:d80b::3/128
                                          On-link
       13    276 fe80::/64                On-link
       12    261 fe80::/64                On-link
       13    276 fe80::17a:4eba:7c80:727f/128
                                          On-link
       12    261 fe80::fc97:1a53:e81a:3454/128
                                          On-link
        1    306 ff00::/8                 On-link
       13    276 ff00::/8                 On-link
       12    261 ff00::/8                 On-link
       14    266 ff00::/8                 On-link
      ===========================================================================
      Persistent Routes:
        None

      Controller0>

## <a name="step-by-step-storsimple-troubleshooting-example"></a>Ejemplo de solución de problemas de StorSimple paso a paso
Hello en el ejemplo siguiente se muestra la solución de problemas detallada de una implementación de StorSimple. En el escenario de ejemplo de Hola, no se puede registrar de dispositivo con un mensaje de error que indica que la configuración de red de Hola o el nombre DNS de hello es incorrecta.

Hola mensaje de error devuelto es:

     Invoke-HcsSetupWizard: An error has occurred while registering hello device. This could be due tooincorrect IP address or DNS name. Please check your network settings and try again. If hello problems persist, contact Microsoft Support.
     +CategoryInfo: Not specified
     +FullyQualifiedErrorID: CiSClientCommunicationErros, Microsoft.HCS.Management.PowerShell.Cmdlets.InvokeHcsSetupWizardCommand

error de Hello podría deberse a cualquiera de hello siguientes:

* Instalación incorrecta de hardware
* Interfaces de red defectuosas
* Dirección IP, máscara de subred, puerta de enlace, servidor DNS principal o proxy web incorrectos
* Clave de registro incorrecta
* Configuración de firewall incorrecta

### <a name="toolocate-and-fix-hello-device-registration-problem"></a>toolocate y corregir el problema de registro de hello dispositivo
1. Compruebe la configuración del dispositivo: en hello controlador activo, ejecute `Invoke-HcsSetupWizard`.
   
   > [!NOTE]
   > Asistente para la instalación de Hello debe ejecutar en el controlador activo Hola. tooverify que están conectados toohello controlador activo, vistazo banner de Hola que aparece en la consola serie Hola. banner de Hello indica si se está conectado toocontroller 0 o controlador 1, y si el controlador de Hola es activo o pasivo. Para obtener más información, consulte demasiado[identificar un controlador activo en el dispositivo](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device).
   > 
   > 
2. Asegúrese de que dicho dispositivo Hola está conectado correctamente: compruebe Hola cable de red de plano posterior del dispositivo Hola. cableado de Hello es el modelo de dispositivo de toohello específico. Para obtener más información, consulte demasiado[instalar el dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md) o [instalar su dispositivo 8600 StorSimple](storsimple-8600-hardware-installation.md).
   
   > [!NOTE]
   > Si está utilizando puertos de red de 10 GbE, necesitará hello toouse proporciona adaptadores QSFP-SFP y cables SFP. Para obtener más información, vea hello [lista de cables, conmutadores y transceptores que recomienda para los puertos de hello 10 GbE](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
   > 
   > 
3. Comprobar estado de Hola Hola interfaz de red:
   
   * Usar mantenimiento Hola Get-NetAdapter cmdlet toodetect Hola Hola de interfaces de red para DATA 0. 
   * Si no funciona el vínculo de hello, Hola **ifindex** estado indicará esa interfaz Hola está inactivo. A continuación, deberá toocheck conexión de red de hello de dispositivo de toohello de puerto de Hola y toohello conmutador. También necesitará toorule out cables inadecuados. 
   * Si sospecha que DATA 0 error puerto en el controlador activo Hola Hola, puede confirmarlo conectándose toohello el puerto DATA 0 en el controlador 1. tooconfirm, desconecte el cable de red de Hola de hello parte posterior del dispositivo de Hola desde el controlador 0, conectar el cable de hello toocontroller 1 y, a continuación, ejecute de nuevo el cmdlet Get-NetAdapter Hola. 
     Si Hola DATA 0 se produce un error en el puerto en un controlador, [póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) para los pasos siguientes. Puede que tenga tooreplace controlador de hello en el sistema.
4. Compruebe el conmutador de hello conectividad toohello:
   
   * Asegúrese de que son interfaces de red 0 DATA controladores 0 y 1 del alojamiento principal en hello misma subred. 
   * Compruebe Hola concentrador o enrutador. Por lo general, debe conectar ambos controladores toohello mismo concentrador o enrutador. 
   * Asegúrese de que modificadores de Hola que utilizar para la conexión de hello tienen DATA 0 para ambos controladores en hello misma vLAN.
5. Elimine los errores de usuario:
   
   * Vuelva a ejecutar el Asistente para la instalación de hello (ejecutar **Invoke-HcsSetupWizard**) y escriba Hola nuevo valores toomake seguro de que no hay ningún error. 
   * Comprobar el registro de hello clave que se usa. Hola la misma clave de registro puede ser tooconnect usa varios dispositivos tooa el servicio StorSimple Manager. Utilice el procedimiento de hello en [clave de registro del servicio de Get hello](storsimple-manage-service.md#get-the-service-registration-key) tooensure que utilizas Hola clave de registro correcta.
     
     > [!IMPORTANT]
     > Si tiene varios servicios en ejecución, deberá tooensure esa clave de registro de hello para servicio adecuado de hello es dispositivo de hello tooregister usado. Si ha registrado un dispositivo con el servicio StorSimple Manager incorrecto hello, necesitará demasiado[póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) para los pasos siguientes. Es posible que tenga tooperform un restablecimiento de fábrica del dispositivo de hello (lo que podría resultar en pérdida de datos) toothen toohello pensado servicio conectarlo.
     > 
     > 
6. Utilice Hola Test-Connection cmdlet tooverify que dispone de conectividad toohello fuera de la red. Para obtener más información, consulte demasiado[solución de problemas con el cmdlet Test-Connection hello](#troubleshoot-with-the-test-connection-cmdlet).
7. Compruebe si existen interferencias de firewall. Si ha comprobado que Hola virtual es correcta la configuración de IP (VIP), subred, puerta de enlace y DNS y sigue teniendo problemas de conectividad, es posible que el firewall está bloqueando la comunicación entre el dispositivo y Hola fuera de la red. Debe tooensure que los puertos 80 y 443 están disponibles en el dispositivo de StorSimple para la comunicación saliente. Para obtener más información, consulte [Requisitos de red para el dispositivo StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
8. Examine los registros de Hola. Vaya demasiado[admite paquetes y registros de dispositivo disponibles para solucionar el problema](#support-packages-and-device-logs-available-for-troubleshooting).
9. Si hello pasos anteriores no resuelven el problema de hello, [póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) para obtener ayuda.

## <a name="next-steps"></a>Pasos siguientes
[Obtenga información acerca de cómo tootroubleshoot un dispositivo operativo](storsimple-troubleshoot-operational-device.md).

<!--Link references-->

[1]: https://technet.microsoft.com/library/dd379547(v=ws.10).aspx
[2]: https://technet.microsoft.com/library/dd392266(v=ws.10).aspx 
