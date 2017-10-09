## <a name="configure-hello-nodejs-simulated-device"></a>Configurar dispositivo simulado de hello Node.js
1. En el panel de supervisión remota de hello, haga clic en **+ agregar un dispositivo** y, a continuación, agregue un *dispositivo personalizado*. Tome nota del centro de IoT Hola hostname, Id. de dispositivo y una clave de dispositivos. Se necesita más adelante en este tutorial cuando se prepara una aplicación de cliente de dispositivo de hello remote_monitoring.js.
2. Asegúrese de que tiene instalada la versión 0.12.x o posterior de Node.js en el equipo de desarrollo. Ejecutar `node --version` en un símbolo del sistema o en una versión de hello toocheck de shell. Para obtener información sobre el uso de un tooinstall de administrador de paquetes Node.js en Linux, consulte [instalar Node.js a través del Administrador de paquetes][node-linux].
3. Cuando haya instalado Node.js, clonar la versión más reciente de Hola de hello [azure iot sdk nodos] [ lnk-github-repo] equipo de desarrollo de tooyour de repositorio. Utilice siempre hello **maestro** rama para la versión más reciente de Hola de bibliotecas de Hola y ejemplos.
4. Desde la copia local de hello [azure iot sdk nodos] [ lnk-github-repo] repositorio, Hola copia siguiendo dos archivos de hello nodo/dispositivo/samples tooan vacía la carpeta en el equipo de desarrollo:
   
   * packages.json
   * remote_monitoring.js
5. Abra el archivo de remote_monitoring.js hello y busque Hola después de la definición de variable:
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. Reemplace **[IoT Hub device connection string]** con la cadena de conexión al dispositivo. Usar valores de hello de clave de dispositivo que se anotó en el paso 1, Id. de dispositivo y nombre de host del centro de IoT. Una cadena de conexión de dispositivo tiene Hola siguiendo el formato:
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    Si es el nombre de host del centro de IoT **contoso** y el identificador de dispositivo es **mydevice**, la cadena de conexión es similar a Hola siguiente fragmento de código:
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Guarde el archivo hello. Ejecute hello siga los comandos en un shell o el símbolo del sistema en carpeta de Hola que contiene estos paquetes de archivos tooinstall Hola necesarios y, a continuación, ejecute la aplicación de ejemplo de Hola:
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a>Observación de la telemetría dinámica en acción
panel de Hello muestra telemetría de temperatura y humedad Hola desde dispositivos simulada de hello existente:

![panel de saludo predeterminado][image1]

Si selecciona el dispositivo simulado Node.js de hello, que se ejecutaron en la sección anterior de hello, verá temperatura y humedad, telemetría de temperatura externo:

![Agregar temperatura externo toohello panel][image2]

solución de supervisión remoto Hello automáticamente detecta el tipo de telemetría de temperatura externos adicionales de Hola y lo agrega toohello gráfico en el panel de Hola.

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png