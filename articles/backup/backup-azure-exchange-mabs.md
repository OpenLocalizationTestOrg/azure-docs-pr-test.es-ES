---
title: Copia de seguridad de un servidor Exchange en Azure Backup con el servidor de copia de seguridad de Azure | Microsoft Docs
description: "Obtenga información sobre cómo realizar una copia de seguridad de un servidor Exchange en Azure Backup con el Azure Backup Server"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: e46557e8-2eaf-4ee0-99ea-00fbb8687dca
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 60b784fd00013c2b9504f8635c6b5c4c592563be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-azure-backup-server"></a>Realice una copia de seguridad de un servidor Exchange en Azure Backup con el servidor de copia de seguridad de Azure
En este artículo se describe cómo configurar un servidor de copia de seguridad de Microsoft Azure (MABS) para realizar una copia de seguridad de un servidor Microsoft Exchange en Azure.  

## <a name="prerequisites"></a>Requisitos previos
Antes de continuar, asegúrese de que el servidor de copia de seguridad de Azure esté [instalado y preparado](backup-azure-microsoft-azure-backup.md).

## <a name="mabs-protection-agent"></a>Agente de protección MABS
Para instalar al agente de protección MABS en el servidor Exchange, siga estos pasos:

1. Asegúrese de que los firewalls estén configurados correctamente. Consulte [Configuración de excepciones de firewall para el agente](https://technet.microsoft.com/library/Hh758204.aspx).
2. Instale el agente en el servidor Exchange; para ello, haga clic en **Administración > Agentes > Instalar** en la consola de administrador de MABS. Consulte [Instalación del agente de protección MABS](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) para ver pasos detallados.

## <a name="create-a-protection-group-for-the-exchange-server"></a>Creación de un grupo de protección para el servidor Exchange
1. En la consola de administrador de MABS, haga clic en **Protección** y luego en **Nuevo** en la cinta de herramientas para abrir el asistente **Crear nuevo grupo de protección**.
2. En la pantalla **Bienvenido** del asistente, haga clic en **Siguiente**.
3. En la pantalla **Seleccionar tipo de grupo de protección**, seleccione **Servidores** y haga clic en **Siguiente**.
4. Seleccione la base de datos del servidor Exchange que desea proteger y haga clic en **Siguiente**.

   > [!NOTE]
   > Si va a proteger Exchange 2013, compruebe en [Requisitos previos de Exchange 2013](https://technet.microsoft.com/library/dn751029.aspx).
   >
   >

    En el ejemplo siguiente, está seleccionada la base de datos de Exchange 2010.

    ![Seleccionar a miembros del grupo](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. Seleccione el método de protección de datos.

    Asigne un nombre al grupo de protección y, a continuación, seleccione las dos opciones siguientes:

   * Deseo protección a corto plazo mediante disco.
   * Deseo protección en línea.
6. Haga clic en **Next**.
7. Seleccione la opción **Ejecutar Eseutil para comprobar la integridad de los datos** si desea comprobar la integridad de las bases de datos de Exchange Server.

    Después de seleccionar esta opción, se ejecutará una comprobación de coherencia de copia de seguridad en MABS para evitar el tráfico de E/S que se genera al ejecutar el comando **eseutil** en el servidor Exchange.

   > [!NOTE]
   > Para usar esta opción, debe copiar los archivos Ese.dll y Eseutil.exe en el directorio C:\Archivos de programa\Microsoft Azure Backup\DPM\DPM\bin del servidor MAB. De lo contrario, se desencadena el siguiente error:   
   > ![Error de eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)
   >
   >
8. Haga clic en **Siguiente**.
9. Seleccione la base de datos para **Copia de seguridad de copia**, y luego haga clic en **Siguiente**.

   > [!NOTE]
   > Si no selecciona "Copia de seguridad completa" al menos para una copia de DAG de una base de datos, no se truncarán los registros.
   >
   >
10. Configure los objetivos de **Copia de seguridad a corto plazo** y haga clic en **Siguiente**.
11. Revise el espacio en disco disponible y haga clic en **Siguiente**.
12. Seleccione la hora a la que el servidor MAB creará la replicación inicial y haga clic en **Siguiente**.
13. Seleccione las opciones de comprobación de coherencia y haga clic en **Siguiente**.
14. Elija la base de datos de la que desea realizar una copia de seguridad en Azure y haga clic en **Siguiente**. Por ejemplo:

    ![Especificar datos de protección en línea](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. Defina la programación de **Copia de seguridad de Azure** y luego haga clic en **Siguiente**. Por ejemplo:

    ![Especificar programación de copia de seguridad en línea](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > Los puntos de recuperación de notas en línea están basados en los puntos de recuperación completos rápidos. Por lo tanto, debe programar el punto de recuperación en línea después de la hora especificada para el punto de recuperación completo rápido.
    >
    >
16. Configure la directiva de retención para **Copia de seguridad de Azure** y luego haga clic en **Siguiente**.
17. Elija una opción de replicación en línea y haga clic en **Siguiente**.

    Si tiene una base de datos grande, se puede tardar mucho tiempo en crear la copia de seguridad inicial a través de la red. Para evitar este problema, puede crear una copia de seguridad sin conexión.  

    ![Especificar directiva de retención en línea](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. Confirme la configuración y haga clic en **Crear grupo**.
19. Haga clic en **Cerrar**.

## <a name="recover-the-exchange-database"></a>Recuperación de la base de datos de Exchange
1. Para recuperar una base de datos de Exchange, haga clic en **Recuperación** en la consola de administrador de MABS.
2. Busque la base de datos de Exchange que desea recuperar.
3. Seleccione un punto de recuperación en línea en la lista desplegable *Hora de recuperación* .
4. Haga clic en **Recuperar** para iniciar el **Asistente para recuperación**.

Para los puntos de recuperación en línea, existen cinco tipos de recuperación:

* **Recuperar en ubicación original de servidor de Exchange :** los datos se recuperarán en el servidor Exchange original.
* **Recuperar en otra base de datos en un servidor de Exchange:** los datos se recuperarán en otra base de datos de otro servidor Exchange.
* **Recuperar en una base de datos de recuperación:** los datos se recuperarán en una base de datos de recuperación de Exchange (RDB).
* **Copiar en una carpeta de red:** los datos se recuperarán en una carpeta de red.
* **Copiar en cinta:** si tiene una biblioteca de cintas o una unidad de cinta independiente conectada y configurada en MABS, el punto de recuperación se copiará en una cinta libre.

    ![Elegir replicación en línea](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a>Pasos siguientes
* [Preguntas más frecuentes de Copia de seguridad de Azure](backup-azure-backup-faq.md)
