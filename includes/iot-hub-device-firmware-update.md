## <a name="create-a-simulated-device-app"></a><span data-ttu-id="988b5-101">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="988b5-101">Create a simulated device app</span></span>
<span data-ttu-id="988b5-102">En esta sección:</span><span class="sxs-lookup"><span data-stu-id="988b5-102">In this section, you:</span></span>

* <span data-ttu-id="988b5-103">Crear una aplicación de consola de Node.js que responde tooa método directo llamado en la nube Hola</span><span class="sxs-lookup"><span data-stu-id="988b5-103">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="988b5-104">Desencadenará una actualización de firmware simulada.</span><span class="sxs-lookup"><span data-stu-id="988b5-104">Trigger a simulated firmware update</span></span>
* <span data-ttu-id="988b5-105">Hola uso notificado propiedades tooenable dispositivos gemelas consultas tooidentify dispositivos y cuándo completó por última vez una actualización de firmware</span><span class="sxs-lookup"><span data-stu-id="988b5-105">Use hello reported properties tooenable device twin queries tooidentify devices and when they last completed a firmware update</span></span>

<span data-ttu-id="988b5-106">Paso 1: Cree una nueva carpeta vacía denominada **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="988b5-106">Step 1: Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="988b5-107">Hola **manageddevice** carpeta, cree un archivo de package.json mediante Hola siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="988b5-107">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="988b5-108">Acepte todos los valores predeterminados de hello:</span><span class="sxs-lookup"><span data-stu-id="988b5-108">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```

<span data-ttu-id="988b5-109">Paso 2: en el símbolo del sistema en hello **manageddevice** carpeta, ejecute hello después comando tooinstall hello **dispositivos de iot de azure** y **azure-iot-dispositivo-mqtt** dispositivo Paquetes SDK:</span><span class="sxs-lookup"><span data-stu-id="988b5-109">Step 2: At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

<span data-ttu-id="988b5-110">Paso 3: Con un editor de texto, cree un **dmpatterns_fwupdate_device.js** archivo Hola **manageddevice** carpeta.</span><span class="sxs-lookup"><span data-stu-id="988b5-110">Step 3: Using a text editor, create a **dmpatterns_fwupdate_device.js** file in hello **manageddevice** folder.</span></span>

<span data-ttu-id="988b5-111">Paso 4: Agregar siguiente hello 'requiere' instrucciones al principio de Hola de hello **dmpatterns_fwupdate_device.js** archivo:</span><span class="sxs-lookup"><span data-stu-id="988b5-111">Step 4: Add hello following 'require' statements at hello start of hello **dmpatterns_fwupdate_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
<span data-ttu-id="988b5-112">Paso 5: Agregar un **connectionString** variable y utilizar toocreate un **cliente** instancia.</span><span class="sxs-lookup"><span data-stu-id="988b5-112">Step 5: Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="988b5-113">Reemplace hello `{yourdeviceconnectionstring}` marcador de posición con la cadena de conexión de Hola que haya realizado previamente una nota de en la sección "Crear una identidad de dispositivo" de hello previamente:</span><span class="sxs-lookup"><span data-stu-id="988b5-113">Replace hello `{yourdeviceconnectionstring}` placeholder with hello connection string you previously made a note of in hello "Create a device identity" section previously:</span></span>
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

<span data-ttu-id="988b5-114">Paso 6: Agregar siguiente Hola informó de función que se usa tooupdate propiedades:</span><span class="sxs-lookup"><span data-stu-id="988b5-114">Step 6: Add hello following function that is used tooupdate reported properties:</span></span>
   
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

<span data-ttu-id="988b5-115">Paso 7: Agregar Hola siguiendo las funciones que simulan descargar y aplicar imagen de firmware de hello:</span><span class="sxs-lookup"><span data-stu-id="988b5-115">Step 7: Add hello following functions that simulate downloading and applying hello firmware image:</span></span>
   
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

<span data-ttu-id="988b5-116">Paso 8: Agregar Hola después de la función que las actualizaciones Hola el estado de actualización de firmware a través de hello informado propiedades demasiado**espera**.</span><span class="sxs-lookup"><span data-stu-id="988b5-116">Step 8: Add hello following function that updates hello firmware update status through hello reported properties too**waiting**.</span></span> <span data-ttu-id="988b5-117">Normalmente, los dispositivos correspondientes estén informados de una actualización disponible y definida por el administrador directiva hace Hola dispositivo toostart descargar y aplicar la actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="988b5-117">Typically, devices are informed of an available update and an administrator defined policy causes hello device toostart downloading and applying hello update.</span></span> <span data-ttu-id="988b5-118">Esta función es Hola donde tooenable lógica que se debe ejecutar la directiva.</span><span class="sxs-lookup"><span data-stu-id="988b5-118">This function is where hello logic tooenable that policy should run.</span></span> <span data-ttu-id="988b5-119">Para simplificar, ejemplo de Hola espera cuatro segundos antes de la imagen de firmware de continuar toodownload hello:</span><span class="sxs-lookup"><span data-stu-id="988b5-119">For simplicity, hello sample waits for four seconds before proceeding toodownload hello firmware image:</span></span>
   
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

<span data-ttu-id="988b5-120">Paso 9: Agregar Hola después de la función que las actualizaciones Hola el estado de actualización de firmware a través de hello informado propiedades demasiado**descargar**.</span><span class="sxs-lookup"><span data-stu-id="988b5-120">Step 9: Add hello following function that updates hello firmware update status through hello reported properties too**downloading**.</span></span> <span data-ttu-id="988b5-121">Hello función, a continuación, simula una descarga de firmware y finalmente actualizaciones Hola tooeither de estado de actualización de firmware **downloadFailed** o **downloadComplete**:</span><span class="sxs-lookup"><span data-stu-id="988b5-121">hello function then simulates a firmware download and finally updates hello firmware update status tooeither **downloadFailed** or **downloadComplete**:</span></span>
   
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

<span data-ttu-id="988b5-122">Paso 10: Agregar Hola después de la función que las actualizaciones Hola el estado de actualización de firmware a través de hello informado propiedades demasiado**aplicar**.</span><span class="sxs-lookup"><span data-stu-id="988b5-122">Step 10: Add hello following function that updates hello firmware update status through hello reported properties too**applying**.</span></span> <span data-ttu-id="988b5-123">Hello función, a continuación, simula Aplicar imagen de firmware de Hola y finalmente actualizaciones Hola tooeither de estado de actualización de firmware **applyFailed** o **applyComplete**:</span><span class="sxs-lookup"><span data-stu-id="988b5-123">hello function then simulates applying hello firmware image and finally updates hello firmware update status tooeither **applyFailed** or **applyComplete**:</span></span>
    
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

<span data-ttu-id="988b5-124">Paso 11: Agregar siguiente Hola función ese Hola identificadores **firmwareUpdate** método directo y el firmware de varias fases de hello inicia el proceso de actualización:</span><span class="sxs-lookup"><span data-stu-id="988b5-124">Step 11: Add hello following function that handles hello **firmwareUpdate** direct method and initiates hello multi-stage firmware update process:</span></span>
    
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

<span data-ttu-id="988b5-125">Paso 12: Por último, agregue Hola después el código que se conecta el centro de IoT tooyour:</span><span class="sxs-lookup"><span data-stu-id="988b5-125">Step 12: Finally, add hello following code that connects tooyour IoT hub:</span></span>
    
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
> <span data-ttu-id="988b5-126">tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento.</span><span class="sxs-lookup"><span data-stu-id="988b5-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="988b5-127">En el código de producción, debe implementar directivas de reintento (por ejemplo, un retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios](https://msdn.microsoft.com/library/hh675232.aspx).</span><span class="sxs-lookup"><span data-stu-id="988b5-127">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling](https://msdn.microsoft.com/library/hh675232.aspx).</span></span>
> 
> 