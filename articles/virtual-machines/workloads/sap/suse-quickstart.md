---
title: "aaaTesting SAP NetWeaver en máquinas virtuales de Microsoft Azure SUSE Linux | Documentos de Microsoft"
description: "Pruebas de SAP NetWeaver en máquinas virtuales de SUSE Linux de Microsoft Azure"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 645e358b-3ca1-4d3d-bf70-b0f287498d7a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: hermannd
ms.openlocfilehash: 0e3faab05417a1a15541e2b79aa7eddacda44611
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="running-sap-netweaver-on-microsoft-azure-suse-linux-vms"></a>Ejecución de SAP NetWeaver en máquinas virtuales de SUSE Linux de Microsoft Azure
Este artículo describen varios tooconsider cosas cuando ejecutas SAP NetWeaver en máquinas virtuales (VM) de Microsoft Azure SUSE Linux. A partir del 19 de mayo de 2016 SAP NetWeaver es compatible oficialmente con máquinas virtuales de SUSE Linux en Azure. Todos los detalles sobre las versiones de Linux, las versiones de kernel SAP etc., se pueden encontrar en la nota de SAP 1928533 "SAP Applications on Azure: Supported Products and Azure VM types" (Aplicaciones SAP en Azure: productos admitidos y tipos de máquina virtual de Azure).
Se puede encontrar documentación adicional sobre SAP en máquinas virtuales Linux aquí: [Uso de SAP en máquinas virtuales (VM) Linux ](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hola siguiente información puede ayudarle a evitar algunos problemas potenciales.

## <a name="suse-images-on-azure-for-running-sap"></a>Imágenes SUSE en Azure para ejecutar SAP
Para ejecutar SAP NetWeaver en Azure, utilice solo SUSE Linux Enterprise Server SLES 12 (SPx). Consulte también la nota SAP 1928533. Una imagen SUSE especial está en hello Azure Marketplace ("SLES 11 SP3 para SAP CAL"), pero no está pensado para uso general. No usar esta imagen porque está reservada para hello [biblioteca de dispositivo de nube de SAP](https://cal.sap.com/) solución.  

Todas las nuevas pruebas e instalaciones en Azure deben realizarse con Azure Resource Manager. toolook para imágenes de SUSE SLES y versiones mediante el uso de PowerShell de Azure o hello Azure interfaz de línea de comandos (CLI), Hola de uso después de comandos. A continuación, puede utilizar la salida de hello, por ejemplo, toodefine Hola imagen del sistema operativo en una plantilla JSON para la implementación de una nueva máquina virtual Linux de SUSE.
Estos comandos de PowerShell son válidos para la versión de Azure PowerShell 1.0.1 y posterior.

Aunque es posible toouse Hola estándar SLES imágenes para las instalaciones de SAP se recomienda toomake uso de Hola SLES nueva para imágenes SAP que están disponibles ahora en hello Azure imagen Galería. Para obtener más información acerca de estas imágenes se puede encontrar en hello correspondiente [página Azure Marketplace]( https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SUSE.SLES-SAP ) o hello [página web de SUSE preguntas más frecuentes sobre SLES para SAP]( https://www.suse.com/products/sles-for-sap/frequently-asked-questions/ ).


* Busque publicadores existentes que incluyan SUSE:
  
   ```
   PS  : Get-AzureRmVMImagePublisher -Location "West Europe"  | where-object { $_.publishername -like "*US*"  }
   CLI : azure vm image list-publishers westeurope | grep "US"
   ```
* Busque ofertas existentes de SUSE:
  
   ```
   PS  : Get-AzureRmVMImageOffer -Location "West Europe" -Publisher "SUSE"
   CLI : azure vm image list-offers westeurope SUSE
   ```
* Busque ofertas de SUSE SLES:
  
   ```
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES"
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP"
   CLI : azure vm image list-skus westeurope SUSE SLES
   CLI : azure vm image list-skus westeurope SUSE SLES-SAP
   ```
* Busque una versión específica de una SKU de SLES:
  
   ```
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES" -skus "12-SP2"
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP" -skus "12-SP2"
   CLI : azure vm image list westeurope SUSE SLES 12-SP2
   CLI : azure vm image list westeurope SUSE SLES-SAP 12-SP2
   ```

## <a name="installing-walinuxagent-in-a-suse-vm"></a>Instalación de WALinuxAgent en una máquina virtual de SUSE
agente de Hello llamado WALinuxAgent es parte de las imágenes SLES de hello en hello Azure Marketplace. Para más información sobre cómo instalarlo manualmente (por ejemplo, al cargar un disco duro virtual (VHD) del sistema operativo de SLES desde una ubicación local), consulte:

* [OpenSUSE](http://software.opensuse.org/package/WALinuxAgent)
* [Las tablas de Azure](../../linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SUSE](https://www.suse.com/communities/blog/suse-linux-enterprise-server-configuration-for-windows-azure/)

## <a name="sap-enhanced-monitoring"></a>"Supervisión mejorada" de SAP
SAP "supervisión mejorada" es un toorun de requisitos previos obligatorio SAP en Azure. Compruebe los detalles en la nota de SAP 2191498 "SAP on Linux with Azure: Enhanced Monitoring" (SAP en Linux con Azure: supervisión mejorada).

## <a name="attaching-azure-data-disks-tooan-azure-linux-vm"></a>Adjuntar tooan de discos de datos de Azure VM de Linux de Azure
Nunca debe montar tooan de discos de datos de Azure VM de Linux de Azure mediante el uso de Id. de dispositivo de Hola. En su lugar, utilice el identificador único universal (UUID) del Hola. Tenga cuidado al usar discos de datos de Azure de toomount de herramientas gráficas, por ejemplo. Compruebe las entradas de hello en/etc/fstab.

problema de Hello con Id. de dispositivo de hello es que es posible que cambien y, a continuación, podría bloquearse hello Azure VM en el proceso de arranque de Hola. problema de hello toomitigate, podría agregar parámetro de nofail de hello en/etc/fstab. Sin embargo, tenga cuidado con nofail porque aplicaciones podrían utilizar el punto de montaje de hello como antes, pueden escribir en el sistema de archivos de raíz de hello en caso de que no se monta un disco de datos de Azure externo durante el arranque de Hola.

Hola única excepción toomounting a través de UUID que está asociando un disco del sistema operativo para solucionar problemas, como se describe en los pasos de la sección de Hola.

## <a name="troubleshooting-a-suse-vm-that-isnt-accessible-anymore"></a>Solución de problemas con una máquina virtual de SUSE a la que ya no es posible tener acceso
Puede haber situaciones donde se bloquea una VM SUSE en Azure en el proceso de arranque de hello (por ejemplo, con un error relacionado con el montaje de discos). Puede comprobar este problema mediante la característica de diagnósticos de arranque de Hola para máquinas virtuales de Azure v2 en hello portal de Azure. Para más información, consulte [Boot diagnostics](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/)(Diagnóstico de arranque).

Problema de hello toosolve unidireccional es tooattach el disco del sistema operativo de Hola de hello dañado VM tooanother SUSE VM en Azure. A continuación, realice los cambios adecuados como editar/etc/fstab o eliminar reglas de udev de red, como se describe en la sección siguiente de Hola.

Hay una tooconsider importante. Implementar varias máquinas virtuales de SUSE de hello hace de la misma imagen de Azure Marketplace (por ejemplo, SLES 11 SP4) Hola OS tooalways de disco se monta Hola mismo UUID. Por tanto, usan Hola UUID tooattach un disco del sistema operativo de una máquina virtual diferente que se ha implementado mediante Hola misma imagen de Azure Marketplace dará como resultado dos UUID idéntico. Esto ocasiona problemas y puede significar que Hola VM destinado a la solución de problemas de hecho arrancará desde Hola adjuntada y dañado disco del sistema operativo en lugar de Hola original.

Hay dos tooavoid formas esto:

* Usar una imagen de Azure Marketplace diferentes para hello solución de problemas de máquina virtual (por ejemplo, SLES 11 SPx en lugar de SLES 12).
* No adjuntar el disco del sistema operativo de hello dañado desde otra máquina virtual mediante UUID: uso algo más.

## <a name="uploading-a-suse-vm-from-on-premises-tooazure"></a>Cargar una VM SUSE desde tooAzure local
Para obtener una descripción de tooupload de pasos de hello una VM SUSE desde tooAzure locales, consulte [preparar una máquina virtual SLES o openSUSE para Azure](../../linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Si desea tooupload una máquina virtual sin Desaprovisionamiento de hello paso al final de hello (por ejemplo, tookeep una instalación existente de SAP, así como nombre de host de hello), compruebe Hola siguientes elementos:

* Asegúrese de que dicho disco Hola SO está montado mediante el uso de Id. de dispositivo no hello y UUID. Cambiar tooUUID solo en/etc/fstab no es suficiente para el disco del sistema operativo de Hola. Además, no olvide cargador de arranque de hello tooadapt a través de YaST o editando /boot/grub/menu.lst.
* Si utiliza el formato VHDX hello para el disco de sistema operativo SUSE hello y convertir tooVHD para cargar tooAzure, es muy probable que ese dispositivo de red Hola dejará de eth0 tooeth1. tooavoid problemas cuando está arrancando en Azure más adelante, cambiar tooeth0 espera tal y como se describe en [corregir eth0 en clona SLES 11 VMware](https://dartron.wordpress.com/2013/09/27/fixing-eth1-in-cloned-sles-11-vmware/).

Además toowhat descrita en el artículo de hello, se recomienda que quite esto:

   /lib/udev/rules.d/75-persistent-net-generator.rules

También puede instalar hello toohelp de agente de Linux de Azure (waagent) para evitar posibles problemas, como no hay varios NIC.

## <a name="deploying-a-suse-vm-on-azure"></a>Implementación de una máquina virtual de SUSE en Azure
Debe crear nuevas máquinas virtuales de SUSE mediante archivos de plantilla JSON en el nuevo modelo de Azure Resource Manager Hola. Después de crea el archivo de plantilla de hello JSON, puede implementar Hola VM mediante Hola siguiente comando CLI como un tooPowerShell alternativo:

   ```
   azure group deployment create "<deployment name>" -g "<resource group name>" --template-file "<../../filename.json>"

   ```
Para más información sobre los archivos de plantilla JSON, consulte [Creación de plantillas de Azure Resource Manager](../../../resource-group-authoring-templates.md) y [Plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/).

Para obtener más información acerca de CLI y el Administrador de recursos de Azure, consulte [Hola Utilice CLI de Azure para Mac, Linux y Windows con el Administrador de recursos de Azure](../../../xplat-cli-azure-resource-manager.md).

## <a name="sap-license-and-hardware-key"></a>Clave de licencia y hardware de SAP
Para la certificación de SAP Azure oficial de hello, un nuevo mecanismo era toocalculate se ha introducido clave de hardware SAP de Hola que se usa para la licencia SAP de Hola. kernel SAP de Hello tenía toobe adaptar toomake uso de este. Las versiones anteriores de kernel de SAP para Linux no incluían este cambio en el código. Por lo tanto, en ciertas situaciones (por ejemplo, VM de Azure el cambio de tamaño), cambia la clave de hardware SAP de Hola y licencia SAP de Hola se ya no sean válidas. Esto se ha resuelto en los kernels de Linux de SAP más recientes de Hola. Para más información, consulte la nota de SAP 1928533.

## <a name="suse-sapconf-package--tuned-adm"></a>Paquete sapconf de SUSE/tuned-adm
SUSE ofrece un paquete denominado "sapconf" que administra un conjunto de opciones específicas de SAP. Para obtener más detalles sobre este paquete de qué hace y cómo tooinstall y utilizarlo, vea [con sapconf tooprepare un sistemas SAP de SUSE Linux Enterprise Server toorun](https://www.suse.com/communities/blog/using-sapconf-to-prepare-suse-linux-enterprise-server-to-run-sap-systems/) y [¿qué es sapconf o cómo tooprepare un SUSE Linux Enterprise ¿Servidor para ejecutar sistemas SAP? ](http://scn.sap.com/community/linux/blog/2014/03/31/what-is-sapconf-or-how-to-prepare-a-suse-linux-enterprise-server-for-running-sap-systems).

Hola mientras tanto hay una nueva herramienta que reemplaza sapconf - optimizar-adm. Uno puede encontrar más detalles sobre esta herramienta Hola dos vínculos siguientes.

La documentación de SLES sobre tuned-adm y el perfil de SAP Hana se encuentra [aquí](https://www.suse.com/documentation/sles-for-sap-12/book_s4s/data/sec_s4s_configure_sapconf.html) 

Puede encontrar información sobre el ajuste de sistemas para cargas de trabajo SAP con tuned-adm [aquí](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/book_s4s/book_s4s.pdf) (capítulo 6.2).

## <a name="nfs-share-in-distributed-sap-installations"></a>Recursos compartidos de NFS en instalaciones de SAP distribuidas
Si tiene una instalación distribuida, por ejemplo, donde desea base de datos de tooinstall Hola y Hola servidores de aplicaciones de SAP en máquinas virtuales independientes: puede compartir directorio /sapmnt de Hola a través de Network File System (NFS). Si tiene problemas con los pasos de instalación de hello después de crear recursos compartidos de NFS para /sapmnt de hello, compruebe toosee si "no_root_squash" está establecida para el recurso compartido de Hola.

## <a name="logical-volumes"></a>Volúmenes lógicos
Hola anteriores si falta un gran volumen lógico en varios discos de datos de Azure (por ejemplo, para hello base de datos SAP), se recomendaba toouse mdadm como lvm no se valida totalmente aún en Azure. toolearn tooset de RAID de Linux en Azure mediante el uso de mdadm, vea [configurar RAID de software en Linux](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Hola mientras tanto a partir del principio de mayo de 2016 también lvm es totalmente compatible en Azure y se puede usar como un toomdadm alternativo. Para más información sobre lvm en Azure, consulte [Configuración del LVM en una máquina virtual Linux en Azure](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="azure-suse-repository"></a>Repositorio SUSE de Azure
Si tiene un problema con el repositorio de Azure SUSE acceso toohello estándar, puede usar un comando simple tooreset lo. Esto puede ocurrir si crea una imagen de sistema operativo privada en una región de Azure y, a continuación, copia Hola imagen tooa otra región donde desea toodeploy nuevas máquinas virtuales que se basan en esta imagen de sistema operativo privada. Sólo tiene que ejecutar Hola siguiente comando dentro de hello VM:

   ```
   service guestregister restart
   ```

## <a name="gnome-desktop"></a>Escritorio Gnome
Si desea toouse Hola Gnome escritorio tooinstall un completo sistema de demostración SAP dentro de una sola máquina virtual, con una GUI de SAP, explorador y la consola de administración de SAP: usan esta sugerencia tooinstall en imágenes de Azure SLES hello:

   Para SLES 11:

   ```
   zypper in -t pattern gnome
   ```

   Para SLES 12:

   ```
   zypper in -t pattern gnome-basic
   ```

## <a name="sap-support-for-oracle-on-linux-in-hello-cloud"></a>Soporte técnico SAP para Oracle en Linux en la nube de Hola
Hay una restricción de soporte técnico de Oracle en Linux en entornos virtualizados. Aunque esto no es un tema específico de Azure, es importante toounderstand. SAP no admite Oracle en SUSE ni en Red Hat en una nube pública como Azure. toodiscuss en este tema, póngase en contacto directamente con Oracle.

