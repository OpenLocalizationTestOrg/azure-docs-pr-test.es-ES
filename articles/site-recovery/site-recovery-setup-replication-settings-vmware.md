---
title: "aaaSet la configuración de replicación para Azure Site Recovery | Documentos de Microsoft"
description: "Describe cómo la replicación de tooorchestrate de toodeploy Site Recovery, la conmutación por error y la recuperación de máquinas virtuales de Hyper-V en VMM nubes tooAzure."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a>Administrar la directiva de replicación para VMware tooAzure


## <a name="create-a-replication-policy"></a>Creación de una directiva de replicación

1. Seleccione **Administrar** > **Infraestructura de Site Recovery**.
2. Seleccione **Directivas de replicación** en **Para VMware y máquinas físicas**.
3. Seleccione **+Directiva de replicación**.

    ![Creación de la directiva de replicación](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. Escriba el nombre de la directiva de Hola.

5. En **umbral de RPO**, especifique el límite RPO de Hola. Se generarán alertas cuando la replicación continua supera este límite.
6. En **retención de punto de recuperación**, especifique (en horas) Hola duración del período de retención de Hola para cada punto de recuperación. Equipos protegidos pueden ser recuperado tooany punto dentro de un período de retención.

    > [!NOTE]
    > Horas de too24 de retención es compatible con almacenamiento replicado toopremium de máquinas. Horas de too72 de retención es compatible con almacenamiento replicado toostandard de máquinas.

    > [!NOTE]
    > Se crea automáticamente una directiva de replicación para la conmutación por recuperación.

7. En **Frecuencia de instantánea coherente con la aplicación**especifique la frecuencia (en minutos) con la que se crearán puntos de recuperación que contengan las instantáneas coherentes con la aplicación.

8. Haga clic en **Aceptar**. Directiva de Hello debe crearse en 30 segundos de too60.

![Generación de directiva de replicación](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a>Asociación de un servidor de configuración con una directiva de replicación
1. Elija toowhich de directiva de replicación de hello desea que el servidor de configuración de tooassociate Hola.
2. Haga clic en **Asociar**.
![Asociación de servidor de configuración](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)

3. Seleccionar servidor de configuración de hello en lista de Hola de servidores.
4. Haga clic en **Aceptar**. servidor de configuración de Hello debe asociará un tootwo minutos.

![Asociación del servidor de configuración](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a>Edición de una directiva de replicación
1. Elija la directiva de replicación de hello para el que desea tooedit configuración de replicación.
![Edición de una directiva de replicación](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)

2. Haga clic en **Edit Settings**(Editar configuración).
![Edición de la configuración de directiva de replicación](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)

3. Cambiar la configuración de hello en función de sus necesidades.
4. Haga clic en **Guardar**. Directiva de Hello debe guardarse en dos minutos toofive, dependiendo de cuántas máquinas virtuales están utilizando esa directiva de replicación.

![Guardado de directiva de replicación](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a>Desasociación de un servidor de configuración de una directiva de replicación
1. Elija toowhich de directiva de replicación de hello desea que el servidor de configuración de tooassociate Hola.
2. Haga clic en **Desasociar**.
3. Seleccionar servidor de configuración de hello en lista de Hola de servidores.
4. Haga clic en **Aceptar**. servidor de configuración de Hello debe puede desasociar en un tootwo minutos.

    > [!NOTE]
    > No se puede anular la asociación de un servidor de configuración si hay al menos un elemento replicado mediante la directiva de Hola. Asegúrese de que no hay elementos replicados mediante la directiva de hello antes de anular la asociación de servidor de configuración de Hola.

## <a name="delete-a-replication-policy"></a>Eliminación de una directiva de replicación

1. Elija la directiva de replicación de Hola que desea toodelete.
2. Hacer clic en **Eliminar**. Directiva de Hello debe eliminarse en 30 segundos de too60.

    > [!NOTE]
    > No se puede eliminar una directiva de replicación, si existe al menos una configuración servidor asociado tooit. Asegúrese de que no hay elementos replicados mediante la directiva de Hola y delete que Hola a todos los asociados servidores de configuración antes de eliminar la directiva de Hola.
