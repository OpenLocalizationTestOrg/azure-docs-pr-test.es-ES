## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="2de0b-101">Preparación de su Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="2de0b-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="2de0b-102">Instalación de Raspbian</span><span class="sxs-lookup"><span data-stu-id="2de0b-102">Install Raspbian</span></span>

<span data-ttu-id="2de0b-103">Si se trata de hello primera vez que usa el instalador de plataforma de frambuesa, necesita tooinstall hello Raspbian SO mediante NOOBS en tarjeta SD de hello incluida en el kit de Hola.</span><span class="sxs-lookup"><span data-stu-id="2de0b-103">If this is hello first time you are using your Raspberry Pi, you need tooinstall hello Raspbian operating system using NOOBS on hello SD card included in hello kit.</span></span> <span data-ttu-id="2de0b-104">Hola [frambuesa Pi Software guía] [ lnk-install-raspbian] describe cómo tooinstall un sistema operativo en el instalador de plataforma de frambuesa.</span><span class="sxs-lookup"><span data-stu-id="2de0b-104">hello [Raspberry Pi Software Guide][lnk-install-raspbian] describes how tooinstall an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="2de0b-105">Este tutorial se da por supuesto que ha instalado el sistema operativo de hello Raspbian en el instalador de plataforma de frambuesa.</span><span class="sxs-lookup"><span data-stu-id="2de0b-105">This tutorial assumes you have installed hello Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="2de0b-106">tarjeta de Hello SD incluida en hello [Microsoft Azure IoT Starter Kit para frambuesa Pi 3] [ lnk-starter-kits] ya tiene NOOBS instalado.</span><span class="sxs-lookup"><span data-stu-id="2de0b-106">hello SD card included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="2de0b-107">Se puede iniciar Hola frambuesa Pi de esta tarjeta y elija tooinstall hello Raspbian OS.</span><span class="sxs-lookup"><span data-stu-id="2de0b-107">You can boot hello Raspberry Pi from this card and choose tooinstall hello Raspbian OS.</span></span>

### <a name="set-up-hello-hardware"></a><span data-ttu-id="2de0b-108">Configurar el hardware de Hola</span><span class="sxs-lookup"><span data-stu-id="2de0b-108">Set up hello hardware</span></span>

<span data-ttu-id="2de0b-109">Este tutorial usa sensor hello BME280 incluido en hello [Microsoft Azure IoT Starter Kit para frambuesa Pi 3] [ lnk-starter-kits] toogenerate los datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="2de0b-109">This tutorial uses hello BME280 sensor included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] toogenerate telemetry data.</span></span> <span data-ttu-id="2de0b-110">Utiliza un tooindicate LED cuando Hola frambuesa Pi procesa una invocación de método desde el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="2de0b-110">It uses an LED tooindicate when hello Raspberry Pi processes a method invocation from hello solution dashboard.</span></span>

<span data-ttu-id="2de0b-111">componentes de Hello en el panel de pan de hello son:</span><span class="sxs-lookup"><span data-stu-id="2de0b-111">hello components on hello bread board are:</span></span>

- <span data-ttu-id="2de0b-112">LED rojo</span><span class="sxs-lookup"><span data-stu-id="2de0b-112">Red LED</span></span>
- <span data-ttu-id="2de0b-113">Resistencia de 220 ohmios (rojo, rojo, marrón)</span><span class="sxs-lookup"><span data-stu-id="2de0b-113">220-Ohm resistor (red, red, brown)</span></span>
- <span data-ttu-id="2de0b-114">Sensor de BME280</span><span class="sxs-lookup"><span data-stu-id="2de0b-114">BME280 sensor</span></span>

<span data-ttu-id="2de0b-115">Hola siguiente diagrama muestra cómo tooconnect su hardware:</span><span class="sxs-lookup"><span data-stu-id="2de0b-115">hello following diagram shows how tooconnect your hardware:</span></span>

![Configuración de hardware para Raspberry Pi][img-connection-diagram]

<span data-ttu-id="2de0b-117">Hello tabla siguiente resume las conexiones de Hola de componentes de hello frambuesa Pi toohello en breadboard hello:</span><span class="sxs-lookup"><span data-stu-id="2de0b-117">hello following table summarizes hello connections from hello Raspberry Pi toohello components on hello breadboard:</span></span>

| <span data-ttu-id="2de0b-118">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="2de0b-118">Raspberry Pi</span></span>            | <span data-ttu-id="2de0b-119">Placa de pruebas</span><span class="sxs-lookup"><span data-stu-id="2de0b-119">Breadboard</span></span>             |<span data-ttu-id="2de0b-120">Color</span><span class="sxs-lookup"><span data-stu-id="2de0b-120">Color</span></span>         |
| ----------------------- | ---------------------- | ------------- |
| <span data-ttu-id="2de0b-121">GND (patilla 14)</span><span class="sxs-lookup"><span data-stu-id="2de0b-121">GND (Pin 14)</span></span>            | <span data-ttu-id="2de0b-122">Patilla -ve de LED (18A)</span><span class="sxs-lookup"><span data-stu-id="2de0b-122">LED -ve pin (18A)</span></span>      | <span data-ttu-id="2de0b-123">Púrpura</span><span class="sxs-lookup"><span data-stu-id="2de0b-123">Purple</span></span>          |
| <span data-ttu-id="2de0b-124">GPCLK0 (patilla 7)</span><span class="sxs-lookup"><span data-stu-id="2de0b-124">GPCLK0 (Pin 7)</span></span>          | <span data-ttu-id="2de0b-125">Resistencia (25A)</span><span class="sxs-lookup"><span data-stu-id="2de0b-125">Resistor (25A)</span></span>         | <span data-ttu-id="2de0b-126">Naranja</span><span class="sxs-lookup"><span data-stu-id="2de0b-126">Orange</span></span>          |
| <span data-ttu-id="2de0b-127">SPI_CE0 (patilla 24)</span><span class="sxs-lookup"><span data-stu-id="2de0b-127">SPI_CE0 (Pin 24)</span></span>        | <span data-ttu-id="2de0b-128">CS (39A)</span><span class="sxs-lookup"><span data-stu-id="2de0b-128">CS (39A)</span></span>               | <span data-ttu-id="2de0b-129">Azul</span><span class="sxs-lookup"><span data-stu-id="2de0b-129">Blue</span></span>          |
| <span data-ttu-id="2de0b-130">SPI_SCLK (patilla 23)</span><span class="sxs-lookup"><span data-stu-id="2de0b-130">SPI_SCLK (Pin 23)</span></span>       | <span data-ttu-id="2de0b-131">SCK (36A)</span><span class="sxs-lookup"><span data-stu-id="2de0b-131">SCK (36A)</span></span>              | <span data-ttu-id="2de0b-132">Amarillo</span><span class="sxs-lookup"><span data-stu-id="2de0b-132">Yellow</span></span>        |
| <span data-ttu-id="2de0b-133">SPI_MISO (patilla 21)</span><span class="sxs-lookup"><span data-stu-id="2de0b-133">SPI_MISO (Pin 21)</span></span>       | <span data-ttu-id="2de0b-134">SDO (37A)</span><span class="sxs-lookup"><span data-stu-id="2de0b-134">SDO (37A)</span></span>              | <span data-ttu-id="2de0b-135">Blanco</span><span class="sxs-lookup"><span data-stu-id="2de0b-135">White</span></span>         |
| <span data-ttu-id="2de0b-136">SPI_MOSI (patilla 19)</span><span class="sxs-lookup"><span data-stu-id="2de0b-136">SPI_MOSI (Pin 19)</span></span>       | <span data-ttu-id="2de0b-137">SDI (38A)</span><span class="sxs-lookup"><span data-stu-id="2de0b-137">SDI (38A)</span></span>              | <span data-ttu-id="2de0b-138">Verde</span><span class="sxs-lookup"><span data-stu-id="2de0b-138">Green</span></span>         |
| <span data-ttu-id="2de0b-139">GND (patilla 6)</span><span class="sxs-lookup"><span data-stu-id="2de0b-139">GND (Pin 6)</span></span>             | <span data-ttu-id="2de0b-140">GND (35A)</span><span class="sxs-lookup"><span data-stu-id="2de0b-140">GND (35A)</span></span>              | <span data-ttu-id="2de0b-141">Negro</span><span class="sxs-lookup"><span data-stu-id="2de0b-141">Black</span></span>         |
| <span data-ttu-id="2de0b-142">3.3 V (patilla 1)</span><span class="sxs-lookup"><span data-stu-id="2de0b-142">3.3 V (Pin 1)</span></span>           | <span data-ttu-id="2de0b-143">3Vo (34A)</span><span class="sxs-lookup"><span data-stu-id="2de0b-143">3Vo (34A)</span></span>              | <span data-ttu-id="2de0b-144">Rojo</span><span class="sxs-lookup"><span data-stu-id="2de0b-144">Red</span></span>           |

<span data-ttu-id="2de0b-145">el programa de instalación del hardware de Hola de toocomplete, debe:</span><span class="sxs-lookup"><span data-stu-id="2de0b-145">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="2de0b-146">Conecte la fuente de alimentación de toohello de frambuesa Pi incluida en el kit de Hola.</span><span class="sxs-lookup"><span data-stu-id="2de0b-146">Connect your Raspberry Pi toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="2de0b-147">Conectar su red de tooyour de frambuesa Pi con cable de Ethernet de hello incluido en el kit.</span><span class="sxs-lookup"><span data-stu-id="2de0b-147">Connect your Raspberry Pi tooyour network using hello Ethernet cable included in your kit.</span></span> <span data-ttu-id="2de0b-148">Como alternativa, puede configurar [Conectividad inalámbrica][lnk-pi-wireless] para su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="2de0b-148">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="2de0b-149">Ahora ha completado el programa de instalación de hardware de Hola de su Pi frambuesa.</span><span class="sxs-lookup"><span data-stu-id="2de0b-149">You have now completed hello hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="2de0b-150">Inicio de sesión y terminal Hola</span><span class="sxs-lookup"><span data-stu-id="2de0b-150">Sign in and access hello terminal</span></span>

<span data-ttu-id="2de0b-151">Tiene dos tooaccess de opciones un entorno de terminal en su Pi frambuesa:</span><span class="sxs-lookup"><span data-stu-id="2de0b-151">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="2de0b-152">Si tiene un teclado y supervisar tooyour conectado frambuesa Pi, puede usar hello Raspbian GUI tooaccess una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="2de0b-152">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

- <span data-ttu-id="2de0b-153">Línea de comandos de acceso hello en el instalador de plataforma de frambuesa mediante SSH desde el equipo de escritorio.</span><span class="sxs-lookup"><span data-stu-id="2de0b-153">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="2de0b-154">Usar una ventana de terminal en hello GUI</span><span class="sxs-lookup"><span data-stu-id="2de0b-154">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="2de0b-155">las credenciales predeterminadas de Hola para Raspbian son nombre de usuario **pi** y la contraseña **frambuesa**.</span><span class="sxs-lookup"><span data-stu-id="2de0b-155">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="2de0b-156">En la barra de tareas de Hola Hola GUI, puede iniciar hello **Terminal** utilidad mediante el icono de Hola que parece un monitor.</span><span class="sxs-lookup"><span data-stu-id="2de0b-156">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="2de0b-157">Inicio de sesión con SSH</span><span class="sxs-lookup"><span data-stu-id="2de0b-157">Sign in with SSH</span></span>

<span data-ttu-id="2de0b-158">Puede utilizar SSH para acceso de línea de comandos tooyour frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="2de0b-158">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="2de0b-159">artículo de Hello [SSH (Secure Shell)] [ lnk-pi-ssh] describe cómo tooconfigure SSH en el instalador de plataforma de frambuesa y cómo tooconnect de [Windows] [ lnk-ssh-windows] o [Linux y Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="2de0b-159">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="2de0b-160">Inicie sesión con el nombre de usuario **pi** y la contraseña **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="2de0b-160">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="2de0b-161">Opcional: Compartir una carpeta en su Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="2de0b-161">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="2de0b-162">Si lo desea, puede que desee tooshare una carpeta en el instalador de plataforma de frambuesa con el entorno de escritorio.</span><span class="sxs-lookup"><span data-stu-id="2de0b-162">Optionally, you may want tooshare a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="2de0b-163">Compartir una carpeta permite toouse su editor de texto preferido del escritorio (como [código de Visual Studio](https://code.visualstudio.com/) o [texto fundamentales](http://www.sublimetext.com/)) tooedit archivos en el instalador de plataforma de frambuesa en lugar de usar `nano` o `vi`.</span><span class="sxs-lookup"><span data-stu-id="2de0b-163">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="2de0b-164">tooshare una carpeta con Windows, configurar un servidor de Samba en hello frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="2de0b-164">tooshare a folder with Windows, configure a Samba server on hello Raspberry Pi.</span></span> <span data-ttu-id="2de0b-165">O bien, usar integrada de hello [SFTP](https://www.raspberrypi.org/documentation/remote-access/) servidor con un cliente SFTP en el escritorio.</span><span class="sxs-lookup"><span data-stu-id="2de0b-165">Alternatively, use hello built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

### <a name="enable-spi"></a><span data-ttu-id="2de0b-166">Habilitación de SPI</span><span class="sxs-lookup"><span data-stu-id="2de0b-166">Enable SPI</span></span>

<span data-ttu-id="2de0b-167">Antes de poder ejecutar la aplicación de ejemplo de Hola, debe habilitar bus interfaz periféricos serie (SPI) Hola Hola frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="2de0b-167">Before you can run hello sample application, you must enable hello Serial Peripheral Interface (SPI) bus on hello Raspberry Pi.</span></span> <span data-ttu-id="2de0b-168">Hola frambuesa Pi se comunica con dispositivos de hello BME280 sensor a través Hola bus SPI.</span><span class="sxs-lookup"><span data-stu-id="2de0b-168">hello Raspberry Pi communicates with hello BME280 sensor device over hello SPI bus.</span></span> <span data-ttu-id="2de0b-169">Usar hello el archivo de configuración de comando tooedit Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="2de0b-169">Use hello following command tooedit hello configuration file:</span></span>

```sh
sudo nano /boot/config.txt
```

<span data-ttu-id="2de0b-170">Busque la línea de saludo:</span><span class="sxs-lookup"><span data-stu-id="2de0b-170">Find hello line:</span></span>

`#dtparam=spi=on`

- <span data-ttu-id="2de0b-171">línea de hello toouncomment, delete hello `#` al principio de Hola.</span><span class="sxs-lookup"><span data-stu-id="2de0b-171">toouncomment hello line, delete hello `#` at hello start.</span></span>
- <span data-ttu-id="2de0b-172">Guarde los cambios (**O Ctrl**, **ENTRAR**) y salga del editor hello (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="2de0b-172">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>
- <span data-ttu-id="2de0b-173">tooenable SPI, reinicie Hola frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="2de0b-173">tooenable SPI, reboot hello Raspberry Pi.</span></span> <span data-ttu-id="2de0b-174">Reiniciar el sistema desconecta terminal hello, necesita toosign de nuevo cuando se reinicia Hola frambuesa Pi:</span><span class="sxs-lookup"><span data-stu-id="2de0b-174">Rebooting disconnects hello terminal, you need toosign in again when hello Raspberry Pi restarts:</span></span>

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