---
title: aaaDistributed transacciones entre bases de datos en la nube
description: "Introducción sobre las transacciones de base de datos elástica con Base de datos SQL de Azure"
services: sql-database
documentationcenter: 
author: torsteng
manager: jhubbard
editor: torsteng
ms.assetid: e14df7a3-7788-4cfb-bcd1-7ad6433ef1f9
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: sql-database
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 9a18f2749108d337bf115b3dc21dd0c7828dd9c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-transactions-across-cloud-databases"></a>Introducción sobre las transacciones de base de datos elástica con Base de datos SQL de Azure
Transacciones de bases de datos elástica para base de datos de SQL de Azure (base de datos SQL) le permiten transacciones toorun que abarcan varias bases de datos en la base de datos SQL. Las transacciones de base de datos elástica para base de datos SQL están disponibles para aplicaciones .NET mediante ADO .NET e integrar con experiencia de programación familiar hello mediante hello [System.Transaction](https://msdn.microsoft.com/library/system.transactions.aspx) clases. biblioteca de hello tooget, consulte [.NET Framework 4.6.1 (instalador Web)](https://www.microsoft.com/download/details.aspx?id=49981).

De forma local, este escenario requiere normalmente la ejecución del Coordinador de transacciones distribuidas de Microsoft (MSDTC). Puesto que MSDTC no está disponible para la aplicación de plataforma como servicio en Azure, las transacciones de hello capacidad toocoordinate distribuida se ahora ha directamente integrado en la base de datos SQL. Las aplicaciones pueden conectarse a las transacciones toolaunch distribuida de base de datos SQL de tooany y una de las bases de datos de hello transparente coordinará transacción Hola distribuida, como se muestra en la figura siguiente de Hola. 

  ![Transacciones distribuidas con Base de datos SQL de Azure mediante transacciones de base de datos elástica ][1]

## <a name="common-scenarios"></a>Escenarios comunes
Las transacciones de base de datos elástica para base de datos SQL habilitar aplicaciones toomake cambios atómicos toodata almacenado en varias bases de datos diferentes de SQL. vista previa de Hola se centra en las experiencias de desarrollo en el cliente en C# y. NET. Para más adelante está prevista una experiencia en el lado servidor mediante T-SQL.  
Hola de destinos de las transacciones de base de datos elástica los escenarios siguientes:

* Aplicaciones de varias bases de datos en Azure: con este escenario, los datos se particionan verticalmente entre varias bases de datos de Base de datos SQL de forma que diferentes clases de datos residen en diferentes bases de datos. Algunas operaciones requieren toodata de cambios que se mantiene en dos o más bases de datos. aplicación Hello usa cambios de hello toocoordinate de base de datos elástica transacciones entre bases de datos y garantizar la atomicidad.
* Aplicaciones de base de datos particionada en Azure: con este escenario, la capa de datos de Hola usa hello [biblioteca de cliente de base de datos elástica](sql-database-elastic-database-client-library.md) o toohorizontally de particionamiento automático partición Hola datos entre varias bases de datos en la base de datos SQL. Un caso de uso principales resulta cambios atómicos tooperform de hello necesario para una aplicación de varios inquilinos particionada cambios abarcan los inquilinos. Piense en una transferencia de un inquilino tooanother, ambos que residen en diferentes bases de datos para la instancia. Un segundo caso es específica particionamiento tooaccommodate las necesidades de capacidad para un inquilino de gran tamaño que a su vez suele implicar que algunos toostretch de necesidades de operaciones atómicas en varias bases de datos utilizadas para hello mismo inquilino. Un tercer caso es tooreference una actualización atómica de datos que se replican a través de las bases de datos. Ahora se pueden coordinar operaciones atómicas, transacciones, a lo largo de estas líneas a través de varias bases de datos mediante la vista previa de Hola.
  Las transacciones de base de datos elástica usan atomicidad de transacciones de confirmación en dos fases tooensure entre bases de datos. Esto resulta adecuado para transacciones que suponen menos de 100 bases de datos a la vez en una única transacción. No se aplican estos límites, pero uno debe esperar tasas de éxito para toosuffer de las transacciones de bases de datos elásticas y rendimiento cuando superen estos límites.

## <a name="installation-and-migration"></a>Instalación y migración
se proporcionan capacidades de Hola para las transacciones de base de datos elástica de base de datos SQL a través de bibliotecas de .NET de las actualizaciones toohello System.Data.dll y System.Transactions.dll. Hello dll asegurarse de que se confirman en dos fases se utiliza cuando sea necesario tooensure atomicidad. el uso de transacciones de base de datos elástica, desarrollo de aplicaciones de toostart instalar [.NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981) o una versión posterior. Cuando se ejecuta en una versión anterior de .NET framework de hello, las transacciones se producirá un error toopromote tooa distribuida transaction y se producirá una excepción.

Después de la instalación, puede usar transacciones distribuida de hello API de System.Transactions con conexiones tooSQL DB. Si tiene aplicaciones existentes de MSDTC que utilizan estas API, basta con volver a generar las aplicaciones existentes de .NET 4.6 después de instalar Hola 4.6.1 Framework. Si los proyectos destinados a .NET 4.6, usarán automáticamente archivos DLL de hello actualizado de la nueva versión de Framework hello y llamadas de API de transacciones distribuidas en combinación con tooSQL conexiones que DB ahora se realizará correctamente.

Recuerde que las transacciones de base de datos elástica no precisan la instalación de MSDTC. Por el contrario, se administran directamente mediante y dentro de Base de datos SQL. Esto simplifica notablemente escenarios de nube como una implementación de MSDTC no es necesario toouse distribuida transacciones con la base de datos SQL. Sección 4 se explica con más detalle cómo Hola y las transacciones de base de datos elástica toodeploy requieren .NET framework junto con su tooAzure de aplicaciones de nube.

## <a name="development-experience"></a>Experiencia de desarrollo
### <a name="multi-database-applications"></a>Aplicaciones de varias bases de datos
Hello código de ejemplo siguiente utiliza experiencia de programación familiar Hola con .NET System.Transactions. Hola TransactionScope, clase establece una transacción de ambiente en. NET. (Una "transacción ambiente" es uno que reside en el subproceso actual de hello). Todas las conexiones abiertas dentro de hello TransactionScope participan en transacciones de Hola. Si diferentes bases de datos participan, hello es transacción tooa automáticamente con privilegios elevados distribuida. resultado de Hello de transacción de Hola se controla estableciendo Hola ámbito toocomplete tooindicate una confirmación.

    using (var scope = new TransactionScope())
    {
        using (var conn1 = new SqlConnection(connStrDb1))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = new SqlConnection(connStrDb2))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T2 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }

### <a name="sharded-database-applications"></a>Aplicaciones de base de datos particionada
Las transacciones de base de datos elástica para base de datos SQL también admiten coordinar las transacciones distribuidas donde se utiliza método de OpenConnectionForKey de Hola Hola bases de datos elásticas biblioteca tooopen de conexiones de cliente para un repositorio ampliados datos capa. Considere la posibilidad de casos donde es necesario tooguarantee la coherencia transaccional de cambios a través de varios valores de clave de particionamiento diferente. Particiones de toohello conexiones hospedaje de los valores de clave de particionamiento diferente de Hola se asíncrona mediante OpenConnectionForKey. En el caso general de hello, las conexiones de hello pueden ser toodifferent particiones tal que garantizar garantías transaccionales requiere una transacción distribuida. Hola siguiendo el ejemplo de código muestra este enfoque. Se supone que una variable denominada shardmap está toorepresent usa una partición se asignan desde la biblioteca de cliente de base de datos elástica hello:

    using (var scope = new TransactionScope())
    {
        using (var conn1 = shardmap.OpenConnectionForKey(tenantId1, credentialsStr))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = shardmap.OpenConnectionForKey(tenantId2, credentialsStr))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T1 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }


## <a name="net-installation-for-azure-cloud-services"></a>Instalación de .NET para servicios en la nube de Azure
Azure proporciona varias ofertas de aplicaciones de .NET toohost. Está disponible en una comparación de diferentes ofertas de hello [comparación de servicio de aplicaciones de Azure, servicios en la nube y máquinas virtuales](../app-service-web/choose-web-site-cloud-service-vm.md). Si hello SO invitado de oferta de hello es menor que .NET 4.6.1 necesarias para transacciones elásticas, deberá too4.6.1 de SO invitado de tooupgrade Hola. 

Para los servicios de aplicación de Azure, actualiza a invitado toohello que SO no se admite actualmente. Para máquinas de virtuales de Azure, simplemente inicie sesión en hello VM y ejecutar el instalador de Hola para hello más reciente de .NET framework. Para los servicios de nube de Azure, necesita la instalación de hello tooinclude de una versión más reciente de .NET en las tareas de inicio de saludo de la implementación. conceptos de Hola y pasos se documentan en [instalar .NET en un rol de servicio de nube](../cloud-services/cloud-services-dotnet-install-dotnet.md).  

Tenga en cuenta que Hola instalador para .NET 4.6.1 puede requerir más espacio de almacenamiento temporal durante Hola arranque proceso en los servicios de nube de Azure de Hola a instalador de .NET 4.6. tooensure una instalación correcta, se necesita tooincrease almacenamiento temporal para el servicio de nube de Azure en el archivo ServiceDefinition.csdef, en la sección de LocalResources de Hola y configuración del entorno de saludo de la tarea de inicio, como se muestra en la siguiente Hola ejemplo:

    <LocalResources>
    ...
        <LocalStorage name="TEMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
        <LocalStorage name="TMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
        <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
            <Environment>
        ...
                <Variable name="TEMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TEMP']/@path" />
                </Variable>
                <Variable name="TMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TMP']/@path" />
                </Variable>
            </Environment>
        </Task>
    </Startup>

## <a name="transactions-across-multiple-servers"></a>Transacciones entre varios servidores
Se admiten transacciones de la base de datos elástica entre diferentes servidores lógicos en Base de datos SQL de Azure. Cuando las transacciones cruzan los límites del servidor lógico, los servidores participantes Hola primero deben toobe especificado en una relación mutua de comunicación. Una vez que se haya establecido la relación de comunicación de hello, cualquier base de datos en cualquiera de hello dos servidores pueden participar en transacciones elásticas con bases de datos de Hola a otro servidor. Con transacciones distribuidas en más de dos servidores lógicos, una relación de comunicación debe toobe en lugar de cualquier par de servidores lógicos.

Usar hello siguiendo las relaciones de toomanage comunicación entre servidores cmdlets de PowerShell para las transacciones de base de datos elástica:

* **Nueva AzureRmSqlServerCommunicationLink**: Utilice esta toocreate cmdlet una nueva relación de comunicación entre dos servidores lógicos de base de datos de SQL Azure. relación de Hello es simétrica, lo que significa que ambos servidores pueden iniciar transacciones con hello otro servidor.
* **Get-AzureRmSqlServerCommunicationLink**: Utilice esta comunicación existente de cmdlet tooretrieve relaciones y sus propiedades.
* **Remove-AzureRmSqlServerCommunicationLink**: Utilice esta tooremove cmdlet una relación de comunicación existente. 

## <a name="monitoring-transaction-status"></a>Supervisión del estado de la transacción
Usar vistas de administración dinámica (DMV) en la base de datos SQL toomonitor estado y progreso de las transacciones de base de datos elástica en curso. Todos los tootransactions relacionados de DMV son relevantes para las transacciones distribuidas en la base de datos de SQL. Puede encontrar Hola correspondiente lista DMV aquí: [transacciones relacionadas Dynamic Management Views y funciones (Transact-SQL)](https://msdn.microsoft.com/library/ms178621.aspx).

Estas DMV son especialmente útiles:

* **sys.dm\_tran\_active\_transactions**: enumera las transacciones actualmente activas y su estado. Hello columna UOW (unidad de trabajo) puede identificar Hola secundarios diferentes las transacciones que pertenecen toohello mismo una transacción distribuida. Todas las transacciones dentro de hello llevar la misma transacción distribuida Hola mismo valor UOW. Vea hello [documentación DMV](https://msdn.microsoft.com/library/ms174302.aspx) para obtener más detalles.
* **Sys.DM\_tran\_base de datos\_transacciones**: proporciona información adicional sobre las transacciones, como la colocación de transacción de hello en el registro de hello. Vea hello [documentación DMV](https://msdn.microsoft.com/library/ms186957.aspx) para obtener más detalles.
* **Sys.DM\_tran\_bloqueos**: proporciona información sobre los bloqueos de Hola que actualmente se incluyen en las transacciones en curso. Vea hello [documentación DMV](https://msdn.microsoft.com/library/ms190345.aspx) para obtener más detalles.

## <a name="limitations"></a>Limitaciones
Hola después actualmente limitaciones aplica tooelastic transacciones de bases de datos en la base de datos SQL:

* Se admiten únicamente transacciones entre bases de datos en Base de datos SQL. Otros proveedores de recursos y bases de datos de [X/Open XA](https://en.wikipedia.org/wiki/X/Open_XA) externos a Base de datos SQL no podrán participar en transacciones de base de datos elástica. Esto significa que dichas transacciones no pueden extenderse entre bases de datos locales de SQL Server y SQL de Azure. Para las transacciones distribuidas de forma local, continuar toouse MSDTC. 
* Solo se admiten transacciones coordinadas por el cliente desde una aplicación .NET. Está prevista la compatibilidad en el lado servidor con T-SQL, por ejemplo, INICIAR TRANSACCIÓN DISTRIBUIDA, pero aún no se encuentra disponible. 
* No se admiten las transacciones por los servicios de WCF. Por ejemplo, tiene un método de servicio de WCF que se ejecuta una transacción. Envolvente Hola llamada dentro de un ámbito de transacción se producirá un error como un [System.ServiceModel.ProtocolException](https://msdn.microsoft.com/library/system.servicemodel.protocolexception).

## <a name="next-steps"></a>Pasos siguientes
Si tiene preguntas, póngase en contacto toous en hello [foro de base de datos SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) y para las solicitudes de características, agréguelos toohello [foro de comentarios de la base de datos SQL](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-transactions-overview/distributed-transactions.png



