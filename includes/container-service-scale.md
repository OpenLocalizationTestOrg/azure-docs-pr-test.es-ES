# <a name="scale-agent-nodes-in-a-container-service-cluster"></a><span data-ttu-id="534cc-101">Escalado de nodos de agente en un clúster de Container Service</span><span class="sxs-lookup"><span data-stu-id="534cc-101">Scale agent nodes in a Container Service cluster</span></span>
<span data-ttu-id="534cc-102">Después de [implementación de un clúster de servicio de contenedor de Azure](../articles/container-service/dcos-swarm/container-service-deployment.md), tendrá que número de hello toochange de nodos de agente.</span><span class="sxs-lookup"><span data-stu-id="534cc-102">After [deploying an Azure Container Service cluster](../articles/container-service/dcos-swarm/container-service-deployment.md), you might need toochange hello number of agent nodes.</span></span> <span data-ttu-id="534cc-103">Por ejemplo, puede que necesite más agentes para poder ejecutar más aplicaciones o instancias de contenedor.</span><span class="sxs-lookup"><span data-stu-id="534cc-103">For example, you might need more agents so you can run more container applications or instances.</span></span> 

<span data-ttu-id="534cc-104">Puede cambiar número de Hola de nodos de agente en un clúster de DC/OS, Docker Swarm o Kubernetes con hello portal de Azure u Hola 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="534cc-104">You can change hello number of agent nodes in a DC/OS, Docker Swarm, or Kubernetes cluster by using hello Azure portal or hello Azure CLI 2.0.</span></span> 

## <a name="scale-with-hello-azure-portal"></a><span data-ttu-id="534cc-105">Escalar con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="534cc-105">Scale with hello Azure portal</span></span>

1. <span data-ttu-id="534cc-106">Hola [portal de Azure](https://portal.azure.com), busque **servicios de contenedor**y, a continuación, haga clic en servicio de contenedor de Hola que desea toomodify.</span><span class="sxs-lookup"><span data-stu-id="534cc-106">In hello [Azure portal](https://portal.azure.com), browse for **Container services**, and then click hello container service that you want toomodify.</span></span>
2. <span data-ttu-id="534cc-107">Hola **servicio de contenedor** hoja, haga clic en **agentes**.</span><span class="sxs-lookup"><span data-stu-id="534cc-107">In hello **Container service** blade, click **Agents**.</span></span>
3. <span data-ttu-id="534cc-108">En **recuento de VM**, escriba Hola deseado número de nodos de agentes.</span><span class="sxs-lookup"><span data-stu-id="534cc-108">In **VM Count**, enter hello desired number of agents nodes.</span></span>

    ![Escalar un grupo en el portal de Hola](./media/container-service-scale/container-service-scale-portal.png)

4. <span data-ttu-id="534cc-110">configuración de hello toosave, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="534cc-110">toosave hello configuration, click **Save**.</span></span>

## <a name="scale-with-hello-azure-cli-20"></a><span data-ttu-id="534cc-111">Escalar con hello 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="534cc-111">Scale with hello Azure CLI 2.0</span></span>

<span data-ttu-id="534cc-112">Asegúrese de que se [instalado](/cli/azure/install-az-cli2) Hola 2.0 más reciente de CLI de Azure y registran en tooan cuenta de azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="534cc-112">Make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan azure account (`az login`).</span></span>

### <a name="see-hello-current-agent-count"></a><span data-ttu-id="534cc-113">Vea el número de agentes de hello actual</span><span class="sxs-lookup"><span data-stu-id="534cc-113">See hello current agent count</span></span>
<span data-ttu-id="534cc-114">número de hello toosee de agentes actualmente en clúster de hello, ejecute hello `az acs show` comando.</span><span class="sxs-lookup"><span data-stu-id="534cc-114">toosee hello number of agents currently in hello cluster, run hello `az acs show` command.</span></span> <span data-ttu-id="534cc-115">Esto muestra la configuración de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="534cc-115">This shows hello cluster configuration.</span></span> <span data-ttu-id="534cc-116">Por ejemplo, Hola siguiente comando muestra Hola configuración del servicio de contenedor de hello denominado `containerservice-myACSName` en grupo de recursos de Hola `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="534cc-116">For example, hello following command shows hello configuration of hello container service named `containerservice-myACSName` in hello resource group `myResourceGroup`:</span></span>

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

<span data-ttu-id="534cc-117">comando Hello devuelve el número de Hola de agentes de hello `Count` valor bajo `AgentPoolProfiles`.</span><span class="sxs-lookup"><span data-stu-id="534cc-117">hello command returns hello number of agents in hello `Count` value under `AgentPoolProfiles`.</span></span>

### <a name="use-hello-az-acs-scale-command"></a><span data-ttu-id="534cc-118">Use Hola az comandos de escala de acs</span><span class="sxs-lookup"><span data-stu-id="534cc-118">Use hello az acs scale command</span></span>
<span data-ttu-id="534cc-119">número de hello toochange de nodos de agente, ejecute hello `az acs scale` comando y proporcione hello **grupo de recursos**, **el nombre del servicio de contenedor**, hello deseado y **nuevo número de agentes**.</span><span class="sxs-lookup"><span data-stu-id="534cc-119">toochange hello number of agent nodes, run hello `az acs scale` command and supply hello **resource group**, **container service name**, and hello desired **new agent count**.</span></span> <span data-ttu-id="534cc-120">Con un número mayor o menor, puede reducir o aumentar verticalmente, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="534cc-120">By using a smaller or higher number, you can scale down or up, respectively.</span></span>

<span data-ttu-id="534cc-121">Por ejemplo, número de hello toochange de agentes en hello too10 de clúster anterior, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="534cc-121">For example, toochange hello number of agents in hello previous cluster too10, type hello following command:</span></span>

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

<span data-ttu-id="534cc-122">Hola 2.0 de CLI de Azure devuelve una cadena JSON que representa la nueva configuración del servicio de contenedor de hello, incluido el nuevo número de agentes Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="534cc-122">hello Azure CLI 2.0 returns a JSON string representing hello new configuration of hello container service, including hello new agent count.</span></span>

<span data-ttu-id="534cc-123">Para obtener más opciones de comando, ejecute `az acs scale --help`.</span><span class="sxs-lookup"><span data-stu-id="534cc-123">For more command options, run `az acs scale --help`.</span></span>

## <a name="scaling-considerations"></a><span data-ttu-id="534cc-124">Consideraciones sobre escalado</span><span class="sxs-lookup"><span data-stu-id="534cc-124">Scaling considerations</span></span>

* <span data-ttu-id="534cc-125">número de Hola de nodos de agente debe estar entre 1 y 100, ambos inclusive.</span><span class="sxs-lookup"><span data-stu-id="534cc-125">hello number of agent nodes must be between 1 and 100, inclusive.</span></span> 

* <span data-ttu-id="534cc-126">Su cuota de núcleos puede limitar el número de Hola de nodos de agente en un clúster.</span><span class="sxs-lookup"><span data-stu-id="534cc-126">Your cores quota can limit hello number of agent nodes in a cluster.</span></span>

* <span data-ttu-id="534cc-127">Las operaciones de escalado de nodo de agente son el conjunto de escalas de máquina virtual de Azure tooan aplicados que contiene el grupo de agente de Hola.</span><span class="sxs-lookup"><span data-stu-id="534cc-127">Agent node scaling operations are applied tooan Azure virtual machine scale set that contains hello agent pool.</span></span> <span data-ttu-id="534cc-128">En un clúster de DC/OS, solo los nodos de agente de grupo privada Hola se escalan por operaciones de Hola que se muestran en este artículo.</span><span class="sxs-lookup"><span data-stu-id="534cc-128">In a DC/OS cluster, only agent nodes in hello private pool are scaled by hello operations shown in this article.</span></span>

* <span data-ttu-id="534cc-129">Función de orchestrator de Hola que se implementan en el clúster, puede escalar por separado número Hola de instancias de un contenedor que se ejecuta en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="534cc-129">Depending on hello orchestrator you deploy in your cluster, you can separately scale hello number of instances of a container running on hello cluster.</span></span> <span data-ttu-id="534cc-130">Por ejemplo, en un clúster de DC/OS, usar hello [interfaz de usuario de maratón](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) número de hello toochange de instancias de una aplicación de contenedor.</span><span class="sxs-lookup"><span data-stu-id="534cc-130">For example, in a DC/OS cluster, use hello [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello number of instances of a container application.</span></span>

* <span data-ttu-id="534cc-131">Actualmente, no se admite el escalado automático de nodos de agente en un clúster de servicio de contenedores.</span><span class="sxs-lookup"><span data-stu-id="534cc-131">Currently, autoscaling of agent nodes in a container service cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="534cc-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="534cc-132">Next steps</span></span>
* <span data-ttu-id="534cc-133">Consulte [más ejemplos](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) de uso de comandos de la CLI de Azure 2.0 con Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="534cc-133">See [more examples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) of using Azure CLI 2.0 commands with Azure Container Service.</span></span>
* <span data-ttu-id="534cc-134">Aprenda más sobre los [grupos de agentes de DC/OS](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) en Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="534cc-134">Learn more about [DC/OS agent pools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span></span>

