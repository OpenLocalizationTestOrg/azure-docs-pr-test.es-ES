---
title: recomendaciones de Advisor alta disponibilidad aaaAzure | Documentos de Microsoft
description: Utilice tooimprove alta disponibilidad de las implementaciones de Azure de Asistente de Azure.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 3ac75ce401271f0212d198d7a7dc75ab702b6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-high-availability-recommendations"></a>Recomendaciones sobre alta disponibilidad de Advisor

Asistente de Azure le ayuda a garantizar y mejorar la continuidad de Hola de las aplicaciones empresariales críticas. Puede obtener recomendaciones de alta disponibilidad por el Asistente de hello **alta disponibilidad** ficha del panel de Asistente de Hola.

![Botón alta disponibilidad en el panel del Asistente de Hola](./media/advisor-high-availability-recommendations/advisor-high-availability-tab.png)


## <a name="ensure-virtual-machine-fault-tolerance"></a>Garantía de la tolerancia a errores en máquinas virtuales

Advisor identifica las máquinas virtuales que no forman parte de un conjunto de disponibilidad y recomienda moverlas a un conjunto de disponibilidad. Para proporcionar redundancia de tooyour aplicaciones, le recomendamos que agrupe dos o más máquinas virtuales en un conjunto de disponibilidad. Esta configuración garantiza que durante un evento de mantenimiento planeado o no, al menos una máquina virtual está disponible y cumple Hola máquina virtual de Azure SLA. Puede elegir cualquier toocreate un conjunto de disponibilidad para hello máquina virtual o tooadd Hola máquina virtual tooan conjunto de disponibilidad existente.

> [!NOTE]
> Si elige una disponibilidad toocreate configurada, debe agregar al menos una máquina virtual más en él. Se recomienda agrupar dos o más máquinas virtuales en la disponibilidad de un conjunto de tooensure que al menos una máquina está disponible durante una interrupción.

![Recomendación de Advisor: para la redundancia de las máquinas virtuales, utilice conjuntos de disponibilidad](./media/advisor-high-availability-recommendations/advisor-high-availability-create-availability-set.png)

## <a name="ensure-availability-set-fault-tolerance"></a>Garantía de la tolerancia a errores del conjunto de disponibilidad 

El asistente identifica los conjuntos de disponibilidad que contienen una sola máquina virtual y recomienda agregar uno o más tooit de máquinas virtuales. Para proporcionar redundancia de tooyour aplicaciones, le recomendamos que agrupe dos o más máquinas virtuales en un conjunto de disponibilidad. Esta configuración garantiza que durante un evento de mantenimiento planeado o no, al menos una máquina virtual está disponible y cumple Hola máquina virtual de Azure SLA. Puede elegir cualquier toocreate una máquina virtual o toouse una máquina virtual existente y tooadd se toohello conjunto de disponibilidad.  

![Recomendación del asistente: agregar uno o más el conjunto de disponibilidad de las máquinas virtuales toothis](./media/advisor-high-availability-recommendations/advisor-high-availability-add-vm-to-availability-set.png)


## <a name="ensure-application-gateway-fault-tolerance"></a>Garantía de la tolerancia a errores de Application Gateway
tooensure Hola continuidad del negocio de aplicaciones de misión crítica que se basan en las puertas de enlace de la aplicación, el asistente identifica instancias de puerta de enlace de aplicaciones que no están configurados para la tolerancia a errores, y recomienda las acciones correctoras que se pueden realizar . Advisor identifica instancias únicas de Application Gateway medianas o grandes, y recomienda que agregue al menos una instancia más. También se identifica único o varios instance pequeña aplicación puertas de enlace y se recomienda migrar toomedium o SKU grandes. El asistente recomienda estos tooensure de acciones que las instancias de puerta de enlace de aplicaciones son toosatisfy configurado Hola actuales requisitos del SLA para estos recursos.

![Recomendación de Advisor: implemente dos o más instancias de Application Gateway medianas o grandes](./media/advisor-high-availability-recommendations/advisor-high-availability-application-gateway.png)

## <a name="improve-hello-performance-and-reliability-of-virtual-machine-disks"></a>Mejorar el rendimiento de Hola y la confiabilidad de los discos de máquina virtual

El asistente identifica las máquinas virtuales con discos estándares y recomienda actualizar toopremium discos.
 
Azure Premium Storage ofrece compatibilidad con discos de alto rendimiento y latencia baja para máquinas virtuales que ejecutan cargas de trabajo intensivas de E/S. Los discos de máquinas virtuales que usan cuentas de Premium Storage almacenan datos en unidades de estado sólido (SSD). Hola recomendados para el rendimiento de la aplicación, se recomienda que migre los discos de máquina virtual que requieren almacenamiento de toopremium alta de e/s por segundo. 

Si los discos no requieren E/S por segundo elevadas, puede limitar los costos si los mantiene en una cuenta de almacenamiento Estándar. Con la cuenta de almacenamiento Estándar, se almacenan los datos de discos de máquinas virtuales en unidades de disco duro (HDD) en lugar de SSD. Puede elegir toomigrate los discos de toopremium de discos de máquina virtual. Los discos premium son compatibles con la mayoría de las SKU de máquinas virtuales. Sin embargo, en algunos casos, si desea que los discos premium toouse, deberá tooupgrade la máquina virtual de SKU.

![Recomendación del asistente: mejorar la confiabilidad de Hola de los discos de máquina virtual mediante la actualización toopremium discos](./media/advisor-high-availability-recommendations/advisor-high-availability-upgrade-to-premium-disks.png)

## <a name="protect-your-virtual-machine-data-from-accidental-deletion"></a>Protección de los datos de máquinas virtuales contra la eliminación accidental
Advisor identifica las máquinas virtuales que no tienen la copia de seguridad habilitada y recomienda habilitarla. Configurar la copia de seguridad de máquina virtual garantiza la disponibilidad de Hola de los datos críticos para la empresa y ofrece protección contra eliminación accidental o los daños.

![Recomendación del asistente: configurar los datos de misión crítica de tooprotect de copia de seguridad de máquina virtual](./media/advisor-high-availability-recommendations/advisor-high-availability-virtual-machine-backup.png)

## <a name="access-high-availability-recommendations-in-advisor"></a>Acceso a las recomendaciones sobre alta disponibilidad en Advisor

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).

2. En el panel izquierdo de hello, haga clic en **más servicios**.

3. Hola servicio panel de menú, en **supervisión y administración**, haga clic en **Asistente de Azure**.  
 Hola Advisor panel se abre.

4. En el panel del Asistente de hello, haga clic en hello **alta disponibilidad** pestaña y, a continuación, seleccione la suscripción de hello para el que desea que las recomendaciones de tooreceive.

> [!NOTE]
> tooaccess las recomendaciones del asistente, primero debe *registrar su suscripción* con el asistente. Una suscripción se registra cuando un *suscripción propietario* inicia Hola Hola de panel y hace clic en el asistente **obtener recomendaciones** botón. Esta operación *solo se realiza una vez*. Después de registra la suscripción de hello, puede tener acceso a las recomendaciones del asistente como *propietario*, *colaborador*, o *lector* para una suscripción de un grupo de recursos, o recurso específico.

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de las recomendaciones de Advisor, consulte:
* [Introducción tooAzure Advisor](advisor-overview.md)
* [Introducción a Advisor](advisor-get-started.md)
* [Recomendaciones sobre el costo de Advisor](advisor-performance-recommendations.md)
* [Recomendaciones sobre rendimiento de Advisor](advisor-performance-recommendations.md)
* [Recomendaciones sobre seguridad de Advisor](advisor-security-recommendations.md)

