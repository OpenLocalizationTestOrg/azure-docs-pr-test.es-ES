<!--author=SharS last changed: 9/17/15-->

En este procedimiento, hará lo siguiente:

1. [Preparar el archivo ejecutable de toorun Hola mantenedor](#to-prepare-to-run-the-maintainer) .
2. [Preparar la base de datos de contenido de Hola y Papelera de reciclaje para su eliminación inmediata de BLOBs huérfanos](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).
3. [Ejecutar Maintainer.exe](#to-run-the-maintainer).
4. [Revertir la base de datos de contenido de Hola y configuración de la Papelera de reciclaje](#to-revert-the-content-database-and-recycle-bin-settings).

#### <a name="tooprepare-toorun-hello-maintainer"></a>tooprepare toorun Hola mantenedor
1. En el servidor front-end Web de hello, abra Hola Shell de administración de SharePoint 2013 como administrador.
2. Desplazarse por las carpetas de toohello *unidad de arranque*: \Program 10.50\Maintainer de almacenamiento remoto de blobs de SQL\.
3. Cambiar el nombre de **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** demasiado**web.config**.
4. Use `aspnet_regiis -pdf connectionStrings` archivo web.config de toodecrypt Hola.
5. En archivo de web.config descifrada de hello, bajo hello `connectionStrings` nodo, agregar la cadena de conexión de hello para la instancia de SQL server y Hola nombre de base de datos de contenido. Vea el siguiente ejemplo de Hola.
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. Use `aspnet_regiis –pef connectionStrings` toore-cifrar el archivo web.config de Hola. 
7. Cambie el nombre tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config de web.config. 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a>base de datos de contenido de hello tooprepare y tooimmediately de Papelera de reciclaje eliminarán BLOBs huérfanos
1. En SQL Server, en SQL Management Studio, Hola ejecute hello las siguientes consultas de actualización de base de datos de contenido de destino hello: 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. En hello web en el servidor front-end, **Administración Central**, editar hello **configuración General de la aplicación Web** para hello deseado Hola de contenido de la base de datos tootemporarily deshabilitar la Papelera de reciclaje. Esta acción también le hello vacía la Papelera de reciclaje para las colecciones de sitios relacionados. toodo, haga clic en **Administración Central** -> **administración de aplicaciones** -> **aplicaciones Web (administrar aplicaciones de web)**  ->  **SharePoint - 80** -> **configuración de aplicación General**. Conjunto hello **estado de la Papelera de reciclaje** demasiado**OFF**.
   
    ![Configuración general de la aplicación web](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a>Hola toorun mantenedor
* En el servidor front-end web de hello, Hola Shell de administración de SharePoint 2013, ejecute hello mantenedor como sigue:
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > Hola solo `GarbageCollection` operación es compatible con StorSimple en este momento. Tenga en cuenta también que los parámetros de hello emitidos para Microsoft.Data.SqlRemoteBlobs.Maintainer.exe distinguen mayúsculas de minúsculas. 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a>base de datos de contenido de hello toorevert y configuración de la Papelera de reciclaje
1. En SQL Server, en SQL Management Studio, Hola ejecute hello las siguientes consultas de actualización de base de datos de contenido de destino hello:
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. En el servidor front-end web de hello, en **Administración Central**, editar hello **configuración General de la aplicación Web** para hello deseado Hola de contenido de la base de datos toore habilitar Papelera de reciclaje. toodo, haga clic en **Administración Central** -> **administración de aplicaciones** -> **aplicaciones Web (administrar aplicaciones de web)**  ->  **SharePoint - 80** -> **configuración de aplicación General**. Establecer estado de la Papelera de reciclaje de hello demasiado**ON**.

