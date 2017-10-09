---
title: aaaMigrate tooAzure con Site Recovery | Documentos de Microsoft
description: "Este artículo proporciona información general de migración de máquinas virtuales y servidores físicos tooAzure con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/05/2017
ms.author: raynew
ms.openlocfilehash: 6e65deee337c5371d441812ddb820dc8bc233684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-tooazure-with-site-recovery"></a>Migrar tooAzure con Site Recovery

Lea este artículo para obtener información general del uso de servicio de Azure Site Recovery de hello para la migración de máquinas virtuales y servidores físicos.

Recuperación del sitio es un servicio de Azure que contribuye estrategia BCDR tooyour, mediante la replicación de organización de servidores físicos locales y máquinas virtuales en la nube toohello (Azure) o tooa centro de datos secundario. Cuando se producen interrupciones en la ubicación principal, conmutación por error toohello ubicación secundaria tookeep aplicaciones y cargas de trabajo disponibles. Producirá un error de ubicación principal tooyour atrás cuando devuelve las operaciones de toonormal. Más información en [¿Qué es Site Recovery?](site-recovery-overview.md) También puede utilizar Site Recovery toomigrate su locales existentes las cargas de trabajo tooAzure tooexpedite el viaje de nube y dispon Hola matriz de características que ofrece Azure.

Para obtener una introducción rápida de cómo tooperform migración, consulte el vídeo de toothis.
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/ASRHowTo-Video2-Migrate-Virtual-Machines-to-Azure/player]

Este artículo describe la implementación en hello [portal de Azure](https://portal.azure.com). Hola [portal de Azure clásico](https://manage.windowsazure.com/) puede ser usado toomaintain existentes almacenes de Site Recovery, pero no se puede crear almacenes nuevos.

Registrar los comentarios de la parte inferior de Hola de este artículo. Formule preguntas técnicas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="what-do-we-mean-by-migration"></a>¿Qué entendemos por migración?

Puede implementar la recuperación de sitio para la replicación de máquinas virtuales locales y servidores físicos, tooAzure o tooa sitio secundario. Replicar máquinas, conmutación por error ellos del sitio primario de hello cuando se producen interrupciones y producirá un error en su sitio primario toohello back-cuando recupera. En suma toothis, puede usar las máquinas virtuales de Site Recovery toomigrate y tooAzure de servidores físicos, para que los usuarios puedan acceder a ellos como máquinas virtuales de Azure. Migración implica la replicación y conmutación por error de hello tooAzure de sitio primario y un gesto de completar la migración.

## <a name="what-can-site-recovery-migrate"></a>¿Qué se puede migrar con Site Recovery?

Puede:

- Migrar las cargas de trabajo que se ejecutan en local toorun máquinas virtuales de Hyper-V, máquinas virtuales de VMware y servidores físicos, máquinas virtuales de Azure. También puede hacer la replicación completa y la conmutación por recuperación en este escenario.
- Migre [máquinas virtuales de IaaS de Azure](site-recovery-migrate-azure-to-azure.md) entre regiones de Azure. Actualmente, en este escenario solo se admite la migración, lo que significa que no se admite la conmutación por recuperación.
- Migrar [instancias de Windows de AWS](site-recovery-migrate-aws-to-azure.md) tooAzure las máquinas virtuales IaaS. Actualmente, en este escenario solo se admite la migración, lo que significa que no se admite la conmutación por recuperación.

## <a name="migrate-on-premises-vms-and-physical-servers"></a>Migración de máquinas virtuales locales y servidores físicos

toomigrate local máquinas virtuales de Hyper-V, máquinas virtuales de VMware y servidores físicos, siga casi Hola mismos pasos que los usados para la replicación normal.

1. Configuración del almacén de Recovery Services
2. Configurar servidores de administración de hello necesario (VMware, VMM, Hyper-V - según lo que desee toomigrate), agréguelos toohello almacén y especificar la configuración de replicación.
3. Habilitar la replicación de hello máquinas que desea toomigrate
4. Después de la migración inicial de hello, ejecute un tooensure de conmutación por error de prueba rápida que todo funciona como debería.
5. Después de comprobar que funciona el entorno de replicación, use una conmutación por error planeada o no planeada en función de lo que su escenario [admita](site-recovery-failover.md). Se recomienda usar una conmutación por error planificada cuando sea posible.
6. Para la migración, no necesita toocommit una conmutación por error, o eliminarla. En su lugar, seleccione hello **completar la migración** opción para cada máquina que desee toomigrate.
     - En **replican elementos**, haga clic en hello VM y haga clic en **completar la migración**. Haga clic en **Aceptar** toocomplete. Puede seguir el progreso en las propiedades de la máquina virtual de hello, en mediante la supervisión de trabajos de completar la migración de hello en **trabajos de recuperación del sitio**.
     - Hola **completar la migración** acción finaliza el proceso de migración de hello, quita la replicación de la máquina de Hola y detiene la facturación de Site Recovery para la máquina de Hola.

![Completar migración](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

## <a name="migrate-between-azure-regions"></a>Migración entre regiones de Azure

Puede migrar máquinas virtuales de Azure entre regiones con Site Recovery. En este escenario solo se admite la migración. En otras palabras, puede replicar máquinas virtuales de Azure de Hola y conmutación por error de ellos tooanother región, pero no se producirá un error nuevo. En este escenario que configurar un almacén de servicios de recuperación, implementar una replicación de toomanage de servidor de configuración local, agregue toohello almacén y especificar la configuración de replicación. Habilitar la replicación para máquinas de Hola que desee toomigrate y ejecuta una rápida conmutación por error de prueba. Después, ejecutar una conmutación por error no planeada con hello **completar la migración** opción.

## <a name="migrate-aws-tooazure"></a>Migrar AWS tooAzure

Puede migrar AWS instancias tooAzure máquinas virtuales. En este escenario solo se admite la migración. En otras palabras, puede replicar instancias AWS hello y conmutación por error de ellos tooAzure, pero no se producirá un error nuevo. Instancias AWS se controlan en hello igual manera que los servidores físicos para la migración. Configurar un almacén de servicios de recuperación, implementar una replicación de toomanage de servidor de configuración local, agregue toohello almacén y especificar la configuración de replicación. Habilitar la replicación para máquinas de Hola que desee toomigrate y ejecuta una rápida conmutación por error de prueba. Después, ejecutar una conmutación por error no planeada con hello **completar la migración** opción.




## <a name="next-steps"></a>Pasos siguientes

- [Migrar máquinas virtuales VMware tooAzure](site-recovery-vmware-to-azure.md)
- [Migrar máquinas virtuales de Hyper-V en tooAzure de nubes VMM](site-recovery-vmm-to-azure.md)
- [Migrar máquinas virtuales de Hyper-V sin tooAzure VMM](site-recovery-hyper-v-site-to-azure.md)
- [Migración de máquinas virtuales de Azure entre regiones de Azure](site-recovery-migrate-azure-to-azure.md)
- [Migrar AWS instancias tooAzure](site-recovery-migrate-aws-to-azure.md)
- [Preparar la replicación de máquinas migradas tooenable](site-recovery-azure-to-azure-after-migration.md) tooanother región para las necesidades de recuperación ante desastres.
- Empezar a proteger las cargas de trabajo mediante la [replicación de máquinas virtuales de Azure.](site-recovery-azure-to-azure.md)
