---
title: "aaaRed infraestructura de actualización de Hat (RHUI) | Documentos de Microsoft"
description: "Obtenga información acerca de Red Hat Update Infrastructure (RHUI) para instancias de Red Hat Enterprise Linux a petición de Microsoft Azure"
services: virtual-machines-linux
documentationcenter: 
author: BorisB2015
manager: timlt
editor: 
ms.assetid: f495f1b4-ae24-46b9-8d26-c617ce3daf3a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: borisb
ms.openlocfilehash: cc244857104b25e4e61862c518db77e915e137ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a>Red Hat Update Infrastructure (RHUI) para máquinas virtuales Red Hat Enterprise Linux a petición en Azure
Máquinas virtuales creadas a partir de Hola a petición Red Hat Enterprise Linux (RHEL) imágenes disponible en Azure Marketplace son tooaccess registrados Hola implementado en Azure la infraestructura de actualización de Hat de rojo (RHUI).  instancias RHEL de petición de Hola tienen repositorio de acceso tooa yum regionales y tooreceive capaz de las actualizaciones incrementales.

lista de repositorios de yum Hello, que es administrado por RHUI, se configura en la instancia RHEL durante el aprovisionamiento. No necesita ninguna configuración adicional - ejecutar toodo `yum update` después de la instancia RHEL actualizaciones más recientes de hello tooget listo.

> [!NOTE]
> En septiembre de 2016 implementamos un RHUI de Azure actualizada y en enero de 2017 comenzamos apagado por fases de hello RHUI anteriores de Azure. Si ha estado utilizando imágenes RHEL hello (o sus instantáneas) de septiembre de 2016 o posterior - probablemente se requiere ninguna acción. Si, sin embargo, tiene las instantáneas anteriores/VMs, su configuración necesita toobe que se actualizó con un acceso ininterrumpido toohello RHUI de Azure.
> 

## <a name="rhui-azure-infrastructure-update"></a>Actualización de la infraestructura RHUI en Azure
A partir de septiembre de 2016, Azure tiene un nuevo conjunto de servidores de Red Hat Update Infrastructure (RHUI). Estos servidores se implementan con [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) para que cualquier máquina virtual, independientemente de la región, pueda usar un único punto de conexión (rhui-1.micrsoft.com). Hola nuevas imágenes de pago por uso de RHEL (PAYG) en servidores nuevos de Azure RHUI de hello Azure Marketplace (versiones con fecha de septiembre de 2016 o posteriores) toohello de punto y no requieren ninguna acción adicional.

### <a name="determine-if-action-is-required"></a>Determinar si se requiere alguna acción
Si experimenta problemas de conexión tooAzure RHUI de la máquina virtual de Azure RHEL PAYG, siga estos pasos
1. Inspeccione la configuración de máquina virtual del punto de conexión de RHUI de Azure.

    Compruebe si `/etc/yum.repos.d/rh-cloud.repo` archivo también contiene referencia`rhui-[1-3].microsoft.com` en URL base del `[rhui-microsoft-azure-rhel*]` sección del archivo de Hola. Si es - utilizas Hola nueva RHUI de Azure.

    Si lo que señala tooa ubicación con hello sigue el patrón `mirrorlist.*cds[1-4].cloudapp.net` -actualización de la configuración de hello es necesaria.

    Si está usando la nueva configuración de Hola y sigue sin poder conectarse tooAzure RHUI - archivo de un caso de soporte técnico con Microsoft o con Red Hat.

    > [!NOTE]
    > Acceso hospedado tooAzure RHUI es toohello limita las máquinas virtuales de [intervalos de direcciones IP de centro de datos de Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).
    > 

2. Si hello RHUI de Azure anterior sigue estando disponible cuando realice esta comprobación y le gustaría tooautomatically actualizar la configuración de hello, ejecute hello siguiente comando:

    `sudo yum update RHEL6`o `sudo yum update RHEL7` según la versión de la familia de hello RHEL.

3. Si ya no se puede conectar toohello antiguo RHUI de Azure, siga Hola manual los pasos descritos en la sección siguiente Hola.

4. Asegúrese de que configuración de hello tooupdate en origen de Hola o instantánea de imagen afectados VM se haya proporcionado de.

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a>Cierre por fases de Hola antiguo RHUI de Azure
Durante el cierre de Hola de hello antiguo RHUI de Azure, restringimos acceder a tooit como se indica a continuación:

1. Restringir aún más el tooset de acceso (ACL) de direcciones IP que ya se está conectando tooit. Posibles efectos secundarios: Si continúa utilizando Hola antiguo RHUI de Azure: las máquinas virtuales nuevas pueden no ser capaz de tooconnect tooit. Máquinas virtuales de RHEL con direcciones IP dinámica que vaya a través de la secuencia de apagado/desasignar/inicio puede recibir IP nueva y, por tanto, también podría empiezan a generar errores tooconnect toohello RHUI de Azure anterior

2. Apagado de los servidores de entrega de contenido reflejados. Posibles efectos secundarios: desconectamos CDSes más puede que vea ya `yum update` tiempo de mantenimiento, seleccione más los tiempos de espera hasta hello cuando ya no se puede conectar toohello antiguo RHUI de Azure.

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a>Hola direcciones IP para servidores de entrega de contenido de hello nuevos RHUI son
Si usas toofurther de configuración de red restringen el acceso de las máquinas virtuales de RHEL PAYG, asegúrese de que Hola después de direcciones IP se permite para `yum update` toowork según se encuentra en el entorno de Hola. 

```
# Azure Global
13.91.47.76
40.85.190.91
52.187.75.218
52.174.163.213

# Azure US Government
13.72.186.193

# Azure Germany
51.5.243.77
51.4.228.145
```

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a>Actualización manual procedimiento toouse Hola nuevos Azure RHUI servidores
Firma de clave pública de descarga (a través de curl) Hola

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

Comprobar clave Hola descargado

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

Comprobar la salida de hello, comprobar `keyid` y `user ID packet`:

```bash
Version: GnuPG v1.4.7 (GNU/Linux)
:public key packet:
        version 4, algo 1, created 1446074508, expires 0
        pkey[0]: [2048 bits]
        pkey[1]: [17 bits]
        keyid: EB3E94ADBE1229CF
:user ID packet: "Microsoft (Release signing) <gpgsecurity@microsoft.com>"
:signature packet: algo 1, keyid EB3E94ADBE1229CF
        version 4, created 1446074508, md5len 0, sigclass 0x13
        digest algo 2, begin of digest 1a 9b
        hashed subpkt 2 len 4 (sig created 2015-10-28)
        hashed subpkt 27 len 1 (key flags: 03)
        hashed subpkt 11 len 5 (pref-sym-algos: 9 8 7 3 2)
        hashed subpkt 21 len 3 (pref-hash-algos: 2 8 3)
        hashed subpkt 22 len 2 (pref-zip-algos: 2 1)
        hashed subpkt 30 len 1 (features: 01)
        hashed subpkt 23 len 1 (key server preferences: 80)
        subpkt 16 len 8 (issuer key ID EB3E94ADBE1229CF)
        data: [2047 bits]
```

Instalar la clave pública de Hola

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

Descargue, compruebe e instale el cliente RPM.

Descargue lo siguiente para RHEL 6:

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

Para RHEL 7:

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

Compruebe:

```bash
rpm -Kv azureclient.rpm
```

Compruebe en la salida esa firma de hello paquete es correcto

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

Instalar Hola RPM

```bash
sudo rpm -U azureclient.rpm
```

Tras la finalización, compruebe que puede tener acceso a Hola de formulario RHUI de Azure VM

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a>All-in-one script para automatizar Hola delante de la tarea
Usar hello siguiente secuencia de comandos como tarea de hello tooautomate necesarios sobre la actualización de las máquinas virtuales toohello nuevo Azure RHUI los servidores afectados.

```sh
# Download key
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 

# Validate key
if ! gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release | grep -q "keyid: EB3E94ADBE1229CF"; then
    echo "Keyfile azure.asc NOT valid. Exiting."
    exit 1
fi

# Install Key
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release

# Download RPM package
if grep -q "release 7" /etc/redhat-release; then
    ver=7
elif  grep -q "release 6" /etc/redhat-release; then
    ver=6
else
    echo "Version not supported, exiting"
    exit 1
fi

url=https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel$ver/rhui-azure-rhel$ver-2.0-2.noarch.rpm
curl -o azureclient.rpm "$url"

# Verify package
if ! rpm -Kv azureclient.rpm | grep -q "key ID be1229cf: OK"; then
    echo "RPM failed validation ($url)"
    exit 1
fi

# Install package
sudo rpm -U azureclient.rpm
```

## <a name="rhui-overview"></a>Introducción sobre RHUI
[Infraestructura de Red Hat actualización](https://access.redhat.com/products/red-hat-update-infrastructure) ofrece un contenido del repositorio de soluciones muy escalables toomanage yum para instancias en la nube de Red Hat Enterprise Linux que están hospedadas por proveedores de nube de certificados de Red Hat. Basándonos en proyecto de pasta de nivel superior de hello, RHUI permite que los proveedores de nube toolocally reflejado repositorio hospedados en Red Hat contenido de, crear repositorios personalizados con su propio contenido y poner dichos grupo grande de repositorios tooa disponibles de los usuarios finales a través de un equilibrio de carga sistema de entrega de contenido.

## <a name="regions-where-rhui-is-available"></a>Regiones donde se implementa RHUI
RHUI está disponible en todas las regiones donde estén disponibles las imágenes a petición RHEL. Actualmente incluyen públicas todas las regiones incluidas en hello [panel de estado de Azure](https://azure.microsoft.com/status/) página, las regiones de Azure en Alemania y de gobierno de EE. En el precio se incluye el acceso de RHUI a las máquinas virtuales aprovisionadas desde imágenes RHEL a petición. Disponibilidad en la nube regionales o nacionales adicionales se actualizarán mientras se expanda disponibilidad de petición RHEL Hola futuras.

> [!NOTE]
> Acceso hospedado tooAzure RHUI es toohello limita las máquinas virtuales de [intervalos de direcciones IP de centro de datos de Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).
> 
> 

## <a name="get-updates-from-another-update-repository"></a>Obtención de actualizaciones de otro repositorio de actualización
Si necesita tooget actualizaciones desde un repositorio de actualización diferentes (en lugar de RHUI hospedado de Azure), primero debe toounregister las instancias de RHUI. Es necesario el registro toore usarlas con la infraestructura de actualización deseado hello (por ejemplo, Red Hat satélite o Red Hat cliente Portal CDN). Necesitará suscripciones apropiadas a Red Hat para estos servicios y registrarse en [Red Hat Cloud Access en Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).

toounregister RHUI y vuelva a registrar tooyour actualización infraestructura siguen estos pasos:

1. Edite /etc/yum.repos.d/rh-cloud.repo y cambie todos `enabled=1` demasiado`enabled=0`. Por ejemplo:
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. Edite /etc/yum/pluginconf.d/rhnplugin.conf y cambie `enabled=0` demasiado`enabled=1`.
3. A continuación, registrar con la infraestructura de hello deseado, como Portal del cliente de Red Hat. Siga la Guía de solución de Red Hat [cómo tooregister y suscribirse a un Portal del cliente de Red Hat de sistema toohello](https://access.redhat.com/solutions/253273).

> [!NOTE]
> Acceso toohello RHUI hospedado de Azure se incluye en el precio de imagen de hello RHEL pago por uso (PAYG). Al anular el registro de una VM de RHEL PAYG de hello RHUI hospedado de Azure no convierte máquina virtual de hello en VM de tipo de Bring Your-posee-licencia (BYOL). Si registra Hola misma máquina virtual con otro origen de actualizaciones puede acumulando gastos por el dobles: la primera vez para hello y precio del software de Azure RHEL segunda vez para suscripciones de Red Hat. 
> 
> Si necesita toouse sistemáticamente una infraestructura de actualizaciones que no sea RHUI hospedado de Azure considere la posibilidad de crear e implementar sus propias imágenes (BYOL-type) como se describe en [crear y cargar Red Hat máquina virtual de Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artículo.
> 

## <a name="next-steps"></a>Pasos siguientes
toocreate una VM de rojo Hat Enterprise Linux de imagen de pago por uso de Azure Marketplace y aproveche RHUI hospedado de Azure vaya demasiado[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/). Será capaz de toouse `yum update` en la instancia RHEL sin ninguna configuración adicional.

