---
title: "Hola aaaInstall servicio de movilidad de replicación de VMware tooAzure | Documentos de Microsoft"
description: "Este artículo describe cómo tooinstall Hola a agente del servicio de movilidad de la replicación de tooAzure de VMware con servicio de Azure Site Recovery Hola."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d3b7bc9c4d84d13317e0b0b47adcf38e8c41d0bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-install-hello-mobility-service"></a>Paso 10: Instalar el servicio de movilidad de Hola


Este artículo describe cómo tooconfigure de configuración de origen y de destino cuando se replican de manera local tooAzure de máquinas virtuales de VMware, mediante hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.

Hola servicio de movilidad captura escrituras de datos en un equipo y los reenvía toohello servidor de procesos. Debe instalarse en cada equipo que desea tooreplicate tooAzure.

Puede instalar manual de servicio de movilidad de hello, mediante una instalación de inserción desde el servidor de proceso de recuperación del sitio de hello cuando está habilitada la replicación o utilizar una herramienta de System Center Configuration Manager. Si utiliza la instalación de inserción, servicio de Hola se instala en hello VM cuando está habilitada la replicación.

Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="install-manually"></a>Instalación manual

1. Comprobar hello [requisitos previos](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) para la instalación manual.
2. Siga [estas instrucciones](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) para la instalación manual mediante el portal de Hola.
3. Si prefiere tooinstall desde la línea de comandos de hello, siga [estas instrucciones](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).

## <a name="install-from-hello-process-server"></a>Instalar desde el servidor de procesos de Hola

Si desea la instalación del servicio de movilidad toopush Hola Hola del servidor de procesos cuando se habilita la replicación para una máquina virtual, necesitará una cuenta que puede usarse por Hola proceso servidor tooaccess Hola máquina virtual. cuenta de Hello solo se utiliza para la instalación de inserción de Hola.

1. Debe haber [creado una cuenta](vmware-walkthrough-prepare-vmware.md) que pueda usarse para la instalación de inserción. A continuación, especificar cuenta de hello que desea toouse al configurar el origen durante la implementación de Site Recovery.
2. A continuación, siga [estas instrucciones](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) si desea que el servicio de movilidad de hello toopush en máquinas virtuales que ejecutan Windows o Linux.

## <a name="other-methods"></a>Otros métodos

Obtenga más información sobre [instalar el servicio de movilidad de hello mediante Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), o mediante [DSC de automatización de Azure](site-recovery-automate-mobility-service-install.md).

## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 11: habilitar la replicación](vmware-walkthrough-enable-replication.md)
