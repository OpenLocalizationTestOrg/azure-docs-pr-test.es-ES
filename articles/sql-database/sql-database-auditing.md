---
title: "aaaGet iniciado a la auditoría de base de datos de SQL de Azure | Documentos de Microsoft"
description: "Introducción a la auditoría de base de datos SQL de Azure"
services: sql-database
documentationcenter: 
author: giladm
manager: jhubbard
editor: giladm
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: giladm
ms.openlocfilehash: 5494c602d702ac41992520f900c393a98cc7c989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-auditing"></a>Introducción a la auditoría de bases de datos SQL
Auditoría de base de datos SQL Azure realiza un seguimiento de eventos de base de datos y escribe el registro de auditoría tooan en su cuenta de almacenamiento de Azure. La auditoría también:

* Puede ayudarle a mantener el cumplimiento de normativas, comprender la actividad de las bases de datos y conocer las discrepancias y anomalías que pueden indicar problemas en el negocio o infracciones de seguridad sospechosas.

* Habilita y facilita estándares de cumplimiento toocompliance, aunque no garantiza el cumplimiento de normas. Para obtener más información sobre Azure programas ese cumplimiento de estándares de soporte técnico, consulte hello [centro de confianza de Azure](https://azure.microsoft.com/support/trust-center/compliance/).


## <a id="subheading-1"></a>Información general de auditoría de base de datos SQL de Azure
Puede usar la auditoría de base de datos SQL para:


* **Conservar** una traza de auditoría de eventos seleccionados. Puede definir categorías de base de datos acciones toobe auditado.
* **Informar** sobre la actividad de la base de datos. Puede usar los informes preconfigurados y un tooget de panel a trabajar rápidamente con actividad y los informes de eventos.
* **Analizar** informes. Puede buscar eventos sospechosos, actividades inusuales y tendencias.

Puede configurar la auditoría para distintos tipos de categorías de eventos, como se explica en hello [configurar la auditoría para la base de datos](#subheading-2) sección.

Los registros de auditoría se escriben tooAzure el almacenamiento de blobs de su suscripción de Azure.


## <a id="subheading-8"></a>Definir la directiva de auditoría de nivel de servidor frente la de nivel de base de datos

Puede definirse una directiva de auditoría para una base de datos específica o como directiva de servidor predeterminada:

* Una directiva de servidor aplica tooall existente y las bases de datos recién creadas en el servidor de Hola.

* Si *está habilitada la auditoría de servidor blob*, lo *siempre se aplica a la base de datos de toohello* (es decir, base de datos de Hola se auditarán), independientemente de la base de datos de hello configuración de auditoría.

* Habilitación de blob de auditoría de base de datos de hello en suma tooenabling en servidor hello, le *no* invalidar o cambiar cualquiera de las opciones de Hola de auditoría de hello server blob. Ambas auditorías existirán en paralelo. En otras palabras, base de datos de Hola se auditará dos veces en paralelo (una vez mediante la directiva de servidor de hello y una vez por la directiva de la base de datos de hello).

   > [!NOTE]
   > Debe habilitar tanto la auditoría de blobs de servidor como la auditoría de blobs de base de datos, a menos que:
    > * Desea que otro toouse *cuenta de almacenamiento* o *período de retención* para una base de datos.
    > * Desea tooaudit evento tipos o categorías de una base de datos que difieren de los tipos de eventos o las categorías que se está auditando para rest Hola de bases de datos de hello en el servidor de Hola. Por ejemplo, podría tener inserciones de la tabla que necesitan toobe auditar sólo para una base de datos.
   > 
   > En caso contrario, se recomienda que habilite la auditoría de nivel de servidor solo blobs y deje proceso de auditoría de nivel de base de datos de hello deshabilitada para todas las bases de datos.


## <a id="subheading-2"></a>Configuración de la auditoría para su base de datos
Hello siguiente sección describe configuración Hola de auditoría usando Hola portal de Azure.

1. Vaya toohello [portal de Azure](https://portal.azure.com).
2. Vaya toohello **configuración** hoja de hello servidor de base de datos/SQL de SQL que desee tooaudit. Hola **configuración** hoja, seleccione **detección de auditoría y amenaza**.

    <a id="auditing-screenshot"></a>![Panel de navegación][1]
3. Si lo prefiere tooset una directiva de auditoría de servidor (que se aplicará tooall existente y las bases de datos recién creadas en este servidor), puede seleccionar hello **ver configuración del servidor** vínculo en la hoja de auditoría de base de datos de Hola. A continuación, puede ver o modificar la configuración de auditoría de servidor hello.

    ![Panel de navegación][2]
4. Si lo prefiere tooenable blob auditoría de nivel de base de datos de hello (en suma tooor en lugar de auditoría de nivel de servidor), para **auditoría**, seleccione **ON**y para **auditoría de tipo** , seleccione **Blob**.

    Si está habilitada la auditoría de servidor blobs, auditoría de base de datos configurada de hello existirá paralelo con la auditoría de blob de servidor hello.  

    ![Panel de navegación][3]
5. Hola tooopen **almacenamiento de registros de auditoría** hoja, seleccione **detalles del almacenamiento**. Seleccione la cuenta de almacenamiento de Azure de Hola donde se guardarán los registros y, a continuación, seleccione el período de retención de hello, después de que Hola se eliminarán los registros antiguos. y, a continuación, haga clic en **Aceptar**. 
   >[!TIP] 
   >Hola tooget máximo partido de plantillas de informes de auditoría de hello, utilice Hola misma cuenta de almacenamiento para todas las bases de datos auditados. 

    <a id="storage-screenshot"></a>![Panel de navegación][4]
6. Si desea toocustomize Hola auditar eventos, puede hacerlo a través de PowerShell o API de REST de Hola. Para obtener más información, vea hello [automatización (API de REST o PowerShell)](#subheading-7) sección.
7. Después de configurar la configuración de auditoría, puede activar la nueva característica de detección de amenazas hello y configurar alertas de seguridad de mensajes de correo electrónico tooreceive. Cuando se usa la detección de amenazas, se reciben alertas proactivas sobre actividades anómalas de la base de datos que pueden indicar posibles amenazas de seguridad. Para obtener más detalles, vea [Introducción a la detección de amenazas](sql-database-threat-detection-get-started.md).
8. Haga clic en **Guardar**.





## <a id="subheading-3"></a>Análisis de registros e informes de auditoría
Los registros de auditoría se agregan en hello cuenta de almacenamiento de Azure que ha elegido durante la instalación. Puede explorar los registros de auditoría con una herramienta como el [Explorador de Azure Storage](http://storageexplorer.com/).

Los registros de auditoría de blobs se guardan como una colección de archivos de blob dentro de un contenedor llamado **sqldbauditlogs**.

Para obtener más información acerca de la jerarquía de Hola de carpeta de almacenamiento de registros de auditoría de blob de hello, convenciones de nomenclatura de blob y formato de registro, vea hello [referencia del formato de registro de auditoría de Blob (descarga de archivo .docx)](https://go.microsoft.com/fwlink/?linkid=829599).

Hay varios métodos que puede usar registros de auditoría de blob de tooview:

* Hola de uso [portal de Azure](https://portal.azure.com).  Base de datos pertinentes de hello abierto. AT Hola superior de la base de datos de hello **detección de auditoría y amenaza** hoja, haga clic en **ver registros de auditoría**.

    ![Panel de navegación][7]

    Un **registros de auditoría** se abre la hoja, desde el que podrá tooview capaz de hello registros.

    - Puede ver fechas específicas haciendo clic en **filtro** en parte superior de Hola de hello **registros de auditoría** hoja.
    - Puede cambiar entre los registros de auditoría que se crearon mediante la directiva de servidor o una directiva de base de datos de auditoría.

       ![Panel de navegación][8]

* Utilice la función de sistema de hello **sys.fn_get_audit_file** datos del registro de auditoría (T-SQL) tooreturn hello en formato tabular. Para obtener más información sobre el uso de esta función, vea hello [sys.fn_get_audit_file documentación](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).


* Use **Combinar archivos de auditoría** en SQL Server Management Studio (a partir de SSMS 17):  
    1. En el menú de SSMS hello, seleccione **archivo** > **abiertos** > **combinar archivos de auditoría**.

        ![Panel de navegación][9]
    2. Hola **agregar archivos de auditoría** abre el cuadro de diálogo. Seleccione uno de hello **agregar** opciones para elegir si auditoría toomerge los archivos de una variable local de disco o importarlos desde el almacenamiento de Azure (será necesario tooprovide los detalles del almacenamiento de Azure y la clave de cuenta).

    3. Después de haber agregado toomerge de todos los archivos, haga clic en **Aceptar** operación de combinación de toocomplete Hola.

    4. Abre el archivo combinado de Hello en SSMS, donde puede ver y analizarlos, así como la exportación se tooan XEL o CSV archivo o tooa una tabla.

* Hola de uso [sincronizar aplicación](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) que hemos creado. Se ejecuta en Azure y utiliza el análisis de registros de Operations Management Suite (OMS) pública API toopush SQL los registros de auditoría en OMS. aplicación de sincronización de Hello inserta los registros de auditoría SQL en análisis de registros de OMS para su uso a través del panel de análisis de registros de OMS Hola. 

* Use Power BI. Puede ver y analizar los datos de registro de auditoría en Power BI. Obtenga más información sobre [Power BI y tenga acceso a una plantilla que se puede descargar](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).

* Descargar archivos de registro de su contenedor de blob de almacenamiento de Azure mediante el portal de Hola o mediante una herramienta como [Azure Storage Explorer](http://storageexplorer.com/).
    * Después de haber descargado localmente un archivo de registro, puede hacer doble clic hello tooopen de archivo, ver y analizar los registros de hello en SSMS.
    * También puede descargar varios archivos al mismo tiempo a través del Explorador de Azure Storage. Haga clic en una subcarpeta específica (por ejemplo, una subcarpeta que incluye todos los archivos de registro para una fecha concreta) y seleccione **Guardar como** toosave en una carpeta local.

* Otros métodos:
   * Después de descargar varios archivos (o en una subcarpeta que incluya los archivos de registro durante un día completo, como se describe en el elemento anterior de hello en esta lista), puede combinarlos localmente como se describe en las instrucciones de los archivos de auditoría de mezcla de SSMS Hola que se ha descrito anteriormente.

   * Ver los registros de auditoría de blobs mediante programación:

     * Hola de uso [lector de eventos extendidos](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) biblioteca de C#.
     * [Consulta de archivos de eventos extendidos](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) mediante PowerShell.




## <a id="subheading-5"></a>Prácticas de producción
<!--hello description in this section refers toopreceding screen captures.-->

### <a id="subheading-6">Auditoría de bases de datos con replicación geográfica</a>
Cuando se utiliza bases de datos de replicación geográfica, es posible tooset la auditoría en la base de datos principal de hello, base de datos secundaria de hello o ambos, según el tipo de auditoría de Hola.

Siga estas instrucciones (Recuerde que auditoría de blobs puede estar activada o desactivada solo desde base de datos principal de hello configuración de auditoría):

* **Base de datos principal**. Activar la auditoría de blob, en el servidor de Hola o en hello propia base de datos, como se describe en hello [configurar la auditoría para la base de datos](#subheading-2) sección.
* **Base de datos secundaria**. Activar la auditoría de blob en la base de datos principal de hello, como se describe en hello [configurar la auditoría para la base de datos](#subheading-2) sección. 
   * Auditoría de blobs debe estar habilitada en hello *principal propia base de datos*, no el servidor de Hola.
   * Después de habilita la auditoría de blobs en la base de datos principal de hello, también se habilitará en la base de datos secundaria de Hola.

     >[!IMPORTANT]
     >De forma predeterminada, configuración de almacenamiento de Hola de base de datos secundaria de hello será idéntico toothose de base de datos principal de hello, haciendo que el tráfico entre regional. Para evitarlo, puede habilitar la auditoría de blobs en el servidor secundario de Hola y configurar el almacenamiento local en la configuración de almacenamiento del servidor secundario de Hola. Esto anulará la ubicación de almacenamiento de Hola de base de datos secundaria de Hola y el resultado en cada base de datos guardar su almacenamiento de toolocal de registros de auditoría.  
<br>

### <a id="subheading-6">Regeneración de clave de almacenamiento</a>
En producción, es probable toorefresh el almacenamiento de claves de forma periódica. Al actualizar las claves, necesita la directiva de auditoría de hello tooresave. proceso de Hello es el siguiente:

1. Abra hello **detalles del almacenamiento** hoja. Hola **clave de acceso de almacenamiento** cuadro, seleccione **secundaria**y haga clic en **Aceptar**. A continuación, haga clic en **guardar** princip Hola de hello hoja de configuración de auditoría.

    ![Panel de navegación][5]
2. Vaya toohello hoja de configuración de almacenamiento y volver a generar clave de acceso principal de Hola.

    ![Panel de navegación][6]
3. Volver atrás toohello hoja de configuración de auditoría, cambiar la clave de acceso de almacenamiento de Hola de tooprimary secundario y, a continuación, haga clic en **Aceptar**. A continuación, haga clic en **guardar** princip Hola de hello hoja de configuración de auditoría.
4. Volver atrás toohello hoja de configuración de almacenamiento y la clave de acceso secundaria de hello Regenerar (como preparación para el ciclo de actualización de la clave siguiente hello).

## <a id="subheading-7"></a>Automatización (PowerShell o API de REST)
También puede configurar la auditoría de base de datos de SQL Azure mediante el uso de hello después de herramientas de automatización:

* **Cmdlets de PowerShell**:

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Remove-AzureRMSqlDatabaseAuditing][103]
   * [Remove-AzureRMSqlServerAuditing][104]
   * [Set-AzureRMSqlDatabaseAuditingPolicy][105]
   * [Set-AzureRMSqlServerAuditingPolicy][106]
   * [Use-AzureRMSqlServerAuditingPolicy][107]

   Para ver un script de ejemplo, consulte [Configuración de la auditoría y detección de amenazas mediante PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).

* **API de REST: auditoría de blobs**:

   * [Create or Update Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695939.aspx) (Creación o actualización de la directiva de auditoría de blobs de la base de datos)
   * [Create or Update Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771861.aspx) (Creación o actualización de la directiva de audioría de blobs del servidor)
   * [Get Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695938.aspx) (Obtención de la directiva de auditoría de bobs de la base de datos)
   * [Get Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771860.aspx) (Obtención de la directiva de auditoría de blobs del servidor)
   * [Get Server Blob Auditing Operation Result](https://msdn.microsoft.com/library/azure/mt771862.aspx) (Obtención de resultados de funcionamiento de la auditoría de blobs del servidor)


<!--Anchors-->
[Azure SQL Database Auditing overview]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3
[Practices for usage in production]: #subheading-5
[Storage Key Regeneration]: #subheading-6
[Automation (PowerShell / REST API)]: #subheading-7
[Blob/Table differences in Server auditing policy inheritance]: (#subheading-8)  

<!--Image references-->
[1]: ./media/sql-database-auditing-get-started/1_auditing_get_started_settings.png
[2]: ./media/sql-database-auditing-get-started/2_auditing_get_started_server_inherit.png
[3]: ./media/sql-database-auditing-get-started/3_auditing_get_started_turn_on.png
[4]: ./media/sql-database-auditing-get-started/4_auditing_get_started_storage_details.png
[5]: ./media/sql-database-auditing-get-started/5_auditing_get_started_storage_key_regeneration.png
[6]: ./media/sql-database-auditing-get-started/6_auditing_get_started_regenerate_key.png
[7]: ./media/sql-database-auditing-get-started/7_auditing_get_started_blob_view_audit_logs.png
[8]: ./media/sql-database-auditing-get-started/8_auditing_get_started_blob_audit_records.png
[9]: ./media/sql-database-auditing-get-started/9_auditing_get_started_ssms_1.png
[10]: ./media/sql-database-auditing-get-started/10_auditing_get_started_ssms_2.png

[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy
