---
title: "aaaBack el almacén de copia de seguridad de tooa clásico implementado máquinas virtuales de Azure | Documentos de Microsoft"
description: "Detectar, registrar y realizar copias de seguridad de las máquinas virtuales con estos procedimientos de copia de seguridad de máquinas virtuales de Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "copia de seguridad de máquinas virtuales; hacer copia de seguridad de máquinas virtuales; recuperación ante desastres y copia de seguridad; copia de seguridad de vm"
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 048e32d9b2bd5bdd7a125225a71a6d805bb4fbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a>Copia de seguridad de máquinas virtuales de Azure (Portal clásico)
> [!div class="op_single_selector"]
> * [Copia el almacén de servicios de máquinas virtuales tooRecovery](backup-azure-arm-vms.md)
> * [Realizar copias de las máquinas virtuales tooBackup almacén](backup-azure-vms.md)
>
>

En este artículo se proporciona procedimientos de Hola para copia de seguridad de un almacén de copia de seguridad de tooa implementado clásico máquina virtual de Azure (VM). Hay algunas tareas que necesita tootake símbolo inglés care de antes de hacer copias de seguridad una máquina virtual de Azure. Si aún no ha hecho Hola completa, por lo que [requisitos previos](backup-azure-vms-prepare.md) tooprepare el entorno para realizar copias de seguridad de las máquinas virtuales.

Para obtener más información, vea los artículos de hello en [planear la infraestructura de copia de seguridad de máquina virtual en Azure](backup-azure-vms-introduction.md) y [máquinas virtuales de Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).

> [!NOTE]
> Azure cuenta con dos modelos de implementación para crear recursos y trabajar con ellos: [Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md). Un almacén de Copia de seguridad solo puede proteger máquinas virtuales con implementación clásica. No puede proteger máquinas virtuales con implementación mediante Resource Manager con un almacén de Copia de seguridad. Vea [copia de seguridad el almacén de servicios de máquinas virtuales tooRecovery](backup-azure-arm-vms.md) para obtener más información sobre cómo trabajar con servicios de recuperación de los almacenes de credenciales.
>
>

La realización de copias de seguridad de máquinas virtuales de Azure consta tres pasos principales:

![Tooback de tres pasos de una VM de IaaS de Azure](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> La copia de seguridad de máquinas virtuales es un proceso local. No se puede realizar copias de seguridad de máquinas virtuales en un almacén de copia de seguridad de tooa región en otra región. Por lo tanto, debe crear un almacén de copia de seguridad en cada región de Azure donde estén las máquinas virtuales de las que se realizará una copia de seguridad.
>
> [!IMPORTANT]
> A partir de marzo de 2017, no podrá usar almacenes de copia de seguridad de hello toocreate portal clásico.
> Ahora puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad. Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.<br/> Después de 15 de octubre de 2017, no puede usar almacenes de copia de seguridad de toocreate de PowerShell. **El 1 de noviembre de 2017**:
>- Todos los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.
>- No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola. En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.
>

## <a name="step-1---discover-azure-virtual-machines"></a>Paso 1: Detección de máquinas virtuales de Azure
tooensure cualquier nueva suscripción toohello agregada de máquinas virtuales (VM) se identifican antes de registrar, ejecute el proceso de detección de Hola. Hola procesar consultas Azure para la lista de Hola de máquinas virtuales de suscripción de hello, junto con información adicional como el nombre del servicio de nube de Hola y región Hola.

1. Inicie sesión en toohello [portal clásico](http://manage.windowsazure.com/)
2. En la lista de hello de servicios de Azure, haga clic en **servicios de recuperación** tooopen lista de Hola de almacenes de copia de seguridad y recuperación del sitio.
    ![Abrir lista de almacenes](./media/backup-azure-vms/choose-vault-list.png)
3. En lista de Hola de almacenes de copia de seguridad, seleccione hello tooback de almacén de una máquina virtual.

    Si se trata de un nuevo portal de Hola de almacén abre toohello **inicio rápido** página.

    ![Abrir menú de elementos registrados](./media/backup-azure-vms/vault-quick-start.png)

    Si previamente se ha configurado el almacén de hello, portal de hello abre el menú de toohello usado más recientemente.
4. Menú de almacén de hello (al principio de Hola de página de hello), haga clic en **elementos registrados**.

    ![Abrir menú de elementos registrados](./media/backup-azure-vms/vault-menu.png)
5. De hello **tipo** menú, seleccione **Máquina Virtual de Azure**.

    ![Seleccionar carga de trabajo](./media/backup-azure-vms/discovery-select-workload.png)
6. Haga clic en **DISCOVER** final Hola de página Hola.
    ![Botón Detectar](./media/backup-azure-vms/discover-button-only.png)

    proceso de detección de Hello puede tardar unos minutos mientras se se tabulan hello las máquinas virtuales. Hay una notificación en la parte inferior de Hola de pantalla de bienvenida que le permite saber que se está ejecutando el proceso de Hola.

    ![Detectar máquinas virtuales](./media/backup-azure-vms/discovering-vms.png)

    notificación de Hello cambia cuando se complete el proceso de Hola. Si el proceso de detección de hello no encontró hello las máquinas virtuales, asegúrese en primer lugar que existen hello las máquinas virtuales. Si existen hello las máquinas virtuales, asegúrese de hello las máquinas virtuales están en Hola misma región que el almacén de copia de seguridad de Hola. Si las máquinas virtuales de hello existen y están en Hola la misma región, asegúrese de que Hello las máquinas virtuales ya no están registrados tooa el almacén de copia de seguridad. Si una máquina virtual es el almacén de copia de seguridad tooa asignado no es almacenes de copia de seguridad de tooother toobe disponibles asignado.

    ![Detección realizada](./media/backup-azure-vms/discovery-complete.png)

    Una vez que ha detectado elementos nuevos de hello, vaya tooStep 2 y registre las máquinas virtuales.

## <a name="step-2---register-azure-virtual-machines"></a>Paso 2: Registro de máquinas virtuales de Azure
Registrar un tooassociate de máquina virtual de Azure con hello servicio de copia de seguridad de Azure. El registro suele ser una actividad que solo se realiza una vez.

1. Navegar por el almacén de copia de seguridad toohello en **servicios de recuperación** en Hola portal de Azure y, a continuación, haga clic en **elementos registrados**.
2. Seleccione **Máquina Virtual de Azure** desde el menú desplegable de Hola.

    ![Seleccionar carga de trabajo](./media/backup-azure-vms/discovery-select-workload.png)
3. Haga clic en **registrar** final Hola de página Hola.
    ![Botón Registrar](./media/backup-azure-vms/register-button-only.png)
4. Hola **registrar elementos** menú contextual, seleccione hello las máquinas virtuales que desea tooregister. Si hay dos o más máquinas virtuales con Hola mismo nombre, utilice toodistinguish de servicio de nube Hola entre ellos.

   > [!TIP]
   > Se pueden registrar varias máquinas virtuales al mismo tiempo.
   >
   >

    Se crea un trabajo para cada máquina virtual que ha seleccionado.
5. Haga clic en **ver trabajo** en hello notificación toogo toohello **trabajos** página.

    ![Registrar trabajo](./media/backup-azure-vms/register-create-job.png)

    máquina virtual de Hola también aparece en la lista de Hola de los elementos registrados, junto con el estado de Hola de operación de registro de hello.

    ![Registrando estado 1](./media/backup-azure-vms/register-status01.png)

    Cuando se completa la operación de hello, estado de hello cambia hello tooreflect *registrado* estado.

    ![Registrando estado 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a>Paso 3: Protección de las máquinas virtuales de Azure
Ahora puede configurar una directiva de copia de seguridad y retención de la máquina virtual de Hola. Se pueden proteger varias máquinas virtuales en una sola acción de protección.

Almacenes de copia de seguridad de Azure creados después de mayo de 2015 vienen con una directiva predeterminada integrada en el almacén de Hola. Esta directiva predeterminada viene con un período de retención predeterminado de 30 días y una programación de copia de seguridad diaria.

1. Navegar por el almacén de copia de seguridad toohello en **servicios de recuperación** en Hola portal de Azure y, a continuación, haga clic en **elementos registrados**.
2. Seleccione **Máquina Virtual de Azure** desde el menú desplegable de Hola.

    ![Seleccionar carga de trabajo en el portal](./media/backup-azure-vms/select-workload.png)
3. Haga clic en **proteger** final Hola de página Hola.

    Hola **Asistente para proteger elementos** aparece. Asistente de Hello solo muestra las máquinas virtuales que están registradas y no protegidas. Seleccione hello las máquinas virtuales que desea tooprotect.

    Si hay dos o más máquinas virtuales con Hola mismo nombre, utilice toodistinguish de servicio de nube Hola entre las máquinas virtuales Hola.

   > [!TIP]
   > Puede proteger varias máquinas virtuales al mismo tiempo.
   >
   >

    ![Configuración de protección a escala](./media/backup-azure-vms/protect-at-scale.png)

4. Elija un **programar copia de seguridad** tooback las máquinas virtuales de Hola que ha seleccionado. Puede seleccionar una directiva de un conjunto existente o definir una nueva.

    Cada directiva de copia de seguridad puede tener asociadas varias máquinas virtuales. Sin embargo, máquina virtual de hello solo puede estar asociado a una directiva en un momento determinado en tiempo.

    ![Protección mediante nueva directiva](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > Una directiva de copia de seguridad incluye un esquema de retención de copias de seguridad programada de Hola. Si selecciona una directiva de copia de seguridad existente, no se puede modificar opciones de retención de hello en el paso siguiente de saludo.
   >
   >

5. Elija un **duración de retención** tooassociate con copias de seguridad de Hola.

    ![Protección con retención flexible](./media/backup-azure-vms/policy-retention.png)

    Directiva de retención especifica Hola período de tiempo para almacenar una copia de seguridad. Puede especificar las directivas de retención diferentes en función de cuando se realizó la copia de seguridad de Hola. Por ejemplo, un punto de copia de seguridad diario (que sirve como punto de recuperación operativo) podría conservarse durante 90 días. En comparación, un punto de copia de seguridad realizado al final de Hola de cada trimestre (por motivos de auditoría) puede necesitar toobe conservan por varios meses o años.

    ![Se realiza una copia de seguridad de la máquina virtual con punto de recuperación](./media/backup-azure-vms/long-term-retention.png)

    En esta imagen de ejemplo:

   * **Directiva de retención diaria**: las copias de seguridad realizadas diariamente se almacenan durante 30 días.
   * **Directiva de retención semanal**: las copias de seguridad realizadas cada domingo se conservan durante 104 semanas.
   * **Directiva de retención mensual**: copias de seguridad realizadas en hello último domingo de cada mes se conservan durante 120 meses.
   * **Directiva de retención anual**: se conservan las copias de seguridad realizadas en hello primer domingo de cada enero de 99 años.

     Un trabajo se crea la directiva de protección de tooconfigure hello y asociar directiva de toothat Hola máquinas virtuales para cada máquina virtual que ha seleccionado.
6. lista de hello tooview de **configurar la protección** trabajos, desde el menú de almacenes de hello, haga clic en **trabajos** y seleccione **configurar la protección** de hello **operación**  filtro.

    ![Configurar trabajo de protección](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a>Copia de seguridad inicial
Una vez que la máquina virtual de hello está protegida con una directiva, muestra en hello **elementos protegidos** ficha con el estado de Hola de *Protected - (pendiente de copia de seguridad inicial)*. De forma predeterminada, copia de seguridad programada Hola primer es hello *copia de seguridad inicial*.

tootrigger Hola copia de seguridad inicial inmediatamente después de configurar la protección:

1. Final de Hola de hello **elementos protegidos** página, haga clic en **copia de seguridad ahora**.

    Hola servicio copia de seguridad de Azure crea un trabajo de copia de seguridad para la operación de copia de seguridad inicial de Hola.
2. Haga clic en hello **trabajos** lista de pestañas tooview Hola de trabajos.

    ![Copia de seguridad en curso](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> Durante la operación de copia de seguridad de hello, Hola servicio copia de seguridad de Azure emite una extensión de copia de seguridad de toohello de comando en cada máquina virtual de tooflush todos los trabajos de escritura y toman una instantánea coherente.
>
>

Cuando finalice la copia de seguridad inicial de hello, estado de Hola de máquina virtual de Hola Hola **elementos protegidos** ficha es *Protected*.

![Se realiza una copia de seguridad de la máquina virtual con punto de recuperación](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a>Visualización de los detalles y el estado de la copia de seguridad
Una vez protegido, recuento de máquinas virtuales de hello también aumenta en hello **panel** resumen de la página. Hola **panel** página también muestra el número de Hola de trabajos de hello últimas 24 horas que estaban *correcta*, tienen *no se pudo*y son *en curso*. En hello **trabajos** , utilice hello **estado**, **operación**, o **de** y **a** toofilter de menús trabajos de Hola.

![Estado de la copia de seguridad en la página Panel](./media/backup-azure-vms/dashboard-protectedvms.png)

Los valores en el panel de Hola se actualizan una vez cada 24 horas.

## <a name="troubleshooting-errors"></a>Solución de errores
Si surgen problemas durante la copia de seguridad de la máquina virtual, mirar hello [artículo de solución de problemas de VM](backup-azure-vms-troubleshoot.md) para obtener ayuda.

## <a name="next-steps"></a>Pasos siguientes
* [Administración y supervisión de las máquinas virtuales](backup-azure-manage-vms.md)
* [Restauración de máquinas virtuales](backup-azure-restore-vms.md)
