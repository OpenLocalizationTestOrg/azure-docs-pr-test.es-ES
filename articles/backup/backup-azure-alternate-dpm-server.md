---
title: datos de aaaRecover desde un servidor de copia de seguridad de Azure | Documentos de Microsoft
description: "Recuperar datos de hello ha protegido del almacén de servicios de recuperación de tooa de cualquier almacén de toothat registrados del servidor de copia de seguridad de Azure."
services: backup
documentationcenter: 
author: nkolli1
manager: shreeshd
editor: 
ms.assetid: a55f8c6b-3627-42e1-9d25-ed3e4ab17b1f
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: adigan;giridham;trinadhk;markgal
ms.openlocfilehash: 74847880e646c3c4f198afe318f1db30363d137a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="recover-data-from-azure-backup-server"></a>Recuperación de datos de Azure Backup Server
Puede usar datos de servidor de copia de seguridad de Azure toorecover hello que ha hecho tooa que del almacén de servicios de recuperación. proceso de Hola para hacerlo por lo que se integra en la consola de administración de servidor de copia de seguridad de Azure de Hola y es similar flujo de trabajo de recuperación de toohello para otros componentes de copia de seguridad de Azure.

> [!NOTE]
> En este artículo es aplicable a [System Center Data Protection Manager 2012 R2 con UR7 o versiones posteriores] (https://support.microsoft.com/en-us/kb/3065246), combinada con hello [agente de copia de seguridad de Azure más reciente](http://aka.ms/azurebackup_agent).
>
>

datos de toorecover desde un servidor de copia de seguridad de Azure:

1. De hello **recuperación** ficha de hello consola de administración del servidor de copia de seguridad de Azure, haga clic en **'Agregar DPM externo'** (en hello parte superior izquierda de la pantalla de bienvenida).   
    ![Agregar DPM externo](./media/backup-azure-alternate-dpm-server/add-external-dpm.png)
2. Descarga nueva **del almacén de credenciales** del almacén de hello asociado con hello **servidor de copia de seguridad de Azure** donde se va a recuperar datos de hello, elegir Hola servidor de copia de seguridad de Azure en lista de Hola de servidores de copia de seguridad de Azure registrado en el almacén de servicios de recuperación de Hola y proporcionar hello **frase de contraseña** asociados con el servidor de hello cuyos datos se va a recuperar.

    ![Credenciales externas de DPM](./media/backup-azure-alternate-dpm-server/external-dpm-credentials.png)

   > [!NOTE]
   > Sólo servidores de copia de seguridad de Azure asociadas con hello mismo almacén de registro puede recuperar los datos de todas las demás.
   >
   >

    Una vez Hola servidor externo de copia de seguridad de Azure correctamente agregado, puede examinar los datos de Hola de servidor externo de Hola y Hola servidor local de copia de seguridad de Azure de hello **recuperación** ficha.
3. Examinar Hola disponible lista de servidores de producción protegidos por Hola servidor externo de copia de seguridad de Azure y seleccione el origen de datos adecuado de Hola.

    ![Ir al servidor DPM externo](./media/backup-azure-alternate-dpm-server/browse-external-dpm.png)
4. Seleccione **Hola mes y año** de hello **puntos de recuperación** de lista desplegable, seleccione Hola necesario **fechaderecuperación** para cuando el punto de recuperación de hello era Hola creada y, a continuación, seleccione **Tiempo de recuperación**.

    Aparece una lista de archivos y carpetas en el panel inferior de hello, que se pueden examinar y recupera la ubicación de tooany.

    ![Puntos de recuperación del servidor DPM externo](./media/backup-azure-alternate-dpm-server/external-dpm-recoverypoint.png)
5. Haga clic en el elemento apropiado de Hola y haga clic en **recuperar**.

    ![Recuperación del DPM externo](./media/backup-azure-alternate-dpm-server/recover.png)
6. Hola de revisión **recuperar selección**. Comprobar datos Hola y el tiempo de copia de seguridad de Hola que se está recuperando, así como el origen de Hola desde el que se creó la copia de seguridad de Hola. Si la selección de hello es incorrecta, haga clic en **cancelar** punto de recuperación adecuado de toonavigate toorecovery back-ficha tooselect. Si la selección de hello es correcta, haga clic en **siguiente**.

    ![Resumen de recuperación del DPM externo](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-summary.png)
7. Seleccione **recuperar en ubicación alternativa de tooan**. **Examinar** toohello ubicación correcta para la recuperación de Hola.

    ![Ubicación alternativa de la recuperación del DPM externo](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-alternate-location.png)
8. Elija la opción Hola relacionados con demasiado**crear copia**, **omitir**, o **sobrescribir**.

   * **Crear copia** -crea una copia del archivo hello si hay un conflicto de nombres.
   * **Omitir** : si hay un conflicto de nombres, no se recupera archivo hello que deja el archivo original de hello.
   * **Sobrescribir** : si hay un conflicto de nombres, sobrescribe la copia existente de Hola de archivo hello.

     Elija la opción adecuada de hello demasiado**Restaurar seguridad**. Puede aplicar la configuración de seguridad de Hola Hola del equipo de destino donde se va a recuperar datos de Hola o configuración de seguridad de Hola que estaban tooproduct aplicable en tiempo de Hola se creó el punto de recuperación de Hola.

     Identificar si un **notificación** se envían una vez por recuperación de Hola se complete correctamente.

     ![Notificaciones de recuperación del DPM externo](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-notifications.png)
9. Hola **resumen** pantalla muestra opciones de hello elegidos hasta ahora. Una vez que pulses **"Recuperar"**, datos hello están toohello recuperada local que corresponda ubicación.

    ![Resumen de las opciones de recuperación del DPM externo](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-options-summary.png)

   > [!NOTE]
   > se puede supervisar el trabajo de recuperación de Hola Hola **supervisión** ficha del programa Hola a servidor de copia de seguridad de Azure.
   >
   >

    ![Supervisión de la recuperación](./media/backup-azure-alternate-dpm-server/monitoring-recovery.png)
10. Puede hacer clic en **borrar DPM externo** en hello **recuperación** pestaña de vista de Hola de tooremove de servidor DPM del servidor DPM externo Hola Hola.

    ![Borrar DPM externo](./media/backup-azure-alternate-dpm-server/clear-external-dpm.png)

## <a name="troubleshooting-error-messages"></a>Solución de mensajes de error
| Nº | Mensaje de error | Pasos para solucionar problemas |
|:---:|:--- |:--- |
| 1. |Este servidor no es el almacén de toohello registrado especificado mediante credenciales de almacén de Hola. |**Causa:** este error aparece cuando el archivo de credenciales de almacén de hello seleccionado no pertenece toohello del almacén de servicios de recuperación asociados con el servidor de copia de seguridad de Azure en qué Hola se intenta la recuperación. <br> **Solución:** archivo de credenciales de almacén de Hola de descarga de Hola Hola del toowhich del almacén de servicios de recuperación está registrado el servidor de copia de seguridad de Azure. |
| 2. |Datos recuperables hello no están disponibles o servidor de hello seleccionado no es un servidor DPM. |**Causa:** no hay ningún otro servidores de copia de seguridad de Azure toohello registrado servicios de recuperación almacén, o servidores de hello todavía no carga los metadatos de Hola o servidor seleccionado hello no es un servidor de copia de seguridad de Azure (también conocido como Windows Server o cliente de Windows). <br> **Solución:** si hay otro almacén de servicios de recuperación de servidores de copia de seguridad de Azure toohello registrado, asegúrese de que ese agente de copia de seguridad de Azure hello más reciente está instalado. <br>Si hay otro almacén de servicios de recuperación de servidores de copia de seguridad de Azure toohello registrado, espere un día después de proceso de recuperación de instalación toostart Hola. trabajo nocturno Hola cargará los metadatos de Hola para toocloud de las copias de seguridad de todos los Hola protegido. datos de Hello estarán disponibles para la recuperación. |
| 3. |Ningún otro servidor DPM es el almacén de toothis registrados. |**Causa:** no hay ningún otro servidor de copia de seguridad de Azure que son almacén toohello registrado desde qué hello es intentos de recuperación.<br>**Solución:** si hay otro almacén de servicios de recuperación de servidores de copia de seguridad de Azure toohello registrado, asegúrese de que ese agente de copia de seguridad de Azure hello más reciente está instalado.<br>Si hay otro almacén de servicios de recuperación de servidores de copia de seguridad de Azure toohello registrado, espere un día después de proceso de recuperación de instalación toostart Hola. trabajo nocturno Hola carga Hola metadatos para todos los toocloud de las copias de seguridad protegido. datos de Hello estarán disponibles para la recuperación. |
| 4. |Hola frase de contraseña de cifrado proporcionada no coincide con la frase de contraseña asociada con hello siguiente servidor:**<server name>** |**Causa:** Hola frase de contraseña de cifrado usada en proceso de Hola de cifrado de datos de saludo de datos del servidor de copia de seguridad de hello Azure que se va a recuperar no coincide con hello frase de contraseña de cifrado proporcionada. agente de Hello es datos de hello toodecrypt no se puede. Hola, por tanto, se produce un error de recuperación.<br>**Solución:** proporcione Hola exacta misma frase de contraseña asociada Hola servidor de copia de seguridad de Azure cuyos datos se va a recuperar. |

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

### <a name="why-cant-i-add-an-external-dpm-server-after-installing-ur7-and-latest-azure-backup-agent"></a>¿Por qué no puedo agregar un servidor DPM externo después de instalar el paquete acumulativo de actualizaciones 7 y el agente de Azure Backup más reciente?

Para hello servidores DPM con orígenes de datos que protegió toohello en la nube (con un paquete acumulativo de actualizaciones anteriores a actualizar paquete acumulativo de actualizaciones 7), debe esperar al menos un día después de instalar hello UR7 y agente de copia de seguridad de Azure más reciente, toostart **server agregar DPM externo** . Hola un día el período de tiempo es necesario tooupload Hola metadatos de tooAzure de grupos de protección de DPM de Hola. Metadatos del grupo de protección se cargan Hola la primera vez a través de una tarea nocturna.

### <a name="what-is-hello-minimum-version-of-hello-microsoft-azure-recovery-services-agent-needed"></a>¿Qué es la versión mínima de Hola de agente de servicios de recuperación de Microsoft Azure Hola necesitado?

versión mínima de Hola de agente de servicios de recuperación de Microsoft Azure de hello, o el agente de copia de seguridad de Azure, tooenable requiere esta característica es 2.0.8719.0.  versión del agente de tooview Hola: abra el Panel de Control  **>**  elementos del Panel de Control de todos los  **>**  programas y características  **>**  Agente de servicios de recuperación de Microsoft Azure. Si la versión de hello es inferior a 2.0.8719.0, descargue e instale hello [agente de copia de seguridad de Azure más reciente](https://go.microsoft.com/fwLink/?LinkID=288905).

![Borrar DPM externo](./media/backup-azure-alternate-dpm-server/external-dpm-azurebackupagentversion.png)

## <a name="next-steps"></a>Pasos siguientes:
•   [Preguntas más frecuentes de Azure Backup](backup-azure-backup-faq.md)
