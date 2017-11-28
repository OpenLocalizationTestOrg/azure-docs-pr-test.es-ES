---
title: aaaGet a trabajar con Azure Service Fabric y 2.0 de CLI de Azure
description: "Obtenga información acerca de cómo toouse hello Azure Service Fabric comandos del módulo de CLI de Azure, versión 2.0. Obtenga información acerca de cómo tooconnect tooa clúster y cómo las aplicaciones de toomanage."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ddbd0ef503dd3fff61494cc2cfa7c9a2e8d0a9a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a><span data-ttu-id="531b3-104">Azure Service Fabric y CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="531b3-104">Azure Service Fabric and Azure CLI 2.0</span></span>

<span data-ttu-id="531b3-105">Hello Azure herramienta de línea de comandos (CLI de Azure) versión 2.0 incluye toohelp comandos administrar clústeres de Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="531b3-105">hello Azure command-line tool (Azure CLI) version 2.0 includes commands toohelp you manage Azure Service Fabric clusters.</span></span> <span data-ttu-id="531b3-106">Obtenga información acerca de cómo se inicia tooget con CLI de Azure y el tejido de servicio.</span><span class="sxs-lookup"><span data-stu-id="531b3-106">Learn how tooget started with Azure CLI and Service Fabric.</span></span>

## <a name="install-azure-cli-20"></a><span data-ttu-id="531b3-107">Instalación de la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="531b3-107">Install Azure CLI 2.0</span></span>

<span data-ttu-id="531b3-108">Puede usar toointeract de comandos de CLI de Azure 2.0 con y administrar clústeres de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="531b3-108">You can use Azure CLI 2.0 commands toointeract with and manage Service Fabric clusters.</span></span> <span data-ttu-id="531b3-109">versión más reciente de hello tooget de CLI de Azure, siga hello [proceso de instalación estándar de CLI de Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="531b3-109">tooget hello latest version of Azure CLI, follow hello [Azure CLI 2.0 standard installation process](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="531b3-110">Para obtener más información, vea hello [información general de CLI de Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="531b3-110">For more information, see hello [Azure CLI 2.0 overview](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="azure-cli-syntax"></a><span data-ttu-id="531b3-111">Sintaxis de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="531b3-111">Azure CLI syntax</span></span>

<span data-ttu-id="531b3-112">Todos los comandos de Service Fabric tienen el prefijo `az sf` en la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="531b3-112">In Azure CLI, all Service Fabric commands are prefixed with `az sf`.</span></span> <span data-ttu-id="531b3-113">Para obtener información general acerca de los comandos de hello puede utilizar, use `az sf -h`.</span><span class="sxs-lookup"><span data-stu-id="531b3-113">For general information about hello commands you can use, use `az sf -h`.</span></span> <span data-ttu-id="531b3-114">Para obtener ayuda con un único comando, use `az sf <command> -h`.</span><span class="sxs-lookup"><span data-stu-id="531b3-114">For help with a single command, use `az sf <command> -h`.</span></span>

<span data-ttu-id="531b3-115">Los comandos de Service Fabric en la CLI de Azure siguen este patrón de nomenclatura:</span><span class="sxs-lookup"><span data-stu-id="531b3-115">Service Fabric commands in Azure CLI follow this naming pattern:</span></span>

```azurecli
az sf <object> <action>
```

<span data-ttu-id="531b3-116">`<object>`es destino de Hola para `<action>`.</span><span class="sxs-lookup"><span data-stu-id="531b3-116">`<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="531b3-117">Selección de un clúster</span><span class="sxs-lookup"><span data-stu-id="531b3-117">Select a cluster</span></span>

<span data-ttu-id="531b3-118">Antes de realizar cualquier operación, debe seleccionar una tooconnect de clúster a.</span><span class="sxs-lookup"><span data-stu-id="531b3-118">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="531b3-119">Para obtener un ejemplo, vea Hola siguiente código.</span><span class="sxs-lookup"><span data-stu-id="531b3-119">For an example, see hello following code.</span></span> <span data-ttu-id="531b3-120">código de Hello conecta tooan segura clúster.</span><span class="sxs-lookup"><span data-stu-id="531b3-120">hello code connects tooan unsecured cluster.</span></span>

> [!WARNING]
> <span data-ttu-id="531b3-121">No utilice clústeres de Service Fabric que no sean seguros en entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="531b3-121">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="531b3-122">punto de conexión de clúster de Hello debe ir precedido por `http` o `https`.</span><span class="sxs-lookup"><span data-stu-id="531b3-122">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="531b3-123">Debe incluir el puerto de Hola para puerta de enlace de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="531b3-123">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="531b3-124">dirección y el puerto de Hola se Hola igual que la dirección URL del explorador de Service Fabric de Hola.</span><span class="sxs-lookup"><span data-stu-id="531b3-124">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="531b3-125">Para los clústeres que están protegidos con un certificado, puede usar archivos .pem o .crt y .key sin cifrar.</span><span class="sxs-lookup"><span data-stu-id="531b3-125">For clusters that are secured with a certificate, you can use either unencrypted .pem files, or .crt and .key files.</span></span> <span data-ttu-id="531b3-126">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="531b3-126">For example:</span></span>

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="531b3-127">Para obtener más información, consulte [clúster de Azure Service Fabric segura de conectar tooa](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="531b3-127">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

> [!NOTE]
> <span data-ttu-id="531b3-128">Hola `select` comando no actuar sobre las solicitudes antes de regresar.</span><span class="sxs-lookup"><span data-stu-id="531b3-128">hello `select` command doesn't act on any requests before it returns.</span></span> <span data-ttu-id="531b3-129">tooverify que ha especificado un clúster correctamente, utilice un comando como `az sf cluster health`.</span><span class="sxs-lookup"><span data-stu-id="531b3-129">tooverify that you've specified a cluster correctly, use a command like `az sf cluster health`.</span></span> <span data-ttu-id="531b3-130">Compruebe que el comando hello no devuelve los errores.</span><span class="sxs-lookup"><span data-stu-id="531b3-130">Verify that hello command doesn't return any errors.</span></span>

## <a name="basic-operations"></a><span data-ttu-id="531b3-131">Operaciones básicas</span><span class="sxs-lookup"><span data-stu-id="531b3-131">Basic operations</span></span>

<span data-ttu-id="531b3-132">La información de la conexión del clúster se mantiene en varias sesiones de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="531b3-132">Cluster connection information persists across multiple Azure CLI sessions.</span></span> <span data-ttu-id="531b3-133">Después de seleccionar un clúster de Service Fabric, puede ejecutar cualquier comando de Service Fabric en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="531b3-133">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="531b3-134">Por ejemplo, hello tooget estado de mantenimiento del clúster de Service Fabric, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="531b3-134">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
az sf cluster health
```

<span data-ttu-id="531b3-135">Hola comando genera siguiente de hello resultado (suponiendo que la salida JSON se especifica en configuración de CLI de Azure de hello):</span><span class="sxs-lookup"><span data-stu-id="531b3-135">hello command results in hello following output (assuming that JSON output is specified in hello Azure CLI configuration):</span></span>

```json
{
  "aggregatedHealthState": "Ok",
  "applicationHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "name": "fabric:/System"
    }
  ],
  "healthEvents": [],
  "nodeHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "id": {
        "id": "66aa824a642124089ee474b398d06a57"
      },
      "name": "_Test_0"
    }
  ],
  "unhealthyEvaluations": []
}
```

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="531b3-136">Sugerencias y solución de problemas</span><span class="sxs-lookup"><span data-stu-id="531b3-136">Tips and troubleshooting</span></span>

<span data-ttu-id="531b3-137">Es posible Hola después información útil si surgen problemas al usar comandos de Service Fabric en CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="531b3-137">You might find hello following information helpful if you run into issues while using Service Fabric commands in Azure CLI.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="531b3-138">Convertir un certificado desde el formato de tooPEM PFX</span><span class="sxs-lookup"><span data-stu-id="531b3-138">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="531b3-139">La CLI de Azure admite los certificados de cliente, como los archivos PEM (extensión .pem).</span><span class="sxs-lookup"><span data-stu-id="531b3-139">Azure CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="531b3-140">Si utiliza los archivos PFX de Windows, debe convertir esos formato tooPEM de certificados.</span><span class="sxs-lookup"><span data-stu-id="531b3-140">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="531b3-141">tooconvert un archivo PEM tooa del archivo PFX, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="531b3-141">tooconvert a PFX file tooa PEM file, use hello following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="531b3-142">Para obtener más información, vea hello [OpenSSL documentación](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="531b3-142">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="531b3-143">Problemas de conexión</span><span class="sxs-lookup"><span data-stu-id="531b3-143">Connection issues</span></span>

<span data-ttu-id="531b3-144">Algunas operaciones pueden generar Hola siguiente mensaje:</span><span class="sxs-lookup"><span data-stu-id="531b3-144">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="531b3-145">Compruebe que Hola especificado de punto de conexión de clúster está disponible y realizando escuchas.</span><span class="sxs-lookup"><span data-stu-id="531b3-145">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="531b3-146">Además, compruebe que Hola que está disponible en la interfaz de usuario del explorador de tejido de servicio de host y puerto.</span><span class="sxs-lookup"><span data-stu-id="531b3-146">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="531b3-147">punto de conexión de tooupdate hello, use `az sf cluster select`.</span><span class="sxs-lookup"><span data-stu-id="531b3-147">tooupdate hello endpoint, use `az sf cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="531b3-148">Registros detallados</span><span class="sxs-lookup"><span data-stu-id="531b3-148">Detailed logs</span></span>

<span data-ttu-id="531b3-149">Los registros detallados a menudo son útiles al depurar o notificar problemas.</span><span class="sxs-lookup"><span data-stu-id="531b3-149">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="531b3-150">CLI de Azure ofrece global `--debug` marca que aumenta el nivel de detalle de Hola de archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="531b3-150">Azure CLI offers a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="531b3-151">Ayuda y sintaxis de los comandos</span><span class="sxs-lookup"><span data-stu-id="531b3-151">Command help and syntax</span></span>

<span data-ttu-id="531b3-152">Seguimiento de comandos de Service Fabric hello las mismas convenciones que CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="531b3-152">Service Fabric commands follow hello same conventions as Azure CLI.</span></span> <span data-ttu-id="531b3-153">Para obtener ayuda con un comando específico o un grupo de comandos, usar hello `-h` marca:</span><span class="sxs-lookup"><span data-stu-id="531b3-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
az sf application -h
```

<span data-ttu-id="531b3-154">Este es otro ejemplo:</span><span class="sxs-lookup"><span data-stu-id="531b3-154">Here's another example:</span></span>

```azurecli
az sf application create -h
```
