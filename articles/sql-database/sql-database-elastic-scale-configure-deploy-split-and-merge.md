---
title: un servicio de dividir-combinar aaaDeploy | Documentos de Microsoft
description: "División y combinación con las herramientas de Base de datos elástica"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 9a993c0f-7052-46cd-aa59-073bea8d535a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6fef641cbc1e73ce34a851c53298a072dade8f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-split-merge-service"></a>Implemente un servicio de división y combinación
herramienta Dividir-combinar de Hello permite mover datos entre bases de datos particionadas. Consulte [Mover datos entre bases de datos en la nube escaladas horizontalmente](sql-database-elastic-scale-overview-split-and-merge.md)

## <a name="download-hello-split-merge-packages"></a>Descargar los paquetes de saludo dividir-combinar
1. Descargar Hola versión más reciente de NuGet desde [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).
2. Abra un símbolo del sistema y desplácese directorio toohello donde descargó nuget.exe. descarga de Hello incluye commmands de PowerShell.
3. Descargue el paquete de división y combinación más reciente de hello en el directorio actual de hello con hello comando siguiente:
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

Hola archivos se colocan en un directorio denominado **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** donde *x.x.xxx.x* refleja el número de versión de Hola. Buscar archivos de servicio de dividir-combinar de hello en hello **content\splitmerge\service** subdirectorio, Hola dividir-combinar PowerShell (y los scripts y archivos .dll de cliente necesario) en hello **content\splitmerge\powershell** subdirectorio.

## <a name="prerequisites"></a>Requisitos previos
1. Crear una base de datos de la base de datos de SQL Azure que se usará como base de datos de estado de la división y combinación de Hola. Vaya toohello [portal de Azure](https://portal.azure.com). Cree una nueva **Base de datos SQL**. Asigne un nombre de base de datos de Hola y cree un nuevo administrador y una contraseña. Estar seguro de nombre de hello toorecord y la contraseña para su uso posterior.
2. Asegúrese de que el servidor de base de datos de SQL Azure permite tooit tooconnect de servicios de Azure. En portal Hola Hola **configuración del Firewall**, asegúrese de que hello **permitir acceso a servicios de tooAzure** opción se establece demasiado**en**. Haga clic en hello "Guardar" icono.
   
   ![Servicios permitidos][1]
3. Cree una cuenta de almacenamiento de Azure que se usará para la salida de diagnóstico. Vaya toohello Portal de Azure. En la barra de la izquierda hello, haga clic en **New**, haga clic en **datos + almacenamiento**, a continuación, **almacenamiento**.
4. Cree un servicio en la nube de Azure que contendrá el servicio de División y combinación.  Vaya toohello Portal de Azure. En la barra de la izquierda hello, haga clic en **New**, a continuación, **proceso**, **servicio de nube**, y **crear**. 

## <a name="configure-your-split-merge-service"></a>Configuración del servicio de división y combinación
### <a name="split-merge-service-configuration"></a>Configuración del servicio División y combinación
1. En carpeta de Hola donde descargó los ensamblados de hello dividir-combinar, cree una copia del programa Hola a **ServiceConfiguration.Template.cscfg** archivo que publicó junto con **SplitMergeService.cspkg** y cambie su nombre **ServiceConfiguration.cscfg**.
2. Abra **ServiceConfiguration.cscfg** en un editor de texto como Visual Studio que valida las entradas como formato de Hola de huellas digitales de certificado.
3. Crear una nueva base de datos o elija un tooserve de base de datos existente como base de datos de estado de Hola para las operaciones de combinación de división y recuperar la cadena de conexión de Hola de esa base de datos. 
   
   > [!IMPORTANT]
   > En este momento, base de datos de estado de hello debe usar intercalación latina hello (SQL\_Latin1\_General\_CP1\_CI\_AS). Para obtener más información, vea [Nombre de intercalación de Windows (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).
   >

   Con la base de datos de SQL Azure, cadena de conexión de hello normalmente tiene el formato de hello:
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. Escriba esta cadena de conexión en el archivo cscfg de hello en ambos hello **SplitMergeWeb** y **SplitMergeWorker** secciones de rol en la configuración de ElasticScaleMetadata Hola.
5. Para hello **SplitMergeWorker** rol, escriba un almacenamiento de tooAzure de cadena de conexión válida para hello **WorkerRoleSynchronizationStorageAccountConnectionString** configuración.

### <a name="configure-security"></a>Configuración de seguridad
Para obtener instrucciones detalladas tooconfigure Hola la seguridad del servicio de hello, consulte toohello [dividir-combinar la configuración de seguridad](sql-database-elastic-scale-split-merge-security-configuration.md).

Por motivos de Hola de una implementación de prueba sencilla para este tutorial, un conjunto mínimo de configuración pasos serán realiza servicio de hello tooget activos y en funcionamiento. Estos pasos habilitan solo Hola una máquina/cuenta ejecutarlas toocommunicate con el servicio de Hola.

### <a name="create-a-self-signed-certificate"></a>Creación de un certificado autofirmado
Crear un nuevo directorio y desde este Hola execute de directorio después de comando mediante un [símbolo del sistema para desarrolladores de Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) ventana:

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

Se le pedirá una clave privada de contraseña tooprotect Hola. Escriba una contraseña segura y confírmela. A continuación, se pedirá Hola contraseña toobe utilizado después de una vez más. Haga clic en **Sí** en hello final tooimport se toohello almacén de raíz de las entidades de certificación de confianza.

### <a name="create-a-pfx-file"></a>Creación de un archivo PFX
Ejecutar Hola siguiente comando de hello misma ventana donde se ejecutó makecert; Use Hola misma contraseña usa toocreate Hola certificado:

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-hello-client-certificate-into-hello-personal-store"></a>Importar el certificado de cliente de hello en el almacén personal de Hola
1. En el Explorador de Windows, haga doble clic en **MyCert.pfx**.
2. Hola **Asistente para importar certificados** seleccione **usuario actual** y haga clic en **siguiente**.
3. Confirmar la ruta de acceso de archivo de Hola y haga clic en **siguiente**.
4. Escriba la contraseña hello, deje **incluyen todas las propiedades extendidas** activada y haga clic en **siguiente**.
5. Deje **almacén de certificados de hello seleccionar automáticamente [...]**  activada y haga clic en **siguiente**.
6. Haga clic en **Finalizar** y en **Aceptar**.

### <a name="upload-hello-pfx-file-toohello-cloud-service"></a>Cargar el servicio de nube de hello PFX archivo toohello
1. Vaya toohello [Portal de Azure](https://portal.azure.com).
2. Seleccione **Servicios en la nube**.
3. Seleccione servicio de nube de Hola que creó anteriormente para el servicio de dividir y combinar Hola.
4. Haga clic en **certificados** en el menú superior Hola.
5. Haga clic en **cargar** en la barra de la parte inferior de Hola.
6. Seleccione el archivo PFX de hello y escriba Hola misma contraseña anterior.
7. Una vez completado, copie huella digital del certificado Hola de nueva entrada de hello en lista de Hola.

### <a name="update-hello-service-configuration-file"></a>Archivo de configuración de servicio de actualización Hola
Pegue la huella digital del certificado Hola copiado anteriormente en el atributo/valor de huella digital de Hola de estos valores.
Para el rol de trabajo de hello:
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

Para el rol de hello web:

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

Tenga en cuenta que para las implementaciones de producción se deben usar certificados independientes para hello entidad emisora de certificados para el cifrado, Hola certificado de servidor y certificados de cliente. Para obtener instrucciones detalladas al respecto, consulte [Configuración de seguridad](sql-database-elastic-scale-split-merge-security-configuration.md).

## <a name="deploy-your-service"></a>Implementación del servicio
1. Vaya toohello [portal de Azure](https://manage.windowsazure.com).
2. Haga clic en hello **servicios en la nube** ficha Hola izquierda y seleccione servicio de nube de Hola que creó anteriormente.
3. Haga clic en **Panel**.
4. Elija el entorno de ensayo de hello, a continuación, haga clic en **cargue una nueva implementación de ensayo**.
   
   ![Ensayo][3]
5. En el cuadro de diálogo de hello, escriba una etiqueta de implementación. Para "Paquete" y "Configuration", haga clic en 'Desde Local' y elija hello **SplitMergeService.cspkg** archivo y el archivo de .cscfg que configuró anteriormente.
6. Asegurarse de esa casilla de hello **implementar aunque uno o varios roles contengan una sola instancia** está activada.
7. Pulse el botón de TIC de hello en la implementación de hello inferior derecho toobegin Hola. Esperar tootake toocomplete unos minutos.

   ![Cargar][4]

## <a name="troubleshoot-hello-deployment"></a>Solucionar problemas de implementación de Hola
Si su rol web se produce un error toocome en línea, es probable que un problema con la configuración de seguridad de Hola. Compruebe que Hola que SSL está configurado como se describió anteriormente.

Si se produce un error en el rol de trabajo toocome en línea, pero su rol web se realiza correctamente, es más probable es que un problema de conexión de base de datos de estado de toohello que creó anteriormente.

* Asegúrese de que la cadena de conexión de hello en su .cscfg es preciso.
* Compruebe que existen bases de datos y servidor hello, y que los Id. de usuario de Hola y contraseña son correctos.
* Base de datos de SQL Azure, cadena de conexión de hello debería tener Hola forma:

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* Asegúrese de no comienza con ese nombre de servidor hello **https://**.
* Asegúrese de que el servidor de base de datos de SQL Azure permite tooit tooconnect de servicios de Azure. toodo, abra https://manage.windowsazure.com, haga clic en "Bases de datos de SQL" en hello izquierda, haga clic en "Servidores" en la parte superior de Hola y seleccione el servidor. Haga clic en **configurar** en hello principales y asegúrese de que hello **servicios de Azure** opción se establece demasiado "Sí". (Consulte los requisitos previos de hello en parte superior de Hola de este artículo).

## <a name="test-hello-service-deployment"></a>Probar la implementación del servicio Hola
### <a name="connect-with-a-web-browser"></a>Conexión con un explorador web
Determinar el punto de conexión de hello web del servicio en la combinación de división. Puede encontrar esto en hello Portal clásico de Azure por van toohello **panel** de servicio en la nube y mira **dirección URL del sitio** en el lado derecho de Hola. Reemplace **http://** con **https://** puesto que la configuración de seguridad predeterminada de hello deshabilita el extremo de hello HTTP. Página de Hola de carga para esta dirección URL en el explorador.

### <a name="test-with-powershell-scripts"></a>Pruebas con scripts de PowerShell
implementación de Hola y el entorno se pueden probar mediante la ejecución de scripts de PowerShell de ejemplo de Hola incluido.

archivos de script de Hola incluidos son:

1. **SetupSampleSplitMergeEnvironment.ps1** : configura una capa de datos de prueba para División y combinación (consulte la tabla que aparece a continuación para ver una descripción detallada).
2. **ExecuteSampleSplitMerge.ps1** -ejecuta operaciones de prueba en pruebas de hello (vea la tabla siguiente para obtener una descripción detallada) de nivel de datos
3. **GetMappings.ps1** : nivel superior script que imprima el estado actual de Hola de asignaciones de particiones de Hola de ejemplo.
4. **ShardManagement.psm1** -script de aplicación auxiliar que ajusta Hola ShardManagement API
5. **SqlDatabaseHelpers.psm1**: script auxiliar para crear y administrar bases de datos SQL.
   
   <table style="width:100%">
     <tr>
       <th>Archivo de PowerShell</th>
       <th>Pasos</th>
     </tr>
     <tr>
       <th rowspan="5">SetupSampleSplitMergeEnvironment.ps1</th>
       <td>1.    Crea una base de datos del administrador de mapa de particiones</td>
     </tr>
     <tr>
       <td>2.    Crea dos bases de datos de particiones.
     </tr>
     <tr>
       <td>3.    Crea un mapa de particiones para esas bases de datos (elimina todo mapa de particiones existente en esas bases de datos). </td>
     </tr>
     <tr>
       <td>4.    Crea una tabla pequeña muestra de las particiones de Hola y rellena la tabla de hello en una de las particiones de Hola.</td>
     </tr>
     <tr>
       <td>5.    Declara hello SchemaInfo para tabla particionada Hola.</td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th>Archivo de PowerShell</th>
       <th>Pasos</th>
     </tr>
   <tr>
       <th rowspan="4">ExecuteSampleSplitMerge.ps1 </th>
       <td>1.    Envía un división solicitud toohello dividir-combinar servicio front-end web, que divide los datos de hello mitad de partición segundo de hello primera partición toohello.</td>
     </tr>
     <tr>
       <td>2.    Sondeos hello web front-end para dividir el estado de la solicitud y espera hasta que se complete la solicitud de Hola de Hola.</td>
     </tr>
     <tr>
       <td>3.    Envía un combinación solicitud toohello dividir-combinar servicio front-end web, que mueve los datos de Hola de particiones primera de hello segunda partición toohello atrás.</td>
     </tr>
     <tr>
       <td>4.    Sondeos Hola front-end web para el estado de solicitud de combinación de Hola y espera hasta que se complete la solicitud de saludo.</td>
     </tr>
   </table>
   
## <a name="use-powershell-tooverify-your-deployment"></a>Usar PowerShell tooverify la implementación
1. Abra una nueva ventana de PowerShell, navegue directorio toohello donde descargó el paquete de división y combinación de hello y, a continuación, navegue al directorio de "powershell" Hola.
2. Crear un servidor de base de datos de SQL Azure (o elija un servidor existente) donde se creará el Administrador de mapa de particiones de Hola y particiones.
   
   > [!NOTE]
   > Hola SetupSampleSplitMergeEnvironment.ps1 script crea todas estas bases de datos en hello mismo servidor por script de Hola de tookeep predeterminado simple. Esto no es una restricción de hello dividir-combinar servicio propio.
   >
   
   Un inicio de sesión de autenticación de SQL con toohello de acceso de lectura/escritura que bases de datos serán necesarios para hello dividir-combinar datos de toomove del servicio y actualizar el mapa de particiones de Hola. Puesto que Hola dividir-combinar servicio se ejecuta en la nube de hello, no admite actualmente la autenticación integrada.
   
   Asegúrese de que hello Azure SQL server está configurado tooallow acceso de la dirección IP de Hola de máquina de hello ejecutando estas secuencias de comandos. Puede encontrar esta opción en el servidor de SQL Azure Hola / configuration / direcciones IP permitidas.
3. Ejecutar el entorno de ejemplo de Hola SetupSampleSplitMergeEnvironment.ps1 script toocreate Hola.
   
   Ejecutar este script se borran los datos de administración de mapa de particiones existentes estructuras en la base de datos de administrador de mapa de particiones de Hola y particiones de Hola. Es posible script de Hola toorerun útil si desea inicializar toore mapa de particiones de Hola o particiones.
   
   Línea de comandos de ejemplo:

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. Ejecute hello Getmappings.ps1 tooview Hola asignaciones de scripts que existen actualmente en el entorno de ejemplo de Hola.
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. Ejecute hello ExecuteSampleSplitMerge.ps1 script tooexecute una operación de división (mover los datos de hello mitad particiones segunda de hello primera partición toohello) y, a continuación, una operación de combinación (mover datos de hello volver a la primera partición de hello). Si ha configurado SSL y deshabilita el punto de conexión del http Hola izquierdo, asegúrese de que usa el punto de conexión de hello https:// en su lugar.
   
   Línea de comandos de ejemplo:

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   Si recibes hello debajo de error, más probable es que es un problema con el certificado del extremo de la Web. Intente conectarse de punto de conexión de toohello Web con su explorador Web favorito y compruebe si hay un error de certificado.
   
     ```
     Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLSsecure channel.
     ```
   
   Si se ha realizado correctamente, la salida de hello debe ser similar Hola siguiente:
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. Experimente con otros tipos de datos. Todas estas secuencias de toman un parámetro de - ShardKeyType opcional que le permite el tipo de clave toospecify Hola. valor predeterminado de Hello es Int32, pero también puede especificar Int64, Guid o binario.

## <a name="create-requests"></a>Creación de solicitudes
servicio de Hello puede usarse mediante la interfaz de usuario web de Hola o importar y utilizar el módulo de PowerShell SplitMerge.psm1 Hola que vaya a enviar las solicitudes a través de rol web de Hola.

servicio de Hello puede mover los datos en tablas particionadas y tablas de referencia. Una tabla particionada tiene una columna de clave de particionamiento y distintos datos de fila en cada partición. Una tabla de referencia no está particionada así que contiene Hola mismo fila de datos en cada partición. Tablas de referencia son útiles para los datos que no cambian con frecuencia y es tooJOIN usado con tablas particionadas en las consultas.

En orden tooperform una operación de combinación de división, debe declarar tablas particionadas hello y tablas de referencia que desee toohave movido. Esto se logra con hello **SchemaInfo** API. Esta API está en hello **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** espacio de nombres.

1. Para cada tabla particionada, cree un **ShardedTableInfo** objeto que describe el nombre del esquema de la tabla de hello primario (opcional, valor predeterminado es demasiado "dbo"), Hola nombre de la tabla y Hola nombre de columna de la tabla que contiene la clave de particionamiento de Hola.
2. Para cada tabla de referencia, cree una **ReferenceTableInfo** objeto que describe el nombre del esquema de la tabla de hello primario (opcional, valor predeterminado es demasiado "dbo") y el nombre de la tabla de Hola.
3. Agregar Hola anteriormente TableInfo objetos tooa nueva **SchemaInfo** objeto.
4. Obtener una referencia tooa **ShardMapManager** objeto y llame a **GetSchemaInfoCollection**.
5. Agregar hello **SchemaInfo** toohello **SchemaInfoCollection**, proporcionando el nombre de asignación de particiones de Hola.

Un ejemplo de esto puede verse en hello SetupSampleSplitMergeEnvironment.ps1 script.

Hola servicio dividir-combinar no crea bases de datos de destino de hello (o esquema de tablas de base de datos de hello) automáticamente. Se deben crear previamente antes de enviar un servicio de toohello de solicitud.

## <a name="troubleshooting"></a>Solución de problemas
Cuando se ejecuta scripts de powershell de ejemplo de Hola, puede ver Hola mensaje siguiente:

   ```
   Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLS secure channel.
   ```

Este error significa que el certificado SSL no está configurado correctamente. Siga las instrucciones de hello en la sección 'Conectar con un explorador web'.

Si no se pueden enviar solicitudes, verá lo siguiente:

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

En este caso, compruebe el archivo de configuración, en configuración de hello determinado para **WorkerRoleSynchronizationStorageAccountConnectionString**. Este error suele indicar que ese rol de trabajo hello no pudo inicializar correctamente base de datos de metadatos de Hola por primera vez. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

