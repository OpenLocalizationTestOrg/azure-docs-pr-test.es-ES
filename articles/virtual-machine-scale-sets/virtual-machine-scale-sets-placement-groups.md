---
title: "aaaWorking con grandes conjuntos de escalas de máquina Virtual de Azure | Documentos de Microsoft"
description: "Lo que necesita tooknow toouse grandes máquina virtual de Azure escalar conjuntos"
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
ms.date: 2/7/2017
ms.author: guybo
ms.openlocfilehash: a39aab25925d7fc50763f0a20148b1f2213b492f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-large-virtual-machine-scale-sets"></a>Uso de grandes conjuntos de escalado de máquinas virtuales
Ahora puede crear Azure [conjuntos de escalas de máquina virtual](/azure/virtual-machine-scale-sets/) con una capacidad de seguridad too1, 000 máquinas virtuales. En este documento, un _conjunto de escalas de máquina virtual grande_ se define como una escala establecida capaz de escalar toogreater de 100 máquinas virtuales. Esta funcionalidad se establece con una propiedad de conjunto de escalado (_singlePlacementGroup=False_). 

Conjuntos de determinados aspectos de gran escala, como los dominios de error y equilibrio de carga comportan de manera diferente tooa conjunto de escala estándar. Este documento explica las características de Hola de conjuntos de gran escala y describe lo que necesita tooknow toosuccessfully usarlos en sus aplicaciones. 

Un enfoque común para implementar la infraestructura de nube a gran escala es toocreate un conjunto de _unidades de escala_, por ejemplo mediante la creación de varias máquinas virtuales escalar conjuntos entre varias redes virtuales y las cuentas de almacenamiento. Este enfoque proporciona más fácil toosingle de administración en comparación con las máquinas virtuales y varias unidades de escala son útiles para muchas aplicaciones, especialmente aquellas que requieren otros componentes apilables como varias redes virtuales y los puntos de conexión. Si la aplicación requiere un único clúster de gran tamaño sin embargo, puede ser más sencillo toodeploy configurada una sola escala de too1, 000 máquinas virtuales. Algunos escenarios de ejemplo son las implementaciones de macrodatos centralizadas y las mallas de computación que requieren una administración sencilla de un grupo grande de nodos de trabajo. Combinar con el conjunto de escalas de VM [discos de datos conectados](virtual-machine-scale-sets-attached-disks.md), conjuntos de gran escala permiten toodeploy una infraestructura escalable que consta de miles de núcleos y petabytes de almacenamiento, como una única operación.

## <a name="placement-groups"></a>Grupos de selección de ubicación 
¿En qué consiste un _grandes_ conjunto especial de escalas no es número Hola de máquinas virtuales, pero el número Hola de _grupos de selección de ubicación_ contiene. Un grupo de selección de ubicación es un conjunto de disponibilidad de Azure tooan de construcción similar, con sus propios dominios de error y dominios de actualización. De forma predeterminada, un conjunto de escalado consta de un único grupo de selección de ubicación con un tamaño máximo de 100 máquinas virtuales. Si una escala de establece la propiedad denominada _singlePlacementGroup_ se establece too_false_, conjunto de escalas de hello puede estar compuesto de varios grupos de selección de ubicación y tiene un intervalo de 0 a 1.000 máquinas virtuales. Cuando se establece valor predeterminado de toohello de _true_, un conjunto de escala se compone de un grupo de selección de ubicación única y tiene un intervalo de 0-100 máquinas virtuales.

## <a name="checklist-for-using-large-scale-sets"></a>Lista de comprobación para usar grandes conjuntos de escalado
toodecide si la aplicación puede hacer un uso eficaz de conjuntos de gran escala, considere la posibilidad de hello según los requisitos:

- Los conjuntos de escalado grandes necesitan Azure Managed Disks. Los conjuntos de escalado grandes que no se crean con Managed Disks requieren varias cuentas de almacenamiento (una por cada 20 máquinas virtuales). Los conjuntos de gran escala son toowork diseñada exclusivamente con tooreduce discos administrados limita el riesgo de Hola de sobrecarga de administración y tooavoid de almacenamiento de la ejecución en una suscripción para las cuentas de almacenamiento. Si no utiliza discos administrados, el conjunto de escala es too100 limita las máquinas virtuales.
- Conjuntos de escalas de creado a partir de imágenes de Azure Marketplace pueden escalar too1, 000 máquinas virtuales.
- Conjuntos de escalas de creado a partir de imágenes personalizadas (imágenes de máquina virtual que crea y carga usted mismo) actualmente pueden escalar too100 las máquinas virtuales.
- Capa 4 equilibrio de carga con hello equilibrador de carga de Azure no se admite todavía para conjuntos de escalas de formada por varios grupos de selección de ubicación. Si necesita hello toouse equilibrador de carga de Azure que escala de hello seguro sea es toouse configurado un grupo de selección de ubicación única, que es el valor predeterminado de Hola.
- 7 de la capa de equilibrio de carga con hello puerta de enlace de aplicaciones de Azure es compatible con todos los conjuntos de escala.
- Un conjunto de escala se define con una sola subred, asegúrese de que la subred tiene un espacio de direcciones lo suficientemente grande como para todas las máquinas virtuales de Hola que necesita. De forma predeterminada un conjunto de escalado de overprovisions (crea máquinas virtuales adicionales durante la implementación o mientras se escala horizontalmente, que no se le cobra por) tooimprove implementación confiabilidad y rendimiento. Permitir un mayor número de Hola de máquinas virtuales que piensa tooscale a dirección espacio 20%.
- Si tiene previsto toodeploy muchas máquinas virtuales, sus límites de cuota de núcleos de proceso pueden necesitar toobe aumentado.
- Los dominios de error y los dominios de actualización solo son coherentes dentro de un grupo de selección de ubicación. Esta arquitectura no cambia Hola general conjunto de disponibilidad de una escala, como las máquinas virtuales se distribuyen uniformemente entre distinto hardware físico, pero lo que significa que si necesita tooguarantee dos máquinas virtuales están en un hardware diferente, asegúrese de que están en error diferentes dominios de Hola mismo grupo de selección de ubicación. Identificador de grupo de dominio y la colocación de error se muestran en hello _instancia vista_ de una escala del conjunto de máquina virtual. Puede ver la vista de instancia Hola de un conjunto de escalas de VM en hello [Explorador de recursos de Azure](https://resources.azure.com/).


## <a name="creating-a-large-scale-set"></a>Creación de un conjunto de escalado grande
Cuando se crea una escala establecida en hello portal de Azure, puede permitir que se grupos de selección de ubicación de tooscale toomultiple por establecer hello _grupo único de la selección de ubicación de límite tooa_ too_False_ opción Hola _Fundamentos_ hoja. Con esta too_False_ de conjunto de opción, puede especificar un _el número de instancias_ valor de seguridad too1, 000.

![](./media/virtual-machine-scale-sets-placement-groups/portal-large-scale.png)

Puede crear a gran escala de máquinas virtuales que se establecen a través de hello [CLI de Azure](https://github.com/Azure/azure-cli) _crear az vmss_ comando. Este comando establece valores predeterminados inteligentes como tamaño de la subred en función de hello _recuento de instancias_ argumento:

```bash
az group create -l southcentralus -n biginfra
az vmss create -g biginfra -n bigvmss --image ubuntults --instance-count 1000
```
Tenga en cuenta que hello _vmss crear_ ciertos valores de configuración si no los especifica valores predeterminados de comando. opciones disponibles de toosee Hola que puede invalidar, intente:
```bash
az vmss create --help
```

Si va a crear a gran escala establecer creando una plantilla de Azure Resource Manager, asegúrese de plantilla de hello crea un conjunto de escala basado en discos administrados de Azure. Puede establecer hello _singlePlacementGroup_ too_false_ propiedad Hola _propiedades_ sección de hello _Microsoft.Compute/virtualMAchineScaleSets_ recursos. Hello siguiente fragmento de JSON muestra a partir de una plantilla de conjunto de escala, incluida la capacidad VM de 1.000 Hola y Hola Hola _"singlePlacementGroup": false_ configuración:
```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "location": "australiaeast",
  "name": "bigvmss",
  "sku": {
    "name": "Standard_DS1_v2",
    "tier": "Standard",
    "capacity": 1000
  },
  "properties": {
    "singlePlacementGroup": false,
    "upgradePolicy": {
      "mode": "Automatic"
    }
```
Para obtener un ejemplo completo de a gran escala conjuntos de plantilla, consulte demasiado[https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json](https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json).

## <a name="converting-an-existing-scale-set-toospan-multiple-placement-groups"></a>Convertir una escala existente establece toospan varios grupos de selección de ubicación
toomake una escala VM existente establecida capaz de escalar toomore de 100 máquinas virtuales, deberá hello toochange _singplePlacementGroup_ too_false_ de propiedad en la escala de hello establece el modelo. Puede probar si cambia esta propiedad con hello [Explorador de recursos de Azure](https://resources.azure.com/). Buscar un conjunto de escala existente, seleccione _editar_ y cambiar hello _singlePlacementGroup_ propiedad. Si no ve esta propiedad, puede estar viendo escala Hola establecido con una versión anterior de hello Microsoft.Compute API.

>[!NOTE] 
Puede cambiar una escala establecida de admitir una única ubicación grupo solo (comportamiento predeterminado de hello) tooa admite varios grupos de selección de ubicación, pero no se puede convertir Hola revés. Por lo tanto, asegúrese de que comprende las propiedades de Hola de conjuntos de gran escala antes de convertir. En concreto, asegúrese de que no es necesario con hello equilibrador de carga de Azure de equilibrio de carga de nivel 4.


