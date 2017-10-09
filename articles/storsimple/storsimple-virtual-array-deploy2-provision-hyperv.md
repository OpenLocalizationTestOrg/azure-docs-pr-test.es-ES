---
title: aaaProvision StorSimple Virtual Array en Hyper-V | Documentos de Microsoft
description: "En este segundo tutorial de implementación de StorSimple Virtual Array, se trata el aprovisionamiento de una matriz virtual en Hyper-V."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 4354963c-e09d-41ac-9c8b-f21abeae9913
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f47d642f740827ae1440b819e07067c6a183527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-hyper-v"></a>Implementar una matriz virtual de StorSimple: Aprovisionamiento en Hyper-V
![](./media/storsimple-virtual-array-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a>Información general
Este tutorial describe cómo tooprovision una StorSimple Virtual Array en un sistema de host que ejecuta Hyper-V en Windows Server 2012 R2, Windows Server 2012 o Windows Server 2008 R2. Este artículo aplica a la implementación de toohello de StorSimple arreglos de discos virtuales en el portal de Azure y la nube de Microsoft Azure Government.

Se necesita tooprovision de privilegios de administrador y se configura una matriz virtual. el programa de instalación de aprovisionamiento e inicial de Hello puede tardar unos 10 toocomplete minutos.

## <a name="provisioning-prerequisites"></a>Requisitos previos de aprovisionamiento
Aquí encontrará tooprovision de requisitos previos de hello una matriz virtual en un sistema de host que ejecuta Hyper-V en Windows Server 2012 R2, Windows Server 2012 o Windows Server 2008 R2.

### <a name="for-hello-storsimple-device-manager-service"></a>Para hello servicio Administrador de dispositivos de StorSimple
Antes de comenzar, asegúrese de que:

* Ha completado todos los pasos de hello en [portal de Hola de preparación de StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).
* Imagen de la matriz virtual de Hola que has descargado para Hyper-V en hello portal de Azure. Para obtener más información, consulte **paso 3: imagen de descarga Hola matriz virtual** de [portal de Hola de preparación para la Guía de StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).

  > [!IMPORTANT]
  > software de Hola que se ejecuta en hello StorSimple Virtual Array solo puede usarse con hello servicio Administrador de dispositivos de StorSimple.
  >
  >

### <a name="for-hello-storsimple-virtual-array"></a>Para hello StorSimple Virtual Array
Antes de implementar una matriz virtual, asegúrese de que:

* Tener acceso tooa host sistema que ejecuta Hyper-V en Windows Server 2008 R2 o posterior que se usa tooa aprovisionar un dispositivo.
* sistema de host de Hello es capaz de toodedicate Hola siguientes tooprovision de recursos de la matriz virtual:

  * Un mínimo de 4 núcleos.
  * Al menos 8 GB de RAM. Si tiene previsto matriz virtual de hello tooconfigure como servidor de archivos, 8 GB es compatible con menos de 2 millones de archivos. Necesita 16 GB de RAM toosupport 2-4 millones de archivos.
  * Una interfaz de red.
  * Un disco virtual de 500 GB para datos.

### <a name="for-hello-network-in-hello-datacenter"></a>Para la red de hello en el centro de datos de Hola
Antes de comenzar, revise Hola requisitos toodeploy una matriz Virtual de StorSimple de red y configurar red del centro de datos de hello según corresponda. Para más información, consulte [Requisitos del sistema de la matriz virtual de StorSimple](storsimple-ova-system-requirements.md#networking-requirements).

## <a name="step-by-step-provisioning"></a>Aprovisionamiento paso a paso
tooprovision y conectar discos virtuales tooa, deberá hello tooperform pasos:

1. Asegúrese de que el sistema de host de hello tiene suficientes recursos toomeet Hola mínimo virtual requisitos de la matriz.
2. Aprovisione una matriz virtual en el hipervisor.
3. Inicie la matriz virtual hello y obtener dirección IP de Hola.

Cada uno de estos pasos se explica en las secciones siguientes de Hola.

## <a name="step-1-ensure-that-hello-host-system-meets-minimum-virtual-array-requirements"></a>Paso 1: Asegurarse de que sistema de host de hello cumple los requisitos mínimos matriz virtual
toocreate una matriz virtual, necesitará:

* rol de Hello Hyper-V instalado en Windows Server 2012 R2, Windows Server 2012 o Windows Server 2008 R2 SP1.
* Administrador de Hyper-V de Microsoft en un cliente de Microsoft Windows conectado toohello host.

Asegúrese de que ese Hola subyacente de hardware (sistema de host) en el que va a crear la matriz virtual hello es hello toodedicate pueda después de la matriz virtual tooyour de recursos:

* Un mínimo de 4 núcleos.
* Al menos 8 GB de RAM. Si tiene previsto matriz virtual de hello tooconfigure como servidor de archivos, 8 GB es compatible con menos de 2 millones de archivos. Necesita 16 GB de RAM toosupport 2-4 millones de archivos.
* Una interfaz de red.
* Un disco virtual de 500 GB para datos del sistema.

## <a name="step-2-provision-a-virtual-array-in-hypervisor"></a>Paso 2: Aprovisionar una matriz virtual en el hipervisor
Realizar Hola siguiendo los pasos tooprovision un dispositivo en el hipervisor.

#### <a name="tooprovision-a-virtual-array"></a>tooprovision una matriz virtual
1. En el host de Windows Server, copie Hola matriz virtual imagen tooa la unidad local. Descargar esta imagen (VHD o VHDX) a través de hello portal de Azure. Tome nota de ubicación de Hola donde copiar imagen Hola usan esta imagen más adelante en el procedimiento de Hola.
2. Abra el **Administrador del servidor**. En hello esquina superior derecha, haga clic en **herramientas** y seleccione **Administrador de Hyper-V**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image1.png)  

   Si está ejecutando Windows Server 2008 R2, abra Administrador de Hyper-V de Hola. En el Administrador de servidores, haga clic en **Roles > Hyper-V > Administrador de Hyper-V**.
3. En **Administrador de Hyper-V**, en el panel de ámbito de hello, haga clic en el menú contextual de sistema nodo tooopen hello y, a continuación, haga clic en **New** > **Máquina Virtual**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image2.png)
4. En hello **antes de comenzar** página de hello nuevo Asistente para la máquina Virtual, haga clic en **siguiente**.
5. En hello **especificar nombre y ubicación** , proporcione un **nombre** de la matriz virtual. Haga clic en **Siguiente**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image4.png)
6. En hello **especificar generación** página, elija el tipo de imagen de dispositivo de hello y, a continuación, haga clic en **siguiente**. Esta página no aparece si está utilizando Windows Server 2008 R2.

   * Elija **Generación 2** si descargó una imagen .vhdx para Windows Server 2012 o versiones posteriores.
   * Elija **Generación 1** si descargó una imagen .vhd para Windows Server 2008 R2 o versiones posteriores.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image5.png)
7. En hello **asignar memoria** página, especifique un **memoria de inicio** de al menos **MB 8192**, no habilite la memoria dinámica y, a continuación, haga clic en **siguiente**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image6.png)  
8. En hello **configurar redes** página, especifique Hola conmutador virtual que está conectado toohello Internet y, a continuación, haga clic en **siguiente**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image7.png)
9. En hello **conectar disco duro virtual** página, elija **usar un disco duro virtual existente**, especifique la ubicación de Hola de imagen de hello matriz virtual (.vhdx o .vhd) y, a continuación, haga clic en **siguiente**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image8m.png)
10. Hola de revisión **resumen** y, a continuación, haga clic en **finalizar** máquina virtual de toocreate Hola.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image9.png)
11. requisitos mínimos de toomeet hello, necesita 4 núcleos. tooadd 4 procesadores virtuales, seleccione el sistema host en hello **Administrador de Hyper-V** ventana. En panel derecho hello en lista de Hola de **máquinas virtuales**, busque la máquina virtual de Hola que acaba de crear. Seleccione y haga clic en el nombre de la máquina de Hola y seleccione **configuración**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image10.png)
12. En hello **configuración** página, en el panel izquierdo hello, haga clic en **procesador**. En el panel derecho hello, establezca **número de procesadores virtuales** too4 (o más). Haga clic en **Apply**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image11.png)
13. requisitos mínimos de toomeet hello, también deberá tooadd un disco de datos virtual de 500 GB. Hola **configuración** página:

    1. En el panel izquierdo de hello, seleccione **controladora SCSI**.
    2. En el panel derecho de hello, seleccione **disco duro,** y haga clic en **agregar**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image12.png)
14. En hello **unidad de disco duro** página, seleccione hello **disco duro Virtual** opción y haga clic en **nuevo**. Hola **Asistente para nuevo disco duro de Virtual** inicia.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image13.png)
15. En hello **antes de comenzar** página de hello nuevo Asistente de disco duro Virtual, haga clic en **siguiente**.
16. En hello **página Elegir formato de disco**, acepte opción predeterminada de Hola de **VHDX** formato. Haga clic en **Siguiente**. Esta pantalla no aparece si se ejecuta Windows Server 2008 R2.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image15.png)
17. En hello **página Elegir tipo de disco**, establezca el tipo de disco duro virtual como **expansión dinámica** (recomendado). **Tamaño fijo** disco funcionará, pero puede que necesite toowait mucho tiempo. Se recomienda que no utilicen hello **Differencing** opción. Haga clic en **Siguiente**. En Windows Server 2012 R2 y Windows Server 2012, **expansión dinámica** es la opción predeterminada de hello mientras que en Windows Server 2008 R2, valor predeterminado de hello es **tamaño fijo**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image16.png)
18. En hello **especificar el nombre y ubicación** , proporcione un **nombre** como **ubicación** (puede examinar tooone) Hola disco de datos. Haga clic en **Siguiente**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image17.png)
19. En hello **configurar disco** página opción Hola seleccione **crear un disco duro virtual en blanco nueva** y especifique el tamaño de hello como **500 GB** (o más). Aunque 500 GB es el requisito mínimo de hello, siempre puede aprovisionar un disco de mayor tamaño. Tenga en cuenta que no se puede expandir o reducir disco Hola una vez aprovisionado. Para obtener más información sobre el tamaño de Hola de tooprovision de disco, revise la sección de ajuste de tamaño de Hola Hola [documento de prácticas recomendada](storsimple-ova-best-practices.md). Haga clic en **Siguiente**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image18.png)
20. En hello **resumen** página, revise los detalles de hello del disco virtual de datos y si se cumplen, haga clic en **finalizar** disco de hello toocreate. Hola asistente se cierra y un disco duro virtual se agrega tooyour máquina.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image19.png)
21. Devolver toohello **configuración** página. Haga clic en **Aceptar** tooclose hello **configuración** página y devolver tooHyper-V Manager ventana.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-hello-virtual-array-and-get-hello-ip"></a>Paso 3: Iniciar matriz virtual hello y obtener IP Hola
Realizar Hola siguiendo los pasos toostart la matriz virtual y conectarse tooit.

#### <a name="toostart-hello-virtual-array"></a>matriz de toostart Hola virtual
1. Inicie la matriz virtual Hola.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image21.png)
2. Después de que se está ejecutando el dispositivo de hello, seleccionar dispositivo de hello, haga clic y seleccione **conectar**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image22.png)
3. Puede que tenga toowait 5-10 minutos para hello dispositivo toobe listo. Se muestra un mensaje de estado sobre el progreso de hello consola tooindicate Hola. Una vez preparado el dispositivo de hello, vaya demasiado**acción**. Presione `Ctrl + Alt + Delete` toolog de matriz virtual toohello. usuario de Hello predeterminado es *StorSimpleAdmin* y la contraseña predeterminada de hello es *Password1*.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image23.png)
4. Por motivos de seguridad, contraseña de administrador de dispositivos de hello expira en el primer inicio de sesión Hola. Son la contraseña de hello toochange solicitadas.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image24.png)

   Escriba una contraseña que contenga al menos 8 caracteres. Hello contraseña debe cumplir al menos 3 fuera Hola según los requisitos de 4: caracteres en mayúsculas, minúsculas, numéricos y especiales. Vuelva a escribir Hola contraseña tooconfirm lo. Se le notificará que esa contraseña Hola ha cambiado.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image25.png)
5. Después de cambia contraseña Hola correctamente, se puede reiniciar matriz virtual Hola. Espere Hola dispositivo toostart.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image26.png)

    consola de Windows PowerShell de Hello de dispositivo de Hola se muestra junto con una barra de progreso.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image27.png)
6. Los pasos 6 a 8 solo se aplican cuando se arranca en un entorno sin DHCP. Si se encuentra en un entorno de DHCP, a continuación, omitir estos pasos y vaya toostep 9. Si ha arrancado el dispositivo en el entorno no DHCP, verá Hola después de la pantalla.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image28m.png)

    A continuación, configure la red de Hola.
7. Hola de uso `Get-HcsIpAddress` comando interfaces de red de hello toolist habilitadas en la matriz virtual. Si el dispositivo tiene una sola interfaz de red habilitada, Hola predeterminado nombre asignado toothis interfaz es `Ethernet`.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image29m.png)
8. Hola de uso `Set-HcsIpAddress` red de cmdlet tooconfigure Hola. Vea el siguiente ejemplo de Hola:

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image30.png)
9. Una vez finalizada la instalación inicial de Hola y ha arrancado dispositivo hello, verá el texto de titular de dispositivo de Hola. Tome nota de dirección IP de Hola y dirección URL de hello del dispositivo de hello pancarta texto toomanage Hola. Usar este sitio web toohello de tooconnect de dirección IP interfaz de usuario de la matriz virtual y la instalación local de hello completa y el registro.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image31m.png)
10. (Opcional) Realice este paso solo si va a implementar el dispositivo en hello gobierno en la nube. Ahora podrá aplicar Hola United States Federal de procesamiento estándar modo información (FIPS) en el dispositivo. estándar de Hello FIPS 140 define los algoritmos criptográficos aprobados para su uso por los sistemas de equipo de Gobierno Federal nos para la protección de Hola de los datos confidenciales.

    1. tooenable Hola el modo FIPS, ejecute hello siguiente cmdlet:

        `Enable-HcsFIPSMode`
    2. Reinicie el dispositivo después de haber habilitado el modo FIPS Hola para que las validaciones criptográficos Hola surtan efecto.

       > [!NOTE]
       > Puede habilitar o deshabilitar el modo FIPS en su dispositivo. Dispositivo de hello alternas entre el modo FIPS y FIPS no no se admite.
       >
       >

Si el dispositivo no cumple los requisitos mínimos de configuración de hello, vea Hola tras error en el texto de titular de hello (que se muestra a continuación). Modificar configuración de dispositivo de Hola para que hello máquina tiene los recursos adecuados toomeet Hola requisitos mínimos. A continuación, puede reiniciar y conecte el dispositivo de toohello. Consulte los requisitos mínimos de configuración de toohello en [paso 1: asegurarse de que sistema de host de hello cumple requisitos de la matriz virtual mínimo](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).

![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image32.png)

Si se enfrenta a algún otro error durante la configuración inicial de hello mediante la interfaz de usuario de web local de hello, consulte toohello después de los flujos de trabajo:

* Ejecutar pruebas de diagnóstico demasiado[solucionar problemas de instalación de la interfaz de usuario de web](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).
* [Genere el paquete de registro y vea los archivos del registro](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="next-steps"></a>Pasos siguientes
* [Configurar la matriz virtual de StorSimple como servidor de archivos](storsimple-virtual-array-deploy3-fs-setup.md)
* [Configurar la matriz virtual de StorSimple como servidor iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md)
