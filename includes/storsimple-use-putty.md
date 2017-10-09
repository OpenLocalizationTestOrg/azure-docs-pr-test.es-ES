<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a>tooconnect a través de la consola serie Hola
1. Conecte el cable serie toohello dispositivo (directamente o a través de un adaptador USB-serie).
2. Abra hello **el Panel de Control**y, a continuación, abra hello **el Administrador de dispositivos**.
3. Identifique el puerto de hello COM como se muestra en hello siguiente ilustración.
   
     ![Conexión a través de la consola serie](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. Inicie PuTTY. 
5. En el panel derecho de hello, cambie hello **tipo de conexión** demasiado**serie**.
6. En el panel derecho de hello, escriba el puerto COM correspondiente de Hola. Asegúrese de que los parámetros de configuración de serie de hello están establecidos como se indica a continuación:
   
   * Velocidad: 115.200
   * Bits de datos: 8
   * Bits de parada: 1
   * Paridad: ninguno
   * Control de flujo: ninguno
     
     Esta configuración se muestra en hello siguiente ilustración.
     
     ![Configuración de PuTTY](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > Si la configuración de control de flujo de hello predeterminada no funciona, intente establecer control de flujo de hello tooXON/XOFF.
     > 
     > 
7. Haga clic en **abiertos** toostart una sesión serie.

