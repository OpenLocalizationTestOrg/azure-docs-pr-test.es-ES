---
title: Hola aaaUpdate agente Linux de Azure desde GitHub | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooupdate agente Linux de Azure para la VM de Linux en la versión más reciente de Azure toohello desde GitHub"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: f1f19300-987d-4f29-9393-9aba866f049c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: mingzhan
ms.openlocfilehash: 4ce7c56efc1e6563e6415f7687573f9fb9e7b4c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a>¿Cómo tooupdate Hola agente Linux de Azure en una máquina virtual

tooupdate su [agente Linux de Azure](https://github.com/Azure/WALinuxAgent) en una VM de Linux en Azure, ya debe tener:

- Tener en Azure una VM que ejecuta Linux.
- Una VM de Linux de conexión toothat mediante SSH.

Siempre debe comprobar para un paquete en el repositorio de distribución de Linux de hello en primer lugar. Es posible paquete Hola disponible no puede ser versión más reciente de hello, sin embargo, al habilitar actualización automática se asegurará Hola agente Linux siempre obtendrá la actualización más reciente de Hola. Si tiene problemas de instalación de los administradores de paquetes de saludo, debe buscar soporte técnico del proveedor de distribución de Hola.

## <a name="updating-hello-azure-linux-agent"></a>Actualizar Hola agente Linux de Azure

## <a name="ubuntu"></a>Ubuntu

#### <a name="check-your-current-package-version"></a>Comprobación de la versión del paquete actual

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>Actualización de la memoria caché del paquete

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Instalar la versión más reciente de paquete de Hola

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a>Comprobación de que la actualización automática está habilitada

En primer lugar, compruebe toosee si está habilitado:

```bash
cat /etc/waagent.conf
```

Busque "AutoUpdate.Enabled". Si ve esta salida, significa que la característica está habilitada:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable ejecutar:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Reinicie el servicio de hello waagent

#### <a name="restart-agent-for-1404"></a>Reinicio del agente para 14.04

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a>Reinicio del agente para 16.04/17.04

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a>Debian

### <a name="debian-7-wheezy"></a>Debian 7 "Wheezy"

#### <a name="check-your-current-package-version"></a>Comprobación de la versión del paquete actual

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a>Actualización de la memoria caché del paquete

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Instalar la versión más reciente de paquete de Hola

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a>Habilitación de la actualización automática del agente
Esta versión de Debian no tiene una versión > = 2.0.16, lo que significa que AutoUpdate no está disponible en este caso. salida de Hello de hello encima comando le mostrará si se trata de un paquete de hello actualizada.

### <a name="debian-8-jessie--debian-9-stretch"></a>Debian 8 "Jessie"/Debian 9 "Stretch"

#### <a name="check-your-current-package-version"></a>Comprobación de la versión del paquete actual

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>Actualización de la memoria caché del paquete

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Instalar la versión más reciente de paquete de Hola

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a>Comprobación de que la actualización automática está habilitada 

En primer lugar, compruebe toosee si está habilitado:

```bash
cat /etc/waagent.conf
```

Busque "AutoUpdate.Enabled". Si ve esta salida, significa que la característica está habilitada:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable ejecutar:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Reinicie el servicio de hello waagent

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a>Red Hat/CentOS

### <a name="rhelcentos-6"></a>RHEL/CentOS 6

#### <a name="check-your-current-package-version"></a>Comprobación de la versión del paquete actual

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>Comprobación de las actualizaciones disponibles

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>Instalar la versión más reciente de paquete de Hola

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a>Comprobación de que la actualización automática está habilitada 

En primer lugar, compruebe toosee si está habilitado:

```bash
cat /etc/waagent.conf
```

Busque "AutoUpdate.Enabled". Si ve esta salida, significa que la característica está habilitada:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable ejecutar:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Reinicie el servicio de hello waagent

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a>RHEL/CentOS 7

#### <a name="check-your-current-package-version"></a>Comprobación de la versión del paquete actual

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>Comprobación de las actualizaciones disponibles

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>Instalar la versión más reciente de paquete de Hola

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a>Comprobación de que la actualización automática está habilitada 

En primer lugar, compruebe toosee si está habilitado:

```bash
cat /etc/waagent.conf
```

Busque "AutoUpdate.Enabled". Si ve esta salida, significa que la característica está habilitada:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable ejecutar:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Reinicie el servicio de hello waagent

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a>SUSE SLES

### <a name="suse-sles-11-sp4"></a>SUSE SLES 11 SP4

#### <a name="check-your-current-package-version"></a>Comprobación de la versión del paquete actual

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>Comprobación de las actualizaciones disponibles

Hola por encima de la salida se mostrará si el paquete de hello está activo toodate.

#### <a name="install-hello-latest-package-version"></a>Instalar la versión más reciente de paquete de Hola

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>Comprobación de que la actualización automática está habilitada 

En primer lugar, compruebe toosee si está habilitado:

```bash
cat /etc/waagent.conf
```

Busque "AutoUpdate.Enabled". Si ve esta salida, significa que la característica está habilitada:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable ejecutar:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Reinicie el servicio de hello waagent

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a>SUSE SLES 12 SP2

#### <a name="check-your-current-package-version"></a>Comprobación de la versión del paquete actual

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>Comprobación de las actualizaciones disponibles

En la salida de hello de hello anterior, esto le mostrará si el paquete de hello está actualizada.

#### <a name="install-hello-latest-package-version"></a>Instalar la versión más reciente de paquete de Hola

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>Comprobación de que la actualización automática está habilitada 

En primer lugar, compruebe toosee si está habilitado:

```bash
cat /etc/waagent.conf
```

Busque "AutoUpdate.Enabled". Si ve esta salida, significa que la característica está habilitada:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable ejecutar:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Reinicie el servicio de hello waagent

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a>Oracle 6 y 7

Para Oracle Linux, asegúrese de que ese hello `Addons` repositorio está habilitado. Elija el archivo de hello tooedit `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) o `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux) y cambie la línea hello `enabled=0` demasiado`enabled=1` en **[ol6_addons]** o **[ol7_addons]** en este archivo.

A continuación, la versión de más reciente de hello tooinstall de hello agente Linux de Azure, tipo:

```bash
sudo yum install WALinuxAgent
```

Si no encuentra el repositorio de complemento de hello simplemente puede agregar estas líneas al final de hello del archivo .repo según la versión de Oracle Linux tooyour:

Para las máquinas virtuales Oracle Linux 6:

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

Para las máquinas virtuales Oracle Linux 7:

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

A continuación, escriba:

```bash
sudo yum update WALinuxAgent
```

Normalmente esto es todo lo que necesita, pero si por algún motivo que necesita tooinstall desde https://github.com directamente, Hola uso siguiendo los pasos.


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a>Actualizar agente Linux de hello cuando no existe ningún paquete de agente de distribución

Instalar wget (no hay algunos distribuciones que no se instalan de forma predeterminada, como las versiones 6.4 y 6.5 Redhat, CentOS y Oracle Linux) escribiendo `sudo yum install wget` en línea de comandos de Hola.

### <a name="1-download-hello-latest-version"></a>1. Descargar la versión más reciente de Hola
Abra [Hola versión del agente de Linux de Azure en GitHub](https://github.com/Azure/WALinuxAgent/releases) en una página web y obtenga más información sobre número de versión más reciente de Hola. (Puede buscar la versión actual escribiendo `waagent --version`).

#### <a name="for-version-22x-or-later-type"></a>Para la versión 2.2.x o posteriores, escriba:
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

Hello línea siguiente usa versión 2.2.0 como ejemplo:

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a>2. Instalar Hola agente Linux de Azure

#### <a name="for-version-22x-use"></a>Para la versión 2.2.x, use:
Puede que necesite paquete de hello tooinstall `setuptools` en primer lugar, consulte [aquí](https://pypi.python.org/pypi/setuptools). A continuación, ejecute:

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a>Comprobación de que la actualización automática está habilitada

En primer lugar, compruebe toosee si está habilitado:

```bash
cat /etc/waagent.conf
```

Busque "AutoUpdate.Enabled". Si ve esta salida, significa que la característica está habilitada:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable ejecutar:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a>3. Reinicie el servicio de hello waagent
Para la mayoría de las distribuciones de Linux:

```bash
sudo service waagent restart
```

Para Ubuntu, use:

```bash
sudo service walinuxagent restart
```

Para CoreOS, use:

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a>4. Confirme la versión del agente de Linux de Azure Hola
    
```bash
waagent -version
```

CoreOS, Hola por encima del comando puede no funcione.

Verá que Hola agente Linux de Azure versión ha sido actualizado a la versión nueva de toohello.

Para obtener más información sobre Hola agente Linux de Azure, consulte [archivo Léame de agente de Linux de Azure](https://github.com/Azure/WALinuxAgent).
