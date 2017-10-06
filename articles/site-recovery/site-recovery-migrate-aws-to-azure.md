---
title: "aaaMigrate las máquinas virtuales de AWS tooAzure | Documentos de Microsoft"
description: "Este artículo describe cómo ejecutar los equipos de toomigrate virtual en tooAzure de Amazon Web Services (AWS) con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a>Migre máquinas virtuales de Amazon Web Services (AWS) tooAzure con Azure Site Recovery

Este artículo describe cómo toomigrate AWS Windows instancias tooAzure las máquinas virtuales con hello [Azure Site Recovery](site-recovery-overview.md) servicio.

Migración es realmente una conmutación por error de AWS tooAzure. No se puede tooAWS de máquinas de conmutación por recuperación, y no hay replicación en curso. En este artículo se describen los pasos de hello para la migración en hello portal de Azure y se basan en las instrucciones de Hola de [replicar una máquina física tooAzure](site-recovery-vmware-to-azure.md).

Enviar comentarios o preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

## <a name="supported-operating-systems"></a>Sistemas operativos compatibles

Recuperación del sitio puede ser instancias de utilizadas toomigrate EC2 que ejecute cualquiera de los siguientes sistemas operativos de hello:

- Windows (solo 64 bits)
    - Windows Server 2008 R2 SP1 + (solo controladores de Citrix PV o de AWS PV). **No se admiten las instancias que ejecutan controladores de RedHat PV**) Windows Server 2012 Windows Server 2012 R2
- Linux (solo 64 bits)
    - Red Hat Enterprise Linux 6.7 (solo instancias virtualizadas de HVM)

## <a name="prerequisites"></a>Requisitos previos

Requisitos para realizar esta implementación:

* **Servidor de configuración**: una máquina virtual de EC2 Amazon ejecuta Windows Server 2012 R2 se implementa como servidor de configuración de Hola. De forma predeterminada, hello otros componentes de Azure Site Recovery (servidor de proceso y servidor de destino maestro) se instalan al implementar el servidor de configuración de Hola. En este artículo se describen los pasos de hello para la migración en hello portal de Azure y se basan en las instrucciones de Hola de [obtener más información](site-recovery-components.md)

* **Instancias de EC2**: Hola Amazon EC2 instancias de máquinas virtuales que desea toomigrate.

## <a name="deployment-steps"></a>Pasos de implementación

1. Cree un almacén de Recovery Services.
2. Grupo de seguridad de las instancias de EC2 Hola debe tener reglas configuradas tooallow comunicación entre instancia EC2 de Hola que desea toomigrate y en el que piensa hello toodeploy servidor de configuración de instancia de Hola.

3. En hello mismo Amazon Virtual privada en la nube como las instancias de EC2, implemente un servidor de configuración de ASR. Consulte Hola VMware / físicas tooAzure los requisitos previos para requisitos de implementación de servidor de configuración.

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  Una vez que el servidor de configuración está implementado en AWS y registrado con el almacén de servicios de recuperación, debería ver los servidores de configuración de Hola y procesos en la infraestructura de Site Recovery tal y como se muestra a continuación:

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. Después de implementar el servidor de configuración de hello (podría tardar hasta too15 minustes para él tooappear), validar que puede comunicarse con máquinas virtuales de Hola que desea toomigrate.

6. [Configure las opciones de replicación](site-recovery-setup-replication-settings-vmware.md).

7. Habilitar la replicación: habilitar la replicación de máquinas virtuales que desee toomigrate Hola. Puede detectar instancias de EC2 Hola con direcciones IP privadas hello, que puede obtener desde la consola de hello EC2.

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. Una vez que se protegieron instancias Hola EC2 y Hola replicación tooAzure está completo, [ejecutar una conmutación por error de prueba](site-recovery-test-failover-to-azure.md) toovalidate rendimiento de su aplicación en Azure.

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. Ejecute una conmutación por error de AWS tooAzure para cada máquina virtual. Si lo desea, puede crear un plan de recuperación y ejecutar varias máquinas virtuales de una conmutación por error, toomigrate de AWS tooAzure. [Obtenga más información](site-recovery-create-recovery-plans.md) sobre los planes de recuperación.

10. Para la migración, no es necesario toocommit una conmutación por error. En su lugar, selecciona la opción de completar la migración de Hola para cada máquina que desee toomigrate. Hola acción de completar la migración finaliza el proceso de migración de hello, quita la replicación de la máquina de Hola y detiene la recuperación del sitio de facturación para la máquina de Hola.

    ![Migrar](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a>Pasos siguientes

- [Preparar la replicación de máquinas migradas tooenable](site-recovery-azure-to-azure-after-migration.md) tooanother región para las necesidades de recuperación ante desastres.
- Empezar a proteger las cargas de trabajo mediante la [replicación de máquinas virtuales de Azure.](site-recovery-azure-to-azure.md)
