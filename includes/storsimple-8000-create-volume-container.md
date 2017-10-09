<!--author=alkohli last changed: 06/22/17-->

#### <a name="toocreate-a-volume-container"></a>toocreate un contenedor de volumen
1. Servicio de administrador de dispositivos de StorSimple tooyour y haga clic en **dispositivos**. En hello tabular listado de dispositivos de hello, seleccione y haga clic en un dispositivo. 

    ![Hoja Contenedor de volúmenes](./media/storsimple-8000-create-volume-container/createvolumecontainer1.png)

2. En el panel del dispositivo hello, haga clic en **+ agregar contenedor de volúmenes**

    ![Hoja Contenedor de volúmenes](./media/storsimple-8000-create-volume-container/createvolumecontainer2.png)

3. Hola **agregar contenedor de volúmenes** hoja:
   
   1. dispositivo de Hola se selecciona automáticamente.
   2. Proporcione un **Nombre** para el contenedor de volúmenes. nombre de Hello debe tener 3 caracteres too32. No se puede cambiar el nombre de un contenedor de volúmenes una vez que se crea.
   3. Seleccione **Habilitar cifrado de almacenamiento de nube** cifrado de tooenable de datos de hello enviados desde el dispositivo de la nube toohello Hola.
   4. Proporcione y confirme una **clave de cifrado de almacenamiento de nube** que es 8 too32 caracteres. Esta clave se usa por tooaccess cifrados los datos del dispositivo Hola.
   5. Seleccione un **cuenta de almacenamiento** tooassociate a este contenedor de volumen. Se puede elegir una cuenta de almacenamiento existente o cuenta de hello predeterminada que se genera en tiempo de presentación de la creación del servicio. También puede usar hello **Agregar nuevo** opción toospecify una cuenta de almacenamiento que no está vinculado toothis suscripción al servicio.
   6. Seleccione **Unlimited** en hello **especificar ancho de banda** lista de desplegable si desea tooconsume Hola ancho de banda disponible. También puede establecer esta opción**personalizado** tooemploy controles de ancho de banda y especifique un valor entre 1 Mbps y 1.000 Mbps.
      Si tiene la información de uso de ancho de banda disponible, es posible que pueda tooallocate ancho de banda según una programación mediante la especificación de **seleccione una plantilla de ancho de banda**. Para un procedimiento paso a paso, vaya demasiado[agregar una plantilla de ancho de banda](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template).

      ![Hoja Contenedor de volúmenes](./media/storsimple-8000-create-volume-container/createvolumecontainer6b.png)
   7. Haga clic en **Crear**.

        ![Hoja Contenedor de volúmenes](./media/storsimple-8000-create-volume-container/createvolumecontainer6.png)
   
       Se le notifica al contenedor de volúmenes de Hola se creó correctamente.

       ![Notificación de creación del contenedor de volúmenes](./media/storsimple-8000-create-volume-container/createvolumecontainer8.png)

   Hola que acaba de crear el contenedor de volumen se muestra en la lista de Hola de contenedores de volumen para el dispositivo.

   ![Hoja Agregar contenedor de volúmenes](./media/storsimple-8000-create-volume-container/createvolumecontainer9.png)


