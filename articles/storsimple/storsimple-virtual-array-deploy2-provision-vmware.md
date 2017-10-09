---
title: aaaProvision StorSimple Virtual Array en VMware | Documentos de Microsoft
description: "En este segundo tutorial de la serie de implementación de matrices virtuales de StorSimple, se trata el aprovisionamiento de un dispositivo virtual en VMware."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 0425b2a9-d36f-433d-8131-ee0cacef95f8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0912c1c315a04ea46b6373a8fcd5554ecae14e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-vmware"></a>Implementar una matriz virtual de StorSimple: Aprovisionamiento en VMware
![](./media/storsimple-virtual-array-deploy2-provision-vmware/vmware4.png)

## <a name="overview"></a>Información general
Este tutorial se describe cómo tooprovision y conéctese tooa StorSimple Virtual Array en un sistema host ejecutando VMware ESXi 5.5 y versiones posteriores. Este artículo aplica a la implementación de toohello de StorSimple arreglos de discos virtuales en el portal de Azure y la nube de Microsoft Azure Government Hola.

Es necesario tooprovision de privilegios de administrador y conecte el dispositivo virtual tooa. el programa de instalación de aprovisionamiento e inicial de Hello puede tardar unos 10 toocomplete minutos.

## <a name="provisioning-prerequisites"></a>Requisitos previos de aprovisionamiento
Hola tooprovision de requisitos previos un dispositivo virtual en un sistema host ejecutando VMware ESXi 5.5 y anterior, son los siguientes.

### <a name="for-hello-storsimple-device-manager-service"></a>Para hello servicio Administrador de dispositivos de StorSimple
Antes de comenzar, asegúrese de que:

* Ha completado todos los pasos de hello en [portal de Hola de preparación de StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).
* Imagen del dispositivo virtual Hola que has descargado para VMware en hello portal de Azure. Para obtener más información, consulte **paso 3: imagen del dispositivo virtual descarga hello** de [portal de Hola de preparación para la Guía de StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).

### <a name="for-hello-storsimple-virtual-device"></a>Para el dispositivo virtual StorSimple Hola
Antes de implementar un dispositivo virtual, asegúrese de que:

* Tendrá acceso tooa host sistema que ejecuta Hyper-V (2008 R2 o posterior) que puede ser usado tooa aprovisionar un dispositivo.
* sistema de host de Hello es capaz de toodedicate Hola siguientes tooprovision de recursos del dispositivo virtual:

  * Un mínimo de 4 núcleos.
  * Al menos 8 GB de RAM. Si tiene previsto matriz virtual de hello tooconfigure como servidor de archivos, 8 GB es compatible con menos de 2 millones de archivos. Necesita 16 GB de RAM toosupport 2-4 millones de archivos.
  * Una interfaz de red.
  * Un disco virtual de 500 GB para datos del sistema.

### <a name="for-hello-network-in-datacenter"></a>Para la red de hello en el centro de datos
Antes de comenzar, asegúrese de que:

* Revisar Hola red requisitos toodeploy un dispositivo StorSimple virtual y red de centro de datos de hello configurado según los requisitos de Hola. 

## <a name="step-by-step-provisioning"></a>Aprovisionamiento paso a paso
tooprovision y conecte el dispositivo virtual tooa, deberá hello tooperform pasos:

1. Asegúrese de que el sistema de host de hello tiene requisitos suficientes recursos toomeet Hola mínimos del dispositivo virtual.
2. Aprovisione un dispositivo virtual en el hipervisor.
3. Inicie el dispositivo virtual de Hola y obtener dirección IP de Hola.

## <a name="step-1-ensure-host-system-meets-minimum-virtual-device-requirements"></a>Paso 1: Asegurarse de que el sistema host cumple los requisitos mínimos del dispositivo virtual
toocreate un dispositivo virtual, necesitará:

* Sistema de host de acceso tooa ejecutando VMware ESXi Server 5.5 y versiones posteriores.
* VMware vSphere client en el host ESXi de sistema toomanage Hola.

  * Un mínimo de 4 núcleos.
  * Al menos 8 GB de RAM. Si tiene previsto matriz virtual de hello tooconfigure como servidor de archivos, 8 GB es compatible con menos de 2 millones de archivos. Necesita 16 GB de RAM toosupport 2-4 millones de archivos.
  * Red toohello capaz de enrutamiento de tráfico tooInternet conectados a una interfaz de red. ancho de banda de Internet mínima Hola debe ser 5 tooallow Mbps para el funcionamiento óptimo del dispositivo Hola.
  * Un disco virtual de 500 GB para datos.

## <a name="step-2-provision-a-virtual-device-in-hypervisor"></a>Paso 2: Aprovisionar un dispositivo virtual en el hipervisor
Realizar Hola siguiendo los pasos tooprovision un dispositivo virtual en el hipervisor.

1. Copie la imagen del dispositivo virtual hello en el sistema. Descargar esta imagen virtual a través de hello portal de Azure.

   1. Asegúrese de que ha descargado el archivo de imagen de hello más reciente. Si ha descargado anteriormente imagen hello, descargarla de nuevo tooensure tiene imagen más reciente de Hola. imagen más reciente de Hello tiene dos archivos (en lugar de uno).
   2. Tome nota de ubicación de Hola donde copiar imagen Hola usan esta imagen más adelante en el procedimiento de Hola.

2. Inicie sesión en toohello servidor ESXi mediante Hola vSphere cliente. Debe toocreate de privilegios de administrador de toohave una máquina virtual.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image1.png)
3. En el cliente de vSphere de hello, en la sección de inventario de hello en el panel izquierdo de hello, seleccione Hola ESXi Server.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image2.png)
4. Cargar el servidor de hello VMDK toohello ESXi. Navegue toohello **configuración** ficha en el panel derecho de Hola. En **Hardware**, seleccione **Storage** (Almacenamiento).

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image3.png)
5. Hola haga panel, en **almacenes de datos**, seleccione Hola almacén de datos donde desea hello tooupload VMDK. almacén de datos de Hello debe tener suficiente espacio libre para hello OS y discos de datos.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image4.png)
6. Haga clic con el botón derecho y seleccione **Browse Datastore**(Examinar almacén de datos).

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image5.png)
7. Aparece la ventana **Datastore Browser** (Explorador del almacén de datos).

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image6.png)
8. En la barra de herramientas de hello, haga clic en ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image7.png) icono toocreate una nueva carpeta. Especifique el nombre de la carpeta de Hola y tome nota del mismo. Utilizará este nombre de carpeta más adelante al crear una máquina virtual (práctica recomendada). Haga clic en **Aceptar**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image8.png)
9. Hola nueva carpeta aparece en panel izquierdo de Hola de hello **explorador del almacén de datos**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image9.png)
10. Haga clic en el icono de carga de hello ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image10.png) y seleccione **cargar archivo**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image11.png)
11. Busque y seleccione archivos VMDK de toohello que ha descargado. Hay dos archivos. Seleccione un tooupload de archivo.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image12m.png)
12. Haga clic en **Abrir**. carga de Hola de hello VMDK archivo toohello especificado inicia de almacén de datos. Puede tardar varios minutos para tooupload de archivo Hola.
13. Una vez finalizada la carga de hello, vea archivo de hello en el almacén de datos de hello en carpeta de Hola que creó.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image14.png)

    Cargar ahora Hola segundo VMDK archivo toohello mismo almacén de datos.
14. Ventana de cliente de vSphere toohello devuelto. Con el servidor ESXi seleccionado, haga clic con el botón secundario y seleccione **Nueva máquina virtual**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image15.png)
15. Aparece una ventana **Crear nueva máquina virtual** . En hello **configuración** página, seleccione hello **personalizado** opción. Haga clic en **Siguiente**.
    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image16.png)
16. En hello **nombre y la ubicación** página, especifique el nombre de saludo de la máquina virtual. Este nombre debe coincidir con nombre de carpeta de hello (procedimiento recomendado) que especificó anteriormente en el paso 8.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image17.png)
17. En hello **almacenamiento** , seleccione un almacén de datos que desee toouse tooprovision la máquina virtual.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image18.png)
18. En hello **versión de la máquina Virtual** página, seleccione **versión de la máquina Virtual: 8**. Todas las versiones 8 too11 son compatibles.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image19.png)
19. En hello **sistema operativo invitado** página, seleccione hello **sistema operativo invitado** como **Windows**. Para **versión**, en la lista desplegable de hello, seleccione **Microsoft Windows Server 2012 (64 bits)**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image20.png)
20. En hello **CPU** página, ajustar hello **número de sockets virtuales** y **número de núcleos por socket virtual** por lo que Hola **número Total de núcleos**es 4 (o más). Haga clic en **Siguiente**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image21.png)
21. En hello **memoria** página, especifique 8 GB (o más) de RAM. Haga clic en **Siguiente**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image22.png)
22. En hello **red** página, especifique el número de Hola Hola de interfaces de red. requisito mínimo de Hello es una interfaz de red.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image23.png)
23. En hello **controladora SCSI** , acepte el valor predeterminado de hello **controlador LSI Logic SAS**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image24.png)
24. En hello **seleccione un disco** página, elija **utilizar un disco virtual existente**. Haga clic en **Siguiente**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image25.png)
25. En hello **Seleccionar disco existente** página, en **ruta de acceso de archivo de disco**, haga clic en **examinar**. Se abrirá un cuadro de diálogo **Examinar almacenes de datos** . Navegar por ubicación toohello donde cargar Hola VMDK. Ahora verá un archivo de almacén de datos de hello tal y como se han combinado los archivos de dos de Hola que haya cargado inicialmente. Seleccione el archivo hello y haga clic en **Aceptar**. Haga clic en **Siguiente**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image26.png)
26. En hello **opciones avanzadas** página, acepte el valor predeterminado de Hola y haga clic en **siguiente**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image27.png)
27. En hello **tooComplete listo** página, revise todos los valores de hello asociados con la nueva máquina virtual de Hola. Comprobar **editar la configuración de máquina virtual de hello antes de la finalización**. Haga clic en **Continue**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image28.png)
28. En hello **propiedades de las máquinas virtuales** página Hola **Hardware** ficha, busque el hardware del dispositivo Hola. Seleccione **Nuevo disco duro**. Haga clic en **Agregar**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image29.png)
29. Verá una ventana **Agregar hardware**. En hello **tipo de dispositivo** página, en **Elegir tipo de hello de dispositivo que se va tooadd**, seleccione **disco duro**y haga clic en **siguiente**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image30.png)
30. En hello **seleccione un disco** página, elija **crear un nuevo disco virtual**. Haga clic en **Siguiente**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image31.png)
31. En hello **crear un disco** página, cambie hello **tamaño de disco** too500 GB (o más). Aunque 500 GB es el requisito mínimo de hello, siempre puede aprovisionar un disco de mayor tamaño. Tenga en cuenta que no se puede expandir o reducir disco Hola una vez aprovisionado. Para obtener más información sobre el tamaño de Hola de tooprovision de disco, revise la sección de ajuste de tamaño de Hola Hola [documento de prácticas recomendada](storsimple-ova-best-practices.md). En **Disk Provisioning** (Aprovisionamiento de disco), seleccione **Thin Provision** (Aprovisionamiento fino). Haga clic en **Siguiente**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image32.png)
32. En hello **opciones avanzadas** , acepte el valor predeterminado de Hola.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image33.png)
33. En hello **tooComplete listo** página, revise las opciones de disco de Hola. Haga clic en **Finalizar**

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image34.png)
34. Devolver la página de propiedades de la máquina Virtual de toohello. Un nuevo disco duro se agrega la máquina virtual de tooyour. Haga clic en **Finalizar**

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image35.png)
35. Con la máquina virtual seleccionada en el panel derecho de hello, navegar toohello **resumen** ficha. Revise la configuración de hello para la máquina virtual.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image36.png)

Ahora la máquina virtual está aprovisionada. paso siguiente Hello es toopower en este equipo y obtener dirección IP de Hola.

## <a name="step-3-start-hello-virtual-device-and-get-hello-ip"></a>Paso 3: Iniciar hello de dispositivo virtual y obtener el IP Hola
Realizar Hola siguiendo los pasos toostart su dispositivo virtual y conectarse tooit.

#### <a name="toostart-hello-virtual-device"></a>dispositivo virtual de hello toostart
1. Inicie el dispositivo virtual Hola. En vSphere Hola Configuration Manager, en el panel izquierdo de hello, seleccione el dispositivo y hacer clic en toobring menú contextual de Hola. Seleccione **Power** (Encendido) y, luego, seleccione **Power on** (Encender). Esto debe encender la máquina virtual. Puede ver el estado de hello en la parte inferior de hello **tareas recientes** panel del cliente de vSphere Hola.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image37.png)
2. tareas de configuración de Hello tardará unos toocomplete minutos. Una vez que se está ejecutando el dispositivo de hello, navegue toohello **consola** ficha. Enviar toolog Ctrl + Alt + Supr en el dispositivo toohello. Como alternativa, puede punto cursor hello en la ventana de la consola de Hola y presione Ctrl + Alt + Insert. usuario de Hello predeterminado es *StorSimpleAdmin* y la contraseña predeterminada de hello es *Password1*.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image38.png)
3. Por motivos de seguridad, contraseña de administrador de dispositivos de hello expira en el primer inicio de sesión Hola. Son la contraseña de hello toochange solicitadas.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image39.png)
4. Escriba una contraseña que contenga al menos 8 caracteres. contraseña de Hello debe contener 3 de 4 de estos requisitos: caracteres en mayúsculas, minúsculas, numéricos y especiales. Vuelva a escribir Hola contraseña tooconfirm lo. Se le notificará que esa contraseña Hola ha cambiado.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image40.png)
5. Después de cambia correctamente contraseña hello, puede reiniciar el dispositivo virtual Hola. Espere a que toocomplete de reinicio de Hola. consola de Windows PowerShell de Hello de dispositivo de hello puede mostrarse junto con una barra de progreso.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image41.png)
6. Los pasos 6 a 8 solo se aplican cuando se arranca en un entorno sin DHCP. Si se encuentra en un entorno de DHCP, a continuación, omitir estos pasos y vaya toostep 9. Si ha arrancado el dispositivo en el entorno no DHCP, verá Hola después de la pantalla.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image42m.png)

   A continuación, configure la red de Hola.
7. Hola de uso `Get-HcsIpAddress` comando interfaces de red de hello toolist habilitadas en el dispositivo virtual. Si el dispositivo tiene una sola interfaz de red habilitada, Hola predeterminado nombre asignado toothis interfaz es `Ethernet`.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image43m.png)
8. Hola de uso `Set-HcsIpAddress` red de cmdlet tooconfigure Hola. A continuación se muestra un ejemplo:

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image44.png)
9. Una vez finalizada la instalación inicial de Hola y ha arrancado dispositivo hello, verá el texto de titular de dispositivo de Hola. Tome nota de dirección IP de Hola y dirección URL de hello del dispositivo de hello pancarta texto toomanage Hola. Usará este sitio web toohello de tooconnect de dirección IP interfaz de usuario de su dispositivo virtual y la instalación local de hello completa y el registro.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image45.png)
10. (Opcional) Realice este paso solo si va a implementar el dispositivo en hello gobierno en la nube. Ahora podrá aplicar Hola United States Federal de procesamiento estándar modo información (FIPS) en el dispositivo. estándar de Hello FIPS 140 define los algoritmos criptográficos aprobados para su uso por los sistemas de equipo de Gobierno Federal nos para la protección de Hola de los datos confidenciales.

    1. tooenable Hola el modo FIPS, ejecute hello siguiente cmdlet:

        `Enable-HcsFIPSMode`
    2. Reinicie el dispositivo después de haber habilitado el modo FIPS Hola para que las validaciones criptográficos Hola surtan efecto.

       > [!NOTE]
       > Puede habilitar o deshabilitar el modo FIPS en su dispositivo. Dispositivo de hello alternas entre el modo FIPS y FIPS no no se admite.
       >
       >

Si el dispositivo no cumple los requisitos mínimos de configuración de hello, verá un error en el texto de titular de hello (que se muestra a continuación). Configuración del dispositivo toomodify Hola necesitará para que tenga requisitos mínimos de los recursos adecuados toomeet Hola. A continuación, puede reiniciar y conecte el dispositivo de toohello. Consulte los requisitos mínimos de configuración de toohello en [paso 1: asegúrese de que el sistema de host de hello cumple los requisitos mínimos del dispositivo virtual](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements).

![](./media/storsimple-virtual-array-deploy2-provision-vmware/image46.png)

Si se enfrenta a algún otro error durante la configuración inicial de hello mediante la interfaz de usuario de web local de hello, consulte toohello después de los flujos de trabajo:

* Ejecutar pruebas de diagnóstico demasiado[solucionar problemas de instalación de la interfaz de usuario de web](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).
* [Genere el paquete de registro y vea los archivos del registro](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="next-steps"></a>Pasos siguientes
* [Configurar la matriz virtual de StorSimple como servidor de archivos](storsimple-virtual-array-deploy3-fs-setup.md)
* [Configurar la matriz virtual de StorSimple como servidor iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md)
