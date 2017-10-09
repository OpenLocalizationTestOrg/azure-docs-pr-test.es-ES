1. <span data-ttu-id="aa6eb-101">Copie Hola instalador tooa carpeta local (por ejemplo, / tmp) en servidores de Hola que desee que tooprotect.</span><span class="sxs-lookup"><span data-stu-id="aa6eb-101">Copy hello installer tooa local folder (for example, /tmp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="aa6eb-102">En un terminal, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="aa6eb-102">In a terminal, run hello following commands:</span></span>
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. <span data-ttu-id="aa6eb-103">tooinstall servicio de movilidad, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="aa6eb-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. <span data-ttu-id="aa6eb-104">Una vez completada la instalación, Hola Mobility Service debe servidor de configuración de tooget toohello registrados.</span><span class="sxs-lookup"><span data-stu-id="aa6eb-104">Once installation is complete, hello Mobility Service needs tooget registered toohello configuration server.</span></span> <span data-ttu-id="aa6eb-105">Siguiente ejecución Hola comando tooregister Hola Mobility Service con el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="aa6eb-105">Run hello following command tooregister hello Mobility Service with Configuration server.</span></span>

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a><span data-ttu-id="aa6eb-106">Línea de comandos del instalador de Mobility Service</span><span class="sxs-lookup"><span data-stu-id="aa6eb-106">Mobility Service installer command-line</span></span>

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|<span data-ttu-id="aa6eb-107">Parámetro</span><span class="sxs-lookup"><span data-stu-id="aa6eb-107">Parameter</span></span>|<span data-ttu-id="aa6eb-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="aa6eb-108">Type</span></span>|<span data-ttu-id="aa6eb-109">Descripción</span><span class="sxs-lookup"><span data-stu-id="aa6eb-109">Description</span></span>|<span data-ttu-id="aa6eb-110">Valores posibles</span><span class="sxs-lookup"><span data-stu-id="aa6eb-110">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="aa6eb-111">-r</span><span class="sxs-lookup"><span data-stu-id="aa6eb-111">-r</span></span> |<span data-ttu-id="aa6eb-112">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="aa6eb-112">Mandatory</span></span>|<span data-ttu-id="aa6eb-113">Especifica si se debe instalar Mobility Service (MS) o debe instalarse MasterTarget(MT)</span><span class="sxs-lookup"><span data-stu-id="aa6eb-113">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="aa6eb-114">MS</span><span class="sxs-lookup"><span data-stu-id="aa6eb-114">MS</span></span> </br> <span data-ttu-id="aa6eb-115">MT</span><span class="sxs-lookup"><span data-stu-id="aa6eb-115">MT</span></span>|
|<span data-ttu-id="aa6eb-116">-d</span><span class="sxs-lookup"><span data-stu-id="aa6eb-116">-d</span></span> |<span data-ttu-id="aa6eb-117">Opcional</span><span class="sxs-lookup"><span data-stu-id="aa6eb-117">Optional</span></span>|<span data-ttu-id="aa6eb-118">Ubicación en que se instalará Mobility Service</span><span class="sxs-lookup"><span data-stu-id="aa6eb-118">Location where Mobility Service will be installed</span></span>|<span data-ttu-id="aa6eb-119">/usr/local/ASR</span><span class="sxs-lookup"><span data-stu-id="aa6eb-119">/usr/local/ASR</span></span>|
|<span data-ttu-id="aa6eb-120">-v</span><span class="sxs-lookup"><span data-stu-id="aa6eb-120">-v</span></span>|<span data-ttu-id="aa6eb-121">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="aa6eb-121">Mandatory</span></span>|<span data-ttu-id="aa6eb-122">Especifica la plataforma de hello en qué Hola se instala el servicio de movilidad</span><span class="sxs-lookup"><span data-stu-id="aa6eb-122">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="aa6eb-123">- **VMware**: utilice este valor si va a instalar Mobility Service en una máquina virtual que se ejecuta en *ESXi Hosts de VMware vSphere*, *Hosts de Hyper-V* y *servidores físicos*</span><span class="sxs-lookup"><span data-stu-id="aa6eb-123">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="aa6eb-124">- **Azure**: utilice este valor si va a instalar el agente en una máquina virtual de IaaS de Azure</span><span class="sxs-lookup"><span data-stu-id="aa6eb-124">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="aa6eb-125">VMware</span><span class="sxs-lookup"><span data-stu-id="aa6eb-125">VMware</span></span> </br> <span data-ttu-id="aa6eb-126">Las tablas de Azure</span><span class="sxs-lookup"><span data-stu-id="aa6eb-126">Azure</span></span>|
|<span data-ttu-id="aa6eb-127">-q</span><span class="sxs-lookup"><span data-stu-id="aa6eb-127">-q</span></span>|<span data-ttu-id="aa6eb-128">Opcional</span><span class="sxs-lookup"><span data-stu-id="aa6eb-128">Optional</span></span>|<span data-ttu-id="aa6eb-129">Especifica el instalador de toorun en modo silencioso</span><span class="sxs-lookup"><span data-stu-id="aa6eb-129">Specifies toorun installer in silent mode</span></span>| <span data-ttu-id="aa6eb-130">N/D</span><span class="sxs-lookup"><span data-stu-id="aa6eb-130">N/A</span></span>|


#### <a name="mobility-service-configuration-command-line"></a><span data-ttu-id="aa6eb-131">Línea de comandos de configuración de Mobility Service</span><span class="sxs-lookup"><span data-stu-id="aa6eb-131">Mobility Service configuration command-line</span></span>

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|<span data-ttu-id="aa6eb-132">Parámetro</span><span class="sxs-lookup"><span data-stu-id="aa6eb-132">Parameter</span></span>|<span data-ttu-id="aa6eb-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="aa6eb-133">Type</span></span>|<span data-ttu-id="aa6eb-134">Descripción</span><span class="sxs-lookup"><span data-stu-id="aa6eb-134">Description</span></span>|<span data-ttu-id="aa6eb-135">Valores posibles</span><span class="sxs-lookup"><span data-stu-id="aa6eb-135">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="aa6eb-136">-i</span><span class="sxs-lookup"><span data-stu-id="aa6eb-136">-i</span></span> |<span data-ttu-id="aa6eb-137">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="aa6eb-137">Mandatory</span></span>|<span data-ttu-id="aa6eb-138">Dirección IP del servidor de configuración de Hola</span><span class="sxs-lookup"><span data-stu-id="aa6eb-138">IP of hello Configuration Server</span></span>|<span data-ttu-id="aa6eb-139">Cualquier dirección IP válida</span><span class="sxs-lookup"><span data-stu-id="aa6eb-139">Any valid IP Address</span></span>|
|<span data-ttu-id="aa6eb-140">-P</span><span class="sxs-lookup"><span data-stu-id="aa6eb-140">-P</span></span> |<span data-ttu-id="aa6eb-141">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="aa6eb-141">Mandatory</span></span>|<span data-ttu-id="aa6eb-142">Archivo de hello de ruta de acceso completa al archivo donde se guarda la frase de contraseña de conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="aa6eb-142">Full file path hello file where hello connection passphrase is saved</span></span>|<span data-ttu-id="aa6eb-143">Cualquier carpeta válida</span><span class="sxs-lookup"><span data-stu-id="aa6eb-143">Any valid folder</span></span>|
