---
title: 'Flujo de grupo de seguridad de red registra aaaManage con Monitor de red de Azure: 1.0 de CLI de Azure | Documentos de Microsoft'
description: "Esta página explica cómo toomanage flujo de grupo de seguridad de red se registra en el Monitor de red de Azure con Azure CLI 1.0"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2535eea665a99cffe7569a8d976333435f946a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli-10"></a><span data-ttu-id="37fdb-103">Configuración de registros de flujo de grupos de seguridad de red con la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="37fdb-103">Configuring Network Security Group Flow logs with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="37fdb-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="37fdb-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="37fdb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="37fdb-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="37fdb-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="37fdb-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="37fdb-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="37fdb-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="37fdb-108">API DE REST</span><span class="sxs-lookup"><span data-stu-id="37fdb-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="37fdb-109">Registros de flujo de grupo de seguridad de red son una característica del Monitor de red que permite tooview información sobre el tráfico IP de entrada y de salida a través de un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="37fdb-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="37fdb-110">Estos registros de flujo se escriben en formato json y mostrar salidos y flujos de entrada en cada regla, Hola flujo Hola NIC que se aplica, tupla de 5 información acerca del flujo de hello (protocolo IP de origen/destino, puerto de origen/destino,) y si hello se permita el tráfico o denegado.</span><span class="sxs-lookup"><span data-stu-id="37fdb-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="37fdb-111">En este artículo, se utiliza la multiplataforma Azure CLI 1.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="37fdb-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="37fdb-112">Network Watcher usa actualmente Azure CLI 1.0 para la compatibilidad con CLI.</span><span class="sxs-lookup"><span data-stu-id="37fdb-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="37fdb-113">Registro del proveedor de Insights</span><span class="sxs-lookup"><span data-stu-id="37fdb-113">Register Insights provider</span></span>

<span data-ttu-id="37fdb-114">En orden para el flujo de registro toowork correctamente, Hola **Microsoft.Insights** proveedor debe estar registrado.</span><span class="sxs-lookup"><span data-stu-id="37fdb-114">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="37fdb-115">Si no está seguro de si hello **Microsoft.Insights** proveedor está registrado, hello ejecución siguiente secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="37fdb-115">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```azurecli
azure provider register --namespace Microsoft.Insights --subscription <subscriptionid>
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="37fdb-116">Habilitación de los registros de flujo de grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="37fdb-116">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="37fdb-117">Hola comando tooenable flujo registros se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="37fdb-117">hello command tooenable flow logs is shown in hello following example:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e true
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="37fdb-118">Deshabilitación de los registros de flujo de grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="37fdb-118">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="37fdb-119">Hola de uso después de registros de flujo de toodisable de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="37fdb-119">Use hello following example toodisable flow logs:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e false
```

## <a name="download-a-flow-log"></a><span data-ttu-id="37fdb-120">Descarga de un registro de flujo</span><span class="sxs-lookup"><span data-stu-id="37fdb-120">Download a Flow log</span></span>

<span data-ttu-id="37fdb-121">ubicación de almacenamiento de Hola de un registro de flujo se define en la creación.</span><span class="sxs-lookup"><span data-stu-id="37fdb-121">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="37fdb-122">Un tooaccess herramienta adecuada estas cuentas de almacenamiento de tooa de guardar registros de flujo es Microsoft Azure Storage Explorer, que puede descargarse aquí: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="37fdb-122">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="37fdb-123">Si se especifica una cuenta de almacenamiento, archivos de captura de paquetes se guardan tooa cuenta de almacenamiento en hello ubicación siguiente:</span><span class="sxs-lookup"><span data-stu-id="37fdb-123">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="37fdb-124">Para obtener información acerca de la estructura de Hola de registro de hello visite [información general de registro de flujo de grupo de seguridad de red](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="37fdb-124">For information about hello structure of hello log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="37fdb-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="37fdb-125">Next Steps</span></span>

<span data-ttu-id="37fdb-126">Obtenga información acerca de cómo demasiado[visualizar los registros de flujo NSG con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="37fdb-126">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="37fdb-127">Obtenga información acerca de cómo demasiado[visualizar los registros de flujo NSG con herramientas de código abierto](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="37fdb-127">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
