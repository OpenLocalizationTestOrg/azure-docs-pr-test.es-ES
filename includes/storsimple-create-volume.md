<!--author=SharS last changed: 02/04/2016-->

#### <a name="toocreate-a-volume"></a>toocreate un volumen
1. En el dispositivo de hello **inicio rápido** página, haga clic en **agregar un volumen**. Esto inicia Hola asistente Agregar un volumen.
2. Hola, agregar un asistente de volumen, en **configuración básica**, Hola siguientes:
   
   1. Proporcione un **Nombre** para el volumen.
   2. Especificar hello **capacidad aprovisionada** para su volumen en GB o TB. capacidad del volumen Hola debe estar entre 1 GB y 64 TB para un dispositivo físico.
   3. En la lista desplegable de hello, seleccione hello **tipo de uso** para su volumen. 
   4. Si está utilizando este volumen para los datos de archivo, seleccione hello **usar este volumen de datos acceso menos frecuente archivados** casilla de verificación. Para los demás casos de uso, seleccione simplemente **Volumen por niveles**. (Los volúmenes por niveles se denominaban anteriormente volúmenes principales).
      
        ![Agregar volumen](./media/storsimple-create-volume/ScreenshotUpdate1VolumeFlow.png)
      
      1. Haga clic en el icono de flecha de Hola ![icono de flecha](./media/storsimple-create-volume/HCS_ArrowIcon-include.png) página siguiente de toogo toohello.
3. Hola **configuración adicional** cuadro de diálogo Agregar un nuevo registro de control de acceso (ACR):
   
   1. Proporcione un **Nombre** para el ACR.
   2. En **nombre del iniciador iSCSI**, proporcionar Hola iSCSI nombre completo (IQN) de su host de Windows. Si no tienes Hola IQN, vaya demasiado[Get hello IQN de un host de Windows Server](#get-the-iqn-of-a-windows-server-host).
   3. Se recomienda que habilite una copia de seguridad predeterminada seleccionando hello **habilitar una copia de seguridad predeterminado para este volumen** casilla de verificación. copia de seguridad de Hello predeterminada creará una directiva que se ejecute a las 22:30 cada día (hora del dispositivo) y crea una instantánea en la nube de este volumen.
      
      > [!NOTE]
      > Una vez habilitada la copia de seguridad de hello, no se puede revertir. Necesitará tooedit Hola volumen toomodify esta configuración.
      > 
      > 
      
        ![Agregar volumen](./media/storsimple-create-volume/AddVolume2-include.png)
4. Haga clic en el icono de verificación de Hola ![icono de marca de verificación](./media/storsimple-create-volume/HCS_CheckIcon-include.png). Se creará un volumen con hello especificado valores.

![Vídeo disponible](./media/storsimple-create-volume/Video_icon.png)**Vídeo disponible**

toowatch un vídeo que muestra cómo toocreate un volumen de StorSimple, haga clic en [aquí](https://azure.microsoft.com/documentation/videos/create-a-storsimple-volume/).

