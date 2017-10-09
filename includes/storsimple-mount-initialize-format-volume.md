<!--author=SharS last changed: 9/17/15-->

#### <a name="toomount-initialize-and-format-a-volume"></a>toomount, inicializar y formatear un volumen
1. Inicie el iniciador iSCSI de Microsoft de Hola.
2. Hola **propiedades del iniciador iSCSI** ventana hello **detección** , haga clic en **detectar Portal**.
3. Hola **detectar Portal de destino** cuadro de diálogo, proporcione la dirección IP de saludo de la interfaz de red habilitada para iSCSI y, a continuación, haga clic en **Aceptar**. 
4. Hola **propiedades del iniciador iSCSI** ventana hello **destinos** pestaña, busque hello **detectados destinos**. estado del dispositivo Hola debe aparecer como **inactivo**.
5. Seleccionar dispositivo de destino de hello y, a continuación, haga clic en **conectar**. Después de conecta el dispositivo de hello, estado de hello debería cambiar demasiado**conectado**. (Para obtener más información acerca del uso del iniciador iSCSI de Microsoft hello, consulte [iniciador iSCSI de instalar y configurar Microsoft][1]).
6. En el host de Windows, presione la tecla del logotipo de Windows hello + X y, a continuación, haga clic en **ejecutar**. 
7. Hola **ejecutar** cuadro de diálogo, escriba **Diskmgmt.msc**. Haga clic en **Aceptar**, hello y **administración de discos** aparecerá el cuadro de diálogo. panel derecho de Hello mostrará volúmenes hello en el host.
8. Hola **administración de discos** ventana, hello volúmenes montados aparecerán como se muestra en hello siguiente ilustración. Haga clic en el volumen de hello detectado (haga clic en el nombre del disco de hello) y, a continuación, haga clic en **Online**.
   
     ![Inicializar el formateo del volumen](./media/storsimple-mount-initialize-format-volume/HCS_InitializeFormatVolume-include.png) 
9. Haga clic en el volumen de hello (haga clic en el nombre del disco de hello) de nuevo y, a continuación, haga clic en **inicializar**.
10. tooformat un volumen simple, lleve a cabo Hola pasos:
    
    1. Seleccione el volumen de hello, haga clic en él (haga clic en área derecha hello) y haga clic en **nuevo volumen Simple**.
    2. En el Asistente para nuevo volumen Simple de hello, especifique Hola volumen tamaño y letra de unidad y configurar el volumen Hola como un sistema de archivos NTFS.
    3. Especifique un tamaño de unidad de asignación de 64 KB. Este tamaño de la unidad de asignación funciona bien con los algoritmos de desduplicación Hola usados en hello solución StorSimple.
    4. Realice un formateo rápido.

![Vídeo disponible](./media/storsimple-mount-initialize-format-volume/Video_icon.png)**Vídeo disponible**

toowatch un vídeo que muestra cómo toomount, inicializar y formato a un volumen de StorSimple, haga clic en [aquí](https://azure.microsoft.com/documentation/videos/mount-initialize-and-format-a-storsimple-volume/).

<!--Link references-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx
