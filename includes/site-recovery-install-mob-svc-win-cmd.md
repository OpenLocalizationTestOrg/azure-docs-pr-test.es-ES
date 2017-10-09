1. <span data-ttu-id="8300c-101">Copiar carpeta local de hello installer tooa (por ejemplo, C:\Temp) en servidores de Hola que desee que tooprotect.</span><span class="sxs-lookup"><span data-stu-id="8300c-101">Copy hello installer tooa local folder (for example, C:\Temp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="8300c-102">Ejecute hello después de comandos como administrador en un símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="8300c-102">Run hello following commands as an administrator at a command prompt:</span></span>

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. <span data-ttu-id="8300c-103">tooinstall servicio de movilidad, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="8300c-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. <span data-ttu-id="8300c-104">Ahora, agente de hello debe toobe registrado con el servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="8300c-104">Now hello agent needs toobe registered with hello Configuration Server.</span></span>

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a><span data-ttu-id="8300c-105">Argumentos de la línea de comandos del instalador de Mobility Service</span><span class="sxs-lookup"><span data-stu-id="8300c-105">Mobility Service installer command-line arguments</span></span>

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| <span data-ttu-id="8300c-106">Parámetro</span><span class="sxs-lookup"><span data-stu-id="8300c-106">Parameter</span></span>|<span data-ttu-id="8300c-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="8300c-107">Type</span></span>|<span data-ttu-id="8300c-108">Descripción</span><span class="sxs-lookup"><span data-stu-id="8300c-108">Description</span></span>|<span data-ttu-id="8300c-109">Valores posibles</span><span class="sxs-lookup"><span data-stu-id="8300c-109">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="8300c-110">/Role</span><span class="sxs-lookup"><span data-stu-id="8300c-110">/Role</span></span>|<span data-ttu-id="8300c-111">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8300c-111">Mandatory</span></span>|<span data-ttu-id="8300c-112">Especifica si se debe instalar Mobility Service (MS) o debe instalarse MasterTarget(MT)</span><span class="sxs-lookup"><span data-stu-id="8300c-112">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="8300c-113">MS</span><span class="sxs-lookup"><span data-stu-id="8300c-113">MS</span></span> </br> <span data-ttu-id="8300c-114">MT</span><span class="sxs-lookup"><span data-stu-id="8300c-114">MT</span></span>|
|<span data-ttu-id="8300c-115">/InstallLocation</span><span class="sxs-lookup"><span data-stu-id="8300c-115">/InstallLocation</span></span>|<span data-ttu-id="8300c-116">Opcional</span><span class="sxs-lookup"><span data-stu-id="8300c-116">Optional</span></span>|<span data-ttu-id="8300c-117">Ubicación en que se instala Mobility Service</span><span class="sxs-lookup"><span data-stu-id="8300c-117">Location where Mobility Service is installed</span></span>|<span data-ttu-id="8300c-118">Cualquier carpeta de equipo de Hola</span><span class="sxs-lookup"><span data-stu-id="8300c-118">Any folder on hello computer</span></span>|
|<span data-ttu-id="8300c-119">/Platform</span><span class="sxs-lookup"><span data-stu-id="8300c-119">/Platform</span></span>|<span data-ttu-id="8300c-120">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8300c-120">Mandatory</span></span>|<span data-ttu-id="8300c-121">Especifica la plataforma de hello en qué Hola se instala el servicio de movilidad</span><span class="sxs-lookup"><span data-stu-id="8300c-121">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="8300c-122">- **VMware**: utilice este valor si va a instalar Mobility Service en una máquina virtual que se ejecuta en *ESXi Hosts de VMware vSphere*, *Hosts de Hyper-V* y *servidores físicos*</span><span class="sxs-lookup"><span data-stu-id="8300c-122">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="8300c-123">- **Azure**: utilice este valor si va a instalar el agente en una máquina virtual de IaaS de Azure</span><span class="sxs-lookup"><span data-stu-id="8300c-123">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="8300c-124">VMware</span><span class="sxs-lookup"><span data-stu-id="8300c-124">VMware</span></span> </br> <span data-ttu-id="8300c-125">Las tablas de Azure</span><span class="sxs-lookup"><span data-stu-id="8300c-125">Azure</span></span>|
|<span data-ttu-id="8300c-126">/Silent</span><span class="sxs-lookup"><span data-stu-id="8300c-126">/Silent</span></span>|<span data-ttu-id="8300c-127">Opcional</span><span class="sxs-lookup"><span data-stu-id="8300c-127">Optional</span></span>|<span data-ttu-id="8300c-128">Especifica el instalador de hello toorun en modo silencioso</span><span class="sxs-lookup"><span data-stu-id="8300c-128">Specifies toorun hello installer in silent mode</span></span>| <span data-ttu-id="8300c-129">N/D</span><span class="sxs-lookup"><span data-stu-id="8300c-129">NA</span></span>|

>[!TIP]
> <span data-ttu-id="8300c-130">registros de instalación de Hello pueden encontrarse en %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span><span class="sxs-lookup"><span data-stu-id="8300c-130">hello setup logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span></span>

#### <a name="mobility-service-registration-command-line-arguments"></a><span data-ttu-id="8300c-131">Argumentos de la línea de comandos del registro de Mobility Service</span><span class="sxs-lookup"><span data-stu-id="8300c-131">Mobility Service registration command-line arguments</span></span>

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | <span data-ttu-id="8300c-132">Parámetro</span><span class="sxs-lookup"><span data-stu-id="8300c-132">Parameter</span></span>|<span data-ttu-id="8300c-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="8300c-133">Type</span></span>|<span data-ttu-id="8300c-134">Descripción</span><span class="sxs-lookup"><span data-stu-id="8300c-134">Description</span></span>|<span data-ttu-id="8300c-135">Valores posibles</span><span class="sxs-lookup"><span data-stu-id="8300c-135">Possible values</span></span>|
  |-|-|-|-|
  |<span data-ttu-id="8300c-136">/CSEndPoint</span><span class="sxs-lookup"><span data-stu-id="8300c-136">/CSEndPoint</span></span> |<span data-ttu-id="8300c-137">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8300c-137">Mandatory</span></span>|<span data-ttu-id="8300c-138">Dirección IP del servidor de configuración de Hola</span><span class="sxs-lookup"><span data-stu-id="8300c-138">IP address of hello configuration server</span></span>| <span data-ttu-id="8300c-139">Cualquier dirección IP válida</span><span class="sxs-lookup"><span data-stu-id="8300c-139">Any valid IP address</span></span>|
  |<span data-ttu-id="8300c-140">/PassphraseFilePath</span><span class="sxs-lookup"><span data-stu-id="8300c-140">/PassphraseFilePath</span></span>|<span data-ttu-id="8300c-141">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8300c-141">Mandatory</span></span>|<span data-ttu-id="8300c-142">Ubicación de frase de contraseña de Hola</span><span class="sxs-lookup"><span data-stu-id="8300c-142">Location of hello passphrase</span></span> |<span data-ttu-id="8300c-143">Cualquier ruta de acceso local o UNC válida</span><span class="sxs-lookup"><span data-stu-id="8300c-143">Any valid UNC or local file path</span></span>|


>[!TIP]
> <span data-ttu-id="8300c-144">Hola AgentConfiguration registros pueden encontrarse en %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span><span class="sxs-lookup"><span data-stu-id="8300c-144">hello AgentConfiguration logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span></span>
