Hola pasos toounregister un servidor de proceso depende de su estado de conexión con el servidor de configuración de Hola.

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a>Anulación del registro de un servidor de procesos que se encuentra en estado conectado

1. Remoto en el servidor de procesos de hello como administrador.
2. Iniciar hello **el Panel de Control** y abra **programas > desinstalar un programa**
3. Desinstalar un programa por su nombre de hello **servidor de configuración o proceso de recuperación de Microsoft Azure sitio**
4. Cuando haya efectuado el paso 3, puede desinstalar las **dependencias del servidor de configuración o de procesos de Microsoft Azure Site Recovery**

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a>Anulación del registro de un servidor de procesos que se encuentra en estado desconectado

> [!WARNING]
> Hola de uso pasos indicados a continuación debe usarse si no hay ninguna máquina virtual de manera toorevive hello en qué Hola se instaló el servidor de procesos.

1. Inicie sesión en el servidor de configuración de tooyour como administrador.
2. Abra un símbolo del sistema administrativo y busque el directorio de toohello `%ProgramData%\ASR\home\svsystems\bin`.
3. Ahora ejecute el comando Hola.

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. Esto depurarán las detalles Hola Hola del servidor de procesos del sistema de Hola.
