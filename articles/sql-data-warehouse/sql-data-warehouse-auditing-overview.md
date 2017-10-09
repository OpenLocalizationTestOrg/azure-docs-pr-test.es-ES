---
title: "aaaAuditing en el almacén de datos de SQL de Azure | Documentos de Microsoft"
description: "Introducción a la auditoría en Almacenamiento de datos SQL de Azure"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a>Auditoría en Almacenamiento de datos SQL de Azure
> [!div class="op_single_selector"]
> * [Auditoría](sql-data-warehouse-auditing-overview.md)
> * [Detección de amenazas](sql-data-warehouse-security-threat-detection.md)
> 
> 

Auditoría de almacenamiento de datos SQL permite toorecord eventos en el registro de auditoría de base de datos tooan en su cuenta de almacenamiento de Azure. La auditoría puede ayudarle a mantener el cumplimiento de normativas, comprender la actividad de las bases de datos y conocer las discrepancias y anomalías que pueden indicar problemas en el negocio o infracciones de seguridad sospechosas. La auditoría de SQL Data Warehouse también se integra con Microsoft Power BI, con el fin de facilitar la generación de análisis e informes detallados.

Las herramientas de auditoría habilitan y facilitan estándares de cumplimiento toocompliance pero no garantizan el cumplimiento de normas. Para obtener más información sobre Azure programas ese cumplimiento de estándares de soporte técnico, consulte hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">centro de confianza de Azure</a>.

* [Conceptos básicos de auditoría de Base de datos]
* [Configuración de la auditoría para su base de datos]
* [Análisis de registros e informes de auditoría]

## <a id="subheading-1"></a>Conceptos básicos de auditoría de Almacenamiento de datos SQL de Azure
La auditoría de Almacenamiento de datos SQL la permite que:

* **Conservar** una traza de auditoría de eventos seleccionados. Puede definir categorías de base de datos acciones toobe auditado.
* **Informar** sobre la actividad de la base de datos. Puede usar los informes preconfigurados y un tooget de panel a trabajar rápidamente con actividad y los informes de eventos.
* **Analizar** informes. Puede buscar eventos sospechosos, actividades inusuales y tendencias.

Puede configurar la auditoría para hello siguientes categorías de eventos:

**Sin formato SQL** y **SQL parametrizadas** para qué hello los registros de auditoría recopilados se clasifican como  

* **Toodata de acceso**
* **Cambios de esquema (DDL)**
* **Cambios de datos (DML)**
* **Cuentas, roles y permisos (DCL)**
* **Procedimiento almacenado**, **Inicio de sesión** y **Administración de transacciones**.

Para cada categoría de eventos, las operaciones de **aciertos** y **errores** se configuran por separado.

Para obtener más información acerca de las actividades de Hola y auditados los eventos, vea hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">referencia de formato de registro de auditoría (descarga de los archivos doc)</a>.

Los registros de auditoría se almacenan en su cuenta de almacenamiento de Azure. Puede definir un período de retención de registro de auditoría.

Puede definirse una directiva de auditoría para una base de datos específica o como directiva de servidor predeterminada. Una directiva de auditoría de servidor predeterminada aplica a las bases de datos de tooall en un servidor, que no tienen una reemplazo base de datos auditoría directiva específica definida.

Antes de configurar la auditoría, compruebe si usa un ["Cliente de nivel inferior"](sql-data-warehouse-auditing-downlevel-clients.md)

## <a id="subheading-2"></a>Configuración de la auditoría para su base de datos
1. Iniciar hello <a href="https://portal.azure.com" target="_blank">portal de Azure</a>.
2. Vaya toohello **configuración** hoja de hello desea tooaudit de almacenamiento de datos de SQL. Hola **configuración** hoja, seleccione **detección de auditoría y amenaza**.
   
    ![][1]
3. A continuación, habilitar la auditoría, haga clic en hello **ON** botón.
   
    ![][3]
4. En la hoja de configuración de auditoría de hello, seleccione **detalles del almacenamiento** hoja de almacenamiento de registros de auditoría de tooopen Hola. Seleccione Hola donde se guardará los registros de cuenta de almacenamiento de Azure, hello y período de retención. 
>[!TIP]
>Hola uso preconfigurada de la misma cuenta de almacenamiento para todas las bases de datos auditados tooget Hola máximo partido de hello informa de plantillas.
   
    ![][4]
5. Haga clic en hello **Aceptar** botón toosave Hola almacenamiento detalles de configuración.
6. En **registro por evento**, haga clic en **correcto** y **error** toolog todos los eventos, o elegir categorías de eventos individuales.
7. Si va a configurar la auditoría para una base de datos, debe cadena de conexión de hello tooalter de su tooensure cliente auditoría de datos se ha capturado correctamente. Comprobar hello [modificar el FQDN de servidor en la cadena de conexión de hello](sql-data-warehouse-auditing-downlevel-clients.md) tema para las conexiones de cliente de nivel inferior.
8. Haga clic en **Aceptar**.

## <a id="subheading-3"></a>Análisis de registros e informes de auditoría
Los registros de auditoría se agrupan en una colección de tablas de almacén con un **SQLDBAuditLogs** prefijo Hola cuenta de almacenamiento de Azure que ha elegido durante la instalación. Puede ver los archivos de registro usando una herramienta como el <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Explorador de almacenamiento de Azure</a>.

Una plantilla de informe panel preconfigurado está disponible como un <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">hoja de cálculo de Excel que se puede descargar</a> toohelp analizar rápidamente los datos de registro. plantilla de hello toouse en los registros de auditoría, necesita Excel 2013 o versiones posterior y Power Query, que puede descargar <a href="http://www.microsoft.com/download/details.aspx?id=39379">aquí</a>.

plantilla de Hello tiene datos de ejemplo ficticio en ella y puede configurar Power Query tooimport el registro de auditoría directamente desde su cuenta de almacenamiento de Azure.

## <a id="subheading-4"></a>Regeneración de clave de almacenamiento
En producción, es probable toorefresh el almacenamiento de claves de forma periódica. Al actualizar las claves, debe directiva de hello toosave. proceso de Hello es el siguiente:

1. Hola auditoría hoja de configuración (descrita anteriormente en el programa de instalación de hello auditoría sección) cambiar hello **clave de acceso de almacenamiento** de *principal* demasiado*secundaria* y  **Guardar**.

   ![][4]
2. Hoja de configuración de almacenamiento vaya toohello y **regenerar** hello *clave de acceso principal*.
3. Volver atrás toohello auditoría hoja de configuración, conmutador hello **clave de acceso de almacenamiento** de *secundaria* demasiado*principal* y presione **guardar**.
4. Volver atrás toohello almacenamiento interfaz de usuario y **regenerar** hello *clave de acceso secundaria* (como preparación para hello claves siguientes ciclo de actualización.

## <a id="subheading-5"></a>Automatización (PowerShell o API de REST)
También puede configurar la auditoría en el almacén de datos de SQL Azure mediante el uso de hello después de herramientas de automatización:

* **Cmdlets de PowerShell**:

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Remove-AzureRMSqlDatabaseAuditing][103]
   * [Remove-AzureRMSqlServerAuditing][104]
   * [Set-AzureRMSqlDatabaseAuditingPolicy][105]
   * [Set-AzureRMSqlServerAuditingPolicy][106]
   * [Use-AzureRMSqlServerAuditingPolicy][107]

<!--Anchors-->
[Conceptos básicos de auditoría de Base de datos]: #subheading-1
[Configuración de la auditoría para su base de datos]: #subheading-2
[Análisis de registros e informes de auditoría]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy