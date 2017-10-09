<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> Cuando se realizan cambios toohello adaptador de StorSimple para la configuración de RBS de SharePoint, debe ser iniciado sesión con una cuenta de usuario que pertenece el grupo de administradores de dominio de toohello. Además, debe tener acceso a la página de configuración de Hola desde un explorador que se ejecuta en hello mismo host como Administración Central.
> 
> 

#### <a name="tooconfigure-rbs"></a>tooconfigure RBS
1. Abra la página de Administración Central de SharePoint de Hola y examinar demasiado**configuración del sistema**. 
2. Hola **StorSimple de Azure** sección, haga clic en **configurar el adaptador de StorSimple**.
   
    ![Configurar el adaptador de StorSimple Hola](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. En hello **configurar el adaptador de StorSimple** página:
   
   1. Asegúrese de que ese hello **habilitar la edición de la ruta de acceso** casilla está activada.
   2. En el cuadro de texto hello, escriba la ruta de acceso de convención de nomenclatura universal (UNC, Universal Naming Convention) de Hola Hola de almacén de blobs.
      
      > [!NOTE]
      > volumen de almacén de blobs de Hello debe estar hospedado en un volumen de iSCSI configurado en el dispositivo StorSimple Hola.

   3. Haga clic en hello **habilitar** botón debajo de cada una de las bases de datos de contenido Hola que quiere tooconfigure de almacenamiento remoto.
      
      > [!NOTE]
      > almacén de blobs de Hello debe ser compartido y es accesible por todos los servidores web de front-end (WFE) y cuenta de usuario de Hola que está configurado para la granja de servidores de SharePoint de hello debe tener el recurso compartido de toohello de acceso.
      
      ![Habilitar a proveedor de RBS Hola](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      Al habilitar o deshabilitar RBS, también podrá ver el siguiente mensaje de Hola.
      
      ![Configuración del adaptador de StorSimple: habilitar y deshabilitar](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. Haga clic en hello **actualización** configuración del botón tooapply Hola. Al hacer clic en hello **actualización** botón, Hola estado de configuración de RBS se actualizará en todos los servidores WFE y conjunto de servidores completo Hola estará habilitado RBS. aparece el siguiente mensaje de Hola.
      
      ![Mensaje de configuración del adaptador](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > Si va a configurar RBS para una granja de SharePoint con un gran número de bases de datos (más de 200), página web de Administración Central de SharePoint de hello, es posible que el tiempo de espera. Si sucede esto, actualice la página de Hola. Esto no afecta el proceso de configuración de Hola.

4. Comprobar la configuración de hello:
   
   1. Inicie sesión en el sitio Web de Administración Central de SharePoint toohello y examinar toohello **configurar el adaptador de StorSimple** página.
   2. Compruebe toomake de detalles de configuración de hello seguro de que coinciden con configuración de Hola que especificó. 
5. Compruebe que RBS funciona correctamente:
   
   1. Cargar un documento tooSharePoint. 
   2. Examinar ruta de acceso UNC toohello que ha configurado. Asegúrese de que se creó la estructura de directorios RBS de Hola y que contiene el objeto de hello cargado.
6. (Opcional) Puede usar Microsoft RBS hello `Migrate()` cmdlet de PowerShell incluido con SharePoint toomigrate existente BLOB toohello contenido el dispositivo StorSimple. Para obtener más información, consulte [migrar contenido dentro o fuera de RBS en SharePoint 2013] [ 6] o [migrar contenido dentro o fuera de RBS (SharePoint Foundation 2010)] [7].
7. (Opcional) En las instalaciones de prueba, puede comprobar que Hola BLOBs se han extraído de base de datos de contenido de hello como sigue: 
   
   1. Inicie SQL Management Studio
   2. Ejecutar consulta ListBlobsInDB_2010.sql o ListBlobsInDB_2013.sql de hello, como se indica a continuación.
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      Si RBS se ha configurado correctamente, debe aparecer un valor NULL en la columna de SizeOfContentInDB Hola para cualquier objeto que se ha cargado y correctamente externalizado con RBS.
8. (Opcional) Después de configurar RBS y mover toohello contenido de BLOB todos los dispositivos de StorSimple, puede mover el dispositivo de toohello de base de datos de contenido de Hola. Si elige la base de datos de contenido de hello toomove, se recomienda que configurar el almacenamiento de contenido de la base de datos de hello en dispositivo hello como el volumen principal. A continuación, use establece que el dispositivo de StorSimple de toohello toomigrate Hola contenido de la base de datos de prácticas recomendadas de SQL Server. 
   
   > [!NOTE]
   > Dispositivo de toohello de base de datos de contenido de hello móvil solo se admite para la serie de hello StorSimple 8000 (no se admite para la serie de hello 5000 o 7000).
   
   Si almacena BLOBs y base de datos de contenido de hello en volúmenes separados en el dispositivo StorSimple hello, se recomienda configurarlos en hello mismo contenedor de volumen. Esto garantiza que se hará la copia de seguridad de ellos juntos.
   
   > [!WARNING]
   > Si no ha habilitado RBS, no se recomienda mover el dispositivo de StorSimple de toohello de hello contenido de la base de datos. Se trata de una configuración no probada.
   
9. Vaya toohello siguiente paso: [configurar la recolección de elementos no utilizados](#configure-garbage-collection).

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
