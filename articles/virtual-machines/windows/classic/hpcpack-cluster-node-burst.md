---
title: "clúster de HPC Pack de tooan de nodos de ráfaga de aaaAdd | Documentos de Microsoft"
description: "Obtenga información acerca de cómo agrupar tooexpand un HPC Pack en Azure a petición agregando instancias de rol de trabajo que ejecutan un servicio en nube"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 24b79a8a-24ad-4002-ae76-75abc9b28c83
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 7ec40ffe76485742c9e458ec49e11805990974e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-on-demand-burst-nodes-tooan-hpc-pack-cluster-in-azure"></a>Agregar "irrumpir" nodos tooan HPC Pack clúster a petición en Azure
Si configuras una [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) clúster en Azure, le podría interesar una manera de capacidad de clúster de Hola de tooquickly escala hacia arriba o hacia abajo, sin mantener un conjunto de máquinas virtuales de nodos de proceso preconfigurados. Este artículo muestra cómo tooadd a petición "irrumpir" nodos (instancias de rol de trabajo ejecuta un servicio en nube) como nodo principal tooa de proceso recursos en Azure. 

> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

![Nodos de ráfaga][burst]

pasos de Hello en este artículo le ayudarán a agregar nodos de Azure rápidamente tooa basada en la nube HPC Pack VM del nodo principal para una implementación de prueba o de prueba de concepto. pasos de alto nivel de Hello son Hola igual que los pasos de hello demasiado "irrumpir tooAzure" tooadd proceso en la nube clúster de HPC Pack de capacidad tooan local. Si desea conseguir un tutorial, consulte [Configurar un clúster de proceso híbrido con Microsoft HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md). Para obtener instrucciones detalladas y consideraciones para las implementaciones de producción, consulte [tooAzure con Microsoft HPC Pack en ráfagas](https://technet.microsoft.com/library/gg481749.aspx).

## <a name="prerequisites"></a>Requisitos previos
* **Nodo principal de HPC Pack implementado en una máquina virtual de Azure** : puede usar una máquina virtual del nodo principal independiente o una que forme parte de un clúster de mayor tamaño. toocreate un nodo principal independiente, consulte [implementar un nodo principal de HPC Pack en una máquina virtual de Azure](../../virtual-machines-windows-hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Para opciones de implementación de clúster de HPC Pack automatizadas, consulte [opciones toocreate y administrar un clúster de Windows HPC en Azure con Microsoft HPC Pack](../../virtual-machines-windows-hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  
  > [!TIP]
  > Si usas hello [script de implementación de IaaS de HPC Pack](hpcpack-cluster-powershell-script.md) toocreate Hola de clúster en Azure, puede incluir nodos de ráfaga de Azure en la implementación automatizada. Vea los ejemplos de hello en ese artículo.
  > 
  > 
* **Suscripción de Azure** -tooadd Azure nodos, puede elegir Hola misma suscripción utiliza toodeploy Hola VM del nodo principal, o una suscripción diferente (o suscripciones).
* **Cuota de núcleos** -podría necesita tooincrease Hola cuota de núcleos, especialmente si elige toodeploy varios nodos de Azure con tamaños de varios núcleos. tooincrease una cuota, [abrir una solicitud de soporte al cliente en línea](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) sin cargo.

## <a name="step-1-create-a-cloud-service-and-a-storage-account-for-hello-azure-nodes"></a>Paso 1: Crear un servicio de nube y una cuenta de almacenamiento para hello nodos de Azure
Use Hola portal de Azure clásico u Hola de herramientas equivalentes tooconfigure recursos que son necesario toodeploy siguientes los nodos de Azure:

* Un nuevo servicio en la nube de Azure
* Una nueva cuenta de almacenamiento de Azure

> [!NOTE]
> No reutilice un servicio en la nube existente en su suscripción. 
> 
> 

**Consideraciones**

* Configurar un servicio de nube diferente para cada plantilla de nodo de Azure que piensa toocreate. Sin embargo, puede usar Hola la misma cuenta de almacenamiento para varias plantillas de nodo.
* Se recomienda que busque servicio de nube de Hola y cuenta de almacenamiento de hello para la implementación de Hola Hola misma región de Azure.

## <a name="step-2-configure-an-azure-management-certificate"></a>Paso 2: Configurar un certificado de administración de Azure
tooadd Azure nodos como recursos de proceso, necesita un certificado de administración en el nodo principal de Hola y carga correspondiente certificado toohello suscripción de Azure usada para la implementación de Hola.

En este escenario, puede elegir hello **certificado predeterminado de la administración de Azure de HPC** que HPC Pack instala y configura automáticamente en el nodo principal. Este certificado resulta de utilidad para pruebas e implementaciones de prueba de concepto. toouse este certificado, cargue el archivo C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer desde el nodo principal de hello suscripción toothe de máquina virtual. certificado de hello tooupload Hola [portal de Azure clásico](https://manage.windowsazure.com), haga clic en **configuración** > **certificados de administración**.

Para el certificado de administración de Hola de tooconfigure opciones adicionales, consulte [Hola de escenarios tooConfigure certificado de administración de Azure para implementaciones de irrupción de Azure](http://technet.microsoft.com/library/gg481759.aspx).

## <a name="step-3-deploy-azure-nodes-toohello-cluster"></a>Paso 3: Implementar el clúster de toohello de nodos de Azure
Hola tooadd pasos e iniciar Azure nodos en este escenario se Hola mismo generalmente como pasos de hello con un nodo principal local. Para obtener más información, vea Hola siguientes secciones en [pasos tooDeploy nodos de Azure con Microsoft HPC Pack](https://technet.microsoft.com/library/gg481758.aspx):

* Crear una plantilla de nodo de Azure
* Agregar clúster de Windows HPC toohello de nodos de Azure
* Iniciar (aprovisionar) Hola nodos de Azure

Después de agregar e iniciar nodos de hello, están preparados para que los trabajos de clúster de toorun toouse.

Si tiene problemas al implementar nodos de Azure, consulte [Solución de problemas de implementaciones de nodos de Azure con Microsoft HPC Pack](http://technet.microsoft.com/library/jj159097.aspx).

## <a name="next-steps"></a>Pasos siguientes
* nodos de ráfaga de toouse un tamaño de instancia de proceso intensivo para hello, consulte Consideraciones de hello en [tamaños de máquinas virtuales de proceso de alto rendimiento](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Si desea aumentar o reducir automáticamente Hola los recursos según la carga de trabajo de clúster de hello informáticos de Azure, consulte [automáticamente aumentar y reducir los recursos de proceso de Azure en un clúster de HPC Pack](hpcpack-cluster-node-autogrowshrink.md).

<!--Image references-->
[burst]: ./media/hpcpack-cluster-node-burst/burst.png
