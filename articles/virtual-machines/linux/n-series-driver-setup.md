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
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a>Instalación de controladores de GPU de NVIDIA en máquinas virtuales de la serie N con Linux

tootake aprovechar las capacidades GPU de Hola de Azure N-series máquinas virtuales que ejecutan Linux, instalación de controladores de gráficos NVIDIA admitidos. Este artículo proporciona pasos de instalación de controlador después de implementar una VM de la serie N. También está disponible la información de instalación del controlador para las [máquinas virtuales Windows](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


Para conocer las especificaciones de máquina virtual de la serie N, las capacidades de almacenamiento y los detalles del disco, vea [Tamaño de máquinas virtuales para GPU Linux](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a>Instalación de los controladores de GRID para máquinas virtuales NV

controladores de NVIDIA CUADRÍCULA tooinstall en máquinas virtuales NV, realizar una tooeach de conexión SSH VM y siga los pasos de Hola para su distribución de Linux. 

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

1. Ejecute hello `lspci` comando. Compruebe que la tarjeta de hello NVIDIA M60 o tarjetas son visibles como dispositivos PCI.

2. Instale las actualizaciones.

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. Deshabilitar el controlador de kernel de estilo Nouveau hello, que es incompatible con el controlador NVIDIA Hola. (Solo usa controladores NVIDIA hello en máquinas virtuales de NV.) toodo esto, cree un archivo en `/etc/modprobe.d `denominado `nouveau.conf` con hello siguiente contenido:

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. Reiniciar Hola VM y vuelva a conectar. Salga del servidor X:

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. Descargue e instale el controlador de la CUADRÍCULA de hello:

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. Cuando se le pregunte si desea toorun Hola nvidia-xconfig utilidad tooupdate el archivo de configuración de X, seleccione **Sí**.

7. Una vez finalizada la instalación, copie gridd.conf /etc/nvidia/gridd.conf.template tooa de archivo nuevo en la ubicación/etc/nvidia /

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. Agregue la Hola siguiente demasiado`/etc/nvidia/gridd.conf`:
 
  ```
  IgnoreSP=TRUE
  ```
9. Reinicie Hola VM y continuar la instalación de hello tooverify.


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>Con base en CentOS 7.3 o Red Hat Enterprise Linux 7.3


1. Actualice el kernel de Hola y DKMS.
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. Deshabilitar el controlador de kernel de estilo Nouveau hello, que es incompatible con el controlador NVIDIA Hola. (Solo usa controladores NVIDIA hello en máquinas virtuales de NV.) toodo esto, cree un archivo en `/etc/modprobe.d `denominado `nouveau.conf` con hello siguiente contenido:

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. Reinicie Hola VM, volver a conectarse e instale Hola últimos servicios de integración de Linux para Hyper-V:
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. Volver a conectar toohello máquina virtual y ejecute hello `lspci` comando. Compruebe que la tarjeta de hello NVIDIA M60 o tarjetas son visibles como dispositivos PCI.
 
5. Descargue e instale el controlador de la CUADRÍCULA de hello:

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. Cuando se le pregunte si desea toorun Hola nvidia-xconfig utilidad tooupdate el archivo de configuración de X, seleccione **Sí**.

7. Una vez finalizada la instalación, copie gridd.conf /etc/nvidia/gridd.conf.template tooa de archivo nuevo en la ubicación/etc/nvidia /
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. Agregue la Hola siguiente demasiado`/etc/nvidia/gridd.conf`:
 
  ```
  IgnoreSP=TRUE
  ```
9. Reinicie Hola VM y continuar la instalación de hello tooverify.

### <a name="verify-driver-installation"></a>Comprobación de la instalación del controlador


tooquery Hola estado del dispositivo GPU, SSH toohello VM y ejecución hello [smi nvidia](https://developer.nvidia.com/nvidia-system-management-interface) instalada con controlador Hola de utilidad de línea de comandos. 

Aparece el siguiente toohello similar de salida:

![Estado del dispositivo de NVIDIA](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a>Servidor X11
Si necesita un X11 servidor para las conexiones remotas tooan NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) es la recomendada porque permite la aceleración de hardware de gráficos. Hola BusID del dispositivo de hello M60 debe agregarse manualmente toohello xconfig archivo (`etc/X11/xorg.conf` en Ubuntu 16.04 LTS, `/etc/X11/XF86config` en 7.3 CentOS o Red Hat Enterprise Server 7.3). Agregar un `"Device"` sección similar siguiente toohello:
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
Además, actualice su `"Screen"` sección toouse este dispositivo.
 
Hola BusID puede encontrarse mediante la ejecución

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
Hola BusID puede cambiar cuando obtiene reasigna o se reinicie una máquina virtual. Por lo tanto, puede que desee toouse Hola de tooupdate de secuencia de comandos BusID en la configuración de hello X11 cuando se reinicia una máquina virtual. Por ejemplo:

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed too${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

Este archivo se puede invocar como raíz en el arranque mediante la creación de una entrada para él en `/etc/rc.d/rc3.d`.


## <a name="install-cuda-drivers-for-nc-vms"></a>Instalación de controladores CUDA para VM de NC

Aquí son controladores NVIDIA tooinstall de pasos en las máquinas virtuales de Linux NC de hello NVIDIA CUDA Kit de herramientas 8.0. 

Los desarrolladores de C y C++ pueden opcionalmente instalar Hola Kit de herramientas toobuild y acelerados por GPU aplicaciones completas. Para obtener más información, vea hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).


> [!NOTE]
> Los vínculos de descarga de controladores de CUDA que se proporcionan aquí están actualizados en el momento de la publicación. Para controladores CUDA hello más recientes, visite hello [NVIDIA](http://www.nvidia.com/) sitio Web.
>

tooinstall CUDA Kit de herramientas, asegúrese de un tooeach de conexión SSH máquina virtual. tooverify que Hola sistema tiene una GPU compatible con CUDA, ejecute el siguiente comando de hello:

```bash
lspci | grep -i NVIDIA
```
Verá toohello similar de salida (mostrando una tarjeta NVIDIA Tesla K80) del ejemplo siguiente:

![Resultado del comando de Ispci](./media/n-series-driver-setup/lspci.png)

Luego, ejecute los comandos de instalación específicos de su distribución.

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

1. Descargue e instale a los controladores CUDA Hola.
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  instalación de Hello puede tardar varios minutos.

2. toooptionally instalación hello CUDA Kit de herramientas completo, tipo:

  ```bash
  sudo apt-get install cuda
  ```

3. Reinicie Hola VM y continuar la instalación de hello tooverify.

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>Con base en CentOS 7.3 o Red Hat Enterprise Linux 7.3

1. Obtenga las actualizaciones. 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. Vuelva a conectarla toohello máquina virtual e instalar Hola últimos servicios de integración de Linux para Hyper-V.

  > [!IMPORTANT]
  > Si instaló una imagen basada en CentOS HPC en una máquina virtual NC24r, omitir tooStep 3. Dado que previamente se instalan controladores de RDMA de Azure y servicios de integración de Linux en imagen de Hola, LIS no deben actualizarse y actualizaciones del núcleo están deshabilitadas de forma predeterminada.
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. Volver a conectar toohello VM y continuar con la instalación con hello siguientes comandos:

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

  instalación de Hello puede tardar varios minutos. 

4. toooptionally instalación hello CUDA Kit de herramientas completo, tipo:

  ```bash
  sudo yum install cuda
  ```

5. Reinicie Hola VM y continuar la instalación de hello tooverify.


### <a name="verify-driver-installation"></a>Comprobación de la instalación del controlador


tooquery Hola estado del dispositivo GPU, SSH toohello VM y ejecución hello [smi nvidia](https://developer.nvidia.com/nvidia-system-management-interface) instalada con controlador Hola de utilidad de línea de comandos. 

Aparece el siguiente toohello similar de salida:

![Estado del dispositivo de NVIDIA](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a>Actualizaciones de controladores CUDA

Se recomienda actualizar periódicamente los controladores CUDA después de la implementación.

#### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>Con base en CentOS 7.3 o Red Hat Enterprise Linux 7.3

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a>Solución de problemas

* Hay un problema conocido con los controladores CUDA en máquinas virtuales de Azure N-series con kernel de Linux de hello 4.4.0-75 Ubuntu 16.04 LTS. Si va a actualizar desde una versión anterior de kernel, actualizar tooat 4.4.0-77 mínimos de versión de kernel. 



## <a name="next-steps"></a>Pasos siguientes

* Para obtener más información sobre Hola GPU NVIDIA Hola N-series las máquinas virtuales, vea:
    * [NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (para máquinas virtuales de Azure NC)
    * [NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (para máquinas virtuales de Azure NV)

* toocapture una imagen de VM de Linux con los controladores NVIDIA instalados, consulte [cómo toogeneralize y capturar una máquina virtual Linux](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
