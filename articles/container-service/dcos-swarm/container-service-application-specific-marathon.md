---
title: "aaaApplication o específica del usuario maratón servicio | Documentos de Microsoft"
description: "Creación de un servicio de Marathon específico del usuario o la aplicación"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenedores, Marathon, microservicios, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 1e6f69ed64e113a3a059788a71ddb57b6d3ad8da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="fc962-104">Creación de un servicio de Marathon específico del usuario o la aplicación</span><span class="sxs-lookup"><span data-stu-id="fc962-104">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="fc962-105">Azure Container Service proporciona un conjunto de servidores maestros en los que preconfiguramos Apache Mesos y Marathon.</span><span class="sxs-lookup"><span data-stu-id="fc962-105">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span></span> <span data-ttu-id="fc962-106">Éstas pueden ser utilizado tooorchestrate las aplicaciones en clúster de hello, pero recomendados no toouse Hola los servidores maestros para este propósito.</span><span class="sxs-lookup"><span data-stu-id="fc962-106">These can be used tooorchestrate your applications on hello cluster, but it's best not toouse hello master servers for this purpose.</span></span> <span data-ttu-id="fc962-107">Por ejemplo, ajustar la configuración de Hola de maratón requiere iniciar sesión en servidores maestros de Hola por sí mismos y realizar cambios, esto le anima únicos servidores maestros que son un poco diferentes de hello estándar y necesidad toobe atendido y administrado de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="fc962-107">For example, tweaking hello configuration of Marathon requires logging into hello master servers themselves and making changes--this encourages unique master servers that are a little different from hello standard and need toobe cared for and managed independently.</span></span> <span data-ttu-id="fc962-108">Además, configuración de hello necesaria para un equipo podría no ser la configuración óptima de Hola para otro equipo.</span><span class="sxs-lookup"><span data-stu-id="fc962-108">Additionally, hello configuration required by one team might not be hello optimal configuration for another team.</span></span>

<span data-ttu-id="fc962-109">En este artículo, explicaremos cómo tooadd un servicio de maratón de aplicación o del usuario.</span><span class="sxs-lookup"><span data-stu-id="fc962-109">In this article, we'll explain how tooadd an application or user-specific Marathon service.</span></span>

<span data-ttu-id="fc962-110">Dado que este servicio pertenecerá tooa solo usuario o equipo, son tooconfigure libre, de manera que lo desean.</span><span class="sxs-lookup"><span data-stu-id="fc962-110">Because this service will belong tooa single user or team, they are free tooconfigure it in any way that they desire.</span></span> <span data-ttu-id="fc962-111">Además, el servicio de contenedor de Azure se asegurará de que el servicio de hello sigue toorun.</span><span class="sxs-lookup"><span data-stu-id="fc962-111">Also, Azure Container Service will ensure that hello service continues toorun.</span></span> <span data-ttu-id="fc962-112">Si se produce un error en el servicio de hello, servicio de contenedor de Azure se reiniciará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="fc962-112">If hello service fails, Azure Container Service will restart it for you.</span></span> <span data-ttu-id="fc962-113">La mayoría de las veces de hello incluso no notarás que tenía el tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="fc962-113">Most of hello time you won't even notice it had downtime.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc962-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fc962-114">Prerequisites</span></span>
<span data-ttu-id="fc962-115">[Implementar una instancia de servicio de contenedor de Azure](container-service-deployment.md) con orchestrator escriba DC/OS y [Asegúrese de que el cliente puede conectarse tooyour clúster](../container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="fc962-115">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect tooyour cluster](../container-service-connect.md).</span></span> <span data-ttu-id="fc962-116">Además, el Hola lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="fc962-116">Also, do hello following steps.</span></span>

[!INCLUDE [install hello DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="fc962-117">Creación de un servicio de Marathon específico del usuario o la aplicación</span><span class="sxs-lookup"><span data-stu-id="fc962-117">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="fc962-118">Empiece por crear un archivo de configuración de JSON que define el nombre de hello del servicio de aplicación de Hola que desea toocreate.</span><span class="sxs-lookup"><span data-stu-id="fc962-118">Begin by creating a JSON configuration file that defines hello name of hello application service that you want toocreate.</span></span> <span data-ttu-id="fc962-119">Aquí usamos `marathon-alice` como nombre de marco de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc962-119">Here we use `marathon-alice` as hello framework name.</span></span> <span data-ttu-id="fc962-120">Guardar archivo hello como algo parecido a `marathon-alice.json`:</span><span class="sxs-lookup"><span data-stu-id="fc962-120">Save hello file as something like `marathon-alice.json`:</span></span>

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

<span data-ttu-id="fc962-121">A continuación, use instancia maratón de Hola DC/OS CLI tooinstall Hola con opciones de Hola que se establecen en el archivo de configuración:</span><span class="sxs-lookup"><span data-stu-id="fc962-121">Next, use hello DC/OS CLI tooinstall hello Marathon instance with hello options that are set in your configuration file:</span></span>

```bash
dcos package install --options=marathon-alice.json marathon
```

<span data-ttu-id="fc962-122">Ahora debería ver su `marathon-alice` servicio se ejecuta en la ficha de servicios de saludo de la interfaz de usuario del controlador de dominio/OS.</span><span class="sxs-lookup"><span data-stu-id="fc962-122">You should now see your `marathon-alice` service running in hello Services tab of your DC/OS UI.</span></span> <span data-ttu-id="fc962-123">Hello interfaz de usuario será `http://<hostname>/service/marathon-alice/` si desea tooaccess directamente.</span><span class="sxs-lookup"><span data-stu-id="fc962-123">hello UI will be `http://<hostname>/service/marathon-alice/` if you want tooaccess it directly.</span></span>

## <a name="set-hello-dcos-cli-tooaccess-hello-service"></a><span data-ttu-id="fc962-124">Establecer Hola DC/OS CLI tooaccess servicio Hola</span><span class="sxs-lookup"><span data-stu-id="fc962-124">Set hello DC/OS CLI tooaccess hello service</span></span>
<span data-ttu-id="fc962-125">Opcionalmente puede configurar este nuevo servicio de la CLI de DC/OS tooaccess por establecer hello `marathon.url` propiedad toopoint toohello `marathon-alice` instancia como sigue:</span><span class="sxs-lookup"><span data-stu-id="fc962-125">You can optionally configure your DC/OS CLI tooaccess this new service by setting hello `marathon.url` property toopoint toohello `marathon-alice` instance as follows:</span></span>

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

<span data-ttu-id="fc962-126">Puede comprobar qué instancia de maratón con la que la CLI funciona contra Hola `dcos config show` comando.</span><span class="sxs-lookup"><span data-stu-id="fc962-126">You can verify which instance of Marathon that your CLI is working against with hello `dcos config show` command.</span></span> <span data-ttu-id="fc962-127">Puede revertir toousing su servicio de maratón maestro con el comando hello `dcos config unset marathon.url`.</span><span class="sxs-lookup"><span data-stu-id="fc962-127">You can revert toousing your master Marathon service with hello command `dcos config unset marathon.url`.</span></span>

