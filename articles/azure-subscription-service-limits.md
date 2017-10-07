---
title: "suscripción aaaAzure límites y cuotas | Documentos de Microsoft"
description: "Se proporciona una lista de límites, cuotas y restricciones de suscripción y servicio comunes de Azure. Esto incluye información sobre cómo se limita tooincrease junto con los valores máximos."
services: 
documentationcenter: 
author: rothja
manager: jeffreyg
editor: 
tags: billing
ms.assetid: 60d848f9-ff26-496e-a5ec-ccf92ad7d125
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: byvinyal
ms.openlocfilehash: a754d56124520791254ab8f1729808f0750ff222
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a>Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure
Este documento enumeran algunos de los límites más comunes de Microsoft Azure hello, que a veces se denominan cuotas. Actualmente, este documento no cubre todos los servicios de Azure. Con el tiempo, lista de Hola se expandirá y actualiza toocover más de plataforma de Hola.

Visite [información general de precios de Azure](https://azure.microsoft.com/pricing/) toolearn más información sobre precios de Azure. Allí, puede calcular los costos mediante hello [Calculadora de precios de](https://azure.microsoft.com/pricing/calculator/) o visitando Hola precios página de detalles de un servicio (por ejemplo, [máquinas virtuales de Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)). Para sugerencias toohelp administrar sus costos, vea [evitar costos inesperados con la administración de costos y facturación de Azure](billing/billing-getting-started.md).

> [!NOTE]
> Si desea tooraise límite de Hola o cuota por encima de hello **límite predeterminado**, [abrir una solicitud de soporte al cliente en línea sin cargo](azure-supportability/resource-manager-core-quotas-request.md). Hello límites no se generará anteriormente hello **límite máximo** valor mostrado en hello las tablas siguientes. Si no hay ningún **límite máximo** columna, a continuación, recursos de hello no tiene límites ajustables. 
> 
> Las suscripciones de evaluación gratuita no son aptas para aumentar el límite ni la cuota. Si tiene una prueba gratuita, puede actualizar tooa [pago por uso](https://azure.microsoft.com/offers/ms-azr-0003p/) suscripción. Para obtener más información, consulte [actualizar evaluación gratuita de Azure tooPay-como--Go](billing/billing-upgrade-azure-subscription.md).
> 

## <a name="limits-and-hello-azure-resource-manager"></a>Límites y hello Azure Resource Manager
Ahora es posible toocombine varios recursos de Azure en tooa único grupo de recursos de Azure. Al utilizar grupos de recursos, los límites de una vez eran globales sea administrados a nivel regional con hello Azure Resource Manager. Para más información sobre los grupos de recursos de Azure, consulte [Información general de Azure Resource Manager](azure-resource-manager/resource-group-overview.md).

En límites de Hola a continuación, una nueva tabla se ha agregado tooreflect las diferencias en los límites de cuando se usa hello Azure Resource Manager. Por ejemplo, hay una tabla de **Límites de suscripción** y una tabla de **Límites de suscripción - Azure Resource Manager**. Cuando un límite aplica a los escenarios de tooboth, solo se muestra en la primera tabla de Hola. A menos que se indique lo contrario, los límites son globales en todas las regiones.

> [!NOTE]
> Es importante tooemphasize que las cuotas de recursos en los grupos de recursos de Azure son accesibles para la suscripción por región y no por suscripción, como las cuotas de administración del servicio de Hola. Usemos las cuotas de núcleo como ejemplo. Si necesita toorequest una cuota aumentar con compatibilidad con núcleos, deberá toodecide cómo núcleos que desee toouse en cada región y, a continuación, realice una solicitud específica para el grupo de recursos de Azure principales cuotas para los importes de Hola y regiones que desee. Por lo tanto, si necesita toouse 30 núcleos en Europa occidental toorun la aplicación en concreto, debe solicitar 30 núcleos en Europa occidental. Pero no tendrá una cuota de núcleos de aumentar en ninguna otra región: Europa occidental solo tendrá cuota de núcleos de 30 Hola.
> <!-- -->
> Como resultado, quizá le resulte útil tooconsider decidir lo que las cuotas de grupo de recursos de Azure necesitan toobe para la carga de trabajo en cualquier una región y de solicitud que importe en cada región en la que está considerando la implementación. Consulte [solucionar problemas de implementación](resource-manager-common-deployment-errors.md) para obtener más ayuda para descubrir las cuotas actuales para regiones específicas.
> 
> 

## <a name="service-specific-limits"></a>Límites específicos del servicio
* [Active Directory](#active-directory-limits)
* [API Management](#api-management-limits)
* [App Service](#app-service-limits)
* [Puerta de enlace de aplicaciones](#application-gateway-limits)
* [Application Insights](#application-insights-limits)
* [Automatización](#automation-limits)
* [Azure Cosmos DB](#azure-cosmos-db-limits)
* [Azure Event Grid](#azure-event-grid-limits)
* [Azure Redis Cache](#azure-redis-cache-limits)
* [Azure RemoteApp](#azure-remoteapp-limits)
* [Backup](#backup-limits)
* [Lote](#batch-limits)
* [Servicios de BizTalk](#biztalk-services-limits)
* [SERVICIO CDN](#cdn-limits)
* [Cloud Services](#cloud-services-limits)
* [Azure Container Instances](#container-instances-limits)
* [Factoría de datos](#data-factory-limits)
* [Análisis de Data Lake](#data-lake-analytics-limits)
* [Data Lake Store](#data-lake-store-limits)
* [DNS](#dns-limits)
* [Event Hubs](#event-hubs-limits)
* [IoT Hub](#iot-hub-limits)
* [Key Vault](#key-vault-limits)
* [Log Analytics/Operational Insights](#log-analytics-limits)
* [Media Services](#media-services-limits)
* [Mobile Engagement](#mobile-engagement-limits)
* [Mobile Services](#mobile-services-limits)
* [Supervisión](#monitor-limits)
* [Multi-Factor Authentication](#multi-factor-authentication)
* [Redes](#networking-limits)
* [Network Watcher](#network-watcher-limits)
* [Servicio Notification Hubs](#notification-hub-service-limits)
* [Grupo de recursos](#resource-group-limits)
* [Scheduler](#scheduler-limits)
* [Search](#search-limits)
* [Service Bus](#service-bus-limits)
* [Recuperación de sitios](#site-recovery-limits)
* [SQL Database](#sql-database-limits)
* [Storage](#storage-limits)
* [Sistema de StorSimple](#storsimple-system-limits)
* [Análisis de transmisiones](#stream-analytics-limits)
* [Suscripción](#subscription-limits)
* [Administrador de tráfico](#traffic-manager-limits)
* [Virtual Machines](#virtual-machines-limits)
* [Conjuntos de escalado de máquina virtual](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a>Límites de suscripción
#### <a name="subscription-limits"></a>Límites de suscripción
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a>Límites de suscripción - Azure Resource Manager
Hola siguiendo los límites se aplica al utilizar grupos de recursos de Azure y hello Azure Resource Manager. Los límites que no han cambiado con hello Azure Resource Manager no se muestran a continuación. Consulte la tabla anterior toohello para esos límites.

Para información sobre el control de límites en las solicitudes de Resource Manager, consulte ///[Throttling Resource Manager requests](resource-manager-request-limits.md) (Limitación de las solicitudes de Resource Manager).

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a>Límites de grupos de recursos
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a>Límites de Virtual Machines
#### <a name="virtual-machine-limits"></a>Límites de Virtual Machines
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a>Límites de Virtual Machines: Azure Resource Manager
Hola siguiendo los límites se aplica al utilizar grupos de recursos de Azure y hello Azure Resource Manager. Los límites que no han cambiado con hello Azure Resource Manager no se muestran a continuación. Consulte la tabla anterior toohello para esos límites.

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a>Límites de los conjuntos de escalas de máquinas virtuales
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a>Límites de Container Instances
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a>Límites de red
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a>Límites de red
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a>Límites de Application Gateway
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a>Límites de Network Watcher
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a>Límites de Traffic Manager
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a>Límites de DNS
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a>Límites de Storage
Para más información sobre los límites de la cuenta de almacenamiento, vea [Objetivos de escalabilidad y rendimiento de Azure Storage](storage/common/storage-scalability-targets.md).
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a>Límites del servicio de Storage
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a>Límites de discos de máquinas virtuales 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

Consulte [Tamaños de máquina virtual](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obtener información adicional.

#### <a name="managed-virtual-machine-disks"></a>Discos de máquinas virtuales administrados

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a>Discos de máquinas virtuales no administrados

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a>Límites de proveedor de recursos de Storage
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a>Límites de Cloud Services
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a>Límites de App Service
siguiente Hola que limita de servicio de aplicaciones incluye límites para las aplicaciones Web, aplicaciones móviles, aplicaciones de API y las aplicaciones lógicas.

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a>Límites de Scheduler
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a>Límites de Batch
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a>Límites de BizTalk Services
Hello tabla siguiente muestran los límites de hello de servicios de Biztalk de Azure.

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a>Límites de Azure Cosmos DB
Base de datos de Cosmos Azure es una base de datos de escala global en las que el rendimiento y el almacenamiento pueden toohandle escalado lo que requiere la aplicación. Si tiene alguna pregunta sobre la escala de hello proporciona la base de datos de Azure Cosmos, envíe un correo electrónico tooaskcosmosdb@microsoft.com.

### <a name="mobile-engagement-limits"></a>Límites de Mobile Engagement
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a>Límites de Search
Niveles de precios determinan la capacidad de Hola y límites de su servicio de búsqueda. Los planes incluyen:

* *Gratis* , compartido con otros suscriptores de Azure, se ha diseñado para proyectos de evaluación y de desarrollo de pequeña envergadura.
* *Básico* proporciona recursos informáticos dedicados para cargas de trabajo de producción en una escala más pequeña, con seguridad de réplicas de toothree para cargas de trabajo de consulta de alta disponibilidad.
* *Estándar (S1, S2, S3, S3 de alta densidad)* es para mayores cargas de trabajo de producción. Varios niveles existen dentro de nivel estándar de Hola para que pueda elegir una configuración de recursos que mejor coincida con el perfil de carga de trabajo.

**Límites por suscripción**

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

**Límites por servicio de búsqueda**

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

toolearn más información acerca de los límites en un nivel más granular, como el tamaño del documento, las consultas por segundo, las claves, las solicitudes y respuestas, vea [límites en la búsqueda de Azure del servicio](search/search-limits-quotas-capacity.md).

### <a name="media-services-limits"></a>Límites de Media Services
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a>Límites de red CDN
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a>Límites de Mobile Services
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a>Límites de Monitor
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a>Límites de servicio de Notification Hubs
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a>Límites de Event Hubs
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a>Límites de Service Bus
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a>Límites de IoT Hub
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a>Límites de Data Factory
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a>Límites de Data Lake Analytics
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a>Límites de Data Lake Store
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a>Límites de Stream Analytics
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a>Límites de Active Directory
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a>Límites de Azure Event Grid
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a>Límites de Azure RemoteApp
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a>Límites del sistema StorSimple
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a>Límites de Log Analytics
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a>Límites de Backup
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a>Límites de Site Recovery
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a>Límites de Application Insights
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a>Límites de API Management
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a>Límites de Azure Redis Cache
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a>Límites de Key Vault
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a>Multi-Factor Authentication
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a>Límites de Automation
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a>Límites de SQL Database
Para conocer los límites de SQL Database, vea [Límites de recursos de SQL Database](sql-database/sql-database-resource-limits.md).

## <a name="see-also"></a>Otras referencias
[Concepto de límites de Azure y aumento de los mismos](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[Tamaños de máquinas virtuales y servicios en la nube de Azure](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Tamaños de Cloud Services](cloud-services/cloud-services-sizes-specs.md)

