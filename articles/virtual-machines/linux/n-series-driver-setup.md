---
title: "Instalación del controlador de la serie N de Azure para Linux | Microsoft Docs"
description: "Instalación de controladores de GPU de NVIDIA para máquinas virtuales de la serie N que se ejecutan en Linux en Azure"
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
ms.openlocfilehash: bdeb4d5ca1d9ff4d7dfd0961690412dd7530572a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a><span data-ttu-id="f110f-103">Instalación de controladores de GPU de NVIDIA en máquinas virtuales de la serie N con Linux</span><span class="sxs-lookup"><span data-stu-id="f110f-103">Install NVIDIA GPU drivers on N-series VMs running Linux</span></span>

<span data-ttu-id="f110f-104">Para aprovechar las funcionalidades de GPU de las máquinas virtuales de la serie N de Azure que ejecutan Linux, instale controladores de gráficos de NVIDIA compatibles.</span><span class="sxs-lookup"><span data-stu-id="f110f-104">To take advantage of the GPU capabilities of Azure N-series VMs running Linux, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="f110f-105">Este artículo proporciona pasos de instalación de controlador después de implementar una VM de la serie N.</span><span class="sxs-lookup"><span data-stu-id="f110f-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="f110f-106">También está disponible la información de instalación del controlador para las [máquinas virtuales Windows](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f110f-106">Driver setup information is also available for [Windows VMs](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


<span data-ttu-id="f110f-107">Para conocer las especificaciones de máquina virtual de la serie N, las capacidades de almacenamiento y los detalles del disco, vea [Tamaño de máquinas virtuales para GPU Linux](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f110f-107">For N-series VM specs, storage capacities, and disk details, see [GPU Linux VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a><span data-ttu-id="f110f-108">Instalación de los controladores de GRID para máquinas virtuales NV</span><span class="sxs-lookup"><span data-stu-id="f110f-108">Install GRID drivers for NV VMs</span></span>

<span data-ttu-id="f110f-109">Para instalar los controladores de NVIDIA GRID en máquinas virtuales NV, realice una conexión SSH a cada máquina virtual y siga los pasos para su distribución de Linux.</span><span class="sxs-lookup"><span data-stu-id="f110f-109">To install NVIDIA GRID drivers on NV VMs, make an SSH connection to each VM and follow the steps for your Linux distribution.</span></span> 

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="f110f-110">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="f110f-110">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="f110f-111">Ejecute el comando `lspci`.</span><span class="sxs-lookup"><span data-stu-id="f110f-111">Run the `lspci` command.</span></span> <span data-ttu-id="f110f-112">Compruebe que la tarjeta o tarjetas NVIDIA M60 son visibles como dispositivos PCI.</span><span class="sxs-lookup"><span data-stu-id="f110f-112">Verify that the NVIDIA M60 card or cards are visible as PCI devices.</span></span>

2. <span data-ttu-id="f110f-113">Instale las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="f110f-113">Install updates.</span></span>

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. <span data-ttu-id="f110f-114">Deshabilite el controlador de kernel Nouveau que es incompatible con el controlador NVIDIA.</span><span class="sxs-lookup"><span data-stu-id="f110f-114">Disable the Nouveau kernel driver, which is incompatible with the NVIDIA driver.</span></span> <span data-ttu-id="f110f-115">(Utilice solo el controlador NVIDIA en máquinas virtuales NV). Para ello cree un archivo en `/etc/modprobe.d `llamado `nouveau.conf` con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="f110f-115">(Only use the NVIDIA driver on NV VMs.) To do this, create a file in `/etc/modprobe.d `named `nouveau.conf` with the following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. <span data-ttu-id="f110f-116">Reinicie la máquina virtual y vuelva a conectar.</span><span class="sxs-lookup"><span data-stu-id="f110f-116">Reboot the VM and reconnect.</span></span> <span data-ttu-id="f110f-117">Salga del servidor X:</span><span class="sxs-lookup"><span data-stu-id="f110f-117">Exit X server:</span></span>

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. <span data-ttu-id="f110f-118">Descargue e instale el controlador de GRID:</span><span class="sxs-lookup"><span data-stu-id="f110f-118">Download and install the GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. <span data-ttu-id="f110f-119">Cuando se le pregunte si desea ejecutar la utilidad nvidia-xconfig para actualizar el archivo de configuración de X, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="f110f-119">When you're asked whether you want to run the nvidia-xconfig utility to update your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="f110f-120">Una vez completada la instalación, copie /etc/nvidia/gridd.conf.template en un nuevo archivo gridd.conf en la ubicación /etc/nvidia/</span><span class="sxs-lookup"><span data-stu-id="f110f-120">After installation completes, copy /etc/nvidia/gridd.conf.template to a new file gridd.conf at location /etc/nvidia/</span></span>

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. <span data-ttu-id="f110f-121">Agregue lo siguiente a `/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="f110f-121">Add the following to `/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="f110f-122">Reinicie la máquina virtual y continúe para comprobar la instalación.</span><span class="sxs-lookup"><span data-stu-id="f110f-122">Reboot the VM and proceed to verify the installation.</span></span>


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="f110f-123">Con base en CentOS 7.3 o Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="f110f-123">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>


1. <span data-ttu-id="f110f-124">Actualice el kernel y DKMS.</span><span class="sxs-lookup"><span data-stu-id="f110f-124">Update the kernel and DKMS.</span></span>
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. <span data-ttu-id="f110f-125">Deshabilite el controlador de kernel Nouveau que es incompatible con el controlador NVIDIA.</span><span class="sxs-lookup"><span data-stu-id="f110f-125">Disable the Nouveau kernel driver, which is incompatible with the NVIDIA driver.</span></span> <span data-ttu-id="f110f-126">(Utilice solo el controlador NVIDIA en máquinas virtuales NV). Para ello cree un archivo en `/etc/modprobe.d `llamado `nouveau.conf` con el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="f110f-126">(Only use the NVIDIA driver on NV VMs.) To do this, create a file in `/etc/modprobe.d `named `nouveau.conf` with the following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. <span data-ttu-id="f110f-127">Reinicie la máquina virtual, vuelva a conectarse e instale la versión más reciente de Linux Integration Services para Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="f110f-127">Reboot the VM, reconnect, and install the latest Linux Integration Services for Hyper-V:</span></span>
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. <span data-ttu-id="f110f-128">Vuelva a conectarse a la máquina virtual y ejecute el comando `lspci`.</span><span class="sxs-lookup"><span data-stu-id="f110f-128">Reconnect to the VM and run the `lspci` command.</span></span> <span data-ttu-id="f110f-129">Compruebe que la tarjeta o tarjetas NVIDIA M60 son visibles como dispositivos PCI.</span><span class="sxs-lookup"><span data-stu-id="f110f-129">Verify that the NVIDIA M60 card or cards are visible as PCI devices.</span></span>
 
5. <span data-ttu-id="f110f-130">Descargue e instale el controlador de GRID:</span><span class="sxs-lookup"><span data-stu-id="f110f-130">Download and install the GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. <span data-ttu-id="f110f-131">Cuando se le pregunte si desea ejecutar la utilidad nvidia-xconfig para actualizar el archivo de configuración de X, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="f110f-131">When you're asked whether you want to run the nvidia-xconfig utility to update your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="f110f-132">Una vez completada la instalación, copie /etc/nvidia/gridd.conf.template en un nuevo archivo gridd.conf en la ubicación /etc/nvidia/</span><span class="sxs-lookup"><span data-stu-id="f110f-132">After installation completes, copy /etc/nvidia/gridd.conf.template to a new file gridd.conf at location /etc/nvidia/</span></span>
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. <span data-ttu-id="f110f-133">Agregue lo siguiente a `/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="f110f-133">Add the following to `/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="f110f-134">Reinicie la máquina virtual y continúe para comprobar la instalación.</span><span class="sxs-lookup"><span data-stu-id="f110f-134">Reboot the VM and proceed to verify the installation.</span></span>

### <a name="verify-driver-installation"></a><span data-ttu-id="f110f-135">Comprobación de la instalación del controlador</span><span class="sxs-lookup"><span data-stu-id="f110f-135">Verify driver installation</span></span>


<span data-ttu-id="f110f-136">Para consultar el estado del dispositivo de GPU, acceda mediante SSH a la máquina virtual y ejecute la utilidad de línea de comandos [smi nvidia](https://developer.nvidia.com/nvidia-system-management-interface) que se instala con el controlador.</span><span class="sxs-lookup"><span data-stu-id="f110f-136">To query the GPU device state, SSH to the VM and run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span> 

<span data-ttu-id="f110f-137">Verá un resultado similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="f110f-137">Output similar to the following appears:</span></span>

![Estado del dispositivo de NVIDIA](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a><span data-ttu-id="f110f-139">Servidor X11</span><span class="sxs-lookup"><span data-stu-id="f110f-139">X11 server</span></span>
<span data-ttu-id="f110f-140">Si necesita un servidor X11 para conexiones remotas a la máquina virtual NV, [x11vnc](http://www.karlrunge.com/x11vnc/) es el recomendado porque permite la aceleración de hardware de gráficos.</span><span class="sxs-lookup"><span data-stu-id="f110f-140">If you need an X11 server for remote connections to an NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) is recommended because it allows hardware acceleration of graphics.</span></span> <span data-ttu-id="f110f-141">El BusID del dispositivo M60 tiene que agregarse manualmente al archivo xconfig (`etc/X11/xorg.conf` en Ubuntu 16.04 LTS, `/etc/X11/XF86config` en 7.3 CentOS o Red Hat Enterprise Server 7.3).</span><span class="sxs-lookup"><span data-stu-id="f110f-141">The BusID of the M60 device must be manually added to the xconfig file (`etc/X11/xorg.conf` on Ubuntu 16.04 LTS, `/etc/X11/XF86config` on CentOS 7.3 or Red Hat Enterprise Server 7.3).</span></span> <span data-ttu-id="f110f-142">Agregue una sección `"Device"` similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="f110f-142">Add a `"Device"` section similar to the following:</span></span>
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
<span data-ttu-id="f110f-143">Además, actualice su sección `"Screen"` para usar este dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f110f-143">Additionally, update your `"Screen"` section to use this device.</span></span>
 
<span data-ttu-id="f110f-144">Encontrará el BusID ejecutando</span><span class="sxs-lookup"><span data-stu-id="f110f-144">The BusID can be found by running</span></span>

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
<span data-ttu-id="f110f-145">El BusID puede cambiar cuando se reasigna o reinicia una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f110f-145">The BusID can change when a VM gets reallocated or rebooted.</span></span> <span data-ttu-id="f110f-146">Por lo tanto, puede ser conveniente utilizar un script para actualizar el BusID en la configuración de X11 cuando se reinicie una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f110f-146">Therefore, you may want to use a script to update the BusID in the X11 configuration when a VM is rebooted.</span></span> <span data-ttu-id="f110f-147">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f110f-147">For example:</span></span>

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed to ${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

<span data-ttu-id="f110f-148">Este archivo se puede invocar como raíz en el arranque mediante la creación de una entrada para él en `/etc/rc.d/rc3.d`.</span><span class="sxs-lookup"><span data-stu-id="f110f-148">This file can be invoked as root on boot by creating an entry for it in `/etc/rc.d/rc3.d`.</span></span>


## <a name="install-cuda-drivers-for-nc-vms"></a><span data-ttu-id="f110f-149">Instalación de controladores CUDA para VM de NC</span><span class="sxs-lookup"><span data-stu-id="f110f-149">Install CUDA drivers for NC VMs</span></span>

<span data-ttu-id="f110f-150">Estos son los pasos para instalar controladores NVIDIA en máquinas virtuales Linux NC desde la versión 8.0 del kit de herramientas de NVIDIA CUDA.</span><span class="sxs-lookup"><span data-stu-id="f110f-150">Here are steps to install NVIDIA drivers on Linux NC VMs from the NVIDIA CUDA Toolkit 8.0.</span></span> 

<span data-ttu-id="f110f-151">Los desarrolladores de C y C++, si lo desean, pueden instalar el kit de herramientas completo para crear aplicaciones aceleradas por GPU.</span><span class="sxs-lookup"><span data-stu-id="f110f-151">C and C++ developers can optionally install the full Toolkit to build GPU-accelerated applications.</span></span> <span data-ttu-id="f110f-152">Para obtener más información, consulte la [guía de instalación de CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span><span class="sxs-lookup"><span data-stu-id="f110f-152">For more information, see the [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span></span>


> [!NOTE]
> <span data-ttu-id="f110f-153">Los vínculos de descarga de controladores de CUDA que se proporcionan aquí están actualizados en el momento de la publicación.</span><span class="sxs-lookup"><span data-stu-id="f110f-153">CUDA driver download links provided here are current at time of publication.</span></span> <span data-ttu-id="f110f-154">Para ver los controladores de CUDA más recientes, visite el sitio web de [NVIDIA](http://www.nvidia.com/).</span><span class="sxs-lookup"><span data-stu-id="f110f-154">For the latest CUDA drivers, visit the [NVIDIA](http://www.nvidia.com/) website.</span></span>
>

<span data-ttu-id="f110f-155">Para instalar el kit de herramientas de CUDA, realice una conexión SSH a cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f110f-155">To install CUDA Toolkit, make an SSH connection to each VM.</span></span> <span data-ttu-id="f110f-156">Para comprobar que el sistema dispone de una GPU compatible con CUDA, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f110f-156">To verify that the system has a CUDA-capable GPU, run the following command:</span></span>

```bash
lspci | grep -i NVIDIA
```
<span data-ttu-id="f110f-157">Verá un resultado similar al siguiente ejemplo (mostrando una tarjeta NVIDIA Tesla K80):</span><span class="sxs-lookup"><span data-stu-id="f110f-157">You will see output similar to the following example (showing an NVIDIA Tesla K80 card):</span></span>

![Resultado del comando de Ispci](./media/n-series-driver-setup/lspci.png)

<span data-ttu-id="f110f-159">Luego, ejecute los comandos de instalación específicos de su distribución.</span><span class="sxs-lookup"><span data-stu-id="f110f-159">Then run installation commands specific for your distribution.</span></span>

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="f110f-160">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="f110f-160">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="f110f-161">Descargue e instale los controladores de CUDA.</span><span class="sxs-lookup"><span data-stu-id="f110f-161">Download and install the CUDA drivers.</span></span>
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  <span data-ttu-id="f110f-162">La instalación puede tardar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="f110f-162">The installation can take several minutes.</span></span>

2. <span data-ttu-id="f110f-163">Para instalar (opcional) el kit de herramientas CUDA completo, escriba:</span><span class="sxs-lookup"><span data-stu-id="f110f-163">To optionally install the complete CUDA toolkit, type:</span></span>

  ```bash
  sudo apt-get install cuda
  ```

3. <span data-ttu-id="f110f-164">Reinicie la máquina virtual y continúe para comprobar la instalación.</span><span class="sxs-lookup"><span data-stu-id="f110f-164">Reboot the VM and proceed to verify the installation.</span></span>

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="f110f-165">Con base en CentOS 7.3 o Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="f110f-165">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

1. <span data-ttu-id="f110f-166">Obtenga las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="f110f-166">Get updates.</span></span> 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. <span data-ttu-id="f110f-167">Vuelva a conectarse a la máquina virtual e instale la versión más reciente de Linux Integration Services para Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="f110f-167">Reconnect to the VM and install the latest Linux Integration Services for Hyper-V.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="f110f-168">Si instaló una imagen HPC basada en CentOS en una máquina virtual NC24r, vaya al paso 3.</span><span class="sxs-lookup"><span data-stu-id="f110f-168">If you installed a CentOS-based HPC image on an NC24r VM, skip to Step 3.</span></span> <span data-ttu-id="f110f-169">Dado que los controladores RDMA de Azure y Linux Integration Services ya están instalados en la imagen, LIS no debe actualizarse y la actualizaciones del kernel están deshabilitadas de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f110f-169">Because Azure RDMA drivers and Linux Integration Services are pre-installed in the image, LIS should not be upgraded, and kernel updates are disabled by default.</span></span>
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. <span data-ttu-id="f110f-170">Vuelva a conectarse a la VM y continúe con la instalación con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="f110f-170">Reconnect to the VM and continue installation with the following commands:</span></span>

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

  <span data-ttu-id="f110f-171">La instalación puede tardar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="f110f-171">The installation can take several minutes.</span></span> 

4. <span data-ttu-id="f110f-172">Para instalar (opcional) el kit de herramientas CUDA completo, escriba:</span><span class="sxs-lookup"><span data-stu-id="f110f-172">To optionally install the complete CUDA toolkit, type:</span></span>

  ```bash
  sudo yum install cuda
  ```

5. <span data-ttu-id="f110f-173">Reinicie la máquina virtual y continúe para comprobar la instalación.</span><span class="sxs-lookup"><span data-stu-id="f110f-173">Reboot the VM and proceed to verify the installation.</span></span>


### <a name="verify-driver-installation"></a><span data-ttu-id="f110f-174">Comprobación de la instalación del controlador</span><span class="sxs-lookup"><span data-stu-id="f110f-174">Verify driver installation</span></span>


<span data-ttu-id="f110f-175">Para consultar el estado del dispositivo de GPU, acceda mediante SSH a la máquina virtual y ejecute la utilidad de línea de comandos [smi nvidia](https://developer.nvidia.com/nvidia-system-management-interface) que se instala con el controlador.</span><span class="sxs-lookup"><span data-stu-id="f110f-175">To query the GPU device state, SSH to the VM and run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span> 

<span data-ttu-id="f110f-176">Verá un resultado similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="f110f-176">Output similar to the following appears:</span></span>

![Estado del dispositivo de NVIDIA](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a><span data-ttu-id="f110f-178">Actualizaciones de controladores CUDA</span><span class="sxs-lookup"><span data-stu-id="f110f-178">CUDA driver updates</span></span>

<span data-ttu-id="f110f-179">Se recomienda actualizar periódicamente los controladores CUDA después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="f110f-179">We recommend that you periodically update CUDA drivers after deployment.</span></span>

#### <a name="ubuntu-1604-lts"></a><span data-ttu-id="f110f-180">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="f110f-180">Ubuntu 16.04 LTS</span></span>

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="f110f-181">Con base en CentOS 7.3 o Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="f110f-181">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a><span data-ttu-id="f110f-182">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="f110f-182">Troubleshooting</span></span>

* <span data-ttu-id="f110f-183">Hay un problema conocido con los controladores CUDA en las máquinas virtuales serie N de Azure que ejecutan el kernel de Linux 4.4.0-75 en Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="f110f-183">There is a known issue with CUDA drivers on Azure N-series VMs running the 4.4.0-75 Linux kernel on Ubuntu 16.04 LTS.</span></span> <span data-ttu-id="f110f-184">Si va a actualizar desde una versión anterior del kernel, actualice al menos a la versión 4.4.0-77.</span><span class="sxs-lookup"><span data-stu-id="f110f-184">If you are upgrading from an earlier kernel version, upgrade to at least kernel version 4.4.0-77.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="f110f-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f110f-185">Next steps</span></span>

* <span data-ttu-id="f110f-186">Para obtener más información sobre las GPU de NVIDIA en las máquinas virtuales de la serie N, consulte:</span><span class="sxs-lookup"><span data-stu-id="f110f-186">For more information about the NVIDIA GPUs on the N-series VMs, see:</span></span>
    * <span data-ttu-id="f110f-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (para máquinas virtuales de Azure NC)</span><span class="sxs-lookup"><span data-stu-id="f110f-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="f110f-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (para máquinas virtuales de Azure NV)</span><span class="sxs-lookup"><span data-stu-id="f110f-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="f110f-189">Para capturar una imagen de una VM Linux con los controladores de NVIDIA instalados, vea [Procedimiento para generalizar y capturar una máquina virtual Linux](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f110f-189">To capture a Linux VM image with your installed NVIDIA drivers, see [How to generalize and capture a Linux virtual machine](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
