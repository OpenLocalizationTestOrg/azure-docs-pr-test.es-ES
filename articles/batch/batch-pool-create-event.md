---
title: "aaa \"eventos de creación de grupo de lote de Azure | Documentos de Microsoft\""
description: "Referencia del evento de creación de grupo de Batch."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: ad31251969af553baa21e8c533d8ea95d3eeaf91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="pool-create-event"></a>Evento de creación del grupo

 Este evento se genera cuando se ha creado un grupo. contenido de Hola de registro de hello expondrá información general sobre el grupo de Hola. Tenga en cuenta que si el tamaño de destino de Hola de agrupación de hello es mayor que 0 nodos de proceso, un evento de inicio de cambio de tamaño de grupo seguirá inmediatamente después de este evento.

 Hello en el ejemplo siguiente se muestra cuerpo Hola de un grupo de creación de eventos para un grupo creado mediante hello CloudServiceConfiguration propiedad.

```
{
    "id": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "3",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicated": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoScale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

|Elemento|Tipo|Notas|
|-------------|----------|-----------|
|id|String|Hola Id. de grupo de Hola.|
|DisplayName|String|Hola nombre para mostrar del grupo de Hola.|
|vmSize|String|tamaño de Hola de hello máquinas virtuales de hello grupo. Todas las máquinas virtuales en un grupo son Hola mismo tamaño. <br/><br/> Para obtener información sobre los tamaños disponibles de máquinas virtuales para los grupos de Cloud Services (grupos creados con cloudServiceConfiguration), consulte [Tamaños para Cloud Services](http://azure.microsoft.com/documentation/articles/cloud-services-sizes-specs/). Batch admite todas las VM de Cloud Services excepto `ExtraSmall`.<br/><br/> Para obtener información acerca de la máquina virtual disponible vea tamaños para grupos con imágenes de hello Marketplace de máquinas virtuales (grupos creados con virtualMachineConfiguration) [tamaños de máquinas virtuales](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-sizes/) (Linux) o [tamaños para Máquinas virtuales](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) (Windows). Batch admite todos los tamaños de máquina virtual de Azure excepto `STANDARD_A0` y aquellos con Premium Storage (series `STANDARD_GS`, `STANDARD_DS` y `STANDARD_DSV2`).|
|[cloudServiceConfiguration](#bk_csconf)|Tipo complejo|configuración del servicio de nube de Hello para el grupo de Hola.|
|[virtualMachineConfiguration](#bk_vmconf)|Tipo complejo|configuración de máquina virtual de Hello para el grupo de Hola.|
|[networkConfiguration](#bk_netconf)|Tipo complejo|configuración de red de Hello para el grupo de Hola.|
|resizeTimeout|Hora|tiempo de espera de Hello para la asignación de grupo de toohello de nodos de proceso especificado para la última operación de cambio de tamaño hello en el grupo de Hola.  (Hola inicial cuando se crea recuentos a grupo de Hola como un cambio de tamaño de ajuste de tamaño).|
|targetDedicated|Int32|número de Hola de nodos de proceso que se solicitan para el grupo de Hola.|
|enableAutoScale|Booleano|Especifica si el tamaño del grupo de hello ajusta automáticamente con el tiempo.|
|enableInterNodeCommunication|Booleano|Especifica si el grupo de hello está configurado para la comunicación directa entre los nodos.|
|isAutoPool|Booleano|Especifica si se creó el grupo de Hola a través del mecanismo de grupo de un trabajo.|
|maxTasksPerNode|Int32|número máximo de Hola de tareas que pueden ejecutarse simultáneamente en un nodo de proceso único en el grupo de Hola.|
|vmFillType|String|Define cómo Hola servicio por lotes distribuye las tareas entre los nodos de cálculo de grupo de Hola. Los valores válidos son Spread o Pack.|

###  <a name="bk_csconf"></a> cloudServiceConfiguration

|Nombre del elemento|Tipo|Notas|
|------------------|----------|-----------|
|osFamily|String|Hola SO invitado de Azure familia toobe instalada en máquinas virtuales de hello en el grupo de Hola.<br /><br /> Los valores posibles son:<br /><br /> **2** – 2 de familia de SO, equivalente tooWindows Server 2008 R2 SP1.<br /><br /> **3** : familia 3 del SO, equivalente tooWindows Server 2012.<br /><br /> **4** – 4 de familia de SO, equivalente tooWindows Server 2012 R2.<br /><br /> Para obtener más información, consulte [Versiones del SO invitado de Azure](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases).|
|targetOSVersion|String|toobe de versión de SO invitado de Azure de Hello instalada en máquinas virtuales de hello en el grupo de Hola.<br /><br /> es el valor predeterminado de Hello  **\***  que especifica la versión de sistema operativo más reciente de Hola para hello especifica la familia.<br /><br /> Para otros valores permitidos, consulte [Versiones del SO invitado de Azure](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases).|

###  <a name="bk_vmconf"></a> virtualMachineConfiguration

|Nombre del elemento|Tipo|Notas|
|------------------|----------|-----------|
|[imageReference](#bk_imgref)|Tipo complejo|Especifica información acerca de la plataforma de Hola o toouse de imagen de Marketplace.|
|nodeAgentSKUId|String|Hola SKU de agente de nodo de lote Hola aprovisionado en el nodo de proceso de Hola.|
|[windowsConfiguration](#bk_winconf)|Tipo complejo|Especifica la configuración de sistema operativo de Windows en la máquina virtual de Hola. Esta propiedad no se debe especificar si hello imageReference hace referencia a una imagen de sistema operativo Linux.|

###  <a name="bk_imgref"></a> imageReference

|Nombre del elemento|Tipo|Notas|
|------------------|----------|-----------|
|publisher|String|publicador de Hola de imagen de Hola.|
|offer|String|oferta de Hola de imagen de Hola.|
|sku|String|Hola SKU de imagen de Hola.|
|versión|String|versión de Hola de imagen de Hola.|

###  <a name="bk_winconf"></a> windowsConfiguration

|Nombre del elemento|Tipo|Notas|
|------------------|----------|-----------|
|enableAutomaticUpdates|Booleano|Indica si la máquina virtual de Hola está habilitada para las actualizaciones automáticas. Si no se especifica esta propiedad, el valor predeterminado de hello es true.|

###  <a name="bk_netconf"></a> networkConfiguration

|Nombre del elemento|Tipo|Notas|
|------------------|--------------|----------|
|subnetId|String|Especifica el identificador de recurso de Hola de subred de hello en el proceso del grupo de qué Hola se crean nodos.|
