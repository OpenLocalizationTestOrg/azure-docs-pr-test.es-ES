---
title: "los grupos de Azure Batch aaaProvision de imágenes personalizadas | Documentos de Microsoft"
description: "Puede crear un lote de proceso de grupo desde una imagen personalizada tooprovision nodos que contienen software hello y los datos que necesita para la aplicación. Imágenes personalizadas son una manera eficaz las cargas de trabajo por lotes de tooconfigure proceso toorun de nodos."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/07/2017
ms.author: tamram
ms.openlocfilehash: 5cb698ee90f7d3ec9ffe69fa4dc602132c3f7569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-custom-image-toocreate-a-pool-of-virtual-machines"></a>Usar un toocreate de imagen personalizada un grupo de máquinas virtuales

Cuando se crea un grupo de máquinas virtuales en Azure Batch, especifique una imagen de máquina virtual (VM) que proporciona el sistema operativo de Hola para cada nodo de proceso en el grupo de Hola. Es posible crear un grupo de máquinas virtuales ya sea con una imagen de Azure Marketplace o si se proporciona una imagen de VHD personalizada que se haya preparado. Al proporcionar una imagen personalizada, tiene control sobre la configuración del sistema operativo de hello en tiempo de Hola que está aprovisionado por cada nodo de ejecución. La imagen personalizada puede incluir aplicaciones así como nodo de ejecución de datos de referencia que están disponibles en hello en cuanto se aprovisiona.

Uso de una imagen personalizada puede ahorrarle tiempo para la obtención de nodos de proceso de la agrupación listo toorun la carga de trabajo por lotes. Aunque siempre puede utilizar una imagen de Azure Marketplace e instalar el software en cada nodo de proceso una vez que se haya aprovisionado, este enfoque puede ser menos eficiente que usar una imagen personalizada. 

Algunas razones toouse una imagen personalizada que se configura para su escenario incluyen la necesidad de:

- **Configurar el sistema operativo de hello (SO)** se puede realizar ninguna configuración especial del sistema operativo de hello en imagen personalizada de Hola. 
- **Instalar aplicaciones de gran tamaño.** Instalar aplicaciones en una imagen personalizada es más eficaz que instalarlas en cada nodo de ejecución una vez que se aprovisiona.
- **Copiar cantidades importantes de datos.** Si los datos de hello toohello copiada de imagen personalizada, solo necesita toobe copiado una vez, en lugar de nodo de proceso tooeach, permite ahorrar tiempo y ancho de banda.
- **Reinicie Hola VM durante el proceso de instalación de Hola.** Hola reiniciándose VM puede ser un proceso lento, especialmente si tiene un número de nodos de proceso.

## <a name="prerequisites"></a>Requisitos previos

- **Una cuenta de lote creada con el modo de asignación de grupo de suscripción de usuario de Hola.** toouse un grupos de máquina Virtual de tooprovision de imagen personalizada, crear su cuenta de lote con hello suscripción usuario [modo de asignación de grupo](batch-api-basics.md#pool-allocation-mode). Con este modo, se asignan a grupos de proceso por lotes en una suscripción de Hola donde reside la cuenta de hello. Vea hello [cuenta](batch-api-basics.md#account) sección [paralelas a gran escala de desarrollar soluciones con el lote de proceso](batch-api-basics.md) para obtener información acerca de cómo establecer el modo de asignación de grupo de hello cuando se crea una cuenta de lote.

- **Una cuenta de Azure Storage.** toocreate un grupo de máquinas virtuales mediante una imagen personalizada, se necesita una cuenta de almacenamiento de Azure estándar, de propósito general en hello misma suscripción y región. Si crea una imagen personalizada de una VM de Azure, se copiará cuenta de almacenamiento de toohello de hello imagen donde reside el disco del sistema operativo de la máquina virtual de hello y no necesitará toocreate una cuenta de almacenamiento independiente. 
    
## <a name="prepare-a-custom-image"></a>Preparación de una imagen personalizada

tooprepare una imagen personalizada para su uso con el lote, debe generalizar una instalación existente de Linux o Windows. Al generalizar una instalación de sistema operativo, quita la información específica de la máquina. resultado de Hello es una imagen que se puede instalar en otros equipos o máquinas virtuales.  

> [!IMPORTANT]
> Proceso por lotes no admite actualmente el uso de Azure administrados tooprovision un grupo de imágenes. imagen personalizada Hello utilizarás tooprovision que un grupo debe almacenarse en el almacenamiento de Azure. 
>
> Al preparar la imagen personalizada, tenga en Hola de cuenta siguientes puntos:
> - Asegurarse de esa imagen del sistema operativo base Hola usar tooprovision las agrupaciones de lote no se cualquiera previamente instalado las extensiones de Azure, como la extensión de Script personalizado de Hola. Si la imagen de hello contiene una extensión previamente instalada, Azure puede encontrar problemas implementar Hola máquina virtual.
> - Asegúrese de que esa imagen del sistema operativo base Hola que proporcionan usa Hola unidad temporal de forma predeterminada, tal y como hello agente de nodo de lote actualmente espera como unidad temporal predeterminada Hola.
>
>

Puede usar cualquier imagen preparada de Windows o Linux existente como imagen personalizada. Por ejemplo, si desea toouse una imagen local, cargar la cuenta de almacenamiento de Azure de tooan de imagen de Hola que se encuentra en Hola misma suscripción y región que la cuenta de proceso por lotes mediante [AzCopy](../storage/storage-use-azcopy.md) u otra herramienta de carga.

También puede preparar una imagen personalizada a partir de una máquina virtual de Azure nueva o existente. Si va a crear una nueva máquina virtual, puede utilizar una imagen de Azure Marketplace como imagen base hello para la imagen personalizada y, a continuación, personalizarlo. imagen base de toocustomize hello, crear una máquina virtual de Azure y agregue sus aplicaciones o datos tooit. A continuación, generalizar Hola VM tooserve como la imagen personalizada y guárdelo tooAzure almacenamiento. 

tooprepare una imagen personalizada desde una máquina virtual de Azure, siga estos pasos:

1. Cree una máquina virtual de Azure **no administrada** a partir de una imagen de Azure Marketplace. Azure Marketplace incluye imágenes para [Windows](../virtual-machines/windows/quick-create-portal.md) y [Linux](../virtual-machines/linux/quick-create-portal.md).
    
    En paso 3 de hello proceso de creación de la máquina virtual, asegúrese de que selecciona **No** para **almacenamiento: utilizar discos administrados** opción. También tome nota del nombre de cuenta de almacenamiento de hello para el disco del sistema operativo de la máquina virtual de hello, tal y como esta cuenta de almacenamiento también es donde Azure guardará la imagen personalizada:

    ![Crear una VM no administrado y el nombre de la cuenta de almacenamiento de nota Hola](media/batch-custom-images/vm-create-storage.png)
 
2. Completar el proceso de Hola de creación de la máquina virtual y espere toobe asignada por Azure. Aquí es una imagen que muestra una máquina virtual en el portal de Azure en estado de ejecución de Hola Hola:

    ![Creación de una máquina virtual a partir de una imagen de Marketplace](media/batch-custom-images/vm-status-running.png)

3. Una vez Hola máquina virtual se está ejecutando, conéctese tooit a través de RDP (para Windows) o SSH (para Linux). Instalar el software necesario o copiar los datos que desee y, a continuación, generalizar Hola máquina virtual. Siga los pasos de hello descritos en [generalizar Hola VM](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sa-copy-generalized.md#generalize-the-vm). 
   
4. Siga los pasos de hello demasiado[sesión tooAzure PowerShell](../virtual-machines/windows/sa-copy-generalized.md#log-in-to-azure-powershell). tooinstall PowerShell de Azure, consulte [información general de Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.2.0). 

5. A continuación, siga los pasos de hello demasiado[Deallocate Hola VM y el conjunto Hola estado toogeneralized](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sa-copy-generalized#deallocate-the-vm-and-set-the-state-to-generalized). 

    Hola portal de Azure, tenga en cuenta que Hola que se cancela la asignación de máquina virtual:

    ![Asegúrese de que Hola que se cancela la asignación de máquina virtual](media/batch-custom-images/vm-status-deallocated.png)

6.  Crear y guardar tooAzure de imagen de máquina virtual de hello almacenamiento con hello [AzureRmVMImage guardar](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) cmdlet de PowerShell. Siga las instrucciones de hello descritas en [crear imagen de hello](../virtual-machines/windows/sa-copy-generalized.md#create-the-image).
    
    imagen de máquina virtual de Hola se guarda la cuenta de almacenamiento de Azure toohello creado al Hola VM, como se muestra en el paso 1 de este procedimiento. Hola AzureRmVMImage guardar cmdlet guarda Hola imagen toohello **system** contenedor en esa cuenta de almacenamiento. Hola `-DestinationContainername` parámetro designa un directorio virtual dentro de hello **system** contenedor. Hola `-VHDNamePrefix` parámetro especifica un prefijo de nombre de blob de Hola. Este prefijo es el nombre del blob toohello antepuesto con un guión. 

    Por ejemplo, supongamos que se llama AzureRmVMImage guardar con hello parámetros siguientes:  

        Save-AzureRmVMImage -ResourceGroupName sample-resource-group -Name vm-custom-image -DestinationContainerName batchimages -VHDNamePrefix custom -Path C:\Temp\Images\vm-custom-image.json

    se guarda la imagen resultante Hello toohello ubicación y nombre de blob que se muestra aquí:

    ![Ubicación del VHD guardado en el contenedor de sistema](media/batch-custom-images/vhd-in-vm-storage-account.png)

    > [!NOTE]
    > Una máquina virtual no administrada de Azure crea varias cuentas de almacenamiento para distintos usos. Si no anotó nombre Hola Hola del contenedor de almacenamiento para el disco de SO de hello cuando hello se creó la máquina virtual, buscar almacenamiento Hola asociado de cuenta que contiene Hola **system** contenedor. Navegar por hello **system** imagen de personalizado contenedor toofind Hola con valores de hello especificados para hello **AzureRmVMImage guardar** comando.

## <a name="create-a-pool-from-a-custom-image-in-hello-portal"></a>Crear un grupo de una imagen personalizada en el portal de Hola

Una vez que guarde la imagen personalizada y conozca la ubicación, puede crear un grupo de Batch a partir de esa imagen. Siga estos toocreate un grupo de pasos de hello portal de Azure:

1. Navegar por cuenta de lote tooyour Hola portal de Azure. Esta cuenta debe ser en hello misma suscripción y región como almacenamiento de Hola de imagen personalizada de Hola que contiene la cuenta. 
2. Hola **configuración** ventana en hello izquierdo, seleccione hello **grupos** elemento de menú.
3. Hola **grupos** (ventana), seleccione hello **agregar** comando.
4. En hello **Agregar grupo** ventana, seleccione **imagen personalizada (Linux y Windows)** de hello **tipo de imagen** lista desplegable. portal de Hello muestra hello **imagen personalizada** selector. Navegue toohello cuenta de almacenamiento donde se encuentra la imagen personalizada y seleccione Hola VHD deseado del contenedor de Hola. 
5. Seleccione Hola correcto **Publisher/oferta/Sku** para el disco duro virtual personalizado.
6. Especificar Hola restantes requiere configuración, incluidos hello **tamaño de nodo**, **dedicados nodos de destino**, y **bajo los nodos de prioridad**, así como cualquier deseado configuraciones opcionales.

    Por ejemplo, para una imagen personalizada del centro de datos de Microsoft Windows Server 2016, Hola **Agregar grupo** ventana aparece como se muestra aquí:

    ![Agregar grupo desde imagen personalizada de Windows](media/batch-custom-images/add-pool-custom-image.png)
  
toocheck si un grupo existente se basa en una imagen personalizada, vea hello **sistema operativo** propiedad en la sección de resumen de recursos de Hola de hello **grupo** ventana. Si se ha creado el grupo de Hola desde una imagen personalizada, se establece demasiado**imagen de VM personalizada**.

Todos los VHD personalizados asociados a un grupo se muestran en el grupo de hello **propiedades** ventana.
 
## <a name="next-steps"></a>Pasos siguientes

- Para información general más detallada acerca de Batch, consulte [Desarrollo de soluciones de procesos paralelos a gran escala con Batch](batch-api-basics.md).
- Para obtener información acerca de cómo crear una cuenta de lote, consulte [crear una cuenta de lote con hello portal de Azure](batch-account-create-portal.md).
