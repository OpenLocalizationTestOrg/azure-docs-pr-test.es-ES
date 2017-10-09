---
title: "aaaCreate varias máquinas virtuales | Documentos de Microsoft"
description: "Opciones para la creación varias máquinas virtuales en Windows"
services: virtual-machines-windows
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dfc1d1bb-a47d-4d7c-9fd2-f12050baacab
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: guybo
ms.openlocfilehash: 37729fabd91049744f6bd94c55221f5c1c65d527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-multiple-azure-virtual-machines"></a>Creación de varias máquinas virtuales de Azure
Hay muchos escenarios en los que tenga toocreate un gran número de máquinas virtuales similares (VM). Por ejemplo, la informática de alto rendimiento (HPC), los análisis de datos a gran escala, los servidores back-end o de nivel intermedio escalables y, con frecuencia, sin estado (como servidores web), y las bases de datos distribuidas.

Este artículo describe Hola opciones disponibles toocreate varias máquinas virtuales en Azure. Estas opciones ir más allá de los casos más sencillos hello en los que crea manualmente una serie de máquinas virtuales. toocreate muchas máquinas virtuales, los procesos de Hola que utilizan normalmente no admiten una ampliación también si necesita toocreate más de una serie de máquinas virtuales.

Una manera de toocreate muchas máquinas virtuales similares es la construcción de Azure Resource Manager toouse Hola de *recursos bucles*.

## <a name="resource-loops"></a>bucles de recursos
Los bucles de recursos son una forma abreviada sintáctica presente en plantillas de Azure Resource Manager. Los bucles de recursos pueden crear un conjunto de recursos configurados de manera similar en un bucle. Puede usar recursos bucles toocreate varias cuentas de almacenamiento, interfaces de red o máquinas virtuales. Para obtener más información acerca de los bucles de recursos, consulte demasiado[crear máquinas virtuales en conjuntos de disponibilidad mediante bucles de recurso](https://azure.microsoft.com/documentation/templates/201-vm-copy-index-loops/).

## <a name="challenges-of-scale"></a>Desafíos de la escala
Aunque los bucles de recurso que sea más fácil toobuild una infraestructura de nube a escala y generan plantillas más concisas, siguen siendo determinados problemas. Por ejemplo, si usa un recurso bucle toocreate 100 máquinas virtuales, debe toocorrelate controladores de interfaz de red (NIC) con máquinas virtuales correspondientes y las cuentas de almacenamiento. Dado que número Hola de máquinas virtuales es probable que toobe diferente Hola número de cuentas de almacenamiento, tendrá toodeal con tamaños de bucle de recursos distinto, demasiado. Se trata de solucionar problemas, pero aumenta significativamente la complejidad de hello con una escala.

Otro desafío surge cuando se necesita una infraestructura que se escale de manera flexible. Por ejemplo, puede que una infraestructura de escalado automático que automáticamente aumenta o disminuye el número de Hola de máquinas virtuales en tooworkload de respuesta. Las máquinas virtuales no proporcionan un toovary mecanismo integrado en número (escalado horizontal y escalado en). Si escalar de mediante la eliminación de las máquinas virtuales, es difícil tooguarantee alta disponibilidad, asegúrese de que las máquinas virtuales se reparten entre dominios de actualización y error.

Por último, cuando se usa un bucle de recursos, varios recursos de toocreate llamadas van toohello de tejido subyacente. Cuando varias llamadas crean recursos similares, Azure tiene un tooimprove oportunidad implícita en este diseño y optimizar el rendimiento y confiabilidad de la implementación. Aquí es donde entran en luego los *conjuntos de escalado de máquinas virtuales* .

## <a name="virtual-machine-scale-sets"></a>Conjuntos de escalado de máquinas virtuales
Conjuntos de escalas de máquina virtual son un toodeploy de recursos de proceso de Azure y administración un conjunto de máquinas virtuales idénticos. Con todas las máquinas virtuales configuradas Hola igual, conjuntos de escalas de VM son tooscale fácil en y escalado horizontal. Basta con cambiar número de Hola de máquinas virtuales en el conjunto de Hola. También puede configurar tooautoscale de conjuntos de escala VM en función de las peticiones de Hola de carga de trabajo de Hola.

Para las aplicaciones que necesitan recursos de proceso tooscale out y en escala de las operaciones están equilibradas implícitamente a través de dominios de error y actualización.

En lugar de correlacionar varios recursos, como los NIC y las máquinas virtuales, un conjunto de escalado tiene propiedades de extensión, máquina virtual, almacenamiento y red que puede configurar de forma centralizada.

Para, se establece una escala de tooVM introducción, consulte toohello [escalas de máquina Virtual establece la página del producto](https://azure.microsoft.com/services/virtual-machine-scale-sets/). Para obtener más información, consulte toohello [escala de máquinas virtuales establece documentación](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/).

