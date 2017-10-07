---
title: "proceso intensivo aaaUse máquinas virtuales de Azure con lote | Documentos de Microsoft"
description: "¿Cómo cambia el tamaño de tootake ventaja de la máquina virtual compatible con RDMA o basadas en la GPU en grupos de Azure Batch"
services: batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: danlep
ms.openlocfilehash: 6a462a5f2a44ddcec8bf4e5c200d444cac8fafe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-rdma-capable-or-gpu-enabled-instances-in-batch-pools"></a>Uso de instancias compatibles con RDMA o habilitadas para GPU en grupos de Batch

toorun determinados trabajos por lotes, puede querer tootake aprovechar los tamaños de máquina virtual de Azure diseñados para el cálculo a gran escala. Por ejemplo, toorun varias instancias [las cargas de trabajo MPI](batch-mpi.md), puede elegir A8, A9, o tamaños H-series que tienen una red de la interfaz de acceso de memoria directa remota (RDMA). Estos tamaños conectan tooan InfiniBand red para la comunicación entre nodos, que puede acelerar las aplicaciones de MPI. O bien, para aplicaciones CUDA, puede elegir tamaños de la serie N que incluyen tarjetas de unidad de procesamiento gráfico (GPU) de NVIDIA Tesla.

Este artículo proporciona instrucciones y ejemplos toouse algunos de los tamaños especializados de Azure en grupos por lotes. Para especificaciones e información preliminar, consulte:

* Tamaños de VM de proceso de alto rendimiento ([Linux](../virtual-machines/linux/sizes-hpc.md) y [Windows](../virtual-machines/windows/sizes-hpc.md)) 

* Tamaños de VM habilitados para GPU ([Linux](../virtual-machines/linux/sizes-gpu.md) y [Windows](../virtual-machines/windows/sizes-gpu.md)) 


## <a name="subscription-and-account-limits"></a>Límites de la cuenta y la suscripción

* **Las cuotas** -una o varias de las cuotas de Azure pueden limitar número de Hola o el tipo de nodos se puede agregar grupo de lote de tooa. Es más probable que toobe limitado al elegir compatible con RDMA, basadas en la GPU u otros tamaños de máquinas virtuales con varios núcleos. Según el tipo de saludo de la cuenta de lote que ha creado, pudieron aplicar cuotas de hello propia toohello cuenta o suscripción tooyour.

    * Si ha creado su cuenta de lote en hello **por lotes servicio** configuración, está limitado por hello [cuota de núcleos dedicados por cuenta de lote](batch-quota-limit.md#resource-quotas). De forma predeterminada, esta cuota es de 20 núcleos. Se aplica una cuota independiente demasiado[máquinas virtuales de prioridad baja](batch-low-pri-vms.md), si los usa. 

    * Si ha creado la cuenta de hello en hello **suscripción usuario** configuración, su suscripción limita el número de Hola de núcleos VM por región. Vea [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../azure-subscription-service-limits.md). La suscripción también aplica un tamaños de VM de cuota regional toocertain, incluidas las instancias HPC y GPU. En la configuración de suscripción de usuario de hello, sin cuotas adicionales aplican toohello cuenta de lote. 

  Tendrá que tooincrease las cuotas de uno o más cuando se utiliza un tamaño de memoria virtual especializado en lote. toorequest un aumento de la cuota, abra un [solicitud de soporte técnico al cliente en línea](../azure-supportability/how-to-create-azure-support-request.md) sin cargo.

* **Disponibilidad de la región** : proceso intensivo máquinas virtuales podrían no estar disponibles en regiones de Hola donde crear las cuentas de lote. toocheck que un tamaño está disponible, consulte [productos disponibles por región](https://azure.microsoft.com/regions/services/).


## <a name="dependencies"></a>Dependencias

Hola RDMA y capacidades GPU de tamaños de proceso intensivo solo se admiten en algunos sistemas operativos. Dependiendo del sistema operativo, tal vez necesite tooinstall o configurar el controlador adicional u otro software. Hola las tablas siguientes resume estas dependencias. Consulte los artículos vinculados para más información. Para grupos de opciones tooconfigure por lotes, vea más adelante en este artículo.


### <a name="linux-pools---virtual-machine-configuration"></a>Grupos de Linux: configuración de la máquina virtual

| Tamaño | Capacidad | Sistemas operativos | Requisitos de software | Configuración del grupo |
| -------- | -------- | ----- |  -------- | ----- |
| [H16r, H16mr, A8 y A9](../virtual-machines/linux/sizes-hpc.md#rdma-capable-instances) | RDMA | HPC SUSE Linux Enterprise Server 12 o<br/>HPC basado en CentOS<br/>(Azure Marketplace) | Intel MPI 5 | Habilitar la comunicación entre nodos y deshabilitar la ejecución de tareas simultáneas |
| [Serie NC*](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms) | GPU NVIDIA Tesla K80 | Ubuntu 16.04 LTS.<br/>Red Hat Enterprise Linux 7.3 o<br/>Basado en CentOS 7.3<br/>(Azure Marketplace) | Controladores de NVIDIA CUDA Toolkit 8.0 | N/D | 
| [Serie NV](../virtual-machines/linux/n-series-driver-setup.md#install-grid-drivers-for-nv-vms) | GPU NVIDIA Tesla M60 | Ubuntu 16.04 LTS<br/>Red Hat Enterprise Linux 7.3<br/>Basado en CentOS 7.3<br/>(Azure Marketplace) | Controladores de NVIDIA GRID 4.3 | N/D |

*La conectividad de RDMA en VM NC24r se admite en HPC basado en CentOS 7.3 con Intel MPI.



### <a name="windows-pools---virtual-machine-configuration"></a>Grupos de Windows: configuración de la máquina virtual

| Tamaño | Capacidad | Sistemas operativos | Requisitos de software | Configuración del grupo |
| -------- | ------ | -------- | -------- | ----- |
| [H16r, H16mr, A8 y A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | RDMA | Windows Server 2012 R2 o<br/>Windows Server 2012 (Azure Marketplace) | Microsoft MPI 2012 R2 o posterior, o<br/> Intel MPI 5<br/><br/>Extensión HpcVMDrivers para VM de Azure | Habilitar la comunicación entre nodos y deshabilitar la ejecución de tareas simultáneas |
| [Serie NC*](../virtual-machines/windows/n-series-driver-setup.md) | GPU NVIDIA Tesla K80 | Windows Server 2016 o <br/>Windows Server 2012 R2 (Azure Marketplace) | Controladores de NVIDIA Tesla o de CUDA Toolkit 8.0| N/D | 
| [Serie NV](../virtual-machines/windows/n-series-driver-setup.md) | GPU NVIDIA Tesla M60 | Windows Server 2016 o<br/>Windows Server 2012 R2 (Azure Marketplace) | Controladores de NVIDIA GRID 4.3 | N/D |

*La conectividad de RDMA en VM NC24r se admite en Windows Server 2012 R2 con la extensión HpcVMDrivers y Microsoft MPI o Intel MPI.

### <a name="windows-pools---cloud-services-configuration"></a>Grupos de Windows: configuración de servicios en la nube

> [!NOTE]
> No se admiten tamaños de N-series en grupos de lote con la configuración de servicios de nube de Hola.
>

| Tamaño | Capacidad | Sistemas operativos | Requisitos de software | Configuración del grupo |
| -------- | ------- | -------- | -------- | ----- |
| [H16r, H16mr, A8 y A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | RDMA | Windows Server 2012 R2,<br/>Windows Server 2012 o<br/>Windows Server 2008 R2 (familia del SO invitado) | Microsoft MPI 2012 R2 o posterior, o<br/>Intel MPI 5<br/><br/>Extensión HpcVMDrivers para VM de Azure | Habilitar la comunicación entre nodos y<br/> deshabilitar la ejecución de tareas simultáneas |





## <a name="pool-configuration-options"></a>Opciones de configuración de grupos

tooconfigure un tamaño de memoria virtual especializado para su grupo de lote, hello las API de lote y herramientas proporcionan varios software tooinstall necesario de opciones o controladores, incluidos:

* [Iniciar tarea](batch-api-basics.md#start-task) -cargar un paquete de instalación como un tooan de archivo de recursos cuenta de almacenamiento de Azure en hello misma región que Hola cuenta de lote. Crear un archivo de recursos de inicio tareas línea de comandos tooinstall hello en modo silencioso cuando se inicia el grupo de Hola. Para obtener más información, vea hello [documentación de la API de REST](/rest/api/batchservice/add-a-pool-to-an-account#bk_starttask).

  > [!NOTE] 
  > tarea de inicio de Hello debe ejecutar con permisos elevados (Administrador) y debe esperar a correcto.
  >

* [Paquete de aplicación](batch-application-packages.md) : agregar un tooyour de paquete de instalación comprimido cuenta de lote y configurar una referencia de paquete en el grupo de Hola. Esta configuración se carga y descomprime el paquete de hello en todos los nodos de grupo de Hola. Si el paquete de hello es un instalador, crear una aplicación de Hola de instalación de inicio tareas línea de comandos toosilently en todos los nodos de grupo. Opcionalmente, instalar paquetes de saludo cuando una tarea está programada toorun en un nodo.

* [Imagen del grupo personalizado](batch-api-basics.md#pool) : crear personalizados de Windows o imagen de VM de Linux que contiene los controladores, software u otra configuración necesaria para hello tamaño de máquina virtual. Si ha creado su cuenta de lote en configuración de suscripción de usuario de hello, especificar imagen personalizada de hello para el grupo de lote. (Las imágenes personalizadas no se admiten en las cuentas en la configuración de servicio de lote de Hola.) Imágenes personalizadas sólo pueden utilizarse con los grupos de configuración de máquina virtual de Hola.

  > [!IMPORTANT]
  > En grupos de Batch, actualmente no puede usar una imagen personalizada creada con discos de Managed Disks o con Premium Storage.
  >



* [Procesar por lotes astilleros](https://github.com/Azure/batch-shipyard) configura automáticamente Hola GPU y RDMA toowork de forma transparente con cargas de trabajo en contenedores en Azure Batch. Batch Shipyard se controla por completo con archivos de configuración. Hay muchas ejemplo receta configuraciones disponibles que permiten a las cargas de trabajo GPU y RDMA como hello [CNTK GPU receta](https://github.com/Azure/batch-shipyard/tree/master/recipes/CNTK-GPU-OpenMPI) que preconfigura controladores de GPU en máquinas virtuales de serie de N y carga de software de Microsoft cognitivos Toolkit como una imagen de Docker.


## <a name="example-microsoft-mpi-on-an-a8-vm-pool"></a>Ejemplo: Microsoft MPI en un grupo de VM A8

toorun las aplicaciones de MPI de Windows en un grupo de nodos de Azure A8, deberá tooinstall una implementación de MPI compatible. Estos son tooinstall de pasos de ejemplo [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) en una ventana de bloque con un paquete de aplicación de lote.

1. Descargar hello [el paquete de instalación](http://go.microsoft.com/FWLink/p/?LinkID=389556) (MSMpiSetup.exe) para la versión más reciente de Hola de Microsoft MPI.
2. Crear un archivo zip del paquete de saludo.
3. Cargar la cuenta de lote de hello paquete tooyour. Para conocer los pasos, vea hello [paquetes de aplicación](batch-application-packages.md) instrucciones. Especifique un identificador de aplicación (por ejemplo, *MSMPI*) y una versión (por ejemplo, *8.1*). 
4. Mediante las API de lote de Hola o portal de Azure, cree un grupo en configuración de servicios de nube de hello con número de hello deseado de nodos y la escala. Hello tabla siguiente muestran tooset de configuración de ejemplo de MPI en modo desatendido mediante una tarea de inicio:

| Configuración | Valor |
| ---- | ----- | 
| **Tipo de imagen** | Cloud Services |
| **Familia de SO** | Windows Server 2012 R2 (familia 4 de SO) |
| **Tamaño del nodo** | Estándar A8 |
| **Comunicación entre nodos habilitada** | True |
| **Número máximo de tareas por nodo** | 1 |
| **Referencias de paquetes de aplicación** | MSMPI |
| **Tarea de inicio habilitada** | True<br>**Línea de comandos** - `"cmd /c %AZ_BATCH_APP_PACKAGE_MSMPI#8.1%\\MSMpiSetup.exe -unattend -force"`<br/>**Identidad del usuario**: Usuario automático de grupo, administrador<br/>**Esperar operación correcta**: True

## <a name="example-nvidia-tesla-drivers-on-nc-vm-pool"></a>Ejemplo: Controladores de NVIDIA Tesla en el grupo de VM NC

aplicaciones de CUDA toorun en un grupo de nodos de contexto de nomenclatura de Linux, deberá tooinstall CUDA Kit de herramientas 8.0 en nodos de Hola. Hola Kit de herramientas instala a controladores de GPU de NVIDIA Tesla necesarios Hola. Estos son los pasos de ejemplo toodeploy una imagen de Ubuntu 16.04 LTS personalizada con controladores de GPU de Hola:

1. Implemente una VM NC6 de Azure en la que se ejecute Ubuntu 16.04 LTS. Por ejemplo, crear Hola VM en hello nos sur región Central. Asegúrese de que crea Hola VM con el almacenamiento estándar, y *sin* discos administrados.
2. Siga Hola pasos tooconnect toohello VM y [instalar controladores CUDA](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms).
3. Cancelar el aprovisionamiento de agente de Linux de hello y, a continuación, capturar imagen de VM de Linux con comandos de hello 1.0 de CLI de Azure. Para conocer los pasos, consulte [Captura de una máquina virtual Linux que se ejecuta en Azure](../virtual-machines/linux/capture-image-nodejs.md). Tome nota del URI de la imagen de Hola.
  > [!IMPORTANT]
  > No utilice imagen de Hola de toocapture de comandos de CLI de Azure 2.0 para el lote de Azure. Comandos de CLI 2.0 Hola sólo captura actualmente máquinas virtuales creadas mediante discos administrados.
  >
4. Crear una cuenta de lote, con la configuración de suscripción de usuario hello, en una región que admite NC las máquinas virtuales.
5. Utilizando las API de lote de Hola o portal de Azure, cree un grupo con una imagen personalizada hello y con hello número deseado de nodos y la escala. Hello tabla siguiente muestran valores de grupo de ejemplo para la imagen de hello:

| Configuración | Valor |
| ---- | ---- |
| **Tipo de imagen** | Imagen personalizada |
| **Imagen personalizada** | URI del formulario de saludo de la imagen`https://yourstorageaccountdisks.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd` |
| **SKU de agente del nodo** | batch.node.ubuntu 16.04 |
| **Tamaño del nodo** | Estándar NC6 |



## <a name="next-steps"></a>Pasos siguientes

* trabajos MPI de toorun en un grupo de lote de Azure, vea hello [Windows](batch-mpi.md) o [Linux](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/) ejemplos.

* Para obtener ejemplos de las cargas de trabajo GPU en lote, vea hello [lote astilleros](https://github.com/Azure/batch-shipyard/) recetas.
