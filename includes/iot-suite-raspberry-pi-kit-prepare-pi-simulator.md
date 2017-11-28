## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="c8e34-101">Preparación de su Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="c8e34-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="c8e34-102">Instalación de Raspbian</span><span class="sxs-lookup"><span data-stu-id="c8e34-102">Install Raspbian</span></span>

<span data-ttu-id="c8e34-103">Si es la primera vez que usa su Raspberry Pi, debe instalar el sistema operativo Raspbian con NOOBS, que se encuentra en la tarjeta SD incluida en el kit.</span><span class="sxs-lookup"><span data-stu-id="c8e34-103">If this is the first time you are using your Raspberry Pi, you need to install the Raspbian operating system using NOOBS on the SD card included in the kit.</span></span> <span data-ttu-id="c8e34-104">En la [guía de software de Raspberry Pi][lnk-install-raspbian], se describe cómo instalar un sistema operativo en Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c8e34-104">The [Raspberry Pi Software Guide][lnk-install-raspbian] describes how to install an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="c8e34-105">En este tutorial se da por supuesto que ha instalado el sistema operativo Raspbian en su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c8e34-105">This tutorial assumes you have installed the Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="c8e34-106">La tarjeta SD incluida en el [kit de inicio de Microsoft Azure IoT para Raspberry Pi 3][lnk-starter-kits] ya tiene NOOBS instalado.</span><span class="sxs-lookup"><span data-stu-id="c8e34-106">The SD card included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="c8e34-107">Puede iniciar Raspberry Pi desde esta tarjeta y elegir instalar el sistema operativo Raspbian.</span><span class="sxs-lookup"><span data-stu-id="c8e34-107">You can boot the Raspberry Pi from this card and choose to install the Raspbian OS.</span></span>

<span data-ttu-id="c8e34-108">Para completar la configuración de hardware, debe:</span><span class="sxs-lookup"><span data-stu-id="c8e34-108">To complete the hardware setup, you need to:</span></span>

- <span data-ttu-id="c8e34-109">Conectar su Raspberry Pi a la fuente de alimentación que se incluye en el kit.</span><span class="sxs-lookup"><span data-stu-id="c8e34-109">Connect your Raspberry Pi to the power supply included in the kit.</span></span>
- <span data-ttu-id="c8e34-110">Conectar su Raspberry Pi a la red mediante el cable Ethernet incluido en el kit.</span><span class="sxs-lookup"><span data-stu-id="c8e34-110">Connect your Raspberry Pi to your network using the Ethernet cable included in your kit.</span></span> <span data-ttu-id="c8e34-111">Como alternativa, puede configurar [Conectividad inalámbrica][lnk-pi-wireless] para su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c8e34-111">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="c8e34-112">Ahora ha completado la configuración de hardware de su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c8e34-112">You have now completed the hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="c8e34-113">Inicio de sesión y acceso al terminal</span><span class="sxs-lookup"><span data-stu-id="c8e34-113">Sign in and access the terminal</span></span>

<span data-ttu-id="c8e34-114">Dispone de dos opciones para acceder a un entorno de terminal en su Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="c8e34-114">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="c8e34-115">Si tiene un teclado y un monitor conectados a su Raspberry Pi, puede usar la GUI de Raspbian para acceder a una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="c8e34-115">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

- <span data-ttu-id="c8e34-116">Acceda a la línea de comandos en su Raspberry Pi mediante SSH desde la máquina de escritorio.</span><span class="sxs-lookup"><span data-stu-id="c8e34-116">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="c8e34-117">Uso de una ventana de terminal en la GUI</span><span class="sxs-lookup"><span data-stu-id="c8e34-117">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="c8e34-118">Las credenciales predeterminadas para Raspbian son el nombre de usuario **pi** y la contraseña **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="c8e34-118">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="c8e34-119">En la barra de tareas en la GUI, puede iniciar la utilidad **Terminal** mediante el icono que parece un monitor.</span><span class="sxs-lookup"><span data-stu-id="c8e34-119">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="c8e34-120">Inicio de sesión con SSH</span><span class="sxs-lookup"><span data-stu-id="c8e34-120">Sign in with SSH</span></span>

<span data-ttu-id="c8e34-121">Puede usar SSH para el acceso de línea de comandos a su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c8e34-121">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="c8e34-122">En el artículo [SSH (Secure Shell)][lnk-pi-ssh], se describe cómo configurar SSH en Raspberry Pi y cómo conectarse desde [Windows][lnk-ssh-windows] o [Linux y Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="c8e34-122">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="c8e34-123">Inicie sesión con el nombre de usuario **pi** y la contraseña **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="c8e34-123">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="c8e34-124">Opcional: Compartir una carpeta en su Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="c8e34-124">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="c8e34-125">Si lo desea, puede compartir una carpeta en su Raspberry Pi con el entorno de escritorio.</span><span class="sxs-lookup"><span data-stu-id="c8e34-125">Optionally, you may want to share a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="c8e34-126">Compartir una carpeta le permite usar el editor de texto de escritorio preferido (como [Visual Studio Code](https://code.visualstudio.com/) o [Sublime Text](http://www.sublimetext.com/)) para editar archivos en su Raspberry Pi en lugar de usar `nano` o `vi`.</span><span class="sxs-lookup"><span data-stu-id="c8e34-126">Sharing a folder enables you to use your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) to edit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="c8e34-127">Para compartir una carpeta con Windows, configure un servidor Samba en Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c8e34-127">To share a folder with Windows, configure a Samba server on the Raspberry Pi.</span></span> <span data-ttu-id="c8e34-128">Como alternativa, use el servidor [SFTP](https://www.raspberrypi.org/documentation/remote-access/) integrado con un cliente SFTP en el escritorio.</span><span class="sxs-lookup"><span data-stu-id="c8e34-128">Alternatively, use the built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/