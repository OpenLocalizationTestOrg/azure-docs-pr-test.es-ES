## <a name="create-a-simulated-device-app"></a>Creación de una aplicación de dispositivo simulado
En esta sección:

* Crear una aplicación de consola de Node.js que responde tooa método directo llamado en la nube Hola
* Desencadenará una actualización de firmware simulada.
* Hola uso notificado propiedades tooenable dispositivos gemelas consultas tooidentify dispositivos y cuándo completó por última vez una actualización de firmware

Paso 1: Cree una nueva carpeta vacía denominada **manageddevice**.  Hola **manageddevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema. Acepte todos los valores predeterminados de hello:
   
    ```
    npm init
    ```

Paso 2: en el símbolo del sistema en hello **manageddevice** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure** y **azure-iot-dispositivo-mqtt** dispositivo Paquetes SDK:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

Paso 3: Con un editor de texto, cree un **dmpatterns_fwupdate_device.js** archivo Hola **manageddevice** carpeta.

Paso 4: Agregar siguiente hello 'requiere' instrucciones al principio de Hola de hello **dmpatterns_fwupdate_device.js** archivo:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
Paso 5: Agregar un **connectionString** variable y utilizar toocreate un **cliente** instancia. Reemplace hello `{yourdeviceconnectionstring}` marcador de posición con la cadena de conexión de Hola que haya realizado previamente una nota de en la sección "Crear una identidad de dispositivo" de hello previamente:
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

Paso 6: Agregar siguiente Hola informó de función que se usa tooupdate propiedades:
   
    ```
    var reportFWUpdateThroughTwin = function(twin, firmwareUpdateValue) {
      var patch = {
          iothubDM : {
            firmwareUpdate : firmwareUpdateValue
          }
      };
   
      twin.properties.reported.update(patch, function(err) {
        if (err) throw err;
        console.log('twin state reported: ' + firmwareUpdateValue.status);
      });
    };
    ```

Paso 7: Agregar Hola siguiendo las funciones que simulan descargar y aplicar imagen de firmware de hello:
   
    ```
    var simulateDownloadImage = function(imageUrl, callback) {
      var error = null;
      var image = "[fake image data]";
   
      console.log("Downloading image from " + imageUrl);
   
      callback(error, image);
    }
   
    var simulateApplyImage = function(imageData, callback) {
      var error = null;
   
      if (!imageData) {
        error = {message: 'Apply image failed because of missing image data.'};
      }
   
      callback(error);
    }
    ```

Paso 8: Agregar Hola después de la función que las actualizaciones Hola el estado de actualización de firmware a través de hello informado propiedades demasiado**espera**. Normalmente, los dispositivos correspondientes estén informados de una actualización disponible y definida por el administrador directiva hace Hola dispositivo toostart descargar y aplicar la actualización de Hola. Esta función es Hola donde tooenable lógica que se debe ejecutar la directiva. Para simplificar, ejemplo de Hola espera cuatro segundos antes de la imagen de firmware de continuar toodownload hello:
   
    ```
    var waitToDownload = function(twin, fwPackageUriVal, callback) {
      var now = new Date();
   
      reportFWUpdateThroughTwin(twin, {
        fwPackageUri: fwPackageUriVal,
        status: 'waiting',
        error : null,
        startedWaitingTime : now.toISOString()
      });
      setTimeout(callback, 4000);
    };
    ```

Paso 9: Agregar Hola después de la función que las actualizaciones Hola el estado de actualización de firmware a través de hello informado propiedades demasiado**descargar**. Hello función, a continuación, simula una descarga de firmware y finalmente actualizaciones Hola tooeither de estado de actualización de firmware **downloadFailed** o **downloadComplete**:
   
    ```
    var downloadImage = function(twin, fwPackageUriVal, callback) {
      var now = new Date();   
   
      reportFWUpdateThroughTwin(twin, {
        status: 'downloading',
      });
   
      setTimeout(function() {
        // Simulate download
        simulateDownloadImage(fwPackageUriVal, function(err, image) {
   
          if (err)
          {
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadfailed',
              error: {
                code: error_code,
                message: error_message,
              }
            });
          }
          else {        
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadComplete',
              downloadCompleteTime: now.toISOString(),
            });
   
            setTimeout(function() { callback(image); }, 4000);   
          }
        });
   
      }, 4000);
    }
    ```

Paso 10: Agregar Hola después de la función que las actualizaciones Hola el estado de actualización de firmware a través de hello informado propiedades demasiado**aplicar**. Hello función, a continuación, simula Aplicar imagen de firmware de Hola y finalmente actualizaciones Hola tooeither de estado de actualización de firmware **applyFailed** o **applyComplete**:
    
    ```
    var applyImage = function(twin, imageData, callback) {
      var now = new Date();   
    
      reportFWUpdateThroughTwin(twin, {
        status: 'applying',
        startedApplyingImage : now.toISOString()
      });
    
      setTimeout(function() {
    
        // Simulate apply firmware image
        simulateApplyImage(imageData, function(err) {
          if (err) {
            reportFWUpdateThroughTwin(twin, {
              status: 'applyFailed',
              error: {
                code: err.error_code,
                message: err.error_message,
              }
            });
          } else { 
            reportFWUpdateThroughTwin(twin, {
              status: 'applyComplete',
              lastFirmwareUpdate: now.toISOString()
            });    
    
          }
        });
    
        setTimeout(callback, 4000);
    
      }, 4000);
    }
    ```

Paso 11: Agregar siguiente Hola función ese Hola identificadores **firmwareUpdate** método directo y el firmware de varias fases de hello inicia el proceso de actualización:
    
    ```
    var onFirmwareUpdate = function(request, response) {
    
      // Respond hello cloud app for hello direct method
      response.send(200, 'FirmwareUpdate started', function(err) {
        if (!err) {
          console.error('An error occured when sending a method response:\n' + err.toString());
        } else {
          console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
        }
      });
    
      // Get hello parameter from hello body of hello method request
      var fwPackageUri = request.payload.fwPackageUri;
    
      // Obtain hello device twin
      client.getTwin(function(err, twin) {
        if (err) {
          console.error('Could not get device twin.');
        } else {
          console.log('Device twin acquired.');
    
          // Start hello multi-stage firmware update
          waitToDownload(twin, fwPackageUri, function() {
            downloadImage(twin, fwPackageUri, function(imageData) {
              applyImage(twin, imageData, function() {});    
            });  
          });
    
        }
      });
    }
    ```

Paso 12: Por último, agregue Hola después el código que se conecta el centro de IoT tooyour:
    
    ```
    client.open(function(err) {
      if (err) {
        console.error('Could not connect tooIotHub client');
      }  else {
        console.log('Client connected tooIoT Hub.  Waiting for firmwareUpdate direct method.');
      }
    
      client.onDeviceMethod('firmwareUpdate', onFirmwareUpdate);
    });
    ```

> [!NOTE]
> tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento. En el código de producción, debe implementar directivas de reintento (por ejemplo, un retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios](https://msdn.microsoft.com/library/hh675232.aspx).
> 
> 