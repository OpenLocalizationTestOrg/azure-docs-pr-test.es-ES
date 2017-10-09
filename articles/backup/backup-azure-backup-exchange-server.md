---
title: aaaBack seguridad un tooAzure de Exchange server copia de seguridad con System Center 2012 R2 DPM | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooback seguridad un tooAzure del servidor de Exchange de copia de seguridad con System Center 2012 R2 DPM"
services: backup
documentationcenter: 
author: MaanasSaran
manager: NKolli1
editor: 
ms.assetid: 13f32256-888e-416e-a78b-40c2a26a5939
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: masaran;jimpark;delhan;trinadhk;markgal
ms.openlocfilehash: fa99296d095c180333474b6d419ebc5ec727547a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-system-center-2012-r2-dpm"></a>Hacer copia de seguridad de un tooAzure de Exchange server copia de seguridad con System Center 2012 R2 DPM
Este artículo se describe cómo tooconfigure una tooback de servidor de System Center 2012 R2 Data Protection Manager (DPM) de un servidor de Microsoft Exchange demasiado Azure Backup.  

## <a name="updates"></a>Actualizaciones
toosuccessfully el servidor DPM de registro Hola con copia de seguridad de Azure, debe instalar Hola último paquete acumulativo de actualizaciones para System Center 2012 R2 DPM y Hola la versión más reciente de hello Azure Backup Agent. Obtener el paquete acumulativo de actualizaciones más reciente de Hola de hello [catálogo de Microsoft](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).

> [!NOTE]
> Para obtener ejemplos de hello en este artículo, se instala la versión 2.0.8719.0 de hello Azure Backup Agent y actualización paquete acumulativo de actualizaciones 6 está instalado en System Center 2012 R2 DPM.
>
>

## <a name="prerequisites"></a>Requisitos previos
Antes de continuar, asegúrese de que todos los Hola [requisitos previos](backup-azure-dpm-introduction.md#prerequisites) para el uso de copia de seguridad de Microsoft Azure se cumplieron las cargas de trabajo tooprotect. Estos requisitos previos Hola siguientes:

* Se ha creado un almacén de copia de seguridad en hello sitio de Azure.
* Credenciales del almacén y agente han sido toohello descargado el servidor DPM.
* Hola agente está instalado en el servidor DPM Hola.
* las credenciales de almacén de Hello eran servidor DPM usa tooregister Hola.
* Si va a proteger Exchange 2016, actualice tooDPM 2012 R2 UR9 o posterior

## <a name="dpm-protection-agent"></a>Agente de protección DPM
agente de protección de DPM tooinstall hello en el servidor de Exchange de hello, siga estos pasos:

1. Asegúrese de que los firewalls de hello estén configurados correctamente. Vea [configurar excepciones de firewall para el agente de hello](https://technet.microsoft.com/library/Hh758204.aspx).
2. Instalar agente de hello en el servidor de Exchange de hello haciendo clic en **Administración > agentes > instalar** en la consola de administrador DPM. Vea [agente de protección DPM Install hello](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) para obtener pasos detallados.

## <a name="create-a-protection-group-for-hello-exchange-server"></a>Cree un grupo de protección para Exchange server de Hola
1. Hola consola de administrador DPM, haga clic en **protección**y, a continuación, haga clic en **New** en Hola Hola de tooopen de cinta de opciones de herramienta **crear nuevo grupo de protección** asistente.
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

    Después de seleccionar esta opción, la comprobación de coherencia de copia de seguridad se ejecutará en hello DPM tooavoid Hola E/S tráfico del servidor que se genera mediante la ejecución de hello **eseutil** comando en el servidor de Exchange de Hola.

   > [!NOTE]
   > toouse esta opción, debe copiar Hola Ese.dll y Eseutil.exe directorio archivos de toohello C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin servidor DPM de Hola. En caso contrario, se desencadena Hola siguiente error:  
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
12. Seleccione hora de hello en qué Hola DPM server creará la replicación inicial de hello y, a continuación, haga clic en **siguiente**.
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
1. Haga clic en una base de datos de Exchange, toorecover **recuperación** Hola consola de administrador DPM.
2. Busque la base de datos de Exchange de Hola que desea toorecover.
3. Seleccione un punto de recuperación en línea de hello *tiempo de recuperación* lista desplegable.
4. Haga clic en **recuperar** toostart hello **Asistente para recuperación**.

Para los puntos de recuperación en línea, existen cinco tipos de recuperación:

* **Recuperar la ubicación del servidor de Exchange de toooriginal:** datos Hola sea servidor de Exchange original toohello recuperada.
* **Recuperar base de datos de tooanother en un servidor Exchange:** datos Hola será la base de datos de tooanother recuperada en otro servidor de Exchange.
* **Recuperar la base de datos de recuperación de tooa:** datos Hola será tooan recuperada base de datos de recuperación de Exchange (RDB).
* **Carpeta de red de copia tooa:** datos Hola será la carpeta de red de tooa recuperada.
* **Copie tootape:** si dispone de una biblioteca de cintas o una unidad de cinta independiente será Hola adjunta y se ha configurado en servidor DPM, el punto de recuperación de hello copiados tooa de cintas libres.

    ![Elegir replicación en línea](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a>Pasos siguientes
* [Preguntas más frecuentes de Copia de seguridad de Azure](backup-azure-backup-faq.md)
