---
title: aaaGet Hola misma experiencia de Office 365 en cualquier dispositivo con Azure RemoteApp | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooshare cualquier aplicación de Office 365 con los usuarios mediante el uso de Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 140056c22c8c69b9ec605318e35a72b144da07eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-same-office-365-experience-on-any-device-with-azure-remoteapp"></a><span data-ttu-id="52589-103">Get Hola misma experiencia de Office 365 en cualquier dispositivo con Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="52589-103">Get hello same Office 365 experience on any device with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="52589-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="52589-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="52589-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="52589-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="52589-106">En este artículo se explicará cómo toodeploy Office 365 en cualquier dispositivo de su empresa.</span><span class="sxs-lookup"><span data-stu-id="52589-106">This article will cover how toodeploy Office 365 on any device in your company.</span></span> <span data-ttu-id="52589-107">Los usuarios pueden obtener hello las mismas capacidades y experiencia de interfaz de usuario en Windows, Apple y Android.</span><span class="sxs-lookup"><span data-stu-id="52589-107">Your users can get hello same capabilities and UI experience on Android, Apple and Windows.</span></span>

<span data-ttu-id="52589-108">Para conseguirlo, usaremos Azure RemoteApp hospedando Office 365 en máquinas virtuales escalables de Azure a las que pueden conectarse los usuarios.</span><span class="sxs-lookup"><span data-stu-id="52589-108">We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to.</span></span> <span data-ttu-id="52589-109">A este conjunto de máquinas virtuales lo denominamos "colección en la nube".</span><span class="sxs-lookup"><span data-stu-id="52589-109">This set of virtual machines we call a "cloud collection".</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="52589-110">Creación de una colección en la nube</span><span class="sxs-lookup"><span data-stu-id="52589-110">Create a cloud collection</span></span>
<span data-ttu-id="52589-111">En primer lugar una vez haya creado una cuenta de Azure, navegue demasiado**RemoteApp** haciendo clic en el vínculo de hello en el lado izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="52589-111">First after you have created an Azure account, navigate too**RemoteApp** by clicking on hello link on hello left side.</span></span>
<span data-ttu-id="52589-112">![Mostrar Azure RemoteApp en hello Portal de Azure](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span><span class="sxs-lookup"><span data-stu-id="52589-112">![Showing Azure RemoteApp on hello Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span></span>

<span data-ttu-id="52589-113">A continuación, continuar, haga clic en **nueva** en la parte inferior de Hola y "Creación rápida" una colección.</span><span class="sxs-lookup"><span data-stu-id="52589-113">Then continue by clicking **new** on hello bottom and "quick creating" a collection.</span></span> <span data-ttu-id="52589-114">Proporcione un nombre, región de hello, suscripción hello, plan de Hola e imagen Hola "Proffesional de Office 2013" que se proporciona.</span><span class="sxs-lookup"><span data-stu-id="52589-114">Provide a name, hello region, hello subscription, hello plan and hello image "Office Proffesional 2013" that we provide.</span></span>
<span data-ttu-id="52589-115">![Cuadro de diálogo Crear](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span><span class="sxs-lookup"><span data-stu-id="52589-115">![Create Dialog](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span></span>

<span data-ttu-id="52589-116">Después de finalizar la debe comenzar el proceso de creación de colección de hello formulario Hola.</span><span class="sxs-lookup"><span data-stu-id="52589-116">Once you finish hello form hello collection creation process should start.</span></span> <span data-ttu-id="52589-117">Esto puede tardar horas tooan más o menos.</span><span class="sxs-lookup"><span data-stu-id="52589-117">This may take up tooan hour or so.</span></span>

![En espera](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

<span data-ttu-id="52589-119">Una vez que se realiza el proceso de hello, lo tendrá un aspecto similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="52589-119">Once hello process is done, it will look something like this.</span></span> <span data-ttu-id="52589-120">Si hacemos clic en **Publicación** , podemos ver que ya publicamos la mayoría de las aplicaciones de Office.</span><span class="sxs-lookup"><span data-stu-id="52589-120">If we click **Publishing** we can see that most Office applications have been published for us already.</span></span>
<span data-ttu-id="52589-121">![Colección creada](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span><span class="sxs-lookup"><span data-stu-id="52589-121">![Collection created](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span></span>

![Aplicaciones publicadas](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

<span data-ttu-id="52589-123">En este momento también puede agregar más usuarios que tienen acceso toothis colección haciendo clic en **acceso de usuario**.</span><span class="sxs-lookup"><span data-stu-id="52589-123">At this point you can also add more users that have access toothis collection by clicking **User Access**.</span></span>
<span data-ttu-id="52589-124">![Configurar el acceso del usuario](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span><span class="sxs-lookup"><span data-stu-id="52589-124">![Configure user access](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span></span>

<span data-ttu-id="52589-125">Ahora vamos a probar conexión tooOffice 365!</span><span class="sxs-lookup"><span data-stu-id="52589-125">Now let's try out connecting tooOffice 365!</span></span>

## <a name="connect-toooffice-365"></a><span data-ttu-id="52589-126">Conectar tooOffice 365</span><span class="sxs-lookup"><span data-stu-id="52589-126">Connect tooOffice 365</span></span>
<span data-ttu-id="52589-127">Se le diríjase demasiado[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), desplácese hacia abajo y haga clic en **descargar clientes** tooinstall cliente de Azure RemoteApp hello en dispositivo Hola se encuentra en.</span><span class="sxs-lookup"><span data-stu-id="52589-127">We'll head over too[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** tooinstall hello Azure RemoteApp client on hello device you're on.</span></span> <span data-ttu-id="52589-128">Hola de capturas de pantalla siguientes son para Windows.</span><span class="sxs-lookup"><span data-stu-id="52589-128">hello screenshots below are for Windows.</span></span>

<span data-ttu-id="52589-129">Una vez que inicia la aplicación hello se le preguntará toosign con su cuenta de Microsoft (anteriormente denominado "Live ID"), use Hola mismo como su cuenta de Azure por ahora.</span><span class="sxs-lookup"><span data-stu-id="52589-129">Once hello application starts you'll be asked toosign in with your Microsoft account (formerly called a "Live ID"), use hello same one as your Azure account for now.</span></span> <span data-ttu-id="52589-130">Tras iniciar sesión, debe ver una notificación sobre nuevas invitaciones, haga clic en ella y verá una lista como la siguiente.</span><span class="sxs-lookup"><span data-stu-id="52589-130">When you're signed in you should see a notification about new invitations, click there and you should see a list like one below.</span></span> <span data-ttu-id="52589-131">Aceptar la invitación de Hola que coincida con el correo electrónico de propietario de cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="52589-131">Accept hello invitation that matches your Azure account owner email.</span></span>

![Nueva invitación](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

<span data-ttu-id="52589-133">Este es lo que aparece cuando hay invitaciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="52589-133">What it looks like when there are new invitations.</span></span>

![Aceptar una aplicación](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

<span data-ttu-id="52589-135">Una vez que acepta la invitación de hello debería ver todas las aplicaciones de Office de hello en el cliente de Azure RemoteApp Hola.</span><span class="sxs-lookup"><span data-stu-id="52589-135">Once you accept hello invitation you should see all hello Office apps in hello Azure RemoteApp client.</span></span>

![Lista de aplicaciones](./media/remoteapp-tutorial-o365anywhere/9-work.png)

<span data-ttu-id="52589-137">Al hacer clic en cualquiera de estas aplicaciones Hola debe iniciarse en hello máquina virtual de Azure y debe tener establecidos.</span><span class="sxs-lookup"><span data-stu-id="52589-137">When you click on any of these hello application should start on hello Azure virtual machine and you should be all set!</span></span> <span data-ttu-id="52589-138">¡Disfrute!</span><span class="sxs-lookup"><span data-stu-id="52589-138">Enjoy!</span></span>

![iniciando](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![powerpoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

