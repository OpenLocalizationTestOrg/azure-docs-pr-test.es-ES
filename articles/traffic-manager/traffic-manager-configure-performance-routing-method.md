---
title: "Configuración del método de enrutamiento del tráfico de rendimiento con Azure Traffic Manager | Microsoft Docs"
description: "En este artículo se explica cómo configurar Traffic Manager para enrutar el tráfico al punto de conexión con latencia más baja."
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
ms.openlocfilehash: 014aa646459cd64fca7c697419324caa3edaeeea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-performance-traffic-routing-method"></a><span data-ttu-id="66bb3-103">Configuración del método de enrutamiento del tráfico de rendimiento</span><span class="sxs-lookup"><span data-stu-id="66bb3-103">Configure the performance traffic routing method</span></span>

<span data-ttu-id="66bb3-104">El método de enrutamiento de tráfico Rendimiento permite dirigir el tráfico al punto de conexión con la menor latencia de red del cliente.</span><span class="sxs-lookup"><span data-stu-id="66bb3-104">The Performance traffic routing method allows you to direct traffic to the endpoint with the lowest latency from the client's network.</span></span> <span data-ttu-id="66bb3-105">Normalmente, el centro de datos con la latencia más baja corresponde a la distancia geográfica más cercana.</span><span class="sxs-lookup"><span data-stu-id="66bb3-105">Typically, the datacenter with the lowest latency is the closest in geographic distance.</span></span> <span data-ttu-id="66bb3-106">Este método de enrutamiento de tráfico no cuenta los cambios en tiempo real en la carga o configuración de red.</span><span class="sxs-lookup"><span data-stu-id="66bb3-106">This traffic routing method cannot account for real-time changes in network configuration or load.</span></span>

##  <a name="to-configure-performance-routing-method"></a><span data-ttu-id="66bb3-107">Pasos para configurar el método de enrutamiento de rendimiento</span><span class="sxs-lookup"><span data-stu-id="66bb3-107">To configure performance routing method</span></span>

1. <span data-ttu-id="66bb3-108">En un explorador, inicie sesión en [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="66bb3-108">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="66bb3-109">Si aún no tiene cuenta, puede registrarse para obtener [una evaluación gratuita durante un mes](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="66bb3-109">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="66bb3-110">En la barra de búsqueda del Portal, busque los **perfiles de Traffic Manager** y, luego, haga clic en el nombre del perfil para el que desea configurar el método de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="66bb3-110">In the portal’s search bar, search for the **Traffic Manager profiles** and then click the profile name that you want to configure the routing method for.</span></span>
3. <span data-ttu-id="66bb3-111">En la hoja **Perfil de Traffic Manager**, compruebe que existen los servicios en la nube y los sitios web que desea incluir en la configuración.</span><span class="sxs-lookup"><span data-stu-id="66bb3-111">In the **Traffic Manager profile** blade, verify that both the cloud services and websites that you want to include in your configuration are present.</span></span>
4. <span data-ttu-id="66bb3-112">En la sección **Configuración**, haga clic en **Configuración**, y en la hoja **Configuración**, proceda de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="66bb3-112">In the **Settings** section, click **Configuration**, and in the **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="66bb3-113">En la **configuración del método de enrutamiento de tráfico**, seleccione **Rendimiento** en **Método de enrutamiento**.</span><span class="sxs-lookup"><span data-stu-id="66bb3-113">For **traffic routing method settings**, for **Routing method** select **Performance**.</span></span>
    2. <span data-ttu-id="66bb3-114">Establezca la misma **configuración de supervisión de puntos de conexión** para todos los puntos de conexión dentro de este perfil de esta forma:</span><span class="sxs-lookup"><span data-stu-id="66bb3-114">Set the **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="66bb3-115">Seleccione el **protocolo** adecuado y especifique el número de **puerto**.</span><span class="sxs-lookup"><span data-stu-id="66bb3-115">Select the appropriate **Protocol**, and specify the **Port** number.</span></span> 
        2. <span data-ttu-id="66bb3-116">En el tipo de **ruta de acceso**, escriba una barra diagonal */*.</span><span class="sxs-lookup"><span data-stu-id="66bb3-116">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="66bb3-117">Para supervisar los puntos de conexión, debe especificar una ruta de acceso y un nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="66bb3-117">To monitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="66bb3-118">Una barra diagonal "/" es una entrada válida para la ruta de acceso relativa e implica que el archivo se encuentra en el directorio raíz (valor predeterminado).</span><span class="sxs-lookup"><span data-stu-id="66bb3-118">A forward slash "/" is a valid entry for the relative path and implies that the file is in the root directory (default).</span></span>
        3. <span data-ttu-id="66bb3-119">Haga clic en **Guardar** en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="66bb3-119">At the top of the page, click **Save**.</span></span>
5.  <span data-ttu-id="66bb3-120">Pruebe los cambios de la configuración de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="66bb3-120">Test the changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="66bb3-121">En la barra de búsqueda del Portal, busque el nombre del perfil de Traffic Manager y haga clic en él en los resultados que se muestran.</span><span class="sxs-lookup"><span data-stu-id="66bb3-121">In the portal’s search bar, search for the Traffic Manager profile name and click the Traffic Manager profile in the results that the displayed.</span></span>
    2.  <span data-ttu-id="66bb3-122">En la hoja del perfil de **Traffic Manager**, haga clic en **Información general**.</span><span class="sxs-lookup"><span data-stu-id="66bb3-122">In the **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="66bb3-123">La hoja **Perfil de Traffic Manager** muestra el nombre DNS del perfil de Traffic Manager que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="66bb3-123">The **Traffic Manager profile** blade displays the DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="66bb3-124">Cualquier cliente puede usar este perfil (por ejemplo, accediendo a él mediante un explorador web) para enrutar el tráfico al punto de conexión correcto según el tipo de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="66bb3-124">This can be used by any clients (for example, by navigating to it using a web browser) to get routed to the right endpoint as determined by the routing type.</span></span> <span data-ttu-id="66bb3-125">En este caso, todas las solicitudes se enrutan al punto de conexión con la menor latencia de red del cliente.</span><span class="sxs-lookup"><span data-stu-id="66bb3-125">In this case all requests are routed to the endpoint with the lowest latency from the client's network.</span></span>
6. <span data-ttu-id="66bb3-126">Una vez que el perfil de Traffic Manager esté en funcionamiento, edite el registro DNS en el servidor DNS relevante para redireccionar el nombre de dominio de la empresa al nombre de dominio del Administrador de tráfico.</span><span class="sxs-lookup"><span data-stu-id="66bb3-126">Once your Traffic Manager profile is working, edit the DNS record on your authoritative DNS server to point your company domain name to the Traffic Manager domain name.</span></span>

![Configuración del método de enrutamiento del tráfico de rendimiento con Traffic Manager][1]

## <a name="next-steps"></a><span data-ttu-id="66bb3-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="66bb3-128">Next steps</span></span>

- <span data-ttu-id="66bb3-129">Obtenga información sobre el [método de enrutamiento del tráfico ponderado](traffic-manager-configure-weighted-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="66bb3-129">Learn about [weighted traffic routing method](traffic-manager-configure-weighted-routing-method.md).</span></span>
- <span data-ttu-id="66bb3-130">Sepa cómo funciona el [método de enrutamiento por prioridad](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="66bb3-130">Learn about [priority routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="66bb3-131">Aprenda a usar el [método de enrutamiento geográfico](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="66bb3-131">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="66bb3-132">Información sobre cómo [probar la configuración de Traffic Manager](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="66bb3-132">Learn how to [test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png