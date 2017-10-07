---
title: "aaaGetting a trabajar con Azure SQL Data Sync (versión preliminar) | Documentos de Microsoft"
description: "Este tutorial le ayuda a comenzar con Azure SQL Data Sync (versión preliminar)."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: douglasl
ms.openlocfilehash: 666d09237e42acc23ae3c8c81e60734a413f5949
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a>Introducción a SQL Data Sync de Azure (vista previa)
En este tutorial, aprenderá cómo tooset la sincronización de datos de SQL Azure mediante la creación de un grupo de sincronización híbrida contiene instancias de base de datos de SQL Azure y SQL Server. nuevo grupo de sincronización Hola esté completamente configurado y se sincroniza en programación Hola establecida.

En este tutorial se asume que tiene al menos alguna experiencia previa con SQL Database y con SQL Server. 

Para obtener información general sobre SQL Data Sync, vea [Sincronización de datos](sql-database-sync-data.md).

Para obtener ejemplos PowerShell completos que muestran cómo tooconfigure SQL Data Sync, vea Hola siguientes artículos:
-   [Usar PowerShell toosync entre varias bases de datos de SQL Azure](scripts/sql-database-sync-data-between-sql-databases.md)
-   [Usar PowerShell toosync entre una base de datos de SQL Azure y una base de datos de SQL Server local](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> documentación técnica completa Hola establecido para la sincronización de datos de SQL Azure, anteriormente ubicada en MSDN, está disponible como un. Documento PDF. Descárguela [aquí](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).

## <a name="step-1---create-sync-group"></a>Paso 1: Creación de un grupo de sincronización

### <a name="locate-hello-data-sync-settings"></a>Busque la configuración de sincronización de datos de Hola

1.  En el explorador, navegue toohello portal de Azure.

2.  En el portal de hello, busque las bases de datos SQL desde el panel o desde el icono de bases de datos SQL de hello en la barra de herramientas de Hola.

    ![Lista de instancias de Azure SQL Database](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  En hello **bases de datos SQL** hoja, seleccione Hola SQL base de datos existente que desee toouse abre la base de datos de hello central para datos de sincronización. hoja de base de datos SQL de Hola.

4.  En la hoja de base de datos SQL de hello para la base de datos seleccionada de hello, seleccione **sincronizar bases de datos de tooother**. se abre la hoja de Data Sync de Hola.

    ![Opción de sincronización de bases de datos tooother](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a>Creación de un grupo de sincronización

1.  En la hoja de la sincronización de datos de hello, seleccione **nuevo grupo de sincronización**. Hola **nuevo grupo de sincronización** hoja se abre con el paso 1, **crear grupo de sincronización**, resaltada. Hola **crear grupo de sincronización de datos** también se abre la hoja.

2.  En hello **crear grupo de sincronización de datos** hoja, Hola siguientes cosas:

    1.  Hola **nombre del grupo de sincronización** , a continuación, escriba un nombre para el nuevo grupo de sincronización Hola.

    2.  Hola **base de datos de metadatos de sincronización** sección, elija si toocreate una nueva base de datos (recomendado) o toouse otra base de datos.

        > [!NOTE]
        > Microsoft recomienda que cree una base de datos nueva y vacía toouse como Hola base de datos de metadatos de sincronización. Data Sync crea tablas en esta base de datos y ejecuta una carga de trabajo frecuente. Esta base de datos se comparte automáticamente como base de datos de metadatos de sincronización para todos los grupos de sincronización en la región seleccionada de Hola Hola. No se puede cambiar base de datos de metadatos de sincronización de hello, su nombre o su nivel de servicio sin colocarlo.

        Si ha elegido **Nueva base de datos**, seleccione **Crear nueva base de datos**. Hola **base de datos SQL** abre la hoja. En hello **base de datos SQL** hoja, asigne un nombre y configurar Hola nueva base de datos. Después seleccione **Aceptar**.

        Si ha elegido **usar base de datos existente**, seleccione base de datos de hello en lista de Hola.

    3.  Hola **sincronización automática** , primero seleccione **en** o **desactivar**.

        Si ha elegido **en**, Hola **frecuencia de sincronización** sección, escriba un número y seleccione segundos, minutos, horas o días.

        ![Establecimiento de la frecuencia de sincronizaicón](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  Hola **la resolución de conflictos** sección, seleccione "Gana la central" o "Miembro wins."

        ![Especifique cómo se resuelven los conflictos](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  Seleccione **Aceptar** y espere Hola nueva sincronización grupo toobe creado e implementado.

## <a name="step-2---add-sync-members"></a>Paso 2: Adición de miembros de sincronización

Después de que se crea e implementa, paso 2, grupo de sincronización hello **agregar miembros de sincronización**, se resalta en hello **nuevo grupo de sincronización** hoja.

Hola **base de datos central** sección, escriba las credenciales existentes de hello para el servidor de base de datos SQL de hello en qué Hola se encuentra la base de datos central. No escriba *nuevas* credenciales en esta sección.

![Base de datos central se ha agregado el grupo de toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a>Adición de una instancia de Azure SQL Database

Hola **base de datos miembro** sección, opcionalmente, agregar un grupo de sincronización de base de datos de SQL Azure toohello seleccionando **agregar una base de datos de Azure**. Hola **Configurar base de datos de Azure** abre la hoja.

En hello **Configurar base de datos de Azure** hoja, Hola siguientes cosas:

1.  Hola **nombre del miembro de sincronización** campo, proporcione un nombre para el nuevo miembro de sincronización Hola. Este nombre es distinto del nombre de Hola de hello propia base de datos.

2.  Hola **suscripción** Hola de campo, seleccione asociados suscripción de Azure para fines de facturación.

3.  Hola **Azure SQL Server** servidor de base de datos SQL existente, seleccione Hola.

4.  Hola **base de datos de SQL Azure** base de datos SQL existente Hola de campo, seleccione.

5.  Hola **direcciones de sincronización** , a continuación, seleccionar la sincronización bidireccional, toohello concentrador, o de hello concentrador.

    ![Adición de un nuevo miembro de sincronización de SQL Database](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  Hola **nombre de usuario** y **contraseña** campos, escriba las credenciales existentes de hello para el servidor de base de datos SQL de hello en qué Hola base de datos miembro se encuentra. No escriba *nuevas* credenciales en esta sección.

7.  Seleccione **Aceptar** y espere Hola nueva sincronización miembro toobe creado e implementado.

    ![Se ha agregado el nuevo miembro de sincronización de SQL Database](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a>Adición de una base de datos local de SQL Server

Hola **base de datos miembro** sección, opcionalmente, agregar un grupo de sincronización de toohello de SQL Server local seleccionando **agregar una base de datos local**. Hola **configurar local** abre la hoja.

En hello **configurar local** hoja, Hola siguientes cosas:

1.  Seleccione **elegir Hola puerta de enlace de agente de sincronización**. Hola **seleccione Agente de sincronización** abre la hoja.

    ![Elegir puerta de enlace del agente de sincronización de Hola](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  En hello **elegir Hola puerta de enlace de agente de sincronización** hoja, elija si toouse un agente existente o crear un nuevo agente.

    Si ha elegido **existente agentes**, seleccione Hola agente existente de la lista de Hola.

    Si ha elegido **crear un nuevo agente**, Hola siguientes cosas:

    1.  Descargar software de agente de sincronización de cliente de Hola de vínculo de hello proporcionado e instalarlo en el equipo Hola donde se encuentra Hola SQL Server.
 
        > [!IMPORTANT]
        > Tener tooopen salida el puerto TCP 1433 en el agente de cliente de hello firewall toolet Hola comunicarse con el servidor de Hola.


    2.  Escriba un nombre para el agente de Hola.

    3.  Seleccione **Crear y generar clave**.

    4.  Portapapeles de toohello clave de agente de copia Hola.
        
        ![Creación de un agente de sincronización](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  Seleccione **Aceptar** tooclose hello **seleccione Agente de sincronización** hoja.

    6.  En el equipo de SQL Server de hello, busque y ejecute la aplicación del agente de sincronización cliente hello.

        ![aplicación cliente de agente de sincronización de datos de Hola](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  En la aplicación del agente de sincronización de hello, seleccione **Enviar clave del agente**. Hola **configuración de base de datos de metadatos de sincronización** abre el cuadro de diálogo.

    8.  Hola **configuración de base de datos de metadatos de sincronización** cuadro de diálogo, pegar en clave del agente Hola copiado de hello portal de Azure. También se proporcionan credenciales existentes de hello para el servidor de base de datos de SQL Azure de hello en qué Hola se encuentra la base de datos de metadatos. (Si ha creado una nueva base de datos de metadatos, esta base de datos está en hello mismo servidor que la base de datos de base de datos central de Hola.) Seleccione **Aceptar** y espere Hola configuración toofinish.

        ![Escriba las credenciales de clave y el servidor de agente Hola](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   Si recibe un error de firewall en este momento, tener una toocreate una regla de firewall en Azure tooallow el tráfico entrante del equipo de SQL Server de Hola. Puede crear reglas de hello manualmente en el portal de hello, pero quizá le resulte más fácil toocreate que en SQL Server Management Studio (SSMS). En SSMS, pruebe a base de datos de tooconnect toohello central en Azure. Escriba su nombre como \<hub_database_name\>.database.windows.net. Siga los pasos de Hola de regla de firewall de Azure de Hola de tooconfigure cuadro de diálogo de Hola. A continuación, devolver toohello aplicación de agente de sincronización cliente.

    9.  En la aplicación del agente de sincronización cliente hello, haga clic en **registrar** tooregister una base de datos de SQL Server con el agente de Hola. Hola **configuración de SQL Server** abre el cuadro de diálogo.

        ![Adición y configuración de una instancia de SQL Server Database](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. Hola **configuración de SQL Server** diálogo cuadro, elija si tooconnect mediante autenticación de SQL Server o autenticación de Windows. Si elige la autenticación de SQL Server, escriba las credenciales existentes de Hola. Proporcione nombre de SQL Server de Hola y Hola de base de datos de Hola que desea toosync. Seleccione **Probar conexión** tootest la configuración. Después, seleccione **Guardar**. base de datos registrada de Hola aparece en la lista Hola.

        ![La base de datos de SQL Server ya está registrada](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. Ahora puede cerrar la aplicación del agente de sincronización cliente hello.

    12. En el portal de hello, en hello **configurar On-Premises** hoja, seleccione **seleccione Hola base de datos.** Hola **Seleccionar base de datos** abre la hoja.

    13. En hello **Seleccionar base de datos** hoja en hello **nombre del miembro de sincronización** campo, proporcione un nombre para el nuevo miembro de sincronización Hola. Este nombre es distinto del nombre de Hola de hello propia base de datos. Seleccionar base de datos de hello lista Hola. Hola **direcciones de sincronización** , a continuación, seleccionar la sincronización bidireccional, toohello concentrador, o de hello concentrador.

        ![Seleccione hello en la base de datos local](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. Seleccione **Aceptar** tooclose hello **Seleccionar base de datos** hoja. A continuación, seleccione **Aceptar** tooclose hello **configurar local** hoja y espere a que Hola sincronizan nuevos miembros toobe creado e implementado. Por último, haga clic en **Aceptar** tooclose hello **seleccionar miembros de sincronización** hoja.

        ![En la base de datos local se ha agregado toosync grupo](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  tooconnect tooSQL Data Sync y el agente local de hello, agregar el rol de toohello de nombre de usuario `DataSync_Executor`. Sincronización de datos, crea este rol en la instancia de SQL Server de Hola.

## <a name="step-3---configure-sync-group"></a>Paso 3: Configuración del grupo de sincronización

Una vez creados e implementados, paso 3, miembros del grupo de sincronización nuevo de hello **Configurar grupo de sincronización**, se resalta en hello **nuevo grupo de sincronización** hoja.

1.  En hello **tablas** hoja, seleccione una base de datos de lista de Hola de sincronización de miembros del grupo y, a continuación, seleccione **actualizar esquema**.

2.  En lista de Hola de tablas disponibles, seleccione las tablas de Hola que desea toosync.

    ![Seleccionar las tablas toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  De forma predeterminada, se seleccionan todas las columnas de tabla de Hola. Si no desea toosync todas las columnas de hello, deshabilite Hola casilla de verificación para las columnas de Hola que no desea toosync. Asegúrese de selecciona columna de clave principal de tooleave Hola.

    ![Seleccionar campos toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  Por último, seleccione **Guardar**.

## <a name="next-steps"></a>Pasos siguientes
¡Enhorabuena! Ha creado un grupo de sincronización que incluye una instancia de SQL Database y una base de datos de SQL Server.

Para obtener más información sobre SQL Database y SQL Data Sync, vea:

-   [Descargar documentación técnica de hello completa de SQL Data Sync](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [Descargue la documentación de API de REST de sincronización de datos de SQL de Hola](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [Información general de SQL Database](sql-database-technical-overview.md)
-   [Administración del ciclo de vida de las aplicaciones](https://msdn.microsoft.com/library/jj907294.aspx)
