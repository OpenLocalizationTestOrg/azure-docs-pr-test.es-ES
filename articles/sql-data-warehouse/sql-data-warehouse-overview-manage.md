---
title: "aaaManage bases de datos en el almacén de datos de SQL de Azure | Documentos de Microsoft"
description: "Información general de administración de bases de datos de Almacenamiento de datos SQL Incluye herramientas de administración, DWU y rendimiento de escalado horizontal, solución de problemas de rendimiento de las consultas, el establecimiento de directivas de seguridad y la restauración una base de datos de daños en los datos o de un apagón regional."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 8576fdb3-71fe-4b3b-a4e0-5e8a7f148acf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: caec6572c4ab395107c3b095adc69a53eae8bd88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a>Administración de base datos en Almacenamiento de datos SQL de Azure
Almacenamiento de datos SQL automatiza muchos aspectos de la administración de las bases de datos. Por ejemplo, tooscale rendimiento solo necesita tooadjust y paga por hello derecha nivel de recursos de proceso y, a continuación, permiten el almacenamiento de datos de SQL hacer todo el trabajo de escalado horizontal y escalado back Hola.

Sin duda, deberá toomonitor su tooidentify de cargas de trabajo, su rendimiento necesita así como solucionar problemas de consultas de larga duración. También necesitará tooperform algunos permisos de toomanage de tareas de seguridad para los usuarios e inicios de sesión.

Esta información general describe estos aspectos de Almacenamiento de datos SQL.

* Herramientas de administración
* Escalado de proceso
* Pausa y reanudación
* Prácticas recomendadas de rendimiento
* Supervisión de consulta
* Seguridad
* Copia de seguridad y restauración

## <a name="management-tools"></a>Herramientas de administración
Puede usar una variedad de bases de datos de herramientas toomanage en el almacén de datos de SQL. Administrar bases de datos, desarrollará preferencias de herramientas para cada tipo de tarea debe tooperform.

### <a name="azure-portal"></a>Azure Portal
Hola [portal de Azure] [ Azure portal] es un portal basado en web donde puede crear, actualizar y eliminar las bases de datos y supervisar los recursos de base de datos. Esta herramienta es muy útil es si principiante con Azure, administra un pequeño número de bases de datos de almacenamiento de datos, o necesita tooquickly realizar alguna acción.

tooget partió Hola portal de Azure, consulte [crear un almacén de datos de SQL (portal de Azure)][Create a SQL Data Warehouse (Azure portal)].

### <a name="sql-server-data-tools-in-visual-studio"></a>SQL Server Data Tools en Visual Studio
[SQL Server Data Tools] [ SQL Server Data Tools] (SSDT) de Visual Studio le permite tooconnect administrar y desarrollar las bases de datos. Si es un programador familiarizado con Visual Studio o con otros entornos de desarrollo integrado (IDE), pruebe a usar SSDT en Visual Studio.

SSDT incluye Hola Explorador de objetos de SQL Server que permite toovisualize, conectar y ejecutar scripts en bases de datos de almacenamiento de datos SQL. tooquickly conectar tooSQL almacenamiento de datos, puede hacer simplemente clic en hello **abierta en Visual Studio** botón de barra de comandos de hello al ver los detalles de la base de datos de Hola Hola Portal clásico de Azure.  

tooget comenzar con SSDT en Visual Studio, vea [consulta el almacenamiento de datos de SQL de Azure con Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].

### <a name="command-line-tools"></a>Herramientas de línea de comandos
Las herramientas de línea de comandos son ideales para automatizar las cargas de trabajo.  PowerShell y sqlcmd son dos tooautomate formas estupendas los procesos.  Se recomienda que estas herramientas para administrar un gran número de servidores lógicos e implementar los cambios de recursos en un entorno de producción como tareas de hello necesarias se pueden incluir en un script y automatizadas, a continuación.

### <a name="dynamic-management-views"></a>Vistas de administración dinámica
DMV son Hola cotidianas de la administración de almacenamiento de datos SQL. Casi toda la información que se presenta en el portal de Hola se basa en las DMV. toosee una lista de las DMV de almacenamiento de datos de SQL, consulte [vistas del sistema de almacenamiento de datos SQL][SQL Data Warehouse system views].

tooget iniciado, consulte [conectar y consultas con sqlcmd][Connect and query with sqlcmd], y [crear una base de datos (PowerShell)][Create a database (PowerShell)].

## <a name="scale-compute"></a>Escalado de proceso
En Almacenamiento de datos SQL, puede escalar horizontalmente o de nuevo de forma rápida el rendimiento mediante el aumento o disminución de los recursos de proceso de la CPU, la memoria y el ancho de banda de E/S. rendimiento de tooscale, todo lo que necesita toodo es ajustar Hola número de unidades de almacenamiento de datos (a Dwu) que el almacenamiento de datos SQL asigna tooyour base de datos. Almacenamiento de datos SQL hace Hola cambiar y controla todos los toohardware de cambios subyacente de Hola o software rápidamente.

vea toolearn más información acerca de ajuste de escala a Dwu, [escalar el rendimiento].

## <a name="pause-and-resume"></a>Pausa y reanudación
los costos de toosave, puede pausar y reanudar proceso recursos a petición. Por ejemplo, si no va a usar base de datos de Hola durante la noche de Hola y fines de semana, puede pausar en esos momentos y reanudar durante el día de Hola. Que no cobra por a Dwu mientras la base de datos de hello está detenida.

Para obtener más información, consulte [Pausa del proceso][Pause compute] y [Reanudación del proceso][Resume compute].

## <a name="performance-best-practices"></a>Prácticas recomendadas de rendimiento
Cuando comienza a trabajar con una nueva tecnología, detectar Hola sugerencias y trucos que funcionan mejor derecho de inicio de hello puede ahorrar una gran cantidad de tiempo.  Encontrará procedimientos recomendados a lo largo de muchos de nuestros temas.

toosee muchos un resumen de consideraciones más importantes de hello al desarrollar la carga de trabajo, consulte [prácticas recomendadas de almacenamiento de datos de SQL][SQL Data Warehouse Best Practices].

## <a name="query-monitoring"></a>Supervisión de consulta
A veces se ejecuta una consulta demasiado larga, pero no está seguro de cuál es la causa de Hola. Almacenamiento de datos de SQL tiene vistas de administración dinámica (DMV) que se puede usar toofigure out qué consulta está tardando demasiado.

consultas de larga duración toofind, consulte [supervisar la carga de trabajo mediante DMV][Monitor your workload using DMVs].

## <a name="security"></a>Seguridad
toomaintain un sistema seguro, debe ser de alerta de Hola y protegerse contra cualquier tipo de acceso no autorizado. Un sistema de seguridad debe toomake seguro de las reglas de firewall están en vigor autorizado por lo que solo pueden conectarse a direcciones IP. Necesita la autenticación correcta de las credenciales de usuario. Después de que un usuario ha conectado toohello base de datos, el usuario de hello solamente debe tener permisos tooperform un número mínimo de acciones. toosecure datos, puede usar el cifrado. También es importante toohave de auditoría y seguimiento para volver a trazar eventos si hay cualquier actividad sospechosa.

toolearn acerca de cómo administrar la seguridad, visite toohello [información general sobre seguridad][Security overview].

## <a name="backup-and-restore"></a>Copia de seguridad y restauración
Una parte esencial de cualquier base de datos de producción es contar con copias de seguridad confiables de los datos. Almacenamiento de datos SQL mantiene los datos seguros al realizar automáticamente una copia de seguridad de las bases de datos activas a intervalos regulares. Estas copias de seguridad le permiten toorecover de escenarios donde ha dañado los datos o se elimina accidentalmente los datos o la base de datos.  Para la programación de copia de seguridad de datos de hello, directiva de retención y toorestore una base de datos, vea [restaurar a partir de la instantánea][Restore from snapshot].

## <a name="next-steps"></a>Pasos siguientes
Usar principios de diseño de bases de datos eficaces le resultará más fácil toomanage las bases de datos en el almacén de datos de SQL. toolearn más, visite toohello [Introducción al desarrollo de][Development overview].

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse (Azure Portal)]: sql-data-warehouse-get-started-provision.md
[Create a database (PowerShell)]: sql-data-warehouse-get-started-provision-powershell.md
[connection]: sql-data-warehouse-develop-connections.md
[Query Azure SQL Data Warehouse with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[Connect and query with sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md
[Development overview]: sql-data-warehouse-overview-develop.md
[Monitor your workload using DMVs]: sql-data-warehouse-manage-monitor.md
[Pause compute]: sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Restore from snapshot]: sql-data-warehouse-restore-database-overview.md
[Resume compute]: sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[escalar el rendimiento]: sql-data-warehouse-manage-compute-overview.md#scale-compute
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
