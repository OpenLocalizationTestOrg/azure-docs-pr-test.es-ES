
* [<span data-ttu-id="f7486-101">Creación rápida de una máquina virtual en Azure</span><span class="sxs-lookup"><span data-stu-id="f7486-101">Quick-create a virtual machine in Azure</span></span>](#quick-create-a-vm-in-azure)
* [<span data-ttu-id="f7486-102">Implementación de una máquina virtual en Azure desde una plantilla</span><span class="sxs-lookup"><span data-stu-id="f7486-102">Deploy a virtual machine in Azure from a template</span></span>](#deploy-a-vm-in-azure-from-a-template)
* [<span data-ttu-id="f7486-103">Creación de una máquina virtual desde una imagen personalizada</span><span class="sxs-lookup"><span data-stu-id="f7486-103">Create a virtual machine from a custom image</span></span>](#create-a-custom-vm-image)
* [<span data-ttu-id="f7486-104">Implementación de una máquina virtual que usa una red virtual y un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="f7486-104">Deploy a virtual machine that uses a virtual network and a load balancer</span></span>](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [<span data-ttu-id="f7486-105">Eliminación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f7486-105">Remove a resource group</span></span>](#remove-a-resource-group)
* [<span data-ttu-id="f7486-106">Mostrar el registro de hello para una implementación de grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f7486-106">Show hello log for a resource group deployment</span></span>](#show-the-log-for-a-resource-group-deployment)
* [<span data-ttu-id="f7486-107">Visualización de información acerca de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="f7486-107">Display information about a virtual machine</span></span>](#display-information-about-a-virtual-machine)
* [<span data-ttu-id="f7486-108">Conectar máquina virtual basadas en Linux de tooa</span><span class="sxs-lookup"><span data-stu-id="f7486-108">Connect tooa Linux-based virtual machine</span></span>](#log-on-to-a-linux-based-virtual-machine)
* [<span data-ttu-id="f7486-109">Detención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="f7486-109">Stop a virtual machine</span></span>](#stop-a-virtual-machine)
* [<span data-ttu-id="f7486-110">Inicio de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="f7486-110">Start a virtual machine</span></span>](#start-a-virtual-machine)
* [<span data-ttu-id="f7486-111">Acoplamiento de un disco de datos</span><span class="sxs-lookup"><span data-stu-id="f7486-111">Attach a data disk</span></span>](#attach-a-data-disk)

## <a name="getting-ready"></a><span data-ttu-id="f7486-112">Preparación</span><span class="sxs-lookup"><span data-stu-id="f7486-112">Getting ready</span></span>
<span data-ttu-id="f7486-113">Para poder usar Hola CLI de Azure con grupos de recursos de Azure, necesitará versión de CLI de Azure correcta de toohave hello y una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="f7486-113">Before you can use hello Azure CLI with Azure resource groups, you need toohave hello right Azure CLI version and an Azure account.</span></span> <span data-ttu-id="f7486-114">Si no tienes Hola CLI de Azure, [instalarlo](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f7486-114">If you don't have hello Azure CLI, [install it](../articles/cli-install-nodejs.md).</span></span>

### <a name="update-your-azure-cli-version-too090-or-later"></a><span data-ttu-id="f7486-115">Actualizar su too0.9.0 de versión de CLI de Azure o posterior</span><span class="sxs-lookup"><span data-stu-id="f7486-115">Update your Azure CLI version too0.9.0 or later</span></span>
<span data-ttu-id="f7486-116">Tipo `azure --version` toosee si ya ha instalado la versión 0.9.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="f7486-116">Type `azure --version` toosee whether you have already installed version 0.9.0 or later.</span></span>

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

<span data-ttu-id="f7486-117">Si su versión no es 0.9.0 o una versión posterior, debe tooupdate mediante uno de Hola instaladores nativo o a través **npm** escribiendo `npm update -g azure-cli`.</span><span class="sxs-lookup"><span data-stu-id="f7486-117">If your version is not 0.9.0 or later, you need tooupdate it by using one of hello native installers or through **npm** by typing `npm update -g azure-cli`.</span></span>

<span data-ttu-id="f7486-118">También puede ejecutar CLI de Azure como un contenedor de Docker mediante Hola siguiente [imagen de Docker](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span><span class="sxs-lookup"><span data-stu-id="f7486-118">You can also run Azure CLI as a Docker container by using hello following [Docker image](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span></span> <span data-ttu-id="f7486-119">Desde un host Docker, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f7486-119">From a Docker host, run hello following command:</span></span>

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="f7486-120">Definición de su cuenta y suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="f7486-120">Set your Azure account and subscription</span></span>
<span data-ttu-id="f7486-121">Si aún no tiene una suscripción de Azure pero tiene una suscripción a MSDN, puede activar sus [beneficios de suscripción a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="f7486-121">If you don't already have an Azure subscription but you do have an MSDN subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="f7486-122">O puede suscribirse a una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f7486-122">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="f7486-123">Ahora [iniciar de forma interactiva en tooyour cuenta de Azure](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) escribiendo `azure login` y siguiendo las indicaciones de Hola para un tooyour de experiencia de inicio de sesión interactivo cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="f7486-123">Now [log in tooyour Azure account interactively](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) by typing `azure login` and following hello prompts for an interactive login experience tooyour Azure account.</span></span> 

> [!NOTE]
> <span data-ttu-id="f7486-124">Si dispone de un trabajo o escuela Id. y sabe no tiene habilitada la autenticación de dos factores, puede **también** usar `azure login -u` junto con hello profesionales o educativas toolog de Id. de *sin* una sesión interactiva.</span><span class="sxs-lookup"><span data-stu-id="f7486-124">If you have a work or school ID and you know you do not have two-factor authentication enabled, you can **also** use `azure login -u` along with hello work or school ID toolog in *without* an interactive session.</span></span> <span data-ttu-id="f7486-125">Si no hay un trabajo o escuela Id., puede [crear un identificador de trabajo o escuela de tu cuenta Microsoft personal](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog Hola igual.</span><span class="sxs-lookup"><span data-stu-id="f7486-125">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog in hello same way.</span></span>
>
>

<span data-ttu-id="f7486-126">La cuenta puede tener más de una suscripción.</span><span class="sxs-lookup"><span data-stu-id="f7486-126">Your account may have more than one subscription.</span></span> <span data-ttu-id="f7486-127">Puede enumerar las suscripciones escribiendo `azure account list`, que podría ser algo similar a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f7486-127">You can list your subscriptions by typing `azure account list`, which might look something like this:</span></span>

```azurecli
azure account list
info:    Executing command account list
data:    Name                              Id                                    Tenant Id                            Current
data:    --------------------------------  ------------------------------------  ------------------------------------  -------
data:    Contoso Admin                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  true
data:    Fabrikam dev                      xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Fabrikam test                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Contoso production                xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
```

<span data-ttu-id="f7486-128">Puede establecer la suscripción actual de Azure Hola escribiendo Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="f7486-128">You can set hello current Azure subscription by typing hello following.</span></span> <span data-ttu-id="f7486-129">Utilice Hola Hola o nombre de Id. de suscripción que tenga recursos de Hola que desee toomanage.</span><span class="sxs-lookup"><span data-stu-id="f7486-129">Use hello subscription name or hello ID that has hello resources you want toomanage.</span></span>

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-toohello-azure-cli-resource-group-mode"></a><span data-ttu-id="f7486-130">Cambiar el modo de grupo de recursos de toohello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="f7486-130">Switch toohello Azure CLI resource group mode</span></span>
<span data-ttu-id="f7486-131">De forma predeterminada, se inicia en modo de administración de servicio de Hola Hola CLI de Azure (**asm** modo).</span><span class="sxs-lookup"><span data-stu-id="f7486-131">By default, hello Azure CLI starts in hello service management mode (**asm** mode).</span></span> <span data-ttu-id="f7486-132">Escriba Hola después tooswitch tooresource el modo de grupo.</span><span class="sxs-lookup"><span data-stu-id="f7486-132">Type hello following tooswitch tooresource group mode.</span></span>

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a><span data-ttu-id="f7486-133">Descripción de las plantillas de recursos y grupos de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="f7486-133">Understanding Azure resource templates and resource groups</span></span>
<span data-ttu-id="f7486-134">La mayoría de las aplicaciones se desarrollan a partir de una combinación de tipos de recursos diferentes (por ejemplo, una o varias máquinas virtuales y cuentas de almacenamiento, una Base de datos SQL, una red virtual o una red de entrega de contenido).</span><span class="sxs-lookup"><span data-stu-id="f7486-134">Most applications are built from a combination of different resource types (such as one or more VMs and storage accounts, a SQL database, a virtual network, or a content delivery network).</span></span> <span data-ttu-id="f7486-135">Hola API de administración de servicios de Azure de forma predeterminada y hello portal de Azure clásico representa estos elementos mediante un enfoque de servicio por servicio.</span><span class="sxs-lookup"><span data-stu-id="f7486-135">hello default Azure service management API and hello Azure classic portal represented these items by using a service-by-service approach.</span></span> <span data-ttu-id="f7486-136">Este enfoque requiere toodeploy y administrar los servicios individuales de hello individualmente (o encontrar otras herramientas que hacerlo) y no como una sola unidad lógica de implementación.</span><span class="sxs-lookup"><span data-stu-id="f7486-136">This approach requires you toodeploy and manage hello individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span></span>

<span data-ttu-id="f7486-137">*Plantillas de administrador de recursos de Azure*, sin embargo, que sea posible, toodeploy y administrar estos recursos diferentes como una unidad lógica de implementación de forma declarativa.</span><span class="sxs-lookup"><span data-stu-id="f7486-137">*Azure Resource Manager templates*, however, make it possible for you toodeploy and manage these different resources as one logical deployment unit in a declarative fashion.</span></span> <span data-ttu-id="f7486-138">En lugar de imperativamente indicar que Azure qué toodeploy un comando después de otro, se describe toda la implementación en un archivo JSON: todos los recursos de Hola y parámetros de implementación y configuración asociada--y saber toodeploy Azure esos recursos como una grupo.</span><span class="sxs-lookup"><span data-stu-id="f7486-138">Instead of imperatively telling Azure what toodeploy one command after another, you describe your entire deployment in a JSON file -- all of hello resources and associated configuration and deployment parameters -- and tell Azure toodeploy those resources as one group.</span></span>

<span data-ttu-id="f7486-139">A continuación, puede administrar Hola ciclo de vida general de los recursos del grupo de hello mediante comandos de administración de recursos de CLI de Azure para:</span><span class="sxs-lookup"><span data-stu-id="f7486-139">You can then manage hello overall life cycle of hello group's resources by using Azure CLI resource management commands to:</span></span>

* <span data-ttu-id="f7486-140">Detener, iniciar o eliminar todos los recursos de hello en el grupo de Hola a la vez.</span><span class="sxs-lookup"><span data-stu-id="f7486-140">Stop, start, or delete all of hello resources within hello group at once.</span></span>
* <span data-ttu-id="f7486-141">Aplicar toolock de reglas de Control de acceso basado en roles (RBAC) hacia abajo de permisos de seguridad en ellos.</span><span class="sxs-lookup"><span data-stu-id="f7486-141">Apply Role-Based Access Control (RBAC) rules toolock down security permissions on them.</span></span>
* <span data-ttu-id="f7486-142">Auditar operaciones.</span><span class="sxs-lookup"><span data-stu-id="f7486-142">Audit operations.</span></span>
* <span data-ttu-id="f7486-143">Etiquetar recursos con metadatos adicionales para un mejor seguimiento.</span><span class="sxs-lookup"><span data-stu-id="f7486-143">Tag resources with additional metadata for better tracking.</span></span>

<span data-ttu-id="f7486-144">Puede aprender mucho más sobre los grupos de recursos de Azure y qué puede hacer por usted en hello [Introducción a Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f7486-144">You can learn lots more about Azure resource groups and what they can do for you in hello [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="f7486-145">Si está interesado en la creación de plantillas, consulte [Creación de plantillas del Administrador de recursos de Azure](../articles/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f7486-145">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../articles/resource-group-authoring-templates.md).</span></span>

## <span data-ttu-id="f7486-146"><a id="quick-create-a-vm-in-azure"></a>Tarea: Creación rápida de una máquina virtual en Azure</span><span class="sxs-lookup"><span data-stu-id="f7486-146"><a id="quick-create-a-vm-in-azure"></a>Task: Quick-create a VM in Azure</span></span>
<span data-ttu-id="f7486-147">A veces, sabrá qué imagen que se necesita, y ahora necesita una máquina virtual desde esa imagen y no le interesa demasiado infraestructura hello, quizás haya tootest algo en una máquina virtual limpia.</span><span class="sxs-lookup"><span data-stu-id="f7486-147">Sometimes you know what image you need, and you need a VM from that image right now and you don't care too much about hello infrastructure -- maybe you have tootest something on a clean VM.</span></span> <span data-ttu-id="f7486-148">Es decir, cuando desea hello toouse `azure vm quick-create` comandos y pasar Hola argumentos necesarios toocreate una máquina virtual y su infraestructura.</span><span class="sxs-lookup"><span data-stu-id="f7486-148">That's when you want toouse hello `azure vm quick-create` command, and pass hello arguments necessary toocreate a VM and its infrastructure.</span></span>

<span data-ttu-id="f7486-149">En primer lugar, cree el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f7486-149">First, create your resource group.</span></span>

```azurecli
azure group create coreos-quick westus
info:    Executing command group create
+ Getting resource group coreos-quick
+ Creating resource group coreos-quick
info:    Created resource group coreos-quick
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick
data:    Name:                coreos-quick
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="f7486-150">En segundo lugar, necesitará una imagen.</span><span class="sxs-lookup"><span data-stu-id="f7486-150">Second, you'll need an image.</span></span> <span data-ttu-id="f7486-151">toofind una imagen con hello CLI de Azure, consulte [Navigating y seleccionar las imágenes de máquina virtual de Azure con hello Azure CLI y PowerShell](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7486-151">toofind an image with hello Azure CLI, see [Navigating and selecting Azure virtual machine images with PowerShell and hello Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="f7486-152">Para este artículo, le presentamos una breve lista de imágenes populares.</span><span class="sxs-lookup"><span data-stu-id="f7486-152">But for this article, here's a short list of popular images.</span></span> <span data-ttu-id="f7486-153">Vamos a usar la imagen Stable de CoreOS para esta creación rápida.</span><span class="sxs-lookup"><span data-stu-id="f7486-153">We'll use CoreOS's Stable image for this quick-create.</span></span>

> [!NOTE]
> <span data-ttu-id="f7486-154">Para ComputeImageVersion, solo puede también tiene que proporcionar 'última' como Hola parámetro en ambos idioma de plantilla de Hola y Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="f7486-154">For ComputeImageVersion, you can also simply supply 'latest' as hello parameter in both hello template language and in hello Azure CLI.</span></span> <span data-ttu-id="f7486-155">Esto le permitirá que tooalways usas hello más reciente y revisado la versión de imagen de hello sin necesidad de toomodify las secuencias de comandos o plantillas.</span><span class="sxs-lookup"><span data-stu-id="f7486-155">This will allow you tooalways use hello latest and patched version of hello image without having toomodify your scripts or templates.</span></span> <span data-ttu-id="f7486-156">Esto se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="f7486-156">This is shown below.</span></span>
>
>

| <span data-ttu-id="f7486-157">PublisherName</span><span class="sxs-lookup"><span data-stu-id="f7486-157">PublisherName</span></span> | <span data-ttu-id="f7486-158">Oferta</span><span class="sxs-lookup"><span data-stu-id="f7486-158">Offer</span></span> | <span data-ttu-id="f7486-159">SKU</span><span class="sxs-lookup"><span data-stu-id="f7486-159">Sku</span></span> | <span data-ttu-id="f7486-160">Versión</span><span class="sxs-lookup"><span data-stu-id="f7486-160">Version</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f7486-161">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="f7486-161">OpenLogic</span></span> |<span data-ttu-id="f7486-162">CentOS</span><span class="sxs-lookup"><span data-stu-id="f7486-162">CentOS</span></span> |<span data-ttu-id="f7486-163">7</span><span class="sxs-lookup"><span data-stu-id="f7486-163">7</span></span> |<span data-ttu-id="f7486-164">7.0.201503</span><span class="sxs-lookup"><span data-stu-id="f7486-164">7.0.201503</span></span> |
| <span data-ttu-id="f7486-165">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="f7486-165">OpenLogic</span></span> |<span data-ttu-id="f7486-166">CentOS</span><span class="sxs-lookup"><span data-stu-id="f7486-166">CentOS</span></span> |<span data-ttu-id="f7486-167">7.1</span><span class="sxs-lookup"><span data-stu-id="f7486-167">7.1</span></span> |<span data-ttu-id="f7486-168">7.1.201504</span><span class="sxs-lookup"><span data-stu-id="f7486-168">7.1.201504</span></span> |
| <span data-ttu-id="f7486-169">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f7486-169">CoreOS</span></span> |<span data-ttu-id="f7486-170">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f7486-170">CoreOS</span></span> |<span data-ttu-id="f7486-171">Versión beta</span><span class="sxs-lookup"><span data-stu-id="f7486-171">Beta</span></span> |<span data-ttu-id="f7486-172">647.0.0</span><span class="sxs-lookup"><span data-stu-id="f7486-172">647.0.0</span></span> |
| <span data-ttu-id="f7486-173">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f7486-173">CoreOS</span></span> |<span data-ttu-id="f7486-174">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f7486-174">CoreOS</span></span> |<span data-ttu-id="f7486-175">Stable</span><span class="sxs-lookup"><span data-stu-id="f7486-175">Stable</span></span> |<span data-ttu-id="f7486-176">633.1.0</span><span class="sxs-lookup"><span data-stu-id="f7486-176">633.1.0</span></span> |
| <span data-ttu-id="f7486-177">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="f7486-177">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="f7486-178">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="f7486-178">DynamicsNAV</span></span> |<span data-ttu-id="f7486-179">2015</span><span class="sxs-lookup"><span data-stu-id="f7486-179">2015</span></span> |<span data-ttu-id="f7486-180">8.0.40459</span><span class="sxs-lookup"><span data-stu-id="f7486-180">8.0.40459</span></span> |
| <span data-ttu-id="f7486-181">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="f7486-181">MicrosoftSharePoint</span></span> |<span data-ttu-id="f7486-182">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="f7486-182">MicrosoftSharePointServer</span></span> |<span data-ttu-id="f7486-183">2013</span><span class="sxs-lookup"><span data-stu-id="f7486-183">2013</span></span> |<span data-ttu-id="f7486-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="f7486-184">1.0.0</span></span> |
| <span data-ttu-id="f7486-185">msopentech</span><span class="sxs-lookup"><span data-stu-id="f7486-185">msopentech</span></span> |<span data-ttu-id="f7486-186">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="f7486-186">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="f7486-187">Estándar</span><span class="sxs-lookup"><span data-stu-id="f7486-187">Standard</span></span> |<span data-ttu-id="f7486-188">1.0.0</span><span class="sxs-lookup"><span data-stu-id="f7486-188">1.0.0</span></span> |
| <span data-ttu-id="f7486-189">msopentech</span><span class="sxs-lookup"><span data-stu-id="f7486-189">msopentech</span></span> |<span data-ttu-id="f7486-190">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="f7486-190">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="f7486-191">Enterprise</span><span class="sxs-lookup"><span data-stu-id="f7486-191">Enterprise</span></span> |<span data-ttu-id="f7486-192">1.0.0</span><span class="sxs-lookup"><span data-stu-id="f7486-192">1.0.0</span></span> |
| <span data-ttu-id="f7486-193">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="f7486-193">MicrosoftSQLServer</span></span> |<span data-ttu-id="f7486-194">WS2012R2 SQL2014</span><span class="sxs-lookup"><span data-stu-id="f7486-194">SQL2014-WS2012R2</span></span> |<span data-ttu-id="f7486-195">Enterprise-Optimized-for-DW</span><span class="sxs-lookup"><span data-stu-id="f7486-195">Enterprise-Optimized-for-DW</span></span> |<span data-ttu-id="f7486-196">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="f7486-196">12.0.2430</span></span> |
| <span data-ttu-id="f7486-197">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="f7486-197">MicrosoftSQLServer</span></span> |<span data-ttu-id="f7486-198">WS2012R2 SQL2014</span><span class="sxs-lookup"><span data-stu-id="f7486-198">SQL2014-WS2012R2</span></span> |<span data-ttu-id="f7486-199">Enterprise-Optimized-for-OLTP</span><span class="sxs-lookup"><span data-stu-id="f7486-199">Enterprise-Optimized-for-OLTP</span></span> |<span data-ttu-id="f7486-200">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="f7486-200">12.0.2430</span></span> |
| <span data-ttu-id="f7486-201">Canonical</span><span class="sxs-lookup"><span data-stu-id="f7486-201">Canonical</span></span> |<span data-ttu-id="f7486-202">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="f7486-202">UbuntuServer</span></span> |<span data-ttu-id="f7486-203">12.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="f7486-203">12.04.5-LTS</span></span> |<span data-ttu-id="f7486-204">12.04.201504230</span><span class="sxs-lookup"><span data-stu-id="f7486-204">12.04.201504230</span></span> |
| <span data-ttu-id="f7486-205">Canonical</span><span class="sxs-lookup"><span data-stu-id="f7486-205">Canonical</span></span> |<span data-ttu-id="f7486-206">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="f7486-206">UbuntuServer</span></span> |<span data-ttu-id="f7486-207">14.04.2-LTS</span><span class="sxs-lookup"><span data-stu-id="f7486-207">14.04.2-LTS</span></span> |<span data-ttu-id="f7486-208">14.04.201503090</span><span class="sxs-lookup"><span data-stu-id="f7486-208">14.04.201503090</span></span> |
| <span data-ttu-id="f7486-209">Microsoft Windows Server</span><span class="sxs-lookup"><span data-stu-id="f7486-209">MicrosoftWindowsServer</span></span> |<span data-ttu-id="f7486-210">Windows Server</span><span class="sxs-lookup"><span data-stu-id="f7486-210">WindowsServer</span></span> |<span data-ttu-id="f7486-211">Centro de datos de 2012</span><span class="sxs-lookup"><span data-stu-id="f7486-211">2012-Datacenter</span></span> |<span data-ttu-id="f7486-212">3.0.201503</span><span class="sxs-lookup"><span data-stu-id="f7486-212">3.0.201503</span></span> |
| <span data-ttu-id="f7486-213">Microsoft Windows Server</span><span class="sxs-lookup"><span data-stu-id="f7486-213">MicrosoftWindowsServer</span></span> |<span data-ttu-id="f7486-214">Windows Server</span><span class="sxs-lookup"><span data-stu-id="f7486-214">WindowsServer</span></span> |<span data-ttu-id="f7486-215">Centro de datos de 2012-R2</span><span class="sxs-lookup"><span data-stu-id="f7486-215">2012-R2-Datacenter</span></span> |<span data-ttu-id="f7486-216">4.0.201503</span><span class="sxs-lookup"><span data-stu-id="f7486-216">4.0.201503</span></span> |
| <span data-ttu-id="f7486-217">Microsoft Windows Server</span><span class="sxs-lookup"><span data-stu-id="f7486-217">MicrosoftWindowsServer</span></span> |<span data-ttu-id="f7486-218">Windows Server</span><span class="sxs-lookup"><span data-stu-id="f7486-218">WindowsServer</span></span> |<span data-ttu-id="f7486-219">Windows-Server-Technical-Preview</span><span class="sxs-lookup"><span data-stu-id="f7486-219">Windows-Server-Technical-Preview</span></span> |<span data-ttu-id="f7486-220">5.0.201504</span><span class="sxs-lookup"><span data-stu-id="f7486-220">5.0.201504</span></span> |
| <span data-ttu-id="f7486-221">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="f7486-221">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="f7486-222">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="f7486-222">WindowsServerEssentials</span></span> |<span data-ttu-id="f7486-223">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="f7486-223">WindowsServerEssentials</span></span> |<span data-ttu-id="f7486-224">1.0.141204</span><span class="sxs-lookup"><span data-stu-id="f7486-224">1.0.141204</span></span> |
| <span data-ttu-id="f7486-225">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="f7486-225">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="f7486-226">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="f7486-226">WindowsServerHPCPack</span></span> |<span data-ttu-id="f7486-227">2012R2</span><span class="sxs-lookup"><span data-stu-id="f7486-227">2012R2</span></span> |<span data-ttu-id="f7486-228">4.3.4665</span><span class="sxs-lookup"><span data-stu-id="f7486-228">4.3.4665</span></span> |

<span data-ttu-id="f7486-229">Basta con crear la máquina virtual mediante la especificación de hello `azure vm quick-create` comando y está listo para mensajes de Hola.</span><span class="sxs-lookup"><span data-stu-id="f7486-229">Just create your VM by entering hello `azure vm quick-create` command and being ready for hello prompts.</span></span> <span data-ttu-id="f7486-230">Debe tener un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="f7486-230">It should look something like this:</span></span>

```azurecli
azure vm quick-create
info:    Executing command vm quick-create
Resource group name: coreos-quick
Virtual machine name: coreos
Location name: westus
Operating system Type [Windows, Linux]: linux
ImageURN (format: "publisherName:offer:skus:version"): coreos:coreos:stable:latest
User name: ops
Password: *********
Confirm password: *********
+ Looking up hello VM "coreos"
info:    Using hello VM Size "Standard_A1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in hello region "westus", trying toocreate new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up hello storage account cli9fd3fce49e9a9b3d14302
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing toocreate new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
+ Looking up hello subnet "coreo-westu-1430261891570-snet" under hello virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying toosetup PublicIP profile
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up hello VM "coreos"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Compute/virtualMachines/coreos
data:    ProvisioningState               :Succeeded
data:    Name                            :coreos
data:    Location                        :westus
data:    FQDN                            :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :coreos
data:        Offer                       :coreos
data:        Sku                         :stable
data:        Version                     :633.1.0
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :cli9fd3fce49e9a9b3d-os-1430261892283
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli9fd3fce49e9a9b3d14302.blob.core.windows.net/vhds/cli9fd3fce49e9a9b3d-os-1430261892283.vhd
data:
data:    OS Profile:
data:      Computer Name                 :coreos
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :false
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Network/networkInterfaces/coreo-westu-1430261891570-nic
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-30-72-E3
data:          Provisioning State        :Succeeded
data:          Name                      :coreo-westu-1430261891570-nic
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.1.4
data:            Public IP address       :104.40.24.124
data:            FQDN                    :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
info:    vm quick-create command OK
```

<span data-ttu-id="f7486-231">Y ya está lista la nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f7486-231">And away you go with your new VM.</span></span>

## <span data-ttu-id="f7486-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Tarea: Implementación de una máquina virtual en Azure desde una plantilla</span><span class="sxs-lookup"><span data-stu-id="f7486-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Task: Deploy a VM in Azure from a template</span></span>
<span data-ttu-id="f7486-233">Siga las instrucciones de hello en estos toodeploy secciones una nueva máquina virtual de Azure mediante una plantilla con hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="f7486-233">Use hello instructions in these sections toodeploy a new Azure VM by using a template with hello Azure CLI.</span></span> <span data-ttu-id="f7486-234">Esta plantilla crea una sola máquina virtual en una nueva red virtual con una sola subred y, a diferencia de `azure vm quick-create`, permite toodescribe exactamente lo que desea y repetir sin errores.</span><span class="sxs-lookup"><span data-stu-id="f7486-234">This template creates a single virtual machine in a new virtual network with a single subnet, and unlike `azure vm quick-create`, enables you toodescribe what you want precisely and repeat it without errors.</span></span> <span data-ttu-id="f7486-235">Esto es lo que crea esta plantilla:</span><span class="sxs-lookup"><span data-stu-id="f7486-235">Here's what this template creates:</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-hello-json-file-for-hello-template-parameters"></a><span data-ttu-id="f7486-236">Paso 1: Examinar el archivo JSON de Hola Hola para parámetros de plantilla</span><span class="sxs-lookup"><span data-stu-id="f7486-236">Step 1: Examine hello JSON file for hello template parameters</span></span>
<span data-ttu-id="f7486-237">Aquí es contenido de hello del archivo JSON de hello para la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="f7486-237">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="f7486-238">(plantilla de hello también se encuentra en [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="f7486-238">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span></span>

<span data-ttu-id="f7486-239">Plantillas son flexibles, por lo que hayan elegido toogive gran cantidad de parámetros o elegido toooffer solo unas pocas mediante la creación de una plantilla que más se fija diseñador Hola.</span><span class="sxs-lookup"><span data-stu-id="f7486-239">Templates are flexible, so hello designer may have chosen toogive you lots of parameters or chosen toooffer only a few by creating a template that is more fixed.</span></span> <span data-ttu-id="f7486-240">En información de pedidos toocollect Hola que es necesaria una plantilla de hello toopass como parámetros, abra el archivo de plantilla de hello (este tema contiene una plantilla insertada, a continuación) y examine hello **parámetros** valores.</span><span class="sxs-lookup"><span data-stu-id="f7486-240">In order toocollect hello information you need toopass hello template as parameters, open hello template file (this topic has a template inline, below) and examine hello **parameters** values.</span></span>

<span data-ttu-id="f7486-241">En este caso, le solicitará la siguiente plantilla de Hola para:</span><span class="sxs-lookup"><span data-stu-id="f7486-241">In this case, hello template below will ask for:</span></span>

* <span data-ttu-id="f7486-242">Un nombre de cuenta de almacenamiento único</span><span class="sxs-lookup"><span data-stu-id="f7486-242">A unique storage account name.</span></span>
* <span data-ttu-id="f7486-243">Un nombre de usuario de administrador para hello VM.</span><span class="sxs-lookup"><span data-stu-id="f7486-243">An admin user name for hello VM.</span></span>
* <span data-ttu-id="f7486-244">Una contraseña</span><span class="sxs-lookup"><span data-stu-id="f7486-244">A password.</span></span>
* <span data-ttu-id="f7486-245">Un nombre de dominio para hello fuera toouse del mundo.</span><span class="sxs-lookup"><span data-stu-id="f7486-245">A domain name for hello outside world toouse.</span></span>
* <span data-ttu-id="f7486-246">Un número de versión de Ubuntu Server, pero solo uno, de una lista</span><span class="sxs-lookup"><span data-stu-id="f7486-246">An Ubuntu Server version number -- but it will accept only one of a list.</span></span>

<span data-ttu-id="f7486-247">Obtenga más información acerca de los [requisitos de usuario y la contraseña](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="f7486-247">See more about [username and password requirements](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span>

<span data-ttu-id="f7486-248">Una vez que decida sobre estos valores, está listo toocreate un grupo para e implementar esta plantilla en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="f7486-248">Once you decide on these values, you're ready toocreate a group for and deploy this template into your Azure subscription.</span></span>

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello storage account where hello virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for hello virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for hello virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello public IP used tooaccess hello virtual machine."
    }
    },
    "ubuntuOSVersion": {
    "type": "string",
    "defaultValue": "14.04.2-LTS",
    "allowedValues": [
        "12.04.5-LTS",
        "14.04.2-LTS",
        "15.04"
    ],
    "metadata": {
        "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
    }
    }
},
"variables": {
    "location": "West US",
    "imagePublisher": "Canonical",
    "imageOffer": "UbuntuServer",
    "OSDiskName": "osdiskforlinuxsimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyUbuntuVM",
    "vmSize": "Standard_D1",
    "virtualNetworkName": "MyVNET",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
},
"resources": [
    {
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[parameters('newStorageAccountName')]",
    "apiVersion": "2015-05-01-preview",
    "location": "[variables('location')]",
    "properties": {
        "accountType": "[variables('storageAccountType')]"
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/publicIPAddresses",
    "name": "[variables('publicIPAddressName')]",
    "location": "[variables('location')]",
    "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
        "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
        }
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[variables('virtualNetworkName')]",
    "location": "[variables('location')]",
    "properties": {
        "addressSpace": {
        "addressPrefixes": [
            "[variables('addressPrefix')]"
        ]
        },
        "subnets": [
        {
            "name": "[variables('subnetName')]",
            "properties": {
            "addressPrefix": "[variables('subnetPrefix')]"
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('nicName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
    ],
    "properties": {
        "ipConfigurations": [
        {
            "name": "ipconfig1",
            "properties": {
            "privateIPAllocationMethod": "Dynamic",
            "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
            },
            "subnet": {
                "id": "[variables('subnetRef')]"
            }
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', parameters('newStorageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
        "computername": "[variables('vmName')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
        "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('ubuntuOSVersion')]",
            "version": "latest"
        },
        "osDisk": {
            "name": "osdisk",
            "vhd": {
            "uri": "[concat('http://',parameters('newStorageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
        }
        },
        "networkProfile": {
        "networkInterfaces": [
            {
            "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
        ]
        }
    }
    }
]
}
```

### <a name="step-2-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="f7486-249">Paso 2: Crear la máquina virtual de Hola mediante la plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="f7486-249">Step 2: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="f7486-250">Una vez que tenga los valores de parámetro listo, debe crear un grupo de recursos para la implementación de plantilla y, a continuación, implementar la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="f7486-250">Once you have your parameter values ready, you must create a resource group for your template deployment and then deploy hello template.</span></span>

<span data-ttu-id="f7486-251">grupo de recursos de hello toocreate, tipo `azure group create <group name> <location>` por nombre de Hola de grupo de Hola que desee y ubicación de centro de datos de hello en el que desea toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f7486-251">toocreate hello resource group, type `azure group create <group name> <location>` with hello name of hello group you want and hello datacenter location into which you want toodeploy.</span></span> <span data-ttu-id="f7486-252">Esto sucede rápidamente:</span><span class="sxs-lookup"><span data-stu-id="f7486-252">This happens quickly:</span></span>

```azurecli
azure group create myResourceGroup westus
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="f7486-253">Implementación de hello toocreate ahora, llamada `azure group deployment create` y pasar:</span><span class="sxs-lookup"><span data-stu-id="f7486-253">Now toocreate hello deployment, call `azure group deployment create` and pass:</span></span>

* <span data-ttu-id="f7486-254">en el archivo de plantilla Hello (si guardó Hola por encima de archivo local de JSON plantilla tooa).</span><span class="sxs-lookup"><span data-stu-id="f7486-254">hello template file (if you saved hello above JSON template tooa local file).</span></span>
* <span data-ttu-id="f7486-255">Una plantilla de URI (si lo desea toopoint en el archivo hello en GitHub o alguna otra dirección web).</span><span class="sxs-lookup"><span data-stu-id="f7486-255">A template URI (if you want toopoint at hello file in GitHub or some other web address).</span></span>
* <span data-ttu-id="f7486-256">grupo de recursos de Hello en el que desea toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f7486-256">hello resource group into which you want toodeploy.</span></span>
* <span data-ttu-id="f7486-257">Un nombre de implementación opcional</span><span class="sxs-lookup"><span data-stu-id="f7486-257">An optional deployment name.</span></span>

<span data-ttu-id="f7486-258">Es posible que toosupply solicitadas Hola valores de parámetros en la sección "parámetros" de Hola de archivo de hello JSON.</span><span class="sxs-lookup"><span data-stu-id="f7486-258">You will be prompted toosupply hello values of parameters in hello "parameters" section of hello JSON file.</span></span> <span data-ttu-id="f7486-259">Cuando haya especificado todos los valores de parámetro de hello, se iniciará la implementación.</span><span class="sxs-lookup"><span data-stu-id="f7486-259">When you have specified all hello parameter values, your deployment will begin.</span></span>

<span data-ttu-id="f7486-260">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f7486-260">Here is an example:</span></span>

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

<span data-ttu-id="f7486-261">Recibirá el mensaje Hola después del tipo de información:</span><span class="sxs-lookup"><span data-stu-id="f7486-261">You will receive hello following type of information:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
data:    DeploymentName     : firstDeployment
data:    ResourceGroupName  : myResourceGroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T07:53:55.1828878Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  -------------
data:    newStorageAccountName  String        storageaccount
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameForPublicIP     String        newdomainname
data:    ubuntuOSVersion        String        14.10
info:    group deployment create command OK
```


## <span data-ttu-id="f7486-262"><a id="create-a-custom-vm-image"></a>Tarea: Creación de una imagen de máquina virtual personalizada</span><span class="sxs-lookup"><span data-stu-id="f7486-262"><a id="create-a-custom-vm-image"></a>Task: Create a custom VM image</span></span>
<span data-ttu-id="f7486-263">Ha visto uso básico de Hola de las plantillas anteriores, por lo que ahora podemos usar similar toocreate instrucciones una máquina virtual personalizada desde un archivo .vhd concreto en Azure mediante una plantilla a través de Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="f7486-263">You've seen hello basic usage of templates above, so now we can use similar instructions toocreate a custom VM from a specific .vhd file in Azure by using a template via hello Azure CLI.</span></span> <span data-ttu-id="f7486-264">Hola diferencia es que esta plantilla crea una sola máquina virtual desde un disco duro virtual (VHD) especificado.</span><span class="sxs-lookup"><span data-stu-id="f7486-264">hello difference here is that this template creates a single virtual machine from a specified virtual hard disk (VHD).</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="f7486-265">Paso 1: Examinar el archivo JSON de hello para la plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="f7486-265">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="f7486-266">Aquí es contenido de hello del archivo JSON de hello para la plantilla de Hola que en esta sección se utiliza como ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f7486-266">Here are hello contents of hello JSON file for hello template that this section uses as an example.</span></span> <span data-ttu-id="f7486-267">(plantilla de hello también se encuentra en [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="f7486-267">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span></span>

<span data-ttu-id="f7486-268">De nuevo, se necesita valores de hello toofind desea tooenter para parámetros de Hola que no tienen valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="f7486-268">Again, you will need toofind hello values you want tooenter for hello parameters that do not have default values.</span></span> <span data-ttu-id="f7486-269">Cuando ejecute hello `azure group deployment create` comando hello Azure CLI le pedirá tooenter esos valores.</span><span class="sxs-lookup"><span data-stu-id="f7486-269">When you run hello `azure group deployment create` command, hello Azure CLI will prompt you tooenter those values.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters" : {
        "userImageStorageAccountName": {
            "type": "string",
            "defaultValue" : "userImageStorageAccountName"
        },
        "userImageStorageContainerName" : {
            "type" : "string",
            "defaultValue" : "userImageStorageContainerName"
        },
        "userImageVhdName" : {
            "type" : "string",
            "defaultValue" : "userImageVhdName"
        },
        "dnsNameForPublicIP" : {
            "type" : "string",
            "defaultValue": "uniqueDnsNameForPublicIP"
        },
        "adminUserName": {
            "type": "string"
        },
        "adminPassword": {
            "type": "securestring"
        },
        "osType" : {
            "type" : "string",
            "allowedValues" : [
                "windows",
                "linux"
            ]
        },
        "subscriptionId":{
            "type" : "string"
        },
        "location": {
            "type": "String",
            "defaultValue" : "West US"
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A2"
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue" : "myPublicIP"
        },
        "vmName": {
            "type": "string",
            "defaultValue" : "myVM"
        },
        "virtualNetworkName":{
            "type" : "string",
            "defaultValue" : "myVNET"
        },
        "nicName":{
            "type" : "string",
            "defaultValue":"myNIC"
        }
    },
    "variables": {
        "addressPrefix":"10.0.0.0/16",
        "subnet1Name": "Subnet-1",
        "subnet2Name": "Subnet-2",
        "subnet1Prefix" : "10.0.0.0/24",
        "subnet2Prefix" : "10.0.1.0/24",
        "publicIPAddressType" : "Dynamic",
        "vnetID":"[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",
        "subnet1Ref" : "[concat(variables('vnetID'),'/subnets/',variables('subnet1Name'))]",
        "userImageName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('userImageVhdName'))]",
        "osDiskVhdName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('vmName'),'osDisk.vhd')]"
    },
    "resources": [
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[parameters('publicIPAddressName')]",
        "location": "[parameters('location')]",
        "properties": {
            "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
            }
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/virtualNetworks",
        "name": "[parameters('virtualNetworkName')]",
        "location": "[parameters('location')]",
        "properties": {
        "addressSpace": {
            "addressPrefixes": [
            "[variables('addressPrefix')]"
            ]
        },
        "subnets": [
            {
            "name": "[variables('subnet1Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet1Prefix')]"
            }
            },
            {
            "name": "[variables('subnet2Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet2Prefix')]"
            }
            }
        ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/networkInterfaces",
        "name": "[parameters('nicName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]",
            "[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]"
        ],
        "properties": {
            "ipConfigurations": [
            {
                "name": "ipconfig1",
                "properties": {
                    "privateIPAllocationMethod": "Dynamic",
                    "publicIPAddress": {
                        "id": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]"
                    },
                    "subnet": {
                        "id": "[variables('subnet1Ref')]"
                    }
                }
            }
            ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Compute/virtualMachines",
        "name": "[parameters('vmName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/networkInterfaces/', parameters('nicName'))]"
        ],
        "properties": {
            "hardwareProfile": {
                "vmSize": "[parameters('vmSize')]"
            },
            "osProfile": {
                "computername": "[parameters('vmName')]",
                "adminUsername": "[parameters('adminUsername')]",
                "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
                "osDisk" : {
                    "name" : "[concat(parameters('vmName'),'-osDisk')]",
                    "osType" : "[parameters('osType')]",
                    "caching" : "ReadWrite",
                    "image" : {
                        "uri" : "[variables('userImageName')]"
                    },
                    "vhd" : {
                        "uri" : "[variables('osDiskVhdName')]"
                    }
                }
            },
            "networkProfile": {
                "networkInterfaces" : [
                {
                    "id": "[resourceId('Microsoft.Network/networkInterfaces',parameters('nicName'))]"
                }
                ]
            }
        }
    }
    ]
}
```

### <a name="step-2-obtain-hello-vhd"></a><span data-ttu-id="f7486-270">Paso 2: Obtener Hola VHD</span><span class="sxs-lookup"><span data-stu-id="f7486-270">Step 2: Obtain hello VHD</span></span>
<span data-ttu-id="f7486-271">Obviamente, necesitará un archivo .vhd para esto.</span><span class="sxs-lookup"><span data-stu-id="f7486-271">Obviously, you'll need a .vhd for this.</span></span> <span data-ttu-id="f7486-272">Puede usar otro que ya creado en Azure, o puede cargar uno.</span><span class="sxs-lookup"><span data-stu-id="f7486-272">You can use one you already have in Azure, or you can upload one.</span></span>

<span data-ttu-id="f7486-273">Para una máquina virtual basada en Windows, consulte [crear y cargar un VHD de Windows Server tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7486-273">For a Windows-based virtual machine, see [Create and upload a Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="f7486-274">Para una máquina virtual basadas en Linux, consulte [crear y cargar un disco duro virtual que contiene el sistema operativo de Linux de hello](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7486-274">For a Linux-based virtual machine, see [Creating and uploading a virtual hard disk that contains hello Linux operating system](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

### <a name="step-3-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="f7486-275">Paso 3: Crear máquina virtual de hello mediante plantilla Hola</span><span class="sxs-lookup"><span data-stu-id="f7486-275">Step 3: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="f7486-276">Ahora está listo toocreate una nueva máquina virtual en función de hello .vhd.</span><span class="sxs-lookup"><span data-stu-id="f7486-276">Now you're ready toocreate a new virtual machine based on hello .vhd.</span></span> <span data-ttu-id="f7486-277">Crear un toodeploy de grupo, mediante `azure group create <location>`:</span><span class="sxs-lookup"><span data-stu-id="f7486-277">Create a group toodeploy into, by using `azure group create <location>`:</span></span>

```azurecli
azure group create myResourceGroupUser eastus
info:    Executing command group create
+ Getting resource group myResourceGroupUser
+ Creating resource group myResourceGroupUser
info:    Created resource group myResourceGroupUser
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupUser
data:    Name:                myResourceGroupUser
data:    Location:            eastus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="f7486-278">A continuación, crear implementación de hello mediante hello `--template-uri` toocall de opción de plantilla de hello directamente (o puede usar hello `--template-file` opción toouse un archivo que haya guardado localmente).</span><span class="sxs-lookup"><span data-stu-id="f7486-278">Then create hello deployment by using hello `--template-uri` option toocall in hello template directly (or you can use hello `--template-file` option toouse a file that you have saved locally).</span></span> <span data-ttu-id="f7486-279">Tenga en cuenta que porque Hola una plantilla con los valores predeterminados especificados, se le solicitará sólo algunas cosas.</span><span class="sxs-lookup"><span data-stu-id="f7486-279">Note that because hello template has defaults specified, you are prompted for only a few things.</span></span> <span data-ttu-id="f7486-280">Si implementa la plantilla de hello en distintos lugares, es posible que algunos conflictos de nomenclaturas se producen con los valores predeterminados de hello (especialmente Hola nombre DNS que cree).</span><span class="sxs-lookup"><span data-stu-id="f7486-280">If you deploy hello template in different places, you may find that some naming collisions occur with hello default values (particularly hello DNS name you create).</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

<span data-ttu-id="f7486-281">Salida es similar a Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="f7486-281">Output looks something like hello following:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
error:   Deployment provisioning state was not successful
data:    DeploymentName     : customVhdDeployment
data:    ResourceGroupName  : myResourceGroupUser
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T14:55:48.0963829Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                           Type          Value
data:    -----------------------------  ------------  ------------------------------------
data:    userImageStorageAccountName    String        userImageStorageAccountName
data:    userImageStorageContainerName  String        userImageStorageContainerName
data:    userImageVhdName               String        userImageVhdName
data:    dnsNameForPublicIP             String        uniqueDnsNameForPublicIP
data:    adminUserName                  String        ops
data:    adminPassword                  SecureString  undefined
data:    osType                         String        linux
data:    subscriptionId                 String        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
data:    location                       String        West US
data:    vmSize                         String        Standard_A2
data:    publicIPAddressName            String        myPublicIP
data:    vmName                         String        myVM
data:    virtualNetworkName             String        myVNET
data:    nicName                        String        myNIC
info:    group deployment create command OK
```

## <span data-ttu-id="f7486-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Tarea: Implementación de una aplicación de varias máquinas virtuales que usa una red virtual y un equilibrador de carga externo</span><span class="sxs-lookup"><span data-stu-id="f7486-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Task: Deploy a multi-VM application that uses a virtual network and an external load balancer</span></span>
<span data-ttu-id="f7486-283">Esta plantilla le permite toocreate dos máquinas virtuales en un equilibrador de carga y configurar una regla de equilibrio de carga en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="f7486-283">This template allows you toocreate two virtual machines under a load balancer and configure a load-balancing rule on Port 80.</span></span> <span data-ttu-id="f7486-284">Esta plantilla también implementa una cuenta de almacenamiento, la red virtual, la dirección IP pública, un conjunto de disponibilidad y las interfaces de red.</span><span class="sxs-lookup"><span data-stu-id="f7486-284">This template also deploys a storage account, virtual network, public IP address, availability set, and network interfaces.</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

<span data-ttu-id="f7486-285">Siga estos toodeploy pasos una aplicación de varias VM que utiliza una red virtual y un equilibrador de carga mediante una plantilla de administrador de recursos en el repositorio de plantilla de GitHub de Hola a través de los comandos de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="f7486-285">Follow these steps toodeploy a multi-VM application that uses a virtual network and a load balancer by using a Resource Manager template in hello GitHub template repository via Azure PowerShell commands.</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="f7486-286">Paso 1: Examinar el archivo JSON de hello para la plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="f7486-286">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="f7486-287">Aquí es contenido de hello del archivo JSON de hello para la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="f7486-287">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="f7486-288">Si desea que la versión más reciente de hello, se encuentra [en el repositorio de GitHub de Hola para plantillas de](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="f7486-288">If you want hello most recent version, it's located [at hello GitHub repository for templates](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span></span> <span data-ttu-id="f7486-289">En este tema usa hello `--template-uri` toocall de conmutador en las plantillas de hello, sino también puede utilizar hello `--template-file` cambiar toopass una versión local.</span><span class="sxs-lookup"><span data-stu-id="f7486-289">This topic uses hello `--template-uri` switch toocall in hello template, but you can also use hello `--template-file` switch toopass a local version.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location of resources"
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of storage account"
            }
        },
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "Admin user name"
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Admin password"
            }
        },
        "dnsNameforLBIP": {
            "type": "string",
            "metadata": {
                "description": "DNS for load balancer IP"
            }
        },
        "backendPort": {
            "type": "int",
            "defaultValue": 3389,
            "metadata": {
                "description": "Back-end port"
            }
        },
        "vmNamePrefix": {
            "type": "string",
            "defaultValue": "myVM",
            "metadata": {
                "description": "Prefix toouse for VM names"
            }
        },
        "vmSourceImageName": {
            "type": "string",
            "defaultValue": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201412.01-en.us-127GB.vhd"
        },
        "lbName": {
            "type": "string",
            "defaultValue": "myLB",
            "metadata": {
                "description": "Load balancer name"
            }
        },
        "nicNamePrefix": {
            "type": "string",
            "defaultValue": "nic",
            "metadata": {
                "description": "Network interface name prefix"
            }
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue": "myPublicIP",
            "metadata": {
                "description": "Public IP name"
            }
        },
        "vnetName": {
            "type": "string",
            "defaultValue": "myVNET",
            "metadata": {
                "description": "Virtual network name"
            }
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A1",
            "metadata": {
                "description": "Size of hello VM"
            }
        }
    },
    "variables": {
        "storageAccountType": "Standard_LRS",
        "vmStorageAccountContainerName": "vhds",
        "availabilitySetName": "myAvSet",
        "addressPrefix": "10.0.0.0/16",
        "subnetName": "Subnet-1",
        "subnetPrefix": "10.0.0.0/24",
        "publicIPAddressType": "Dynamic",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('vnetName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables ('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',parameters('lbName'))]",
        "numberOfInstances": 2,
        "nicId1": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 0))]",
        "nicId2": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 1))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/LBFE')]",
        "backEndIPConfigID1": "[concat(variables('nicId1'),'/ipConfigurations/ipconfig1')]",
        "backEndIPConfigID2": "[concat(variables('nicId2'),'/ipConfigurations/ipconfig1')]",
        "sourceImageName": "[concat('/', subscription().subscriptionId,'/services/images/',parameters('vmSourceImageName'))]",
        "lbPoolID": "[concat(variables('lbID'),'/backendAddressPools/LBBE')]",
        "lbProbeID": "[concat(variables('lbID'),'/probes/tcpProbe')]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('storageAccountName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": { }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/publicIPAddresses",
            "name": "[parameters('publicIPAddressName')]",
            "location": "[parameters('location')]",
            "properties": {
                "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
                "dnsSettings": {
                    "domainNameLabel": "[parameters('dnsNameforLBIP')]"
                }
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/virtualNetworks",
            "name": "[parameters('vnetName')]",
            "location": "[parameters('location')]",
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "[variables('addressPrefix')]"
                    ]
                },
                "subnets": [
                    {
                        "name": "[variables('subnetName')]",
                        "properties": {
                            "addressPrefix": "[variables('subnetPrefix')]"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/networkInterfaces",
            "name": "[concat(parameters('nicNamePrefix'), copyindex())]",
            "location": "[parameters('location')]",
            "copy": {
                "name": "nicLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "dependsOn": [
                "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
            ],
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipconfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "subnet": {
                                "id": "[variables('subnetRef')]"
                            }
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/backendAddressPools/LBBE')]"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/inboundNatRule/RDP-VM', copyindex())]"
                            }
                        ]


                    }
                ]

            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "name": "[parameters('lbName')]",
            "type": "Microsoft.Network/loadBalancers",
            "location": "[parameters('location')]",
            "dependsOn": [
                "nicLoop",
                "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]"
            ],
            "properties": {
                "frontendIPConfigurations": [
                    {
                        "name": "LBFE",
                        "properties": {
                            "publicIPAddress": {
                                "id": "[variables('publicIPAddressID')]"
                            }
                        }
                    }
                ],
                "backendAddressPools": [
                    {
                        "name": "LBBE"

                    }
                ],
                "inboundNatRules": [
                    {
                        "name": "RDP-VM1",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50001,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    },
                    {
                        "name": "RDP-VM2",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50002,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    }
                ],
                "loadBalancingRules": [
                    {
                        "name": "LBRule",
                        "properties": {
                            "frontendIPConfiguration": {
                                "id": "[variables('frontEndIPConfigID')]"
                            },
                            "backendAddressPool": {
                                "id": "[variables('lbPoolID')]"
                            },
                            "protocol": "tcp",
                            "frontendPort": 80,
                            "backendPort": 80,
                            "enableFloatingIP": false,
                            "idleTimeoutInMinutes": 5,
                            "probe": {
                                "id": "[variables('lbProbeID')]"
                            }
                        }
                    }
                ],
                "probes": [
                    {
                        "name": "tcpProbe",
                        "properties": {
                            "protocol": "tcp",
                            "port": 80,
                            "intervalInSeconds": "5",
                            "numberOfProbes": "2"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[concat(parameters('vmNamePrefix'), copyindex())]",
            "copy": {
                "name": "virtualMachineLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "location": "[parameters('location')]",
            "dependsOn": [
                "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]",
                "[concat('Microsoft.Network/networkInterfaces/', parameters('nicNamePrefix'), copyindex())]",
                "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]"
            ],
            "properties": {
                "availabilitySet": {
                    "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
                },
                "hardwareProfile": {
                    "vmSize": "[parameters('vmSize')]"
                },
                "osProfile": {
                    "computername": "[concat(parameters('vmNamePrefix'), copyIndex())]",
                    "adminUsername": "[parameters('adminUsername')]",
                    "adminPassword": "[parameters('adminPassword')]"
                },
                "storageProfile": {
                    "sourceImage": {
                        "id": "[variables('sourceImageName')]"
                    },
                    "destinationVhdsContainer": "[concat('http://',parameters('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/')]"
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'),copyindex()))]"
                        }
                    ]
                }
            }
        }
    ]
}
```

### <a name="step-2-create-hello-deployment-by-using-hello-template"></a><span data-ttu-id="f7486-290">Paso 2: Crear la implementación de hello mediante plantilla Hola</span><span class="sxs-lookup"><span data-stu-id="f7486-290">Step 2: Create hello deployment by using hello template</span></span>
<span data-ttu-id="f7486-291">Crear un grupo de recursos para la plantilla de hello mediante `azure group create <location>`.</span><span class="sxs-lookup"><span data-stu-id="f7486-291">Create a resource group for hello template by using `azure group create <location>`.</span></span> <span data-ttu-id="f7486-292">A continuación, cree una implementación en ese grupo de recursos mediante el uso de `azure group deployment create` y pasar el grupo de recursos de hello, pasar un nombre de la implementación y responder a mensajes de Hola para los parámetros de plantilla de Hola que no dispongan de valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="f7486-292">Then, create a deployment into that resource group by using `azure group deployment create` and passing hello resource group, passing a deployment name, and answering hello prompts for parameters in hello template that did not have default values.</span></span>

```azurecli
azure group create lbgroup westus
info:    Executing command group create
+ Getting resource group lbgroup
+ Creating resource group lbgroup
info:    Created resource group lbgroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/lbgroup
data:    Name:                lbgroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="f7486-293">Ahora use hello `azure group deployment create` hello y comando `--template-uri` plantilla de opción toodeploy Hola.</span><span class="sxs-lookup"><span data-stu-id="f7486-293">Now use hello `azure group deployment create` command and hello `--template-uri` option toodeploy hello template.</span></span> <span data-ttu-id="f7486-294">Prepare los valores de parámetros cuando se le pida, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="f7486-294">Be ready with your parameter values when it prompts you, as shown below.</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
location: westus
newStorageAccountName: storagename
adminUsername: ops
adminPassword: password
dnsNameforLBIP: lbdomainname
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "newdeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.compute
info:    Registering provider microsoft.network
+ Waiting for deployment toocomplete
data:    DeploymentName     : newdeployment
data:    ResourceGroupName  : lbgroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T20:58:40.1678876Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  ----------------------
data:    location               String        westus
data:    newStorageAccountName  String        storagename
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameforLBIP         String        lbdomainname
data:    backendPort            Int           3389
data:    vmNamePrefix           String        myVM
data:    imagePublisher         String        MicrosoftWindowsServer
data:    imageOffer             String        WindowsServer
data:    imageSKU               String        2012-R2-Datacenter
data:    lbName                 String        myLB
data:    nicNamePrefix          String        nic
data:    publicIPAddressName    String        myPublicIP
data:    vnetName               String        myVNET
data:    vmSize                 String        Standard_A1
info:    group deployment create command OK
```

<span data-ttu-id="f7486-295">Tenga en cuenta que esta plantilla implementa una imagen de Windows Server; sin embargo, también se podría reemplazar fácilmente por cualquier imagen de Linux.</span><span class="sxs-lookup"><span data-stu-id="f7486-295">Note that this template deploys a Windows Server image; however, it could easily be replaced by any Linux image.</span></span> <span data-ttu-id="f7486-296">¿Se desea toocreate un clúster de Docker con varios administradores de conjunto?</span><span class="sxs-lookup"><span data-stu-id="f7486-296">Want toocreate a Docker cluster with multiple swarm managers?</span></span> <span data-ttu-id="f7486-297">[Puede hacerlo](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span><span class="sxs-lookup"><span data-stu-id="f7486-297">[You can do it](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span></span>

## <span data-ttu-id="f7486-298"><a id="remove-a-resource-group"></a>Tarea: Eliminación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f7486-298"><a id="remove-a-resource-group"></a>Task: Remove a resource group</span></span>
<span data-ttu-id="f7486-299">Recuerde que puede volver a implementar el grupo de recursos de tooa, pero si ha terminado con uno, puede eliminar mediante `azure group delete <group name>`.</span><span class="sxs-lookup"><span data-stu-id="f7486-299">Remember that you can redeploy tooa resource group, but if you are done with one, you can delete it by using `azure group delete <group name>`.</span></span>

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <span data-ttu-id="f7486-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Tarea: Mostrar el registro de hello para una implementación de grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f7486-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Task: Show hello log for a resource group deployment</span></span>
<span data-ttu-id="f7486-301">Es común al crear o usar plantillas.</span><span class="sxs-lookup"><span data-stu-id="f7486-301">This one is common while you're creating or using templates.</span></span> <span data-ttu-id="f7486-302">implementación de Hello llamada toodisplay Hola registros de un grupo es `azure group log show <groupname>`, que muestra una gran cantidad de información que es útil para comprender por qué algo ha ocurrido--o no.</span><span class="sxs-lookup"><span data-stu-id="f7486-302">hello call toodisplay hello deployment logs for a group is `azure group log show <groupname>`, which displays quite a bit of information that's useful for understanding why something happened -- or didn't.</span></span> <span data-ttu-id="f7486-303">(Para más información sobre cómo solucionar problemas en las implementaciones, así como para ver otra información acerca de los problemas, consulte [Solución de errores comunes de implementación de Azure con Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span><span class="sxs-lookup"><span data-stu-id="f7486-303">(For more information on troubleshooting your deployments, as well as other information about issues, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span></span>

<span data-ttu-id="f7486-304">tootarget errores específicos, por ejemplo, podría usar herramientas como **jq** tooquery cosas un poco más concretamente, por ejemplo, los errores individuales tiene toocorrect.</span><span class="sxs-lookup"><span data-stu-id="f7486-304">tootarget specific failures, for example, you might use tools like **jq** tooquery things a bit more precisely, such as which individual failures you need toocorrect.</span></span> <span data-ttu-id="f7486-305">Hello siguiente ejemplo se utiliza **jq** tooparse una implementación de registro para **lbgroup**, que buscan errores.</span><span class="sxs-lookup"><span data-stu-id="f7486-305">hello following example uses **jq** tooparse a deployment log for **lbgroup**, looking for failures.</span></span>

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
<span data-ttu-id="f7486-306">Puede detectar rápidamente qué salió mal, corregirlo y volver a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="f7486-306">You can discover very quickly what went wrong, fix, and retry.</span></span> <span data-ttu-id="f7486-307">Hola después de case, plantilla de hello tenía ha crear dos máquinas virtuales en hello mismo tiempo, lo que crea un bloqueo en .vhd Hola.</span><span class="sxs-lookup"><span data-stu-id="f7486-307">In hello following case, hello template had been creating two VMs at hello same time, which created a lock on hello .vhd.</span></span> <span data-ttu-id="f7486-308">(Después de que se modificó la plantilla de hello, Hola se implementó correctamente rápidamente.)</span><span class="sxs-lookup"><span data-stu-id="f7486-308">(After we modified hello template, hello deployment succeeded quickly.)</span></span>

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"hello resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed tooacquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <span data-ttu-id="f7486-309"><a id="display-information-about-a-virtual-machine"></a>Tarea: Visualización de información sobre una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="f7486-309"><a id="display-information-about-a-virtual-machine"></a>Task: Display information about a virtual machine</span></span>
<span data-ttu-id="f7486-310">Puede ver información sobre máquinas virtuales específicas en el grupo de recursos mediante el uso de hello `azure vm show <groupname> <vmname>` comando.</span><span class="sxs-lookup"><span data-stu-id="f7486-310">You can see information about specific VMs in your resource group by using hello `azure vm show <groupname> <vmname>` command.</span></span> <span data-ttu-id="f7486-311">Si tiene más de una máquina virtual en el grupo, en primer lugar deberá hello toolist máquinas virtuales en un grupo mediante el uso de `azure vm list <groupname>`.</span><span class="sxs-lookup"><span data-stu-id="f7486-311">If you have more than one VM in your group, you might first need toolist hello VMs in a group by using `azure vm list <groupname>`.</span></span>

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

<span data-ttu-id="f7486-312">Y, después, buscar myVM1:</span><span class="sxs-lookup"><span data-stu-id="f7486-312">And then, looking up myVM1:</span></span>

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up hello VM "myVM1"
+ Looking up hello NIC "nic1"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Failed
data:    Name                            :myVM1
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :MicrosoftWindowsServer
data:        Offer                       :WindowsServer
data:        Sku                         :2012-R2-Datacenter
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Windows
data:        Name                        :osdisk
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :http://zoostorageralph.blob.core.windows.net/vhds/osdisk.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Windows Configuration:
data:        Provision VM Agent          :true
data:        Enable automatic updates    :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Network/networkInterfaces/nic1
data:          Primary                   :false
data:          Provisioning State        :Succeeded
data:          Name                      :nic1
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.0.5
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/availabilitySets/MYAVSET
info:    vm show command OK
```

> [!NOTE]
> <span data-ttu-id="f7486-313">Si desea que el almacén de tooprogrammatically y manipular el resultado de hello de los comandos de la consola, quizá le interese toouse un análisis de JSON herramienta como  **[jq](https://github.com/stedolan/jq)**  o  **[jsawk](https://github.com/micha/jsawk)** , o bibliotecas de lenguaje que son buenas para la tarea hello.</span><span class="sxs-lookup"><span data-stu-id="f7486-313">If you want tooprogrammatically store and manipulate hello output of your console commands, you may want toouse a JSON parsing tool such as **[jq](https://github.com/stedolan/jq)** or **[jsawk](https://github.com/micha/jsawk)**, or language libraries that are good for hello task.</span></span>
>
>

## <span data-ttu-id="f7486-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Tarea: Inicie sesión en la máquina virtual basadas en Linux de tooa</span><span class="sxs-lookup"><span data-stu-id="f7486-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Task: Log on tooa Linux-based virtual machine</span></span>
<span data-ttu-id="f7486-315">Las máquinas de Linux no suelen toothrough conectado SSH.</span><span class="sxs-lookup"><span data-stu-id="f7486-315">Typically Linux machines are connected toothrough SSH.</span></span> <span data-ttu-id="f7486-316">Para obtener más información, consulte [cómo toouse SSH con Linux en Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7486-316">For more information, see [How toouse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <span data-ttu-id="f7486-317"><a id="stop-a-virtual-machine"></a>Tarea: Detención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="f7486-317"><a id="stop-a-virtual-machine"></a>Task: Stop a VM</span></span>
<span data-ttu-id="f7486-318">Ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="f7486-318">Run this command:</span></span>

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> <span data-ttu-id="f7486-319">Utilice este parámetro tookeep Hola dirección IP virtual (VIP) de red virtual de hello en caso de que sea Hola última VM en esa red virtual.</span><span class="sxs-lookup"><span data-stu-id="f7486-319">Use this parameter tookeep hello virtual IP (VIP) of hello vnet in case it's hello last VM in that vnet.</span></span> <br><br> <span data-ttu-id="f7486-320">Si usas hello `StayProvisioned` parámetro, le facturará aún por hello VM.</span><span class="sxs-lookup"><span data-stu-id="f7486-320">If you use hello `StayProvisioned` parameter, you'll still be billed for hello VM.</span></span>
>
>

## <span data-ttu-id="f7486-321"><a id="start-a-virtual-machine"></a>Tarea: Inicio de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="f7486-321"><a id="start-a-virtual-machine"></a>Task: Start a VM</span></span>
<span data-ttu-id="f7486-322">Ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="f7486-322">Run this command:</span></span>

```azurecli
azure vm start <group name> <virtual machine name>
```

## <span data-ttu-id="f7486-323"><a id="attach-a-data-disk"></a>Tarea: Acoplamiento de un disco de datos</span><span class="sxs-lookup"><span data-stu-id="f7486-323"><a id="attach-a-data-disk"></a>Task: Attach a data disk</span></span>
<span data-ttu-id="f7486-324">También necesitará toodecide si tooattach un disco nuevo o uno que contiene datos.</span><span class="sxs-lookup"><span data-stu-id="f7486-324">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="f7486-325">Para un disco nuevo, comando hello, crea el archivo .vhd de hello y lo adjunta Hola mismo comando.</span><span class="sxs-lookup"><span data-stu-id="f7486-325">For a new disk, hello command creates hello .vhd file and attaches it in hello same command.</span></span>

<span data-ttu-id="f7486-326">tooattach un disco nuevo, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="f7486-326">tooattach a new disk, run this command:</span></span>

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

<span data-ttu-id="f7486-327">tooattach un disco de datos existente, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="f7486-327">tooattach an existing data disk, run this command:</span></span>

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

<span data-ttu-id="f7486-328">A continuación, necesitará toomount disco de hello, tal y como lo haría normalmente en Linux.</span><span class="sxs-lookup"><span data-stu-id="f7486-328">Then you'll need toomount hello disk, as you normally would in Linux.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7486-329">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f7486-329">Next steps</span></span>
<span data-ttu-id="f7486-330">Para obtener mucha más ejemplos de uso de la CLI de Azure con hello **arm** modo, vea [Using Hola CLI de Azure para Mac, Linux y Windows con el Administrador de recursos de Azure](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f7486-330">For far more examples of Azure CLI usage with hello **arm** mode, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span></span> <span data-ttu-id="f7486-331">toolearn más información acerca de los recursos de Azure y sus conceptos, vea [Introducción a Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f7486-331">toolearn more about Azure resources and their concepts, see [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="f7486-332">Para ver más plantillas que puede usar, consulte [Plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/) e [Implementación de marcos de aplicaciones conocidos mediante plantillas de Azure Resource Manager](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7486-332">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/) and [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
