---
title: "el programa de instalación del controlador de aaaAzure N-series para Linux | Documentos de Microsoft"
description: "¿Cómo tooset los controladores de GPU NVIDIA N-series ejecución de máquinas virtuales Linux en Azure"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d91695d0-64b9-4e6b-84bd-18401eaecdde
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7db1b3859f9075c6d9f0319f39418946ea08743f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a><span data-ttu-id="10b13-103">Instalación de controladores de GPU de NVIDIA en máquinas virtuales de la serie N con Linux</span><span class="sxs-lookup"><span data-stu-id="10b13-103">Install NVIDIA GPU drivers on N-series VMs running Linux</span></span>

<span data-ttu-id="10b13-104">tootake aprovechar las capacidades GPU de Hola de Azure N-series máquinas virtuales que ejecutan Linux, instalación de controladores de gráficos NVIDIA admitidos.</span><span class="sxs-lookup"><span data-stu-id="10b13-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Linux, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="10b13-105">Este artículo proporciona pasos de instalación de controlador después de implementar una VM de la serie N.</span><span class="sxs-lookup"><span data-stu-id="10b13-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="10b13-106">También está disponible la información de instalación del controlador para las [máquinas virtuales Windows](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10b13-106">Driver setup information is also available for [Windows VMs](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


<span data-ttu-id="10b13-107">Para conocer las especificaciones de máquina virtual de la serie N, las capacidades de almacenamiento y los detalles del disco, vea [Tamaño de máquinas virtuales para GPU Linux](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10b13-107">For N-series VM specs, storage capacities, and disk details, see [GPU Linux VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a><span data-ttu-id="10b13-108">Instalación de los controladores de GRID para máquinas virtuales NV</span><span class="sxs-lookup"><span data-stu-id="10b13-108">Install GRID drivers for NV VMs</span></span>

<span data-ttu-id="10b13-109">controladores de NVIDIA CUADRÍCULA tooinstall en máquinas virtuales NV, realizar una tooeach de conexión SSH VM y siga los pasos de Hola para su distribución de Linux.</span><span class="sxs-lookup"><span data-stu-id="10b13-109">tooinstall NVIDIA GRID drivers on NV VMs, make an SSH connection tooeach VM and follow hello steps for your Linux distribution.</span></span> 

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="10b13-110">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="10b13-110">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="10b13-111">Ejecute hello `lspci` comando.</span><span class="sxs-lookup"><span data-stu-id="10b13-111">Run hello `lspci` command.</span></span> <span data-ttu-id="10b13-112">Compruebe que la tarjeta de hello NVIDIA M60 o tarjetas son visibles como dispositivos PCI.</span><span class="sxs-lookup"><span data-stu-id="10b13-112">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>

2. <span data-ttu-id="10b13-113">Instale las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="10b13-113">Install updates.</span></span>

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. <span data-ttu-id="10b13-114">Deshabilitar el controlador de kernel de estilo Nouveau hello, que es incompatible con el controlador NVIDIA Hola.</span><span class="sxs-lookup"><span data-stu-id="10b13-114">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="10b13-115">(Solo usa controladores NVIDIA hello en máquinas virtuales de NV.) toodo esto, cree un archivo en `/etc/modprobe.d `denominado `nouveau.conf` con hello siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="10b13-115">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. <span data-ttu-id="10b13-116">Reiniciar Hola VM y vuelva a conectar.</span><span class="sxs-lookup"><span data-stu-id="10b13-116">Reboot hello VM and reconnect.</span></span> <span data-ttu-id="10b13-117">Salga del servidor X:</span><span class="sxs-lookup"><span data-stu-id="10b13-117">Exit X server:</span></span>

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. <span data-ttu-id="10b13-118">Descargue e instale el controlador de la CUADRÍCULA de hello:</span><span class="sxs-lookup"><span data-stu-id="10b13-118">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. <span data-ttu-id="10b13-119">Cuando se le pregunte si desea toorun Hola nvidia-xconfig utilidad tooupdate el archivo de configuración de X, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="10b13-119">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="10b13-120">Una vez finalizada la instalación, copie gridd.conf /etc/nvidia/gridd.conf.template tooa de archivo nuevo en la ubicación/etc/nvidia /</span><span class="sxs-lookup"><span data-stu-id="10b13-120">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. <span data-ttu-id="10b13-121">Agregue la Hola siguiente demasiado`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="10b13-121">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="10b13-122">Reinicie Hola VM y continuar la instalación de hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="10b13-122">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="10b13-123">Con base en CentOS 7.3 o Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="10b13-123">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>


1. <span data-ttu-id="10b13-124">Actualice el kernel de Hola y DKMS.</span><span class="sxs-lookup"><span data-stu-id="10b13-124">Update hello kernel and DKMS.</span></span>
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. <span data-ttu-id="10b13-125">Deshabilitar el controlador de kernel de estilo Nouveau hello, que es incompatible con el controlador NVIDIA Hola.</span><span class="sxs-lookup"><span data-stu-id="10b13-125">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="10b13-126">(Solo usa controladores NVIDIA hello en máquinas virtuales de NV.) toodo esto, cree un archivo en `/etc/modprobe.d `denominado `nouveau.conf` con hello siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="10b13-126">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. <span data-ttu-id="10b13-127">Reinicie Hola VM, volver a conectarse e instale Hola últimos servicios de integración de Linux para Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="10b13-127">Reboot hello VM, reconnect, and install hello latest Linux Integration Services for Hyper-V:</span></span>
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. <span data-ttu-id="10b13-128">Volver a conectar toohello máquina virtual y ejecute hello `lspci` comando.</span><span class="sxs-lookup"><span data-stu-id="10b13-128">Reconnect toohello VM and run hello `lspci` command.</span></span> <span data-ttu-id="10b13-129">Compruebe que la tarjeta de hello NVIDIA M60 o tarjetas son visibles como dispositivos PCI.</span><span class="sxs-lookup"><span data-stu-id="10b13-129">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>
 
5. <span data-ttu-id="10b13-130">Descargue e instale el controlador de la CUADRÍCULA de hello:</span><span class="sxs-lookup"><span data-stu-id="10b13-130">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. <span data-ttu-id="10b13-131">Cuando se le pregunte si desea toorun Hola nvidia-xconfig utilidad tooupdate el archivo de configuración de X, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="10b13-131">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="10b13-132">Una vez finalizada la instalación, copie gridd.conf /etc/nvidia/gridd.conf.template tooa de archivo nuevo en la ubicación/etc/nvidia /</span><span class="sxs-lookup"><span data-stu-id="10b13-132">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. <span data-ttu-id="10b13-133">Agregue la Hola siguiente demasiado`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="10b13-133">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="10b13-134">Reinicie Hola VM y continuar la instalación de hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="10b13-134">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="verify-driver-installation"></a><span data-ttu-id="10b13-135">Comprobación de la instalación del controlador</span><span class="sxs-lookup"><span data-stu-id="10b13-135">Verify driver installation</span></span>


<span data-ttu-id="10b13-136">tooquery Hola estado del dispositivo GPU, SSH toohello VM y ejecución hello [smi nvidia](https://developer.nvidia.com/nvidia-system-management-interface) instalada con controlador Hola de utilidad de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="10b13-136">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="10b13-137">Aparece el siguiente toohello similar de salida:</span><span class="sxs-lookup"><span data-stu-id="10b13-137">Output similar toohello following appears:</span></span>

![Estado del dispositivo de NVIDIA](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a><span data-ttu-id="10b13-139">Servidor X11</span><span class="sxs-lookup"><span data-stu-id="10b13-139">X11 server</span></span>
<span data-ttu-id="10b13-140">Si necesita un X11 servidor para las conexiones remotas tooan NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) es la recomendada porque permite la aceleración de hardware de gráficos.</span><span class="sxs-lookup"><span data-stu-id="10b13-140">If you need an X11 server for remote connections tooan NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) is recommended because it allows hardware acceleration of graphics.</span></span> <span data-ttu-id="10b13-141">Hola BusID del dispositivo de hello M60 debe agregarse manualmente toohello xconfig archivo (`etc/X11/xorg.conf` en Ubuntu 16.04 LTS, `/etc/X11/XF86config` en 7.3 CentOS o Red Hat Enterprise Server 7.3).</span><span class="sxs-lookup"><span data-stu-id="10b13-141">hello BusID of hello M60 device must be manually added toohello xconfig file (`etc/X11/xorg.conf` on Ubuntu 16.04 LTS, `/etc/X11/XF86config` on CentOS 7.3 or Red Hat Enterprise Server 7.3).</span></span> <span data-ttu-id="10b13-142">Agregar un `"Device"` sección similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="10b13-142">Add a `"Device"` section similar toohello following:</span></span>
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
<span data-ttu-id="10b13-143">Además, actualice su `"Screen"` sección toouse este dispositivo.</span><span class="sxs-lookup"><span data-stu-id="10b13-143">Additionally, update your `"Screen"` section toouse this device.</span></span>
 
<span data-ttu-id="10b13-144">Hola BusID puede encontrarse mediante la ejecución</span><span class="sxs-lookup"><span data-stu-id="10b13-144">hello BusID can be found by running</span></span>

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
<span data-ttu-id="10b13-145">Hola BusID puede cambiar cuando obtiene reasigna o se reinicie una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="10b13-145">hello BusID can change when a VM gets reallocated or rebooted.</span></span> <span data-ttu-id="10b13-146">Por lo tanto, puede que desee toouse Hola de tooupdate de secuencia de comandos BusID en la configuración de hello X11 cuando se reinicia una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="10b13-146">Therefore, you may want toouse a script tooupdate hello BusID in hello X11 configuration when a VM is rebooted.</span></span> <span data-ttu-id="10b13-147">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="10b13-147">For example:</span></span>

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed too${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

<span data-ttu-id="10b13-148">Este archivo se puede invocar como raíz en el arranque mediante la creación de una entrada para él en `/etc/rc.d/rc3.d`.</span><span class="sxs-lookup"><span data-stu-id="10b13-148">This file can be invoked as root on boot by creating an entry for it in `/etc/rc.d/rc3.d`.</span></span>


## <a name="install-cuda-drivers-for-nc-vms"></a><span data-ttu-id="10b13-149">Instalación de controladores CUDA para VM de NC</span><span class="sxs-lookup"><span data-stu-id="10b13-149">Install CUDA drivers for NC VMs</span></span>

<span data-ttu-id="10b13-150">Aquí son controladores NVIDIA tooinstall de pasos en las máquinas virtuales de Linux NC de hello NVIDIA CUDA Kit de herramientas 8.0.</span><span class="sxs-lookup"><span data-stu-id="10b13-150">Here are steps tooinstall NVIDIA drivers on Linux NC VMs from hello NVIDIA CUDA Toolkit 8.0.</span></span> 

<span data-ttu-id="10b13-151">Los desarrolladores de C y C++ pueden opcionalmente instalar Hola Kit de herramientas toobuild y acelerados por GPU aplicaciones completas.</span><span class="sxs-lookup"><span data-stu-id="10b13-151">C and C++ developers can optionally install hello full Toolkit toobuild GPU-accelerated applications.</span></span> <span data-ttu-id="10b13-152">Para obtener más información, vea hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span><span class="sxs-lookup"><span data-stu-id="10b13-152">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span></span>


> [!NOTE]
> <span data-ttu-id="10b13-153">Los vínculos de descarga de controladores de CUDA que se proporcionan aquí están actualizados en el momento de la publicación.</span><span class="sxs-lookup"><span data-stu-id="10b13-153">CUDA driver download links provided here are current at time of publication.</span></span> <span data-ttu-id="10b13-154">Para controladores CUDA hello más recientes, visite hello [NVIDIA](http://www.nvidia.com/) sitio Web.</span><span class="sxs-lookup"><span data-stu-id="10b13-154">For hello latest CUDA drivers, visit hello [NVIDIA](http://www.nvidia.com/) website.</span></span>
>

<span data-ttu-id="10b13-155">tooinstall CUDA Kit de herramientas, asegúrese de un tooeach de conexión SSH máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="10b13-155">tooinstall CUDA Toolkit, make an SSH connection tooeach VM.</span></span> <span data-ttu-id="10b13-156">tooverify que Hola sistema tiene una GPU compatible con CUDA, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="10b13-156">tooverify that hello system has a CUDA-capable GPU, run hello following command:</span></span>

```bash
lspci | grep -i NVIDIA
```
<span data-ttu-id="10b13-157">Verá toohello similar de salida (mostrando una tarjeta NVIDIA Tesla K80) del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="10b13-157">You will see output similar toohello following example (showing an NVIDIA Tesla K80 card):</span></span>

![Resultado del comando de Ispci](./media/n-series-driver-setup/lspci.png)

<span data-ttu-id="10b13-159">Luego, ejecute los comandos de instalación específicos de su distribución.</span><span class="sxs-lookup"><span data-stu-id="10b13-159">Then run installation commands specific for your distribution.</span></span>

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="10b13-160">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="10b13-160">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="10b13-161">Descargue e instale a los controladores CUDA Hola.</span><span class="sxs-lookup"><span data-stu-id="10b13-161">Download and install hello CUDA drivers.</span></span>
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  <span data-ttu-id="10b13-162">instalación de Hello puede tardar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="10b13-162">hello installation can take several minutes.</span></span>

2. <span data-ttu-id="10b13-163">toooptionally instalación hello CUDA Kit de herramientas completo, tipo:</span><span class="sxs-lookup"><span data-stu-id="10b13-163">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo apt-get install cuda
  ```

3. <span data-ttu-id="10b13-164">Reinicie Hola VM y continuar la instalación de hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="10b13-164">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="10b13-165">Con base en CentOS 7.3 o Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="10b13-165">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

1. <span data-ttu-id="10b13-166">Obtenga las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="10b13-166">Get updates.</span></span> 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. <span data-ttu-id="10b13-167">Vuelva a conectarla toohello máquina virtual e instalar Hola últimos servicios de integración de Linux para Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="10b13-167">Reconnect toohello VM and install hello latest Linux Integration Services for Hyper-V.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="10b13-168">Si instaló una imagen basada en CentOS HPC en una máquina virtual NC24r, omitir tooStep 3.</span><span class="sxs-lookup"><span data-stu-id="10b13-168">If you installed a CentOS-based HPC image on an NC24r VM, skip tooStep 3.</span></span> <span data-ttu-id="10b13-169">Dado que previamente se instalan controladores de RDMA de Azure y servicios de integración de Linux en imagen de Hola, LIS no deben actualizarse y actualizaciones del núcleo están deshabilitadas de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="10b13-169">Because Azure RDMA drivers and Linux Integration Services are pre-installed in hello image, LIS should not be upgraded, and kernel updates are disabled by default.</span></span>
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. <span data-ttu-id="10b13-170">Volver a conectar toohello VM y continuar con la instalación con hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="10b13-170">Reconnect toohello VM and continue installation with hello following commands:</span></span>

  ```bash
  sudo yum install kernel-devel

  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

  sudo yum install dkms

  CUDA_REPO_PKG=cuda-repo-rhel7-8.0.61-1.x86_64.rpm

  wget http://developer.download.nvidia.com/compute/cuda/repos/rhel7/x86_64/${CUDA_REPO_PKG} -O /tmp/${CUDA_REPO_PKG}

  sudo rpm -ivh /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo yum install cuda-drivers
  ```

  <span data-ttu-id="10b13-171">instalación de Hello puede tardar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="10b13-171">hello installation can take several minutes.</span></span> 

4. <span data-ttu-id="10b13-172">toooptionally instalación hello CUDA Kit de herramientas completo, tipo:</span><span class="sxs-lookup"><span data-stu-id="10b13-172">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo yum install cuda
  ```

5. <span data-ttu-id="10b13-173">Reinicie Hola VM y continuar la instalación de hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="10b13-173">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="verify-driver-installation"></a><span data-ttu-id="10b13-174">Comprobación de la instalación del controlador</span><span class="sxs-lookup"><span data-stu-id="10b13-174">Verify driver installation</span></span>


<span data-ttu-id="10b13-175">tooquery Hola estado del dispositivo GPU, SSH toohello VM y ejecución hello [smi nvidia](https://developer.nvidia.com/nvidia-system-management-interface) instalada con controlador Hola de utilidad de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="10b13-175">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="10b13-176">Aparece el siguiente toohello similar de salida:</span><span class="sxs-lookup"><span data-stu-id="10b13-176">Output similar toohello following appears:</span></span>

![Estado del dispositivo de NVIDIA](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a><span data-ttu-id="10b13-178">Actualizaciones de controladores CUDA</span><span class="sxs-lookup"><span data-stu-id="10b13-178">CUDA driver updates</span></span>

<span data-ttu-id="10b13-179">Se recomienda actualizar periódicamente los controladores CUDA después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="10b13-179">We recommend that you periodically update CUDA drivers after deployment.</span></span>

#### <a name="ubuntu-1604-lts"></a><span data-ttu-id="10b13-180">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="10b13-180">Ubuntu 16.04 LTS</span></span>

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="10b13-181">Con base en CentOS 7.3 o Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="10b13-181">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a><span data-ttu-id="10b13-182">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="10b13-182">Troubleshooting</span></span>

* <span data-ttu-id="10b13-183">Hay un problema conocido con los controladores CUDA en máquinas virtuales de Azure N-series con kernel de Linux de hello 4.4.0-75 Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="10b13-183">There is a known issue with CUDA drivers on Azure N-series VMs running hello 4.4.0-75 Linux kernel on Ubuntu 16.04 LTS.</span></span> <span data-ttu-id="10b13-184">Si va a actualizar desde una versión anterior de kernel, actualizar tooat 4.4.0-77 mínimos de versión de kernel.</span><span class="sxs-lookup"><span data-stu-id="10b13-184">If you are upgrading from an earlier kernel version, upgrade tooat least kernel version 4.4.0-77.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="10b13-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="10b13-185">Next steps</span></span>

* <span data-ttu-id="10b13-186">Para obtener más información sobre Hola GPU NVIDIA Hola N-series las máquinas virtuales, vea:</span><span class="sxs-lookup"><span data-stu-id="10b13-186">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="10b13-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (para máquinas virtuales de Azure NC)</span><span class="sxs-lookup"><span data-stu-id="10b13-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="10b13-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (para máquinas virtuales de Azure NV)</span><span class="sxs-lookup"><span data-stu-id="10b13-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="10b13-189">toocapture una imagen de VM de Linux con los controladores NVIDIA instalados, consulte [cómo toogeneralize y capturar una máquina virtual Linux](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10b13-189">toocapture a Linux VM image with your installed NVIDIA drivers, see [How toogeneralize and capture a Linux virtual machine](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
