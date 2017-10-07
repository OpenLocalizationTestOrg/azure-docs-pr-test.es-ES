---
title: "aaaOverview de máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "Describe los servicios de proceso, almacenamiento y red de Azure con máquinas virtuales de Linux."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: rickstercdn
manager: timlt
editor: 
ms.assetid: 7965a80f-ea24-4cc2-bc43-60b574101902
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 09/14/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 958e219d53026d787a7a41f2fd13c29c739a9238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux"></a>Azure y Linux
Microsoft Azure es una colección cada vez mayor de servicios en la nube, públicos e integrados, que incluyen servicios de análisis, máquinas virtuales, bases de datos, móviles, de red, de almacenamiento y web, ideales para hospedar sus soluciones.  Microsoft Azure proporciona una plataforma informática escalable que permite tooonly pago por lo que usa, si desea - sin necesidad de tooinvest en hardware local.  Azure está listo cuando están tooscale sus soluciones de seguridad y out toowhatever escala necesite necesidades de hello tooservice de sus clientes.

Si está familiarizado con Hola distintas características de Amazon AWS, puede examinar hello Azure vs AWS [documento de definición de asignación](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/).

## <a name="regions"></a>Regiones
Recursos de Microsoft Azure se distribuyen en varias regiones geográficas alrededor de Hola a todos.  Un "region" representa varios centros de datos en una única área geográfica.  Tenemos 34 regiones disponibles con carácter general alrededor de Hola a todos con un regiones 4 adicionales anunciado. Dado que seguimos tooexpand nuestra cobertura global - mantenemos que una lista actualizada de existente y recientemente anunció regiones.

* [Regiones de Azure](https://azure.microsoft.com/regions/)

## <a name="availability"></a>Disponibilidad
Anunciamos que una sector iniciales instancia única máquina de contrato de nivel de servicio del 99,9% proporciona que implementar Hola máquinas virtuales con almacenamiento de premium para todos los discos.  En orden para su tooqualify de implementación para nuestro estándar 99,95% contrato de nivel de servicio de VM, sigue necesitando toodeploy dos o más máquinas virtuales en ejecución la carga de trabajo dentro de un conjunto de disponibilidad. Esto garantizará que las máquinas virtuales estén distribuidas en varios dominios de error en nuestros centros de datos e implementadas en hosts con diferentes tiempos de mantenimiento. Hola completa [SLA de Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/) explica Hola garantizada la disponibilidad de Azure como un todo.

## <a name="managed-disks"></a>Managed Disks

Administrar discos controla el almacenamiento de Azure creación de cuentas y administración en segundo plano de Hola para usted y garantiza que no tengan tooworry acerca de los límites de escalabilidad de Hola de cuenta de almacenamiento de Hola. Simplemente especifique el tamaño del disco de Hola y nivel de rendimiento de hello (Standard o Premium) y Azure crea y administra el disco de hello en su nombre. Incluso a medida que agregue más discos o escala vertical y horizontalmente Hola VM, no tienes tooworry sobre el almacenamiento de Hola que se va a usar. Si va a crear nuevas máquinas virtuales, [usar hello Azure CLI 2.0](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) u Hola toocreate Azure portal máquinas virtuales con discos de datos y sistema operativo administrado. Si tiene máquinas virtuales con discos no administrados, puede [convertir su toobe de máquinas virtuales con discos administrados el respaldo](convert-unmanaged-to-managed-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

También puede administrar sus imágenes personalizadas en una cuenta de almacenamiento por cada región de Azure y usarlos toocreate cientos de máquinas virtuales en hello misma suscripción. Para obtener más información acerca de los discos administrados, vea hello [información general de discos administradas](../windows/managed-disks-overview.md).

## <a name="azure-virtual-machines--instances"></a>Máquinas virtuales e instancias de Azure
Microsoft Azure permite ejecutar varias de las distribuciones de Linux más populares proporcionadas y mantenidas por diversos asociados.  Encontrará las distribuciones como Red Hat Enterprise, CentOS, Debian, Ubuntu, CoreOS, RancherOS, FreeBSD y mucho más en hello Azure Marketplace. Se trabaja activamente con diversos Linux Comunidades tooadd incluso más tipos toohello [Distros de Linux con el respaldo de Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lista.

Si la distribución de Linux preferido de elección no está presente actualmente en la Galería de hello, puede "Traer su propios Linux" máquina virtual por [crear y cargar un VHD de Linux en Azure](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Máquinas virtuales de Azure le permiten toodeploy una amplia gama de las soluciones de informática de forma ágil. Puede implementar prácticamente cualquier carga de trabajo y cualquier lenguaje en prácticamente cualquier sistema operativo, ya sea Windows, Linux o uno creado de forma personalizada por alguno de los que integran nuestra lista cada vez mayor de asociados. ¿Todavía no ve lo que busca?  No se preocupe, también puede traer sus propias imágenes desde el entorno local.

## <a name="vm-sizes"></a>Tamaños de máquina virtual
Cuando se implementa una máquina virtual en Azure, va tooselect un tamaño de máquina virtual dentro de uno de nuestra serie de tamaños que es adecuado tooyour carga de trabajo. tamaño de Hello también afecta al Hola potencia de procesamiento, memoria y la capacidad de almacenamiento de máquina virtual de Hola. Se le facturará según la cantidad de Hola Hola de tiempo VM se esté ejecutando y consumen sus recursos asignados. Consulte una lista completa de [tamaños de máquina virtual](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Estas son algunas directrices básicas para seleccionar un tamaño de máquina virtual desde una de nuestras series (A, D, DS, G y GS).
* Las máquinas virtuales de la serie A son las más económicas para empezar con cargas de trabajo ligeras y escenarios de desarrollo y pruebas. Están ampliamente disponibles en todas las regiones y puede conectarse y usar todas las máquinas de toovirtual disponibles de recursos estándar.
* Los tamaños de la serie A (A8 - A11) son configuraciones especiales para procesos intensivos adecuadas para aplicaciones de clúster de proceso de alto rendimiento.
* Máquinas virtuales de la serie D son toorun diseñado aplicaciones que requieren mayor capacidad de proceso y rendimiento de disco temporal. Máquinas virtuales de serie D proporcionan procesadores más rápidos, una mayor proporción de memoria a núcleo y una unidad de estado sólida (SSD) para el disco temporal de Hola.
* Dv2-series, es la versión más reciente de Hola de nuestra serie D, cuenta con una CPU más eficaz. Hola Dv2 serie CPU es aproximadamente un 35% más rápido que Hola serie D CPU. Se basa en hello última generación v3 de 2,4 GHz Intel Xeon® E5-2673 procesador (Haskell) y con hello aumento tecnología Intel Turbo 2.0, pueden crecer hasta too3.2 GHz. Hola Dv2 serie tiene Hola mismas configuraciones de memoria y disco como Hola serie D.
* Máquinas virtuales de serie G ofrecen hello más memoria y ejecutan en hosts que tienen procesadores de la familia Intel Xeon E5 V3.

Nota: DS-series y GS-series las máquinas virtuales tienen acceso tooPremium almacenamiento: almacenamiento de alto rendimiento, latencia baja para cargas de trabajo intensivas de E/S de seguridad de nuestro SSD. Premium Storage está disponible en determinadas regiones. Para obtener información, consulte:

* [Premium Storage: almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](../../storage/common/storage-premium-storage.md)

## <a name="automation"></a>Automation
tooachieve una cultura correctos de DevOps, toda infraestructura debe ser el código.  Cuando todos Hola infraestructura reside en el código puede ser fácil volver a crear (servidores de Phoenix).  Azure funciona con automatización principales de hello todas las herramientas como Ansible, Chef, SaltStack y Puppet.  Asimismo, tiene sus propias herramientas de automatización:

* [Plantillas de Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [VMAccess de Azure](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Azure está implementando la compatibilidad con [cloud-init](http://cloud-init.io/) en la mayoría de las distribuciones de Linux que admiten este paquete.  En estos momentos, las máquinas virtuales Ubuntu de Canonical se implementan con cloud-init habilitado de forma predeterminada.  Rojo sombreros RHEL, CentOS y Fedora admite init de la nube, sin embargo hello Azure mantenidas RedHat las imágenes no tienen instalado de init en la nube.  init de nube toouse en un sistema operativo de la familia de RedHat, debe crear una imagen personalizada con instalado de init en la nube.

* [Uso de cloud-init en máquinas virtuales con Linux](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quotas"></a>Cuotas
Cada suscripción de Azure tiene límites de cuota predeterminados en su lugar que podría afectar a la implementación de Hola de un gran número de máquinas virtuales para el proyecto. límite actual de Hola por suscripción es 20 máquinas virtuales por región.  Los límites de cuota se pueden elevar rápida y fácilmente presentando una incidencia de soporte técnico solicitando un aumento del límite.  Más información sobre los límites de cuota:

* [Límites de servicio de suscripción de Azure](../../azure-subscription-service-limits.md)

## <a name="partners"></a>Asociados
Microsoft trabaja en estrecha colaboración con nuestros socios de imágenes de hello tooensure disponibles se actualizó y optimizadas para un tiempo de ejecución de Azure.  Para obtener más información sobre nuestros asociados, visite las siguientes páginas de Marketplace.

* Linux en Azure: [distribuciones aprobadas](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* SUSE - [Azure Marketplace - SUSE Linux Enterprise Server](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?search=%27SUSE%27)
* Red Hat: [Azure Marketplace - RedHat Enterprise Linux 7.2](https://azure.microsoft.com/marketplace/partners/redhat/redhatenterpriselinux72/)
* Canonical: [Azure Marketplace - Ubuntu Server 16.04 LTS](https://azure.microsoft.com/marketplace/partners/canonical/ubuntuserver1604lts/)
* Debian: [Azure Marketplace - Debian 8 "Jessie"](https://azure.microsoft.com/marketplace/partners/credativ/debian8/)
* FreeBSD: [Azure Marketplace - FreeBSD 10.3](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
* CoreOS: [Azure Marketplace - CoreOS (Stable)](https://azure.microsoft.com/marketplace/partners/coreos/coreosstable/)
* RancherOS: [Azure Marketplace - RancherOS](https://azure.microsoft.com/marketplace/partners/rancher/rancheros/)
* Bitnami: [Bitnami Library for Azure](https://azure.bitnami.com/)
* Mesosphere: [Azure Marketplace - Mesosphere DC/OS on Azure](https://azure.microsoft.com/marketplace/partners/mesosphere/dcosdcos/)
* Docker: [Azure Marketplace - Azure Container Service with Docker Swarm](https://azure.microsoft.com/marketplace/partners/microsoft/acsswarms/)
* Jenkins: [Azure Marketplace - CloudBees Jenkins Platform](https://azure.microsoft.com/marketplace/partners/cloudbees/jenkins-platformjenkins-platform/)

## <a name="getting-started-with-linux-on-azure"></a>Introducción a Linux en Azure
toobegin con Azure se necesita una cuenta de Azure, Hola CLI de Azure instalado y un par de claves públicas y privadas de SSH.

### <a name="sign-up-for-an-account"></a>Registro para obtener una cuenta
Hola primer paso para usar Hola nube de Azure es toosign hacia arriba para una cuenta de Azure.  Vaya toohello [registro de la cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/) página tooget iniciado.

### <a name="install-hello-cli"></a>Instalar Hola CLI
Con la nueva cuenta de Azure, puede empezar a inmediatamente mediante Hola portal de Azure, que es un panel de administración basada en web.  Hola toomanage nube de Azure a través de la línea de comandos de hello instalar hello `azure-cli`.  Instalar hello [CLI de Azure 2.0](/cli/azure/install-azure-cli) en la estación de trabajo Mac o Linux.

### <a name="create-an-ssh-key-pair"></a>Creación de un par de claves SSH
Ahora tiene una cuenta de Azure, portal web de Azure de Hola y Hola CLI de Azure.  Hola siguiente paso es toocreate un par de claves de SSH es tooSSH usado en Linux sin utilizar una contraseña.  [Crear claves SSH en Linux y Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooenable mejorarán la seguridad y los inicios de sesión sin contraseña.

### <a name="create-a-vm-using-hello-cli"></a>Crear una máquina virtual mediante Hola CLI
Crear una VM Linux utilizando Hola CLI es un toodeploy de forma rápida una máquina virtual sin dejando Hola terminal en que está trabajando.  Todo lo que puede especificar en el portal web de hello está disponible a través de un indicador de línea de comandos o un conmutador.  

* [Crear una VM de Linux con hello CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="create-a-vm-in-hello-portal"></a>Crear una máquina virtual en el portal de Hola
Crear una VM de Linux en el portal web de Azure de hello es una manera punto tooeasily y click-through Hola implementación de varias opciones tooget tooa.  En lugar de utilizar marcadores de línea de comandos o modificadores, es capaz de tooview un diseño web "nice" de varias opciones y configuración.  Todos los elementos disponibles a través de la interfaz de línea de comandos de hello también está disponible en el portal de Hola.

* [Crear una VM de Linux con hello Portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="login-using-ssh-without-a-password"></a>Inicio de sesión mediante SSH sin una contraseña
Hola VM ahora se ejecuta en Azure y están listo toolog en.  Uso de contraseñas toolog en mediante SSH es inseguro y lleve mucho tiempo.  Utilizar claves de SSH se Hola modo más seguro y también hello toologin de manera más rápida.  Cuando se crea VM de Linux a través del portal de Hola u Hola CLI, tiene dos opciones de autenticación.  Si elige una contraseña de SSH, Azure configura Hola VM tooallow los inicios de sesión a través de las contraseñas.  Si ha elegido toouse una clave pública SSH, Azure configura Hola VM tooonly permitir inicios de sesión a través de SSH de claves y deshabilita los inicios de sesión de contraseña. toosecure permitir inicios de sesión de claves SSH, use la VM de Linux solamente Hola opción de clave pública SSH durante la creación de VM en el portal de Hola o CLI Hola.

## <a name="related-azure-components"></a>Componentes de Azure relacionados
## <a name="storage"></a>Storage
* [Introducción tooMicrosoft almacenamiento de Azure](../../storage/common/storage-introduction.md)
* [Agregar una VM de Linux con cli de azure hello tooa de disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [¿Cómo tooattach datos de un disco tooa VM de Linux en hello portal de Azure](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a>Redes
* [Información general sobre redes virtuales](../../virtual-network/virtual-networks-overview.md)
* [Direcciones IP en Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)
* [Abrir puertos tooa VM de Linux en Azure](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Crear un nombre de dominio completo en hello portal de Azure](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="containers"></a>Contenedores
* [Máquinas virtuales y contenedores de Azure](containers.md)
* [Presentación del servicio Contenedor de Azure](../../container-service/container-service-intro.md)
* [Implementación de un clúster del servicio Contenedor de Azure](../../container-service/dcos-swarm/container-service-deployment.md)

## <a name="next-steps"></a>Pasos siguientes
Ya tiene una visión general de Linux en Azure.  paso siguiente Hello es toodive en y crear algunas máquinas virtuales.

* [Explore nuestra creciente lista de scripts de ejemplo para tareas comunes mediante la CLI de Azure](cli-samples.md)
