<!--author=SharS last changed: 9/17/15-->

### <a name="upgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-storsomple-adapter-for-sharepoint"></a>Actualizar SharePoint 2010 tooSharePoint 2013 y, a continuación, instalar hello StorSomple adaptador para SharePoint
> [!IMPORTANT]
> Los archivos migrados previamente tooexternal almacenamiento mediante RBS no estarán disponible hasta que termine la actualización de Hola y Hola característica RBS se vuelva a habilitar. toolimit usuario afectan, lleve a cabo cualquier actualización o reinstalación de una ventana de mantenimiento planeada.
> 
> 

#### <a name="tooupgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-adapter"></a>tooSharePoint tooupgrade 2010 de SharePoint 2013 y, a continuación, instalar Hola adaptador
1. En la granja de servidores de SharePoint 2010 hello, Nota Hola BLOB almacenar la ruta de acceso para hello externalizado BLOBs y bases de datos de contenido de hello para el que RBS está habilitado. 
2. Instalar y configurar una nueva granja de SharePoint 2013 Hola. 
3. Mover las bases de datos, aplicaciones y colecciones de sitios de granja de SharePoint 2013 nuevo de toohello de granja de servidores de hello SharePoint 2010. Para obtener instrucciones, vaya demasiado[información general del proceso de actualización de hello tooSharePoint 2013](https://technet.microsoft.com/library/cc262483.aspx).
4. Instalar Hola el adaptador de StorSimple para SharePoint en la nueva granja de Hola. Vaya demasiado[Hola de instalar el adaptador de StorSimple para SharePoint](#install-the-storsimple-adapter-for-sharepoint) para conocer los procedimientos.
5. Con la información de Hola que anotó en el paso 1, habilitar RBS para hello mismo conjunto de bases de datos de contenido y proporcione Hola mismo BLOB almacenar la ruta de acceso que se usó en la instalación de hello SharePoint 2010. Vaya demasiado[configurar RBS](#configure-rbs) para conocer los procedimientos. Después de completar este paso, los archivos previamente externalizados deben ser accesibles desde la nueva granja de Hola. 

### <a name="upgrade-hello-storsimple-adapter-for-sharepoint"></a>Hola de actualización del adaptador de StorSimple para SharePoint
> [!IMPORTANT]
> Debe programar esta actualización toooccur durante una ventana de mantenimiento planificado para hello siguientes motivos:
> 
> * Previamente externalizado contenido no estará disponible hasta que se vuelve a instalar el adaptador de Hola.
> * Contenido se ha cargado toohello sitio después de desinstalar versión anterior de Hola de hello el adaptador de StorSimple para SharePoint, pero antes de instalar la nueva versión de hello, se almacenará en la base de datos de contenido de Hola. Necesitará toomove ese dispositivo de StorSimple toohello contenido después de instalar el nuevo adaptador de Hola. Puede usar Microsoft hello` RBS Migrate()` cmdlet de PowerShell que se incluye con el contenido de SharePoint toomigrate Hola. Para obtener más información, vea [migrar contenido dentro o fuera de RBS](https://technet.microsoft.com/library/ff628255.aspx). 
> 
> 

#### <a name="tooupgrade-hello-storsimple-adapter-for-sharepoint"></a>Hola tooupgrade adaptador de StorSimple para SharePoint
1. Desinstalar versión anterior de hello del adaptador de StorSimple para SharePoint.
   
   > [!NOTE]
   > Esto deshabilitará automáticamente RBS en bases de datos de contenido de Hola. Sin embargo, los BLOBs existentes permanecerán en el dispositivo StorSimple Hola. Dado que RBS está deshabilitado y Hola BLOBs no han sido migrados toohello atrás bases de datos de contenido, se producirá un error en las solicitudes de los BLOBs. 
   > 
   > 
2. Instalación Hola nuevo adaptador de StorSimple para SharePoint. nuevo adaptador de Hello reconocerá automáticamente Hola contenido bases de datos que se hayan habilitado o deshabilitados para RBS y usará la configuración anterior de Hola.

