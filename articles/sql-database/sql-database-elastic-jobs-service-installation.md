---
title: "trabajos de base de datos elástica aaaInstalling | Documentos de Microsoft"
description: "Guiará a través de la instalación de función de trabajo elástico Hola."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0349f66a4428f81d00d43681d7f2177f273ec032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="installing-elastic-database-jobs-overview"></a>Información general sobre la instalación de Trabajos de base de datos elástica
[**Trabajos de base de datos elásticos** ](sql-database-elastic-jobs-overview.md) puede instalarse a través de PowerShell o a través de hello Portal.You clásico de Azure puede obtener acceso a toocreate y administrar los trabajos mediante Hola API de PowerShell solo si instalar paquetes de PowerShell de Hola. Además, Hola PowerShell APIs proporcionan una funcionalidad significativamente mayor que el portal de hello en este momento.

Si ya ha instalado **trabajos de base de datos elástica** a través de hello Portal desde una existente **grupo elástico**, última versión preliminar Powershell Hola incluye secuencias de comandos tooupgrade la instalación existente. Es altamente recomendado tooupgrade su toohello de instalación más reciente **trabajos de base de datos elástica** componentes en orden tootake aprovechar las nuevas funcionalidades expuestas a través de Hola PowerShell APIs.

## <a name="prerequisites"></a>Requisitos previos
* Una suscripción de Azure. Para obtener una versión de evaluación gratuita, consulte [Versión de evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Azure PowerShell. Instalar la versión más reciente hello mediante hello [instalador de plataforma Web](http://go.microsoft.com/fwlink/p/?linkid=320376). Para obtener información detallada, vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).
* [Utilidad de línea de comandos de NuGet](https://nuget.org/nuget.exe) es tooinstall usado Hola bases de datos elásticas trabajos paquete. Para obtener más información, consulte http://docs.nuget.org/docs/start-here/installing-nuget.

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a>Descargue e importe el paquete de PowerShell de trabajos de bases de datos elásticas Hola
1. Inicia la ventana de comandos de PowerShell de Microsoft Azure y ve directorio toohello donde descargó la utilidad de línea de comandos del NuGet (nuget.exe).
2. Descargue e importe **trabajos de base de datos elástica** paquete en el directorio actual de hello con hello siguiente comando:
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    Hola **trabajos de base de datos elástica** archivos se colocan en el directorio local de hello en una carpeta denominada **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** donde *x.x.xxxx.x* refleja el número de versión de Hola. cmdlets de PowerShell de Hello (incluidos los archivos .dll de cliente necesario) se encuentran en hello **tools\ElasticDatabaseJobs** subdirectorio hello tooinstall de secuencias de comandos de PowerShell, actualizar y desinstalar también residen en hello  **herramientas** subdirectorio.
3. Desplácese subdirectorio herramientas toohello bajo la carpeta de hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x escribiendo cd de herramientas, por ejemplo:
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. Ejecute el directorio de hello.\InstallElasticDatabaseJobsCmdlets.ps1 scripts toocopy hello ElasticDatabaseJobs en $home\Documents\WindowsPowerShell\Modules. Esto también importará automáticamente módulo Hola para su uso, por ejemplo:
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a>Instalar componentes de trabajos de bases de datos elásticas hello mediante PowerShell
1. Inicia una ventana de comandos de PowerShell de Microsoft Azure y ve toohello \tools subdirectorio bajo la carpeta de Hola Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x: escriba cd \tools
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. Ejecutar script de PowerShell de hello.\InstallElasticDatabaseJobs.ps1 y suministrar valores de sus variables solicitados. Esta secuencia de comandos creará los componentes de hello descritos en [bases de datos elásticas trabajos componentes y precios](sql-database-elastic-jobs-overview.md#components-and-pricing) además de configurar Hola servicio de nube de Azure tooappropriately usan componentes dependientes de Hola.

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

Al ejecutar este comando, se abrirá una ventana para especificar el **nombre de usuario** y la **contraseña**. No trata sus credenciales de Azure, escriba el nombre de usuario de Hola y la contraseña que se desea toocreate para el nuevo servidor de hello las credenciales de administrador de Hola.

parámetros de Hello proporcionados en esta invocación de ejemplo pueden modificarse para la configuración deseada. siguiente Hola proporciona más información sobre el comportamiento de Hola de cada parámetro:

<table style="width:100%">
  <tr>
    <th>Parámetro</th>
    <th>Description</th>
  </tr>

<tr>
    <td>ResourceGroupName</td>
    <td>Proporciona el nombre del grupo de recursos de Azure de hello creado hello toocontain que acaba de crear componentes de Azure. Este parámetro tiene como valor predeterminado demasiado "__ElasticDatabaseJob". No es recomendable toochange este valor.</td>
    </tr>

</tr>

    <tr>
    <td>ResourceGroupLocation</td>
    <td>Proporciona hello toobe de ubicación de Azure permiten Hola que acaba de crear componentes de Azure. Este parámetro tiene como valor predeterminado toohello ubicación Central US.</td>
</tr>

<tr>
    <td>ServiceWorkerCount</td>
    <td>Proporciona el número de Hola de tooinstall de los trabajadores de servicio. Este parámetro tiene como valor predeterminado too1. Un número mayor de los trabajadores puede ser usado tooscale out Hola servicio y tooprovide alta disponibilidad. Se recomienda toouse "2" para las implementaciones que necesitan una alta disponibilidad del servicio de Hola.</td>
    </tr>

</tr>
    <tr>
    <td>ServiceVmSize</td>
    <td>Proporciona el tamaño VM de hello para el uso dentro de hello servicio en la nube. Este parámetro tiene como valor predeterminado tooA0. Se aceptan valores de parámetros de A0/A1 y A2/A3 que hacer al trabajo de hello rol toouse un tamaño ExtraSmall/pequeño/mediano/grande, respectivamente. Para obtener más información sobre los tamaños de rol de trabajo, consulte [Componentes y precios de trabajos de base de datos elástica](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</tr>
    <tr>
    <td>SqlServerDatabaseSlo</td>
    <td>Proporciona el objetivo de nivel de servicio de Hola para un servidor Standard edition. Este parámetro tiene como valor predeterminado tooS0. Se aceptan valores de parámetro de S0, S1, S2 y S3 que hacer Hola base de datos de SQL Azure toouse Hola respectivo SLO. Para obtener más información sobre SLO de SQL Database, consulte [Componentes y precios de trabajos de base de datos elástica](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorUserName</td>
    <td>Proporciona el nombre de usuario de administrador de Hola para hello que acaba de crear el servidor de base de datos de SQL Azure. Cuando no se especifica, abrirá a una ventana de credenciales de PowerShell tooprompt credenciales Hola.</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorPassword</td>
    <td>Proporciona la contraseña de administrador de Hola para hello que acaba de crear el servidor de base de datos de SQL Azure. Cuando no se proporciona una ventana de credenciales PowerShell abrirá tooprompt credenciales Hola.</td>
</tr>
</table>

Para los sistemas que tienen como destino con un número grande de trabajos que se ejecutan en paralelo en un gran número de bases de datos, se recomienda como parámetros de toospecify: ServiceWorkerCount - 2 - ServiceVmSize A2 - SqlServerDatabaseSlo S2.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a>Actualización de una instalación existente de componentes de Trabajos de base de datos elástica mediante PowerShell
**trabajos de base de datos elástica** se pueden actualizar en una instalación existente para escalado y alta disponibilidad. Este proceso permite futuras actualizaciones de código de servicio sin necesidad de toodrop y volver a crear la base de datos de control de Hola. Este proceso también puede usarse en hello misma versión toomodify Hola servicio VM tamaño u Hola servidor worker del recuento.

tamaño de máquina virtual de hello tooupdate de una instalación, Hola ejecución siguiente secuencia de comandos con parámetros actualiza los valores de toohello de su elección.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th>Parámetro</th>
  <th>Description</th>
</tr>

  <tr>
    <td>ResourceGroupName</td>
    <td>Identifica el nombre del grupo de recursos de Azure de hello utilizado al instalar componentes de trabajo de base de datos elástica de hello inicialmente. Este parámetro tiene como valor predeterminado demasiado "__ElasticDatabaseJob". Ya que no es recomendable toochange este valor, que no debería haber toospecify este parámetro.</td>
    </tr>
</tr>

</tr>

  <tr>
    <td>ServiceWorkerCount</td>
    <td>Proporciona el número de Hola de tooinstall de los trabajadores de servicio.  Este parámetro tiene como valor predeterminado too1.  Un número mayor de los trabajadores puede ser usado tooscale out Hola servicio y tooprovide alta disponibilidad.  Se recomienda toouse "2" para las implementaciones que necesitan una alta disponibilidad del servicio de Hola.</td>
</tr>

</tr>

    <tr>
    <td>ServiceVmSize</td>
    <td>Proporciona el tamaño VM de hello para el uso dentro de hello servicio en la nube. Este parámetro tiene como valor predeterminado tooA0. Se aceptan valores de parámetros de A0/A1 y A2/A3 que hacer al trabajo de hello rol toouse un tamaño ExtraSmall/pequeño/mediano/grande, respectivamente. Para obtener más información sobre los tamaños de rol de trabajo, consulte [Componentes y precios de trabajos de base de datos elástica](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a>Instalar componentes de trabajos de bases de datos elásticas hello mediante Hola Portal
Una vez que tenga [crea un grupo elástico](sql-database-elastic-pool-manage-portal.md), puede instalar **trabajos de base de datos elástica** ejecución tooenable de componentes de las tareas administrativas en cada base de datos en el grupo elástico Hola. A diferencia de cuando utilizando Hola **trabajos de base de datos elástica** PowerShell APIs, interfaz del portal de hello está restringido actualmente tooonly ejecutar en un grupo existente.

**Estimado toocomplete de tiempo:** 10 minutos.

1. Desde la vista de panel de Hola de grupo elástico de Hola a través de hello [Portal de Azure](https://portal.azure.com/#) , haga clic en **crear trabajo**.
2. Si va a crear un trabajo para hello primera vez, debe instalar **trabajos de base de datos elástica** haciendo clic en **términos de vista previa**.
3. Aceptar términos Hola haciendo clic en Hola casilla de verificación.
4. En la vista de Hola "instalar servicios", haga clic en **CREDENCIALES de trabajo**.
   
    ![Instalar servicios de Hola][1]
5. Escriba un nombre de usuario y una contraseña de administración de la base de datos. Como parte de la instalación de hello, se crea un nuevo servidor de base de datos de SQL Azure. Dentro de este nuevo servidor, una nueva base de datos, conocida como base de datos de control de hello, se crea y utiliza los metadatos de hello toocontain para los trabajos de base de datos elástica. nombre de usuario de Hello y una contraseña creados aquí se usan a fin de hello del inicio de sesión de base de datos de control de toohello. Se usa una credencial independiente para la ejecución de secuencias de comandos en bases de datos de hello en el grupo de Hola.
   
    ![Creación del nombre de usuario y la contraseña][2]
6. Haga clic en el botón Aceptar Hola. componentes de Hola se crean automáticamente en unos minutos en una nueva [grupo de recursos](../azure-resource-manager/resource-group-overview.md). nuevo grupo de recursos Hola está anclado toohello iniciar panel, tal y como se muestra a continuación. Todos los trabajos de base de datos una vez creados, elástica (servicio en la nube, base de datos SQL, Bus de servicio y almacenamiento) se crean en el grupo de Hola.
   
    ![Grupo de recursos en el panel de inicio][3]
7. Si intenta toocreate o administrar un trabajo mientras se está instalando los trabajos de base de datos elástica, al proporcionar **credenciales** , verá el siguiente mensaje de Hola.
   
    ![Implementación en curso][4]

Si se requiere la desinstalación, elimine el grupo de recursos de Hola. Vea [cómo toouninstall Hola bases de datos elásticas trabajo componentes](sql-database-elastic-jobs-uninstall.md).

## <a name="next-steps"></a>Pasos siguientes
Asegúrese de una credencial con los derechos apropiados de hello para la ejecución del script se crea en cada base de datos del grupo de hello, para más información, vea [proteger la base de datos de SQL](sql-database-manage-logins.md).
Vea [crear y administrar los trabajos de una base de datos elástica](sql-database-elastic-jobs-create-and-manage.md) tooget iniciado.

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
