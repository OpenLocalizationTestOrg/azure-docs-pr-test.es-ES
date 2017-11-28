## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="00315-101">Preparación de su Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="00315-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="00315-102">Instalación de Raspbian</span><span class="sxs-lookup"><span data-stu-id="00315-102">Install Raspbian</span></span>

<span data-ttu-id="00315-103">Si es la primera vez que usa su Raspberry Pi, debe instalar el sistema operativo Raspbian con NOOBS, que se encuentra en la tarjeta SD incluida en el kit.</span><span class="sxs-lookup"><span data-stu-id="00315-103">If this is the first time you are using your Raspberry Pi, you need to install the Raspbian operating system using NOOBS on the SD card included in the kit.</span></span> <span data-ttu-id="00315-104">En la [guía de software de Raspberry Pi][lnk-install-raspbian], se describe cómo instalar un sistema operativo en Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="00315-104">The [Raspberry Pi Software Guide][lnk-install-raspbian] describes how to install an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="00315-105">En este tutorial se da por supuesto que ha instalado el sistema operativo Raspbian en su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="00315-105">This tutorial assumes you have installed the Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="00315-106">La tarjeta SD incluida en el [kit de inicio de Microsoft Azure IoT para Raspberry Pi 3][lnk-starter-kits] ya tiene NOOBS instalado.</span><span class="sxs-lookup"><span data-stu-id="00315-106">The SD card included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="00315-107">Puede iniciar Raspberry Pi desde esta tarjeta y elegir instalar el sistema operativo Raspbian.</span><span class="sxs-lookup"><span data-stu-id="00315-107">You can boot the Raspberry Pi from this card and choose to install the Raspbian OS.</span></span>

### <a name="set-up-the-hardware"></a><span data-ttu-id="00315-108">Configuración del hardware</span><span class="sxs-lookup"><span data-stu-id="00315-108">Set up the hardware</span></span>

<span data-ttu-id="00315-109">Este tutorial utiliza el sensor de BME280 incluido en el [Kit de inicio de Microsoft Azure IoT para Raspberry Pi 3][lnk-starter-kits] para generar datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="00315-109">This tutorial uses the BME280 sensor included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] to generate telemetry data.</span></span> <span data-ttu-id="00315-110">Usa un LED para indicar si Raspberry Pi procesa una invocación de método desde el panel de soluciones.</span><span class="sxs-lookup"><span data-stu-id="00315-110">It uses an LED to indicate when the Raspberry Pi processes a method invocation from the solution dashboard.</span></span>

<span data-ttu-id="00315-111">Los componentes en la placa de pruebas son:</span><span class="sxs-lookup"><span data-stu-id="00315-111">The components on the bread board are:</span></span>

- <span data-ttu-id="00315-112">LED rojo</span><span class="sxs-lookup"><span data-stu-id="00315-112">Red LED</span></span>
- <span data-ttu-id="00315-113">Resistencia de 220 ohmios (rojo, rojo, marrón)</span><span class="sxs-lookup"><span data-stu-id="00315-113">220-Ohm resistor (red, red, brown)</span></span>
- <span data-ttu-id="00315-114">Sensor de BME280</span><span class="sxs-lookup"><span data-stu-id="00315-114">BME280 sensor</span></span>

<span data-ttu-id="00315-115">En el diagrama siguiente se muestra cómo conectar el hardware:</span><span class="sxs-lookup"><span data-stu-id="00315-115">The following diagram shows how to connect your hardware:</span></span>

![Configuración de hardware para Raspberry Pi][img-connection-diagram]

<span data-ttu-id="00315-117">En la tabla siguiente se resumen las conexiones entre Raspberry Pi y los componentes en la placa de pruebas:</span><span class="sxs-lookup"><span data-stu-id="00315-117">The following table summarizes the connections from the Raspberry Pi to the components on the breadboard:</span></span>

| <span data-ttu-id="00315-118">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="00315-118">Raspberry Pi</span></span>            | <span data-ttu-id="00315-119">Placa de pruebas</span><span class="sxs-lookup"><span data-stu-id="00315-119">Breadboard</span></span>             |<span data-ttu-id="00315-120">Color</span><span class="sxs-lookup"><span data-stu-id="00315-120">Color</span></span>         |
| ----------------------- | ---------------------- | ------------- |
| <span data-ttu-id="00315-121">GND (patilla 14)</span><span class="sxs-lookup"><span data-stu-id="00315-121">GND (Pin 14)</span></span>            | <span data-ttu-id="00315-122">Patilla -ve de LED (18A)</span><span class="sxs-lookup"><span data-stu-id="00315-122">LED -ve pin (18A)</span></span>      | <span data-ttu-id="00315-123">Púrpura</span><span class="sxs-lookup"><span data-stu-id="00315-123">Purple</span></span>          |
| <span data-ttu-id="00315-124">GPCLK0 (patilla 7)</span><span class="sxs-lookup"><span data-stu-id="00315-124">GPCLK0 (Pin 7)</span></span>          | <span data-ttu-id="00315-125">Resistencia (25A)</span><span class="sxs-lookup"><span data-stu-id="00315-125">Resistor (25A)</span></span>         | <span data-ttu-id="00315-126">Naranja</span><span class="sxs-lookup"><span data-stu-id="00315-126">Orange</span></span>          |
| <span data-ttu-id="00315-127">SPI_CE0 (patilla 24)</span><span class="sxs-lookup"><span data-stu-id="00315-127">SPI_CE0 (Pin 24)</span></span>        | <span data-ttu-id="00315-128">CS (39A)</span><span class="sxs-lookup"><span data-stu-id="00315-128">CS (39A)</span></span>               | <span data-ttu-id="00315-129">Azul</span><span class="sxs-lookup"><span data-stu-id="00315-129">Blue</span></span>          |
| <span data-ttu-id="00315-130">SPI_SCLK (patilla 23)</span><span class="sxs-lookup"><span data-stu-id="00315-130">SPI_SCLK (Pin 23)</span></span>       | <span data-ttu-id="00315-131">SCK (36A)</span><span class="sxs-lookup"><span data-stu-id="00315-131">SCK (36A)</span></span>              | <span data-ttu-id="00315-132">Amarillo</span><span class="sxs-lookup"><span data-stu-id="00315-132">Yellow</span></span>        |
| <span data-ttu-id="00315-133">SPI_MISO (patilla 21)</span><span class="sxs-lookup"><span data-stu-id="00315-133">SPI_MISO (Pin 21)</span></span>       | <span data-ttu-id="00315-134">SDO (37A)</span><span class="sxs-lookup"><span data-stu-id="00315-134">SDO (37A)</span></span>              | <span data-ttu-id="00315-135">Blanco</span><span class="sxs-lookup"><span data-stu-id="00315-135">White</span></span>         |
| <span data-ttu-id="00315-136">SPI_MOSI (patilla 19)</span><span class="sxs-lookup"><span data-stu-id="00315-136">SPI_MOSI (Pin 19)</span></span>       | <span data-ttu-id="00315-137">SDI (38A)</span><span class="sxs-lookup"><span data-stu-id="00315-137">SDI (38A)</span></span>              | <span data-ttu-id="00315-138">Verde</span><span class="sxs-lookup"><span data-stu-id="00315-138">Green</span></span>         |
| <span data-ttu-id="00315-139">GND (patilla 6)</span><span class="sxs-lookup"><span data-stu-id="00315-139">GND (Pin 6)</span></span>             | <span data-ttu-id="00315-140">GND (35A)</span><span class="sxs-lookup"><span data-stu-id="00315-140">GND (35A)</span></span>              | <span data-ttu-id="00315-141">Negro</span><span class="sxs-lookup"><span data-stu-id="00315-141">Black</span></span>         |
| <span data-ttu-id="00315-142">3.3 V (patilla 1)</span><span class="sxs-lookup"><span data-stu-id="00315-142">3.3 V (Pin 1)</span></span>           | <span data-ttu-id="00315-143">3Vo (34A)</span><span class="sxs-lookup"><span data-stu-id="00315-143">3Vo (34A)</span></span>              | <span data-ttu-id="00315-144">Rojo</span><span class="sxs-lookup"><span data-stu-id="00315-144">Red</span></span>           |

<span data-ttu-id="00315-145">Para completar la configuración de hardware, debe:</span><span class="sxs-lookup"><span data-stu-id="00315-145">To complete the hardware setup, you need to:</span></span>

- <span data-ttu-id="00315-146">Conectar su Raspberry Pi a la fuente de alimentación que se incluye en el kit.</span><span class="sxs-lookup"><span data-stu-id="00315-146">Connect your Raspberry Pi to the power supply included in the kit.</span></span>
- <span data-ttu-id="00315-147">Conectar su Raspberry Pi a la red mediante el cable Ethernet incluido en el kit.</span><span class="sxs-lookup"><span data-stu-id="00315-147">Connect your Raspberry Pi to your network using the Ethernet cable included in your kit.</span></span> <span data-ttu-id="00315-148">Como alternativa, puede configurar [Conectividad inalámbrica][lnk-pi-wireless] para su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="00315-148">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="00315-149">Ahora ha completado la configuración de hardware de su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="00315-149">You have now completed the hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="00315-150">Inicio de sesión y acceso al terminal</span><span class="sxs-lookup"><span data-stu-id="00315-150">Sign in and access the terminal</span></span>

<span data-ttu-id="00315-151">Dispone de dos opciones para acceder a un entorno de terminal en su Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="00315-151">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="00315-152">Si tiene un teclado y un monitor conectados a su Raspberry Pi, puede usar la GUI de Raspbian para acceder a una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="00315-152">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

- <span data-ttu-id="00315-153">Acceda a la línea de comandos en su Raspberry Pi mediante SSH desde la máquina de escritorio.</span><span class="sxs-lookup"><span data-stu-id="00315-153">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="00315-154">Uso de una ventana de terminal en la GUI</span><span class="sxs-lookup"><span data-stu-id="00315-154">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="00315-155">Las credenciales predeterminadas para Raspbian son el nombre de usuario **pi** y la contraseña **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="00315-155">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="00315-156">En la barra de tareas en la GUI, puede iniciar la utilidad **Terminal** mediante el icono que parece un monitor.</span><span class="sxs-lookup"><span data-stu-id="00315-156">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="00315-157">Inicio de sesión con SSH</span><span class="sxs-lookup"><span data-stu-id="00315-157">Sign in with SSH</span></span>

<span data-ttu-id="00315-158">Puede usar SSH para el acceso de línea de comandos a su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="00315-158">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="00315-159">En el artículo [SSH (Secure Shell)][lnk-pi-ssh], se describe cómo configurar SSH en Raspberry Pi y cómo conectarse desde [Windows][lnk-ssh-windows] o [Linux y Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="00315-159">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="00315-160">Inicie sesión con el nombre de usuario **pi** y la contraseña **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="00315-160">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="00315-161">Opcional: Compartir una carpeta en su Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="00315-161">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="00315-162">Si lo desea, puede compartir una carpeta en su Raspberry Pi con el entorno de escritorio.</span><span class="sxs-lookup"><span data-stu-id="00315-162">Optionally, you may want to share a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="00315-163">Compartir una carpeta le permite usar el editor de texto de escritorio preferido (como [Visual Studio Code](https://code.visualstudio.com/) o [Sublime Text](http://www.sublimetext.com/)) para editar archivos en su Raspberry Pi en lugar de usar `nano` o `vi`.</span><span class="sxs-lookup"><span data-stu-id="00315-163">Sharing a folder enables you to use your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) to edit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="00315-164">Para compartir una carpeta con Windows, configure un servidor Samba en Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="00315-164">To share a folder with Windows, configure a Samba server on the Raspberry Pi.</span></span> <span data-ttu-id="00315-165">Como alternativa, use el servidor [SFTP](https://www.raspberrypi.org/documentation/remote-access/) integrado con un cliente SFTP en el escritorio.</span><span class="sxs-lookup"><span data-stu-id="00315-165">Alternatively, use the built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

### <a name="enable-spi"></a><span data-ttu-id="00315-166">Habilitación de SPI</span><span class="sxs-lookup"><span data-stu-id="00315-166">Enable SPI</span></span>

<span data-ttu-id="00315-167">Para poder ejecutar la aplicación de ejemplo, debe habilitar el bus de interfaz de periféricos en serie (SPI) en Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="00315-167">Before you can run the sample application, you must enable the Serial Peripheral Interface (SPI) bus on the Raspberry Pi.</span></span> <span data-ttu-id="00315-168">Raspberry Pi se comunica con el dispositivo de sensor de BME280 a través del bus SPI.</span><span class="sxs-lookup"><span data-stu-id="00315-168">The Raspberry Pi communicates with the BME280 sensor device over the SPI bus.</span></span> <span data-ttu-id="00315-169">Use el comando siguiente para editar el archivo de configuración:</span><span class="sxs-lookup"><span data-stu-id="00315-169">Use the following command to edit the configuration file:</span></span>

```sh
sudo nano /boot/config.txt
```

<span data-ttu-id="00315-170">Busque la línea:</span><span class="sxs-lookup"><span data-stu-id="00315-170">Find the line:</span></span>

`#dtparam=spi=on`

- <span data-ttu-id="00315-171">Para quitar la marca de comentario de la línea, elimine `#` al principio.</span><span class="sxs-lookup"><span data-stu-id="00315-171">To uncomment the line, delete the `#` at the start.</span></span>
- <span data-ttu-id="00315-172">Guarde los cambios (**Ctrl-O**, **ENTRAR**) y salga del editor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="00315-172">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>
- <span data-ttu-id="00315-173">Para habilitar SPI, reinicie Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="00315-173">To enable SPI, reboot the Raspberry Pi.</span></span> <span data-ttu-id="00315-174">Al reiniciarlo, se desconecta el terminal. Debe iniciar sesión de nuevo cuando se reinicia Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="00315-174">Rebooting disconnects the terminal, you need to sign in again when the Raspberry Pi restarts:</span></span>

  ```sh
  sudo reboot
  ```


[img-connection-diagram]: media/iot-suite-raspberry-pi-kit-prepare-pi/rpi2_remote_monitoring.png

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/