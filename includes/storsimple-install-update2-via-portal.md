<!--author=alkohli last changed: 02/06/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a>tooinstall una actualización de hello portal de Azure

1. En la página de servicio de StorSimple de hello, seleccione el dispositivo. Navegue demasiado**dispositivos** > **mantenimiento**.
2. En la parte inferior de Hola de página de hello, haga clic en **examinar actualizaciones**. Se crea un trabajo tooscan si hay actualizaciones disponibles. Se le notifica cuando se completa correctamente el trabajo de Hola.
3. Hola **las actualizaciones de Software** sección Hola misma página, hay disponibles nuevas actualizaciones de software de Hola. Se recomienda que revise notas de la versión de Hola antes de aplicar una actualización en el dispositivo.
4. En la parte inferior de Hola de página de hello, haga clic en **instalar actualizaciones**y, a continuación, **Aceptar**.
5. Hola **instalar actualizaciones** cuadro de diálogo, asegúrese de que ha seguido las recomendaciones de hello, a continuación, seleccione **entiendo Hola por encima de requisito y estoy listo tooupgrade mi dispositivo** y haga clic en comprobar Hola botón.
   
    ![Mensaje de confirmación](./media/storsimple-install-update2-via-portal/InstallUpdate12_2M.png)
6. Ahora se inicia un conjunto de comprobaciones previas. Estas comprobaciones incluyen:
   
   * **Comprobaciones de estado del controlador** tooverify que ambos Hola controladores de dispositivo están activados y en línea.
   * **Comprobaciones de estado del componente de hardware** tooverify que Hola a todos los componentes de hardware en el dispositivo StorSimple sean correctos.
   * **DATA 0 comprueba** tooverify que DATA 0 está habilitado en el dispositivo. Si la interfaz no está habilitada, tendrá que habilitarla y, después, volver a intentarlo.
   * **DATA 2 y DATA 3 comprobaciones** tooverify que no están habilitadas las interfaces de red DATA 2 y DATA 3. Si se habilitan estas interfaces, debe deshabilitar estas y, a continuación, intente tooupdate el dispositivo. Esta comprobación solo se realiza se va a realizar una actualización de un dispositivo que ejecuta software de disponibilidad general. Los dispositivos que ejecuten las versiones 0.1, 0.2, o 0.3 no necesitarán esta comprobación.
   * **Comprobación de la puerta de enlace** en cualquier dispositivo ejecutando un tooUpdate anterior de versión 1. Esta comprobación se realiza en todos los dispositivos de hello ejecutando 1 de anteriores a la actualización software, pero se produce un error en los dispositivos de Hola que tienen una puerta de enlace configurada para una interfaz de red diferentes a DATA 0.
     
     Hola actualización se aplica si todas las comprobaciones se ha completado correctamente. Se le notificará cuando Hola comprobaciones están en curso.
     
     ![Notificación de comprobación previa](./media/storsimple-install-update2-via-portal/InstallUpdate12_3M.png)
     
     Hola aquí te mostramos un ejemplo en el que no se pudo Hola comprobaciones. Debe comprobar que ambos controladores de dispositivo de hello están en línea y en buen estado. También necesita mantenimiento de hello toocheck Hola de componentes de hardware. En este ejemplo, los componentes del controlador 0 y del controlador 1 necesitan atención. Si no se puede resolver estos problemas por sí mismo, puede que tenga toocontact Microsoft Support.
     
       ![Error en las comprobaciones](./media/storsimple-install-update2-via-portal/HCS_PreUpgradeChecksFailed-include.png)
7. Después de las comprobaciones de Hola se haya completado correctamente, se crea un trabajo de actualización. Se le notificará cuando el trabajo de actualización de Hola se creó correctamente.
   
    ![Creación del trabajo de actualización](./media/storsimple-install-update2-via-portal/InstallUpdate12_44M.png)
   
    a continuación, se aplica la actualización de Hello en el dispositivo.
    
8. progreso de hello toomonitor de trabajo de actualización de hello, haga clic en **ver trabajo**. En hello **trabajos** página, puede ver Hola progreso de la actualización.
9. Hola actualización puede tardar unos toocomplete horas. Seleccione el trabajo de actualización de Hola y haga clic en **detalles** detalles de hello tooview de trabajo de Hola en cualquier momento.
10. Una vez completado el trabajo de hello, navegue toohello **mantenimiento** página y desplácese hacia abajo demasiado**las actualizaciones de Software**.

