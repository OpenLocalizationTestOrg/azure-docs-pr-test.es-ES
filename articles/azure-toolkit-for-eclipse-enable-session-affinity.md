---
title: "Habilitar la afinidad de la sesión con el kit de herramientas de Azure para Eclipse"
description: "Averigüe cómo habilitar la afinidad de sesión con el kit de herramientas de Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: ab8623d6f9751ed6d71d9a5b1c0d5e939c442862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enable-session-affinity"></a><span data-ttu-id="7cd6c-103">Habilitar la afinidad de la sesión</span><span class="sxs-lookup"><span data-stu-id="7cd6c-103">Enable Session Affinity</span></span>
<span data-ttu-id="7cd6c-104">En el Kit de herramientas de Azure para Eclipse, puede habilitar la afinidad de la sesión HTTP o "sesiones permanentes", para sus roles.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-104">Within the Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="7cd6c-105">En la siguiente imagen se muestra el cuadro de diálogo de propiedades **Equilibrio de carga** que se us para habilitar la característica de afinidad de sesión:</span><span class="sxs-lookup"><span data-stu-id="7cd6c-105">The following image shows the **Load Balancing** properties dialog used to enable the session affinity feature:</span></span>

![][ic719492]

## <a name="to-enable-session-affinity-for-your-role"></a><span data-ttu-id="7cd6c-106">Para habilitar la afinidad de sesión para su rol</span><span class="sxs-lookup"><span data-stu-id="7cd6c-106">To enable session affinity for your role</span></span>
1. <span data-ttu-id="7cd6c-107">Haga clic con el botón secundario en el rol en el Explorador de proyectos de Eclipse, haga clic en **Azure** y, luego, en **Load Balancing** (Equilibrio de carga).</span><span class="sxs-lookup"><span data-stu-id="7cd6c-107">Right-click the role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>

2. <span data-ttu-id="7cd6c-108">En el cuadro de diálogo **Propiedades del equilibrio de carga de WorkerRole1** :</span><span class="sxs-lookup"><span data-stu-id="7cd6c-108">In the **Properties for WorkerRole1 Load Balancing** dialog:</span></span>

   <span data-ttu-id="7cd6c-109">a.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-109">a.</span></span> <span data-ttu-id="7cd6c-110">Active **Habilitar afinidad de sesión HTTP (sesiones permanentes) para este rol**</span><span class="sxs-lookup"><span data-stu-id="7cd6c-110">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>

   <span data-ttu-id="7cd6c-111">b.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-111">b.</span></span> <span data-ttu-id="7cd6c-112">Para **Input endpoint to use** (Punto de conexión de entrada que se va a usar), seleccione un punto de conexión de entrada que se usará, por ejemplo, **http (public:80, private:8080)**.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-112">For **Input endpoint to use**, select an input endpoint to use, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="7cd6c-113">Su aplicación debe usar este punto de conexión como su punto de conexión HTTP.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-113">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="7cd6c-114">Puede habilitar varios puntos de conexión para su rol, pero solo puede seleccionar uno de ellos para admitir sesiones permanentes.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-114">You can enable multiple endpoints for your role, but you can select only one of them to support sticky sessions.</span></span>

   <span data-ttu-id="7cd6c-115">c.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-115">c.</span></span> <span data-ttu-id="7cd6c-116">Vuelva a compilar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-116">Rebuild your application.</span></span>

<span data-ttu-id="7cd6c-117">Una vez habilitada, si tiene más de una instancia de rol, las solicitudes HTTP procedentes de un cliente concreto seguirán controlándose por la misma instancia de rol.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-117">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by the same role instance.</span></span>

<span data-ttu-id="7cd6c-118">El Kit de herramientas de Eclipse permite esto al instalar un módulo IIS especial llamado enrutamiento de solicitudes de aplicaciones (ARR) en cada una de sus instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-118">The Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="7cd6c-119">ARR vuelve a enrutar las solicitudes HTTP para la instancia de rol adecuada.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-119">ARR reroutes HTTP requests to the appropriate role instance.</span></span> <span data-ttu-id="7cd6c-120">El kit de herramientas vuelve a configurar automáticamente el punto de conexión seleccionado de manera que el tráfico HTTP entrante se enruta primero al software de ARR.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-120">The toolkit automatically reconfigures the selected endpoint so that the incoming HTTP traffic is first routed to the ARR software.</span></span> <span data-ttu-id="7cd6c-121">El kit de herramientas también crea un nuevo punto de conexión interno al que está configurado el servidor Java para escuchar.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-121">The toolkit also creates a new internal endpoint that your Java server is configured to listen to.</span></span> <span data-ttu-id="7cd6c-122">Ese es el punto de conexión usado por ARR para volver a enrutar el tráfico HTTP a la instancia de rol adecuada.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-122">That is the endpoint used by ARR to reroute the HTTP traffic to the appropriate role instance.</span></span> <span data-ttu-id="7cd6c-123">De este modo, cada instancia de rol de su implementación de varias instancias actúa como proxy inverso para todas las demás instancias, lo que permite sesiones permanentes.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-123">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all the other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="7cd6c-124">Notas sobre la afinidad de sesión</span><span class="sxs-lookup"><span data-stu-id="7cd6c-124">Notes about session affinity</span></span>
* <span data-ttu-id="7cd6c-125">La afinidad de sesión no funciona en el emulador de proceso.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-125">Session affinity does not work in the compute emulator.</span></span> <span data-ttu-id="7cd6c-126">La configuración se puede aplicar en el emulador de proceso sin interferir con su proceso de compilación o ejecución del emulador de proceso, pero la propia característica no funciona en el emulador de proceso.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-126">The settings can be applied in the compute emulator without interfering with your build process or compute emulator execution, but the feature itself does not function within the compute emulator.</span></span>

* <span data-ttu-id="7cd6c-127">Al habilitar la afinidad de sesión aumentará la cantidad del espacio de disco usado por la implementación en Azure, puesto que se descargará software adicional y se instalará en sus instancias de rol cuando se inicie su servicio en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-127">Enabling session affinity will result in an increase in the amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in the Azure cloud.</span></span>

* <span data-ttu-id="7cd6c-128">El tiempo para inicializar cada rol será superior.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-128">The time to initialize each role will take longer.</span></span>

* <span data-ttu-id="7cd6c-129">Se agregará un punto de conexión interno para que funcione como enrutador de tráfico, como se ha mencionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7cd6c-129">An internal endpoint, to function as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="7cd6c-130">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="7cd6c-130">See Also</span></span>
<span data-ttu-id="7cd6c-131">[Kit de herramientas de Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="7cd6c-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="7cd6c-132">[Creación de una aplicación Hola a todos para Azure en Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="7cd6c-132">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="7cd6c-133">[Instalación del Kit de herramientas de Azure para Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="7cd6c-133">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="7cd6c-134">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="7cd6c-134">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How to Maintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
