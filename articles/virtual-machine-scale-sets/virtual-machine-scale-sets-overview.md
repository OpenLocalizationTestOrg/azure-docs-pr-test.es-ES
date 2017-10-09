---
title: "información general sobre conjuntos de escalas de máquina virtual aaaAzure | Documentos de Microsoft"
description: "Más información sobre los conjuntos de escalado de máquinas virtuales de Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 788b2d1636e0bf4ef3fbf94aed9b3303c5fafa82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-virtual-machine-scale-sets-in-azure"></a>¿Qué son los conjuntos de escalado de máquinas virtuales en Azure?
Conjuntos de escalas de máquina virtual son un recurso de proceso de Azure que puede usar toodeploy y administrar un conjunto de máquinas virtuales idénticos. Con todas las máquinas virtuales configuradas Hola igual, conjuntos de escalas son Autoescala true toosupport diseñada y ningún previamente el aprovisionamiento de máquinas virtuales se requiere. Por lo que resulta más fácil de servicios a gran escala toobuild que tienen como destino de proceso intensivo, grandes cantidades de datos y las cargas de trabajo en contenedores.

Para las aplicaciones que necesitan recursos de proceso tooscale out y en escala de las operaciones están equilibradas implícitamente a través de dominios de error y actualización. Para, se establece un tooscale introducción adicional, consulte toohello [anuncio del blog de Azure](https://azure.microsoft.com/blog/azure-virtual-machine-scale-sets-ga/).

Para más información acerca de los conjuntos de escalado, vea estos vídeos:

* [Mark Russinovich talks Azure Scale Sets](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/) (Mark Russinovich habla sobre los conjuntos de escalado de Azure)  
* [Virtual Machine Scale Sets with Guy Bowerman](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

## <a name="creating-and-managing-scale-sets"></a>Creación y administración de conjuntos de escalado
Puede crear una escala establecida en hello [portal de Azure](https://portal.azure.com) seleccionando **nueva** y escribiendo **escala** en la barra de búsqueda de Hola. **Conjunto de escalas de máquina virtual** aparece en los resultados de Hola. Desde allí, puede rellene Hola necesario campos toocustomize e implementar el conjunto de escala. También tiene opciones tooset las reglas de escalado automático básica basada en el uso de CPU en el portal de Hola.

Los conjuntos de escalado de máquinas virtuales se pueden definir e implementar mediante plantillas JSON y [API de REST](https://msdn.microsoft.com/library/mt589023.aspx), igual que las máquinas virtuales individuales de Azure Resource Manager. Por tanto, puede utilizar cualquier método de implementación estándar de Azure Resource Manager. Para más información sobre las plantillas, consulte [Creación de plantillas del Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).

Puede encontrar un conjunto de plantillas de ejemplo para la escala de la máquina virtual se establece en hello [repositorio de GitHub de plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates). (Busque las plantillas con **vmss** en el título de Hola.)

Para obtener ejemplos de plantilla de inicio rápido de hello, un botón "Implementar tooAzure" archivo Léame de Hola para cada plantilla vincula toohello característica de implementación del portal. escala de hello toodeploy establecer, haga clic en el botón de hello y, a continuación, rellene los parámetros que son necesarios en el portal de Hola. 

## <a name="scaling-a-scale-set-out-and-in"></a>Escalado y reducción verticales de un conjunto de escalado
Puede cambiar la capacidad de Hola de una escala establecida en hello portal de Azure, haga clic en hello **ajuste de escala en** sección bajo **configuración**. 

escala de toochange establece capacidad en línea de comandos de hello, use hello **escala** comando [CLI de Azure](https://github.com/Azure/azure-cli). Por ejemplo, use este tooset comando una capacidad de tooa del conjunto de escala de 10 máquinas virtuales:

```bash
az vmss scale -g resourcegroupname -n scalesetname --new-capacity 10 
```

número de hello tooset de máquinas virtuales en una escala de establecer mediante PowerShell, use hello **AzureRmVmss actualización** comando:

```PowerShell
$vmss = Get-AzureRmVmss -ResourceGroupName resourcegroupname -VMScaleSetName scalesetname  
$vmss.Sku.Capacity = 10
Update-AzureRmVmss -ResourceGroupName resourcegroupname -Name scalesetname -VirtualMachineScaleSet $vmss
```

tooincrease o disminuir el número de Hola de máquinas virtuales en una escala de establecer mediante una plantilla de Azure Resource Manager, cambiar hello **capacidad** propiedad y volver a implementar la plantilla de Hola. Esta simplicidad la convierte en conjuntos de escalas de toointegrate fácil con escalado automático de Azure o toowrite que su propia capa de escala personalizado si necesita toodefine eventos de escala personalizada que Azure el escalado automático no admite. 

Si está volviendo a implementar una capacidad de hello Azure Resource Manager toochange de plantilla, puede definir una plantilla mucho más pequeña que incluye solo hello **SKU** paquetes de propiedad con hello actualizan capacidad. [Este es un ejemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing).

## <a name="autoscale"></a>Autoscale

Un conjunto de escala se puede configurar opcionalmente con la configuración de escalado automático cuando se crea en Hola portal de Azure. número de Hola de máquinas virtuales, a continuación, se puede aumentar o disminuir según el uso de CPU promedio. 

Muchas de Hola escalan las plantillas de conjunto de hello [plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates) definir la configuración de escalado automático. También puede agregar tooan de configuración de escalado automático existente conjunto de escala. Por ejemplo, esta secuencia de comandos de PowerShell de Azure agrega el conjunto de escalas de escalado automático basado en CPU tooa:

```PowerShell

$subid = "yoursubscriptionid"
$rgname = "yourresourcegroup"
$vmssname = "yourscalesetname"
$location = "yourlocation" # e.g. southcentralus

$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:05:00 -ScaleActionCooldown 00:05:00 -ScaleActionDirection Increase -ScaleActionValue 1
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -Operator LessThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:05:00 -ScaleActionCooldown 00:05:00 -ScaleActionDirection Decrease -ScaleActionValue 1
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "autoprofile1"
Add-AzureRmAutoscaleSetting -Location $location -Name "autosetting1" -ResourceGroup $rgname -TargetResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -AutoscaleProfiles $profile1
```

Puede encontrar una lista de métricas válido tooscale en [métricas con el Monitor de Azure admitidas](../monitoring-and-diagnostics/monitoring-supported-metrics.md) en hello encabezado "Microsoft.Compute/virtualMachineScaleSets." Opciones más avanzadas de escalado automático también están disponibles, incluido el escalado automático basado en programación y uso webhooks toointegrate con los sistemas de alerta.

## <a name="monitoring-your-scale-set"></a>Supervisión del conjunto de escalado
Hola [portal de Azure](https://portal.azure.com) listas escala establece y muestra sus propiedades. portal de Hello también admite las operaciones de administración. Se pueden realizar operaciones de administración tanto en conjuntos de escalado como en máquinas virtuales individuales de un conjunto de escalado. portal de Hello también proporciona un gráfico de uso de recursos personalizable. 

Si necesita toosee o editar Hola subyacente definición JSON de un recurso de Azure, también puede usar [Explorador de recursos de Azure](https://resources.azure.com). Conjuntos de escalas son un recurso en el proveedor de recursos de Microsoft.Compute Azure Hola. Desde este sitio, puede ver expandiendo Hola siguientes vínculos:

**Suscripciones** > **su suscripción** > **resourceGroups** > **proveedores** > **Microsoft.Compute** > **virtualMachineScaleSets** > **su conjunto de escalado** &gt; etc.

## <a name="scale-set-scenarios"></a>Escenarios de conjuntos de escalado
En esta sección se enumeran algunos escenarios típicos de conjuntos de escalado. Algunos servicios de alto nivel de Azure (como Batch, Service Fabric y Container Service) usan estos escenarios.

* **Usar RDP o SSH tooconnect tooscale establece instancias**: un conjunto de escala se crea dentro de una red virtual y máquinas virtuales individuales en el conjunto de escalas de hello no se asignan direcciones IP públicas de forma predeterminada. Esta directiva evita los gastos de Hola y sobrecarga de administración de IP pública independiente de asignar direcciones tooall nodos de hello en la cuadrícula de proceso. Si es necesario dirigir las conexiones externas tooscale establece las máquinas virtuales, puede configurar una escala conjunto tooautomatically asignar pública IP direcciones toonew máquinas virtuales. O bien puede conectarse tooVMs de otros recursos de la red virtual que se pueden asignar direcciones IP públicas, por ejemplo, equilibradores de carga y las máquinas virtuales independientes. 
* **Conectar tooVMs mediante las reglas NAT**: puede crear una dirección IP pública, asignar tooa equilibrador de carga y definir un grupo NAT de entrada. Estas acciones asignan puertos en el puerto de tooa de dirección IP de hello en una máquina virtual en el conjunto de escalas de Hola. Por ejemplo:
  
  | Origen | Puerto de origen | Destino | Puerto de destino |
  | --- | --- | --- | --- |
  |  Dirección IP pública |Puerto 50000 |vmss\_0 |Puerto 22 |
  |  Dirección IP pública |Puerto 50001 |vmss\_1 |Puerto 22 |
  |  Dirección IP pública |Puerto 50002 |vmss\_2 |Puerto 22 |
  
   En [en este ejemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-linux-nat), NAT reglas están definida tooenable una tooevery de conexión de SSH VM en un conjunto de escala, mediante el uso de una dirección IP pública única de las direcciones.
  
   [En este ejemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-nat) Hola igual con RDP y Windows.
* **Conectar tooVMs mediante un "jumpbox"**: si crea un conjunto de escala y una máquina virtual independiente en hello mismo virtual de red, hello independiente hello y VM conjunto de escalas de máquina virtual pueda conectar tooone otra mediante su dirección IP interna direcciones, tal como se define por hello virtual red o subred. Si crea una dirección IP pública y asignar toohello independiente VM, puede usar RDP o SSH tooconnect toohello VM independiente. A continuación, puede conectarse desde que escala de máquinas tooyour establecido instancias. En este punto, ya se habrá percatado de que un simple conjunto de escalado es, por naturaleza, más seguro que una simple máquina virtual independiente con una dirección IP pública en su configuración predeterminada.
  
   Por ejemplo, en [esta plantilla](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-linux-jumpbox) se implementa un conjunto de escalado simple con una máquina virtual independiente. 
* **Instancias de conjunto de tooscale de equilibrio de carga**: si desea clúster de cálculo tooa toodeliver de trabajo de máquinas virtuales mediante el uso de un enfoque de round robin, puede configurar un equilibrador de carga de Azure con las reglas de equilibrio de carga de nivel 4 en consecuencia. Puede definir sondeos tooverify que la aplicación se ejecuta al hacer ping en los puertos con un protocolo especificado, el intervalo y la ruta de acceso de solicitud. [Azure Application Gateway](https://azure.microsoft.com/services/application-gateway/) también admite conjuntos de escalado, junto con escenarios de equilibrio de carga de nivel 7, y más sofisticados.
  
   [En este ejemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-ubuntu-web-ssl) crea un conjunto de escala que se ejecuta en servidores web Apache y utiliza una carga de Hola de toobalance de equilibrador de carga que recibe de cada máquina virtual. (Busque en el tipo de recurso de hello Microsoft.Network/loadBalancers y networkProfile y extensionProfile en virtualMachineScaleSet).

   En [este ejemplo de Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-ubuntu-app-gateway) y en [este ejemplo de Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-app-gateway) se usa Application Gateway.  

* **Implementación de un conjunto de escalado como clúster de proceso en un administrador de clústeres PaaS**: los conjuntos de escalado a veces se describen como un rol de trabajo de última generación. Aunque una descripción válida, corre Hola riesgo de escala confuso conjunto de características con las características de servicios de nube de Azure. Hasta cierto punto, los conjuntos de escalado proporcionan unos verdaderos rol de trabajo o recurso de trabajo. Son un recurso de proceso generalizado que no depende de la plataforma ni del runtime, se puede personalizar y se integra en el IaaS de Azure Resource Manager.
  
   Los roles de trabajo de Cloud Services están limitados en lo que respecta a la compatibilidad con plataformas o runtimes (solo imágenes de plataformas de Windows). Pero también incluye servicios como el intercambio de VIP, la configuración de las opciones de actualización y la configuración específica de la implementación de runtimes o aplicaciones. Estos servicios *aún* no están disponibles en los conjuntos de escalado, o los prestan otros servicios de PaaS de alto nivel como Azure Service Fabric. Puede ver los conjuntos de escalado como una infraestructura que admite PaaS. Las soluciones de PaaS, como [Service Fabric](https://azure.microsoft.com/services/service-fabric/), se basan en esta infraestructura.
  
   En [este ejemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos) de este enfoque, [Azure Container Service](https://azure.microsoft.com/services/container-service/) implementa un clúster basado en conjuntos de escalado con un orquestador del contenedor.

## <a name="scale-set-performance-and-scale-guidance"></a>Guía de escalado y rendimiento del conjunto de escalado
* Una escala conjunto admite seguridad too1, 000 máquinas virtuales. Si crea y cargar sus propias imágenes de máquina virtual personalizadas, el límite de hello es 100. Para ver todo lo que se debe saber al usar conjuntos de escalado grandes, consulte [Uso de grandes conjuntos de escalado de máquinas virtuales](virtual-machine-scale-sets-placement-groups.md).
* No es necesario toopre-crear conjuntos de escalas de toouse de cuentas de almacenamiento de Azure. Compatibilidad con conjuntos de escala Azure administra discos, que negar los problemas de rendimiento sobre el número de Hola de discos por cuenta de almacenamiento. Para más información, consulte [Conjuntos de escalado de máquinas virtuales y discos administrados](virtual-machine-scale-sets-managed-disks.md).
* Considere la posibilidad de usar Azure Premium Storage, en lugar de Azure Storage, para lograr unos tiempos de aprovisionamiento de máquinas virtuales menores y más predecibles, y mejorar el rendimiento de E/S.
* cuota de núcleos de Hello en la región de hello en el que se va a implementar limita el número de Hola de máquinas virtuales que se puede crear. Tendrá que tooincrease de soporte al cliente de toocontact el límite de cuota de proceso, incluso si tiene un límite más alto de núcleos para su uso con los servicios de nube de Azure hoy en día. tooquery la cuota, ejecute este comando de CLI de Azure: `azure vm list-usage`. O bien, ejecute este comando de PowerShell: `Get-AzureRmVMUsage`.

## <a name="frequently-asked-questions-for-scale-sets"></a>Preguntas más frecuentes acerca de los conjuntos de escalado
**P.** ¿Cuántas máquinas virtuales puede contener un conjunto de escalado?

**R.** Un conjunto de escala puede tener 0 too1, 000 máquinas virtuales basadas en imágenes de plataforma o 0 too100 máquinas virtuales basadas en imágenes personalizadas. 

**P.** ¿Se admiten discos de datos en los conjuntos de escalado?

**R.** Sí. Un conjunto de escala puede definir una configuración de discos de datos adjuntos que se aplica tooall las máquinas virtuales en el conjunto de Hola. Para más información, consulte [Conjuntos de escalado de máquinas virtuales de Azure y discos de datos conectados](virtual-machine-scale-sets-attached-disks.md). Otras opciones para almacenar datos son las siguientes:

* Archivos de Azure (unidades compartidas SMB)
* Unidad de sistema operativo
* Unidad temporal (local, sin el respaldo de Azure Storage)
* Servicio de datos de Azure (por ejemplo, tablas y blobs de Azure)
* Servicio de datos externos (por ejemplo, una base de datos remota)

**P.** ¿Qué regiones de Azure admiten conjuntos de escalado?

**R.** Todas las regiones admiten conjuntos de escalado.

**P.** ¿Cómo se crea un conjunto de escalado con una imagen personalizada?

**R.** Cree un disco administrado basado en el VHD de su imagen personalizada y cree una referencia a él en la plantilla del conjunto de escalado. [Este es un ejemplo](https://github.com/chagarw/MDPP/tree/master/101-vmss-custom-os).

**P.** ¿Si reducir mi escala de establece la capacidad del too15 20, que se quitan las máquinas virtuales?

**R.** Máquinas virtuales se quitan de la escala de hello conjunto uniformemente entre los dominios de actualización y la disponibilidad de toomaximize de dominios de error. Máquinas virtuales con hello que primero se quitan los identificadores de más alto.

**P.** ¿Qué ocurre si, a continuación, aumentar la capacidad de Hola de 15 too18?

**R.** Si se aumenta la capacidad too18, se crean 3 nuevas máquinas virtuales. Cada vez, Id. de instancia VM de Hola se incrementa de hello anterior valor más alto (por ejemplo, 20, 21, 22). Las máquinas virtuales están equilibradas entre los dominios de error y los dominios de actualización.

**P.** Si se usan varias extensiones en un conjunto de escalado, ¿se puede exigir una secuencia de ejecución?

**R.** No directamente, pero para la extensión customScript de hello, el script puede esperar a que otro toofinish de extensión. Para obtener orientación adicional en la secuenciación de extensión en la entrada de blog de Hola [secuenciación de extensión en conjuntos de escalas de VM de Azure](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).

**P.** ¿Funcionan los conjuntos de escalado con los conjuntos de disponibilidad de Azure?

**R.** Sí. Un conjunto de escalado es un conjunto de disponibilidad implícita con 5 dominios de error y 5 dominios de actualización. Escala conjuntos de más de 100 máquinas virtuales que abarquen varias *grupos de selección de ubicación*, que son conjuntos de disponibilidad toomultiple equivalente. Para más información, consulte [Uso de grandes conjuntos de escalado de máquinas virtuales](virtual-machine-scale-sets-placement-groups.md). Un conjunto de disponibilidad de las máquinas virtuales puede existir en hello misma red virtual como un conjunto de escala de máquinas virtuales. Una configuración común es tooput control máquinas virtuales de nodos (que a menudo requieren configuración única) en la disponibilidad de un conjunto y colocan nodos de datos en el conjunto de escalas de Hola.

Puede encontrar más tooquestions respuestas sobre la escala se establece en hello [escala de la máquina virtual de Azure establece preguntas más frecuentes sobre](virtual-machine-scale-sets-faq.md).
