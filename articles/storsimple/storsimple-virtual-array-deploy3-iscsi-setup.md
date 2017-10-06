---
title: "instalación de servidor de iSCSI de Azure StorSimple Virtual Array aaaMicrosoft | Documentos de Microsoft"
description: "Describe cómo registrar el servidor de iSCSI de StorSimple tooperform la instalación inicial y complete el programa de instalación de dispositivos."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4db116d1-978b-48e8-b572-a719a8425dbc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: b4ff6391cb2af69d4e83dcdac5e027f8498005b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array--set-up-as-an-iscsi-server-via-azure-portal"></a>Implementación de una matriz virtual de StorSimple: configurar como un servidor iSCSI mediante Azure Portal

![flujo del proceso de configuración de iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/iscsi4.png)

## <a name="overview"></a>Información general

Este tutorial de implementación aplica toohello Microsoft Azure StorSimple Virtual Array. Este tutorial describe cómo tooperform instalación inicial de hello, registrar el servidor de iSCSI de StorSimple, configuración de dispositivo de hello completa y, a continuación, crear, montar, inicializar y formatear volúmenes en la matriz Virtual de StorSimple configurado como un servidor de iSCSI. 

procedimientos de Hello descritos aquí tardar aproximadamente 30 minutos too1 hora toocomplete. información de Hello publicada en este artículo aplica tooStorSimple arreglos de discos virtuales.

## <a name="setup-prerequisites"></a>Requisitos previos de instalación

Antes de instalar y configurar StorSimple Virtual Array, asegúrese de que:

* Está aprovisionado una matriz virtual y tooit tal y como se describe en [implementar StorSimple Virtual Array - aprovisionar una matriz virtual de Hyper-V](storsimple-ova-deploy2-provision-hyperv.md) o [implementar StorSimple Virtual Array - aprovisionar una matriz virtual de VMware ](storsimple-virtual-array-deploy2-provision-vmware.md).
* Tiene la clave de registro del servicio de Hola de Hola que creaste toomanage los arreglos de discos virtuales de StorSimple de servicio de administrador de dispositivos de StorSimple. Para obtener más información, consulte **paso 2: clave de registro del servicio de Get hello** en [implementar StorSimple Virtual Array - Prepare portal hello](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).
* Si se trata de hello segunda o posteriores matriz virtual que va a registrar con un servicio de administrador de dispositivos de StorSimple existente, debe tener la clave de cifrado de datos del servicio de Hola. Esta clave se generó al primer dispositivo de Hola se registró correctamente con este servicio. Si se pierde esta clave, consulte **clave de cifrado de datos del servicio de Get hello** en [uso Hola tooadminister de interfaz de usuario Web de la matriz Virtual de StorSimple](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key).

## <a name="step-by-step-setup"></a>Configuración paso a paso

Usar hello seguimiento tooset instrucciones paso a paso una y configure la matriz Virtual de StorSimple:

* [Paso 1: Completar web local de hello el programa de instalación de la interfaz de usuario y registrar el dispositivo](#step-1-complete-the-local-web-ui-setup-and-register-your-device)
* [Paso 2: Hola completa requiere configuración de dispositivo](#step-2-complete-the-required-device-setup)
* [Paso 3: Agregar un volumen](#step-3-add-a-volume)
* [Paso 4: Montar, inicializar y formatear un volumen](#step-4-mount-initialize-and-format-a-volume)

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a>Paso 1: Completar web local de hello el programa de instalación de la interfaz de usuario y registrar el dispositivo

#### <a name="toocomplete-hello-setup-and-register-hello-device"></a>toocomplete Hola el programa de instalación y registrar un dispositivo Hola

1. Abra una ventana del explorador. tooconnect toohello web tipo de interfaz de usuario:
   
    `https://<ip-address of network interface>`
   
    Use la dirección URL de conexión de hello anotada en el paso anterior de Hola. Verá un error que le notifica que hay un problema con el certificado de seguridad del sitio Web de Hola. Haga clic en **continuar toothis web página**.
   
    ![error de certificado de seguridad](./media/storsimple-virtual-array-deploy3-iscsi-setup/image3.png)
2. Interfaz de usuario del dispositivo virtual como web de inicio de sesión toohello **StorSimpleAdmin**. Escriba la contraseña del Administrador de dispositivos de Hola que cambió en el paso 3: dispositivo virtual de inicio hello en [implementar StorSimple Virtual Array - aprovisionar un dispositivo virtual de Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) o [implementar StorSimple Virtual Array - Aprovisionar un dispositivo virtual de VMware](storsimple-virtual-array-deploy2-provision-vmware.md).
   
    ![Página de inicio de sesión](./media/storsimple-virtual-array-deploy3-iscsi-setup/image4.png)
3. Se le llevará toohello **inicio** página. Esta página describe Hola varias opciones de configuración necesarias tooconfigure y registrar Hola dispositivo virtual con el servicio de administrador de dispositivos de StorSimple Hola. Tenga en cuenta que hello **configuración de red**, **configuración de proxy Web**, y **configuración de tiempo** son opcionales. Hola solo requiere configuración **configuración de dispositivo** y **configuración de nube**.
   
    ![Página de inicio](./media/storsimple-virtual-array-deploy3-iscsi-setup/image5.png)
4. En hello **configuración de red** página en **interfaces de red**, DATA 0 se configurarán automáticamente para usted. Cada interfaz de red se establece por tooget de forma predeterminada una dirección IP automáticamente (DHCP). Por lo tanto, una dirección IP, una subred y una puerta de enlace se asignarán automáticamente (tanto para IPv4 como para IPv6).
   
    Mientras planea toodeploy el dispositivo como un servidor de iSCSI (almacenamiento en bloque tooprovision), le recomendamos que deshabilite hello **obtener dirección IP automáticamente** opción y configurar direcciones IP estáticas.
   
    ![Página de configuración de red](./media/storsimple-virtual-array-deploy3-iscsi-setup/image6.png)
   
    Si agrega más de una interfaz de red durante el aprovisionamiento de hello de dispositivo de hello, se pueden configurar aquí. Tenga en cuenta que puede configurar la interfaz de red como IPv4 únicamente o como IPv4 e IPv6. No se admiten las configuraciones de solo IPv6.
5. Servidores DNS son necesarios, ya que se utilizan cuando el dispositivo intenta toocommunicate con los proveedores de servicios de almacenamiento de nube o tooresolve el dispositivo por su nombre si se configura como un servidor de archivos. En hello **configuración de red** página en hello **servidores DNS**:
   
   1. Se configurarán automáticamente un servidor DNS principal y secundario. Si elige tooconfigure direcciones IP estáticas, puede especificar servidores DNS. Para lograr la alta disponibilidad, se recomienda que configure un servidor DNS principal y uno secundario.
   2. Haga clic en **Apply**. Esto aplicará y validar la configuración de red de Hola.
6. En hello **configuración de dispositivo** página:
   
   1. Asignar un único **nombre** tooyour dispositivo. Este nombre puede tener de 1 a 15 caracteres y puede contener letras, números y guiones.
   2. Haga clic en hello **servidor iSCSI** icono ![el icono del servidor de iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/image7.png) para hello **tipo** de dispositivo que está creando. Un servidor de iSCSI le permitirá tooprovision almacenamiento en bloque.
   3. Especificar si desea que este dispositivo toobe Unidos a un dominio. Si el dispositivo es un servidor de iSCSI, a continuación, unirse a dominio hello es opcional. Si decide toonot combinación su dominio de tooa del servidor de iSCSI, haga clic en **aplicar**, espere Hola configuración toobe aplicado y, a continuación, omita el paso siguiente de toohello.
      
       Si desea que los dominios de tooa toojoin Hola dispositivo. Escriba un **nombre de dominio** y, después, haga clic en **Aplicar**.
      
      > [!NOTE]
      > Si va a unir el dominio tooa del servidor de iSCSI, asegúrese de que la matriz virtual está en su propia unidad organizativa (OU) de Microsoft Azure Active Directory y ningún objeto de directiva de grupo (GPO) son tooit aplicada.
      > 
      > 
   4. Aparece un cuadro de diálogo. Escriba sus credenciales de dominio en formato de hello especificado. Haga clic en el icono de verificación de Hola ![icono de marca de verificación](./media/storsimple-virtual-array-deploy3-iscsi-setup/image15.png). se comprobará las credenciales de dominio de Hola. Verá un mensaje de error si Hola credenciales son incorrectas.
      
       ![credentials](./media/storsimple-virtual-array-deploy3-iscsi-setup/image8.png)
   5. Haga clic en **Apply**. Esto aplicará y validar la configuración de dispositivo de Hola.
7. Configure el servidor proxy web (de manera opcional). Aunque la configuración del proxy web es opcional, tenga en cuenta que, si usa un proxy web, solo puede configurarlo aquí.
   
    ![configurar el proxy web](./media/storsimple-virtual-array-deploy3-iscsi-setup/image9.png)
   
    En hello **proxy Web** página:
   
   1. Fuente de alimentación hello **dirección URL del proxy Web** en este formato: *http://host-IP dirección* o *FDQN:Port número*. Tenga en cuenta que no se admiten direcciones URL HTTPS.
   2. Especifique **Autenticación** como **Básica** o **Ninguna**.
   3. Si usa la autenticación, también necesitará tooprovide una **nombre de usuario** y **contraseña**.
   4. Haga clic en **Apply**. Esto se valide y aplicar la configuración de proxy web de hello configurado.
8. (Opcional) configurar las opciones de tiempo de hello para el dispositivo, como la zona horaria y Hola servidores NTP principal y secundarios. Se requieren servidores NTP, ya que el dispositivo debe sincronizar la hora para que pueda autenticarse con los proveedores de servicios en la nube.
   
    ![Time settings](./media/storsimple-virtual-array-deploy3-iscsi-setup/image10.png)
   
    En hello **configuración de tiempo** página:
   
   1. Desde la lista desplegable de hello, seleccione hello **zona horaria** basadas en ubicación geográfica de hello en qué Hola se va a implementar el dispositivo. zona de horaria predeterminada de Hello para el dispositivo es PST. El dispositivo usará esta zona horaria para todas las operaciones programadas.
   2. Especifique un **servidor NTP principal** para el dispositivo o acepte el valor predeterminado de Hola de time.windows.com. Asegúrese de que su red permite toopass de tráfico NTP desde su toohello de centro de datos Internet.
   3. Opcionalmente, especifique un **servidor NTP secundario** para el dispositivo.
   4. Haga clic en **Apply**. Esto se valide y aplicar la configuración de tiempo de hello configurado.
9. Configurar opciones de nube de hello para el dispositivo. En este paso, se complete la configuración del dispositivo local de hello y, a continuación, registrar dispositivo Hola con el servicio de administrador de dispositivos de StorSimple.
   
   1. Escriba hello **clave de registro del servicio** que obtuvo **paso 2: clave de registro del servicio de Get hello** en [implementar StorSimple Virtual Array - preparar Hola Portal](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).
   2. Si esto no es dispositivo primera Hola que va a registrar con este servicio, deberá hello tooprovide **clave de cifrado de datos de servicio**. Esta clave es necesaria con hello servicio Registro tooregister clave dispositivos adicionales con hello servicio Administrador de dispositivos de StorSimple. Para obtener más información, consulte demasiado[clave de cifrado de datos del servicio de Get hello](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) en local de interfaz de usuario web.
   3. Haga clic en **Registrar**. Esto reiniciará el dispositivo de Hola. Puede que tenga toowait de 2 a 3 minutos antes de que se ha registrado correctamente el dispositivo de Hola. Una vez reiniciado el dispositivo de hello, se le llevará toohello inicio de sesión en la página.
      
      ![Registrar dispositivo](./media/storsimple-virtual-array-deploy3-iscsi-setup/image11.png)
10. Devolver toohello portal de Azure.
11. Navegue toohello **dispositivos** hoja de su servicio. Si tiene muchos de recursos, haga clic en **Todos los recursos**, haga clic en el nombre del servicio (búsquelo si fuera necesario) y, después, en **Dispositivos**.
12. En hello **dispositivos** hoja, compruebe que dicho dispositivo Hola se ha conectado correctamente toohello servicio consultando el estado de Hola. estado de dispositivo de Hello debe ser **listo tooset seguridad**.
    
    ![Registrar dispositivo](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png)

## <a name="step-2-configure-hello-device-as-iscsi-server"></a>Paso 2: Configurar dispositivo hello como servidor de iSCSI

Realizar Hola pasos de hello el programa de instalación de dispositivo de Azure toocomplete portal Hola necesario.

#### <a name="tooconfigure-hello-device-as-iscsi-server"></a>dispositivo de hello tooconfigure como servidor de iSCSI

1. Servicio de administrador de dispositivos de StorSimple tooyour go y, a continuación, vaya demasiado**Administración > dispositivos**. Hola **dispositivos** hoja, un dispositivo de hello select que acaba de crear. Este dispositivo se mostrará como **listo tooset seguridad**.
   
    ![Configurar dispositivo como servidor iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png) 
2. Haga clic en el dispositivo de Hola y verá un mensaje de pancarta que indica que el dispositivo hello es toosetup listo.
   
    ![Configurar dispositivo como servidor iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis2m.png)  
3. Haga clic en **configurar** en la barra de comandos de dispositivo de Hola. Esto abrirá hello **configurar** hoja. Hola **configurar** hoja, Hola siguientes:
   
   * nombre del servidor iSCSI Hola se rellena automáticamente.
   * Asegúrese de que el cifrado de almacenamiento en nube Hola se establece demasiado**habilitado**. Esto garantiza que los datos de hello enviados desde el dispositivo de la nube toohello Hola estén cifrados.
   * Especifique una clave de cifrado de 32 caracteres y regístrela en una aplicación de administración de claves para futuras referencias.
   * Seleccione un toobe de cuenta de almacenamiento utilizada con su dispositivo. En esta suscripción, puede seleccionar una cuenta de almacenamiento existente, o puede hacer clic en **agregar** toochoose una cuenta de otra suscripción.
     
     ![Configurar dispositivo como servidor iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis4m.png)
4. Haga clic en **configurar** toocomplete al configurar el servidor de iSCSI Hola.
   
    ![Configurar dispositivo como servidor iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis5m.png) 
5. Se le notificará que la creación del servidor iSCSI Hola está en curso. Después de crea correctamente el servidor de iSCSI de hello, Hola **dispositivos** hoja se actualiza y estado del dispositivo correspondiente hello es **Online**.
   
    ![Configurar dispositivo como servidor iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis9m.png)

## <a name="step-3-add-a-volume"></a>Paso 3: Agregar un volumen

1. Hola **dispositivos** hoja, un dispositivo de hello seleccione recién configurado como un servidor de iSCSI. Haga clic en **...**  (o bien pulse el botón derecho en esta fila) y en el menú contextual de hello, seleccione **agregar volumen**. También puede hacer clic en **+ agregar volumen** de barra de comandos de Hola. Esto abrirá hello **agregar volumen** hoja.
   
    ![Agregar un volumen](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis10m.png)
2. Hola **agregar volumen** hoja, Hola siguientes:
   
   * Hola **nombre del volumen** , a continuación, escriba un nombre único para su volumen. nombre de Hello debe ser una cadena que contiene 3 too127 caracteres.
   * Hola **tipo** lista desplegable lista, especifique si toocreate una **"en capas"** o **anclado localmente** volumen. Para las cargas de trabajo que requieren garantías locales, latencias bajas y un rendimiento más alto, seleccione **Volumen anclado** **localmente**. Para todos los demás datos, seleccione **Volumen** **en capas**.
   * Hola **capacidad** , especifique el tamaño de hello del volumen de Hola. Un volumen en capas debe tener entre 500 GB y 5 TB, mientras que un volumen anclado localmente debe oscilar entre 50 GB y 500 GB.
     
     Un volumen anclado localmente se realiza un aprovisionamiento grueso y asegura que los datos principal de hello en volumen de hello permanece en el dispositivo de hello y no volcarse toohello en la nube.
     
     Un volumen en capas en hello con aprovisionamiento fino otra parte. Cuando se crea un volumen en capas, aproximadamente el 10% del espacio de Hola se aprovisionó en nivel local hello y 90% del espacio de Hola se aprovisiona en nube Hola. Por ejemplo, si ha aprovisionado un volumen de 1 TB, 100 GB residiría en el espacio local hello y 900 GB se utilizaría en nube Hola Hola cuando capas de datos. A su vez, esto implica es que si se queda sin espacio local en todos los hello en dispositivo hello, no se puede aprovisionar un recurso compartido en capas (ya no estará disponible Hola 10%).
     
     ![Agregar un volumen](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis12.png)
   * Haga clic en **hosts conectados**, seleccione un acceso control registro (ACR) correspondiente toohello iniciador iSCSI que desee tooconnect toothis volumen y, a continuación, haga clic en **seleccione**. <br><br> 
3. tooadd un nuevo host conectado, haga clic en **agregar nueva**, escriba un nombre de host de Hola y su iSCSI (IQN) nombre completo y, a continuación, haga clic en **agregar**. Si no tienes Hola IQN, vaya demasiado[Apéndice A: obtener Hola IQN de un host de Windows Server](#appendix-a-get-the-iqn-of-a-windows-server-host).
   
      ![Agregar un volumen](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis15m.png)
4. Cuando haya terminado de configurar el volumen, haga clic en **Aceptar**. Se creará un volumen con hello especificado configuración y verá una notificación. De forma predeterminada, se habilitará para el volumen de hello supervisión y copia de seguridad.
   
     ![Agregar un volumen](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis18m.png)
5. tooconfirm que Hola volumen estaba se creó correctamente, vaya toohello **volúmenes** hoja. Debería ver los volúmenes de Hola que aparecen.
   
   ![Agregar un volumen](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis20m.png)

## <a name="step-4-mount-initialize-and-format-a-volume"></a>Paso 4: Montar, inicializar y formatear un volumen

Realizar Hola siguientes pasos toomount, inicializar y dar formato a los volúmenes de StorSimple en un host de Windows Server.

#### <a name="toomount-initialize-and-format-a-volume"></a>toomount, inicializar y formatear un volumen

1. Abra hello **iniciador iSCSI** aplicación en el servidor adecuado Hola.
2. Hola **propiedades del iniciador iSCSI** ventana hello **detección** , haga clic en **detectar Portal**.
   
    ![Detectar portal](./media/storsimple-virtual-array-deploy3-iscsi-setup/image22.png)
3. Hola **detectar Portal de destino** cuadro de diálogo, proporcione la dirección IP de saludo de la interfaz de red habilitada para iSCSI y, a continuación, haga clic en **Aceptar**.
   
    ![Dirección IP](./media/storsimple-virtual-array-deploy3-iscsi-setup/image23.png)
4. Hola **propiedades del iniciador iSCSI** ventana hello **destinos** pestaña, busque hello **detectados destinos**. (Cada volumen será un destino detectado). estado del dispositivo Hola debe aparecer como **inactivo**.
   
    ![Destinos detectados](./media/storsimple-virtual-array-deploy3-iscsi-setup/image24.png)
5. Seleccione un dispositivo de destino y luego haga clic en **Conectar**. Después de conecta el dispositivo de hello, estado de hello debería cambiar demasiado**conectado**. (Para obtener más información acerca del uso del iniciador iSCSI de Microsoft hello, consulte [iniciador iSCSI de instalar y configurar Microsoft][1].
   
    ![seleccionar dispositivo de destino](./media/storsimple-virtual-array-deploy3-iscsi-setup/image25.png)
6. En el host de Windows, presione la tecla del logotipo de Windows hello + X y, a continuación, haga clic en **ejecutar**.
7. Hola **ejecutar** cuadro de diálogo, escriba **Diskmgmt.msc**. Haga clic en **Aceptar**, hello y **administración de discos** aparecerá el cuadro de diálogo. panel derecho de Hello mostrará volúmenes hello en el host.
8. Hola **administración de discos** ventana, hello volúmenes montados aparecerán como se muestra en hello siguiente ilustración. Haga clic en el volumen de hello detectado (haga clic en el nombre del disco de hello) y, a continuación, haga clic en **Online**.
   
    ![Administración de discos](./media/storsimple-virtual-array-deploy3-iscsi-setup/image26.png)
9. Haga clic con el botón derecho y seleccione **Inicializar disco**.
   
    ![inicializar disco 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image27.png)
10. En el cuadro de diálogo de hello, seleccione Hola discos tooinitialize y, a continuación, haga clic en **Aceptar**.
    
    ![inicializar disco 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image28.png)
11. se inicia el Asistente para nuevo volumen Simple de Hola. Seleccione un tamaño de disco y luego haga clic en **Siguiente**.
    
    ![asistente para nuevo volumen 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image29.png)
12. Asignar un volumen de toohello de letra de unidad y, a continuación, haga clic en **siguiente**.
    
    ![asistente para nuevo volumen 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image30.png)
13. Escriba el volumen de hello parámetros tooformat Hola. **En Windows Server, solo se admite NTFS.** Establecer too64K de tamaño de unidad de asignación de Hola. Proporcione una etiqueta para el volumen. Es una práctica recomendada para este nombre de volumen de nombre toobe toohello idénticos que proporcionó en la matriz Virtual de StorSimple. Haga clic en **Siguiente**.
    
    ![asistente para nuevo volumen 3](./media/storsimple-virtual-array-deploy3-iscsi-setup/image31.png)
14. Compruebe los valores de hello para el volumen y, a continuación, haga clic en **finalizar**.
    
    ![asistente para nuevo volumen 4](./media/storsimple-virtual-array-deploy3-iscsi-setup/image32.png)
    
    Hola volúmenes aparecerán como **en línea** en hello **administración de discos** página.
    
    ![volúmenes en línea](./media/storsimple-virtual-array-deploy3-iscsi-setup/image33.png)

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo toouse Hola IU web local demasiado[administrar la matriz Virtual de StorSimple](storsimple-ova-web-ui-admin.md).

## <a name="appendix-a-get-hello-iqn-of-a-windows-server-host"></a>Apéndice A: Hola de Get IQN de un host de Windows Server

Realizar Hola siguiendo los pasos tooget Hola iSCSI nombre completo (IQN) de un host de Windows que ejecuta Windows Server 2012.

#### <a name="tooget-hello-iqn-of-a-windows-host"></a>Hola tooget IQN de un host de Windows

1. Inicie el iniciador iSCSI de Microsoft de hello en el host de Windows.
2. Hola **propiedades del iniciador iSCSI** ventana hello **configuración** ficha, seleccione y copie cadena Hola de hello **nombre del iniciador** campo.
   
    ![Propiedades del iniciador iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/image34.png)
3. Guarde esta cadena.

<!--Reference link-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx



