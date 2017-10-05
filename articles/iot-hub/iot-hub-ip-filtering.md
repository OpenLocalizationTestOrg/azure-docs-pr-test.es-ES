---
title: "Filtros de conexión IP de Azure IoT Hub | Microsoft Docs"
description: "Describe cómo usar el filtrado de IP para bloquear las conexiones de direcciones IP específicas de su instancia de Azure IoT Hub. Puede bloquear conexiones de direcciones IP concretas o de intervalos."
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 85f5f044faddd5180f0c19d3f2c235b20f6373d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-ip-filters"></a><span data-ttu-id="ad0ad-104">Uso de filtros IP</span><span class="sxs-lookup"><span data-stu-id="ad0ad-104">Use IP filters</span></span>

<span data-ttu-id="ad0ad-105">La seguridad es un aspecto importante de cualquier solución de IoT basada en Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="ad0ad-106">En ciertas ocasiones necesitará especificar explícitamente las direcciones IP desde las que se pueden conectar los dispositivos como parte de la configuración de seguridad.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-106">Sometimes you need to explicitly specify the IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="ad0ad-107">La característica de _filtro IP_ le permite configurar reglas para rechazar o aceptar tráfico de direcciones IPv4 específicas.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-107">The _IP filter_ feature enables you to configure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-to-use"></a><span data-ttu-id="ad0ad-108">Cuándo se deben usar</span><span class="sxs-lookup"><span data-stu-id="ad0ad-108">When to use</span></span>

<span data-ttu-id="ad0ad-109">Hay dos casos específicos cuando resulta útil bloquear los puntos de conexión de IoT hub para determinadas direcciones IP:</span><span class="sxs-lookup"><span data-stu-id="ad0ad-109">There are two specific use-cases when it is useful to block the IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="ad0ad-110">IoT Hub debe recibir tráfico solo de un intervalo concreto de direcciones IP y rechazar todo lo demás.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="ad0ad-111">Por ejemplo, cuando se usa IoT Hub con [Azure ExpressRoute] para crear conexiones privadas entre una instancia de IoT Hub y la infraestructura local.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-111">For example, you are using your IoT hub with [Azure Express Route] to create private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="ad0ad-112">Cuando necesite rechazar el tráfico de direcciones IP que el administrador de IoT Hub haya identificado como sospechosas.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-112">You need to reject traffic from IP addresses that have been identified as suspicious by the IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="ad0ad-113">Cómo se aplican las reglas de filtro</span><span class="sxs-lookup"><span data-stu-id="ad0ad-113">How filter rules are applied</span></span>

<span data-ttu-id="ad0ad-114">Las reglas de filtro IP se aplican en el nivel de servicio de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-114">The IP filter rules are applied at the IoT Hub service level.</span></span> <span data-ttu-id="ad0ad-115">Por lo tanto, las reglas de filtro IP se aplican a todas las conexiones de los dispositivos y aplicaciones de back-end mediante un protocolo admitido.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-115">Therefore the IP filter rules apply to all connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="ad0ad-116">Cualquier intento de conexión desde una dirección IP que coincida con una regla IP de rechazo en su centro de IoT recibe un código de estado 401 no autorizado y la descripción.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="ad0ad-117">El mensaje de respuesta no menciona la regla IP.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-117">The response message does not mention the IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="ad0ad-118">Configuración predeterminada</span><span class="sxs-lookup"><span data-stu-id="ad0ad-118">Default setting</span></span>

<span data-ttu-id="ad0ad-119">De forma predeterminada, la cuadrícula de **filtro IP** del portal para un centro de IoT está vacía.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-119">By default, the **IP Filter** grid in the portal for an IoT hub is empty.</span></span> <span data-ttu-id="ad0ad-120">Esta configuración predeterminada significa que el centro de acepta la conexión de cualquier dirección IP.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="ad0ad-121">Esta configuración predeterminada es equivalente a una regla que acepta el intervalo de direcciones IP 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-121">This default setting is equivalent to a rule that accepts the 0.0.0.0/0 IP address range.</span></span>

![Configuración predeterminada de filtro de direcciones IP de IoT Hub][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="ad0ad-123">Incorporación o edición de una regla de filtro IP</span><span class="sxs-lookup"><span data-stu-id="ad0ad-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="ad0ad-124">Al agregar una regla de filtro IP, le pediremos los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="ad0ad-124">When you add an IP filter rule, you are prompted for the following values:</span></span>

- <span data-ttu-id="ad0ad-125">Un **nombre de regla de filtro IP** que debe ser una cadena única, que distinta mayúsculas de minúsculas y alfanumérica de hasta 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up to 128 characters long.</span></span> <span data-ttu-id="ad0ad-126">Solo se aceptan los caracteres alfanuméricos de 7 bits ASCII más `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}`.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-126">Only the ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="ad0ad-127">Seleccione un **Rechazar** o **Aceptar** como **acción** para la regla de filtro IP.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-127">Select a **reject** or **accept** as the **action** for the IP filter rule.</span></span>
- <span data-ttu-id="ad0ad-128">Proporcione una única dirección IPv4 o un bloque de direcciones IP en la notación CIDR.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="ad0ad-129">Por ejemplo, en notación CIDR, 192.168.100.0/22 representa las direcciones IPv4 de 1024 de 192.168.100.0 a 192.168.103.255.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-129">For example, in CIDR notation 192.168.100.0/22 represents the 1024 IPv4 addresses from 192.168.100.0 to 192.168.103.255.</span></span>

![Incorporación de una regla de filtro IP a una instancia de IoT Hub][img-ip-filter-add-rule]

<span data-ttu-id="ad0ad-131">Tras guardar la regla, se mostrará una alerta que le informará de que la actualización está en curso.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-131">After you save the rule, you see an alert notifying you that the update is in progress.</span></span>

![Notificación acerca de cómo guardar una regla de filtro IP][img-ip-filter-save-new-rule]

<span data-ttu-id="ad0ad-133">La opción **Agregar** está deshabilitada cuando se alcanza el máximo de 10 reglas de filtro IP.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-133">The **Add** option is disabled when you reach the maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="ad0ad-134">Puede editar una regla existente al hacer doble clic en la fila que la contiene.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-134">You can edit an existing rule by double-clicking the row that contains the rule.</span></span>

> [!NOTE]
> <span data-ttu-id="ad0ad-135">Rechazar direcciones de IP puede evitar que otros servicios de Azure (por ejemplo, Azure Stream Analytics, Azure Virtual Machines o el Explorador de dispositivos del portal) interactúen con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or the Device Explorer in the portal) from interacting with the IoT hub.</span></span>

> [!WARNING]
> <span data-ttu-id="ad0ad-136">Si usa Azure Stream Analytics (ASA) para leer mensajes de una instancia de IoT Hub con el filtrado IP habilitado, use el punto de conexión y el nombre compatibles con Event Hub de su instancia de IoT Hub en la cadena de conexión de ASA.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-136">If you use Azure Stream Analytics (ASA) to read messages from an IoT hub with IP filtering enabled, use the Event Hub-compatible name and endpoint of your IoT Hub in the ASA connection string.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="ad0ad-137">Eliminación de una regla de filtro IP</span><span class="sxs-lookup"><span data-stu-id="ad0ad-137">Delete an IP filter rule</span></span>

<span data-ttu-id="ad0ad-138">Para eliminar una regla de filtro IP, seleccione una o varias reglas en la cuadrícula y haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-138">To delete an IP filter rule, select one or more rules in the grid and click **Delete**.</span></span>

![Eliminación de una regla de filtro IP de IoT Hub][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="ad0ad-140">Evaluación de las reglas de filtro IP</span><span class="sxs-lookup"><span data-stu-id="ad0ad-140">IP filter rule evaluation</span></span>

<span data-ttu-id="ad0ad-141">Las reglas de filtro IP se aplican en orden y la primera regla que coincida con la dirección IP determina la acción de aceptar o rechazar.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-141">IP filter rules are applied in order and the first rule that matches the IP address determines the accept or reject action.</span></span>

<span data-ttu-id="ad0ad-142">Por ejemplo, si desea aceptar las direcciones del intervalo 192.168.100.0/22 y rechazar todas las demás, la primera regla de la cuadrícula debe aceptar el intervalo de direcciones 192.168.100.0/22.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-142">For example, if you want to accept addresses in the range 192.168.100.0/22 and reject everything else, the first rule in the grid should accept the address range 192.168.100.0/22.</span></span> <span data-ttu-id="ad0ad-143">La siguiente regla debe rechazar todas las direcciones mediante el intervalo 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-143">The next rule should reject all addresses by using the range 0.0.0.0/0.</span></span>

<span data-ttu-id="ad0ad-144">Puede cambiar el orden de las reglas de filtro IP en la cuadrícula al hacer clic en los tres puntos verticales situados al principio de las filas y mediante el método arrastrar y colocar.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-144">You can change the order of your IP filter rules in the grid by clicking the three vertical dots at the start of a row and using drag and drop.</span></span>

<span data-ttu-id="ad0ad-145">Para guardar el nuevo orden de reglas de filtro IP, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ad0ad-145">To save your new IP filter rule order, click **Save**.</span></span>

![Cambiar el orden de las reglas de filtro IP de IoT Hub][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="ad0ad-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ad0ad-147">Next steps</span></span>

<span data-ttu-id="ad0ad-148">Para explorar aún más las funcionalidades de IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="ad0ad-148">To further explore the capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="ad0ad-149">[Supervisión de operaciones][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="ad0ad-149">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="ad0ad-150">[Métricas de IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="ad0ad-150">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
<span data-ttu-id="ad0ad-151">[Azure ExpressRoute]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services</span><span class="sxs-lookup"><span data-stu-id="ad0ad-151">[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services</span></span>

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md