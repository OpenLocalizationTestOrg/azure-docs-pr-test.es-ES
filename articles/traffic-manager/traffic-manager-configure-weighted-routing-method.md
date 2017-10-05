---
title: "Configuración del método de enrutamiento de tráfico round-robin ponderado con Azure Traffic Manager | Microsoft Docs"
description: "En este artículo se explica cómo equilibrar la carga del tráfico con un método round-robin en Traffic Manager"
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
ms.openlocfilehash: 7aa4c9120d44ff1b3e59a57090ea04e3f8021fc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-weighted-traffic-routing-method-in-traffic-manager"></a><span data-ttu-id="78da1-103">Configuración del método de enrutamiento de tráfico ponderado en Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="78da1-103">Configure the weighted traffic routing method in Traffic Manager</span></span>

<span data-ttu-id="78da1-104">Un patrón del método de enrutamiento del tráfico es proporcionar un conjunto de extremos idénticos, que incluye servicios en la nube y sitios web, y enviar tráfico a cada uno de ellos de forma equitativa (round robin).</span><span class="sxs-lookup"><span data-stu-id="78da1-104">A common traffic routing method pattern is to provide a set of identical endpoints, which include cloud services and websites, and send traffic to each in a round-robin fashion.</span></span> <span data-ttu-id="78da1-105">Los siguientes pasos describen cómo configurar este tipo de método de enrutamiento de tráfico.</span><span class="sxs-lookup"><span data-stu-id="78da1-105">The following steps outline how to configure this type of traffic routing method.</span></span>

> [!NOTE]
> <span data-ttu-id="78da1-106">Azure ya proporciona la funcionalidad de equilibrio de carga Round Robin para sitios web en un centro de datos (también denominado "región").</span><span class="sxs-lookup"><span data-stu-id="78da1-106">Azure Websites already provide round-robin load balancing functionality for websites within a datacenter (also known as a region).</span></span> <span data-ttu-id="78da1-107">El Administrador de tráfico permite especificar el método de enrutamiento del tráfico round robin para sitios web en distintos centros de datos.</span><span class="sxs-lookup"><span data-stu-id="78da1-107">Traffic Manager allows you to specify round-robin traffic routing method for websites in different datacenters.</span></span>

## <a name="to-configure-the-weighted-traffic-routing-method"></a><span data-ttu-id="78da1-108">Para configurar el método de enrutamiento de tráfico ponderado</span><span class="sxs-lookup"><span data-stu-id="78da1-108">To configure the weighted traffic routing method</span></span>

1. <span data-ttu-id="78da1-109">En un explorador, inicie sesión en [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="78da1-109">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="78da1-110">Si aún no tiene cuenta, puede registrarse para obtener [una evaluación gratuita durante un mes](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="78da1-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="78da1-111">En la barra de búsqueda del Portal, busque los **perfiles de Traffic Manager** y, luego, haga clic en el nombre del perfil para el que desea configurar el método de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="78da1-111">In the portal’s search bar, search for the **Traffic Manager profiles** and then click the profile name that you want to configure the routing method for.</span></span>
3. <span data-ttu-id="78da1-112">En la hoja **Perfil de Traffic Manager**, compruebe que existen los servicios en la nube y los sitios web que desea incluir en la configuración.</span><span class="sxs-lookup"><span data-stu-id="78da1-112">In the **Traffic Manager profile** blade, verify that both the cloud services and websites that you want to include in your configuration are present.</span></span>
4. <span data-ttu-id="78da1-113">En la sección **Configuración**, haga clic en **Configuración** y, en la hoja **Configuración**, proceda de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="78da1-113">In the **Settings** section, click **Configuration**, and in the **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="78da1-114">En **Configuración del método de enrutamiento del tráfico**, compruebe que dicho método sea **Ponderado**.</span><span class="sxs-lookup"><span data-stu-id="78da1-114">For **traffic routing method settings**, verify that the traffic routing method is **Weighted**.</span></span> <span data-ttu-id="78da1-115">De no ser así, haga clic en **Ponderado** en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="78da1-115">If it is not, click **Weighted** from the dropdown list.</span></span>
    2. <span data-ttu-id="78da1-116">Establezca la misma **configuración de supervisión de puntos de conexión** para todos los puntos de conexión dentro de este perfil de esta forma:</span><span class="sxs-lookup"><span data-stu-id="78da1-116">Set the **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="78da1-117">Seleccione el **protocolo** adecuado y especifique el número de **puerto**.</span><span class="sxs-lookup"><span data-stu-id="78da1-117">Select the appropriate **Protocol**, and specify the **Port** number.</span></span> 
        2. <span data-ttu-id="78da1-118">En el tipo de **ruta de acceso**, escriba una barra diagonal */*.</span><span class="sxs-lookup"><span data-stu-id="78da1-118">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="78da1-119">Para supervisar los puntos de conexión, debe especificar una ruta de acceso y un nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="78da1-119">To monitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="78da1-120">Una barra diagonal "/" es una entrada válida para la ruta de acceso relativa e implica que el archivo se encuentra en el directorio raíz (valor predeterminado).</span><span class="sxs-lookup"><span data-stu-id="78da1-120">A forward slash "/" is a valid entry for the relative path and implies that the file is in the root directory (default).</span></span>
        3. <span data-ttu-id="78da1-121">Haga clic en **Guardar** en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="78da1-121">At the top of the page, click **Save**.</span></span>
5. <span data-ttu-id="78da1-122">Pruebe los cambios de la configuración de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="78da1-122">Test the changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="78da1-123">En la barra de búsqueda del Portal, busque el nombre del perfil de Traffic Manager y haga clic en él en los resultados que se muestran.</span><span class="sxs-lookup"><span data-stu-id="78da1-123">In the portal’s search bar, search for the Traffic Manager profile name and click the Traffic Manager profile in the results that the displayed.</span></span>
    2.  <span data-ttu-id="78da1-124">En la hoja del perfil de **Traffic Manager**, haga clic en **Información general**.</span><span class="sxs-lookup"><span data-stu-id="78da1-124">In the **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="78da1-125">La hoja **Perfil de Traffic Manager** muestra el nombre DNS del perfil de Traffic Manager que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="78da1-125">The **Traffic Manager profile** blade displays the DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="78da1-126">Cualquier cliente puede usar este perfil (por ejemplo, mediante un explorador web) para enrutar el tráfico al punto de conexión correcto según el tipo de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="78da1-126">This can be used by any clients (for example,by navigating to it using a web browser) to get routed to the right endpoint as determined by the routing type.</span></span> <span data-ttu-id="78da1-127">En este caso, todas las solicitudes se enrutan a cada punto de conexión según round-robin.</span><span class="sxs-lookup"><span data-stu-id="78da1-127">In this case all requests are routed each endpoint in a round-robin fashion.</span></span>
6. <span data-ttu-id="78da1-128">Una vez que el perfil de Traffic Manager esté en funcionamiento, edite el registro DNS en el servidor DNS relevante para redireccionar el nombre de dominio de la empresa al nombre de dominio del Administrador de tráfico.</span><span class="sxs-lookup"><span data-stu-id="78da1-128">Once your Traffic Manager profile is working, edit the DNS record on your authoritative DNS server to point your company domain name to the Traffic Manager domain name.</span></span>

![Configuración del método de enrutamiento de tráfico ponderado con Traffic Manager][1]

## <a name="next-steps"></a><span data-ttu-id="78da1-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="78da1-130">Next steps</span></span>

- <span data-ttu-id="78da1-131">Información sobre el [método de enrutamiento de tráfico por prioridad](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="78da1-131">Learn about [priority traffic routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="78da1-132">Información sobre el [método de enrutamiento de tráfico de rendimiento](traffic-manager-configure-performance-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="78da1-132">Learn about [performance traffic routing method](traffic-manager-configure-performance-routing-method.md).</span></span>
- <span data-ttu-id="78da1-133">Información sobre el [método de enrutamiento geográfico](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="78da1-133">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="78da1-134">Información sobre cómo [probar la configuración de Traffic Manager](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="78da1-134">Learn how to [test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
