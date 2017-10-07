---
title: "información general de máquinas virtuales aaaWindows | Documentos de Microsoft"
description: "Aprenda a crear y administrar máquinas virtuales Windows en Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: fbae9c8e-2341-4ed0-bb20-fd4debb2f9ca
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 8015b1aa4bcdaac2e721f25d85a5bc995a22f0f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-windows-virtual-machines-in-azure"></a>Información general sobre las máquinas virtuales Windows en Azure

Las máquinas virtuales (VM) de Azure son uno de los diversos tipos de [recursos informáticos a petición y escalables](../../app-service-web/choose-web-site-cloud-service-vm.md) que ofrece Azure. Normalmente, se elige una máquina virtual cuando se necesita más control sobre el entorno informático de Hola que ofrecen hello otras opciones. En este artículo se proporciona información sobre lo que debe considerar antes de crear una máquina virtual, cómo crearla y cómo administrarla.

Un proporciona Azure VM Hola flexibilidad de virtualización sin necesidad de toobuy y mantener el hardware físico de Hola que lo ejecuta. Sin embargo, todavía necesita toomaintain Hola VM mediante la realización de tareas, como configurar, aplicar revisiones e instalar software de Hola que se ejecuta en él.

Las máquinas virtuales de Azure se pueden usar de diversas maneras. A continuación, se indican algunos ejemplos:

* **Desarrollar y probar** : máquinas virtuales de Azure ofrecen una rápida y fácilmente toocreate un equipo con configuraciones específicas requiere toocode y probar una aplicación.
* **Las aplicaciones de nube de hello** – porque puede fluctuar demanda de la aplicación, puede tener sentido económico toorun en una máquina virtual en Azure. Paga por las máquinas virtuales adicionales cuando las necesite y las desactiva cuando ya no sean necesarias.
* **Extended datacenter** : máquinas virtuales en una red virtual de Azure puede ascender fácilmente a la red de la organización tooyour conectado.

número de Hola de máquinas virtuales que usa su aplicación puede escalar verticalmente y out toowhatever es necesario toomeet sus necesidades.

## <a name="what-do-i-need-toothink-about-before-creating-a-vm"></a>¿Qué es necesario toothink sobre antes de crear una máquina virtual?
Siempre hay gran cantidad de [consideraciones de diseño](/architecture/reference-architectures/virtual-machines-linux?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) cuando se crea una infraestructura de aplicaciones en Azure. Estos aspectos de una máquina virtual va toothink importante antes de empezar:

* nombres de Hello los recursos de aplicación
* ubicación de Hola donde se almacenan los recursos de Hola
* tamaño de Hola de hello VM
* número máximo de Hola de máquinas virtuales que se pueden crear
* se ejecuta el sistema operativo Hola Hola VM
* configuración de Hola de hello VM después de iniciarse
* Hola ese Hola que máquina virtual debe de recursos relacionados

### <a name="naming"></a>Nomenclatura
Una máquina virtual tiene un [nombre](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooit asignado y tiene un nombre de equipo configurado como parte del sistema operativo de Hola. nombre de Hola de una máquina virtual puede tener caracteres too15.

Si usas un disco del sistema operativo Azure toocreate Hola, nombre de equipo de Hola y el nombre de la máquina virtual de hello son Hola igual. Si se [cargar y usar su propia imagen](upload-generalized-managed.md) que contiene un sistema operativo previamente configurado y usar toocreate una máquina virtual, nombres de hello pueden ser diferentes. Se recomienda que al cargar su propio archivo de imagen, defina nombre_equipo hello en el sistema operativo de Hola y el nombre de la máquina virtual de Hola Hola igual.

### <a name="locations"></a>Ubicaciones
Todos los recursos creados en Azure se distribuyen entre varios [regiones geográficas](https://azure.microsoft.com/regions/) alrededor de Hola a todos. Normalmente, se llama a la región de hello **ubicación** cuando se crea una máquina virtual. Para una máquina virtual, ubicación de hello especifica donde se almacenan los discos duros virtuales Hola.

Esta tabla muestra algunas de las formas de hello que puede obtener una lista de ubicaciones disponibles.

| Método | Descripción |
| --- | --- |
| Azure Portal |Seleccione una ubicación de la lista de hello cuando se crea una máquina virtual. |
| Azure PowerShell |Hola de uso [Get AzureRmLocation](/powershell/module/azurerm.resources/get-azurermlocation) comando. |
| API de REST |Hola de uso [enumerar ubicaciones](https://docs.microsoft.com/rest/api/resources/subscriptions#Subscriptions_ListLocations) operación. |

### <a name="vm-size"></a>Tamaño de VM
Hola [tamaño](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) de hello VM que usa viene determinado por carga de trabajo de Hola que desea toorun. tamaño de Hola que elija determina, a continuación, factores como el procesamiento de la capacidad de energía, memoria y almacenamiento. Azure ofrece una amplia variedad de tamaños toosupport muchos tipos de usos.

Azure cobra un [precio por hora](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) basándose en la máquina virtual de hello tamaño y sistema operativo. Durante las horas parciales, Azure cargos por solo de minutos de hello usado. El precio del almacenamiento se calcula y se cobra por separado.

### <a name="vm-limits"></a>Límites de máquina virtual
La suscripción tiene el valor predeterminado [límites de cuota](../../azure-subscription-service-limits.md) en su lugar que podría afectar a la implementación de Hola de muchas máquinas virtuales para el proyecto. límite actual de Hola por suscripción es 20 máquinas virtuales por región. Para aumentar estos límites, cree una incidencia de soporte técnico y solicite un aumento.

### <a name="operating-system-disks-and-images"></a>Imágenes y discos del sistema operativo
Máquinas virtuales utilizan [discos duros virtuales (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toostore su sistema operativo (SO) y los datos. Discos duros virtuales también se usan para las imágenes de hello que puede elegir entre tooinstall un sistema operativo. 

Azure proporciona muchos [imágenes marketplace](https://azure.microsoft.com/marketplace/virtual-machines/) toouse con varias versiones y tipos de sistemas operativos Windows Server. Las imágenes de Marketplace se identifican mediante el publicador de la imagen, la oferta, la SKU y la versión (normalmente, la versión se especifica como la más reciente). 

Esta tabla muestran algunas maneras de que se puede encontrar información de Hola para una imagen.

| Método | Descripción |
| --- | --- |
| Azure Portal |valores de Hello automáticamente se especifican automáticamente cuando se selecciona una imagen toouse. |
| Azure PowerShell |[Get-AzureRMVMImagePublisher](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimagepublisher) -Location "ubicación"<BR>[Get-AzureRMVMImageOffer](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimageoffer) -Location "ubicación" -Publisher "nombreDePublicador"<BR>[Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) -Location "ubicación" -Publisher "nombreDePublicador" -Offer "nombreDeOferta" |
| API de REST |[List image publishers](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publishers) (Lista de publicadores de imágenes)<BR>[List image offers](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offers) (Lista de ofertas de imágenes)<BR>[List image skus](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offer-skus) (Lista de SKU de imágenes) |

Puede elegir demasiado[cargar y usar su propia imagen](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account) y cuando lo hace, el nombre del publicador de Hola y oferta, sku no se utilizan.

### <a name="extensions"></a>Extensiones
Las [extensiones](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) de máquina virtual ofrecen funcionalidades adicionales de máquina virtual por medio de la configuración posterior a la implementación y tareas automatizadas.

Pueden llevarse a cabo estas tareas comunes mediante las extensiones:

* **Ejecutar scripts personalizados** : hello [extensión de Script personalizada](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) le ayudará a configurar las cargas de trabajo en hello VM mediante la ejecución de la secuencia de comandos cuando hello máquina virtual se aprovisiona.
* **Implementar y administrar las configuraciones** : hello [extensión de configuración de estado deseado (DSC) de PowerShell](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) le ayuda a configurar DSC en una máquina virtual toomanage entornos y configuraciones.
* **Recopilar datos de diagnóstico** : hello [extensión de diagnósticos de Azure](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) le ayuda a configurar datos de diagnóstico de toocollect VM de Hola que pueden ser utilizado toomonitor Hola estado de la aplicación.

### <a name="related-resources"></a>Recursos relacionados
recursos de Hello en esta tabla se usan por hello VM y necesitan tooexist o se crea cuando se crea la VM de Hola.

| Recurso | Obligatorio | Description |
| --- | --- | --- |
| [Grupos de recursos](../../azure-resource-manager/resource-group-overview.md) |Sí |Hola VM debe estar contenido en un grupo de recursos. |
| [Cuenta de almacenamiento](../../storage/common/storage-create-storage-account.md) |Sí |Hola VM debe toostore de cuenta de almacenamiento de hello sus discos duros virtuales. |
| [Red virtual](../../virtual-network/virtual-networks-overview.md) |Sí |Hola VM debe ser un miembro de una red virtual. |
| [Dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) |No |Hola máquina virtual puede tener un tooremotely de tooit de dirección asignada de IP pública obtener acceso a él. |
| [Interfaz de red](../../virtual-network/virtual-network-network-interface.md) |Sí |Hola VM debe hello toocommunicate de interfaz de red en la red de Hola. |
| [Discos de datos](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |No |Hola VM puede incluir capacidades de almacenamiento de tooexpand de discos de datos. |

## <a name="how-do-i-create-my-first-vm"></a>¿Cómo se crea la primera máquina virtual?
Hay varias opciones para crear la máquina virtual. elección de Hola que realice depende de entorno de Hola en que se ejecuta. 

Esta tabla proporciona tooget de información que se inició la creación de la máquina virtual.

| Método | Artículo |
| --- | --- |
| Azure Portal |[Crear una máquina virtual con Windows y portal de Hola](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Plantillas |[Creación de una máquina virtual Windows con una plantilla del Administrador de recursos](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Azure PowerShell |[Creación de una máquina virtual Windows con PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| SDK de cliente |[Implementación de recursos de Azure mediante C#](csharp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| API de REST |[Create or update a VM](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-create-or-update) (Creación o actualización de una máquina virtual) |

Aunque se espera que nunca suceda, en ocasiones algo sale mal. Si esta situación puede ocurrir tooyou, ver información de hello en [problemas de implementación del Administrador de recursos de solución de problemas con la creación de una máquina virtual de Windows en Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="how-do-i-manage-hello-vm-that-i-created"></a>¿Cómo administro Hola VM que he creado?
Las máquinas virtuales pueden administrarse mediante un portal basado en el explorador, herramientas de línea de comandos con compatibilidad para scripts o directamente a través de API. Algunas tareas de administración habituales que puede realizar están obteniendo información acerca de una máquina virtual, iniciar sesión tooa VM, administrar la disponibilidad y realizar copias de seguridad.

### <a name="get-information-about-a-vm"></a>Obtención información acerca de una máquina virtual
Esta tabla muestran algunas de las formas de Hola que puede obtener información acerca de una máquina virtual.

| Método | Descripción |
| --- | --- |
| Azure Portal |En el menú del concentrador hello, haga clic en **máquinas virtuales** y, a continuación, seleccione Hola VM de lista de Hola. En la hoja de Hola para hello VM, que tiene información de toooverview de acceso, valores de configuración y las métricas de supervisión. |
| Azure PowerShell |Para obtener información sobre el uso de máquinas virtuales de toomanage de PowerShell, consulte [crear y administrar máquinas virtuales de Windows con el módulo de PowerShell de Azure de hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |
| API de REST |Hola de uso [información obtener VM](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) información de tooget operación sobre una máquina virtual. |
| SDK de cliente |Para obtener información acerca del uso de C# toomanage máquinas virtuales, consulte [administrar máquinas virtuales de Azure mediante el Administrador de recursos de Azure y C#](csharp-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |

### <a name="log-on-toohello-vm"></a>Inicie sesión en toohello VM
Use botón Conectar de Hola Hola portal de Azure demasiado[iniciar una sesión de escritorio remoto (RDP)](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). A veces posibles problemas al tratar de toouse una conexión remota. Si esta situación puede ocurrir tooyou, consulte información de Ayuda de hello en [tooan de conexiones de escritorio remoto solucionar problemas de Azure máquina virtual que ejecuta Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="manage-availability"></a>Administración de la disponibilidad
Es importante toounderstand cómo demasiado[garantizar una alta disponibilidad](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para la aplicación. Esta configuración implica la creación de varios tooensure de máquinas virtuales que se ejecuta al menos uno.

Para su tooqualify implementación nuestro contrato de nivel de servicio de VM 99.95, deberá toodeploy dos o más máquinas virtuales en ejecución la carga de trabajo dentro de un [conjunto de disponibilidad](tutorial-availability-sets.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Esta configuración garantiza que las máquinas virtuales estén distribuidas entre varios dominios de error e implementadas en hosts con diferentes períodos de mantenimiento. Hola completa [SLA de Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/) explica Hola garantizada la disponibilidad de Azure como un todo.

### <a name="back-up-hello-vm"></a>Respaldar Hola VM
A [del almacén de servicios de recuperación](../../backup/backup-introduction-to-azure-backup.md) corresponde a datos de uso tooprotect activos en los servicios de copia de seguridad de Azure y Azure Site Recovery. Puede usar un almacén de servicios de recuperación demasiado[implementar y administrar las copias de seguridad para las máquinas virtuales implementadas por el Administrador de recursos con PowerShell](../../backup/backup-azure-vms-automation.md). 

## <a name="next-steps"></a>Pasos siguientes
* Si su intención es toowork con máquinas virtuales de Linux, mirar [Azure y Linux](../linux/overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Más información acerca de cómo configurar la infraestructura de hello las directrices de Hola [tutorial de infraestructura de Azure de ejemplo](infrastructure-example.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
