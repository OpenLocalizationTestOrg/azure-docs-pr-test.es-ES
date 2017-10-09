---
title: aaaBack seguridad un tooAzure de Exchange server copia de seguridad con el servidor de copia de seguridad de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooback seguridad un tooAzure del servidor de Exchange de copia de seguridad utilizando el servidor de copia de seguridad de Azure"
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
ms.openlocfilehash: db874161151fc57c5b79c41531e18d577f567f66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-azure-backup-server"></a>Hacer copia de seguridad de un tooAzure de Exchange server copia de seguridad con el servidor de copia de seguridad de Azure
Este artículo se describe cómo tooconfigure tooback de servidor de copia de seguridad de Microsoft Azure (MABS) de un tooAzure de servidor de Microsoft Exchange.  

## <a name="prerequisites"></a>Requisitos previos
Antes de continuar, asegúrese de que el servidor de copia de seguridad de Azure esté [instalado y preparado](backup-azure-microsoft-azure-backup.md).

## <a name="mabs-protection-agent"></a>Agente de protección MABS
agente de protección de MABS tooinstall hello en el servidor de Exchange de hello, siga estos pasos:

1. Asegúrese de que los firewalls de hello estén configurados correctamente. Vea [configurar excepciones de firewall para el agente de hello](https://technet.microsoft.com/library/Hh758204.aspx).
2. Instalar agente de hello en el servidor de Exchange de hello haciendo clic en **Administración > agentes > instalar** en la consola de administrador de MABS. Vea [agente de protección de instalación hello MABS](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) para obtener pasos detallados.

## <a name="create-a-protection-group-for-hello-exchange-server"></a>Cree un grupo de protección para Exchange server de Hola
1. En la consola de administrador de MABS hello, haga clic en **protección**y, a continuación, haga clic en **New** en Hola Hola de tooopen de cinta de opciones de herramienta **crear nuevo grupo de protección** asistente.
2. En hello **bienvenida** pantalla del asistente, haga clic hello **siguiente**.
3. En hello **Seleccionar tipo de grupo de protección** pantalla, seleccione **servidores** y haga clic en **siguiente**.
4. Base de datos de servidor de Exchange de hello SELECT que desee tooprotect y haga clic en **siguiente**.

   > [!NOTE]
   > Si va a proteger Exchange 2013, compruebe hello [requisitos previos de Exchange 2013](https://technet.microsoft.com/library/dn751029.aspx).
   >
   >

    En el siguiente ejemplo de Hola, base de datos de Exchange 2010 Hola está seleccionada.

    ![Seleccionar a miembros del grupo](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. Seleccionar método de protección de datos de Hola.

    Nombre de grupo de protección de hello y, a continuación, seleccione ambos Hola siguientes opciones:

   * Deseo protección a corto plazo mediante disco.
   * Deseo protección en línea.
6. Haga clic en **Siguiente**.
7. Seleccione hello **integridad de los datos toocheck ejecutar Eseutil** opción si desea que la integridad de hello toocheck de bases de datos de Exchange Server de Hola.

    Después de seleccionar esta opción, la comprobación de coherencia de copia de seguridad se ejecutará en MABS tooavoid Hola E/S el tráfico que se genera mediante la ejecución de hello **eseutil** comando en el servidor de Exchange de Hola.

   > [!NOTE]
   > toouse esta opción, debe copiar Hola Ese.dll y Eseutil.exe archivos toohello C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directorio Hola AM servidor. En caso contrario, se desencadena Hola siguiente error:  
   > ![Error de eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)
   >
   >
8. Haga clic en **Siguiente**.
9. Base de datos seleccione hello **copia de seguridad**y, a continuación, haga clic en **siguiente**.

   > [!NOTE]
   > Si no selecciona "Copia de seguridad completa" al menos para una copia de DAG de una base de datos, no se truncarán los registros.
   >
   >
10. Configure los objetivos de Hola para **copia de seguridad a corto plazo**y, a continuación, haga clic en **siguiente**.
11. Revise el espacio en disco disponible hello y, a continuación, haga clic en **siguiente**.
12. Seleccione hora de hello en qué Hola AM Server creará la replicación inicial de hello y, a continuación, haga clic en **siguiente**.
13. Seleccione las opciones de comprobación de coherencia de hello y, a continuación, haga clic en **siguiente**.
14. Elija la base de datos de Hola que desee tooback seguridad tooAzure y, a continuación, haga clic en **siguiente**. Por ejemplo:

    ![Especificar datos de protección en línea](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. Definir programación Hola para **copia de seguridad de Azure**y, a continuación, haga clic en **siguiente**. Por ejemplo:

    ![Especificar programación de copia de seguridad en línea](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > Los puntos de recuperación de notas en línea están basados en los puntos de recuperación completos rápidos. Por lo tanto, debe programar el punto de recuperación en línea hello después del horario de Hola que se especifica para hello express punto de recuperación completa.
    >
    >
16. Configurar la directiva de retención de Hola para **copia de seguridad de Azure**y, a continuación, haga clic en **siguiente**.
17. Elija una opción de replicación en línea y haga clic en **Siguiente**.

    Si tiene una base de datos grande, puede tardar mucho tiempo para toobe de copia de seguridad inicial de hello creado a través de red de Hola. tooavoid este problema, puede crear una copia de seguridad sin conexión.  

    ![Especificar directiva de retención en línea](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. Confirmar configuración de hello y, a continuación, haga clic en **crear grupo**.
19. Haga clic en **Cerrar**.

## <a name="recover-hello-exchange-database"></a>Recuperar base de datos de Exchange de Hola
1. toorecover una base de datos de Exchange, haga clic en **recuperación** en la consola de administrador de MABS Hola.
2. Busque la base de datos de Exchange de Hola que desea toorecover.
3. Seleccione un punto de recuperación en línea de hello *tiempo de recuperación* lista desplegable.
4. Haga clic en **recuperar** toostart hello **Asistente para recuperación**.

Para los puntos de recuperación en línea, existen cinco tipos de recuperación:

* **Recuperar la ubicación del servidor de Exchange de toooriginal:** datos Hola sea servidor de Exchange original toohello recuperada.
* **Recuperar base de datos de tooanother en un servidor Exchange:** datos Hola será la base de datos de tooanother recuperada en otro servidor de Exchange.
* **Recuperar la base de datos de recuperación de tooa:** datos Hola será tooan recuperada base de datos de recuperación de Exchange (RDB).
* **Carpeta de red de copia tooa:** datos Hola será la carpeta de red de tooa recuperada.
* **Copie tootape:** si dispone de una biblioteca de cintas o una unidad de cinta independiente que se adjunta y se ha configurado en MABS, punto de recuperación de hello será copiados tooa de cintas libres.

    ![Elegir replicación en línea](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a>Pasos siguientes
* [Preguntas más frecuentes de Copia de seguridad de Azure](backup-azure-backup-faq.md)
