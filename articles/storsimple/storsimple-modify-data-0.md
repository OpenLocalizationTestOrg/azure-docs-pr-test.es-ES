---
title: "Hola aaaModify DATA 0 configuración en un dispositivo StorSimple | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Windows PowerShell para StorSimple tooreconfigure Hola datos interfaz de red 0 en el dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 58e3d509-f425-4a7f-b650-d496a7c85193
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: caec51c3344d953299253301c2a0d7577d553c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-device"></a>Modificar la configuración de interfaz de red 0 Hola datos en el dispositivo StorSimple
## <a name="overview"></a>Información general
El dispositivo de StorSimple de Microsoft Azure tiene seis interfaces de red, desde DATA 0 tooDATA 5. Hola DATA 0 interfaz siempre se configura mediante la interfaz de Windows PowerShell de Hola o de consola serie de Hola y está habilitada para la nube automáticamente. Tenga en cuenta que no se puede configurar la interfaz de red 0 de datos a través de hello portal de Azure clásico. 

Hola DATA 0 interfaz primero se configura a través del Asistente para la instalación de Hola durante la implementación inicial de dispositivo de StorSimple Hola. Cuando el dispositivo de hello está en un modo de funcionamiento, puede que necesite tooreconfigure DATA 0 configuración. Este tutorial proporciona dos métodos de configuración de red 0 datos toomodify, tanto a través de Windows PowerShell para StorSimple.

Después de leer este tutorial, podrá:

* Modificar datos 0 los valores a través del Asistente para la instalación de Hola de red
* Modificar la configuración de red 0 de datos a través de hello `Set-HcsNetInterface` cmdlet

## <a name="modify-data-0-network-settings-through-setup-wizard"></a>Modificar la configuración de red de DATA 0 mediante el asistente para la instalación
Puede volver a configurar la configuración de red 0 de datos por conexión toohello de interfaz de Windows PowerShell del dispositivo StorSimple e iniciar una sesión del Asistente de instalación. Realizar Hola siguiendo los pasos toomodify DATA 0 configuración:

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a>configuración de red 0 toomodify datos a través del Asistente para la instalación
1. En el menú de consola serie de hello, elija la opción 1, **iniciar sesión con acceso completo**. Cuando se le solicite proporcionar hello **contraseña de administrador de dispositivo**. contraseña de Hello predeterminada es `Password1`.
2. En hello símbolo del sistema, escriba:
   
    `Invoke-HcsSetupWizard`
3. Se mostrará un asistente de instalación toohelp configurar Hola DATA 0 interfaz del dispositivo. Proporcione nuevos valores para la máscara de red, la puerta de enlace y la dirección IP de Hola.

> [!NOTE]
> Hola fijo controladores IP necesitará toobe volver a configurar a través de hello **configurar** página del dispositivo de StorSimple de Hola Hola portal de Azure clásico. Para obtener más información, consulte demasiado[modificar interfaces de red](storsimple-modify-device-config.md#modify-network-interfaces).
> 
> 

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a>Modificación de la configuración de red de DATA 0 mediante el cmdlet Set-HcsNetInterface
Un tooreconfigure de forma alternativa DATA 0 es de interfaz de red mediante el uso de Hola de hello `Set-HcsNetInterface` cmdlet. Hola cmdlet se ejecuta desde la interfaz de Windows PowerShell de hello de dispositivo StorSimple. Cuando se utiliza este procedimiento, IP fijas del controlador hello también pueden configurarse aquí. Realizar Hola siguiendo los pasos toomodify Hola DATA 0 configuración: 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a>configuración de red 0 toomodify datos a través del cmdlet Set-HcsNetInterface Hola
1. En el menú de consola serie de hello, elija la opción 1, **iniciar sesión con acceso completo**. Cuando se le solicite proporcionar la contraseña de administrador de dispositivos de Hola. contraseña de Hello predeterminada es `Password1`.
2. En hello símbolo del sistema, escriba:
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    Hola en ángulo corchetes, escriba Hola sigue valores para DATA 0:
   
   * Dirección IPv4
   * Puerta de enlace IPv4
   * Máscara de subred IPv4
   * Dirección IPv4 fija para el controlador 0
   * Dirección IPv4 fija para el controlador 1
     
     Para obtener más información sobre el uso de Hola de este cmdlet, vaya demasiado[de Windows PowerShell para StorSimple referencia del cmdlet](https://technet.microsoft.com/library/dn688161.aspx).

## <a name="next-steps"></a>Pasos siguientes
* interfaces de red tooconfigure diferentes a DATA 0, puede usar hello [página de configuración en el portal de Azure clásico hello](storsimple-modify-device-config.md). 
* Si experimenta problemas al configurar las interfaces de red, consulte demasiado[solucionar problemas de implementación](storsimple-troubleshoot-deployment.md).

