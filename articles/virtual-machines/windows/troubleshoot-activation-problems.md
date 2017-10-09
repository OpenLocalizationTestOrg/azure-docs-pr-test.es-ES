---
title: "aaaTroubleshoot problemas de activación de máquina virtual de Windows en Azure | Documentos de Microsoft"
description: "Proporciona Hola solucionar pasos para solucionar problemas de activación de máquina virtual de Windows en Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 4ebdac66166e80dcd68cd9e2931b30a29ac01eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a>Solución de problemas de activación de máquinas virtuales Windows de Azure

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Si tienes algún problema al activar la máquina de virtual de Windows Azure (VM) que se crea a partir de una imagen personalizada, puede usar información de hello proporcionada en este problema de hello tootroubleshoot de documento. 

## <a name="symptom"></a>Síntoma

Cuando intente tooactivate una VM de Windows Azure, recibirá un error mensaje es similar a Hola según muestra:

**Error: Hola 0xC004F074 LicensingService de Software informó de que ese equipo hello no se pudo activar. No Key ManagementService (KMS) could be contacted. Vea Hola registro de eventos de aplicación para obtener información adicional.**

## <a name="cause"></a>Causa
Por lo general, problemas de activación de la máquina virtual de Azure ocurrir si Hola VM de Windows no está configurada de utilizando Hola correspondiente clave de configuración de cliente KMS u Hola VM de Windows tiene un toohello de problema de conectividad servicio de KMS de Azure (kms.core.windows.net, puerto 1668). 

## <a name="solution"></a>Solución

>[!NOTE]
>Si está usando una VPN de sitio a sitio y forzar el túnel, vea [Use Azure personalizado enruta tooenable activación de KMS con la tunelización forzada](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx). 
>
>Si usas ExpressRoute y tiene una ruta predeterminada publica, vea [máquina virtual de Azure puede conmutar por error tooactivate ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).

### <a name="step-1-configure-hello-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a>Paso 1 Configurar Hola clave KMS apropiada cliente el programa de instalación (para Windows Server 2016 y Windows Server 2012 R2)

Para hello máquina virtual que se crea a partir de una imagen personalizada de Windows Server 2016 o Windows Server 2012 R2, debe configurar Hola clave KMS apropiada cliente el programa de instalación para hello máquina virtual.

Este paso no aplica tooWindows 2012 o Windows 2008 R2. Usa la característica de activación de automatización de la máquina Virtual (AVMA) de hello, que solo es compatible con Windows Server 2016 y Windows Server 2012 R2.

1. Ejecute **slmgr.vbs /dlv** en un símbolo del sistema con privilegios elevados. Compruebe Hola valor de descripción en la salida de hello y, a continuación, determine si se creó desde comercial (canal MINORISTA) o medios de licencias por volumen (VOLUME_KMSCLIENT):
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. Si **slmgr.vbs /dlv** muestra canal MINORISTA, ejecute hello después Hola de comandos tooset [clave de configuración de cliente KMS](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) para la versión de Hola de Windows Server se utiliza y obligarlo tooretry activación: 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    Por ejemplo, para Windows Server 2016 Datacenter, ejecutaría Hola siguiente comando:

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-hello-connectivity-between-hello-vm-and-azure-kms-service"></a>Paso 2 Compruebe la conectividad de hello entre Hola VM y el servicio de KMS de Azure

1. Descargue y extraiga hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) carpeta local de herramienta tooa Hola VM que no lo activa. 

2. Paso tooStart, buscar en Windows PowerShell, haga clic en Windows PowerShell y, a continuación, seleccione Ejecutar como administrador.

3. Asegúrese de que ese hello en la que máquina virtual está configurado el servidor de KMS de Azure correcta de toouse Hola. toodo esto, ejecute el siguiente comando:
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    Hola comando debe devolver: nombre del equipo de servicio de administración de claves establece tookms.core.windows.net:1688 correctamente.

4. Comprobar mediante Psping que dispone de conectividad toohello KMS servidor. Cambiar carpeta toohello donde extrajo descarga Pstools.zip de hello y, a continuación, ejecute el siguiente de hello:
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  En línea de segundo al último de Hola de salida de hello, asegúrese de que ve: enviados = 4, recibidos = 4, perdidos = 0 (0% perdidos).

  Si pierde es mayor que 0 (cero), Hola VM no tiene servidor KMS de toohello de conectividad. En esta situación, si hello máquina virtual está en una red virtual y se un servidor DNS personalizado especificado, debe asegurarse de que ese servidor DNS es capaz de tooresolve kms.core.windows.net. O bien, cambiar Hola DNS server tooone que resolver kms.core.windows.net.

  Tenga en cuenta que si quita todos los servidores DNS de una red virtual, las máquinas virtuales usan el servicio DNS interno de Azure. Este servicio pude resolver kms.core.windows.net.
  
Compruebe también que firewall de invitado hello no se configuró de forma que bloquearía los intentos de activación.

5. Después de comprobar la conectividad correcta tookms.core.windows.net, ejecute hello siguiente comando en ese símbolo del sistema con privilegios elevados de Windows PowerShell. Este comando intenta la activación varias veces.

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

Una activación correcta devuelve información similar a Hola siguiente:

**Activación de Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … El producto se activó correctamente.**

## <a name="faq"></a>P+F 

### <a name="i-created-hello-windows-server-2016-from-azure-marketplace-do-i-need-tooconfigure-kms-key-for-activating-hello-windows-server-2016"></a>He creado Hola Windows Server 2016 de Azure Marketplace. ¿Es necesario tooconfigure clave KMS para activar Hola Windows Server 2016? 
 
No. imagen de Hello en Azure Marketplace tiene Hola clave KMS apropiada cliente el programa de instalación ya configurado. 

### <a name="does-windows-activation-work-hello-same-way-regardless-if-hello-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a>¿Trabajo de activación de Windows hello misma forma independientemente si Hola VM está usando Azure híbrida uso beneficio (centro) o no? 
 
Sí. 
 
### <a name="what-happens-if-windows-activation-period-expires"></a>¿Qué sucede si el período de activación de Windows expira? 
 
Cuando ha expirado el período de gracia de Hola y Windows no está activado todavía, Windows Server 2008 R2 y versiones posteriores de Windows mostrará notificaciones adicionales sobre la activación. papel tapiz del escritorio Hola permanece negro y Windows Update se instalará la seguridad y actualizaciones críticas únicamente, pero las actualizaciones opcionales no. Vea las notificaciones de hello sección final Hola de hello [condiciones de licencias](http://technet.microsoft.com/en-us/library/ff793403.aspx) página.   

## <a name="need-help-contact-support"></a>¿Necesita ayuda? Póngase en contacto con el servicio de soporte técnico.
Si aún necesita ayuda, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget rápidamente para solucionar el problema.
