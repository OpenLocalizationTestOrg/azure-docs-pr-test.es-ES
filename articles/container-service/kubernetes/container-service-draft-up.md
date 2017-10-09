---
title: aaaUse borrador con registro de contenedor de Azure y el servicio de contenedor de Azure | Documentos de Microsoft
description: "Crear un clúster de ACS Kubernetes y un registro de contenedor de Azure toocreate su primera aplicación en Azure con Borrador."
services: container-service
documentationcenter: 
author: squillace
manager: gamonroy
editor: 
tags: draft, helm, acs, azure-container-service
keywords: Docker, contenedores, microservicios, Kubernetes, Draft, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: f5e21cda01e5e8452bf86a5c8fa458904d89f451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-toobuild-and-deploy-an-application-tookubernetes"></a><span data-ttu-id="9745e-104">Usar borrador con toobuild de servicio de contenedor de Azure y el registro de contenedor de Azure e implementar una aplicación tooKubernetes</span><span class="sxs-lookup"><span data-stu-id="9745e-104">Use Draft with Azure Container Service and Azure Container Registry toobuild and deploy an application tooKubernetes</span></span>

<span data-ttu-id="9745e-105">[Borrador](https://aka.ms/draft) es una nueva herramienta de código abierto que hace más fácil toodevelop aplicaciones contenedor e implementarlas tooKubernetes clústeres sin saber mucho sobre Docker y Kubernetes--o incluso su instalación.</span><span class="sxs-lookup"><span data-stu-id="9745e-105">[Draft](https://aka.ms/draft) is a new open-source tool that makes it easy toodevelop container-based applications and deploy them tooKubernetes clusters without knowing much about Docker and Kubernetes -- or even installing them.</span></span> <span data-ttu-id="9745e-106">Con herramientas como borrador permite a su enfoque de los equipos compilación aplicación hello con Kubernetes, no se presta tanta tooinfrastructure atención.</span><span class="sxs-lookup"><span data-stu-id="9745e-106">Using tools like Draft let you and your teams focus on building hello application with Kubernetes, not paying as much attention tooinfrastructure.</span></span>

<span data-ttu-id="9745e-107">Puede usar Draft con cualquier registro de imágenes de Docker y cualquier clúster de Kubernetes, incluidos los locales.</span><span class="sxs-lookup"><span data-stu-id="9745e-107">You can use Draft with any Docker image registry and any Kubernetes cluster, including locally.</span></span> <span data-ttu-id="9745e-108">Este tutorial muestra cómo toouse ACS con toocreate Kubernetes, ACR y DNS de Azure, un desarrollador de CI/CD en vivo de canalización con Borrador.</span><span class="sxs-lookup"><span data-stu-id="9745e-108">This tutorial shows how toouse ACS with Kubernetes, ACR, and Azure DNS toocreate a live CI/CD developer pipeline using Draft.</span></span>


## <a name="create-an-azure-container-registry"></a><span data-ttu-id="9745e-109">Creación de una instancia de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="9745e-109">Create an Azure Container Registry</span></span>
<span data-ttu-id="9745e-110">Le resultará muy fácil [crear un nuevo registro de contenedor de Azure](../../container-registry/container-registry-get-started-azure-cli.md), pero Hola pasos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="9745e-110">You can easily [create a new Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md), but hello steps are as follows:</span></span>

1. <span data-ttu-id="9745e-111">Crear un toomanage de grupo de recursos de Azure en el clúster de Kubernetes de hello y del registro ACR en ACS.</span><span class="sxs-lookup"><span data-stu-id="9745e-111">Create a Azure resource group toomanage your ACR registry and hello Kubernetes cluster in ACS.</span></span>
      ```azurecli
      az group create --name draft --location eastus
      ```

2. <span data-ttu-id="9745e-112">Cree un registro de imagen ACR con [az acr create](/cli/azure/acr#create)</span><span class="sxs-lookup"><span data-stu-id="9745e-112">Create an ACR image registry using [az acr create](/cli/azure/acr#create)</span></span>
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a><span data-ttu-id="9745e-113">Creación de Azure Container Service mediante Kubernetes</span><span class="sxs-lookup"><span data-stu-id="9745e-113">Create an Azure Container Service with Kubernetes</span></span>

<span data-ttu-id="9745e-114">Ahora está listo toouse [az acs crear](/cli/azure/acs#create) clúster toocreate un ACS utilizando Kubernetes como hello `--orchestrator-type` valor.</span><span class="sxs-lookup"><span data-stu-id="9745e-114">Now you're ready toouse [az acs create](/cli/azure/acs#create) toocreate an ACS cluster using Kubernetes as hello `--orchestrator-type` value.</span></span>
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> <span data-ttu-id="9745e-115">Porque Kubernetes no tiene tipos de orchestrator de hello predeterminado, asegúrese de usar hello `--orchestrator-type kubernetes` cambiar.</span><span class="sxs-lookup"><span data-stu-id="9745e-115">Because Kubernetes is not hello default orchestrator type, be sure you use hello `--orchestrator-type kubernetes` switch.</span></span>

<span data-ttu-id="9745e-116">salida de Hello cuando se realiza correctamente es similar a continuación toohello.</span><span class="sxs-lookup"><span data-stu-id="9745e-116">hello output when successful looks similar toohello following.</span></span>

```json
waiting for AAD role toopropagate.done
{
  "id": "/subscriptions/<guid>/resourceGroups/draft/providers/Microsoft.Resources/deployments/azurecli14904.93snip09",
  "name": "azurecli1496227204.9323909",
  "properties": {
    "correlationId": "<guid>",
    "debugSetting": null,
    "dependencies": [],
    "mode": "Incremental",
    "outputs": null,
    "parameters": {
      "clientSecret": {
        "type": "SecureString"
      }
    },
    "parametersLink": null,
    "providers": [
      {
        "id": null,
        "namespace": "Microsoft.ContainerService",
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "locations": [
              "westus"
            ],
            "properties": null,
            "resourceType": "containerServices"
          }
        ]
      }
    ],
    "provisioningState": "Succeeded",
    "template": null,
    "templateLink": null,
    "timestamp": "2017-05-31T10:46:29.434095+00:00"
  },
  "resourceGroup": "draft"
}
```

<span data-ttu-id="9745e-117">Ahora que tiene un clúster, puede importar las credenciales de hello mediante hello [az kubernetes get-credenciales de acs](/cli/azure/acs/kubernetes#get-credentials) comando.</span><span class="sxs-lookup"><span data-stu-id="9745e-117">Now that you have a cluster, you can import hello credentials by using hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="9745e-118">Ahora tiene un archivo de configuración local para el clúster, que es qué timón y un borrador necesitan tooget su trabajo.</span><span class="sxs-lookup"><span data-stu-id="9745e-118">Now you have a local configuration file for your cluster, which is what Helm and Draft need tooget their work done.</span></span>

## <a name="install-and-configure-draft"></a><span data-ttu-id="9745e-119">Instalación y configuración de Draft</span><span class="sxs-lookup"><span data-stu-id="9745e-119">Install and configure draft</span></span>
<span data-ttu-id="9745e-120">instrucciones de instalación de Hola de borrador que se encuentran en hello [repositorio de borrador](https://github.com/Azure/draft/blob/master/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="9745e-120">hello installation instructions for Draft are in hello [Draft repository](https://github.com/Azure/draft/blob/master/docs/install.md).</span></span> <span data-ttu-id="9745e-121">Son relativamente simples, pero requiere cierta configuración, ya que depende de [timón](https://aka.ms/helm) toocreate e implementar un gráfico de timón en clúster de Kubernetes Hola.</span><span class="sxs-lookup"><span data-stu-id="9745e-121">They are relatively simple, but do require some configuration, as it depends on [Helm](https://aka.ms/helm) toocreate and deploy a Helm chart into hello Kubernetes cluster.</span></span>

1. <span data-ttu-id="9745e-122">[Descarga e instalación de Helm](https://aka.ms/helm#install).</span><span class="sxs-lookup"><span data-stu-id="9745e-122">[Download and install Helm](https://aka.ms/helm#install).</span></span>
2. <span data-ttu-id="9745e-123">Utilice toosearch timón para e instale `stable/traefik`y entrada controlador tooenable las solicitudes para las compilaciones de entrada.</span><span class="sxs-lookup"><span data-stu-id="9745e-123">Use Helm toosearch for and install `stable/traefik`, and ingress controller tooenable inbound requests for your builds.</span></span>
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    <span data-ttu-id="9745e-124">Ahora se establece una inspección en hello `ingress` controlador toocapture Hola IP valor externo cuando se implementa.</span><span class="sxs-lookup"><span data-stu-id="9745e-124">Now set a watch on hello `ingress` controller toocapture hello external IP value when it is deployed.</span></span> <span data-ttu-id="9745e-125">Esta dirección IP será Hola uno [asignado tooyour implementación dominio](#wire-up-deployment-domain) en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="9745e-125">This IP address will be hello one [mapped tooyour deployment domain](#wire-up-deployment-domain) in hello next section.</span></span>

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    <span data-ttu-id="9745e-126">En este caso, Hola direcciones IP externas de dominio de la implementación de hello es `13.64.108.240`.</span><span class="sxs-lookup"><span data-stu-id="9745e-126">In this case, hello external IP for hello deployment domain is `13.64.108.240`.</span></span> <span data-ttu-id="9745e-127">Ahora puede asignar la IP de toothat de dominio.</span><span class="sxs-lookup"><span data-stu-id="9745e-127">Now you can map your domain toothat IP.</span></span>

## <a name="wire-up-deployment-domain"></a><span data-ttu-id="9745e-128">Conexión del dominio de implementación</span><span class="sxs-lookup"><span data-stu-id="9745e-128">Wire up deployment domain</span></span>

<span data-ttu-id="9745e-129">Draft crea una versión para cada gráfico de Helm que crea: cada aplicación en la que esté trabajando.</span><span class="sxs-lookup"><span data-stu-id="9745e-129">Draft creates a release for each Helm chart it creates -- each application you are working on.</span></span> <span data-ttu-id="9745e-130">Cada uno obtiene un nombre generado que se usa por borrador como un _subdominio_ encima de la raíz de hello _dominio implementación_ que usted controla.</span><span class="sxs-lookup"><span data-stu-id="9745e-130">Each one gets a generated name that is used by draft as a _subdomain_ on top of hello root _deployment domain_ that you control.</span></span> <span data-ttu-id="9745e-131">(En este ejemplo, utilizamos `squillace.io` como dominio de implementación de hello.) tooenable este comportamiento subdominio, debe crear un registro a para `'*'` las entradas de DNS para el dominio de la implementación, para que cada uno de ellos genere subdominio es enrutado toohello Kubernetes controlador de entrada del clúster.</span><span class="sxs-lookup"><span data-stu-id="9745e-131">(In this example, we use `squillace.io` as hello deployment domain.) tooenable this subdomain behavior, you must create an A record for `'*'` in your DNS entries for your deployment domain, so that each generated subdomain is routed toohello Kubernetes cluster's ingress controller.</span></span>

<span data-ttu-id="9745e-132">Su propio proveedor de dominio tiene sus propios servidores DNS de manera tooassign; demasiado[delegar su tooAzure de servidores de nombres de dominio DNS](../../dns/dns-delegate-domain-azure-dns.md), tomar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9745e-132">Your own domain provider has their own way tooassign DNS servers; too[delegate your domain nameservers tooAzure DNS](../../dns/dns-delegate-domain-azure-dns.md), you take hello following steps:</span></span>

1. <span data-ttu-id="9745e-133">Cree un grupo de recursos para su zona.</span><span class="sxs-lookup"><span data-stu-id="9745e-133">Create a resource group for your zone.</span></span>
    ```azurecli
    az group create --name squillace.io --location eastus
    {
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io",
      "location": "eastus",
      "managedBy": null,
      "name": "zones",
      "properties": {
        "provisioningState": "Succeeded"
      },
      "tags": null
    }
    ```

2. <span data-ttu-id="9745e-134">Cree una zona DNS para su dominio.</span><span class="sxs-lookup"><span data-stu-id="9745e-134">Create a DNS zone for your domain.</span></span>
<span data-ttu-id="9745e-135">Hola de uso [crear zona de dns de red az](/cli/azure/network/dns/zone#create) comando tooobtain Hola servidores de nombres toodelegate DNS controlar tooAzure DNS para su dominio.</span><span class="sxs-lookup"><span data-stu-id="9745e-135">Use hello [az network dns zone create](/cli/azure/network/dns/zone#create) command tooobtain hello nameservers toodelegate DNS control tooAzure DNS for your domain.</span></span>
    ```azurecli
    az network dns zone create --resource-group squillace.io --name squillace.io
    {
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/zones/providers/Microsoft.Network/dnszones/squillace.io",
      "location": "global",
      "maxNumberOfRecordSets": 5000,
      "name": "squillace.io",
      "nameServers": [
        "ns1-09.azure-dns.com.",
        "ns2-09.azure-dns.net.",
        "ns3-09.azure-dns.org.",
        "ns4-09.azure-dns.info."
      ],
      "numberOfRecordSets": 2,
      "resourceGroup": "squillace.io",
      "tags": {},
      "type": "Microsoft.Network/dnszones"
    }
    ```
3. <span data-ttu-id="9745e-136">Agregar servidores DNS de hello que tendrá toohello los proveedores de dominio para el dominio de la implementación, lo que permite toorepoint DNS de Azure toouse su dominio como desee.</span><span class="sxs-lookup"><span data-stu-id="9745e-136">Add hello DNS servers you are given toohello domain provider for your deployment domain, which enables you toouse Azure DNS toorepoint your domain as you want.</span></span>
4. <span data-ttu-id="9745e-137">Crear una entrada de conjunto de registros A para su toohello de asignación de dominio de implementación `ingress` IP del paso 2 de la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="9745e-137">Create an A record-set entry for your deployment domain mapping toohello `ingress` IP from step 2 of hello previous section.</span></span>
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
<span data-ttu-id="9745e-138">salida de Hello es similar:</span><span class="sxs-lookup"><span data-stu-id="9745e-138">hello output looks something like:</span></span>
    ```json
    {
      "arecords": [
        {
          "ipv4Address": "13.64.108.240"
        }
      ],
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io/providers/Microsoft.Network/dnszones/squillace.io/A/*",
      "metadata": null,
      "name": "*",
      "resourceGroup": "squillace.io",
      "ttl": 3600,
      "type": "Microsoft.Network/dnszones/A"
    }
    ```

5. <span data-ttu-id="9745e-139">Configurar el registro de borrador toouse y crear subdominios para cada gráfico timón crea.</span><span class="sxs-lookup"><span data-stu-id="9745e-139">Configure Draft toouse your registry and create subdomains for each Helm chart it creates.</span></span> <span data-ttu-id="9745e-140">tooconfigure borrador, se necesita:</span><span class="sxs-lookup"><span data-stu-id="9745e-140">tooconfigure Draft, you need:</span></span>
  - <span data-ttu-id="9745e-141">el nombre de Azure Container Registry (en este ejemplo, `draft`)</span><span class="sxs-lookup"><span data-stu-id="9745e-141">your Azure Container Registry name (in this example, `draft`)</span></span>
  - <span data-ttu-id="9745e-142">la clave del registro, o la contraseña, de `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span><span class="sxs-lookup"><span data-stu-id="9745e-142">your registry key, or password, from `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span></span>
  - <span data-ttu-id="9745e-143">dominio de implementación de Hello raíz que ha configurado la dirección IP externa de toomap toohello Kubernetes entrada (en este caso, `squillace.io`)</span><span class="sxs-lookup"><span data-stu-id="9745e-143">hello root deployment domain that you have configured toomap toohello Kubernetes ingress external IP address (here, `squillace.io`)</span></span>

  <span data-ttu-id="9745e-144">Llame a `draft init` y proceso de configuración de hello solicita valores de hello indicados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9745e-144">Call `draft init` and hello configuration process prompts you for hello values above.</span></span> <span data-ttu-id="9745e-145">proceso de Hello parece algo siguiente Hola Hola primera vez que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="9745e-145">hello process looks something like hello following hello first time you run it.</span></span>
 ```bash
    $ draft init
    Creating pack ruby...
    Creating pack node...
    Creating pack gradle...
    Creating pack maven...
    Creating pack php...
    Creating pack python...
    Creating pack dotnetcore...
    Creating pack golang...
    $DRAFT_HOME has been configured at /Users/ralphsquillace/.draft.

    In order tooinstall Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

<span data-ttu-id="9745e-146">Ahora está listo toodeploy una aplicación.</span><span class="sxs-lookup"><span data-stu-id="9745e-146">Now you're ready toodeploy an application.</span></span>


## <a name="build-and-deploy-an-application"></a><span data-ttu-id="9745e-147">Compilación e implementación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="9745e-147">Build and deploy an application</span></span>

<span data-ttu-id="9745e-148">En el repositorio de borrador de hello son [seis de las aplicaciones de ejemplo simple](https://github.com/Azure/draft/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="9745e-148">In hello Draft repo are [six simple example applications](https://github.com/Azure/draft/tree/master/examples).</span></span> <span data-ttu-id="9745e-149">Clonar el repositorio de Hola y vamos a usar hello [ejemplo de Python](https://github.com/Azure/draft/tree/master/examples/python).</span><span class="sxs-lookup"><span data-stu-id="9745e-149">Clone hello repo and let's use hello [Python example](https://github.com/Azure/draft/tree/master/examples/python).</span></span> <span data-ttu-id="9745e-150">Cambiar en el directorio de ejemplos/Python hello y escriba `draft create` aplicación de hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="9745e-150">Change into hello examples/Python directory, and type `draft create` toobuild hello application.</span></span> <span data-ttu-id="9745e-151">Debería ser similar el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9745e-151">It should look like hello following example.</span></span>
```bash
$ draft create
--> Python app detected
--> Ready toosail
```

<span data-ttu-id="9745e-152">salida de Hello incluye un archivo Dockerfile y un gráfico de timón.</span><span class="sxs-lookup"><span data-stu-id="9745e-152">hello output includes a Dockerfile and a Helm chart.</span></span> <span data-ttu-id="9745e-153">toobuild e implementar, simplemente escriba `draft up`.</span><span class="sxs-lookup"><span data-stu-id="9745e-153">toobuild and deploy, you just type `draft up`.</span></span> <span data-ttu-id="9745e-154">salida de Hello es extensa, pero se inicia como el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9745e-154">hello output is extensive, but begins like hello following example.</span></span>
```bash
$ draft up
--> Building Dockerfile
Step 1 : FROM python:onbuild
onbuild: Pulling from library/python
10a267c67f42: Pulling fs layer
fb5937da9414: Pulling fs layer
9021b2326a1e: Pulling fs layer
dbed9b09434e: Pulling fs layer
ea8a37f15161: Pulling fs layer
<snip>
```

<span data-ttu-id="9745e-155">y cuando finaliza correctamente con algo similar toohello siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9745e-155">and when successful ends with something similar toohello following example.</span></span>
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying tooKubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io tooaccess your application

Watching local files for changes...
```

<span data-ttu-id="9745e-156">Lo que es el nombre de su gráfico, ahora puede `curl http://gangly-bronco.squillace.io` tooreceive respuesta de hello, `Hello World!`.</span><span class="sxs-lookup"><span data-stu-id="9745e-156">Whatever your chart's name is, you can now `curl http://gangly-bronco.squillace.io` tooreceive hello reply, `Hello World!`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9745e-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9745e-157">Next steps</span></span>

<span data-ttu-id="9745e-158">Ahora que tiene un clúster de ACS Kubernetes, puede investigar mediante [registro de contenedor de Azure](../../container-registry/container-registry-intro.md) toocreate más y diferentes implementaciones de este escenario.</span><span class="sxs-lookup"><span data-stu-id="9745e-158">Now that you have an ACS Kubernetes cluster, you can investigate using [Azure Container Registry](../../container-registry/container-registry-intro.md) toocreate more and different deployments of this scenario.</span></span> <span data-ttu-id="9745e-159">Por ejemplo, puede crear un conjunto de registros DNS de dominios draft._basedomain.toplevel_ que controle aspectos de un subdominio más profundo para implementaciones de ACS específicas.</span><span class="sxs-lookup"><span data-stu-id="9745e-159">For example, you can create a draft._basedomain.toplevel_ domain DNS record-set that controls things off of a deeper subdomain for specific ACS deployments.</span></span>






