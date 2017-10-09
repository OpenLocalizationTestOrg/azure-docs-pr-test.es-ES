---
title: "aaaEnable o deshabilitar la supervisión de VM de Azure"
description: "Describe cómo tooEnable o deshabilitar la supervisión de VM de Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a><span data-ttu-id="aeaaa-103">Habilitación o deshabilitación de la supervisión de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="aeaaa-103">Enable or Disable Azure VM Monitoring</span></span>

<span data-ttu-id="aeaaa-104">Esta sección describe cómo tooenable o deshabilitar la supervisión en Virtual equipos ejecutan en Azure.</span><span class="sxs-lookup"><span data-stu-id="aeaaa-104">This section describes how tooenable or disable monitoring on Virtual machines running on Azure.</span></span> <span data-ttu-id="aeaaa-105">Puede habilitar o deshabilitar la supervisión mediante el portal de Hola o interfaz de línea de comandos de Azure para Mac, Linux y Windows (Hola CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="aeaaa-105">You can enable or disable monitoring using hello portal or Azure Command-line Interface for Mac, Linux, and Windows (hello Azure CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aeaaa-106">Este documento describe la versión 2.3 de hello extensión de diagnóstico de Linux, que está en desuso.</span><span class="sxs-lookup"><span data-stu-id="aeaaa-106">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="aeaaa-107">Se admitirá la versión 2.3 hasta el 30 de junio de 2018.</span><span class="sxs-lookup"><span data-stu-id="aeaaa-107">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="aeaaa-108">Versión 3.0 de hello que extensión de diagnóstico de Linux pueden habilitarse en su lugar.</span><span class="sxs-lookup"><span data-stu-id="aeaaa-108">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="aeaaa-109">Para obtener más información, consulte [Hola documentación](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="aeaaa-109">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a><span data-ttu-id="aeaaa-110">Habilitar / deshabilitar la supervisión a través de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="aeaaa-110">Enable / Disable Monitoring through hello Azure portal</span></span>

<span data-ttu-id="aeaaa-111">Puede habilitar la supervisión de la máquina virtual de Azure, que proporciona datos sobre la instancia en períodos de un minuto.</span><span class="sxs-lookup"><span data-stu-id="aeaaa-111">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span></span> <span data-ttu-id="aeaaa-112">(se aplican cambios de almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="aeaaa-112">(storage changes apply).</span></span> <span data-ttu-id="aeaaa-113">Datos de diagnóstico detallada, a continuación, están disponibles para hello VM en gráficos de portal de Hola o a través de hello API.</span><span class="sxs-lookup"><span data-stu-id="aeaaa-113">Detailed diagnostics data is then available for hello VM in hello portal graphs or through hello API.</span></span> <span data-ttu-id="aeaaa-114">De forma predeterminada, Azure Portal permite la supervisión basada en host de un conjunto limitado de métricas.</span><span class="sxs-lookup"><span data-stu-id="aeaaa-114">By default, Azure portal enables host-based monitoring of a limited set of metrics.</span></span> <span data-ttu-id="aeaaa-115">Puede habilitar la supervisión de las métricas desde dentro de una máquina virtual mientras Hola que VM esté en funcionamiento o en estado detenido.</span><span class="sxs-lookup"><span data-stu-id="aeaaa-115">You can enable monitoring of metrics from within a VM while hello VM is running or in stopped state.</span></span>

* <span data-ttu-id="aeaaa-116">Abra hello Azure portal en [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aeaaa-116">Open hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
* <span data-ttu-id="aeaaa-117">Hola barra de navegación izquierda, haga clic en máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="aeaaa-117">In hello left navigation, click Virtual machines.</span></span>
* <span data-ttu-id="aeaaa-118">En máquinas virtuales de hello lista, seleccione una instancia de ejecución o detenida.</span><span class="sxs-lookup"><span data-stu-id="aeaaa-118">In hello list Virtual machines, select a running or stopped instance.</span></span> <span data-ttu-id="aeaaa-119">se abre la hoja de "Máquina Virtual" Hola.</span><span class="sxs-lookup"><span data-stu-id="aeaaa-119">hello "Virtual machine" blade opens.</span></span>
* <span data-ttu-id="aeaaa-120">Haga clic en Toda la configuración.</span><span class="sxs-lookup"><span data-stu-id="aeaaa-120">Click All settings.</span></span>
* <span data-ttu-id="aeaaa-121">Haga clic en Diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="aeaaa-121">Click Diagnostics.</span></span>
* <span data-ttu-id="aeaaa-122">Cambiar estado tooOn o desactivado.</span><span class="sxs-lookup"><span data-stu-id="aeaaa-122">Change status tooOn or Off.</span></span> <span data-ttu-id="aeaaa-123">También puede elegir en este nivel de hoja Hola de detalles que le gustaría tener tooenable en la máquina virtual de supervisión.</span><span class="sxs-lookup"><span data-stu-id="aeaaa-123">You can also pick in this blade hello level of monitoring details you would like tooenable for your virtual machine.</span></span>

![Habilitar / deshabilitar la supervisión a través de hello portal de Azure.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a><span data-ttu-id="aeaaa-125">Habilitación y deshabilitación de la supervisión con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="aeaaa-125">Enable / Disable Monitoring with Azure CLI</span></span>

<span data-ttu-id="aeaaa-126">tooenable de supervisión para una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="aeaaa-126">tooenable monitoring for an Azure VM.</span></span>

* <span data-ttu-id="aeaaa-127">Cree un archivo (con un nombre como PrivateConfig.json):</span><span class="sxs-lookup"><span data-stu-id="aeaaa-127">Create a file (named such as PrivateConfig.json):</span></span>

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* <span data-ttu-id="aeaaa-128">Habilitar la extensión de hello mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="aeaaa-128">Enable hello extension via Azure CLI.</span></span>

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

<span data-ttu-id="aeaaa-129">Para obtener más información, consulte [rendimiento y datos de diagnóstico de uso de la extensión de diagnóstico de Linux tooMonitor Linux VM](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="aeaaa-129">For more information, see [Using Linux Diagnostic Extension tooMonitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
