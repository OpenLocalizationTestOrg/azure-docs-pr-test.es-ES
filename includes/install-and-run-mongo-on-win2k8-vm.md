Siga estos pasos tooinstall y ejecute MongoDB en una máquina virtual que ejecuta Windows Server.

> [!IMPORTANT]
> Las características de seguridad de MongoDB, como la vinculación de direcciones IP y la autenticación, no se encuentran habilitadas de forma predeterminada. Características de seguridad deben habilitarse antes de implementar el entorno de producción de MongoDB tooa.  Para más información, consulte [Seguridad y autenticación](http://www.mongodb.org/display/DOCS/Security+and+Authentication).
>
>

1. Una vez haya conectado la máquina virtual de toohello mediante Escritorio remoto, abra Internet Explorer de hello **iniciar** menú en la máquina virtual de Hola.
2. Seleccione hello **herramientas** botón en la esquina superior derecha de Hola.  En **opciones de Internet**, seleccione hello **seguridad** ficha y, a continuación, seleccione hello **sitios de confianza** icono y por último, haga clic en hello **sitios** botón. Agregar *https://\*. mongodb.org* toohello lista de sitios de confianza.
3. Vaya demasiado[descargas - MongoDB](https://www.mongodb.com/download-center#community).
4. Buscar hello **versión estable actual** de **Community Server**, seleccione Hola más reciente **64-bit** versión en la columna de Windows hello. Descargue y ejecute el programa de instalación de hello MSI.
5. MongoDB se suele instalar en C:\Archivos de programa\MongoDB. Busque las Variables de entorno en el escritorio de Hola y agregue la variable de ruta de acceso de hello MongoDB binarios path toohello. Por ejemplo, podría encontrar los archivos binarios de hello en C:\Program Files\MongoDB\Server\3.4\bin en su equipo.
6. Cree los directorios de datos y de registro de MongoDB en disco de datos de hello (como unidad **F:**) que creó en hello pasos anteriores. De **iniciar**, seleccione **símbolo** tooopen una ventana del símbolo del sistema.  Escriba:

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. toorun Hola base de datos, ejecute:

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    Todos los mensajes de registro son dirigido toohello *F:\MongoLogs\mongolog.log* archivo mongod.exe server se inicia y preasigna archivos de diario. Puede tardar varios minutos para MongoDB toopreallocate archivos de diario de Hola y empiece a escuchar las conexiones. símbolo de Hello permanece centrado en esta tarea mientras se ejecuta la instancia de MongoDB.
8. Hola toostart MongoDB shell administrativo, abra otra ventana de comandos de **iniciar** y Hola de tipo siguientes comandos:

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    crea base de datos de Hello mediante insert Hola.
9. Como alternativa, puede instalar mongod.exe como servicio:

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    Se instala un servicio denominado MongoDB con la descripción "Mongo DB". Hola `--logpath` opción debe ser toospecify usa un archivo de registro, desde Hola ejecutando el servicio no tiene una salida de toodisplay de la ventana de comandos.  Hola `--logappend` opción especifica que un reinicio del servicio de hello hace el archivo de registro existente de salida tooappend toohello.  Hola `--dbpath` opción especifica la ubicación de Hola Hola del directorio de datos. Para ver más opciones de línea de comandos relacionadas con los servicios, consulte [Opciones de línea de comandos relacionadas con los servicios][MongoWindowsSvcOptions].

    servicio de hello toostart, ejecute este comando:

        C:\> net start MongoDB
10. Ahora que MongoDB está instalado y en ejecución, deberá tooopen un puerto en Firewall de Windows por lo que se puede conectarse de forma remota tooMongoDB.  De hello **iniciar** menú, seleccione **herramientas administrativas** y, a continuación, **Firewall de Windows con seguridad avanzada**.
11. a) en el panel izquierdo de hello, seleccione **reglas de entrada**.  Hola **acciones** panel en hello derecha, seleccione **nueva regla...** .

    ![Firewall de Windows][Image1]

    b) en hello **entrada Asistente para nueva regla**, seleccione **puerto** y, a continuación, haga clic en **siguiente**.

    ![Firewall de Windows][Image2]

    c) Seleccione **TCP** y luego **Puertos locales específicos**.  Especifique un puerto de "27017" (MongoDB escucha en el puerto de forma predeterminada Hola) y haga clic en **siguiente**.

    ![Firewall de Windows][Image3]

    d) seleccione **Permitir conexión hello** y haga clic en **siguiente**.

    ![Firewall de Windows][Image4]

    e) Haga clic en **Siguiente** de nuevo.

    ![Firewall de Windows][Image5]

    f) Especifique un nombre para la regla de hello, como "MongoPort" y haga clic en **finalizar**.

    ![Firewall de Windows][Image6]

12. Si no ha configurado un punto de conexión para MongoDB cuando se creó la máquina virtual de hello, hágalo ahora. Necesita regla de firewall de Hola y Hola extremo toobe tooconnect pueda tooMongoDB remotamente.

  Hola portal de Azure, haga clic en **máquinas virtuales (clásicas)**, haga clic en nombre de saludo de la nueva máquina virtual y, a continuación, haga clic en **extremos**.

    ![Puntos de conexión][Image7]

13. Haga clic en **Agregar**.

14. Agregar un punto de conexión con el nombre "Mongo", protocolo **TCP**y ambos **público** y **privada** puertos conjunto demasiado "27017". Apertura de este puerto permite toobe de MongoDB acceso remoto.

    ![Puntos de conexión][Image9]

> [!NOTE]
> Hola 27017 Hola puerto predeterminado es utilizado por MongoDB. Puede cambiar este puerto predeterminado mediante la especificación de hello `--port` parámetro al iniciar hello mongod.exe servidor. Asegúrese de toogive seguro Hola el mismo número de puerto en firewall de Hola y Hola extremo "Mongo" Hola anteriores instrucciones.
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
