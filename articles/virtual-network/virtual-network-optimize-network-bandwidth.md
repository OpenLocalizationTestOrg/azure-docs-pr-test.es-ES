---
title: rendimiento de red VM aaaOptimize | Documentos de Microsoft
description: "Obtenga información acerca de cómo el rendimiento de la red de toooptimize máquina virtual de Azure."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: steveesp
ms.openlocfilehash: a5cff2d0ab6e3553c3f90d99629521a431477de0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a>Optimización del rendimiento de red en las máquinas virtuales de Azure

Las máquinas virtuales de Azure (VM) tienen una configuración de red predeterminada que se puede optimizar para mejorar aún más el rendimiento de la red. Este artículo describe cómo toooptimize red de rendimiento para Windows de Microsoft Azure y máquinas virtuales de Linux, incluidas las distribuciones principales como Ubuntu, CentOS y Red Hat.

## <a name="windows-vm"></a>Máquina virtual de Windows

Si la máquina virtual de Windows es compatible con [Accelerated redes](virtual-network-create-vm-accelerated-networking.md), habilitar esta característica sería la configuración óptima de hello para el rendimiento. En el caso de otras máquinas virtuales Windows, el uso de escalado en el lado de la recepción (RSS) pueden logar un rendimiento máximo mayor que las que no lo usan. En las máquinas virtuales Windows, RSS se puede deshabilitar de forma predeterminada. Completar hello siguiendo los pasos toodetermine si RSS está habilitado y tooenable si está deshabilitado.

1. Escriba hello `Get-NetAdapterRss` toosee de comandos de PowerShell si RSS está habilitado para un adaptador de red. Hola siguiendo la salida de ejemplo devuelto de hello `Get-NetAdapterRss`, RSS no está habilitado.

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. Escriba Hola después tooenable comando RSS:

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    comando de Hello anterior no tiene una salida. comando Hello cambia configuración de NIC, provocar la pérdida de conectividad temporal de aproximadamente un minuto. Aparece un cuadro de diálogo volviendo a conectarse durante la pérdida de conectividad de Hola. Normalmente se restaure la conectividad después tercer intento de Hola.
3. Confirme que RSS está habilitado en hello VM escribiendo hello `Get-NetAdapterRss` comando nuevo. Si se realiza correctamente, se devuelve la siguiente salida de ejemplo de Hola:

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a>Máquina virtual de Linux

De manera predeterminada, en las máquinas virtuales Linux de Azure RSS está siempre habilitado. Núcleos Linux publicados a partir de enero de 2017 incluyen nuevas opciones de optimización de red que permiten un rendimiento de red de VM de Linux tooachieve superior.

### <a name="ubuntu"></a>Ubuntu

Optimización de la orden tooget hello, actualice primero toohello admitido la última versión, a partir de junio de 2017, que es:
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
Una vez completada la actualización de hello, escriba Hola después del núcleo de comandos tooget hello más reciente:

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

Comando opcional:

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a>Kernel de versión preliminar de Azure de Ubuntu
> [!WARNING]
> Esta vista previa de Linux de Azure no puede tener el kernel Hola de mismo nivel de disponibilidad y confiabilidad como imágenes de Marketplace y núcleos que por lo general son versión de disponibilidad. características de Hello no se admiten, pueden haber limitado las capacidades y no pueden ser tan confiable como núcleo de hello predeterminado. No utilice este kernel para cargas de trabajo de producción.

Significativa al rendimiento se puede lograr mediante la instalación de hello propuesto kernel de Linux de Azure. tootry este kernel, agregue esta línea too/etc/apt/sources.list

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

Luego, ejecute estos comandos como raíz.
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a>CentOS

Optimización de la orden tooget hello, actualice primero toohello admitido la última versión, a partir de julio de 2017, que es:
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
Una vez completada la actualización de hello, instalación Hola servicios de integración de Linux (LIS) más reciente.
optimización del rendimiento de Hello es en LIS, desde 4.2.2-2. Escriba Hola después comandos tooinstall LIS:

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a>Red Hat

Optimización de la orden tooget hello, actualice primero toohello admitido la última versión, a partir de julio de 2017, que es:
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
Una vez completada la actualización de hello, instalación Hola servicios de integración de Linux (LIS) más reciente.
optimización del rendimiento de Hello es en LIS, desde 4.2. Escriba Hola después toodownload de comandos e instalar LIS:

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

Obtener más información sobre Linux Integration Services versión 4.2 para Hyper-V mediante la visualización hello [página de descarga de](https://www.microsoft.com/download/details.aspx?id=55106).

## <a name="next-steps"></a>Pasos siguientes
* Ahora que hello VM está optimizada, vea el resultado de hello con [pruebas VM de Azure de ancho de banda/rendimiento](virtual-network-bandwidth-testing.md) para su escenario.
* Obtenga más información con las [Preguntas más frecuentes (P+F) acerca de Azure Virtual Network](virtual-networks-faq.md)
