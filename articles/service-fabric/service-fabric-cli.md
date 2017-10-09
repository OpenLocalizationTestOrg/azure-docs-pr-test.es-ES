---
title: aaaGet a trabajar con Azure Service Fabric CLI (sfctl)
description: "Obtenga información acerca de cómo toouse Hola CLI de tejido de servicio de Azure. Obtenga información acerca de cómo tooconnect tooa clúster y cómo las aplicaciones de toomanage."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: f76e8ff65bb38dfb63791da0a23e19b93b337f6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-command-line"></a><span data-ttu-id="8bc1f-104">Línea de comandos de Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8bc1f-104">Azure Service Fabric command line</span></span>

<span data-ttu-id="8bc1f-105">Hello Azure Service Fabric CLI (sfctl) es una utilidad de línea de comandos para interactuar y administrar entidades de Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-105">hello Azure Service Fabric CLI (sfctl) is a command-line utility for interacting and managing Azure Service Fabric entities.</span></span> <span data-ttu-id="8bc1f-106">Sfctl puede utilizarse con clústeres de Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-106">Sfctl can be used with either Windows or Linux clusters.</span></span> <span data-ttu-id="8bc1f-107">Sfctl se ejecuta en cualquier plataforma que sea compatible con Python.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-107">Sfctl runs on any platform where python is supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8bc1f-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8bc1f-108">Prerequisites</span></span>

<span data-ttu-id="8bc1f-109">Tooinstallation anterior, asegúrese de que el entorno tiene python y pip instalado.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-109">Prior tooinstallation, make sure your environment has both python and pip installed.</span></span> <span data-ttu-id="8bc1f-110">Para obtener más información, eche un vistazo a hello [pip documentación de inicio rápido](https://pip.pypa.io/en/latest/quickstart/)y oficial [python instala documentación](https://wiki.python.org/moin/BeginnersGuide/Download).</span><span class="sxs-lookup"><span data-stu-id="8bc1f-110">For more information, take a look at hello [pip quickstart documentation](https://pip.pypa.io/en/latest/quickstart/), and official [python install documentation](https://wiki.python.org/moin/BeginnersGuide/Download).</span></span>

<span data-ttu-id="8bc1f-111">Aunque se admite ambos python 2.7 y 3.6, se recomienda toouse python 3.6.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-111">While both python 2.7 and 3.6 are supported, it is recommended toouse python 3.6.</span></span>

## <a name="install"></a><span data-ttu-id="8bc1f-112">Instalación</span><span class="sxs-lookup"><span data-stu-id="8bc1f-112">Install</span></span>

<span data-ttu-id="8bc1f-113">Hello Azure Service Fabric CLI (sfctl) se empaqueta como un paquete de python.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-113">hello Azure Service Fabric CLI (sfctl) is packaged as a python package.</span></span> <span data-ttu-id="8bc1f-114">tooinstall Hola versión más reciente ejecutar:</span><span class="sxs-lookup"><span data-stu-id="8bc1f-114">tooinstall hello latest version run:</span></span>

```bash
pip install sfctl
```

<span data-ttu-id="8bc1f-115">Después de la instalación, ejecute `sfctl -h` tooget información acerca de los comandos disponibles.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-115">After installation, run `sfctl -h` tooget information about available commands.</span></span>

## <a name="cli-syntax"></a><span data-ttu-id="8bc1f-116">Sintaxis de la CLI</span><span class="sxs-lookup"><span data-stu-id="8bc1f-116">CLI syntax</span></span>

<span data-ttu-id="8bc1f-117">Los comandos siempre tienen el prefijo `sfctl`.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-117">Commands are prefixed always with `sfctl`.</span></span> <span data-ttu-id="8bc1f-118">Para obtener información general de todos los comandos que puede usar, use `sfctl -h`.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-118">For general information about all commands you can use, use `sfctl -h`.</span></span> <span data-ttu-id="8bc1f-119">Para obtener ayuda con un único comando, use `sfctl <command> -h`.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-119">For help with a single command, use `sfctl <command> -h`.</span></span>

<span data-ttu-id="8bc1f-120">Seguimiento de comandos una estructura repetible, con destino Hola Hola de comandos anterior verbo de Hola o acción:</span><span class="sxs-lookup"><span data-stu-id="8bc1f-120">Commands follow a repeatable structure, with hello target of hello command preceding hello verb or action:</span></span>

```azurecli
sfctl <object> <action>
```

<span data-ttu-id="8bc1f-121">En este ejemplo, `<object>` es destino de Hola para `<action>`.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-121">In this example, `<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="8bc1f-122">Selección de un clúster</span><span class="sxs-lookup"><span data-stu-id="8bc1f-122">Select a cluster</span></span>

<span data-ttu-id="8bc1f-123">Antes de realizar cualquier operación, debe seleccionar una tooconnect de clúster a.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-123">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="8bc1f-124">Por ejemplo, ejecute hello después tooselect y conectar toohello clúster con el nombre de hello `testcluster.com`.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-124">For example, run hello following tooselect and connect toohello cluster with hello name `testcluster.com`.</span></span>

> [!WARNING]
> <span data-ttu-id="8bc1f-125">No utilice clústeres de Service Fabric que no sean seguros en entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-125">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="8bc1f-126">punto de conexión de clúster de Hello debe ir precedido por `http` o `https`.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-126">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="8bc1f-127">Debe incluir el puerto de Hola para puerta de enlace de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-127">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="8bc1f-128">dirección y el puerto de Hola se Hola igual que la dirección URL del explorador de Service Fabric de Hola.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-128">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="8bc1f-129">Para clústeres que están protegidos con un certificado, puede especificar un certificado PEM codificado.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-129">For clusters that are secured with a certificate, you can specify a PEM encoded certificate.</span></span> <span data-ttu-id="8bc1f-130">certificado de Hello puede especificarse como un único archivo o el certificado y el par de claves.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-130">hello certificate can be specified as a single file or cert and key pair.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="8bc1f-131">Para obtener más información, consulte [clúster de Azure Service Fabric segura de conectar tooa](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="8bc1f-131">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="basic-operations"></a><span data-ttu-id="8bc1f-132">Operaciones básicas</span><span class="sxs-lookup"><span data-stu-id="8bc1f-132">Basic operations</span></span>

<span data-ttu-id="8bc1f-133">La información de la conexión del clúster se mantiene en varias sesiones de sfctl.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-133">Cluster connection information persists across multiple sfctl sessions.</span></span> <span data-ttu-id="8bc1f-134">Después de seleccionar un clúster de Service Fabric, puede ejecutar cualquier comando de Service Fabric en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-134">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="8bc1f-135">Por ejemplo, hello tooget estado de mantenimiento del clúster de Service Fabric, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8bc1f-135">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
sfctl cluster health
```

<span data-ttu-id="8bc1f-136">resultados del comando Hola Hola después de salida:</span><span class="sxs-lookup"><span data-stu-id="8bc1f-136">hello command results in hello following output:</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="8bc1f-137">Sugerencias y solución de problemas</span><span class="sxs-lookup"><span data-stu-id="8bc1f-137">Tips and troubleshooting</span></span>

<span data-ttu-id="8bc1f-138">Sugerencias y consejos para resolver problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-138">Some suggestions and tips for solving common issues.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="8bc1f-139">Convertir un certificado desde el formato de tooPEM PFX</span><span class="sxs-lookup"><span data-stu-id="8bc1f-139">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="8bc1f-140">Hola Service Fabric CLI admite certificados de cliente como archivos PEM (extensión .pem).</span><span class="sxs-lookup"><span data-stu-id="8bc1f-140">hello Service Fabric CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="8bc1f-141">Si utiliza los archivos PFX de Windows, debe convertir esos formato tooPEM de certificados.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-141">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="8bc1f-142">tooconvert un archivo PEM tooa del archivo PFX, utilice el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8bc1f-142">tooconvert a PFX file tooa PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="8bc1f-143">Para obtener más información, vea hello [OpenSSL documentación](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="8bc1f-143">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="8bc1f-144">Problemas de conexión</span><span class="sxs-lookup"><span data-stu-id="8bc1f-144">Connection issues</span></span>

<span data-ttu-id="8bc1f-145">Algunas operaciones pueden generar Hola siguiente mensaje:</span><span class="sxs-lookup"><span data-stu-id="8bc1f-145">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="8bc1f-146">Compruebe que Hola especificado de punto de conexión de clúster está disponible y realizando escuchas.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-146">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="8bc1f-147">Además, compruebe que Hola que está disponible en la interfaz de usuario del explorador de tejido de servicio de host y puerto.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-147">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="8bc1f-148">punto de conexión de tooupdate hello, use `sfctl cluster select`.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-148">tooupdate hello endpoint, use `sfctl cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="8bc1f-149">Registros detallados</span><span class="sxs-lookup"><span data-stu-id="8bc1f-149">Detailed logs</span></span>

<span data-ttu-id="8bc1f-150">Los registros detallados a menudo son útiles al depurar o notificar problemas.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-150">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="8bc1f-151">Hay un global `--debug` marca que aumenta el nivel de detalle de Hola de archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="8bc1f-151">There is a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="8bc1f-152">Ayuda y sintaxis de los comandos</span><span class="sxs-lookup"><span data-stu-id="8bc1f-152">Command help and syntax</span></span>

<span data-ttu-id="8bc1f-153">Para obtener ayuda con un comando específico o un grupo de comandos, usar hello `-h` marca:</span><span class="sxs-lookup"><span data-stu-id="8bc1f-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
sfctl application -h
```

<span data-ttu-id="8bc1f-154">Otro ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8bc1f-154">Another example:</span></span>

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a><span data-ttu-id="8bc1f-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8bc1f-155">Next steps</span></span>

* [<span data-ttu-id="8bc1f-156">Implementar una aplicación con hello Azure Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="8bc1f-156">Deploy an application with hello Azure Service Fabric CLI</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="8bc1f-157">Introducción a Service Fabric con Linux</span><span class="sxs-lookup"><span data-stu-id="8bc1f-157">Get started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
