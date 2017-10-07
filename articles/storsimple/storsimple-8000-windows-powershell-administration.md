---
title: "aaaPowerShell para la administración de dispositivos de StorSimple | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Windows PowerShell para StorSimple toomanage dispositivo StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/03/2017
ms.author: alkohli@microsoft.com
ms.openlocfilehash: e9e4bd025933cdef68b861d93749a107d1689536
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-for-storsimple-tooadminister-your-device"></a>Usar Windows PowerShell para StorSimple tooadminister el dispositivo

## <a name="overview"></a>Información general

Windows PowerShell para StorSimple proporciona una interfaz de línea de comandos que puede usar toomanage el dispositivo de StorSimple de Microsoft Azure. Como sugiere su nombre hello, es una interfaz de línea de comandos basado en Windows PowerShell, que se compila en un espacio de ejecución restringido. Desde la perspectiva de Hola de usuario de hello en línea de comandos de hello, un espacio de ejecución limitado aparece como una versión restringida de Windows PowerShell. Además de conservar algunas capacidades básicas de Hola de Windows PowerShell, esta interfaz tiene cmdlets adicionales específicamente orientados a la administración de su dispositivo de StorSimple de Microsoft Azure.

Este artículo describe Hola Windows PowerShell para características de StorSimple, incluido cómo puede conectarse toothis interfaz y contiene procedimientos paso a toostep de vínculos o flujos de trabajo que puede realizar con esta interfaz. los flujos de trabajo de Hello incluyen cómo la tooregister el dispositivo, configure la interfaz de red de hello en el dispositivo, instale actualizaciones que requieren hello toobe de dispositivo en modo de mantenimiento, cambie el estado del dispositivo hello, y solucionar los problemas que puede experimentar.

Después de leer este artículo, aprenderá a:

* Conecte el dispositivo de StorSimple tooyour mediante Windows PowerShell para StorSimple.
* Administrar el dispositivo StorSimple con Windows PowerShell para StorSimple.
* Obtener ayuda de Windows PowerShell para StorSimple.

> [!NOTE]
> * Windows PowerShell para StorSimple cmdlets le permiten toomanage dispositivo de StorSimple desde una consola serie o remotamente a través de comunicación remota de Windows PowerShell. Para obtener más información acerca de cada uno de los cmdlets individuales de Hola que puede usarse en esta interfaz, vaya demasiado[referencia de cmdlet de Windows PowerShell para StorSimple](https://technet.microsoft.com/library/dn688168.aspx).
> * cmdlets de PowerShell de Azure StorSimple Hola son un conjunto diferente de cmdlets que permiten tooautomate StorSimple de nivel de servicio y las tareas de migración de línea de comandos de Hola. Para obtener más información acerca de hello cmdlets de PowerShell de Azure para StorSimple, vaya toohello [referencia de cmdlets de Azure StorSimple](https://docs.microsoft.com/powershell/servicemanagement/azure.storsimple/v3.1.0/azure.storsimple).


Puede tener acceso a Hola Windows PowerShell para StorSimple mediante uno de los siguientes métodos de hello:

* [Conecte la consola serie del dispositivo tooStorSimple](#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)
* [Conectarse de forma remota tooStorSimple mediante Windows PowerShell](#connect-remotely-to-storsimple-using-windows-powershell-for-storsimple)

## <a name="connect-toowindows-powershell-for-storsimple-via-hello-device-serial-console"></a>Conectar tooWindows PowerShell para StorSimple a través de la consola serie del dispositivo Hola

También puede [descargar PuTTY](http://www.putty.org/) o similar tooWindows de tooconnect de software de emulación de terminales PowerShell para StorSimple. Necesita tooconfigure PuTTY específicamente tooaccess Hola dispositivo Microsoft Azure StorSimple. Hello en los temas siguientes contienen pasos detallados acerca de cómo tooconfigure PuTTy y conecte el dispositivo de toohello. También se explican varias opciones de menú de consola serie de Hola.

### <a name="putty-settings"></a>Configuración de PuTTY

Asegúrese de que utiliza Hola siguiendo la interfaz de Windows PowerShell de configuración PuTTY tooconnect toohello de consola serie de Hola.

#### <a name="tooconfigure-putty"></a>tooconfigure PuTTY

1. Hola PuTTY **reconfiguración** cuadro de diálogo hello **categoría** panel, seleccione **teclado**.
2. Asegúrese de que ese Hola siguientes opciones seleccionadas (son valores predeterminados de Hola cuando se inicia una nueva sesión).
   
   | Elemento de teclado | Seleccionar |
   | --- | --- |
   | Tecla retroceso |Control-? (127) |
   | Teclas de inicio y fin |Estándar |
   | Teclas de función y teclado numérico |ESC[n~ |
   | Estado inicial de las teclas de dirección |Normal |
   | Estado inicial del teclado numérico |Normal |
   | Habilitar las características de teclado adicionales |Control-Alt es diferente de AltGr |
   
    ![Configuración de Putty compatible](./media/storsimple-windows-powershell-administration/IC740877.png)
3. Haga clic en **Apply**.
4. Hola **categoría** panel, seleccione **traducción**.
5. Hola **juego de caracteres remotos** cuadro de lista, seleccione **UTF-8**.
6. En **Handling of line drawing characters** (Control de caracteres de dibujo de líneas), seleccione **Use Unicode line drawing code points** (Usar puntos de código de dibujo de líneas Unicode). Hello captura de pantalla siguiente muestra las selecciones de PuTTY correctas Hola.
   
    ![Configuración de Putty de UTF](./media/storsimple-windows-powershell-administration/IC740878.png)
7. Haga clic en **Apply**.

Ahora puede usar la consola serie del dispositivo de toohello tooconnect PuTTY haciendo Hola pasos.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="about-hello-serial-console"></a>Acerca de la consola serie Hola

Al tener acceso a la interfaz de Windows PowerShell de hello del dispositivo StorSimple a través de la consola serie hello, se presenta un mensaje de pancarta, y luego las opciones de menú.

mensaje de pancarta Hello contiene información básica de dispositivo de StorSimple como modelo hello, nombre, versión de software instalada y estado del controlador de Hola que está obteniendo acceso. Hola siguiente imagen muestra un ejemplo de un mensaje de pancarta.

![Mensaje de banner en serie](./media/storsimple-windows-powershell-administration/IC741098.png)

> [!IMPORTANT]
> Puede utilizar tooidentify de mensaje de pancarta Hola si Hola controlador se encuentra conectado toois _Active_ o _pasivo_.

siguiente imagen muestra de Hola Hola diversas opciones de espacio de ejecución que están disponibles en el menú de consola serie de Hola.

![Registrar el dispositivo 2](./media/storsimple-windows-powershell-administration/IC740906.png)

Puede elegir entre Hola después de configuración:

1. **Inicie sesión con acceso completo** esta opción le permite tooconnect (con las credenciales adecuadas de hello) toohello **SSAdminConsole** ejecución en Hola de controlador local. (Hola local es Hola controlador que está accediendo actualmente a través de la consola de serie de hello de dispositivo StorSimple.) Esta opción también puede utilizarse tooallow tooaccess Microsoft Support no restringido (una sesión de soporte técnico) del espacio de ejecución tootroubleshoot los posibles problemas del dispositivo. Después de usar la opción 1 toolog en, puede permitir el ingeniero de Microsoft Support Hola espacio de ejecución tooaccess sin restricciones mediante la ejecución de un cmdlet específico. Para obtener más información, consulte demasiado[iniciar una sesión de soporte técnico](storsimple-8000-contact-microsoft-support.md#start-a-support-session-in-windows-powershell-for-storsimple).
   
2. **Inicie sesión en el controlador toopeer con acceso total** esta opción es Hola igual que la opción 1, excepto en que puede conectarse (con las credenciales adecuadas de hello) toohello **SSAdminConsole** espacio de ejecución en el controlador de hello del mismo nivel. Dado que el dispositivo de StorSimple de hello es un dispositivo de alta disponibilidad con dos controladores en una configuración activo / pasivo, punto hace referencia toohello otro controlador de dispositivo de Hola que tiene acceso a través de la consola serie hello).
   Toooption similar 1, esta opción también puede ser usado tooallow espacio de ejecución de Microsoft Support tooaccess sin restricciones en un controlador del mismo nivel.

3. **Conectarse con acceso limitado** esta opción está tooaccess usa la interfaz de Windows PowerShell en modo limited. No se le solicitarán las credenciales de acceso. Esta opción conecta tooa más restringido en comparación con el espacio de ejecución toooptions 1 y 2.  Algunas de las tareas de Hola que están disponibles a través de la opción 1 que **no* realizarse en este espacio de ejecución son:
   
   * Restablecer la configuración de fábrica de toohello
   * Cambiar la contraseña de Hola
   * Habilitar o deshabilitar el acceso de soporte
   * Aplicar actualizaciones
   * Instalar revisiones

    > [!NOTE]
    > Esta es la opción de hello preferido si ha olvidado la contraseña de administrador de dispositivos de hello y no se puede conectar a través de la opción 1 o 2.

4. **Cambiar idioma** esta opción permite un idioma para mostrar en la interfaz de Windows PowerShell de hello toochange Hola. idiomas de Hello admitidos son inglés, japonés, ruso, francés, surcoreano, español, italiano, alemán, chino y portugués (Brasil).

## <a name="connect-remotely-toostorsimple-using-windows-powershell-for-storsimple"></a>Conectarse de forma remota tooStorSimple mediante Windows PowerShell para StorSimple

Puede usar el dispositivo de StorSimple de tooyour de tooconnect de comunicación remota de Windows PowerShell. Cuando se conecta de este modo, no verá un menú. (Verá un menú solo si usa la consola serie de hello en hello dispositivo tooconnect. Conecta de forma remota le lleva directamente toohello equivalente de "opción 1: acceso completo" en la consola serie Hola.) Con la comunicación remota de Windows PowerShell, conecte tooa espacio de ejecución específica. También puede especificar el idioma para mostrar hello.

Hello idioma para mostrar es independiente del idioma de Hola que establecen mediante hello **cambiar idioma** opción en el menú de consola serie de Hola. PowerShell remoto seleccionará automáticamente la configuración regional de hello de dispositivo de Hola que se conecta desde si no se especifica ninguno.

> [!NOTE]
> Si está trabajando con hosts virtuales de Microsoft Azure y aparatos de nube de StorSimple, puede usar Windows PowerShell hello y comunicación remota de host virtual tooconnect toohello dispositivo de nube. Si ha configurado una ubicación de recurso compartido en el host de hello en qué información toosave de sesión de Windows PowerShell de hello, deben tenerse en cuenta que hello _todos_ principal incluye solo los usuarios autenticados. Por lo tanto, si ha configurado acceso tooallow Hola por _todos los usuarios_ y se conecta sin especificar las credenciales, se usará principal anónimos no autenticados de Hola y verá un error. toofix este problema, en hello compartir host debe habilitar la cuenta de invitado de hello y, a continuación, asigne toohello participación de hello invitado cuenta acceso completo o debe especificar credenciales válidas junto con hello cmdlet de Windows PowerShell.


Puede usar tooconnect HTTP o HTTPS a través de comunicación remota de Windows PowerShell. Use las instrucciones de Hola Hola tutoriales:

* [Conectarse de forma remota mediante HTTP](storsimple-remote-connect.md#connect-through-http)
* [Conectarse de forma remota mediante HTTPS](storsimple-remote-connect.md#connect-through-https)

## <a name="connection-security-considerations"></a>Consideraciones de seguridad de conexión

Cuando decida cómo tooconnect tooWindows PowerShell para StorSimple, tenga en cuenta los siguiente hello:

* Conexión directa toohello consola serie del dispositivo es segura, pero conexión toohello de consola serie a través de conmutadores de red no lo es. Tenga cuidado Hola riesgo de seguridad al conectarse toodevice serie a través de conmutadores de red.
* Conexión a través de una sesión HTTP puede ofrecer más seguridad que se conectan a través de la consola serie de Hola a través de la red. Aunque esto no es el método más seguro de hello, es aceptable en redes de confianza.
* Conexión a través de una sesión HTTPS es más segura de Hola y Hola opción recomendada.

## <a name="administer-your-storsimple-device-using-windows-powershell-for-storsimple"></a>Administrar el dispositivo StorSimple con Windows PowerShell para StorSimple

Hello tabla siguiente muestra un resumen de todas las tareas de administración comunes de Hola y flujos de trabajo complejos que pueden realizarse dentro de la interfaz de Windows PowerShell de hello de dispositivo StorSimple. Para obtener más información sobre cada flujo de trabajo, haga clic en tabla de Hola la entrada adecuada de Hola.

#### <a name="windows-powershell-for-storsimple-workflows"></a>Flujos de trabajo de Windows PowerShell para StorSimple

| Si desea toodo esto... | Utilice este procedimiento. |
| --- | --- |
| Registrar el dispositivo |[Configurar y registrar dispositivo hello mediante Windows PowerShell para StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |
| Configurar el proxy web </br>Ver la configuración de proxy web |[Configurar el proxy web para el dispositivo StorSimple](storsimple-8000-configure-web-proxy.md) |
| Modificar la configuración de interfaz de red de DATA 0 en el dispositivo |[Modificar la configuración de interfaz de red de DATA 0 en el dispositivo](storsimple-8000-modify-data-0.md) |
| Detener un controlador  </br> Reiniciar o apagar un solo controlador </br> Apagar un dispositivo</br>Restablecer la configuración predeterminada de hello dispositivo toofactory |[Administrar controladores de dispositivo](storsimple-8000-manage-device-controller.md) |
| Instalar revisiones y actualizaciones de modo de mantenimiento |[Actualizar su dispositivo](storsimple-update-device.md) |
| Acceder al modo de mantenimiento  </br>Salir del modo de mantenimiento |[Modos del dispositivo StorSimple](storsimple-8000-device-modes.md) |
| Crear un paquete de soporte</br>Descifrar y editar un paquete de soporte |[Crear y administrar paquetes de soporte técnico](storsimple-8000-create-manage-support-package.md) |
| Iniciar una sesión de soporte</br> |[Iniciar una sesión de soporte en Windows PowerShell para StorSimple](storsimple-8000-create-manage-support-package.md#create-a-support-package) |

## <a name="get-help-in-windows-powershell-for-storsimple"></a>Obtener ayuda de Windows PowerShell para StorSimple

En Windows PowerShell para StorSimple, la Ayuda del cmdlet está disponible. Una versión actualizada en línea de esta Ayuda también está disponible, que se puede usar tooupdate Hola ayuda en el sistema.

Obtener ayuda en esta interfaz es toothat similar en Windows PowerShell, y la mayoría de hello cmdlets relacionados con la Ayuda funcionará. Puede encontrar ayuda de Windows PowerShell en línea en hello biblioteca de TechNet: [Scripting con Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=108518).

Hola aquí te mostramos una breve descripción de tipos de Hola de ayuda para esta interfaz de Windows PowerShell, incluido cómo tooupdate Hola ayuda.

### <a name="tooget-help-for-a-cmdlet"></a>Ayuda de tooget para un cmdlet

* tooget ayuda para cualquier cmdlet o una función, Hola de uso siguiente comando:`Get-Help <cmdlet-name>`
* tooget ayuda en línea sobre cualquier cmdlet, use el cmdlet anterior de hello con hello `-Online` parámetro:`Get-Help <cmdlet-name> -Online`
* Para obtener ayuda completa, puede usar hello `–Full` parámetro y para obtener ejemplos, usar hello `–Examples` parámetro.

### <a name="tooupdate-help"></a>tooupdate ayuda

Puede actualizar fácilmente Hola ayuda en la interfaz de Windows PowerShell de Hola. Realizar Hola siguiendo los pasos tooupdate Hola ayuda en el sistema.

#### <a name="tooupdate-cmdlet-help"></a>Ayuda del cmdlet tooupdate
1. Inicie Windows PowerShell con hello **ejecutar como administrador** opción.
2. En hello símbolo del sistema, escriba:`Update-Help`
3. Hola actualizado se instalarán los archivos de ayuda.
4. Una vez instalados los archivos de Ayuda de hello, escriba: `Get-Help Get-Command`. Esto mostrará una lista de cmdlets para que la Ayuda está disponible.

> [!NOTE]
> tooget una lista de todos los cmdlets disponibles de hello en un espacio de ejecución, inicie sesión en la opción de menú correspondiente toohello y ejecute hello `Get-Command` cmdlet.


## <a name="next-steps"></a>Pasos siguientes

Si experimenta problemas con el dispositivo de StorSimple al realizar uno de Hola por encima de los flujos de trabajo, consulte demasiado[herramientas para solucionar problemas en implementaciones de StorSimple](storsimple-troubleshoot-deployment.md#tools-for-troubleshooting-storsimple-deployments).

