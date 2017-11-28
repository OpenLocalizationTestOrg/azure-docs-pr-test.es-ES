---
title: "filtros de conexión de IP del centro de IoT aaaAzure | Documentos de Microsoft"
description: "Cómo las direcciones IP toouse filtrado de conexiones de tooblock de IP específica para tooyour centro de IoT de Azure. Puede bloquear conexiones de direcciones IP concretas o de intervalos."
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
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a><span data-ttu-id="69e48-104">Uso de filtros IP</span><span class="sxs-lookup"><span data-stu-id="69e48-104">Use IP filters</span></span>

<span data-ttu-id="69e48-105">La seguridad es un aspecto importante de cualquier solución de IoT basada en Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="69e48-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="69e48-106">En ciertas ocasiones necesitará tooexplicitly especificar direcciones IP de Hola desde el que pueden conectar dispositivos como parte de la configuración de seguridad.</span><span class="sxs-lookup"><span data-stu-id="69e48-106">Sometimes you need tooexplicitly specify hello IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="69e48-107">Hola _filtro IP_ característica permite tooconfigure reglas para rechazar o aceptar tráfico de direcciones IPv4 específicas.</span><span class="sxs-lookup"><span data-stu-id="69e48-107">hello _IP filter_ feature enables you tooconfigure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-toouse"></a><span data-ttu-id="69e48-108">Cuando toouse</span><span class="sxs-lookup"><span data-stu-id="69e48-108">When toouse</span></span>

<span data-ttu-id="69e48-109">Hay dos casos de uso específicos cuando resulta útil tooblock Hola centro de IoT los puntos de conexión para determinadas direcciones IP:</span><span class="sxs-lookup"><span data-stu-id="69e48-109">There are two specific use-cases when it is useful tooblock hello IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="69e48-110">IoT Hub debe recibir tráfico solo de un intervalo concreto de direcciones IP y rechazar todo lo demás.</span><span class="sxs-lookup"><span data-stu-id="69e48-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="69e48-111">Por ejemplo, se utiliza el centro de IoT con [Azure Express Route] toocreate conexiones privadas entre un centro de IoT y su infraestructura local.</span><span class="sxs-lookup"><span data-stu-id="69e48-111">For example, you are using your IoT hub with [Azure Express Route] toocreate private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="69e48-112">Necesita tooreject tráfico de direcciones IP que se han identificado como sospechosa por administrador de base de datos central de hello IoT.</span><span class="sxs-lookup"><span data-stu-id="69e48-112">You need tooreject traffic from IP addresses that have been identified as suspicious by hello IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="69e48-113">Cómo se aplican las reglas de filtro</span><span class="sxs-lookup"><span data-stu-id="69e48-113">How filter rules are applied</span></span>

<span data-ttu-id="69e48-114">se aplican las reglas de filtro IP de Hello en Hola de nivel de servicio del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="69e48-114">hello IP filter rules are applied at hello IoT Hub service level.</span></span> <span data-ttu-id="69e48-115">Por lo tanto, las reglas de filtro IP de hello aplican las conexiones de tooall desde dispositivos y aplicaciones de back-end mediante un protocolo admitido.</span><span class="sxs-lookup"><span data-stu-id="69e48-115">Therefore hello IP filter rules apply tooall connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="69e48-116">Cualquier intento de conexión desde una dirección IP que coincida con una regla IP de rechazo en su centro de IoT recibe un código de estado 401 no autorizado y la descripción.</span><span class="sxs-lookup"><span data-stu-id="69e48-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="69e48-117">mensaje de respuesta de Hello no mencione la regla IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="69e48-117">hello response message does not mention hello IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="69e48-118">Configuración predeterminada</span><span class="sxs-lookup"><span data-stu-id="69e48-118">Default setting</span></span>

<span data-ttu-id="69e48-119">De forma predeterminada, Hola **filtro IP** cuadrícula en el portal de Hola para un centro de IoT está vacío.</span><span class="sxs-lookup"><span data-stu-id="69e48-119">By default, hello **IP Filter** grid in hello portal for an IoT hub is empty.</span></span> <span data-ttu-id="69e48-120">Esta configuración predeterminada significa que el centro de acepta la conexión de cualquier dirección IP.</span><span class="sxs-lookup"><span data-stu-id="69e48-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="69e48-121">Esta configuración predeterminada es la regla de tooa equivalente que acepta el intervalo de direcciones IP de hello 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="69e48-121">This default setting is equivalent tooa rule that accepts hello 0.0.0.0/0 IP address range.</span></span>

![Configuración predeterminada de filtro de direcciones IP de IoT Hub][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="69e48-123">Incorporación o edición de una regla de filtro IP</span><span class="sxs-lookup"><span data-stu-id="69e48-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="69e48-124">Cuando se agrega una regla de filtrado IP, le pediremos Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="69e48-124">When you add an IP filter rule, you are prompted for hello following values:</span></span>

- <span data-ttu-id="69e48-125">Un **nombre de regla de filtro IP** que debe ser una cadena única, entre mayúsculas y minúsculas, alfanumérica seguridad too128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="69e48-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up too128 characters long.</span></span> <span data-ttu-id="69e48-126">Solo caracteres alfanuméricos de hello ASCII 7 bits más `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` se aceptan.</span><span class="sxs-lookup"><span data-stu-id="69e48-126">Only hello ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="69e48-127">Seleccione un **rechazar** o **Aceptar** como hello **acción** para regla de filtrado IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="69e48-127">Select a **reject** or **accept** as hello **action** for hello IP filter rule.</span></span>
- <span data-ttu-id="69e48-128">Proporcione una única dirección IPv4 o un bloque de direcciones IP en la notación CIDR.</span><span class="sxs-lookup"><span data-stu-id="69e48-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="69e48-129">Por ejemplo, en CIDR notación 192.168.100.0/22 representa las direcciones IPv4 Hola 1024 de 192.168.100.0 too192.168.103.255.</span><span class="sxs-lookup"><span data-stu-id="69e48-129">For example, in CIDR notation 192.168.100.0/22 represents hello 1024 IPv4 addresses from 192.168.100.0 too192.168.103.255.</span></span>

![Agregar un centro de IoT IP tooan de regla de filtro][img-ip-filter-add-rule]

<span data-ttu-id="69e48-131">Después de guardar la regla de hello, verá una alerta que le avise que esa actualización Hola está en curso.</span><span class="sxs-lookup"><span data-stu-id="69e48-131">After you save hello rule, you see an alert notifying you that hello update is in progress.</span></span>

![Notificación acerca de cómo guardar una regla de filtro IP][img-ip-filter-save-new-rule]

<span data-ttu-id="69e48-133">Hola **agregar** opción está deshabilitada cuando se alcanza el máximo de Hola de 10 reglas de filtrado IP.</span><span class="sxs-lookup"><span data-stu-id="69e48-133">hello **Add** option is disabled when you reach hello maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="69e48-134">Puede editar una regla existente haciendo doble clic en la fila de Hola que contiene la regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="69e48-134">You can edit an existing rule by double-clicking hello row that contains hello rule.</span></span>

> [!NOTE]
> <span data-ttu-id="69e48-135">Rechazar IP direcciones pueden impedir que otros servicios de Azure (por ejemplo, análisis de transmisiones de Azure, máquinas virtuales de Azure o hello explorador del dispositivo en el portal de hello) interactuar con el centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="69e48-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or hello Device Explorer in hello portal) from interacting with hello IoT hub.</span></span>

> [!WARNING]
> <span data-ttu-id="69e48-136">Si usa mensajes de tooread de análisis de transmisiones de Azure (ASA) de un centro de IoT con filtrado de IP habilitada, utilizar nombre de concentrador de eventos-compatible de Hola y el extremo de su centro de IoT Hola cadena de conexión del ASA.</span><span class="sxs-lookup"><span data-stu-id="69e48-136">If you use Azure Stream Analytics (ASA) tooread messages from an IoT hub with IP filtering enabled, use hello Event Hub-compatible name and endpoint of your IoT Hub in hello ASA connection string.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="69e48-137">Eliminación de una regla de filtro IP</span><span class="sxs-lookup"><span data-stu-id="69e48-137">Delete an IP filter rule</span></span>

<span data-ttu-id="69e48-138">toodelete una regla de filtro IP, seleccione una o varias reglas en la cuadrícula de Hola y haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="69e48-138">toodelete an IP filter rule, select one or more rules in hello grid and click **Delete**.</span></span>

![Eliminación de una regla de filtro IP de IoT Hub][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="69e48-140">Evaluación de las reglas de filtro IP</span><span class="sxs-lookup"><span data-stu-id="69e48-140">IP filter rule evaluation</span></span>

<span data-ttu-id="69e48-141">Se aplican las reglas de filtro IP en orden y primera regla Hola de esa dirección IP de coincidencias Hola determina Hola Aceptar o rechazar la acción.</span><span class="sxs-lookup"><span data-stu-id="69e48-141">IP filter rules are applied in order and hello first rule that matches hello IP address determines hello accept or reject action.</span></span>

<span data-ttu-id="69e48-142">Por ejemplo, si desea direcciones tooaccept en hello intervalo 192.168.100.0/22 y todo lo demás rechazar, Hola primera regla cuadrícula Hola debe aceptar Hola dirección intervalo 192.168.100.0/22.</span><span class="sxs-lookup"><span data-stu-id="69e48-142">For example, if you want tooaccept addresses in hello range 192.168.100.0/22 and reject everything else, hello first rule in hello grid should accept hello address range 192.168.100.0/22.</span></span> <span data-ttu-id="69e48-143">regla siguiente Hola debe rechazar todas las direcciones mediante el uso de intervalo de hello 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="69e48-143">hello next rule should reject all addresses by using hello range 0.0.0.0/0.</span></span>

<span data-ttu-id="69e48-144">Puede cambiar el orden de Hola de las reglas de filtrado IP en la cuadrícula de hello haciendo clic en hello tres puntos verticales situados al principio de Hola de una fila y mediante arrastrar y colocar.</span><span class="sxs-lookup"><span data-stu-id="69e48-144">You can change hello order of your IP filter rules in hello grid by clicking hello three vertical dots at hello start of a row and using drag and drop.</span></span>

<span data-ttu-id="69e48-145">filtrar de la IP nueva toosave orden de reglas, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="69e48-145">toosave your new IP filter rule order, click **Save**.</span></span>

![Cambiar el orden de Hola de las reglas de filtrado de IP del centro de IoT][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="69e48-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="69e48-147">Next steps</span></span>

<span data-ttu-id="69e48-148">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="69e48-148">toofurther explore hello capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="69e48-149">[Supervisión de operaciones][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="69e48-149">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="69e48-150">[Métricas de IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="69e48-150">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md