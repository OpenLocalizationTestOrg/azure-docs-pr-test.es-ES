---
title: "método de enrutamiento con Azure Traffic Manager de tráfico aaaConfigure ponderada round robin | Documentos de Microsoft"
description: "Este artículo explica cómo tooload equilibrar el tráfico con un método round robin en Traffic Manager"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: 7e2866ead0b2b653845435dd420a763c5e175f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-weighted-traffic-routing-method-in-traffic-manager"></a><span data-ttu-id="f5a97-103">Configurar método de enrutamiento de tráfico de hello ponderada en Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="f5a97-103">Configure hello weighted traffic routing method in Traffic Manager</span></span>

<span data-ttu-id="f5a97-104">Un patrón común de método de enrutamiento de tráfico es tooprovide un conjunto de extremos idénticos, lo cual incluye servicios en la nube y sitios Web y enviar tráfico tooeach en un modo round-robin.</span><span class="sxs-lookup"><span data-stu-id="f5a97-104">A common traffic routing method pattern is tooprovide a set of identical endpoints, which include cloud services and websites, and send traffic tooeach in a round-robin fashion.</span></span> <span data-ttu-id="f5a97-105">Hola pasos describen cómo tooconfigure este tipo de método de enrutamiento de tráfico.</span><span class="sxs-lookup"><span data-stu-id="f5a97-105">hello following steps outline how tooconfigure this type of traffic routing method.</span></span>

> [!NOTE]
> <span data-ttu-id="f5a97-106">Azure ya proporciona la funcionalidad de equilibrio de carga Round Robin para sitios web en un centro de datos (también denominado "región").</span><span class="sxs-lookup"><span data-stu-id="f5a97-106">Azure Websites already provide round-robin load balancing functionality for websites within a datacenter (also known as a region).</span></span> <span data-ttu-id="f5a97-107">Traffic Manager permite un método de enrutamiento de tráfico de round robin toospecify para los sitios Web en distintos centros de datos.</span><span class="sxs-lookup"><span data-stu-id="f5a97-107">Traffic Manager allows you toospecify round-robin traffic routing method for websites in different datacenters.</span></span>

## <a name="tooconfigure-hello-weighted-traffic-routing-method"></a><span data-ttu-id="f5a97-108">método de enrutamiento de tráfico tooconfigure Hola ponderada</span><span class="sxs-lookup"><span data-stu-id="f5a97-108">tooconfigure hello weighted traffic routing method</span></span>

1. <span data-ttu-id="f5a97-109">Desde un explorador, inicie sesión en toohello [portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f5a97-109">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="f5a97-110">Si aún no tiene cuenta, puede registrarse para obtener [una evaluación gratuita durante un mes](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="f5a97-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="f5a97-111">En la barra de búsqueda del portal de hello, busque hello **perfiles de Traffic Manager** y, a continuación, haga clic en nombre de perfil de Hola que desea que el método de enrutamiento de hello tooconfigure para.</span><span class="sxs-lookup"><span data-stu-id="f5a97-111">In hello portal’s search bar, search for hello **Traffic Manager profiles** and then click hello profile name that you want tooconfigure hello routing method for.</span></span>
3. <span data-ttu-id="f5a97-112">Hola **perfil de Traffic Manager** hoja, compruebe que ambos Hola servicios en la nube y sitios Web que desea tooinclude en la configuración está presentes.</span><span class="sxs-lookup"><span data-stu-id="f5a97-112">In hello **Traffic Manager profile** blade, verify that both hello cloud services and websites that you want tooinclude in your configuration are present.</span></span>
4. <span data-ttu-id="f5a97-113">Hola **configuración** sección, haga clic en **configuración**y en hello **configuración** hoja, completa, como sigue:</span><span class="sxs-lookup"><span data-stu-id="f5a97-113">In hello **Settings** section, click **Configuration**, and in hello **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="f5a97-114">Para **configuración del método de enrutamiento de tráfico**, compruebe que es el método de enrutamiento de tráfico de hello **Weighted**.</span><span class="sxs-lookup"><span data-stu-id="f5a97-114">For **traffic routing method settings**, verify that hello traffic routing method is **Weighted**.</span></span> <span data-ttu-id="f5a97-115">Si no es así, haga clic en **Weighted** en lista de desplegable Hola.</span><span class="sxs-lookup"><span data-stu-id="f5a97-115">If it is not, click **Weighted** from hello dropdown list.</span></span>
    2. <span data-ttu-id="f5a97-116">Conjunto hello **configuración del monitor de punto de conexión** idénticos para todas las cada punto de conexión dentro de este perfil como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="f5a97-116">Set hello **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="f5a97-117">Seleccione Hola adecuado **protocolo**y especifique hello **puerto** número.</span><span class="sxs-lookup"><span data-stu-id="f5a97-117">Select hello appropriate **Protocol**, and specify hello **Port** number.</span></span> 
        2. <span data-ttu-id="f5a97-118">En el tipo de **ruta de acceso**, escriba una barra diagonal */*.</span><span class="sxs-lookup"><span data-stu-id="f5a97-118">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="f5a97-119">los puntos de conexión de toomonitor, debe especificar una ruta de acceso y nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="f5a97-119">toomonitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="f5a97-120">Una barra diagonal "/" es una entrada válida para la ruta de acceso relativa de Hola e implica que el archivo hello esté en el directorio raíz de hello (valor predeterminado).</span><span class="sxs-lookup"><span data-stu-id="f5a97-120">A forward slash "/" is a valid entry for hello relative path and implies that hello file is in hello root directory (default).</span></span>
        3. <span data-ttu-id="f5a97-121">En la parte superior de Hola de página de hello, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="f5a97-121">At hello top of hello page, click **Save**.</span></span>
5. <span data-ttu-id="f5a97-122">Probar cambios de hello en la configuración como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="f5a97-122">Test hello changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="f5a97-123">En la barra de búsqueda del portal de hello, busque el nombre del perfil de Traffic Manager de Hola y haga clic en perfil de Traffic Manager de hello en los resultados de Hola que hello muestra.</span><span class="sxs-lookup"><span data-stu-id="f5a97-123">In hello portal’s search bar, search for hello Traffic Manager profile name and click hello Traffic Manager profile in hello results that hello displayed.</span></span>
    2.  <span data-ttu-id="f5a97-124">Hola **Traffic Manager** hoja de perfil, haga clic en **Introducción**.</span><span class="sxs-lookup"><span data-stu-id="f5a97-124">In hello **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="f5a97-125">Hola **perfil de Traffic Manager** hoja muestra el nombre DNS de Hola de su perfil de Traffic Manager recién creado.</span><span class="sxs-lookup"><span data-stu-id="f5a97-125">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="f5a97-126">Esto se puede utilizar cualquier extremo derecho de los clientes (por ejemplo, desplazándose tooit mediante un explorador web) tooget enrutado toohello determinado por el tipo de enrutamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5a97-126">This can be used by any clients (for example,by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="f5a97-127">En este caso, todas las solicitudes se enrutan a cada punto de conexión según round-robin.</span><span class="sxs-lookup"><span data-stu-id="f5a97-127">In this case all requests are routed each endpoint in a round-robin fashion.</span></span>
6. <span data-ttu-id="f5a97-128">Una vez que el perfil de Traffic Manager está en funcionamiento, edite registro DNS de hello en su toopoint de servidor DNS autoritativo su nombre de dominio de empresa dominio nombre toohello Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="f5a97-128">Once your Traffic Manager profile is working, edit hello DNS record on your authoritative DNS server toopoint your company domain name toohello Traffic Manager domain name.</span></span>

![Configuración del método de enrutamiento de tráfico ponderado con Traffic Manager][1]

## <a name="next-steps"></a><span data-ttu-id="f5a97-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f5a97-130">Next steps</span></span>

- <span data-ttu-id="f5a97-131">Información sobre el [método de enrutamiento de tráfico por prioridad](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="f5a97-131">Learn about [priority traffic routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="f5a97-132">Información sobre el [método de enrutamiento de tráfico de rendimiento](traffic-manager-configure-performance-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="f5a97-132">Learn about [performance traffic routing method](traffic-manager-configure-performance-routing-method.md).</span></span>
- <span data-ttu-id="f5a97-133">Información sobre el [método de enrutamiento geográfico](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="f5a97-133">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="f5a97-134">Obtenga información acerca de cómo demasiado[Probar configuración de Traffic Manager](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="f5a97-134">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
