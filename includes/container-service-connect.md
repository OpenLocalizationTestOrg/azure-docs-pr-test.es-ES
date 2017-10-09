# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="12c17-101">Realizar una conexión remota tooa Kubernetes, DC/OS o Docker Swarm Cluster Server</span><span class="sxs-lookup"><span data-stu-id="12c17-101">Make a remote connection tooa Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="12c17-102">Después de crear un clúster de servicio de contenedor de Azure, es necesario tooconnect toohello clúster toodeploy y administrar las cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="12c17-102">After creating an Azure Container Service cluster, you need tooconnect toohello cluster toodeploy and manage workloads.</span></span> <span data-ttu-id="12c17-103">Este artículo describe cómo tooconnect toohello master VM de hello de clúster desde un equipo remoto.</span><span class="sxs-lookup"><span data-stu-id="12c17-103">This article describes how tooconnect toohello master VM of hello cluster from a remote computer.</span></span> 

<span data-ttu-id="12c17-104">Hola Kubernetes, DC/OS, Docker Swarm clústeres y proporcionan extremos HTTP localmente.</span><span class="sxs-lookup"><span data-stu-id="12c17-104">hello Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="12c17-105">Para Kubernetes, este punto de conexión de forma segura se expone en Hola internet y puede tener acceso a él mediante la ejecución de hello `kubectl` herramienta de línea de comandos desde cualquier equipo conectado a internet.</span><span class="sxs-lookup"><span data-stu-id="12c17-105">For Kubernetes, this endpoint is securely exposed on hello internet, and you can access it by running hello `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="12c17-106">Para el controlador de dominio/OS y Docker Swarm, recomendamos que cree un túnel de shell seguro (SSH) desde el sistema de administración de clúster de toohello de equipo local.</span><span class="sxs-lookup"><span data-stu-id="12c17-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer toohello cluster management system.</span></span> <span data-ttu-id="12c17-107">Después de establece el túnel de hello, puede ejecutar comandos que utilizan los extremos HTTP de Hola e interfaz web de vista Hola orchestrator (si está disponible) desde el sistema local.</span><span class="sxs-lookup"><span data-stu-id="12c17-107">After hello tunnel is established, you can run commands which use hello HTTP endpoints and view hello orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="12c17-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="12c17-108">Prerequisites</span></span>

* <span data-ttu-id="12c17-109">Un clúster de Kubernetes, DC/OS o Docker Swarm [implementado en Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="12c17-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="12c17-110">SSH RSA archivo de clave privada correspondiente toohello toohello agregada de clave pública clúster durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="12c17-110">SSH RSA private key file, corresponding toohello public key added toohello cluster during deployment.</span></span> <span data-ttu-id="12c17-111">Estos comandos dan por hecho es clave SSH privada hello en `$HOME/.ssh/id_rsa` en el equipo.</span><span class="sxs-lookup"><span data-stu-id="12c17-111">These commands assume that hello private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="12c17-112">Para más información, consulte estas instrucciones para [macOS y Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) o [Windows](../articles/virtual-machines/linux/ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="12c17-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="12c17-113">Si Hola conexión SSH no funciona, puede que tenga demasiado [restablecer las claves SSH](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span><span class="sxs-lookup"><span data-stu-id="12c17-113">If hello SSH connection isn't working, you may need too [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-tooa-kubernetes-cluster"></a><span data-ttu-id="12c17-114">Conectar tooa Kubernetes clúster</span><span class="sxs-lookup"><span data-stu-id="12c17-114">Connect tooa Kubernetes cluster</span></span>

<span data-ttu-id="12c17-115">Siga estos pasos tooinstall y configurar `kubectl` en el equipo.</span><span class="sxs-lookup"><span data-stu-id="12c17-115">Follow these steps tooinstall and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="12c17-116">En Linux o Mac OS, podría necesitar toorun comandos de hello en esta sección utilizando `sudo`.</span><span class="sxs-lookup"><span data-stu-id="12c17-116">On Linux or macOS, you might need toorun hello commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="12c17-117">Instalación de kubectl</span><span class="sxs-lookup"><span data-stu-id="12c17-117">Install kubectl</span></span>
<span data-ttu-id="12c17-118">Una manera de tooinstall esta herramienta es hello toouse `az acs kubernetes install-cli` comando de CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="12c17-118">One way tooinstall this tool is toouse hello `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="12c17-119">toorun este comando, asegúrese de que se [instalado](/cli/azure/install-az-cli2) Hola 2.0 más reciente de CLI de Azure y registran en tooan cuenta de Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="12c17-119">toorun this command, make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="12c17-120">Como alternativa, puede descargar hello más reciente `kubectl` cliente directamente desde hello [Kubernetes libera página](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="12c17-120">Alternatively, you can download hello latest `kubectl` client directly from hello [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="12c17-121">Para más información, consulte [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (Instalación y configuración de kubectl).</span><span class="sxs-lookup"><span data-stu-id="12c17-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="12c17-122">Descarga de las credenciales del clúster</span><span class="sxs-lookup"><span data-stu-id="12c17-122">Download cluster credentials</span></span>
<span data-ttu-id="12c17-123">Una vez que tenga `kubectl` instalado, es necesario que los equipos del tooyour toocopy Hola clúster credenciales.</span><span class="sxs-lookup"><span data-stu-id="12c17-123">Once you have `kubectl` installed, you need toocopy hello cluster credentials tooyour machine.</span></span> <span data-ttu-id="12c17-124">Las credenciales de una manera toodo get hello es con hello `az acs kubernetes get-credentials` comando.</span><span class="sxs-lookup"><span data-stu-id="12c17-124">One way toodo get hello credentials is with hello `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="12c17-125">Pase el nombre de Hola Hola del grupo de recursos y nombre hello del recurso de servicio de contenedor de hello:</span><span class="sxs-lookup"><span data-stu-id="12c17-125">Pass hello name of hello resource group and hello name of hello container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="12c17-126">Este comando descarga las credenciales del clúster Hola demasiado`$HOME/.kube/config`, donde `kubectl` espera toobe encuentra.</span><span class="sxs-lookup"><span data-stu-id="12c17-126">This command downloads hello cluster credentials too`$HOME/.kube/config`, where `kubectl` expects it toobe located.</span></span>

<span data-ttu-id="12c17-127">Como alternativa, puede usar `scp` toosecurely archivo de hello de copia de `$HOME/.kube/config` en el equipo local de hello maestro VM tooyour.</span><span class="sxs-lookup"><span data-stu-id="12c17-127">Alternatively, you can use `scp` toosecurely copy hello file from `$HOME/.kube/config` on hello master VM tooyour local machine.</span></span> <span data-ttu-id="12c17-128">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="12c17-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="12c17-129">Si se encuentra en Windows, puede usar Bash en Ubuntu en Windows, el cliente de copia de archivo seguro PuTTy de Hola o una herramienta similar.</span><span class="sxs-lookup"><span data-stu-id="12c17-129">If you are on Windows, you can use Bash on Ubuntu on Windows, hello PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="12c17-130">Uso de kubectl</span><span class="sxs-lookup"><span data-stu-id="12c17-130">Use kubectl</span></span>

<span data-ttu-id="12c17-131">Una vez que tenga `kubectl` configurado, probar la conexión de hello haciendo una lista de nodos de hello en el clúster:</span><span class="sxs-lookup"><span data-stu-id="12c17-131">Once you have `kubectl` configured, test hello connection by listing hello nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="12c17-132">Puede probar otros comandos `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="12c17-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="12c17-133">Por ejemplo, puede ver hello Kubernetes panel.</span><span class="sxs-lookup"><span data-stu-id="12c17-133">For example, you can view hello Kubernetes Dashboard.</span></span> <span data-ttu-id="12c17-134">En primer lugar, ejecute a un proxy de servidor de la API de Kubernetes toohello:</span><span class="sxs-lookup"><span data-stu-id="12c17-134">First, run a proxy toohello Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="12c17-135">Hello Kubernetes UI está ahora disponible en: `http://localhost:8001/ui`.</span><span class="sxs-lookup"><span data-stu-id="12c17-135">hello Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="12c17-136">Para obtener más información, vea hello [inicio rápido de Kubernetes](http://kubernetes.io/docs/user-guide/quick-start/).</span><span class="sxs-lookup"><span data-stu-id="12c17-136">For more information, see hello [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-tooa-dcos-or-swarm-cluster"></a><span data-ttu-id="12c17-137">Conectar el clúster de DC/OS o conjunto de tooa</span><span class="sxs-lookup"><span data-stu-id="12c17-137">Connect tooa DC/OS or Swarm cluster</span></span>

<span data-ttu-id="12c17-138">Hola toouse DC/OS y clústeres de Docker Swarm implementados por el servicio de contenedor de Azure, siga estas toocreate instrucciones un túnel SSH de su sistema local de Linux, Mac OS o Windows.</span><span class="sxs-lookup"><span data-stu-id="12c17-138">toouse hello DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions toocreate a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="12c17-139">Estas instrucciones se centran en la tunelización de tráfico TCP a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="12c17-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="12c17-140">También puede iniciar una sesión interactiva de SSH con uno de los sistemas de administración de hello interna en el clúster, pero no se recomienda esto.</span><span class="sxs-lookup"><span data-stu-id="12c17-140">You can also start an interactive SSH session with one of hello internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="12c17-141">Al trabajar directamente en un sistema interno, pueden producirse cambios en la configuración de manera involuntaria.</span><span class="sxs-lookup"><span data-stu-id="12c17-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="12c17-142">Creación de un túnel de SSH en Linux o macOS</span><span class="sxs-lookup"><span data-stu-id="12c17-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="12c17-143">Hola primera cosa que se realiza al crear un túnel SSH en Linux o Mac OS es nombre DNS toolocate Hola público de patrones de carga equilibrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c17-143">hello first thing that you do when you create an SSH tunnel on Linux or macOS is toolocate hello public DNS name of hello load-balanced masters.</span></span> <span data-ttu-id="12c17-144">Siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="12c17-144">Follow these steps:</span></span>


1. <span data-ttu-id="12c17-145">Hola [portal de Azure](https://portal.azure.com), busque el grupo de recursos de toohello que contiene el clúster del servicio de contenedor.</span><span class="sxs-lookup"><span data-stu-id="12c17-145">In hello [Azure portal](https://portal.azure.com), browse toohello resource group containing your container service cluster.</span></span> <span data-ttu-id="12c17-146">Expanda el grupo de recursos de Hola para que se muestre cada recurso.</span><span class="sxs-lookup"><span data-stu-id="12c17-146">Expand hello resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="12c17-147">Haga clic en hello **servicio de contenedor** recurso y haga clic en **Introducción**.</span><span class="sxs-lookup"><span data-stu-id="12c17-147">Click hello **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="12c17-148">Hola **Master FQDN** de hello clúster aparece bajo **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="12c17-148">hello **Master FQDN** of hello cluster appears under **Essentials**.</span></span> <span data-ttu-id="12c17-149">Guarde este nombre para usarlo más adelante.</span><span class="sxs-lookup"><span data-stu-id="12c17-149">Save this name for later use.</span></span> 

    ![Nombre DNS público](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="12c17-151">O bien, ejecute hello `az acs show` comando en su servicio de contenedor.</span><span class="sxs-lookup"><span data-stu-id="12c17-151">Alternatively, run hello `az acs show` command on your container service.</span></span> <span data-ttu-id="12c17-152">Busque hello **Master perfil: fqdn** propiedad en la salida del comando Hola.</span><span class="sxs-lookup"><span data-stu-id="12c17-152">Look for hello **Master Profile:fqdn** property in hello command output.</span></span>

3. <span data-ttu-id="12c17-153">Ahora, abra un shell y ejecute hello `ssh` comando especificando Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="12c17-153">Now open a shell and run hello `ssh` command by specifying hello following values:</span></span> 

    <span data-ttu-id="12c17-154">**LOCAL_PORT** es Hola el puerto TCP en lado de servicio de Hola de hello túnel tooconnect a.</span><span class="sxs-lookup"><span data-stu-id="12c17-154">**LOCAL_PORT** is hello TCP port on hello service side of hello tunnel tooconnect to.</span></span> <span data-ttu-id="12c17-155">Para el conjunto, establezca este too2375.</span><span class="sxs-lookup"><span data-stu-id="12c17-155">For Swarm, set this too2375.</span></span> <span data-ttu-id="12c17-156">Para el controlador de dominio/OS, establezca este too80.</span><span class="sxs-lookup"><span data-stu-id="12c17-156">For DC/OS, set this too80.</span></span> 
    <span data-ttu-id="12c17-157">**REMOTE_PORT** es el puerto de Hola de punto de conexión de Hola que desea tooexpose.</span><span class="sxs-lookup"><span data-stu-id="12c17-157">**REMOTE_PORT** is hello port of hello endpoint that you want tooexpose.</span></span> <span data-ttu-id="12c17-158">Para Swarm, utilice el puerto 2375.</span><span class="sxs-lookup"><span data-stu-id="12c17-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="12c17-159">Para DC/OS, utilice el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="12c17-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="12c17-160">**Nombre de usuario** es nombre de usuario de Hola que ha proporcionado al implementar el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c17-160">**USERNAME** is hello user name that was provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="12c17-161">**DNSPREFIX** es Hola prefijo DNS que proporcionó al implementar el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c17-161">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="12c17-162">**REGIÓN** es región hello en el que se encuentra el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="12c17-162">**REGION** is hello region in which your resource group is located.</span></span>  
    <span data-ttu-id="12c17-163">**PATH_TO_PRIVATE_KEY** [opcional] es Hola ruta de acceso toohello clave privada correspondiente clave pública toohello que proporcionó al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c17-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is hello path toohello private key that corresponds toohello public key you provided when you created hello cluster.</span></span> <span data-ttu-id="12c17-164">Utilice esta opción con hello `-i` marca.</span><span class="sxs-lookup"><span data-stu-id="12c17-164">Use this option with hello `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="12c17-165">Hola puerto de conexión de SSH es 2200 y no Hola puerto estándar 22.</span><span class="sxs-lookup"><span data-stu-id="12c17-165">hello SSH connection port is 2200 and not hello standard port 22.</span></span> <span data-ttu-id="12c17-166">En un clúster con más de una máquina virtual principal, se trata de hello conexión puerto toohello primer patrón de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="12c17-166">In a cluster with more than one master VM, this is hello connection port toohello first master VM.</span></span>
  > 

  <span data-ttu-id="12c17-167">comando de Hello devuelve sin salida.</span><span class="sxs-lookup"><span data-stu-id="12c17-167">hello command returns without output.</span></span>

<span data-ttu-id="12c17-168">Ver ejemplos de hello para DC/OS y conjunto de hello las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="12c17-168">See hello examples for DC/OS and Swarm in hello following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="12c17-169">Túnel de DC/OS</span><span class="sxs-lookup"><span data-stu-id="12c17-169">DC/OS tunnel</span></span>
<span data-ttu-id="12c17-170">tooopen un túnel para los puntos de conexión de controlador de dominio/OS, ejecute un comando como Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="12c17-170">tooopen a tunnel for DC/OS endpoints, run a command like hello following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="12c17-171">Asegúrese de que no haya otro proceso local enlazado al puerto 80.</span><span class="sxs-lookup"><span data-stu-id="12c17-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="12c17-172">Si es necesario, puede especificar un puerto local distinto del 80, como el puerto 8080.</span><span class="sxs-lookup"><span data-stu-id="12c17-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="12c17-173">Sin embargo, algunos vínculos de la interfaz de usuario web podrían no funcionar cuando se utiliza este puerto.</span><span class="sxs-lookup"><span data-stu-id="12c17-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="12c17-174">Ahora puede acceder a los puntos de conexión de Hola DC/OS desde el sistema local a través de hello las siguientes direcciones URL (suponiendo que el puerto local 80):</span><span class="sxs-lookup"><span data-stu-id="12c17-174">You can now access hello DC/OS endpoints from your local system through hello following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="12c17-175">DC/OS: `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="12c17-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="12c17-176">Marathon: `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="12c17-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="12c17-177">Mesos: `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="12c17-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="12c17-178">De forma similar, puede llegar a API de rest de Hola para cada aplicación a través de este túnel.</span><span class="sxs-lookup"><span data-stu-id="12c17-178">Similarly, you can reach hello rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="12c17-179">Túnel de Swarm</span><span class="sxs-lookup"><span data-stu-id="12c17-179">Swarm tunnel</span></span>
<span data-ttu-id="12c17-180">tooopen un punto de conexión de túnel toohello conjunto, al ejecutar un comando como Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="12c17-180">tooopen a tunnel toohello Swarm endpoint, run a command like hello following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="12c17-181">Asegúrese de que no haya otro proceso local enlazado al puerto 2375.</span><span class="sxs-lookup"><span data-stu-id="12c17-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="12c17-182">Por ejemplo, si se ejecuta el demonio de Docker Hola localmente, se establece por toouse puerto 2375.</span><span class="sxs-lookup"><span data-stu-id="12c17-182">For example, if you are running hello Docker daemon locally, it's set by default toouse port 2375.</span></span> <span data-ttu-id="12c17-183">Si es necesario, puede especificar un puerto local distinto al puerto 2375.</span><span class="sxs-lookup"><span data-stu-id="12c17-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="12c17-184">Ahora puede acceder mediante la interfaz de línea de comandos de Docker de hello (CLI de Docker) en el sistema local de clúster Docker Swarm Hola.</span><span class="sxs-lookup"><span data-stu-id="12c17-184">Now you can access hello Docker Swarm cluster using hello Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="12c17-185">Para obtener las instrucciones de instalación, consulte [Install Docker](https://docs.docker.com/engine/installation/) (Instalación de Docker).</span><span class="sxs-lookup"><span data-stu-id="12c17-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="12c17-186">Establecer el toohello de variable de entorno DOCKER_HOST puerto local que ha configurado para el túnel de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c17-186">Set your DOCKER_HOST environment variable toohello local port you configured for hello tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="12c17-187">Ejecute comandos de Docker ese clúster de Docker Swarm toohello de túnel.</span><span class="sxs-lookup"><span data-stu-id="12c17-187">Run Docker commands that tunnel toohello Docker Swarm cluster.</span></span> <span data-ttu-id="12c17-188">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="12c17-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="12c17-189">Creación de un túnel de SSH en Windows</span><span class="sxs-lookup"><span data-stu-id="12c17-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="12c17-190">Existen varias opciones para crear túneles de SSH en Windows.</span><span class="sxs-lookup"><span data-stu-id="12c17-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="12c17-191">Si está ejecutando Bash en Ubuntu en Windows o una herramienta similar, puede seguir instrucciones túneles SSH de hello, que se explicó anteriormente en este artículo para macOS y Linux.</span><span class="sxs-lookup"><span data-stu-id="12c17-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow hello SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="12c17-192">Como alternativa en Windows, esta sección se describe cómo túnel de toouse toocreate PuTTY Hola.</span><span class="sxs-lookup"><span data-stu-id="12c17-192">As an alternative on Windows, this section describes how toouse PuTTY toocreate hello tunnel.</span></span>

1. <span data-ttu-id="12c17-193">[Descargar PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour sistema de Windows.</span><span class="sxs-lookup"><span data-stu-id="12c17-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour Windows system.</span></span>

2. <span data-ttu-id="12c17-194">Ejecute la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="12c17-194">Run hello application.</span></span>

3. <span data-ttu-id="12c17-195">Escriba un nombre de host que se compone del nombre de usuario de administrador de clúster de Hola y Hola de nombre DNS público del primer patrón de hello en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c17-195">Enter a host name that is comprised of hello cluster admin user name and hello public DNS name of hello first master in hello cluster.</span></span> <span data-ttu-id="12c17-196">Hola **nombre de Host** parece demasiado`azureuser@PublicDNSName`.</span><span class="sxs-lookup"><span data-stu-id="12c17-196">hello **Host Name** looks similar too`azureuser@PublicDNSName`.</span></span> <span data-ttu-id="12c17-197">Escriba 2200 de hello **puerto**.</span><span class="sxs-lookup"><span data-stu-id="12c17-197">Enter 2200 for hello **Port**.</span></span>

    ![Configuración 1 de PuTTY](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="12c17-199">Seleccione **SSH > Auth** (SSL > Aut.). Agregue un ruta de acceso tooyour archivo de clave privada (en formato. ppk) para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="12c17-199">Select **SSH > Auth**. Add a path tooyour private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="12c17-200">Puede usar una herramienta como [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate este archivo de Hola clúster de hello toocreate usa claves de SSH.</span><span class="sxs-lookup"><span data-stu-id="12c17-200">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate this file from hello SSH key used toocreate hello cluster.</span></span>

    ![Configuración 2 de PuTTY](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="12c17-202">Seleccione **SSH > túneles** y configure siguiente Hola reenviados puertos:</span><span class="sxs-lookup"><span data-stu-id="12c17-202">Select **SSH > Tunnels** and configure hello following forwarded ports:</span></span>

    * <span data-ttu-id="12c17-203">**Puerto de origen:** use el 80 para DC/OS o el 2375 para Swarm.</span><span class="sxs-lookup"><span data-stu-id="12c17-203">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="12c17-204">**Destino:** use localhost:80 para DC/OS o localhost:2375 para Swarm.</span><span class="sxs-lookup"><span data-stu-id="12c17-204">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="12c17-205">Hola siguiente ejemplo se configura para DC/OS, pero tendrá un aspecto similar para Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="12c17-205">hello following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="12c17-206">El puerto 80 no debe estar en uso cuando se cree este túnel.</span><span class="sxs-lookup"><span data-stu-id="12c17-206">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![Configuración 3 de PuTTY](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="12c17-208">Cuando haya terminado, haga clic en **sesión > Guardar** configuración de conexión de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="12c17-208">When you're finished, click **Session > Save** toosave hello connection configuration.</span></span>

7. <span data-ttu-id="12c17-209">tooconnect toohello PuTTY de sesión, haga clic en **abiertos**.</span><span class="sxs-lookup"><span data-stu-id="12c17-209">tooconnect toohello PuTTY session, click **Open**.</span></span> <span data-ttu-id="12c17-210">Cuando se conecta, puede ver la configuración del puerto de hello en el registro de eventos PuTTY de Hola.</span><span class="sxs-lookup"><span data-stu-id="12c17-210">When you connect, you can see hello port configuration in hello PuTTY event log.</span></span>

    ![Registro de eventos de PuTTY](./media/container-service-connect/putty4.png)

<span data-ttu-id="12c17-212">Después de configurar el túnel de Hola para DC/OS, puede tener acceso a Hola relacionados con puntos de conexión en:</span><span class="sxs-lookup"><span data-stu-id="12c17-212">After you've configured hello tunnel for DC/OS, you can access hello related endpoints at:</span></span>

* <span data-ttu-id="12c17-213">DC/OS: `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="12c17-213">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="12c17-214">Marathon: `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="12c17-214">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="12c17-215">Mesos: `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="12c17-215">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="12c17-216">Después de configurar el túnel de Hola para Docker Swarm, abra su tooconfigure de configuración de Windows una variable de entorno de sistema denominada `DOCKER_HOST` con un valor de `:2375`.</span><span class="sxs-lookup"><span data-stu-id="12c17-216">After you've configured hello tunnel for Docker Swarm, open your Windows settings tooconfigure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="12c17-217">A continuación, puede tener acceso a clúster de conjunto de Hola a través de hello CLI de Docker.</span><span class="sxs-lookup"><span data-stu-id="12c17-217">Then, you can access hello Swarm cluster through hello Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12c17-218">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="12c17-218">Next steps</span></span>
<span data-ttu-id="12c17-219">Implementar y administrar contenedores en un clúster:</span><span class="sxs-lookup"><span data-stu-id="12c17-219">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="12c17-220">Trabajo con Azure Container Service y Kubernetes</span><span class="sxs-lookup"><span data-stu-id="12c17-220">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="12c17-221">Administración de contenedores con la API de REST</span><span class="sxs-lookup"><span data-stu-id="12c17-221">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="12c17-222">Trabajar con Docker Swarm y de saludo servicio de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="12c17-222">Work with hello Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

