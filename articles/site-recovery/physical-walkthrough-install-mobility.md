---
title: "Hola aaaInstall servicio de movilidad de replicación de servidor físico tooAzure | Documentos de Microsoft"
description: "Este artículo describe cómo tooinstall Hola a agente del servicio de movilidad en servidores físicos replicar tooAzure con servicio de Azure Site Recovery Hola."
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
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a>Paso 9: Instalar el servicio de movilidad de Hola


Este artículo describe cómo componente de servicio de movilidad de tooinstall Hola al replicar local tooAzure de servidores físicos de Windows o Linux, mediante hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.

Hola servicio de movilidad captura escrituras de datos en un equipo y los reenvía toohello servidor de procesos. Debe instalarse en cada servidor que desea tooreplicate tooAzure.

Se puede instalar manualmente el servicio de movilidad de hello, o mediante una instalación de inserción de hello Site Recovery proceso servidor cuando está habilitada la replicación, o mediante una herramienta como System Center Configuration Manager. Si utiliza la instalación de inserción, servicio de hello está instalado en el servidor de hello cuando se habilita la replicación.

Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="install-manually"></a>Instalación manual

1. Comprobar hello [requisitos previos](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) para la instalación manual.
2. Siga [estas instrucciones](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) para la instalación manual mediante el portal de Hola.
3. Si prefiere tooinstall desde la línea de comandos de hello, siga [estas instrucciones](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).

## <a name="install-from-hello-process-server"></a>Instalar desde el servidor de procesos de Hola

Si desea toopush Hola instalación del servicio de movilidad Hola del servidor de procesos cuando se habilita la replicación de una máquina, necesita una cuenta que puede usarse para la máquina de hello proceso servidor tooaccess Hola. cuenta de Hello solo se utiliza para la instalación de inserción de Hola.

1. Si no ha creado una cuenta, hágalo haciendo uso de estas instrucciones:

    - Puede usar una cuenta local o de dominio.
    - Para Windows, si no usa una cuenta de dominio, debe toodisable control de acceso de usuarios remotos en el equipo local de Hola. toodo, Hola registrar con **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, agregar una entrada DWORD hello **LocalAccountTokenFilterPolicy**, con un valor de 1.
    - Si desea que entrada de registro de hello tooadd de Windows desde una CLI, escriba:

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - Para Linux, la cuenta de hello debe ser raíz Hola servidor de origen Linux.

2. A continuación, siga [estas instrucciones](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) si desea que el servicio de movilidad de hello toopush en máquinas virtuales que ejecutan Windows o Linux.

## <a name="other-installation-methods"></a>Otros métodos de instalación

- [Obtenga información acerca de](site-recovery-install-mobility-service-using-sccm.md) instalar servicio de movilidad de hello mediante Configuration Manager
- [Más información sobre la ](site-recovery-automate-mobility-service-install.md)instalación con DSC de Azure Automation.


## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 10: habilitar la replicación](physical-walkthrough-enable-replication.md)
