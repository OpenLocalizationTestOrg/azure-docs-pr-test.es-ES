## <a name="specify-hello-behavior-of-hello-iot-device"></a><span data-ttu-id="7e4f5-101">Especificar el comportamiento de Hola de dispositivos de IoT Hola</span><span class="sxs-lookup"><span data-stu-id="7e4f5-101">Specify hello behavior of hello IoT device</span></span>

<span data-ttu-id="7e4f5-102">Hola biblioteca de cliente de centro de IoT serializador utiliza un formato de Hola de toospecify de modelo de intercambios de dispositivo de hello mensajes hello con centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-102">hello IoT Hub serializer client library uses a model toospecify hello format of hello messages hello device exchanges with IoT Hub.</span></span>

1. <span data-ttu-id="7e4f5-103">Agregar Hola siguiendo las declaraciones de variable después de hello `#include` instrucciones.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-103">Add hello following variable declarations after hello `#include` statements.</span></span> <span data-ttu-id="7e4f5-104">Reemplace los valores de marcador de posición de hello [Id. de dispositivo] y [clave de dispositivo] con los valores indicados para el dispositivo en el panel de solución de supervisión remota de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-104">Replace hello placeholder values [Device Id] and [Device Key] with values you noted for your device in hello remote monitoring solution dashboard.</span></span> <span data-ttu-id="7e4f5-105">Usar hello Hostname del centro de IoT de hello solución panel tooreplace [el centro de IOT Name].</span><span class="sxs-lookup"><span data-stu-id="7e4f5-105">Use hello IoT Hub Hostname from hello solution dashboard tooreplace [IoTHub Name].</span></span> <span data-ttu-id="7e4f5-106">Por ejemplo, si el nombre de host de IoT Hub es **contoso.azure-devices.net**, sustituya [IoTHub Name] por **contoso**:</span><span class="sxs-lookup"><span data-stu-id="7e4f5-106">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>
   
    ```c
    static const char* deviceId = "[Device Id]";
    static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
    ```

1. <span data-ttu-id="7e4f5-107">Agregar Hola siguiendo el modelo de hello toodefine de código que permite hello toocommunicate de dispositivo con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-107">Add hello following code toodefine hello model that enables hello device toocommunicate with IoT Hub.</span></span> <span data-ttu-id="7e4f5-108">Este modelo especifica ese dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="7e4f5-108">This model specifies that hello device:</span></span>

   - <span data-ttu-id="7e4f5-109">Puede enviar datos de temperatura, temperatura externa, humedad y un id. de dispositivo como telemetría.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-109">Can send temperature, external temperature, humidity, and a device id as telemetry.</span></span>
   - <span data-ttu-id="7e4f5-110">Puede enviar metadatos sobre Hola dispositivo tooIoT concentrador.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-110">Can send metadata about hello device tooIoT Hub.</span></span> <span data-ttu-id="7e4f5-111">dispositivo de Hello envía metadatos básicos una **DeviceInfo** objeto en el inicio.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-111">hello device sends basic metadata in a **DeviceInfo** object at startup.</span></span>
   - <span data-ttu-id="7e4f5-112">Puede enviar propiedades notificadas, toohello gemelas de dispositivo en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-112">Can send reported properties, toohello device twin in IoT Hub.</span></span> <span data-ttu-id="7e4f5-113">Estas propiedades notificadas se agrupan en propiedades de configuración, dispositivo y sistema.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-113">These reported properties are grouped into configuration, device, and system properties.</span></span>
   - <span data-ttu-id="7e4f5-114">Puede recibir y actuar en propiedades que desee establecidas en gemelas de dispositivo de hello en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-114">Can receive and act on desired properties set in hello device twin in IoT Hub.</span></span>
   - <span data-ttu-id="7e4f5-115">Puede responder toohello **reiniciar** y **InitiateFirmwareUpdate** dirigir los métodos llamados mediante el portal de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-115">Can respond toohello **Reboot** and **InitiateFirmwareUpdate** direct methods invoked through hello solution portal.</span></span> <span data-ttu-id="7e4f5-116">dispositivo de Hello envía información sobre métodos directos de Hola admite el uso de propiedades del informes.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-116">hello device sends information about hello direct methods it supports using reported properties.</span></span>
   
    ```c
    // Define hello Model
    BEGIN_NAMESPACE(Contoso);

    /* Reported properties */
    DECLARE_STRUCT(SystemProperties,
      ascii_char_ptr, Manufacturer,
      ascii_char_ptr, FirmwareVersion,
      ascii_char_ptr, InstalledRAM,
      ascii_char_ptr, ModelNumber,
      ascii_char_ptr, Platform,
      ascii_char_ptr, Processor,
      ascii_char_ptr, SerialNumber
    );

    DECLARE_STRUCT(LocationProperties,
      double, Latitude,
      double, Longitude
    );

    DECLARE_STRUCT(ReportedDeviceProperties,
      ascii_char_ptr, DeviceState,
      LocationProperties, Location
    );

    DECLARE_MODEL(ConfigProperties,
      WITH_REPORTED_PROPERTY(double, TemperatureMeanValue),
      WITH_REPORTED_PROPERTY(uint8_t, TelemetryInterval)
    );

    /* Part of DeviceInfo */
    DECLARE_STRUCT(DeviceProperties,
      ascii_char_ptr, DeviceID,
      _Bool, HubEnabledState
    );

    DECLARE_DEVICETWIN_MODEL(Thermostat,
      /* Telemetry (temperature, external temperature and humidity) */
      WITH_DATA(double, Temperature),
      WITH_DATA(double, ExternalTemperature),
      WITH_DATA(double, Humidity),
      WITH_DATA(ascii_char_ptr, DeviceId),

      /* DeviceInfo */
      WITH_DATA(ascii_char_ptr, ObjectType),
      WITH_DATA(_Bool, IsSimulatedDevice),
      WITH_DATA(ascii_char_ptr, Version),
      WITH_DATA(DeviceProperties, DeviceProperties),

      /* Device twin properties */
      WITH_REPORTED_PROPERTY(ReportedDeviceProperties, Device),
      WITH_REPORTED_PROPERTY(ConfigProperties, Config),
      WITH_REPORTED_PROPERTY(SystemProperties, System),

      WITH_DESIRED_PROPERTY(double, TemperatureMeanValue, onDesiredTemperatureMeanValue),
      WITH_DESIRED_PROPERTY(uint8_t, TelemetryInterval, onDesiredTelemetryInterval),

      /* Direct methods implemented by hello device */
      WITH_METHOD(Reboot),
      WITH_METHOD(InitiateFirmwareUpdate, ascii_char_ptr, FwPackageURI),

      /* Register direct methods with solution portal */
      WITH_REPORTED_PROPERTY(ascii_char_ptr_no_quotes, SupportedMethods)
    );

    END_NAMESPACE(Contoso);
    ```

## <a name="implement-hello-behavior-of-hello-device"></a><span data-ttu-id="7e4f5-117">Implementar el comportamiento de hello de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="7e4f5-117">Implement hello behavior of hello device</span></span>
<span data-ttu-id="7e4f5-118">Ahora agregue el código que implementa el comportamiento de hello definido en el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-118">Now add code that implements hello behavior defined in hello model.</span></span>

1. <span data-ttu-id="7e4f5-119">Agregar Hola después de funciones que controlen las propiedades de hello deseado establecidas en el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-119">Add hello following functions that handle hello desired properties set in hello solution dashboard.</span></span> <span data-ttu-id="7e4f5-120">Estas propiedades deseadas se definen en el modelo de hello:</span><span class="sxs-lookup"><span data-stu-id="7e4f5-120">These desired properties are defined in hello model:</span></span>

    ```c
    void onDesiredTemperatureMeanValue(void* argument)
    {
      /* By convention 'argument' is of hello type of hello MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TemperatureMeanValue = %f\r\n", thermostat->TemperatureMeanValue);

    }

    void onDesiredTelemetryInterval(void* argument)
    {
      /* By convention 'argument' is of hello type of hello MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TelemetryInterval = %d\r\n", thermostat->TelemetryInterval);
    }
    ```

1. <span data-ttu-id="7e4f5-121">Agregar Hola después de funciones que controlen métodos directos Hola invocados a través del centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-121">Add hello following functions that handle hello direct methods invoked through hello IoT hub.</span></span> <span data-ttu-id="7e4f5-122">Estos métodos directos se definen en el modelo de hello:</span><span class="sxs-lookup"><span data-stu-id="7e4f5-122">These direct methods are defined in hello model:</span></span>

    ```c
    /* Handlers for direct methods */
    METHODRETURN_HANDLE Reboot(Thermostat* thermostat)
    {
      (void)(thermostat);

      METHODRETURN_HANDLE result = MethodReturn_Create(201, "\"Rebooting\"");
      printf("Received reboot request\r\n");
      return result;
    }

    METHODRETURN_HANDLE InitiateFirmwareUpdate(Thermostat* thermostat, ascii_char_ptr FwPackageURI)
    {
      (void)(thermostat);

      METHODRETURN_HANDLE result = MethodReturn_Create(201, "\"Initiating Firmware Update\"");
      printf("Recieved firmware update request. Use package at: %s\r\n", FwPackageURI);
      return result;
    }
    ```

1. <span data-ttu-id="7e4f5-123">Agregue Hola después de la función que envía una solución de toohello preconfigurado de mensaje:</span><span class="sxs-lookup"><span data-stu-id="7e4f5-123">Add hello following function that sends a message toohello preconfigured solution:</span></span>
   
    ```c
    /* Send data tooIoT Hub */
    static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
    {
      IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
      if (messageHandle == NULL)
      {
        printf("unable toocreate a new IoTHubMessage\r\n");
      }
      else
      {
        if (IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, NULL, NULL) != IOTHUB_CLIENT_OK)
        {
          printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
          printf("IoTHubClient accepted hello message for delivery\r\n");
        }

        IoTHubMessage_Destroy(messageHandle);
      }
      free((void*)buffer);
    }
    ```

1. <span data-ttu-id="7e4f5-124">Agregue Hola siguiente controlador de devolución de llamada que se ejecuta cuando el dispositivo Hola envió nuevos valores de propiedad notificado solución toohello preconfigurado:</span><span class="sxs-lookup"><span data-stu-id="7e4f5-124">Add hello following callback handler that runs when hello device has sent new reported property values toohello preconfigured solution:</span></span>

    ```c
    /* Callback after sending reported properties */
    void deviceTwinCallback(int status_code, void* userContextCallback)
    {
      (void)(userContextCallback);
      printf("IoTHub: reported properties delivered with status_code = %u\n", status_code);
    }
    ```

1. <span data-ttu-id="7e4f5-125">Agregar siguiente Hola función tooconnect la solución de toohello preconfigurado de dispositivos en la nube de hello e intercambiar datos.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-125">Add hello following function tooconnect your device toohello preconfigured solution in hello cloud, and exchange data.</span></span> <span data-ttu-id="7e4f5-126">Esta función realiza Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7e4f5-126">This function performs hello following steps:</span></span>

    - <span data-ttu-id="7e4f5-127">Inicializa la plataforma de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-127">Initializes hello platform.</span></span>
    - <span data-ttu-id="7e4f5-128">Registra el espacio de nombres de hello Contoso con biblioteca de serialización de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-128">Registers hello Contoso namespace with hello serialization library.</span></span>
    - <span data-ttu-id="7e4f5-129">Inicializa a Hola cliente con la cadena de conexión de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-129">Initializes hello client with hello device connection string.</span></span>
    - <span data-ttu-id="7e4f5-130">Cree una instancia de hello **termostato** modelo.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-130">Create an instance of hello **Thermostat** model.</span></span>
    - <span data-ttu-id="7e4f5-131">Crea y envía valores de propiedades notificadas.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-131">Creates and sends reported property values.</span></span>
    - <span data-ttu-id="7e4f5-132">Envía un objeto **DeviceInfo**.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-132">Sends a **DeviceInfo** object.</span></span>
    - <span data-ttu-id="7e4f5-133">Crea una telemetría de toosend bucle cada segundo.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-133">Creates a loop toosend telemetry every second.</span></span>
    - <span data-ttu-id="7e4f5-134">Desinicializa todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="7e4f5-134">Deinitializes all resources.</span></span>

      ```c
      void remote_monitoring_run(void)
      {
        if (platform_init() != 0)
        {
          printf("Failed tooinitialize hello platform.\n");
        }
        else
        {
          if (SERIALIZER_REGISTER_NAMESPACE(Contoso) == NULL)
          {
            printf("Unable tooSERIALIZER_REGISTER_NAMESPACE\n");
          }
          else
          {
            IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, MQTT_Protocol);
            if (iotHubClientHandle == NULL)
            {
              printf("Failure in IoTHubClient_CreateFromConnectionString\n");
            }
            else
            {
      #ifdef MBED_BUILD_TIMESTAMP
              // For mbed add hello certificate information
              if (IoTHubClient_SetOption(iotHubClientHandle, "TrustedCerts", certificates) != IOTHUB_CLIENT_OK)
              {
                  printf("Failed tooset option \"TrustedCerts\"\n");
              }
      #endif // MBED_BUILD_TIMESTAMP
              Thermostat* thermostat = IoTHubDeviceTwin_CreateThermostat(iotHubClientHandle);
              if (thermostat == NULL)
              {
                printf("Failure in IoTHubDeviceTwin_CreateThermostat\n");
              }
              else
              {
                /* Set values for reported properties */
                thermostat->Config.TemperatureMeanValue = 55.5;
                thermostat->Config.TelemetryInterval = 3;
                thermostat->Device.DeviceState = "normal";
                thermostat->Device.Location.Latitude = 47.642877;
                thermostat->Device.Location.Longitude = -122.125497;
                thermostat->System.Manufacturer = "Contoso Inc.";
                thermostat->System.FirmwareVersion = "2.22";
                thermostat->System.InstalledRAM = "8 MB";
                thermostat->System.ModelNumber = "DB-14";
                thermostat->System.Platform = "Plat 9.75";
                thermostat->System.Processor = "i3-7";
                thermostat->System.SerialNumber = "SER21";
                /* Specify hello signatures of hello supported direct methods */
                thermostat->SupportedMethods = "{\"Reboot\": \"Reboot hello device\", \"InitiateFirmwareUpdate--FwPackageURI-string\": \"Updates device Firmware. Use parameter FwPackageURI toospecifiy hello URI of hello firmware file\"}";

                /* Send reported properties tooIoT Hub */
                if (IoTHubDeviceTwin_SendReportedStateThermostat(thermostat, deviceTwinCallback, NULL) != IOTHUB_CLIENT_OK)
                {
                  printf("Failed sending serialized reported state\n");
                }
                else
                {
                  printf("Send DeviceInfo object tooIoT Hub at startup\n");
      
                  thermostat->ObjectType = "DeviceInfo";
                  thermostat->IsSimulatedDevice = 0;
                  thermostat->Version = "1.0";
                  thermostat->DeviceProperties.HubEnabledState = 1;
                  thermostat->DeviceProperties.DeviceID = (char*)deviceId;

                  unsigned char* buffer;
                  size_t bufferSize;

                  if (SERIALIZE(&buffer, &bufferSize, thermostat->ObjectType, thermostat->Version, thermostat->IsSimulatedDevice, thermostat->DeviceProperties) != CODEFIRST_OK)
                  {
                    (void)printf("Failed serializing DeviceInfo\n");
                  }
                  else
                  {
                    sendMessage(iotHubClientHandle, buffer, bufferSize);
                  }

                  /* Send telemetry */
                  thermostat->Temperature = 50;
                  thermostat->ExternalTemperature = 55;
                  thermostat->Humidity = 50;
                  thermostat->DeviceId = (char*)deviceId;

                  while (1)
                  {
                    unsigned char*buffer;
                    size_t bufferSize;

                    (void)printf("Sending sensor value Temperature = %f, Humidity = %f\n", thermostat->Temperature, thermostat->Humidity);

                    if (SERIALIZE(&buffer, &bufferSize, thermostat->DeviceId, thermostat->Temperature, thermostat->Humidity, thermostat->ExternalTemperature) != CODEFIRST_OK)
                    {
                      (void)printf("Failed sending sensor value\r\n");
                    }
                    else
                    {
                      sendMessage(iotHubClientHandle, buffer, bufferSize);
                    }

                    ThreadAPI_Sleep(1000);
                  }

                  IoTHubDeviceTwin_DestroyThermostat(thermostat);
                }
              }
              IoTHubClient_Destroy(iotHubClientHandle);
            }
            serializer_deinit();
          }
        }
        platform_deinit();
      }
    ```
   
    <span data-ttu-id="7e4f5-135">Como referencia, este es un ejemplo **telemetría** toohello mensaje enviado preconfigurado soluciones:</span><span class="sxs-lookup"><span data-stu-id="7e4f5-135">For reference, here is a sample **Telemetry** message sent toohello preconfigured solution:</span></span>
   
    ```
    {"DeviceId":"mydevice01", "Temperature":50, "Humidity":50, "ExternalTemperature":55}
    ```