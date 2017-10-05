---
title: Uso de Draft con Azure Container Service y Azure Container Registry | Microsoft Docs
description: "Creación de un clúster de ACS Kubernetes y Azure Container Registry para crear la primera aplicación en Azure con Draft."
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
ms.openlocfilehash: e7e3ea461145571753a1a6d768b52118dcbfb507
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-to-build-and-deploy-an-application-to-kubernetes"></a><span data-ttu-id="3be61-104">Uso de Draft con Azure Container Service y Azure Container Registry para crear e implementar una aplicación en Kubernetes</span><span class="sxs-lookup"><span data-stu-id="3be61-104">Use Draft with Azure Container Service and Azure Container Registry to build and deploy an application to Kubernetes</span></span>

<span data-ttu-id="3be61-105">[Draft](https://aka.ms/draft) es una nueva herramienta de código abierto que facilita el desarrollo de aplicaciones basadas en contenedores y su implementación en clústeres de Kubernetes sin necesidad de tener un gran conocimiento sobre Docker y Kubernetes, o incluso su instalación.</span><span class="sxs-lookup"><span data-stu-id="3be61-105">[Draft](https://aka.ms/draft) is a new open-source tool that makes it easy to develop container-based applications and deploy them to Kubernetes clusters without knowing much about Docker and Kubernetes -- or even installing them.</span></span> <span data-ttu-id="3be61-106">Con herramientas como Draft, usted y su equipo pueden centrarse en la creación de la aplicación con Kubernetes, sin tener que prestar mucha atención a la infraestructura.</span><span class="sxs-lookup"><span data-stu-id="3be61-106">Using tools like Draft let you and your teams focus on building the application with Kubernetes, not paying as much attention to infrastructure.</span></span>

<span data-ttu-id="3be61-107">Puede usar Draft con cualquier registro de imágenes de Docker y cualquier clúster de Kubernetes, incluidos los locales.</span><span class="sxs-lookup"><span data-stu-id="3be61-107">You can use Draft with any Docker image registry and any Kubernetes cluster, including locally.</span></span> <span data-ttu-id="3be61-108">Este tutorial muestra cómo utilizar ACS con Kubernetes, ACR y Azure DNS para crear una canalización de desarrollador de CI/CD en vivo mediante Draft.</span><span class="sxs-lookup"><span data-stu-id="3be61-108">This tutorial shows how to use ACS with Kubernetes, ACR, and Azure DNS to create a live CI/CD developer pipeline using Draft.</span></span>


## <a name="create-an-azure-container-registry"></a><span data-ttu-id="3be61-109">Creación de una instancia de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="3be61-109">Create an Azure Container Registry</span></span>
<span data-ttu-id="3be61-110">Le resultará muy fácil [crear una nueva instancia de Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md) con los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3be61-110">You can easily [create a new Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md), but the steps are as follows:</span></span>

1. <span data-ttu-id="3be61-111">Cree un grupo de recursos de Azure para administrar el registro ACR y el clúster de Kubernetes en ACS.</span><span class="sxs-lookup"><span data-stu-id="3be61-111">Create a Azure resource group to manage your ACR registry and the Kubernetes cluster in ACS.</span></span>
      ```azurecli
      az group create --name draft --location eastus
      ```

2. <span data-ttu-id="3be61-112">Cree un registro de imagen ACR con [az acr create](/cli/azure/acr#create)</span><span class="sxs-lookup"><span data-stu-id="3be61-112">Create an ACR image registry using [az acr create](/cli/azure/acr#create)</span></span>
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a><span data-ttu-id="3be61-113">Creación de Azure Container Service mediante Kubernetes</span><span class="sxs-lookup"><span data-stu-id="3be61-113">Create an Azure Container Service with Kubernetes</span></span>

<span data-ttu-id="3be61-114">Ya está listo para usar [az acs create](/cli/azure/acs#create) y crear un clúster de ACS utilizando Kubernetes como el valor `--orchestrator-type`.</span><span class="sxs-lookup"><span data-stu-id="3be61-114">Now you're ready to use [az acs create](/cli/azure/acs#create) to create an ACS cluster using Kubernetes as the `--orchestrator-type` value.</span></span>
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> <span data-ttu-id="3be61-115">Como Kubernetes no es el tipo de orquestador predeterminado, asegúrese de utilizar el conmutador `--orchestrator-type kubernetes`.</span><span class="sxs-lookup"><span data-stu-id="3be61-115">Because Kubernetes is not the default orchestrator type, be sure you use the `--orchestrator-type kubernetes` switch.</span></span>

<span data-ttu-id="3be61-116">El resultado, cuando es correcto, es parecido al siguiente.</span><span class="sxs-lookup"><span data-stu-id="3be61-116">The output when successful looks similar to the following.</span></span>

```json
waiting for AAD role to propagate.done
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

<span data-ttu-id="3be61-117">Ahora que tiene un clúster, puede importar las credenciales mediante el comando [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials).</span><span class="sxs-lookup"><span data-stu-id="3be61-117">Now that you have a cluster, you can import the credentials by using the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="3be61-118">Ya tiene un archivo de configuración local para el clúster, que es lo que Helm y Draft necesitan para realizar su trabajo.</span><span class="sxs-lookup"><span data-stu-id="3be61-118">Now you have a local configuration file for your cluster, which is what Helm and Draft need to get their work done.</span></span>

## <a name="install-and-configure-draft"></a><span data-ttu-id="3be61-119">Instalación y configuración de Draft</span><span class="sxs-lookup"><span data-stu-id="3be61-119">Install and configure draft</span></span>
<span data-ttu-id="3be61-120">Las instrucciones de instalación de Draft se encuentran en el [repositorio de Draft](https://github.com/Azure/draft/blob/master/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="3be61-120">The installation instructions for Draft are in the [Draft repository](https://github.com/Azure/draft/blob/master/docs/install.md).</span></span> <span data-ttu-id="3be61-121">Son relativamente sencillas pero requieren cierta configuración, ya que dependen de [Helm](https://aka.ms/helm) para crear e implementar un gráfico de Helm en el clúster de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="3be61-121">They are relatively simple, but do require some configuration, as it depends on [Helm](https://aka.ms/helm) to create and deploy a Helm chart into the Kubernetes cluster.</span></span>

1. <span data-ttu-id="3be61-122">[Descarga e instalación de Helm](https://aka.ms/helm#install).</span><span class="sxs-lookup"><span data-stu-id="3be61-122">[Download and install Helm](https://aka.ms/helm#install).</span></span>
2. <span data-ttu-id="3be61-123">Use Helm para buscar e instalar `stable/traefik` y el controlador de entrada para permitir las solicitudes entrantes de las compilaciones.</span><span class="sxs-lookup"><span data-stu-id="3be61-123">Use Helm to search for and install `stable/traefik`, and ingress controller to enable inbound requests for your builds.</span></span>
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    <span data-ttu-id="3be61-124">Ahora establezca una inspección en el controlador `ingress` para capturar el valor de IP externo cuando se implemente.</span><span class="sxs-lookup"><span data-stu-id="3be61-124">Now set a watch on the `ingress` controller to capture the external IP value when it is deployed.</span></span> <span data-ttu-id="3be61-125">Esta dirección IP será la [asignada a su dominio de implementación](#wire-up-deployment-domain) en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="3be61-125">This IP address will be the one [mapped to your deployment domain](#wire-up-deployment-domain) in the next section.</span></span>

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    <span data-ttu-id="3be61-126">En este caso, la dirección IP externa para el dominio de la implementación es `13.64.108.240`.</span><span class="sxs-lookup"><span data-stu-id="3be61-126">In this case, the external IP for the deployment domain is `13.64.108.240`.</span></span> <span data-ttu-id="3be61-127">Ya puede asignar su dominio a esa dirección IP.</span><span class="sxs-lookup"><span data-stu-id="3be61-127">Now you can map your domain to that IP.</span></span>

## <a name="wire-up-deployment-domain"></a><span data-ttu-id="3be61-128">Conexión del dominio de implementación</span><span class="sxs-lookup"><span data-stu-id="3be61-128">Wire up deployment domain</span></span>

<span data-ttu-id="3be61-129">Draft crea una versión para cada gráfico de Helm que crea: cada aplicación en la que esté trabajando.</span><span class="sxs-lookup"><span data-stu-id="3be61-129">Draft creates a release for each Helm chart it creates -- each application you are working on.</span></span> <span data-ttu-id="3be61-130">Cada una obtiene un nombre generado que Draft usa como _subdominio_ además del _dominio de implementación_ de raíz que usted controla.</span><span class="sxs-lookup"><span data-stu-id="3be61-130">Each one gets a generated name that is used by draft as a _subdomain_ on top of the root _deployment domain_ that you control.</span></span> <span data-ttu-id="3be61-131">(En este ejemplo, utilizamos `squillace.io` como dominio de implementación.) Para habilitar este comportamiento de subdominio, debe crear un registro D para `'*'` en las entradas de DNS para el dominio de implementación, de modo que cada subdominio generado se enrute al controlador de entrada del clúster de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="3be61-131">(In this example, we use `squillace.io` as the deployment domain.) To enable this subdomain behavior, you must create an A record for `'*'` in your DNS entries for your deployment domain, so that each generated subdomain is routed to the Kubernetes cluster's ingress controller.</span></span>

<span data-ttu-id="3be61-132">Su propio proveedor de dominios tiene su propia forma de asignar servidores DNS; para [delegar los servidores de nombres de dominio en Azure DNS](../../dns/dns-delegate-domain-azure-dns.md), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3be61-132">Your own domain provider has their own way to assign DNS servers; to [delegate your domain nameservers to Azure DNS](../../dns/dns-delegate-domain-azure-dns.md), you take the following steps:</span></span>

1. <span data-ttu-id="3be61-133">Cree un grupo de recursos para su zona.</span><span class="sxs-lookup"><span data-stu-id="3be61-133">Create a resource group for your zone.</span></span>
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

2. <span data-ttu-id="3be61-134">Cree una zona DNS para su dominio.</span><span class="sxs-lookup"><span data-stu-id="3be61-134">Create a DNS zone for your domain.</span></span>
<span data-ttu-id="3be61-135">Utilice el comando [az network dns zone create](/cli/azure/network/dns/zone#create) para obtener que los servidores de nombres deleguen el control de DNS en Azure DNS para su dominio.</span><span class="sxs-lookup"><span data-stu-id="3be61-135">Use the [az network dns zone create](/cli/azure/network/dns/zone#create) command to obtain the nameservers to delegate DNS control to Azure DNS for your domain.</span></span>
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
3. <span data-ttu-id="3be61-136">Agregue los servidores DNS que se le proporcionen al proveedor de dominios para su dominio de implementación, lo que le permite usar Azure DNS para redirigir el dominio tal como lo desee.</span><span class="sxs-lookup"><span data-stu-id="3be61-136">Add the DNS servers you are given to the domain provider for your deployment domain, which enables you to use Azure DNS to repoint your domain as you want.</span></span>
4. <span data-ttu-id="3be61-137">Cree una entrada de conjunto de registros D para la asignación del dominio de implementación para la IP `ingress` en el paso 2 de la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="3be61-137">Create an A record-set entry for your deployment domain mapping to the `ingress` IP from step 2 of the previous section.</span></span>
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
<span data-ttu-id="3be61-138">El resultado se parece a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3be61-138">The output looks something like:</span></span>
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

5. <span data-ttu-id="3be61-139">Configure Draft para usar el registro y crear subdominios para cada gráfico de Helm que cree.</span><span class="sxs-lookup"><span data-stu-id="3be61-139">Configure Draft to use your registry and create subdomains for each Helm chart it creates.</span></span> <span data-ttu-id="3be61-140">Para configurar Draft, necesita:</span><span class="sxs-lookup"><span data-stu-id="3be61-140">To configure Draft, you need:</span></span>
  - <span data-ttu-id="3be61-141">el nombre de Azure Container Registry (en este ejemplo, `draft`)</span><span class="sxs-lookup"><span data-stu-id="3be61-141">your Azure Container Registry name (in this example, `draft`)</span></span>
  - <span data-ttu-id="3be61-142">la clave del registro, o la contraseña, de `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span><span class="sxs-lookup"><span data-stu-id="3be61-142">your registry key, or password, from `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span></span>
  - <span data-ttu-id="3be61-143">el dominio de implementación de raíz que ha configurado para asignar a la dirección IP externa de entrada de Kubernetes (en este caso, `squillace.io`)</span><span class="sxs-lookup"><span data-stu-id="3be61-143">the root deployment domain that you have configured to map to the Kubernetes ingress external IP address (here, `squillace.io`)</span></span>

  <span data-ttu-id="3be61-144">Llame a `draft init`; el proceso de configuración le pide los valores indicados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3be61-144">Call `draft init` and the configuration process prompts you for the values above.</span></span> <span data-ttu-id="3be61-145">El proceso es algo parecido a lo siguiente la primera vez que lo ejecuta.</span><span class="sxs-lookup"><span data-stu-id="3be61-145">The process looks something like the following the first time you run it.</span></span>
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

    In order to install Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

<span data-ttu-id="3be61-146">Ya está listo para implementar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="3be61-146">Now you're ready to deploy an application.</span></span>


## <a name="build-and-deploy-an-application"></a><span data-ttu-id="3be61-147">Compilación e implementación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="3be61-147">Build and deploy an application</span></span>

<span data-ttu-id="3be61-148">En el repositorio de Draft, hay [seis aplicaciones sencillas de ejemplo](https://github.com/Azure/draft/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="3be61-148">In the Draft repo are [six simple example applications](https://github.com/Azure/draft/tree/master/examples).</span></span> <span data-ttu-id="3be61-149">Clone el repositorio y vamos a usar el [ejemplo de Python](https://github.com/Azure/draft/tree/master/examples/python).</span><span class="sxs-lookup"><span data-stu-id="3be61-149">Clone the repo and let's use the [Python example](https://github.com/Azure/draft/tree/master/examples/python).</span></span> <span data-ttu-id="3be61-150">Cambie al directorio examples/Python y escriba `draft create` para compilar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3be61-150">Change into the examples/Python directory, and type `draft create` to build the application.</span></span> <span data-ttu-id="3be61-151">Debe tener un aspecto similar al ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="3be61-151">It should look like the following example.</span></span>
```bash
$ draft create
--> Python app detected
--> Ready to sail
```

<span data-ttu-id="3be61-152">El resultado incluye un archivo Dockerfile y un gráfico de Helm.</span><span class="sxs-lookup"><span data-stu-id="3be61-152">The output includes a Dockerfile and a Helm chart.</span></span> <span data-ttu-id="3be61-153">Para la compilación e implementación, solo tiene que escribir `draft up`.</span><span class="sxs-lookup"><span data-stu-id="3be61-153">To build and deploy, you just type `draft up`.</span></span> <span data-ttu-id="3be61-154">El resultado es exhaustivo pero comienza de forma similar al ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="3be61-154">The output is extensive, but begins like the following example.</span></span>
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

<span data-ttu-id="3be61-155">y, cuando es correcto, finaliza de modo parecido al ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="3be61-155">and when successful ends with something similar to the following example.</span></span>
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying to Kubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io to access your application

Watching local files for changes...
```

<span data-ttu-id="3be61-156">Sea cual sea el nombre de su gráfico, ya puede ejecutar `curl http://gangly-bronco.squillace.io` para recibir la respuesta, `Hello World!`.</span><span class="sxs-lookup"><span data-stu-id="3be61-156">Whatever your chart's name is, you can now `curl http://gangly-bronco.squillace.io` to receive the reply, `Hello World!`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3be61-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3be61-157">Next steps</span></span>

<span data-ttu-id="3be61-158">Ahora que tiene un clúster de ACS Kubernetes, puede investigar mediante [Azure Container Registry](../../container-registry/container-registry-intro.md) para crear más implementaciones de este escenario y también otras distintas.</span><span class="sxs-lookup"><span data-stu-id="3be61-158">Now that you have an ACS Kubernetes cluster, you can investigate using [Azure Container Registry](../../container-registry/container-registry-intro.md) to create more and different deployments of this scenario.</span></span> <span data-ttu-id="3be61-159">Por ejemplo, puede crear un conjunto de registros DNS de dominios draft._basedomain.toplevel_ que controle aspectos de un subdominio más profundo para implementaciones de ACS específicas.</span><span class="sxs-lookup"><span data-stu-id="3be61-159">For example, you can create a draft._basedomain.toplevel_ domain DNS record-set that controls things off of a deeper subdomain for specific ACS deployments.</span></span>






