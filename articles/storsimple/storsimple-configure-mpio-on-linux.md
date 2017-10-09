---
title: aaaConfigure MPIO en el host de StorSimple Linux | Documentos de Microsoft
description: Configurar MPIO en el host de Linux tooa StorSimple conectado ejecutando 6.6 de CentOS
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: d9f7e02903243494c909313fb2c33ac690764274
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a><span data-ttu-id="cf6cd-103">Configuración de MPIO en un host de StorSimple que ejecuta CentOS</span><span class="sxs-lookup"><span data-stu-id="cf6cd-103">Configure MPIO on a StorSimple host running CentOS</span></span>
<span data-ttu-id="cf6cd-104">Este artículo explica Hola pasos necesarios tooconfigure E/S de múltiples rutas (MPIO) en el servidor de host de Centos 6.6.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-104">This article explains hello steps required tooconfigure Multipathing IO (MPIO) on your Centos 6.6 host server.</span></span> <span data-ttu-id="cf6cd-105">servidor de host de Hello es tooyour conectado de dispositivo de StorSimple de Microsoft Azure para lograr alta disponibilidad a través de los iniciadores iSCSI.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-105">hello host server is connected tooyour Microsoft Azure StorSimple device for high availability via iSCSI initiators.</span></span> <span data-ttu-id="cf6cd-106">Se describe en la detección automática de detalle Hola de dispositivos de múltiples rutas de acceso y el programa de instalación específicos de hello sólo para volúmenes de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-106">It describes in detail hello automatic discovery of multipath devices and hello specific setup only for StorSimple volumes.</span></span>

<span data-ttu-id="cf6cd-107">Este procedimiento es aplicable tooall modelos de Hola de dispositivos de la serie StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-107">This procedure is applicable tooall hello models of StorSimple 8000 series devices.</span></span>

> [!NOTE]
> <span data-ttu-id="cf6cd-108">No se puede usar este procedimiento para un dispositivo virtual de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-108">This procedure cannot be used for a StorSimple virtual device.</span></span> <span data-ttu-id="cf6cd-109">Para obtener más información, vea cómo tooconfigure hospedar servidores del dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-109">For more information, see how tooconfigure host servers for your virtual device.</span></span>
> 
> 

## <a name="about-multipathing"></a><span data-ttu-id="cf6cd-110">Acerca de múltiples rutas</span><span class="sxs-lookup"><span data-stu-id="cf6cd-110">About multipathing</span></span>
<span data-ttu-id="cf6cd-111">característica de múltiples rutas de Hello permite tooconfigure varias rutas de acceso de E/S entre un servidor host y un dispositivo de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-111">hello multipathing feature allows you tooconfigure multiple I/O paths between a host server and a storage device.</span></span> <span data-ttu-id="cf6cd-112">Estas rutas de acceso de E/S son conexiones físicas de SAN que pueden incluir cables independientes, conmutadores, interfaces de red y controladores.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-112">These I/O paths are physical SAN connections that can include separate cables, switches, network interfaces, and controllers.</span></span> <span data-ttu-id="cf6cd-113">Múltiples rutas agrega las rutas de E/S de hello, tooconfigure un nuevo dispositivo que está asociado con todas las rutas de acceso de hello agregado.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-113">Multipathing aggregates hello I/O paths, tooconfigure a new device that is associated with all of hello aggregated paths.</span></span>

<span data-ttu-id="cf6cd-114">propósito de Hola de múltiples rutas tiene dos aspectos:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-114">hello purpose of multipathing is two-fold:</span></span>

* <span data-ttu-id="cf6cd-115">**Alta disponibilidad**: proporciona una ruta de acceso alternativa si se produce un error en cualquier elemento de ruta de acceso de hello E/S (por ejemplo, un cable, conmutador, interfaz de red o controlador).</span><span class="sxs-lookup"><span data-stu-id="cf6cd-115">**High availability**: It provides an alternate path if any element of hello I/O path (such as a cable, switch, network interface, or controller) fails.</span></span>
* <span data-ttu-id="cf6cd-116">**Equilibrio de carga**: dependiendo de su dispositivo de almacenamiento de configuración de hello, puede mejorar el rendimiento de hello detectando cargas en las rutas de acceso de E/S de Hola y reequilibrio dinámicamente las cargas.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-116">**Load balancing**: Depending on hello configuration of your storage device, it can improve hello performance by detecting loads on hello I/O paths and dynamically rebalancing those loads.</span></span>

### <a name="about-multipathing-components"></a><span data-ttu-id="cf6cd-117">Acerca de los componentes de múltiples rutas</span><span class="sxs-lookup"><span data-stu-id="cf6cd-117">About multipathing components</span></span>
<span data-ttu-id="cf6cd-118">La característica de múltiples rutas en Linux consta de componentes del kernel y de componentes del espacio de usuario, como se indica más abajo.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-118">Multipathing in Linux consists of kernel components and user-space components as tabulated below.</span></span>

* <span data-ttu-id="cf6cd-119">**Kernel**: componente principal de hello es hello *dispositivo asignador* que redistribuye i/OS y admite la conmutación por error para las rutas de acceso y grupos de la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-119">**Kernel**: hello main component is hello *device-mapper* that reroutes I/O and supports failover for paths and path groups.</span></span>

* <span data-ttu-id="cf6cd-120">**Espacio de usuario**: se trata de *herramientas de múltiples rutas* que administrar detectar dispositivos indicando a módulo de múltiples rutas de acceso de dispositivo asignador de hello qué toodo.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-120">**User-space**: These are *multipath-tools* that manage multipathed devices by instructing hello device-mapper multipath module what toodo.</span></span> <span data-ttu-id="cf6cd-121">herramientas de Hola se componen de:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-121">hello tools consist of:</span></span>
   
   * <span data-ttu-id="cf6cd-122">**Multipath**: muestra y configura los dispositivos con múltiples rutas.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-122">**Multipath**: lists and configures multipathed devices.</span></span>
   * <span data-ttu-id="cf6cd-123">**Multipathd**: daemon que se ejecuta de rutas de acceso de Hola de múltiples rutas y monitores.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-123">**Multipathd**: daemon that executes multipath and monitors hello paths.</span></span>
   * <span data-ttu-id="cf6cd-124">**Nombre de Devmap**: proporciona un significativo tooudev de nombre de dispositivo para devmaps.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-124">**Devmap-name**: provides a meaningful device-name tooudev for devmaps.</span></span>
   * <span data-ttu-id="cf6cd-125">**Kpartx**: asigna devmaps lineal toodevice particiones toomake múltiples rutas mapas cargas.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-125">**Kpartx**: maps linear devmaps toodevice partitions toomake multipath maps partitionable.</span></span>
   * <span data-ttu-id="cf6cd-126">**Multipath.conf**: archivo de configuración del demonio de múltiples rutas de acceso que es usado toooverwrite Hola configuración integrada tabla.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-126">**Multipath.conf**: configuration file for multipath daemon that is used toooverwrite hello built-in configuration table.</span></span>

### <a name="about-hello-multipathconf-configuration-file"></a><span data-ttu-id="cf6cd-127">Sobre el archivo de configuración de hello multipath.conf</span><span class="sxs-lookup"><span data-stu-id="cf6cd-127">About hello multipath.conf configuration file</span></span>
<span data-ttu-id="cf6cd-128">archivo de configuración de Hello `/etc/multipath.conf` realiza muchos Hola múltiples rutas características configurables por el usuario.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-128">hello configuration file `/etc/multipath.conf` makes many of hello multipathing features user-configurable.</span></span> <span data-ttu-id="cf6cd-129">Hola `multipath` daemon de kernel hello y comando `multipathd` usar la información de este archivo.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-129">hello `multipath` command and hello kernel daemon `multipathd` use information found in this file.</span></span> <span data-ttu-id="cf6cd-130">archivo Hello se consulta solo durante la configuración de Hola de dispositivos de múltiples rutas de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-130">hello file is consulted only during hello configuration of hello multipath devices.</span></span> <span data-ttu-id="cf6cd-131">Asegúrese de que todos los cambios se realizan antes de ejecutar hello `multipath` comando.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-131">Make sure that all changes are made before you run hello `multipath` command.</span></span> <span data-ttu-id="cf6cd-132">Si modifica el archivo hello posteriormente, se necesita toostop e iniciar multipathd nuevo para hello cambios tootake efecto.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-132">If you modify hello file afterwards, you will need toostop and start multipathd again for hello changes tootake effect.</span></span>

<span data-ttu-id="cf6cd-133">Hola multipath.conf tiene cinco secciones:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-133">hello multipath.conf has five sections:</span></span>

- <span data-ttu-id="cf6cd-134">**Valores predeterminados de nivel de sistema***(defaults)*: puede invalidar los valores predeterminados de nivel de sistema.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-134">**System level defaults** *(defaults)*: You can override system level defaults.</span></span>
- <span data-ttu-id="cf6cd-135">**En la lista negra dispositivos** *(lista negra)*: puede especificar la lista de Hola de dispositivos que no deben controlarse mediante el asignador de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-135">**Blacklisted devices** *(blacklist)*: You can specify hello list of devices that should not be controlled by device-mapper.</span></span>
- <span data-ttu-id="cf6cd-136">**Generar una lista negra excepciones** *(blacklist_exceptions)*: puede identificar toobe de dispositivos específicos que se tratan como dispositivos de múltiples rutas, incluso si aparece en la lista negra de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-136">**Blacklist exceptions** *(blacklist_exceptions)*: You can identify specific devices toobe treated as multipath devices even if listed in hello blacklist.</span></span>
- <span data-ttu-id="cf6cd-137">**Configuración específica del controlador de almacenamiento** *(dispositivos)*: puede especificar opciones de configuración que serán aplicado toodevices que tienen información de proveedor y producto.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-137">**Storage controller specific settings** *(devices)*: You can specify configuration settings that will be applied toodevices that have Vendor and Product information.</span></span>
- <span data-ttu-id="cf6cd-138">**Configuración específica del dispositivo** *(multipaths)*: puede usar esta configuración sección toofine ajustar Hola para cada LUN.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-138">**Device specific settings** *(multipaths)*: You can use this section toofine-tune hello configuration settings for individual LUNs.</span></span>

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a><span data-ttu-id="cf6cd-139">Configurar múltiples rutas en el host conectado tooLinux de StorSimple</span><span class="sxs-lookup"><span data-stu-id="cf6cd-139">Configure multipathing on StorSimple connected tooLinux host</span></span>
<span data-ttu-id="cf6cd-140">Un host de Linux de StorSimple dispositivo conectado tooa puede configurarse para alta disponibilidad y equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-140">A StorSimple device connected tooa Linux host can be configured for high availability and load balancing.</span></span> <span data-ttu-id="cf6cd-141">Por ejemplo, si el host de Linux de hello tiene dos interfaces conectadas toohello hello y SAN dispositivo tiene dos interfaces conectadas toohello SAN que estas interfaces se encuentran en Hola misma subred, a continuación, habrá 4 rutas disponibles.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-141">For example, if hello Linux host has two interfaces connected toohello SAN and hello device has two interfaces connected toohello SAN such that these interfaces are on hello same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="cf6cd-142">Sin embargo, si cada interfaz de datos en la interfaz de dispositivo y el host de Hola se encuentran en una subred IP diferente (y no enrutables), a continuación, las rutas de acceso de solo 2 estará disponibles.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-142">However, if each DATA interface on hello device and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span> <span data-ttu-id="cf6cd-143">Puede configurar múltiples rutas tooautomatically detectar todas las rutas de acceso disponibles de hello, elegir un algoritmo de equilibrio de carga para esas rutas, aplicar opciones de configuración específicas para volúmenes de StorSimple solo y, a continuación, habilitar y comprobar múltiples rutas.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-143">You can configure multipathing tooautomatically discover all hello available paths, choose a load-balancing algorithm for those paths, apply specific configuration settings for StorSimple-only volumes, and then enable and verify multipathing.</span></span>

<span data-ttu-id="cf6cd-144">Hello siguiente procedimiento describe cómo tooconfigure de múltiples rutas cuando un dispositivo de StorSimple con dos interfaces de red está conectado tooa host con dos interfaces de red.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-144">hello following procedure describes how tooconfigure multipathing when a StorSimple device with two network interfaces is connected tooa host with two network interfaces.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf6cd-145">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cf6cd-145">Prerequisites</span></span>
<span data-ttu-id="cf6cd-146">Esta sección describe los requisitos previos de configuración de hello para el servidor de CentOS y el dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-146">This section details hello configuration prerequisites for CentOS server and your StorSimple device.</span></span>

### <a name="on-centos-host"></a><span data-ttu-id="cf6cd-147">En el host CentOS</span><span class="sxs-lookup"><span data-stu-id="cf6cd-147">On CentOS host</span></span>
1. <span data-ttu-id="cf6cd-148">Asegúrese de que el host CentOS tiene dos interfaces de red habilitadas.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-148">Make sure that your CentOS host has 2 network interfaces enabled.</span></span> <span data-ttu-id="cf6cd-149">Escriba:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-149">Type:</span></span>
   
    `ifconfig`
   
    <span data-ttu-id="cf6cd-150">Hello en el ejemplo siguiente se muestra el resultado de hello cuando dos interfaces de red (`eth0` y `eth1`) están presentes en el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-150">hello following example shows hello output when two network interfaces (`eth0` and `eth1`) are present on hello host.</span></span>
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. <span data-ttu-id="cf6cd-151">Instale *iSCSI-initiator-utils* en el servidor CentOS.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-151">Install *iSCSI-initiator-utils* on your CentOS server.</span></span> <span data-ttu-id="cf6cd-152">Realizar Hola siguiendo los pasos tooinstall *utilidades de iniciador iSCSI*.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-152">Perform hello following steps tooinstall *iSCSI-initiator-utils*.</span></span>
   
   1. <span data-ttu-id="cf6cd-153">Inicie sesión como `root` en el host CentOS.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-153">Log on as `root` into your CentOS host.</span></span>
   2. <span data-ttu-id="cf6cd-154">Instalar hello *utilidades de iniciador iSCSI*.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-154">Install hello *iSCSI-initiator-utils*.</span></span> <span data-ttu-id="cf6cd-155">Escriba:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-155">Type:</span></span>
      
       `yum install iscsi-initiator-utils`
   3. <span data-ttu-id="cf6cd-156">Después de hello *utilidades de iniciador iSCSI* está correctamente instalado, inicie el servicio iSCSI Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-156">After hello *iSCSI-Initiator-utils* is successfully installed, start hello iSCSI service.</span></span> <span data-ttu-id="cf6cd-157">Escriba:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-157">Type:</span></span>
      
       `service iscsid start`
      
       <span data-ttu-id="cf6cd-158">En ocasiones, `iscsid` realmente no se puede iniciar y Hola `--force` opción puede ser necesaria</span><span class="sxs-lookup"><span data-stu-id="cf6cd-158">On occasions, `iscsid` may not actually start and hello `--force` option may be needed</span></span>
   4. <span data-ttu-id="cf6cd-159">tooensure que el iniciador iSCSI está habilitado durante el tiempo de arranque, use hello `chkconfig` servicio de hello tooenable de comandos.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-159">tooensure that your iSCSI initiator is enabled during boot time, use hello `chkconfig` command tooenable hello service.</span></span>
      
       `chkconfig iscsi on`
   5. <span data-ttu-id="cf6cd-160">tooverify que estaba correctamente el programa de instalación, ejecute el comando de hello:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-160">tooverify that that it was properly setup, run hello command:</span></span>
      
       `chkconfig --list | grep iscsi`
      
       <span data-ttu-id="cf6cd-161">A continuación se muestra una salida de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-161">A sample output is shown below.</span></span>
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       <span data-ttu-id="cf6cd-162">En hello ejemplo anterior, puede ver que el entorno de iSCSI se ejecutará en tiempo de arranque en ejecución niveles 2, 3, 4 y 5.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-162">From hello above example, you can see that your iSCSI environment will run on boot time on run levels 2, 3, 4, and 5.</span></span>
3. <span data-ttu-id="cf6cd-163">Instale *device-mapper-multipath*.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-163">Install *device-mapper-multipath*.</span></span> <span data-ttu-id="cf6cd-164">Escriba:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-164">Type:</span></span>
   
    `yum install device-mapper-multipath`
   
    <span data-ttu-id="cf6cd-165">se iniciará la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-165">hello installation will start.</span></span> <span data-ttu-id="cf6cd-166">Tipo de **Y** toocontinue cuando se le pida confirmación.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-166">Type **Y** toocontinue when prompted for confirmation.</span></span>

### <a name="on-storsimple-device"></a><span data-ttu-id="cf6cd-167">En el dispositivo de StorSimple</span><span class="sxs-lookup"><span data-stu-id="cf6cd-167">On StorSimple device</span></span>
<span data-ttu-id="cf6cd-168">El dispositivo de StorSimple debe disponer de:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-168">Your StorSimple device should have:</span></span>

* <span data-ttu-id="cf6cd-169">Un mínimo de dos interfaces habilitadas para iSCSI.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-169">A minimum of two interfaces enabled for iSCSI.</span></span> <span data-ttu-id="cf6cd-170">tooverify que dos interfaces están habilitadas para iSCSI en el dispositivo StorSimple, lleve a cabo Hola pasos de hello portal de Azure clásico para el dispositivo StorSimple:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-170">tooverify that two interfaces are iSCSI-enabled on your StorSimple device, perform hello following steps in hello Azure classic portal for your StorSimple device:</span></span>
  
  1. <span data-ttu-id="cf6cd-171">Inicie sesión en el portal clásico de hello para el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-171">Log into hello classic portal for your StorSimple device.</span></span>
  2. <span data-ttu-id="cf6cd-172">Seleccione el servicio StorSimple Manager, haga clic en **dispositivos** y elija el dispositivo de StorSimple específico de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-172">Select your StorSimple Manager service, click **Devices** and choose hello specific StorSimple device.</span></span> <span data-ttu-id="cf6cd-173">Haga clic en **configurar** y comprobar la configuración de interfaz de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-173">Click **Configure** and verify hello network interface settings.</span></span> <span data-ttu-id="cf6cd-174">A continuación se muestra una captura de pantalla con dos interfaces de red habilitadas para iSCSI.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-174">A screenshot with two iSCSI-enabled network interfaces is shown below.</span></span> <span data-ttu-id="cf6cd-175">En este caso DATA 2 y DATA 3, las dos interfaces de 10 GbE están habilitadas para iSCSI.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-175">Here DATA 2 and DATA 3, both 10 GbE interfaces are enabled for iSCSI.</span></span>
     
      ![Configuración de MPIO StorSimple DATA 2](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![Configuración de MPIO StorSimple DATA 3](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      <span data-ttu-id="cf6cd-178">Hola **configurar** página</span><span class="sxs-lookup"><span data-stu-id="cf6cd-178">In hello **Configure** page</span></span>
     
     1. <span data-ttu-id="cf6cd-179">Asegúrese de que ambas interfaces de red están habilitadas para iSCSI.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-179">Ensure that both network interfaces are iSCSI-enabled.</span></span> <span data-ttu-id="cf6cd-180">Hola **habilitado para iSCSI** campo debe estar establecido demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-180">hello **iSCSI enabled** field should be set too**Yes**.</span></span>
     2. <span data-ttu-id="cf6cd-181">Asegúrese de que las interfaces de red de hello tienen Hola velocidad del mismo, debe ser 1 GbE o 10 GbE.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-181">Ensure that hello network interfaces have hello same speed, both should be 1 GbE or 10 GbE.</span></span>
     3. <span data-ttu-id="cf6cd-182">Anote las direcciones IPv4 de Hola de interfaces de hello habilitada para iSCSI y guardar para su uso posterior en el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-182">Note hello IPv4 addresses of hello iSCSI-enabled interfaces and save for later use on hello host.</span></span>
* <span data-ttu-id="cf6cd-183">interfaces de iSCSI de Hello en el dispositivo de StorSimple deben ser accesibles desde el servidor de CentOS Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-183">hello iSCSI interfaces on your StorSimple device should be reachable from hello CentOS server.</span></span>
      <span data-ttu-id="cf6cd-184">tooverify, necesita las direcciones IP tooprovide Hola de las interfaces de red habilitada para iSCSI de StorSimple en su servidor host.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-184">tooverify this, you need tooprovide hello IP addresses of your StorSimple iSCSI-enabled network interfaces on your host server.</span></span> <span data-ttu-id="cf6cd-185">Hola comandos usados y Hola salida correspondiente con DATA2 (10.126.162.25) y DATA3 (10.126.162.26) se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-185">hello commands used and hello corresponding output with DATA2 (10.126.162.25) and DATA3 (10.126.162.26) is shown below:</span></span>
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a><span data-ttu-id="cf6cd-186">Configuración de hardware</span><span class="sxs-lookup"><span data-stu-id="cf6cd-186">Hardware configuration</span></span>
<span data-ttu-id="cf6cd-187">Se recomienda que se conectan en rutas de acceso independientes para la redundancia de la dos interfaces de red iSCSI Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-187">We recommend that you connect hello two iSCSI network interfaces on separate paths for redundancy.</span></span> <span data-ttu-id="cf6cd-188">Hola siguiente ilustración muestra la configuración de hardware recomendada de Hola para lograr alta disponibilidad y equilibrio de carga de múltiples rutas para el servidor de CentOS y el dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-188">hello figure below shows hello recommended hardware configuration for high availability and load-balancing multipathing for your CentOS server and StorSimple device.</span></span>

![Configuración de hardware MPIO para StorSimple tooLinux host](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

<span data-ttu-id="cf6cd-190">Como se muestra en hello anterior figura:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-190">As shown in hello preceding figure:</span></span>

* <span data-ttu-id="cf6cd-191">El dispositivo StorSimple está en una configuración activa-pasiva con dos controladores.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-191">Your StorSimple device is in an active-passive configuration with two controllers.</span></span>
* <span data-ttu-id="cf6cd-192">Dos conmutadores de SAN son controladores de dispositivo de tooyour conectado.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-192">Two SAN switches are connected tooyour device controllers.</span></span>
* <span data-ttu-id="cf6cd-193">En el dispositivo StorSimple se habilitan dos iniciadores iSCSI.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-193">Two iSCSI initiators are enabled on your StorSimple device.</span></span>
* <span data-ttu-id="cf6cd-194">Dos interfaces de red están habilitadas en el host CentOS.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-194">Two network interfaces are enabled on your CentOS host.</span></span>

<span data-ttu-id="cf6cd-195">Hola por encima de configuración brindará 4 rutas de acceso independientes entre el host de hello y dispositivo si las interfaces de host y los datos de hello sean enrutables.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-195">hello above configuration will yield 4 separate paths between your device and hello host if hello host and data interfaces are routable.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="cf6cd-196">Recomendamos no combinar interfaces de red de 1 GbE y de 10 GbE para las múltiples rutas.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-196">We recommend that you do not mix 1 GbE and 10 GbE network interfaces for multipathing.</span></span> <span data-ttu-id="cf6cd-197">Cuando se usan dos interfaces de red, ambas interfaces Hola deben ser Hola idéntico tipo.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-197">When using two network interfaces, both hello interfaces should be hello identical type.</span></span>
> * <span data-ttu-id="cf6cd-198">En el dispositivo StorSimple, DATA0, DATA1, DATA4 y DATA5 son interfaces de 1 GbE mientras que DATA2 y DATA3 son interfaces de red de 10 GbE.|</span><span class="sxs-lookup"><span data-stu-id="cf6cd-198">On your StorSimple device, DATA0, DATA1, DATA4 and DATA5 are 1 GbE interfaces whereas DATA2 and DATA3 are 10 GbE network interfaces.|</span></span>
> 
> 

## <a name="configuration-steps"></a><span data-ttu-id="cf6cd-199">Pasos de configuración</span><span class="sxs-lookup"><span data-stu-id="cf6cd-199">Configuration steps</span></span>
<span data-ttu-id="cf6cd-200">pasos de configuración de Hola de múltiples rutas implican la configuración de rutas de acceso disponibles hello para la detección automática, especificar toouse algoritmo Hola equilibrio de carga, habilitar múltiples rutas y por último, comprobar la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-200">hello configuration steps for multipathing involve configuring hello available paths for automatic discovery, specifying hello load-balancing algorithm toouse, enabling multipathing and finally verifying hello configuration.</span></span> <span data-ttu-id="cf6cd-201">Cada uno de estos pasos se explica con detalle en las secciones siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-201">Each of these steps is discussed in detail in hello following sections.</span></span>

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a><span data-ttu-id="cf6cd-202">Paso 1: Configuración de múltiples rutas para la detección automática</span><span class="sxs-lookup"><span data-stu-id="cf6cd-202">Step 1: Configure multipathing for automatic discovery</span></span>
<span data-ttu-id="cf6cd-203">dispositivos de Hello compatible con múltiples rutas pueden detectar y configurar automáticamente.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-203">hello multipath-supported devices can be automatically discovered and configured.</span></span>

1. <span data-ttu-id="cf6cd-204">Inicialice el archivo `/etc/multipath.conf` .</span><span class="sxs-lookup"><span data-stu-id="cf6cd-204">Initialize `/etc/multipath.conf` file.</span></span> <span data-ttu-id="cf6cd-205">Escriba:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-205">Type:</span></span>
   
     `mpathconf --enable`
   
    <span data-ttu-id="cf6cd-206">Hola encima comando creará una `sample/etc/multipath.conf` archivo.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-206">hello above command will create a `sample/etc/multipath.conf` file.</span></span>
2. <span data-ttu-id="cf6cd-207">Inicie el servicio de múltiples rutas.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-207">Start multipath service.</span></span> <span data-ttu-id="cf6cd-208">Escriba:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-208">Type:</span></span>
   
    `service multipathd start`
   
    <span data-ttu-id="cf6cd-209">Verá Hola después de salida:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-209">You will see hello following output:</span></span>
   
    `Starting multipathd daemon:`
3. <span data-ttu-id="cf6cd-210">Habilite la detección automática de múltiples rutas.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-210">Enable automatic discovery of multipaths.</span></span> <span data-ttu-id="cf6cd-211">Escriba:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-211">Type:</span></span>
   
    `mpathconf --find_multipaths y`
   
    <span data-ttu-id="cf6cd-212">Esto modificará Hola sección de valores predeterminados de su `multipath.conf` tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-212">This will modify hello defaults section of your `multipath.conf` as shown below:</span></span>
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a><span data-ttu-id="cf6cd-213">Paso 2: Configuración de múltiples rutas para volúmenes de StorSimple</span><span class="sxs-lookup"><span data-stu-id="cf6cd-213">Step 2: Configure multipathing for StorSimple volumes</span></span>
<span data-ttu-id="cf6cd-214">De forma predeterminada, todos los dispositivos son negros aparecen en el archivo de multipath.conf hello y se omitirán.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-214">By default, all devices are black listed in hello multipath.conf file and will be bypassed.</span></span> <span data-ttu-id="cf6cd-215">Necesitará toocreate lista negra excepciones tooallow multirruta para volúmenes de los dispositivos de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-215">You will need toocreate blacklist exceptions tooallow multipathing for volumes from StorSimple devices.</span></span>

1. <span data-ttu-id="cf6cd-216">Editar hello `/etc/mulitpath.conf` archivo.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-216">Edit hello `/etc/mulitpath.conf` file.</span></span> <span data-ttu-id="cf6cd-217">Escriba:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-217">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="cf6cd-218">Busque la sección de blacklist_exceptions de hello en el archivo de multipath.conf Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-218">Locate hello blacklist_exceptions section in hello multipath.conf file.</span></span> <span data-ttu-id="cf6cd-219">El dispositivo de StorSimple debe toobe aparece como una excepción de la lista negra de esta sección.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-219">Your StorSimple device needs toobe listed as a blacklist exception in this section.</span></span> <span data-ttu-id="cf6cd-220">Puede quite la marca de comentario relevante líneas toomodify de este archivo, tal y como se muestra a continuación (use solo Hola modelo específico de dispositivo de Hola que esté utilizando):</span><span class="sxs-lookup"><span data-stu-id="cf6cd-220">You can uncomment relevant lines in this file toomodify it as shown below (use only hello specific model of hello device you are using):</span></span>
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a><span data-ttu-id="cf6cd-221">Paso 3: Configuración de múltiples rutas por round-robin</span><span class="sxs-lookup"><span data-stu-id="cf6cd-221">Step 3: Configure round-robin multipathing</span></span>
<span data-ttu-id="cf6cd-222">Este algoritmo de equilibrio de carga utiliza todos los controlador activo de hello toohello multipaths disponibles de forma equilibrada, round robin.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-222">This load-balancing algorithm uses all hello available multipaths toohello active controller in a balanced, round-robin fashion.</span></span>

1. <span data-ttu-id="cf6cd-223">Editar hello `/etc/multipath.conf` archivo.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-223">Edit hello `/etc/multipath.conf` file.</span></span> <span data-ttu-id="cf6cd-224">Escriba:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-224">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="cf6cd-225">En hello `defaults` Hola de conjunto, en una sección `path_grouping_policy` demasiado`multibus`.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-225">Under hello `defaults` section, set hello `path_grouping_policy` too`multibus`.</span></span> <span data-ttu-id="cf6cd-226">Hola `path_grouping_policy` especifica tooapply toounspecified multipaths de agrupación directiva de hello predeterminado ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-226">hello `path_grouping_policy` specifies hello default path grouping policy tooapply toounspecified multipaths.</span></span> <span data-ttu-id="cf6cd-227">sección de valores predeterminados de Hello tendrá un aspecto tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-227">hello defaults section will look as shown below.</span></span>
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> <span data-ttu-id="cf6cd-228">Hola valores más comunes de `path_grouping_policy` incluyen:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-228">hello most common values of `path_grouping_policy` include:</span></span>
> 
> * <span data-ttu-id="cf6cd-229">conmutación por error = 1 ruta de acceso por grupo de prioridad</span><span class="sxs-lookup"><span data-stu-id="cf6cd-229">failover = 1 path per priority group</span></span>
> * <span data-ttu-id="cf6cd-230">multibus = todas las rutas de acceso válidas en un grupo de prioridad</span><span class="sxs-lookup"><span data-stu-id="cf6cd-230">multibus = all valid paths in 1 priority group</span></span>
> 
> 

### <a name="step-4-enable-multipathing"></a><span data-ttu-id="cf6cd-231">Paso 4: Habilitación de múltiples rutas</span><span class="sxs-lookup"><span data-stu-id="cf6cd-231">Step 4: Enable multipathing</span></span>
1. <span data-ttu-id="cf6cd-232">Reinicie hello `multipathd` daemon.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-232">Restart hello `multipathd` daemon.</span></span> <span data-ttu-id="cf6cd-233">Escriba:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-233">Type:</span></span>
   
    `service multipathd restart`
2. <span data-ttu-id="cf6cd-234">salida de Hello será tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-234">hello output will be as shown below:</span></span>
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a><span data-ttu-id="cf6cd-235">Paso 5: Comprobación de múltiples rutas</span><span class="sxs-lookup"><span data-stu-id="cf6cd-235">Step 5: Verify multipathing</span></span>
1. <span data-ttu-id="cf6cd-236">En primer lugar, asegúrese de que iSCSI se establece conexión con el dispositivo de StorSimple de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-236">First make sure that iSCSI connection is established with hello StorSimple device as follows:</span></span>
   
   <span data-ttu-id="cf6cd-237">a.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-237">a.</span></span> <span data-ttu-id="cf6cd-238">Detecte su dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-238">Discover your StorSimple device.</span></span> <span data-ttu-id="cf6cd-239">Escriba:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-239">Type:</span></span>
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    <span data-ttu-id="cf6cd-240">salida de Hello cuando una dirección IP de DATA0 es 10.126.162.25 y el puerto 3260 se abre en el dispositivo de StorSimple de hello para el tráfico saliente iSCSI es tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-240">hello output when IP address for DATA0 is 10.126.162.25 and port 3260 is opened on hello StorSimple device for outbound iSCSI traffic is as shown below:</span></span>
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    <span data-ttu-id="cf6cd-241">Hola copia IQN del dispositivo de StorSimple, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, de hello anterior de salida.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-241">Copy hello IQN of your StorSimple device, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, from hello preceding output.</span></span>

   <span data-ttu-id="cf6cd-242">b.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-242">b.</span></span> <span data-ttu-id="cf6cd-243">Conecte el dispositivo toohello usando el IQN de destino.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-243">Connect toohello device using target IQN.</span></span> <span data-ttu-id="cf6cd-244">dispositivo de StorSimple de Hello es destino de iSCSI Hola aquí.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-244">hello StorSimple device is hello iSCSI target here.</span></span> <span data-ttu-id="cf6cd-245">Escriba:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-245">Type:</span></span>

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    <span data-ttu-id="cf6cd-246">Hello en el ejemplo siguiente se muestra la salida con un IQN de destino de `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-246">hello following example shows output with a target IQN of `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span></span> <span data-ttu-id="cf6cd-247">salida de Hello indica que se han conectado correctamente toohello dos interfaces de red habilitada para iSCSI en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-247">hello output indicates that you have successfully connected toohello two iSCSI-enabled network interfaces on your device.</span></span>

    ```
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    <span data-ttu-id="cf6cd-248">Si ve interfaz sólo un host y dos rutas de acceso aquí, deberá tooenable ambas interfaces hello en el host para iSCSI.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-248">If you see only one host interface and two paths here, then you need tooenable both hello interfaces on host for iSCSI.</span></span> <span data-ttu-id="cf6cd-249">Puede seguir hello [instrucciones en la documentación de Linux](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span><span class="sxs-lookup"><span data-stu-id="cf6cd-249">You can follow hello [detailed instructions in Linux documentation](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span></span>

2. <span data-ttu-id="cf6cd-250">Un volumen es servidor de CentOS de toohello expuesto desde el dispositivo de StorSimple Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-250">A volume is exposed toohello CentOS server from hello StorSimple device.</span></span> <span data-ttu-id="cf6cd-251">Para obtener más información, consulte [paso 6: crear un volumen](storsimple-deployment-walkthrough.md#step-6-create-a-volume) a través de hello portal de Azure clásico en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-251">For more information, see [Step 6: Create a volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via hello Azure classic portal on your StorSimple device.</span></span>

3. <span data-ttu-id="cf6cd-252">Compruebe las rutas de acceso disponibles Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-252">Verify hello available paths.</span></span> <span data-ttu-id="cf6cd-253">Escriba:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-253">Type:</span></span>

      ```
      multipath –l
      ```

      <span data-ttu-id="cf6cd-254">Hola de ejemplo siguiente muestra la salida de hello para dos interfaces de red en una interfaz de red de host único de StorSimple dispositivo conectado tooa con dos rutas de acceso disponibles.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-254">hello following example shows hello output for two network interfaces on a StorSimple device connected tooa single host network interface with two available paths.</span></span>

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        hello following example shows hello output for two network interfaces on a StorSimple device connected tootwo host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After hello paths are configured, refer toohello specific instructions on your host operating system (Centos 6.6) toomount and format this volume.

## <a name="troubleshoot-multipathing"></a><span data-ttu-id="cf6cd-255">Solución de problemas de múltiples rutas</span><span class="sxs-lookup"><span data-stu-id="cf6cd-255">Troubleshoot multipathing</span></span>
<span data-ttu-id="cf6cd-256">En esta sección se proporcionan algunos consejos útiles si surge algún problema durante la configuración de múltiples rutas.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-256">This section provides some helpful tips if you run into any issues during multipathing configuration.</span></span>

<span data-ttu-id="cf6cd-257">P:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-257">Q.</span></span> <span data-ttu-id="cf6cd-258">No veo cambios hello en `multipath.conf` archivo surten efecto.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-258">I do not see hello changes in `multipath.conf` file taking effect.</span></span>

<span data-ttu-id="cf6cd-259">A.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-259">A.</span></span> <span data-ttu-id="cf6cd-260">Si ha realizado cualquier toohello cambios `multipath.conf` archivo, necesitará que el servicio de múltiples rutas de toorestart Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-260">If you have made any changes toohello `multipath.conf` file, you will need toorestart hello multipathing service.</span></span> <span data-ttu-id="cf6cd-261">Escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-261">Type hello following command:</span></span>

    service multipathd restart

<span data-ttu-id="cf6cd-262">P:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-262">Q.</span></span> <span data-ttu-id="cf6cd-263">He habilitado dos interfaces de red en el host de Hola y dos interfaces de red en el dispositivo StorSimple Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-263">I have enabled two network interfaces on hello StorSimple device and two network interfaces on hello host.</span></span> <span data-ttu-id="cf6cd-264">Cuando la lista de rutas de acceso disponibles hello, veo dos rutas de acceso.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-264">When I list hello available paths, I see only two paths.</span></span> <span data-ttu-id="cf6cd-265">Esperaba toosee cuatro rutas disponibles.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-265">I expected toosee four available paths.</span></span>

<span data-ttu-id="cf6cd-266">A.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-266">A.</span></span> <span data-ttu-id="cf6cd-267">Asegúrese de que las rutas de acceso de hello dos se encuentran en hello misma subred y enrutables.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-267">Make sure that hello two paths are on hello same subnet and routable.</span></span> <span data-ttu-id="cf6cd-268">Si son las interfaces de red de hello en distintas redes VLAN y no enrutables, verá dos rutas de acceso.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-268">If hello network interfaces are on different vLANs and not routable, you will see only two paths.</span></span> <span data-ttu-id="cf6cd-269">Una manera de tooverify se trata de toomake seguro de que puede comunicarse con ambas interfaces de host de Hola desde una interfaz de red en el dispositivo StorSimple Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-269">One way tooverify this is toomake sure that you can reach both hello host interfaces from a network interface on hello StorSimple device.</span></span> <span data-ttu-id="cf6cd-270">Necesitará demasiado[póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) como esta comprobación solo puede realizarse a través de una sesión de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-270">You will need too[contact Microsoft Support](storsimple-contact-microsoft-support.md) as this verification can only be done via a support session.</span></span>

<span data-ttu-id="cf6cd-271">P:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-271">Q.</span></span> <span data-ttu-id="cf6cd-272">Cuando muestro las rutas de acceso disponibles, no aparece ninguna salida.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-272">When I list available paths, I do not see any output.</span></span>

<span data-ttu-id="cf6cd-273">A.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-273">A.</span></span> <span data-ttu-id="cf6cd-274">Por lo general, no ve las rutas de acceso de detectar sugiere un problema con el demonio de múltiples rutas de Hola y es más probable es que cualquier problema radica en hello `multipath.conf` archivo.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-274">Typically, not seeing any multipathed paths suggests a problem with hello multipathing daemon, and it’s most likely that any problem here lies in hello `multipath.conf` file.</span></span>

<span data-ttu-id="cf6cd-275">También sería conveniente comprobar que realmente puede ver algunos discos después de conectarse toohello destino, tal y como se recibe ninguna respuesta de anuncios de Hola múltiples rutas también puede significar que no tiene ningún disco.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-275">It would also be worth checking that you can actually see some disks after connecting toohello target, as no response from hello multipath listings could also mean you don’t have any disks.</span></span>

* <span data-ttu-id="cf6cd-276">Usar hello después de bus SCSI de comando toorescan hello:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-276">Use hello following command toorescan hello SCSI bus:</span></span>
  
    <span data-ttu-id="cf6cd-277">`$ rescan-scsi-bus.sh `(part of sg3_utils package)</span><span class="sxs-lookup"><span data-stu-id="cf6cd-277">`$ rescan-scsi-bus.sh `(part of sg3_utils package)</span></span>
* <span data-ttu-id="cf6cd-278">Escriba Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-278">Type hello following commands:</span></span>
  
    `$ dmesg | grep sd*`
     
     <span data-ttu-id="cf6cd-279">O</span><span class="sxs-lookup"><span data-stu-id="cf6cd-279">Or</span></span>
  
    `$ fdisk –l`
  
    <span data-ttu-id="cf6cd-280">Se devolverán los detalles de los discos agregados recientemente.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-280">These will return details of recently added disks.</span></span>
* <span data-ttu-id="cf6cd-281">toodetermine si se trata de un disco de StorSimple, usar hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-281">toodetermine whether it is a StorSimple disk, use hello following commands:</span></span>
  
    `cat /sys/block/<DISK>/device/model`
  
    <span data-ttu-id="cf6cd-282">Esto devolverá una cadena, que determinará si es un disco de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-282">This will return a string, which will determine if it’s a StorSimple disk.</span></span>

<span data-ttu-id="cf6cd-283">Una causa menos probable pero posible también podría ser iscsid pid desusado.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-283">A less likely but possible cause could also be stale iscsid pid.</span></span> <span data-ttu-id="cf6cd-284">Usar hello siguientes comando toolog off de sesiones de iSCSI de hello:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-284">Use hello following command toolog off from hello iSCSI sessions:</span></span>

    iscsiadm -m node --logout -p <Target_IP>

<span data-ttu-id="cf6cd-285">Repita este comando para todas las interfaces de red de hello conectado en el destino de iSCSI de hello, que es el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-285">Repeat this command for all hello connected network interfaces on hello iSCSI target, which is your StorSimple device.</span></span> <span data-ttu-id="cf6cd-286">Una vez que ha cerrado la sesión de todas las sesiones de iSCSI de hello, utilice sesión iSCSI de hello iSCSI target IQN tooreestablish Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-286">Once you have logged off from all hello iSCSI sessions, use hello iSCSI target IQN tooreestablish hello iSCSI session.</span></span> <span data-ttu-id="cf6cd-287">Escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-287">Type hello following command:</span></span>

    iscsiadm -m node --login -T <TARGET_IQN>


<span data-ttu-id="cf6cd-288">P:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-288">Q.</span></span> <span data-ttu-id="cf6cd-289">No estoy seguro de si el dispositivo está en la lista blanca.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-289">I am not sure if my device is whitelisted.</span></span>

<span data-ttu-id="cf6cd-290">A.</span><span class="sxs-lookup"><span data-stu-id="cf6cd-290">A.</span></span> <span data-ttu-id="cf6cd-291">tooverify si el dispositivo está en la lista blanca, utilice Hola siguiente comando interactivo para solucionar problemas:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-291">tooverify whether your device is whitelisted, use hello following troubleshooting interactive command:</span></span>

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


<span data-ttu-id="cf6cd-292">Para obtener más información, consulte demasiado[usar la solución de problemas de comando interactivo de múltiples rutas](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span><span class="sxs-lookup"><span data-stu-id="cf6cd-292">For more information, go too[use troubleshooting interactive command for multipathing](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span></span>

## <a name="list-of-useful-commands"></a><span data-ttu-id="cf6cd-293">Lista de comandos útiles</span><span class="sxs-lookup"><span data-stu-id="cf6cd-293">List of useful commands</span></span>
| <span data-ttu-id="cf6cd-294">Cuando se le pida confirmación, escriba </span><span class="sxs-lookup"><span data-stu-id="cf6cd-294">Type</span></span> | <span data-ttu-id="cf6cd-295">Comando</span><span class="sxs-lookup"><span data-stu-id="cf6cd-295">Command</span></span> | <span data-ttu-id="cf6cd-296">Description</span><span class="sxs-lookup"><span data-stu-id="cf6cd-296">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cf6cd-297">**iSCSI**</span><span class="sxs-lookup"><span data-stu-id="cf6cd-297">**iSCSI**</span></span> |`service iscsid start` |<span data-ttu-id="cf6cd-298">Iniciar el servicio iSCSI</span><span class="sxs-lookup"><span data-stu-id="cf6cd-298">Start iSCSI service</span></span> |
| &nbsp; |`service iscsid stop` |<span data-ttu-id="cf6cd-299">Detener el servicio iSCSI</span><span class="sxs-lookup"><span data-stu-id="cf6cd-299">Stop iSCSI service</span></span> |
| &nbsp; |`service iscsid restart` |<span data-ttu-id="cf6cd-300">Reiniciar el servicio iSCSI</span><span class="sxs-lookup"><span data-stu-id="cf6cd-300">Restart iSCSI service</span></span> |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |<span data-ttu-id="cf6cd-301">Detección de destinos disponibles en hello especificado dirección</span><span class="sxs-lookup"><span data-stu-id="cf6cd-301">Discover available targets on hello specified address</span></span> |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |<span data-ttu-id="cf6cd-302">Inicie sesión en el destino de iSCSI toohello</span><span class="sxs-lookup"><span data-stu-id="cf6cd-302">Log in toohello iSCSI target</span></span> |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |<span data-ttu-id="cf6cd-303">Cierre la sesión de destino iSCSI de Hola</span><span class="sxs-lookup"><span data-stu-id="cf6cd-303">Log out from hello iSCSI target</span></span> |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |<span data-ttu-id="cf6cd-304">Imprimir el nombre del iniciador iSCSI</span><span class="sxs-lookup"><span data-stu-id="cf6cd-304">Print iSCSI initiator name</span></span> |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |<span data-ttu-id="cf6cd-305">Comprobar estado de Hola de sesión de iSCSI de Hola y volumen detectados en el host de Hola</span><span class="sxs-lookup"><span data-stu-id="cf6cd-305">Check hello state of hello iSCSI session and volume discovered on hello host</span></span> |
| &nbsp; |`iscsi –m session` |<span data-ttu-id="cf6cd-306">Muestra todas las sesiones de iSCSI de hello establecidas entre el host de Hola y de dispositivo de StorSimple de Hola</span><span class="sxs-lookup"><span data-stu-id="cf6cd-306">Shows all hello iSCSI sessions established between hello host and hello StorSimple device</span></span> |
|  | | |
| <span data-ttu-id="cf6cd-307">**Múltiples rutas**</span><span class="sxs-lookup"><span data-stu-id="cf6cd-307">**Multipathing**</span></span> |`service multipathd start` |<span data-ttu-id="cf6cd-308">Iniciar el daemon de múltiples rutas</span><span class="sxs-lookup"><span data-stu-id="cf6cd-308">Start multipath daemon</span></span> |
| &nbsp; |`service multipathd stop` |<span data-ttu-id="cf6cd-309">Detener el daemon de múltiples rutas</span><span class="sxs-lookup"><span data-stu-id="cf6cd-309">Stop multipath daemon</span></span> |
| &nbsp; |`service multipathd restart` |<span data-ttu-id="cf6cd-310">Reiniciar el daemon de múltiples rutas</span><span class="sxs-lookup"><span data-stu-id="cf6cd-310">Restart multipath daemon</span></span> |
| &nbsp; |`chkconfig multipathd on` </br> <span data-ttu-id="cf6cd-311">OR</span><span class="sxs-lookup"><span data-stu-id="cf6cd-311">OR</span></span> </br> `mpathconf –with_chkconfig y` |<span data-ttu-id="cf6cd-312">Habilitar múltiples rutas daemon toostart al arrancar el sistema</span><span class="sxs-lookup"><span data-stu-id="cf6cd-312">Enable multipath daemon toostart at boot time</span></span> |
| &nbsp; |`multipathd –k` |<span data-ttu-id="cf6cd-313">Inicie la consola interactiva de Hola para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="cf6cd-313">Start hello interactive console for troubleshooting</span></span> |
| &nbsp; |`multipath –l` |<span data-ttu-id="cf6cd-314">Enumerar dispositivos y conexiones de múltiples rutas</span><span class="sxs-lookup"><span data-stu-id="cf6cd-314">List multipath connections and devices</span></span> |
| &nbsp; |`mpathconf --enable` |<span data-ttu-id="cf6cd-315">Crear un archivo de ejemplo mulitpath.conf en `/etc/mulitpath.conf`</span><span class="sxs-lookup"><span data-stu-id="cf6cd-315">Create a sample mulitpath.conf file in `/etc/mulitpath.conf`</span></span> |
|  | | |

## <a name="next-steps"></a><span data-ttu-id="cf6cd-316">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cf6cd-316">Next steps</span></span>
<span data-ttu-id="cf6cd-317">Como va a configurar MPIO en el host de Linux, también deberá toohello toorefer después de CentoS 6.6 documentos:</span><span class="sxs-lookup"><span data-stu-id="cf6cd-317">As you are configuring MPIO on Linux host, you may also need toorefer toohello following CentoS 6.6 documents:</span></span>

* [<span data-ttu-id="cf6cd-318">Configuración de MPIO en CentOS</span><span class="sxs-lookup"><span data-stu-id="cf6cd-318">Setting up MPIO on CentOS</span></span>](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [<span data-ttu-id="cf6cd-319">Guía de aprendizaje de Linux</span><span class="sxs-lookup"><span data-stu-id="cf6cd-319">Linux Training Guide</span></span>](http://linux-training.be/files/books/LinuxAdm.pdf)

