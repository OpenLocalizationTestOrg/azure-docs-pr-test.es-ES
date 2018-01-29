---
title: Tutorial para la seguridad de X.509 en Azure IoT Hub | Microsoft Docs
description: "Introducción a la seguridad basada en X.509 en Azure IoT Hub en un entorno simulado."
services: iot-hub
documentationcenter: 
author: dsk-2015
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/10/2017
ms.author: dkshir
ms.openlocfilehash: 93f9099d7aef1161f7789e7b21a88a8691cb2a8e
ms.sourcegitcommit: 933af6219266cc685d0c9009f533ca1be03aa5e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="set-up-x509-security-in-your-azure-iot-hub"></a>Configuración de la seguridad de X.509 en Azure IoT Hub

Este tutorial simula los pasos necesarios para proteger Azure IoT Hub mediante la *autenticación de certificado X.509*. Con fines ilustrativos, mostraremos cómo usar la herramienta de código abierto OpenSSL para crear certificados localmente en una máquina Windows. Se recomienda usar este tutorial solo para la realización de pruebas. Para el entorno de producción debe comprar los certificados a una *entidad de certificación (CA) raíz*. 

## <a name="prerequisites"></a>Requisitos previos
Este tutorial requiere que tenga listos los siguientes recursos:

- Ha creado una instancia de IoT Hub con su suscripción de Azure. Para ver los pasos con detalle, consulte [Creación de una instancia de IoT Hub mediante Azure Portal](iot-hub-create-through-portal.md). 
- [Visual Studio 2015 o Visual Studio 2017](https://www.visualstudio.com/vs/) están instalados en la máquina. 

<a id="getcerts"></a>

## <a name="get-x509-ca-certificates"></a>Obtención de certificados de entidad de certificación X.509
La seguridad basada en certificados X.509 de IoT Hub requiere que comience con un [cadena de certificados X.509](https://en.wikipedia.org/wiki/X.509#Certificate_chains_and_cross-certification), que incluya el certificado raíz, así como cualquier certificado intermedio hasta el certificado de hoja. 

Puede elegir cualquiera de los siguientes métodos para obtener los certificados:
- Comprar certificados X.509 a una *entidad de certificación (CA) raíz*. Se recomienda para entornos de producción.
O bien,
- Crear sus propios certificados X.509 mediante una herramienta de terceros como [OpenSSL](https://www.openssl.org/). Es apropiado tanto para pruebas como para desarrollo. Las secciones *Creación de certificados X.509* y *Creación de una cadena de certificados X.509* del artículo [Uso de PowerShell para crear certificados X.509](iot-hub-security-x509-create-certificates.md) le guían a través de un script de PowerShell de ejemplo para crear los certificados mediante OpenSSL y PowerShell. Si prefiere usar el shell de **Bash** en lugar de PowerShell, consulte las secciones relacionadas de [Managing CA Certificates Sample](https://github.com/Azure/azure-iot-sdk-c/blob/master/tools/CACertificates/CACertificateOverview.md) (Administración del ejemplo de certificados de CA). En el resto de este tutorial se usará el entorno de OpenSSL configurado en esta guía de *procedimientos* para examinar la seguridad X.509 de un extremo a otro en Azure IoT Hub.


<a id="registercerts"></a>

## <a name="register-x509-ca-certificates-to-your-iot-hub"></a>Registro de certificados de entidad de certificación X.509 en una instancia de IoT Hub

Estos pasos muestran cómo agregar una entidad de certificación nueva a una instancia de IoT Hub a través del portal.

1. En Azure Portal, navegue a su instancia de IoT Hub y abra el menú **CONFIGURACIÓN** > **Certificados**. 
2. Haga clic en **Agregar** para agregar un certificado nuevo.
3. Escriba un nombre para mostrar descriptivo para el certificado. Seleccione en la máquina el archivo de certificado raíz denominado *RootCA.cer* que creó en la sección anterior. Haga clic en **Cargar**.
4. Una vez que reciba la notificación de que el certificado se ha cargado correctamente, haga clic en **Guardar**.

    ![Carga del certificado](./media/iot-hub-security-x509-get-started/add-new-cert.png)  

   El certificado se mostrará en la lista **Explorador de certificados**. Observe que el **ESTADO** de este certificado es *Sin comprobar*.

5. Haga clic en el certificado que agregó en el paso anterior.

6. En la hoja **Detalles del certificado**, haga clic en **Generar código de verificación**.

7. Crea un **código de verificación** para validar la propiedad del certificado. Copie el código en el Portapapeles. 

   ![Comprobar certificado](./media/iot-hub-security-x509-get-started/verify-cert.png)  

8. Ahora, tiene que firmar este *código de verificación* con la clave privada asociada con el certificado de entidad de certificación X.509, lo que genera una firma. Hay herramientas disponibles para realizar este proceso de firma, como por ejemplo, OpenSSL. Esto se conoce como la [prueba de posesión](https://tools.ietf.org/html/rfc5280#section-3.1). Si ha usado los scripts de PowerShell de ejemplo de la sección anterior, ejecute el script mencionado en la sección [Proof of possession of your X.509 CA certificate](iot-hub-security-x509-create-certificates.md#signverificationcode) (Prueba de posesión de un certificado de entidad de certificación X.509).
 
9. Cargue la firma resultante del paso 8 en su instancia de IoT Hub del portal. En la hoja **Detalles del certificado** de Azure Portal, navegue hasta **Archivo .pem o .cer del certificado de verificación** y seleccione la firma, por ejemplo, *VerifyCert4.cer* creado por el comando de PowerShell de ejemplo mediante el icono del _Explorador de archivos_ que aparece al lado.

10. Una vez que el certificado se cargue correctamente, haga clic en **Comprobar**. El **ESTADO** del certificado cambia a  **_Comprobado_**  en la hoja **Certificados**. Si no se actualiza automáticamente, haga clic en **Actualizar**.

   ![Cargar comprobación de certificado](./media/iot-hub-security-x509-get-started/upload-cert-verification.png)  


<a id="createdevice"></a>

## <a name="create-an-x509-device-for-your-iot-hub"></a>Creación de un dispositivo X.509 para una instancia de IoT Hub

1. En Azure Portal, navegue a **Device Explorer** en la instancia de IoT Hub.

2. Haga clic en **Agregar** para agregar un dispositivo nuevo. 

3. Escribe un nombre para mostrar descriptivo en **Id. de dispositivo** y seleccione **_X.509 CA Signed_** (X.509 con firma de CA) en **Tipo de autenticación**. Haga clic en **Guardar**.

   ![Crear un dispositivo X.509 en el portal](./media/iot-hub-security-x509-get-started/create-x509-device.png)



<a id="authenticatedevice"></a>

## <a name="authenticate-your-x509-device-with-the-x509-certificates"></a>Autenticación de un dispositivo X.509 con los certificados X.509

Para autenticar un dispositivo X.509, en primer lugar hay que firmarlo con el certificado de entidad de certificación. La firma de dispositivos de hoja se suele realizar en la fábrica, donde se han habilitado las herramientas de fabricación pertinentes. Cuando el dispositivo pasa de un fabricante a otro, la acción de firma de cada fabricante se captura como un certificado intermedio en la cadena. El resultado final es una cadena de certificados del certificado de entidad de certificación al certificado de hoja del dispositivo. Si ha usado nuestros scripts de PowerShell en las secciones anteriores, puede ejecutar el script mencionado en la sección *Create leaf X.509 certificate for your device* (Creación de un certificado X.509 de hoja para un dispositivo) del artículo [PowerShell scripts to manage CA-signed X.509 certificates](iot-hub-security-x509-create-certificates.md) (Scripts de PowerShell para administrar certificados X.509 con la firma de una autoridad de certificación) para simular este proceso.

A continuación, se mostrará cómo crear una aplicación de C# para simular el dispositivo X.509 registrado en su instancia de IoT Hub. Se enviarán los valores de temperatura y humedad del dispositivo simulado al centro. Tenga en cuenta que en este tutorial, solo se va a crear la aplicación del dispositivo. La creación de la aplicación del servicio IoT Hub de centro de IoT que enviará una respuesta a los eventos enviados por este dispositivo simulado queda como ejercicio para los lectores. La aplicación de C# asume que ha seguido los scripts de PowerShell que se mencionan en el artículo [PowerShell scripts to manage CA-signed X.509 certificates](iot-hub-security-x509-create-certificates.md) (Scripts de PowerShell para administrar certificados X.509 con la firma de una autoridad de certificación)

1. En Visual Studio, cree un nuevo proyecto Windows Classic Desktop de Visual C# con la plantilla de proyecto Aplicación de consola. Asigne al proyecto el nombre **SimulateX509Device**.
   ![Crear proyecto de dispositivo X.509 en Visual Studio](./media/iot-hub-security-x509-get-started/create-device-project.png)

2. En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **SimulateX509Device** y haga clic en **Administrar paquetes NuGet**. En la ventana Administrador de paquetes NuGet, seleccione **Examinar** y busque **microsoft.azure.devices.client**. Seleccione **Instalar** para instalar el paquete **Microsoft.Azure.Devices.Client** y acepte las condiciones de uso. Este procedimiento descarga, instala y agrega una referencia al paquete NuGet del SDK de dispositivo IoT de Azure y sus dependencias.
   ![Agregar paquete NuGet del SDK de dispositivo en Visual Studio](./media/iot-hub-security-x509-get-started/device-sdk-nuget.png)

3. Agregue las siguientes líneas de código al principio del archivo *Program.cs*:
    
    ```CSharp
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using System.Security.Cryptography.X509Certificates;
    ```

4. Agregue las siguientes líneas de código dentro de la clase **Program**:
    
    ```CSharp
        private static int MESSAGE_COUNT = 5;
        private const int TEMPERATURE_THRESHOLD = 30;
        private static String deviceId = "<your-device-id>";
        private static float temperature;
        private static float humidity;
        private static Random rnd = new Random();
    ```
   En lugar del marcador de posición _<your_device_id>_ utilice el nombre de dispositivo descriptivo que usó en la sección anterior.

5. Agregue la siguiente función para crear números aleatorios de temperatura y humedad, y enviar dichos valores al centro:
    ```CSharp
    static async Task SendEvent(DeviceClient deviceClient)
    {
        string dataBuffer;
        Console.WriteLine("Device sending {0} messages to IoTHub...\n", MESSAGE_COUNT);

        for (int count = 0; count < MESSAGE_COUNT; count++)
        {
            temperature = rnd.Next(20, 35);
            humidity = rnd.Next(60, 80);
            dataBuffer = string.Format("{{\"deviceId\":\"{0}\",\"messageId\":{1},\"temperature\":{2},\"humidity\":{3}}}", deviceId, count, temperature, humidity);
            Message eventMessage = new Message(Encoding.UTF8.GetBytes(dataBuffer));
            eventMessage.Properties.Add("temperatureAlert", (temperature > TEMPERATURE_THRESHOLD) ? "true" : "false");
            Console.WriteLine("\t{0}> Sending message: {1}, Data: [{2}]", DateTime.Now.ToLocalTime(), count, dataBuffer);

            await deviceClient.SendEventAsync(eventMessage);
        }
    }
    ```

6. Por último, agregue las siguientes líneas de código a la función **Main**, pero reemplace los marcadores de posición _device-id_, _your-iot-hub-name_ y  _absolute-path-to-your-device-pfx-file_ en función de lo que solicite el programa de instalación.
    ```CSharp
    try
    {
        var cert = new X509Certificate2(@"<absolute-path-to-your-device-pfx-file>", "123");
        var auth = new DeviceAuthenticationWithX509Certificate("<device-id>", cert);
        var deviceClient = DeviceClient.Create("<your-iot-hub-name>.azure-devices.net", auth, TransportType.Amqp_Tcp_Only);

        if (deviceClient == null)
        {
            Console.WriteLine("Failed to create DeviceClient!");
        }
        else
        {
            Console.WriteLine("Successfully created DeviceClient!");
            SendEvent(deviceClient).Wait();
        }

        Console.WriteLine("Exiting...\n");
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error in sample: {0}", ex.Message);
    }
    ```
   Este código se conecta a su instancia de IoT Hub mediante la creación de la cadena de conexión para el dispositivo X.509. Una vez que se ha conectado correctamente, envía eventos de temperatura y humedad al centro y espera su respuesta. 
7. Dado que esta aplicación accede a un archivo *.pfx*, es preciso ejecutarla en modo de *administrador*. Compile la solución de Visual Studio. Abra una nueva ventana de comandos como **administrador** y navegue hasta la carpeta que contiene esta solución. Navegue hasta la ruta de acceso *bin/Debug* en la carpeta de soluciones. Ejecute la aplicación **SimulateX509Device.exe** desde la ventana de comandos de _administración_. Debería ver que el dispositivo se conecta correctamente al centro y envía los eventos. 
   ![Ejecutar aplicación de dispositivo](./media/iot-hub-security-x509-get-started/device-app-success.png)

## <a name="see-also"></a>Otras referencias
Para obtener más información sobre cómo proteger la solución de IoT, consulte:

* [Procedimientos recomendados para la seguridad de IoT][lnk-security-best-practices]
* [Arquitectura de seguridad de IoT][lnk-security-architecture]
* [Protección de su implementación de IoT][lnk-security-deployment]

Para explorar aún más las funcionalidades de IoT Hub, consulte:

* [Implementación de Azure IoT Edge en un dispositivo simulado en Linux: versión preliminar][lnk-iotedge]

[lnk-security-best-practices]: iot-hub-security-best-practices.md
[lnk-security-architecture]: iot-hub-security-architecture.md
[lnk-security-deployment]: iot-hub-security-deployment.md

[lnk-iotedge]: ../iot-edge/tutorial-simulate-device-linux.md
