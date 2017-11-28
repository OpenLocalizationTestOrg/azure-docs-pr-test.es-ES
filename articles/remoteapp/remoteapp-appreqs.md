---
title: Requisitos de las aplicaciones para RemoteApp de Azure | Microsoft Docs
description: Conozca los requisitos de las aplicaciones que desea usar en Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 4427eef6-288a-49e1-97eb-fee67d99f26a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 13d42df97ea2b090180f5865a4eac25945f9f34c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="app-requirements"></a><span data-ttu-id="87dcf-103">Requisitos de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="87dcf-103">App requirements</span></span>
> [!IMPORTANT]
> <span data-ttu-id="87dcf-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="87dcf-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="87dcf-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="87dcf-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="87dcf-106">Azure RemoteApp admite el streaming de aplicaciones Windows de 32 o 64 bits desde una imagen de Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="87dcf-106">Azure RemoteApp supports streaming 32-bit or 64-bit Windows-based applications from a Windows Server 2012 R2 image.</span></span> <span data-ttu-id="87dcf-107">La mayoría de las aplicaciones Windows de 32 o 64 bits se ejecutan "tal cual" en el entorno de Azure RemoteApp (Servicios de Escritorio remoto antes conocido como Terminal Services).</span><span class="sxs-lookup"><span data-stu-id="87dcf-107">Most existing 32-bit or 64-bit Windows-based applications run "as is" in Azure RemoteApp (Remote Desktop Services or formerly known as Terminal Services) environment.</span></span> <span data-ttu-id="87dcf-108">Sin embargo, hay una diferencia entre ejecutar y ejecutar bien; algunas aplicaciones funcionan correctamente y su rendimiento es adecuado, mientras que otras no.</span><span class="sxs-lookup"><span data-stu-id="87dcf-108">However, there is a difference between running and running well - some applications function correctly and perform well, while others do not.</span></span> <span data-ttu-id="87dcf-109">La siguiente información proporciona instrucciones para el desarrollo de aplicaciones en un entorno de Servicios de Escritorio remoto y su prueba para garantizar la compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="87dcf-109">The following information provides guidance for developing applications in a Remote Desktop Services environment and testing to ensure compatibility.</span></span>

<span data-ttu-id="87dcf-110">Sugerencia: estamos trabajando en la creación de algunos ejemplos prácticos de aplicaciones para usted.</span><span class="sxs-lookup"><span data-stu-id="87dcf-110">Tip: We're working on creating some working examples of apps for you.</span></span> <span data-ttu-id="87dcf-111">Verá algunos temas nuevos en los que se analiza el uso de Microsoft Access, QuickBooks y App-V en RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="87dcf-111">You'll see new topics that discuss using Microsoft Access, QuickBooks, and App-V in RemoteApp.</span></span>

## <a name="requirements"></a><span data-ttu-id="87dcf-112">Requisitos</span><span class="sxs-lookup"><span data-stu-id="87dcf-112">Requirements</span></span>
<span data-ttu-id="87dcf-113">Estos tres requisitos, si se siguen, ayudarán a sus aplicaciones a ejecutarse bien en RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="87dcf-113">These three requirements, if followed, help your application run well in RemoteApp:</span></span>

1. <span data-ttu-id="87dcf-114">Las aplicaciones que cumplan todos los [Requisitos de certificación para aplicaciones de escritorio de Windows](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) y que se ajusten a las [Instrucciones de programación de Servicios de Escritorio remoto](https://msdn.microsoft.com/library/aa383490.aspx) tendrán completa compatibilidad con RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="87dcf-114">Applications that meet all [Certification requirements for Windows desktop apps](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) and adhere to [Remote Desktop Services programming guidelines](https://msdn.microsoft.com/library/aa383490.aspx) will have complete compatibility with RemoteApp.</span></span>
2. <span data-ttu-id="87dcf-115">Las aplicaciones nunca deben almacenar los datos localmente en la imagen o en instancias de RemoteApp que se puedan perder.</span><span class="sxs-lookup"><span data-stu-id="87dcf-115">Applications should never store data locally on the image or RemoteApp instances that can be lost.</span></span>  <span data-ttu-id="87dcf-116">Después de crear una colección de RemoteApp, las instancias se clonan y están sin estado y solo deben contener aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="87dcf-116">After you create a RemoteApp collection, the instances are cloned and are stateless and should only contain applications.</span></span> <span data-ttu-id="87dcf-117">Almacene los datos en un origen externo o en el perfil del usuario.</span><span class="sxs-lookup"><span data-stu-id="87dcf-117">Store data in an external source or within the user's profile.</span></span>
3. <span data-ttu-id="87dcf-118">Las imágenes personalizadas nunca deben contener datos que se puedan perder.</span><span class="sxs-lookup"><span data-stu-id="87dcf-118">Custom images should never contain data that can be lost.</span></span>  

## <a name="testing-your-apps"></a><span data-ttu-id="87dcf-119">Prueba de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="87dcf-119">Testing your apps</span></span>
<span data-ttu-id="87dcf-120">Use estos pasos para probar las aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="87dcf-120">Use these steps to testing applications:</span></span>

1. <span data-ttu-id="87dcf-121">Instale Windows Server 2012 R2 y su aplicación</span><span class="sxs-lookup"><span data-stu-id="87dcf-121">Install Windows Server 2012 R2 and your application</span></span>
2. <span data-ttu-id="87dcf-122">Habilite Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="87dcf-122">Enable Remote Desktop</span></span>
3. <span data-ttu-id="87dcf-123">Cree dos cuentas de usuario, UsuarioA y UsuarioB, y agregue ambas cuentas de usuario al grupo de seguridad de Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="87dcf-123">Create two user accounts, UserA and UserB, adding both user accounts to the Remote Desktop security group.</span></span>
4. <span data-ttu-id="87dcf-124">Compruebe la compatibilidad multisesión mediante el establecimiento de dos sesiones de RDS simultáneas en el equipo mientras se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="87dcf-124">Check multi-session compatibility by establishing two simultaneous RDS sessions to the PC while launching the application.</span></span>
5. <span data-ttu-id="87dcf-125">Valide el comportamiento de la aplicación</span><span class="sxs-lookup"><span data-stu-id="87dcf-125">Validate app behavior</span></span>

## <a name="application-development-guidelines"></a><span data-ttu-id="87dcf-126">Instrucciones para el desarrollo de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="87dcf-126">Application development guidelines</span></span>
<span data-ttu-id="87dcf-127">Use las siguientes instrucciones para desarrollar aplicaciones para RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="87dcf-127">Use the following guidelines for developing applications for RemoteApp.</span></span>

### <a name="multiple-users"></a><span data-ttu-id="87dcf-128">Varios usuarios</span><span class="sxs-lookup"><span data-stu-id="87dcf-128">Multiple users</span></span>
* <span data-ttu-id="87dcf-129">La instalación de una [aplicación para un único usuario ](https://msdn.microsoft.com/library/aa380661.aspx)puede crear problemas en un entorno de varios usuarios.</span><span class="sxs-lookup"><span data-stu-id="87dcf-129">Installing an [application for a single user ](https://msdn.microsoft.com/library/aa380661.aspx)can create problems in a multiuser environment.</span></span>
* <span data-ttu-id="87dcf-130">Las aplicaciones deben [almacenar información específica del usuario](https://msdn.microsoft.com/library/aa383452.aspx) en ubicaciones específicas del usuario, aparte de la información global que se aplica a todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="87dcf-130">Applications should [store user-specific information](https://msdn.microsoft.com/library/aa383452.aspx) in user-specific locations, separately from global information that applies to all users.</span></span>
* <span data-ttu-id="87dcf-131">RemoteApp usa varios [espacios de nombres para objetos de kernel](https://msdn.microsoft.com/library/aa382954.aspx); un espacio de nombres global lo usan principalmente los servicios en aplicaciones cliente/servidor.</span><span class="sxs-lookup"><span data-stu-id="87dcf-131">RemoteApp uses multiple [namespaces for kernel objects](https://msdn.microsoft.com/library/aa382954.aspx); a global namespace is used primarily by services in client/server applications.</span></span>
* <span data-ttu-id="87dcf-132">No es seguro suponer que el nombre del equipo o la [dirección IP](https://msdn.microsoft.com/library/aa382942.aspx) que se asignen al equipo se asocian a un único usuario, dado que varios usuarios pueden iniciar sesión a la vez en un servidor host de sesión de Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="87dcf-132">It is not safe to assume that the computer name or the [IP address](https://msdn.microsoft.com/library/aa382942.aspx) assigned to the computer are associated with a single user because multiple users can be logged on simultaneously to a Remote Desktop Session Host (RD Session Host) server.</span></span>

### <a name="performance"></a><span data-ttu-id="87dcf-133">Rendimiento</span><span class="sxs-lookup"><span data-stu-id="87dcf-133">Performance</span></span>
* <span data-ttu-id="87dcf-134">Deshabilite los [efectos gráficos](https://msdn.microsoft.com/library/aa380822.aspx) antes de agregar la aplicación a RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="87dcf-134">Disable [graphic effects](https://msdn.microsoft.com/library/aa380822.aspx) before you add your app to RemoteApp.</span></span>
* <span data-ttu-id="87dcf-135">Para maximizar la disponibilidad de la CPU para todos los usuarios, deshabilite las [tareas en segundo plano ](https://msdn.microsoft.com/library/aa380665.aspx) o cree tareas en segundo plano eficientes que no consuman muchos recursos.</span><span class="sxs-lookup"><span data-stu-id="87dcf-135">To maximize CPU availability for all users, either disable [background tasks ](https://msdn.microsoft.com/library/aa380665.aspx) or create efficient background tasks that are not resource-intensive.</span></span>
* <span data-ttu-id="87dcf-136">Debe ajustar y equilibrar el [uso de subprocesos](https://msdn.microsoft.com/library/aa383520.aspx) de la aplicación en un entorno de varios usuarios y procesadores.</span><span class="sxs-lookup"><span data-stu-id="87dcf-136">You should tune and balance application [thread usage](https://msdn.microsoft.com/library/aa383520.aspx) for a multiuser, multiprocessor environment.</span></span>
* <span data-ttu-id="87dcf-137">Para optimizar el rendimiento, resulta conveniente [detectar](https://msdn.microsoft.com/library/aa380798.aspx) si las aplicaciones se ejecutan en una sesión de cliente.</span><span class="sxs-lookup"><span data-stu-id="87dcf-137">To optimize performance, it is good practice for applications to [detect](https://msdn.microsoft.com/library/aa380798.aspx) whether they are running in a client session.</span></span>

