---
title: "almacenes y servidores de servicios de aaaManage recuperación de Azure | Documentos de Microsoft"
description: "Use este tutorial toolearn cómo los servicios de recuperación de Azure toomanage almacenes de credenciales y los servidores."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: b4c35c86faa0828b3c63a13b85c095c0cbaba50e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a>Supervisión y administración de almacenes y servidores de los Servicios de recuperación de Azure para máquinas Windows
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-manage-windows-server.md)
> * [Clásico](backup-azure-manage-windows-server-classic.md)
>
>

En este artículo encontrará información general del programa Hola a copia de seguridad tareas de administración y supervisión disponibles a través de hello el agente de copia de seguridad de Microsoft Azure hello y portal de Azure. En este artículo se asume que ya tiene una suscripción de Azure y que ha creado al menos un almacén de Recovery Services.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a>Apertura de un almacén de Recovery Services

panel de almacén de servicios de recuperación de Hello muestra detalles de Hola o los atributos de un almacén de servicios de recuperación.

1. Inicie sesión en toohello [Portal de Azure](https://portal.azure.com/) con su suscripción de Azure.
2. En el menú del concentrador hello, haga clic en **más servicios**.

    ![Apertura de la lista de almacenes de Recovery Services paso 1.](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. Desea tooopen un almacén de servicios de recuperación. En el cuadro de diálogo de hello, comience a escribir **servicios de recuperación**. Cuando empiece a escribir, se filtrará la lista de hello en función de los datos especificados. Haga clic en **servicios de recuperación de los almacenes de credenciales** toodisplay lista de hello de servicios de recuperación de los almacenes de credenciales en su suscripción.

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    Abre la lista de Hola de almacenes de servicios de recuperación.

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. En lista de Hola de almacenes de credenciales, seleccione nombre de Hola de hello almacén de servicios de recuperación que desee tooopen. se abre la hoja de panel de almacén de servicios de recuperación de Hola.

    ![panel del almacén de Servicios de recuperación](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    Ahora que ha abierto el almacén de servicios de recuperación de hello, lleve a cabo cualquiera de las tareas de supervisión o administración de Hola.

## <a name="monitor-backup-jobs-and-alerts"></a>Supervisión de trabajos y alertas de copia de seguridad

Supervisar trabajos y almacén de servicios de recuperación de las alertas de hello panel, donde verá:

* Detalles de las alertas de copia de seguridad
* Archivos y carpetas, así como máquinas virtuales de Azure protegidas en la nube de Hola
* Almacenamiento total usado en Azure
* Estado del trabajo de copia de seguridad

![Copia de seguridad de las tareas del panel](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

Haga clic en información de hello en cada uno de estos iconos abrirá la hoja asociado de Hola donde administrar tareas relacionadas.

De arriba Hola de hello panel:

* El icono de configuración proporciona acceso a las tareas de copia de seguridad disponibles.
* Almacén de copia de seguridad: ayuda a realizar una copia de nuevos archivos y carpetas (o máquinas virtuales de Azure) servicios de recuperación de toohello.
* Delete: si el almacén de servicios de recuperación ya no se está usando, puede eliminarla toofree liberar espacio de almacenamiento. Delete solo se habilita después de que todos los servidores protegidos que se haya eliminado del almacén de Hola.

![Copia de seguridad de las tareas del panel](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a>Alertas de copias de seguridad mediante el agente de Azure Backup:
| Nivel de alerta | Alertas enviadas |
| --- | --- |
| Crítico |Error de copia de seguridad, error de recuperación |
| Warning (Advertencia) |Copia de seguridad completada con advertencias (si no se copian archivos de menos de cien debido a problemas de toocorruption y más de un millón de archivos se copia correctamente) |
| Informativo |None |

## <a name="manage-backup-alerts"></a>Administración de alertas de copia de seguridad
Haga clic en hello **alertas de copia de seguridad** icono tooopen hello **alertas de copia de seguridad** hoja y administrar las alertas.

![Alertas de copias de seguridad](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

mosaico muestra las alertas de copia de seguridad de Hola Hola número de:

* alertas críticas sin resolver en las últimas 24 horas
* alertas de advertencia sin resolver en las últimas 24 horas

Al hacer clic en cada uno de estos vínculos le toohello **alertas de copia de seguridad** hoja con una vista filtrada de estas alertas (críticas o de advertencia).

Desde la hoja de alertas de copia de seguridad de hello,:

* Elija hello tooinclude de información adecuada con las alertas.

    ![Elegir columnas](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* Filtrar alertas por gravedad, el estado y la hora de inicio y finalización.

    ![Filtrar alertas](./media/backup-azure-manage-windows-server/filter-alerts.png)
* Configure las notificaciones según la gravedad, la frecuencia y los destinatarios, y active o desactive las alertas.

    ![Filtrar alertas](./media/backup-azure-manage-windows-server/configure-notifications.png)

Si **por la alerta** se selecciona como hello **notificar** frecuencia se produce ninguna agrupación o la reducción de los correos electrónicos. Cada alerta generará una notificación. Ésta es configuración predeterminada de hello y correo electrónico de resolución de hello también se envía inmediatamente.

Si **implícita por hora** se selecciona como hello **notificar** frecuencia un correo electrónico se envía el usuario toohello que les indica que hay no resuelta nuevas alertas generadas en hello última hora. Se envía un correo electrónico de resolución final Hola de hora de Hola.

Las alertas se pueden enviar por hello siguientes niveles de gravedad:

* Crítico
* Warning (Advertencia)
* informativo

Desactivar alerta Hola con hello **desactivar** botón en la hoja de detalles del trabajo de Hola. Al hacer clic en Desactivar, puede proporcionar notas de resolución.

Elegir columnas de hello desea tooappear como parte de la alerta de hello con hello **Elegir columnas** botón.

> [!NOTE]
> De hello **configuración** hoja, administrar alertas de copia de seguridad seleccionando **supervisión e informes > alertas y eventos > alertas de copia de seguridad** y, a continuación, haga clic en **filtro** o  **Configurar notificaciones**.
>
>

## <a name="manage-backup-items"></a>Administración de elementos de copia de seguridad
Administrar copias de seguridad local ahora está disponible en el portal de administración de Hola. Sección de copia de seguridad de Hola de, en el panel de Hola Hola **elementos de copia de seguridad** icono muestra el número de Hola de elementos de copia de seguridad protegidos toohello almacén.

Haga clic en **carpetas de archivos** Hola icono elementos de copia de seguridad.

![Icono Elementos de copia de seguridad](./media/backup-azure-manage-windows-server/backup-items-tile.png)

Elementos de copia de seguridad de Hello hoja se abre con hello Filtrar conjunto tooFile-carpeta donde verá cada copia de seguridad específica artículo anotado.

![Elementos de copia de seguridad](./media/backup-azure-manage-windows-server/backup-item-list.png)

Si selecciona un elemento específico de copia de seguridad de la lista de hello, puede ver detalles esenciales de Hola para ese elemento.

> [!NOTE]
> De hello **configuración** hoja, administrar archivos y carpetas mediante la selección **elementos protegidos > elementos de copia de seguridad** y, a continuación, seleccione **carpetas de archivos** de hello menú desplegable.
>
>

![Elementos de copia de seguridad en la configuración](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a>Administración de trabajos de copia de seguridad
Trabajos de copia de seguridad local (al servidor local de hello es hacer una copia de seguridad tooAzure) y las copias de seguridad de Azure están visibles en el panel de Hola.

En la sección de copias de seguridad del panel de Hola Hola, mosaico de trabajo de copia de seguridad de hello muestra número Hola de trabajos:

* En curso
* no se pudo Hola últimas 24 horas.

toomanage los trabajos de copia de seguridad, haga clic en hello **trabajos de copia de seguridad** icono, que abre una hoja de trabajos de copia de seguridad de Hola.

![Elementos de copia de seguridad en la configuración](./media/backup-azure-manage-windows-server/backup-jobs.png)

Modificar información de hello disponible en la hoja de trabajos de copia de seguridad de hello con hello **Elegir columnas** situado en la parte superior de Hola de página de Hola.

Hola de uso **filtro** tooselect botón entre los archivos y carpetas y copia de seguridad de máquina virtual de Azure.

Si no ve la copia de seguridad de archivos y carpetas, haga clic en **filtro** situado en la parte superior de Hola de página de Hola y seleccione **archivos y carpetas** desde el menú de tipo de elemento de saludo.

> [!NOTE]
> De hello **configuración** hoja, administrar los trabajos de copia de seguridad seleccionando **supervisión e informes > trabajos > trabajos de copia de seguridad** y, a continuación, seleccione **carpetas de archivos** de colocación de Hola tecla menú.
>
>

## <a name="monitor-backup-usage"></a>Supervisión del uso de Copia de seguridad
En la sección de copias de seguridad del panel de Hola Hola, icono de uso de copia de seguridad de hello muestra el almacenamiento de hello usado en Azure. El uso de almacenamiento se proporciona para:

* Uso de almacenamiento LRS asociada con el almacén de hello en la nube
* Uso de almacenamiento de nube GRS asociada con el almacén de Hola

## <a name="manage-your-production-servers"></a>Administración de los servidores de producción
Haga clic en los servidores de producción de toomanage **configuración**.

En Administrar, haga clic en **Infraestructura de copia de seguridad > Servidores de producción**.

listas de hoja de servidores de producción de Hello de todos los servidores de producción disponibles. Haga clic en un servidor en los detalles del servidor de hello lista tooopen Hola.

![Elementos protegidos](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-hello-azure-backup-agent"></a>Agente de copia de seguridad de Azure Hola abierto
Abra hello **agente de copia de seguridad de Microsoft Azure** (encontrarlo buscando su equipo para *copia de seguridad de Microsoft Azure*).

![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)

De hello **acciones** disponible en hello derecha de la consola de agente de copia de seguridad de hello realizar Hola después de las tareas de administración:

* Registrar un servidor
* Programación de una copia de seguridad
* Realizar una copia de seguridad en ese momento
* Cambiar propiedades

![Acciones de la consola del agente de Microsoft Azure Backup](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> demasiado**recuperar datos**, consulte [restaurar archivos tooa Windows server o el equipo cliente de Windows](backup-azure-restore-windows-server.md).
>
>

## <a name="modify-hello-backup-schedule"></a>Modificar programación de copia de seguridad de Hola
1. En el agente de copia de seguridad de Microsoft Azure hello, haga clic en **programar copias de seguridad**.

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. Hola **Asistente para la programación de copia de seguridad** deje hello **realizar cambios horas o los elementos de toobackup** opción seleccionada y haga clic en **siguiente**.

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. Si desea tooadd o cambiar elementos en hello **seleccionar elementos tooBackup** pantalla haga clic en **agregar elementos**.

    También puede establecer **configuración de exclusión** desde esta página del Asistente para saludo. Si desea que los archivos tooexclude o tipos de archivo leen el procedimiento de Hola para agregar [configuración de exclusión](#manage-exclusion-settings).
4. Seleccione Hola archivos y carpetas que desee tooback seguridad y haga clic en **bien**.

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. Especificar hello **programar copia de seguridad** y haga clic en **siguiente**.

    Puede programar copias de seguridad diarias (un máximo de 3 veces al día) o semanales.

    ![Elementos para la copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > Especificar la programación de copia de seguridad de Hola se explica con detalle en esta [artículo](backup-azure-backup-cloud-as-tape.md).
   >

6. Seleccione hello **directiva de retención** para copia de seguridad de Hola y haga clic en **siguiente**.

    ![Elementos para la copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. En hello **confirmación** Hola revisar la información de la pantalla y haga clic en **finalizar**.
8. Una vez que el Asistente de hello finaliza la creación de hello **programar copia de seguridad**, haga clic en **cerrar**.

    Después de modificar la protección, puede confirmar que las copias de seguridad se activan correctamente por van toohello **trabajos** ficha y confirmar que los cambios se reflejan en hello trabajos de copia de seguridad.

## <a name="enable-network-throttling"></a>Habilitación de la limitación de la red

agente de copia de seguridad de Azure Hola incluye una pestaña de limitación que permite toocontrol uso de ancho de banda de red durante la transferencia de datos. Este control puede ser útil si necesita tooback los datos durante las horas laborables, pero no desea hello toointerfere de proceso de copia de seguridad con otro tráfico de internet. Limitación de datos transferencia aplica tooback seguridad y restaurar las actividades.  

tooenable limitación:

1. Hola **agente de copia de seguridad**, haga clic en **cambiar las propiedades de**.
2. En Hola ** limitación ficha, seleccione **Habilitar límite para las operaciones de copia de seguridad de uso de ancho de banda de internet**.

    ![Limitación de la red](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    Una vez habilitada la limitación, especifique Hola permitido ancho de banda para transfirieron datos de copia de seguridad durante la **horas laborables** y **horas de descanso**.

    los valores de ancho de banda de Hello comienzan en 512 kilobytes por segundo (Kbps) y pueden crecer hasta too1023 megabytes por segundo (Mbps). También puede designar el inicio de Hola y de fin para **horas laborables**, y los días de la semana de Hola se consideran trabajo días. tiempo de Hello fuera Hola designado horas laborables es considerada toobe horas de descanso.
3. Haga clic en **Aceptar**.

## <a name="manage-exclusion-settings"></a>Administración de la configuración de exclusión
1. Abra hello **agente de copia de seguridad de Microsoft Azure** (puede encontrarlo buscando en el equipo para *copia de seguridad de Microsoft Azure*).

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. En el agente de copia de seguridad de Microsoft Azure hello, haga clic en **programar copias de seguridad**.

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. Hola Asistente para la programación de copia de seguridad deje hello **realizar cambios horas o los elementos de toobackup** opción seleccionada y haga clic en **siguiente**.

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. Haga clic en **Configuración de exclusión**.

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. Haga clic en **Agregar exclusión**.

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. Seleccionar ubicación de hello y, a continuación, haga clic en **Aceptar**.

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. Agregar extensión de archivo de Hola Hola **tipo de archivo** campo.

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    Adición de una extensión .mp3

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    tooadd otra extensión, haga clic en **Agregar exclusión** y escriba otra extensión de tipo de archivo (agregar una extensión de JPEG).

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. Cuando haya agregado todas las extensiones de hello, haga clic en **Aceptar**.
9. Continuar a través de hello Asistente para la programación de copia de seguridad haciendo clic en **siguiente** hasta hello **página de confirmación**, a continuación, haga clic en **finalizar**.

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes
**Q1. estado del trabajo de copia de seguridad de Hello muestra como completado en hello agente de copia de seguridad de Azure, ¿por qué no se obtener reflejan inmediatamente en el portal?**

R1. No existe se en retraso máximo de 15 minutos entre el estado del trabajo de copia de seguridad de Hola refleja en el agente de copia de seguridad de Azure de Hola y Hola portal de Azure.

**¿Q.2 cuando se produce un error en un trabajo de copia de seguridad, cuánto tiempo tarda tooraise una alerta?**

A.2 una alerta se genera en 20 minutos de hello Azure error de copia de seguridad.

**P3. ¿Hay algún caso en el que no se envíe ningún correo electrónico si se configuran las notificaciones?**

R3. A continuación se muestran casos de hello cuando no se enviará la notificación de hello en alertas irrelevantes de orden tooreduce hello:

* Si se configuran las notificaciones por hora y una alerta se genera y resuelto durante la hora de Hola
* Se canceló el trabajo.
* Se produjo un error en el segundo trabajo de copia de seguridad porque el trabajo de copia de seguridad original está en curso.

## <a name="troubleshooting-monitoring-issues"></a>Solución de problemas de supervisión
**Problema:** trabajos y alertas desde el agente de copia de seguridad de Azure de hello no aparecen en el portal de Hola.

**Pasos para solucionar problemas:** Hola proceso, ```OBRecoveryServicesManagementAgent```, envía Hola toohello de datos de alerta y el trabajo de servicio de copia de seguridad de Azure. En ocasiones este proceso puede quedar atascado o apagado.

1. no se está ejecutando el proceso de hello tooverify, abra **el Administrador de tareas** y compruebe si hello ```OBRecoveryServicesManagementAgent``` proceso se está ejecutando.
2. Suponiendo que no se está ejecutando el proceso de hello, abra **el Panel de Control** y examinar la lista de hello de servicios. Inicie o reinicie el **agente de administración de Microsoft Azure Recovery Services**.

    Para obtener más información, examine los registros de hello en:<br/>
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` Por ejemplo:<br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a>Pasos siguientes
* [Restauración de Windows Server o el cliente de Windows desde Azure](backup-azure-restore-windows-server.md)
* toolearn más información acerca de la copia de seguridad de Azure, consulte [información general sobre la copia de seguridad de Azure](backup-introduction-to-azure-backup.md)
* Visite hello [foro de copia de seguridad de Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)
