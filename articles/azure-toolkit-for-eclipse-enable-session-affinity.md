---
title: "uso de afinidad de la sesión de aaaEnable Hola Kit de herramientas de Azure para Eclipse"
description: "Obtenga información acerca de cómo tooenable sesión afinidad con hello Azure Toolkit for Eclipse."
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
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a><span data-ttu-id="12e76-103">Habilitar la afinidad de la sesión</span><span class="sxs-lookup"><span data-stu-id="12e76-103">Enable Session Affinity</span></span>
<span data-ttu-id="12e76-104">Dentro de hello Azure Toolkit for Eclipse, puede habilitar afinidad de la sesión HTTP, o "sesiones permanentes", para sus roles.</span><span class="sxs-lookup"><span data-stu-id="12e76-104">Within hello Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="12e76-105">Hello siguiente imagen muestra hello **equilibrio de carga** la característica de afinidad de la sesión propiedades diálogo utiliza tooenable hello:</span><span class="sxs-lookup"><span data-stu-id="12e76-105">hello following image shows hello **Load Balancing** properties dialog used tooenable hello session affinity feature:</span></span>

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a><span data-ttu-id="12e76-106">afinidad de la sesión de tooenable para el rol</span><span class="sxs-lookup"><span data-stu-id="12e76-106">tooenable session affinity for your role</span></span>
1. <span data-ttu-id="12e76-107">Haga clic en función de hello en el Explorador de proyectos de Eclipse, haga clic en **Azure**y, a continuación, haga clic en **equilibrio de carga**.</span><span class="sxs-lookup"><span data-stu-id="12e76-107">Right-click hello role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>

2. <span data-ttu-id="12e76-108">Hola **propiedades de equilibrio de carga de WorkerRole1** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="12e76-108">In hello **Properties for WorkerRole1 Load Balancing** dialog:</span></span>

   <span data-ttu-id="12e76-109">a.</span><span class="sxs-lookup"><span data-stu-id="12e76-109">a.</span></span> <span data-ttu-id="12e76-110">Active **Habilitar afinidad de sesión HTTP (sesiones permanentes) para este rol**</span><span class="sxs-lookup"><span data-stu-id="12e76-110">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>

   <span data-ttu-id="12e76-111">b.</span><span class="sxs-lookup"><span data-stu-id="12e76-111">b.</span></span> <span data-ttu-id="12e76-112">Para **toouse de extremo de entrada**, seleccione un extremo de entrada toouse, por ejemplo, **http (público: 80, private: 8080)**.</span><span class="sxs-lookup"><span data-stu-id="12e76-112">For **Input endpoint toouse**, select an input endpoint toouse, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="12e76-113">Su aplicación debe usar este punto de conexión como su punto de conexión HTTP.</span><span class="sxs-lookup"><span data-stu-id="12e76-113">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="12e76-114">Puede habilitar varios puntos de conexión para el rol, pero puede seleccionar solo una de ellas toosupport sesiones permanentes.</span><span class="sxs-lookup"><span data-stu-id="12e76-114">You can enable multiple endpoints for your role, but you can select only one of them toosupport sticky sessions.</span></span>

   <span data-ttu-id="12e76-115">c.</span><span class="sxs-lookup"><span data-stu-id="12e76-115">c.</span></span> <span data-ttu-id="12e76-116">Vuelva a compilar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="12e76-116">Rebuild your application.</span></span>

<span data-ttu-id="12e76-117">Una vez habilitada, si tiene más de una instancia de rol, las solicitudes HTTP procedentes de un cliente en particular seguirán estando controladas por hello misma instancia de rol.</span><span class="sxs-lookup"><span data-stu-id="12e76-117">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by hello same role instance.</span></span>

<span data-ttu-id="12e76-118">Hola Kit de herramientas Eclipse hace esto posible mediante la instalación de un módulo IIS especial llamado enrutamiento de solicitud de aplicaciones (ARR) en cada una de las instancias del rol.</span><span class="sxs-lookup"><span data-stu-id="12e76-118">hello Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="12e76-119">ARR vuelve a enrutar instancia de rol correspondiente de toohello de las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="12e76-119">ARR reroutes HTTP requests toohello appropriate role instance.</span></span> <span data-ttu-id="12e76-120">Kit de herramientas de Hello vuelve a configurar automáticamente el punto de conexión de hello seleccionado para que el tráfico HTTP entrante hello es el primer software ARR de toohello enrutado.</span><span class="sxs-lookup"><span data-stu-id="12e76-120">hello toolkit automatically reconfigures hello selected endpoint so that hello incoming HTTP traffic is first routed toohello ARR software.</span></span> <span data-ttu-id="12e76-121">Kit de herramientas de Hello también crea un nuevo extremo interno que se toolisten configurado para el servidor de Java.</span><span class="sxs-lookup"><span data-stu-id="12e76-121">hello toolkit also creates a new internal endpoint that your Java server is configured toolisten to.</span></span> <span data-ttu-id="12e76-122">Que es el punto de conexión de hello utilizado por ARR tooreroute Hola HTTP tráfico toohello rol correspondiente instancia.</span><span class="sxs-lookup"><span data-stu-id="12e76-122">That is hello endpoint used by ARR tooreroute hello HTTP traffic toohello appropriate role instance.</span></span> <span data-ttu-id="12e76-123">De esta manera, cada instancia de rol en la implementación de varias instancias actúa como un proxy inverso para todos los Hola otras instancias, lo que permite sesiones permanentes.</span><span class="sxs-lookup"><span data-stu-id="12e76-123">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all hello other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="12e76-124">Notas sobre la afinidad de sesión</span><span class="sxs-lookup"><span data-stu-id="12e76-124">Notes about session affinity</span></span>
* <span data-ttu-id="12e76-125">Afinidad de la sesión no funciona en el emulador de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="12e76-125">Session affinity does not work in hello compute emulator.</span></span> <span data-ttu-id="12e76-126">configuración de Hola se puede aplicar en el emulador de proceso de hello sin interferir con el proceso de compilación o ejecución de emulador de proceso, pero propia característica hello no funciona en el emulador de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="12e76-126">hello settings can be applied in hello compute emulator without interfering with your build process or compute emulator execution, but hello feature itself does not function within hello compute emulator.</span></span>

* <span data-ttu-id="12e76-127">Al habilitar la afinidad de sesión dará como resultado un aumento en la cantidad de Hola de espacio en disco utilizado por la implementación en Azure, tal y como se descargarse e instalarse en las instancias del rol cuando se inicia el servicio en nube de Azure Hola software adicional.</span><span class="sxs-lookup"><span data-stu-id="12e76-127">Enabling session affinity will result in an increase in hello amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in hello Azure cloud.</span></span>

* <span data-ttu-id="12e76-128">Hola tiempo tooinitialize cada rol tardará más tiempo.</span><span class="sxs-lookup"><span data-stu-id="12e76-128">hello time tooinitialize each role will take longer.</span></span>

* <span data-ttu-id="12e76-129">Un extremo interno, toofunction como un nuevo tráfico como se mencionó anteriormente, se agregarán.</span><span class="sxs-lookup"><span data-stu-id="12e76-129">An internal endpoint, toofunction as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="12e76-130">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="12e76-130">See Also</span></span>
<span data-ttu-id="12e76-131">[Kit de herramientas de Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="12e76-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="12e76-132">[Creación de una aplicación Hola a todos para Azure en Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="12e76-132">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="12e76-133">[Instalar hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="12e76-133">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="12e76-134">Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="12e76-134">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
