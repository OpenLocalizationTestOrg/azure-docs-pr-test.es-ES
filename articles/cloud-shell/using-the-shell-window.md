---
title: "Uso de la ventana Azure Cloud Shell (versión preliminar) | Microsoft Docs"
description: Tutorial de la ventana Azure Cloud Shell.
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: juluk
ms.openlocfilehash: a47961dfdaf178a6b793bd68105d9792a9275bb3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-azure-cloud-shell-window"></a><span data-ttu-id="a8b9d-103">Uso de la ventana Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="a8b9d-103">Using the Azure Cloud Shell window</span></span>

<span data-ttu-id="a8b9d-104">En este documento se explica cómo usar la ventana Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="a8b9d-104">This document explains how to use the Cloud Shell window.</span></span>

## <a name="concurrent-sessions"></a><span data-ttu-id="a8b9d-105">Sesiones simultáneas</span><span class="sxs-lookup"><span data-stu-id="a8b9d-105">Concurrent sessions</span></span>
<span data-ttu-id="a8b9d-106">Cloud Shell permite varias sesiones simultáneas en pestañas del explorador posibilitando que cada sesión exista como un proceso Bash independiente.</span><span class="sxs-lookup"><span data-stu-id="a8b9d-106">Cloud Shell enables multiple concurrent sessions across browser tabs by allowing each session to exist as a separate Bash process.</span></span>
<span data-ttu-id="a8b9d-107">Si sale de una sesión, asegúrese de salir de cada ventana de sesión, ya que cada proceso se ejecuta de forma independiente aunque se ejecuten en la misma máquina.</span><span class="sxs-lookup"><span data-stu-id="a8b9d-107">If exiting a session, be sure to exit from each session window as each process runs independently although they run on the same machine.</span></span>

## <a name="restart-cloud-shell"></a><span data-ttu-id="a8b9d-108">Reinicio de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="a8b9d-108">Restart Cloud Shell</span></span>
![](media/recycle.png)
> [!WARNING]
> <span data-ttu-id="a8b9d-109">Al reiniciar Cloud Shell se restablecerá el estado de la máquina y todos los archivos que no conserve el recurso compartido de archivos se perderán.</span><span class="sxs-lookup"><span data-stu-id="a8b9d-109">Restarting Cloud Shell will reset machine state and any files not persisted by your file share will be lost.</span></span>

* <span data-ttu-id="a8b9d-110">Haga clic en el icono de reinicio de la barra de herramientas para recibir el nuevo entorno Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="a8b9d-110">Click the restart icon on the toolbar to receive a new Cloud Shell environment.</span></span>

## <a name="minimize--maximize-cloud-shell-window"></a><span data-ttu-id="a8b9d-111">Minimizar y maximizar la ventana Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="a8b9d-111">Minimize & maximize Cloud Shell window</span></span>
![](media/minmax.png)
* <span data-ttu-id="a8b9d-112">Haga clic en el icono Minimizar situado en la parte superior derecha de la ventana para ocultarla.</span><span class="sxs-lookup"><span data-stu-id="a8b9d-112">Click the minimize icon on the top right of the window to hide it.</span></span> <span data-ttu-id="a8b9d-113">Haga clic en el icono Cloud Shell de nuevo para mostrarla.</span><span class="sxs-lookup"><span data-stu-id="a8b9d-113">Click the Cloud Shell icon again to unhide.</span></span>
* <span data-ttu-id="a8b9d-114">Haga clic en el icono Maximizar para establecer la ventana en la altura máxima.</span><span class="sxs-lookup"><span data-stu-id="a8b9d-114">Click the maximize icon to set window to max height.</span></span> <span data-ttu-id="a8b9d-115">Para restablecer el tamaño anterior de la ventana, haga clic en Restaurar.</span><span class="sxs-lookup"><span data-stu-id="a8b9d-115">To restore window to previous size, click restore.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="a8b9d-116">Copiar y pegar</span><span class="sxs-lookup"><span data-stu-id="a8b9d-116">Copy and paste</span></span>
* <span data-ttu-id="a8b9d-117">Windows: `Ctrl-insert` para copiar y `Shift-insert` para pegar.</span><span class="sxs-lookup"><span data-stu-id="a8b9d-117">Windows: `Ctrl-insert` to copy and `Shift-insert` to paste.</span></span> <span data-ttu-id="a8b9d-118">Hacer clic con el botón derecho en la lista desplegable también habilita copiar y pegar.</span><span class="sxs-lookup"><span data-stu-id="a8b9d-118">Right-click dropdown can also enable copy/paste.</span></span>
  * <span data-ttu-id="a8b9d-119">Es posible que Firefox o IE no admitan los permisos del Portapapeles correctamente.</span><span class="sxs-lookup"><span data-stu-id="a8b9d-119">FireFox/IE may not support clipboard permissions properly.</span></span>
* <span data-ttu-id="a8b9d-120">Mac OS: `Cmd-c` para copiar y `Cmd-v` para pegar.</span><span class="sxs-lookup"><span data-stu-id="a8b9d-120">Mac OS: `Cmd-c` to copy and `Cmd-v` to paste.</span></span> <span data-ttu-id="a8b9d-121">Hacer clic con el botón derecho en la lista desplegable también habilita copiar y pegar.</span><span class="sxs-lookup"><span data-stu-id="a8b9d-121">Right-click dropdown can also enable copy/paste.</span></span>

## <a name="resize-cloud-shell-window"></a><span data-ttu-id="a8b9d-122">Cambio del tamaño de la ventana Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="a8b9d-122">Resize Cloud Shell window</span></span>
* <span data-ttu-id="a8b9d-123">Haga clic y arrastre el borde superior de la barra de herramientas hacia arriba o hacia abajo para cambiar el tamaño de la ventana Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="a8b9d-123">Click and drag the top edge of the toolbar up or down to resize the Cloud Shell window.</span></span>

## <a name="scrolling-text-display"></a><span data-ttu-id="a8b9d-124">Desplazamiento de la presentación del texto</span><span class="sxs-lookup"><span data-stu-id="a8b9d-124">Scrolling text display</span></span>
* <span data-ttu-id="a8b9d-125">Desplácese con el mouse o panel táctil para mover texto terminal.</span><span class="sxs-lookup"><span data-stu-id="a8b9d-125">Scroll with your mouse or touchpad to move terminal text.</span></span>

## <a name="exit-command"></a><span data-ttu-id="a8b9d-126">Comando Exit</span><span class="sxs-lookup"><span data-stu-id="a8b9d-126">Exit command</span></span>
<span data-ttu-id="a8b9d-127">Al ejecutar `exit` se terminará la sesión activa.</span><span class="sxs-lookup"><span data-stu-id="a8b9d-127">Running `exit` terminates the active session.</span></span> <span data-ttu-id="a8b9d-128">Este comportamiento se produce de forma predeterminada después de 20 minutos sin interacción.</span><span class="sxs-lookup"><span data-stu-id="a8b9d-128">This behavior occurs by default after 20 minutes without interaction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8b9d-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a8b9d-129">Next steps</span></span>
[<span data-ttu-id="a8b9d-130">Inicio rápido de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="a8b9d-130">Cloud Shell Quickstart</span></span>](quickstart.md)
