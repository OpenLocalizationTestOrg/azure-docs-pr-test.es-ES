---
title: aaaRestore una sola tabla de copia de seguridad de base de datos de SQL de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toorestore una sola tabla de copia de seguridad de base de datos de SQL Azure."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a>Cómo toorestore una sola tabla desde una copia de seguridad de base de datos de SQL Azure
Puede encontrarse con una situación en la que modificar accidentalmente algunos datos en una base de datos SQL y ahora desea toorecover Hola única afectados tabla. Este artículo describe cómo toorestore una sola tabla en una base de datos de una base de datos SQL de hello [copias de seguridad automáticas](sql-database-automated-backups.md).

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a>Pasos de preparación: cambiar el nombre de tabla de Hola y restaure una copia de base de datos de Hola
1. Identificar la tabla de hello en la base de datos de SQL Azure que desea tooreplace con copia de hello restaurado. Utilice la tabla de Microsoft SQL Management Studio toorename Hola. Por ejemplo, cambiar el nombre de tabla de hello como &lt;nombre de la tabla&gt;_old.
   
   > [!NOTE]
   > tooavoid está bloqueado, asegúrese de que no hay ninguna actividad ejecutar en la tabla de Hola que ha cambiado. Si encuentra algún problema, realice este procedimiento durante una ventana de mantenimiento.
   >

2. Restaurar una copia de seguridad de su punto de tooa de base de datos en el tiempo que desea que toorecover toousing hello [punto-In_Time restaurar](sql-database-recovery-using-backups.md#point-in-time-restore) pasos.
   
   > [!NOTE]
   > nombre de Hola de base de datos de hello restaurar será en formato de marca de tiempo + DBName Hola; Por ejemplo, **Adventureworks2012_2016-01-01T22-12Z**. Este paso no sobrescribe el nombre de base de datos existente de hello en el servidor de Hola. Se trata de una medida de seguridad, y está pensado tooallow se tooverify Hola restaura base de datos antes de quitar la base de datos actual y cambiar el nombre de base de datos de hello restaurar para su uso en producción.
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a>Copiando la tabla Hola de hello restaurado la base de datos mediante el uso de la herramienta de migración de base de datos de SQL de Hola

1. Descargue e instale hello [Asistente para migración de base de datos de SQL](https://sqlazuremw.codeplex.com).
2. Abra Hola Asistente para migración de base de datos de SQL, en hello **Seleccionar proceso** , seleccione **base de datos en analizar/migrar**y, a continuación, haga clic en **siguiente**.

   ![Asistente para migración de Base de datos SQL: seleccionar proceso](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. Hola **conectar tooServer** diálogo cuadro, aplique Hola después de configuración:

   * Nombre del servidor: **su servidor SQL**
   * Autenticación: **Autenticación de SQL Server**
   * Inicio de sesión: **sus datos de inicio de sesión**
   * Contraseña: **su contraseña**
   * **Master DB (List all databases)** [BD maestra (Enumerar todas las bases de datos)]
   
   > [!NOTE]
   > De forma predeterminada el Asistente de hello guarda la información de inicio de sesión. Si no quiere que lo haga, seleccione **Forget Login Information (No recordar la información de inicio de sesión)**.
   >
   
     ![Asistente para migración de base de datos SQL: seleccionar origen, paso 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. Hola **Seleccionar origen** cuadro de diálogo, el nombre de la base de datos de hello seleccione Restaurar de hello **pasos de preparación** como origen de la sección y, a continuación, haga clic en **siguiente**.
   
    ![Asistente para migración de base de datos SQL: seleccionar origen, paso 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. Hola **elegir objetos** cuadro de diálogo, seleccione hello **seleccionar objetos de base de datos específica** opción y, a continuación, seleccione table(or tables) Hola que desea que el servidor de destino de toomigrate toohello.
   ![Asistente para migración de base de datos SQL: elegir objetos](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)
6. En hello **resumen del Asistente para secuencia de comandos** página, haga clic en **Sí** cuando se le pregunta acerca de si está listo toogenerate una secuencia de comandos SQL. También tiene Hola Hola toosave secuencia de comandos TSQL opción para su uso posterior.
   ![Asistente para migración de base de datos SQL: resumen del Asistente de scripts](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)
7. En hello **resumen de los resultados** página, haga clic en **siguiente**.
   ![Asistente para migración de base de datos SQL: resumen de resultados](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)
8. En hello **configurar conexión de servidor de destino** página, haga clic en **conectar tooServer**y, a continuación, escriba los detalles de hello como se indica a continuación:
   
   * **Nombre del servidor**: instancia de servidor de destino
   * **Autenticación**: **Autenticación de SQL Server**. Escriba sus credenciales de inicio de sesión.
   * **Base de datos**: **Master DB (List all databases)** [BD maestra (Enumerar todas las bases de datos)]. Esta opción muestra todas las bases de datos de hello en el servidor de destino de Hola.
     
     ![Asistente para migración de base de datos SQL: configurar conexión del servidor de destino](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. Haga clic en **conectar**, seleccione la base de datos de destino de Hola que desea toomove Hola tabla y, a continuación, haga clic en **siguiente**. Esto debería termine de ejecutar script de Hola generado previamente y debería ver Hola recién movido la base de datos de destino de toohello copiada de tabla.

## <a name="verification-step"></a>Paso de comprobación

- Hola de consultas y pruebas recién había copiado tabla toomake seguro de que los datos de hello están intactos. Tras la confirmación, puede quitar el formulario de hello cambia el nombre de tabla **pasos de preparación** sección. (por ejemplo, &lt;nombre de la tabla&gt;_old).

## <a name="next-steps"></a>Pasos siguientes
[Información general: copias de seguridad automatizadas de Base de datos SQL](sql-database-automated-backups.md)

