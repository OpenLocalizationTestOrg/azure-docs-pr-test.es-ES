> [!div class="op_single_selector"]
> * [C en Windows](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [C en Linux](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [Node.js](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a>Información general de escenario
En este escenario, se crea un dispositivo que envía Hola después de supervisión remota de telemetría toohello [preconfigurado solución][lnk-what-are-preconfig-solutions]:

* Temperatura exterior
* Temperatura interior
* Humedad

Para simplificar, valores de ejemplo genera el código de hello en dispositivo hello, pero recomendamos ejemplo Hola tooextend: conectar dispositivo tooyour de sensores real y enviar telemetría real.

dispositivo de Hello también es toomethods toorespond puede invocar desde el panel de la solución de Hola y desea valores de propiedad establecidos en el panel de la solución de Hola.

toocomplete este tutorial, necesita una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para más información, consulte la [evaluación gratuita de Azure][lnk-free-trial].

## <a name="before-you-start"></a>Antes de comenzar
Antes de escribir ningún código para el dispositivo, debe aprovisionar la solución preconfigurada de supervisión remota y aprovisionar un nuevo dispositivo personalizado en esa solución.

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>Aprovisionar su solución preconfigurada de supervisión remota
dispositivo de Hola que creará en este tutorial envía la instancia de datos de tooan de hello [supervisión remota] [ lnk-remote-monitoring] preconfigurado solución. Si aún no aprovisionada Hola supervisión solución preconfigurada en su cuenta de Azure remota, use Hola pasos:

1. En hello <https://www.azureiotsuite.com/> página, haga clic en  **+**  toocreate una solución.
2. Haga clic en **seleccione** en hello **supervisión remota** panel toocreate la solución.
3. En hello **crear remoto solución de supervisión** página, escriba un **nombre de la solución** de su elección, seleccione hello **región** desee toodeploy a y seleccione hello Azure suscripción toowant toouse. Haga clic en **Crear solución**.
4. Espere hasta que se complete el proceso de aprovisionamiento de Hola.

> [!WARNING]
> las soluciones de Hello preconfigurado usan los servicios de Azure facturables. Asegúrese de tooremove Hola solución preconfigurada de la suscripción cuando haya terminado con él tooavoid los cargos innecesarios. Puede quitar completamente una solución preconfigurada de su suscripción visitando hello <https://www.azureiotsuite.com/> página.
> 
> 

Cuando finalice el proceso para hello remoto de solución de supervisión de aprovisionamiento de hello, haga clic en **iniciar** tooopen panel de solución de hello en el explorador.

![Panel de soluciones][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a>Aprovisionar el dispositivo en hello remoto de solución de supervisión
> [!NOTE]
> Si ya ha aprovisionado un dispositivo en la solución, puede omitir este paso. Necesita credenciales de dispositivo de hello tooknow cuando se crea la aplicación de cliente de Hola.
> 
> 

Para una solución de toohello preconfigurado tooconnect de dispositivo, debe identificarse tooIoT concentrador con credenciales válidas. Puede recuperar las credenciales del dispositivo Hola de panel de la solución de Hola. Incluye las credenciales del dispositivo hello en la aplicación de cliente más adelante en este tutorial.

tooadd una solución de supervisión remota de tooyour de dispositivo, Hola completa siguiendo los pasos en el panel de la solución de hello:

1. En hello esquina izquierda inferior del panel de hello, haga clic en **agregar un dispositivo**.
   
   ![Agregar un dispositivo][1]
2. Hola **dispositivo personalizado** del panel, haga clic en **agregar nueva**.
   
   ![Agregar un dispositivo personalizado][2]
3. Elija **Permitirme definir mi propio id. de dispositivo**. Escriba un Id. de dispositivo como **mydevice**, haga clic en **Check ID** tooverify ese nombre no está en uso y, a continuación, haga clic en **crear** dispositivo de tooprovision Hola.
   
   ![Agregar id. de dispositivo][3]
4. Hacer que un dispositivo de hello tenga en cuenta las credenciales (Id. de dispositivo, el nombre de host de IoT Hub y clave de dispositivo). La aplicación cliente necesita estos toohello de tooconnect valores remoto de solución de supervisión. A continuación, haga clic en **Hecho**.
   
    ![Ver las credenciales del dispositivo][4]
5. Seleccione el dispositivo en la lista de dispositivos de hello en el panel de la solución de Hola. A continuación, en hello **detalles del dispositivo** del panel, haga clic en **Habilitar dispositivo**. Hola estado del dispositivo es ahora **ejecutando**. solución de supervisión remoto Hello ahora puede reciba datos de telemetría del dispositivo e invocar métodos de dispositivo de Hola.

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/