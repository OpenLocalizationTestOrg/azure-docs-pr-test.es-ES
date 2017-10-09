<!--author=alkohli last changed: 07/07/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a>tooinstall una actualización de hello portal de Azure

1. En la página de servicio de StorSimple de hello, seleccione el dispositivo.

    ![Selección del dispositivo](./media/storsimple-8000-install-update4-via-portal/update1.png)

2. Navegue demasiado**configuración de dispositivo** > **actualizaciones del dispositivo**.

    ![Haga clic en Actualizaciones del dispositivo.](./media/storsimple-8000-install-update4-via-portal/update2.png)

2. Aparecerá una notificación si hay nuevas actualizaciones disponibles. O bien, en hello **actualizaciones del dispositivo** hoja, haga clic en **examinar actualizaciones**. Se crea un trabajo tooscan si hay actualizaciones disponibles. Se le notifica cuando se completa correctamente el trabajo de Hola.

    ![Haga clic en Actualizaciones del dispositivo.](./media/storsimple-8000-install-update4-via-portal/update3.png)

3. Se recomienda que revise notas de la versión de Hola antes de aplicar una actualización en el dispositivo. tooapply actualizaciones, haga clic en **instalar actualizaciones**. Hola **confirmar las actualizaciones normales** hoja, los requisitos previos de revisión hello toocomplete antes de aplicar las actualizaciones. Seleccione hello tooindicate de casilla de verificación que sean tooupdate listo Hola dispositivo y, a continuación, haga clic en **instalar**.

    ![Haga clic en Actualizaciones del dispositivo.](./media/storsimple-8000-install-update4-via-portal/update4.png)

6. Ahora se inicia un conjunto de comprobaciones previas. Estas comprobaciones incluyen:
   
   * **Comprobaciones de estado del controlador** tooverify que ambos Hola controladores de dispositivo están activados y en línea.
   * **Comprobaciones de estado del componente de hardware** tooverify que Hola a todos los componentes de hardware en el dispositivo StorSimple sean correctos.
   * **DATA 0 comprueba** tooverify que DATA 0 está habilitado en el dispositivo. Si la interfaz no está habilitada, tendrá que habilitarla y, después, volver a intentarlo.

    actualización de Hola se descarga e instala sólo si todas las comprobaciones de Hola se completan correctamente. Se le notificará cuando Hola comprobaciones están en curso. Si se producen errores hello prechecks, a continuación, le proporcionará motivos hello para el error. Solucionar los problemas y, a continuación, vuelva a intentar la operación de Hola. Si no se puede resolver estos problemas por sí mismo, puede que tenga toocontact Microsoft Support.

7. Después de hello prechecks se haya completado correctamente, se crea un trabajo de actualización. Se le notificará cuando el trabajo de actualización de Hola se creó correctamente.
   
    ![Creación del trabajo de actualización](./media/storsimple-8000-install-update4-via-portal/update6.png)
   
    a continuación, se aplica la actualización de Hello en el dispositivo.

9. Hola actualización puede tardar unos toocomplete horas. Seleccione el trabajo de actualización de Hola y haga clic en **detalles** detalles de hello tooview de trabajo de Hola en cualquier momento.

    ![Creación del trabajo de actualización](./media/storsimple-8000-install-update4-via-portal/update8.png)

     También puede supervisar el progreso de Hola de trabajo de actualización de Hola de **configuración del dispositivo > trabajos**. En hello **trabajos** hoja, puede ver Hola progreso de la actualización.

     ![Creación del trabajo de actualización](./media/storsimple-8000-install-update4-via-portal/update7.png)

10. Una vez completado el trabajo de hello, navegue toohello **configuración del dispositivo > actualizaciones del dispositivo**. Esto se actualizará la versión de software de Hola.

    ![Creación del trabajo de actualización](./media/storsimple-8000-install-update4-via-portal/update9.png)

