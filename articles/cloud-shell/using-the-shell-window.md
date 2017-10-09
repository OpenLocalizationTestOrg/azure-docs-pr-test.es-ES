---
title: ventana del Shell de nube de Azure (vista previa) de hello aaaUsing | Documentos de Microsoft
description: Ventana del Shell de nube de Azure de tutorial Hola.
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
ms.openlocfilehash: 571db3c8e177799a9e05f38a7cf8d2a4d5f8c8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cloud-shell-window"></a><span data-ttu-id="d68bd-103">Utilizando la ventana del Shell de nube de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="d68bd-103">Using hello Azure Cloud Shell window</span></span>

<span data-ttu-id="d68bd-104">Este documento explica cómo toouse Hola ventana del Shell en la nube.</span><span class="sxs-lookup"><span data-stu-id="d68bd-104">This document explains how toouse hello Cloud Shell window.</span></span>

## <a name="concurrent-sessions"></a><span data-ttu-id="d68bd-105">Sesiones simultáneas</span><span class="sxs-lookup"><span data-stu-id="d68bd-105">Concurrent sessions</span></span>
<span data-ttu-id="d68bd-106">En la nube Shell permite varias sesiones simultáneas en pestañas del explorador al permitir que cada tooexist sesión como un proceso independiente de Bash.</span><span class="sxs-lookup"><span data-stu-id="d68bd-106">Cloud Shell enables multiple concurrent sessions across browser tabs by allowing each session tooexist as a separate Bash process.</span></span>
<span data-ttu-id="d68bd-107">Si salir de una sesión, asegúrese de que tooexit de cada ventana de sesión como cada proceso se ejecuta de forma independiente aunque se ejecuten en Hola misma máquina.</span><span class="sxs-lookup"><span data-stu-id="d68bd-107">If exiting a session, be sure tooexit from each session window as each process runs independently although they run on hello same machine.</span></span>

## <a name="restart-cloud-shell"></a><span data-ttu-id="d68bd-108">Reinicio de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="d68bd-108">Restart Cloud Shell</span></span>
![](media/recycle.png)
> [!WARNING]
> <span data-ttu-id="d68bd-109">Al reiniciar Cloud Shell se restablecerá el estado de la máquina y todos los archivos que no conserve el recurso compartido de archivos se perderán.</span><span class="sxs-lookup"><span data-stu-id="d68bd-109">Restarting Cloud Shell will reset machine state and any files not persisted by your file share will be lost.</span></span>

* <span data-ttu-id="d68bd-110">Haga clic en el icono de reinicio de hello en la barra de herramientas de hello tooreceive un nuevo entorno de Shell en la nube.</span><span class="sxs-lookup"><span data-stu-id="d68bd-110">Click hello restart icon on hello toolbar tooreceive a new Cloud Shell environment.</span></span>

## <a name="minimize--maximize-cloud-shell-window"></a><span data-ttu-id="d68bd-111">Minimizar y maximizar la ventana Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="d68bd-111">Minimize & maximize Cloud Shell window</span></span>
![](media/minmax.png)
* <span data-ttu-id="d68bd-112">Haga clic en hello minimizar (icono) en hello parte superior derecha del saludo ventana toohide lo.</span><span class="sxs-lookup"><span data-stu-id="d68bd-112">Click hello minimize icon on hello top right of hello window toohide it.</span></span> <span data-ttu-id="d68bd-113">Haga clic en hello icono de Shell en la nube nuevo toounhide.</span><span class="sxs-lookup"><span data-stu-id="d68bd-113">Click hello Cloud Shell icon again toounhide.</span></span>
* <span data-ttu-id="d68bd-114">Haga clic en hello maximizar el alto del icono tooset ventana toomax.</span><span class="sxs-lookup"><span data-stu-id="d68bd-114">Click hello maximize icon tooset window toomax height.</span></span> <span data-ttu-id="d68bd-115">toorestore ventana tooprevious cambio de tamaño, haga clic en restaurar.</span><span class="sxs-lookup"><span data-stu-id="d68bd-115">toorestore window tooprevious size, click restore.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="d68bd-116">Copiar y pegar</span><span class="sxs-lookup"><span data-stu-id="d68bd-116">Copy and paste</span></span>
* <span data-ttu-id="d68bd-117">Windows: `Ctrl-insert` toocopy y `Shift-insert` toopaste.</span><span class="sxs-lookup"><span data-stu-id="d68bd-117">Windows: `Ctrl-insert` toocopy and `Shift-insert` toopaste.</span></span> <span data-ttu-id="d68bd-118">Hacer clic con el botón derecho en la lista desplegable también habilita copiar y pegar.</span><span class="sxs-lookup"><span data-stu-id="d68bd-118">Right-click dropdown can also enable copy/paste.</span></span>
  * <span data-ttu-id="d68bd-119">Es posible que Firefox o IE no admitan los permisos del Portapapeles correctamente.</span><span class="sxs-lookup"><span data-stu-id="d68bd-119">FireFox/IE may not support clipboard permissions properly.</span></span>
* <span data-ttu-id="d68bd-120">Mac OS: `Cmd-c` toocopy y `Cmd-v` toopaste.</span><span class="sxs-lookup"><span data-stu-id="d68bd-120">Mac OS: `Cmd-c` toocopy and `Cmd-v` toopaste.</span></span> <span data-ttu-id="d68bd-121">Hacer clic con el botón derecho en la lista desplegable también habilita copiar y pegar.</span><span class="sxs-lookup"><span data-stu-id="d68bd-121">Right-click dropdown can also enable copy/paste.</span></span>

## <a name="resize-cloud-shell-window"></a><span data-ttu-id="d68bd-122">Cambio del tamaño de la ventana Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="d68bd-122">Resize Cloud Shell window</span></span>
* <span data-ttu-id="d68bd-123">Haga clic y arrastre el borde superior de Hola de barra de herramientas de hello hacia arriba o hacia abajo de la ventana de Shell en la nube de hello tooresize.</span><span class="sxs-lookup"><span data-stu-id="d68bd-123">Click and drag hello top edge of hello toolbar up or down tooresize hello Cloud Shell window.</span></span>

## <a name="scrolling-text-display"></a><span data-ttu-id="d68bd-124">Desplazamiento de la presentación del texto</span><span class="sxs-lookup"><span data-stu-id="d68bd-124">Scrolling text display</span></span>
* <span data-ttu-id="d68bd-125">Desplácese con el mouse o teclado táctil toomove terminal texto especificado.</span><span class="sxs-lookup"><span data-stu-id="d68bd-125">Scroll with your mouse or touchpad toomove terminal text.</span></span>

## <a name="exit-command"></a><span data-ttu-id="d68bd-126">Comando Exit</span><span class="sxs-lookup"><span data-stu-id="d68bd-126">Exit command</span></span>
<span data-ttu-id="d68bd-127">Ejecuta `exit` finaliza la sesión activa de Hola.</span><span class="sxs-lookup"><span data-stu-id="d68bd-127">Running `exit` terminates hello active session.</span></span> <span data-ttu-id="d68bd-128">Este comportamiento se produce de forma predeterminada después de 20 minutos sin interacción.</span><span class="sxs-lookup"><span data-stu-id="d68bd-128">This behavior occurs by default after 20 minutes without interaction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d68bd-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d68bd-129">Next steps</span></span>
[<span data-ttu-id="d68bd-130">Inicio rápido de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="d68bd-130">Cloud Shell Quickstart</span></span>](quickstart.md)
