# <a name="make-a-remote-connection-to-a-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="2b7fb-101">Establecimiento de una conexión remota a un clúster de Kubernetes, DC/OS o Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="2b7fb-101">Make a remote connection to a Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="2b7fb-102">Después de crear un clúster de Azure Container Service, es preciso conectarse al clúster para implementar y administrar las cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-102">After creating an Azure Container Service cluster, you need to connect to the cluster to deploy and manage workloads.</span></span> <span data-ttu-id="2b7fb-103">En este artículo se describe cómo conectarse a la máquina virtual maestra del clúster desde un equipo remoto.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-103">This article describes how to connect to the master VM of the cluster from a remote computer.</span></span> 

<span data-ttu-id="2b7fb-104">Los clústeres de Kubernetes, DC/OS y Docker Swarm proporcionan los puntos de conexión de HTTP localmente.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-104">The Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="2b7fb-105">En el caso de Kubernetes, dicho punto de conexión se expone de forma segura en Internet y para acceder a él es preciso ejecutar la herramienta de línea de comandos `kubectl` desde cualquier equipo conectado a Internet.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-105">For Kubernetes, this endpoint is securely exposed on the internet, and you can access it by running the `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="2b7fb-106">Para DC/OS y Docker Swarm, se recomienda crear un túnel de shell seguro (SSH) desde el equipo local al sistema de administración del clúster.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer to the cluster management system.</span></span> <span data-ttu-id="2b7fb-107">Después de establecer el túnel, puede ejecutar comandos que utilizan los puntos de conexión HTTP y ver la interfaz de web de Orchestrator desde el sistema local.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-107">After the tunnel is established, you can run commands which use the HTTP endpoints and view the orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2b7fb-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2b7fb-108">Prerequisites</span></span>

* <span data-ttu-id="2b7fb-109">Un clúster de Kubernetes, DC/OS o Docker Swarm [implementado en Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="2b7fb-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="2b7fb-110">Archivo de clave privada RSA de SSH, correspondiente a la clave pública agregada al clúster durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-110">SSH RSA private key file, corresponding to the public key added to the cluster during deployment.</span></span> <span data-ttu-id="2b7fb-111">Estos comandos asumen que la clave privada SSH está en `$HOME/.ssh/id_rsa` en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-111">These commands assume that the private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="2b7fb-112">Para más información, consulte estas instrucciones para [macOS y Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) o [Windows](../articles/virtual-machines/linux/ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="2b7fb-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="2b7fb-113">Si la conexión SSH no funciona, es posible que tenga que [restablecer las claves SSH](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span><span class="sxs-lookup"><span data-stu-id="2b7fb-113">If the SSH connection isn't working, you may need to [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-to-a-kubernetes-cluster"></a><span data-ttu-id="2b7fb-114">Conexión a un clúster de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="2b7fb-114">Connect to a Kubernetes cluster</span></span>

<span data-ttu-id="2b7fb-115">Para instalar y configurar `kubectl` en el equipo, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-115">Follow these steps to install and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="2b7fb-116">En Linux o macOS, puede que tenga que ejecutar los comandos de esta sección mediante `sudo`.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-116">On Linux or macOS, you might need to run the commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="2b7fb-117">Instalación de kubectl</span><span class="sxs-lookup"><span data-stu-id="2b7fb-117">Install kubectl</span></span>
<span data-ttu-id="2b7fb-118">Una forma de instalar esta herramienta es usar la el comando `az acs kubernetes install-cli` de la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-118">One way to install this tool is to use the `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="2b7fb-119">Para ejecutar este comando, asegúrese de que [ha instalado](/cli/azure/install-az-cli2) la CLI de Azure 2.0 más reciente y que ha iniciado sesión en una cuenta de Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="2b7fb-119">To run this command, make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and logged in to an Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="2b7fb-120">Como alternativa, puede descargar el cliente `kubectl` más reciente directamente desde la [página de versiones de Kubernetes](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="2b7fb-120">Alternatively, you can download the latest `kubectl` client directly from the [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="2b7fb-121">Para más información, consulte [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (Instalación y configuración de kubectl).</span><span class="sxs-lookup"><span data-stu-id="2b7fb-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="2b7fb-122">Descarga de las credenciales del clúster</span><span class="sxs-lookup"><span data-stu-id="2b7fb-122">Download cluster credentials</span></span>
<span data-ttu-id="2b7fb-123">Una vez que tenga `kubectl` instalado, debe copiar las credenciales del clúster en la máquina.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-123">Once you have `kubectl` installed, you need to copy the cluster credentials to your machine.</span></span> <span data-ttu-id="2b7fb-124">Una manera de obtener las credenciales es usar el comando `az acs kubernetes get-credentials`.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-124">One way to do get the credentials is with the `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="2b7fb-125">Pase el nombre del grupo de recursos y el nombre del recurso del servicio de contenedor:</span><span class="sxs-lookup"><span data-stu-id="2b7fb-125">Pass the name of the resource group and the name of the container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="2b7fb-126">El comando descarga las credenciales del clúster en `$HOME/.kube/config`, donde `kubectl` espera que se encuentre.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-126">This command downloads the cluster credentials to `$HOME/.kube/config`, where `kubectl` expects it to be located.</span></span>

<span data-ttu-id="2b7fb-127">Como alternativa, puede usar `scp` para copiar de forma segura el archivo de `$HOME/.kube/config` en la máquina virtual maestra al equipo local.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-127">Alternatively, you can use `scp` to securely copy the file from `$HOME/.kube/config` on the master VM to your local machine.</span></span> <span data-ttu-id="2b7fb-128">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2b7fb-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="2b7fb-129">Si se encuentra en Windows, puede usar Bash en Ubuntu en Windows, el cliente de copia de archivos segura PuTTy o una herramienta similar.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-129">If you are on Windows, you can use Bash on Ubuntu on Windows, the PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="2b7fb-130">Uso de kubectl</span><span class="sxs-lookup"><span data-stu-id="2b7fb-130">Use kubectl</span></span>

<span data-ttu-id="2b7fb-131">Una vez que haya configurado `kubectl`, puede probar la conexión con una lista de los nodos del clúster:</span><span class="sxs-lookup"><span data-stu-id="2b7fb-131">Once you have `kubectl` configured, test the connection by listing the nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="2b7fb-132">Puede probar otros comandos `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="2b7fb-133">Por último, puede ver el panel de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-133">For example, you can view the Kubernetes Dashboard.</span></span> <span data-ttu-id="2b7fb-134">En primer lugar, ejecute un proxy al servidor de API de Kubernetes:</span><span class="sxs-lookup"><span data-stu-id="2b7fb-134">First, run a proxy to the Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="2b7fb-135">La interfaz de usuario de Kubernetes está disponible en: `http://localhost:8001/ui`.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-135">The Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="2b7fb-136">Para más información, consulte el [inicio rápido de Kubernetes](http://kubernetes.io/docs/user-guide/quick-start/).</span><span class="sxs-lookup"><span data-stu-id="2b7fb-136">For more information, see the [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-to-a-dcos-or-swarm-cluster"></a><span data-ttu-id="2b7fb-137">Conexión a un clúster de DC/OS o Swarm</span><span class="sxs-lookup"><span data-stu-id="2b7fb-137">Connect to a DC/OS or Swarm cluster</span></span>

<span data-ttu-id="2b7fb-138">Para usar los clústeres de DC/OS y Docker Swarm implementados mediante Azure Container Service, siga estas instrucciones para crear un túnel SSH desde su sistema local Linux, macOS o Windows.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-138">To use the DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions to create a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="2b7fb-139">Estas instrucciones se centran en la tunelización de tráfico TCP a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="2b7fb-140">También puede iniciar una sesión SSH interactiva con uno de los sistemas de administración del clúster interno, si bien esto no es recomendable.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-140">You can also start an interactive SSH session with one of the internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="2b7fb-141">Al trabajar directamente en un sistema interno, pueden producirse cambios en la configuración de manera involuntaria.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="2b7fb-142">Creación de un túnel de SSH en Linux o macOS</span><span class="sxs-lookup"><span data-stu-id="2b7fb-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="2b7fb-143">Lo primero que se hace al crear un túnel de SSH en Linux o macOS es buscar el nombre DNS público de los patrones de carga equilibrada.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-143">The first thing that you do when you create an SSH tunnel on Linux or macOS is to locate the public DNS name of the load-balanced masters.</span></span> <span data-ttu-id="2b7fb-144">Siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="2b7fb-144">Follow these steps:</span></span>


1. <span data-ttu-id="2b7fb-145">En [Azure Portal](https://portal.azure.com), desplácese el grupo de recursos que contiene el clúster del servicio de contenedor.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-145">In the [Azure portal](https://portal.azure.com), browse to the resource group containing your container service cluster.</span></span> <span data-ttu-id="2b7fb-146">Expanda el grupo de recursos de forma que se muestren todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-146">Expand the resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="2b7fb-147">Haga clic en el recurso **Azure Container Service** y, a continuación, haga clic en **Información general**.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-147">Click the **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="2b7fb-148">El **nombre de dominio completo del maestro** del clúster se muestra en **Información esencial**.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-148">The **Master FQDN** of the cluster appears under **Essentials**.</span></span> <span data-ttu-id="2b7fb-149">Guarde este nombre para usarlo más adelante.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-149">Save this name for later use.</span></span> 

    ![Nombre DNS público](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="2b7fb-151">También puede ejecutar el comando `az acs show` en el servicio del contenedor.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-151">Alternatively, run the `az acs show` command on your container service.</span></span> <span data-ttu-id="2b7fb-152">Busque la propiedad **Master Profile:fqdn** en el resultado del comando.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-152">Look for the **Master Profile:fqdn** property in the command output.</span></span>

3. <span data-ttu-id="2b7fb-153">Ahora, abra un shell y ejecute el comando `ssh` mediante la especificación de los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="2b7fb-153">Now open a shell and run the `ssh` command by specifying the following values:</span></span> 

    <span data-ttu-id="2b7fb-154">**LOCAL_PORT** es el puerto TCP en el servicio del túnel al que conectarse.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-154">**LOCAL_PORT** is the TCP port on the service side of the tunnel to connect to.</span></span> <span data-ttu-id="2b7fb-155">Para Swarm, establezca esta opción en 2375.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-155">For Swarm, set this to 2375.</span></span> <span data-ttu-id="2b7fb-156">Para DC/OS, establezca esta opción en 80.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-156">For DC/OS, set this to 80.</span></span> 
    <span data-ttu-id="2b7fb-157">**REMOTE_PORT** es el puerto del punto de conexión que desea exponer.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-157">**REMOTE_PORT** is the port of the endpoint that you want to expose.</span></span> <span data-ttu-id="2b7fb-158">Para Swarm, utilice el puerto 2375.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="2b7fb-159">Para DC/OS, utilice el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="2b7fb-160">**USERNAME** es el nombre de usuario que se especificó cuando se implementó el clúster.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-160">**USERNAME** is the user name that was provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="2b7fb-161">**DNSPREFIX** es el prefijo DNS que proporcionó al implementar el clúster.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-161">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="2b7fb-162">**REGION** es la región en la que está ubicado el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-162">**REGION** is the region in which your resource group is located.</span></span>  
    <span data-ttu-id="2b7fb-163">**PATH_TO_PRIVATE_KEY** [OPCIONAL] es la ruta de acceso a la clave privada correspondiente a la clave pública que proporcionó al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is the path to the private key that corresponds to the public key you provided when you created the cluster.</span></span> <span data-ttu-id="2b7fb-164">Esta opción se usa con la marca `-i`.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-164">Use this option with the `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="2b7fb-165">El puerto de conexión SSH es el 2200 y no el puerto 22 estándar.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-165">The SSH connection port is 2200 and not the standard port 22.</span></span> <span data-ttu-id="2b7fb-166">En un clúster con más de una máquina virtual maestra, éste es el puerto de conexión a la primera máquina virtual maestra.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-166">In a cluster with more than one master VM, this is the connection port to the first master VM.</span></span>
  > 

  <span data-ttu-id="2b7fb-167">El comando no genera ninguna salida.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-167">The command returns without output.</span></span>

<span data-ttu-id="2b7fb-168">En las secciones siguientes encontrar los ejemplos de DC/OS y Swarm.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-168">See the examples for DC/OS and Swarm in the following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="2b7fb-169">Túnel de DC/OS</span><span class="sxs-lookup"><span data-stu-id="2b7fb-169">DC/OS tunnel</span></span>
<span data-ttu-id="2b7fb-170">Para abrir un túnel para los puntos de conexión relacionados con DC/OS, ejecute un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="2b7fb-170">To open a tunnel for DC/OS endpoints, run a command like the following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="2b7fb-171">Asegúrese de que no haya otro proceso local enlazado al puerto 80.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="2b7fb-172">Si es necesario, puede especificar un puerto local distinto del 80, como el puerto 8080.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="2b7fb-173">Sin embargo, algunos vínculos de la interfaz de usuario web podrían no funcionar cuando se utiliza este puerto.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="2b7fb-174">Ahora puede acceder a los puntos de conexión de DC/OS desde el sistema local a través de las siguientes direcciones URL (suponiendo que se usa el puerto local 80):</span><span class="sxs-lookup"><span data-stu-id="2b7fb-174">You can now access the DC/OS endpoints from your local system through the following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="2b7fb-175">DC/OS: `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="2b7fb-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="2b7fb-176">Marathon: `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="2b7fb-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="2b7fb-177">Mesos: `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="2b7fb-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="2b7fb-178">De igual forma, se puede acceder a las API de REST de cada aplicación a través de este túnel.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-178">Similarly, you can reach the rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="2b7fb-179">Túnel de Swarm</span><span class="sxs-lookup"><span data-stu-id="2b7fb-179">Swarm tunnel</span></span>
<span data-ttu-id="2b7fb-180">Para abrir un túnel al punto de conexión relacionado con Swarm, ejecute un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="2b7fb-180">To open a tunnel to the Swarm endpoint, run a command like the following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="2b7fb-181">Asegúrese de que no haya otro proceso local enlazado al puerto 2375.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="2b7fb-182">Por ejemplo, si ejecuta localmente el demonio de Docker, está configurado para usar el puerto 2375 de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-182">For example, if you are running the Docker daemon locally, it's set by default to use port 2375.</span></span> <span data-ttu-id="2b7fb-183">Si es necesario, puede especificar un puerto local distinto al puerto 2375.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="2b7fb-184">Ahora puede tener acceso al clúster de Docker Swarm mediante la interfaz de línea de comandos de Docker (CLI de Docker) en el sistema local.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-184">Now you can access the Docker Swarm cluster using the Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="2b7fb-185">Para obtener las instrucciones de instalación, consulte [Install Docker](https://docs.docker.com/engine/installation/) (Instalación de Docker).</span><span class="sxs-lookup"><span data-stu-id="2b7fb-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="2b7fb-186">Establezca la variable de entorno DOCKER_HOST en el puerto local configurado para el túnel.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-186">Set your DOCKER_HOST environment variable to the local port you configured for the tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="2b7fb-187">Ejecute comandos de Docker que conectan por el túnel al clúster Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-187">Run Docker commands that tunnel to the Docker Swarm cluster.</span></span> <span data-ttu-id="2b7fb-188">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2b7fb-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="2b7fb-189">Creación de un túnel de SSH en Windows</span><span class="sxs-lookup"><span data-stu-id="2b7fb-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="2b7fb-190">Existen varias opciones para crear túneles de SSH en Windows.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="2b7fb-191">Si está ejecutando Bash en Ubuntu en Windows o una herramienta similar, puede seguir las instrucciones sobre túneles SSH mostradas anteriormente en este artículo para macOS y Linux.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow the SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="2b7fb-192">Como alternativa en Windows, esta sección describe cómo usar PuTTY para crear el túnel.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-192">As an alternative on Windows, this section describes how to use PuTTY to create the tunnel.</span></span>

1. <span data-ttu-id="2b7fb-193">[Descargue PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) en el sistema Windows.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to your Windows system.</span></span>

2. <span data-ttu-id="2b7fb-194">Ejecute la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-194">Run the application.</span></span>

3. <span data-ttu-id="2b7fb-195">Escriba un nombre de host que conste del nombre de usuario de administrador de clústeres y el nombre DNS público del primer patrón del clúster.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-195">Enter a host name that is comprised of the cluster admin user name and the public DNS name of the first master in the cluster.</span></span> <span data-ttu-id="2b7fb-196">El **nombre de host** es similar a `azureuser@PublicDNSName`.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-196">The **Host Name** looks similar to `azureuser@PublicDNSName`.</span></span> <span data-ttu-id="2b7fb-197">Escriba 2200 en el campo **Puerto**.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-197">Enter 2200 for the **Port**.</span></span>

    ![Configuración 1 de PuTTY](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="2b7fb-199">Seleccione **SSH > Auth** (SSL > Aut.).</span><span class="sxs-lookup"><span data-stu-id="2b7fb-199">Select **SSH > Auth**.</span></span> <span data-ttu-id="2b7fb-200">Agregue una ruta de acceso al archivo de claves privadas (en formato. ppk) para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-200">Add a path to your private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="2b7fb-201">Puede usar una herramienta como [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) para generar este archivo a partir de la clave SSH utilizada para crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-201">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to generate this file from the SSH key used to create the cluster.</span></span>

    ![Configuración 2 de PuTTY](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="2b7fb-203">Seleccione **SSH > Tunnels** (SSH > Túneles) y configure los siguientes puertos reenviados:</span><span class="sxs-lookup"><span data-stu-id="2b7fb-203">Select **SSH > Tunnels** and configure the following forwarded ports:</span></span>

    * <span data-ttu-id="2b7fb-204">**Puerto de origen:** use el 80 para DC/OS o el 2375 para Swarm.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-204">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="2b7fb-205">**Destino:** use localhost:80 para DC/OS o localhost:2375 para Swarm.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-205">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="2b7fb-206">En el siguiente ejemplo se configura para DC/OS, pero su aspecto sería similar para Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-206">The following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2b7fb-207">El puerto 80 no debe estar en uso cuando se cree este túnel.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-207">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![Configuración 3 de PuTTY](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="2b7fb-209">Cuando haya terminado, haga clic en **Session > Save** (Sesión > Guardar) para guardar la configuración de la conexión.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-209">When you're finished, click **Session > Save** to save the connection configuration.</span></span>

7. <span data-ttu-id="2b7fb-210">Para conectarse a la sesión de PuTTY, haga clic en **Open** (Abrir).</span><span class="sxs-lookup"><span data-stu-id="2b7fb-210">To connect to the PuTTY session, click **Open**.</span></span> <span data-ttu-id="2b7fb-211">Cuando se conecte, podrá ver la configuración del puerto en el registro de eventos de PuTTY.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-211">When you connect, you can see the port configuration in the PuTTY event log.</span></span>

    ![Registro de eventos de PuTTY](./media/container-service-connect/putty4.png)

<span data-ttu-id="2b7fb-213">Cuando haya configurado el túnel de DC/OS, podrá acceder a los puntos de conexión relacionados en:</span><span class="sxs-lookup"><span data-stu-id="2b7fb-213">After you've configured the tunnel for DC/OS, you can access the related endpoints at:</span></span>

* <span data-ttu-id="2b7fb-214">DC/OS: `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="2b7fb-214">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="2b7fb-215">Marathon: `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="2b7fb-215">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="2b7fb-216">Mesos: `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="2b7fb-216">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="2b7fb-217">Una vez que haya configurado el túnel de Docker Swarm, abra la configuración de Windows para configurar una variable de entorno de sistema denominada `DOCKER_HOST` con un valor de `:2375`.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-217">After you've configured the tunnel for Docker Swarm, open your Windows settings to configure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="2b7fb-218">Después, podrá acceder al clúster de Swarm a través de la CLI de Docker.</span><span class="sxs-lookup"><span data-stu-id="2b7fb-218">Then, you can access the Swarm cluster through the Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b7fb-219">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2b7fb-219">Next steps</span></span>
<span data-ttu-id="2b7fb-220">Implementar y administrar contenedores en un clúster:</span><span class="sxs-lookup"><span data-stu-id="2b7fb-220">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="2b7fb-221">Trabajo con Azure Container Service y Kubernetes</span><span class="sxs-lookup"><span data-stu-id="2b7fb-221">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="2b7fb-222">Administración de contenedores con la API de REST</span><span class="sxs-lookup"><span data-stu-id="2b7fb-222">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="2b7fb-223">Administración de contenedores con Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="2b7fb-223">Work with the Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

