---
title: "aaaTroubleshoot implementar problemas de la máquina virtual de Linux de Azure | Documentos de Microsoft"
description: "Solución de problemas de implementación de la máquina virtual Linux en el modelo de implementación de Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a>Solución de problemas de implementación de la máquina virtual Linux en Azure

problemas de implementación de máquina virtual (VM) de tootroubleshoot en Azure, revise hello [problemas principales](#top-issues) para las soluciones y los errores comunes.

Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en [Hola foros de Azure de MSDN y el desbordamiento de la pila](https://azure.microsoft.com/support/forums/). Como alternativa, puede registrar un incidente de soporte técnico de Azure. Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y seleccione **obtener admiten**.

## <a name="top-issues"></a>Principales problemas
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a>no admiten clústeres de Hola Hola solicitado tamaño de máquina virtual
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Vuelva a intentar la solicitud Hola con un tamaño más pequeño de la máquina virtual.
- Si hello tamaño de hello solicitada que no se puede cambiar la máquina virtual:
    - Detener todas las máquinas virtuales de hello en el conjunto de disponibilidad de Hola. Haga clic en **Grupos de recursos** > su grupo de recursos > **Recursos** > su conjunto de disponibilidad > **Máquinas virtuales** > su máquina virtual > **Detener**.
    - Después de que todos Hola detener las máquinas virtuales, crear Hola VM en el tamaño de hello deseado.
    - Iniciar Hola nueva máquina virtual en primer lugar y, a continuación, seleccione cada uno de hello detiene las máquinas virtuales y haga clic en Inicio.


## <a name="hello-cluster-does-not-have-free-resources"></a>Hola clúster no tiene recursos libres
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Reintentar solicitud de hello más tarde.
- Si puede hello nueva máquina virtual se establecer parte de una disponibilidad diferentes
    - Crear una máquina virtual en un conjunto de disponibilidad diferentes (Hola misma región).
    - Agregar Hola nueva VM toohello misma red virtual.

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a>Cómo se activa mi crédito mensual para Visual Studio Enterprise (BizSpark)

tooactivate su mensual del crédito, vea este [artículo](https://azure.microsoft.com/offers/ms-azr-0064p/).

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a>¿Por qué no puedo instalar controladores GPU de Hola para una máquina virtual NV de Ubuntu?

Actualmente, la compatibilidad con la GPU de Linux solo está disponible en las máquinas virtuales de Azure NC que ejecutan Ubuntu Server 16.04 LTS. Para más información consulte [Configuración de controladores de GPU para máquinas virtuales de la serie N con Linux](n-series-driver-setup.md).

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a>Faltan los controladores para mi máquina virtual de la serie N de Linux

Los controladores para las máquinas virtuales basadas en Linux se encuentran [aquí](n-series-driver-setup.md). 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a>No puedo encontrar una instancia de la GPU en mi máquina virtual de la serie N

tootake aprovechar las capacidades GPU de Hola de Azure N-series máquinas virtuales que ejecutan Windows Server 2016 o Windows Server 2012 R2, debe instalar a los controladores de gráficos NVIDIA en cada máquina virtual después de la implementación. La información de instalación del controlador está disponible para las [máquinas virtuales Windows](../windows/n-series-driver-setup.md) y las [máquinas virtuales Linux](n-series-driver-setup.md).

## <a name="is-n-series-vms-available-in-my-region"></a>¿Hay máquinas virtuales de la serie N en mi región?

Puede consultar la disponibilidad de Hola de hello [productos disponibles por tabla region](https://azure.microsoft.com/regions/services)y el precio de [aquí](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a>No estoy toosee capaz de familia de tamaño de máquina virtual que desea al cambiar el tamaño de la máquina virtual.

Cuando una máquina virtual se está ejecutando, es el servidor físico tooa implementado. servidores físicos de Hello en regiones de Azure se agrupan en clústeres de hardware físico comunes. Cambiar el tamaño de una máquina virtual que requiere clústeres de hardware de hello VM toobe movido toodifferent es diferente en función de qué modelo de implementación se usa toodeploy Hola VM.

- Máquinas virtuales implementadas en el modelo de implementación clásico, implementación del servicio de nube de hello deben quitarse y volver a implementar las máquinas virtuales tooa tamaño de toochange Hola de otra familia de tamaño.

- Máquinas virtuales implementadas en el modelo de implementación de administrador de recursos, debe detener todas las máquinas virtuales en conjunto antes de cambiar el tamaño de Hola de cualquier máquina virtual en el conjunto de disponibilidad de Hola de disponibilidad de Hola.

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a>Hello lista tamaño de máquina virtual no se admite mientras se implementa en el conjunto de disponibilidad.

Elija un tamaño que es compatible con clúster del conjunto de disponibilidad de Hola. Se recomienda al crear que un conjunto de disponibilidad toochoose Hola mayor tamaño de máquina virtual piensa que necesita y tiene que ser el primer toohello de implementación de conjunto de disponibilidad.

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a>¿Qué distribuciones o versiones de Linux son compatibles con Azure?

Encontrará la lista de hello en Linux en [Azure-Endorsed distribuciones](endorsed-distros.md).

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a>¿Puedo agregar un conjunto de disponibilidad de tooan clásico VM existente?

Sí. Puede agregar una existente tooa VM clásico nueva o conjunto de disponibilidad existentes. Para obtener más información, consulte [agrega un conjunto de disponibilidad de tooan de máquina virtual existente](../windows/classic/configure-availability.md#addmachine).


## <a name="next-steps"></a>Pasos siguientes
Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en [Hola foros de Azure de MSDN y el desbordamiento de la pila](https://azure.microsoft.com/support/forums/).

Como alternativa, puede registrar un incidente de soporte técnico de Azure. Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y seleccione **obtener admiten**.
