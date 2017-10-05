---
title: "Obtención de la misma experiencia de Office 365 en cualquier dispositivo con Azure RemoteApp | Microsoft Docs"
description: "Aprenda a compartir cualquier aplicación de Office 365 con sus usuarios mediante Azure RemoteApp."
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
ms.openlocfilehash: 584c781c97097cda3c1455ade05cba8659f11073
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-same-office-365-experience-on-any-device-with-azure-remoteapp"></a><span data-ttu-id="fdaca-103">Obtención de la misma experiencia de Office 365 en cualquier dispositivo con Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="fdaca-103">Get the same Office 365 experience on any device with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fdaca-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="fdaca-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="fdaca-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="fdaca-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="fdaca-106">Este artículo tratará cómo implementar Office 365 en cualquier dispositivo de su empresa.</span><span class="sxs-lookup"><span data-stu-id="fdaca-106">This article will cover how to deploy Office 365 on any device in your company.</span></span> <span data-ttu-id="fdaca-107">Los usuarios pueden obtener las mismas capacidades y experiencia de interfaz de usuario en Android, Apple y Windows.</span><span class="sxs-lookup"><span data-stu-id="fdaca-107">Your users can get the same capabilities and UI experience on Android, Apple and Windows.</span></span>

<span data-ttu-id="fdaca-108">Para conseguirlo, usaremos Azure RemoteApp hospedando Office 365 en máquinas virtuales escalables de Azure a las que pueden conectarse los usuarios.</span><span class="sxs-lookup"><span data-stu-id="fdaca-108">We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to.</span></span> <span data-ttu-id="fdaca-109">A este conjunto de máquinas virtuales lo denominamos "colección en la nube".</span><span class="sxs-lookup"><span data-stu-id="fdaca-109">This set of virtual machines we call a "cloud collection".</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="fdaca-110">Crear una colección en la nube</span><span class="sxs-lookup"><span data-stu-id="fdaca-110">Create a cloud collection</span></span>
<span data-ttu-id="fdaca-111">En primer lugar, tras crear una cuenta de Azure, navegue hasta **RemoteApp** haciendo clic en el vínculo situado a la izquierda.</span><span class="sxs-lookup"><span data-stu-id="fdaca-111">First after you have created an Azure account, navigate to **RemoteApp** by clicking on the link on the left side.</span></span>
<span data-ttu-id="fdaca-112">![Visualización de RemoteApp de Azure en el Portal de Azure](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span><span class="sxs-lookup"><span data-stu-id="fdaca-112">![Showing Azure RemoteApp on the Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span></span>

<span data-ttu-id="fdaca-113">Continúe haciendo clic en **Nuevo** en la parte inferior y en "Creación rápida" para crear así una colección.</span><span class="sxs-lookup"><span data-stu-id="fdaca-113">Then continue by clicking **new** on the bottom and "quick creating" a collection.</span></span> <span data-ttu-id="fdaca-114">Facilite un nombre, la región, la suscripción, el plan y la imagen "Office Professional 2013" que proporcionamos.</span><span class="sxs-lookup"><span data-stu-id="fdaca-114">Provide a name, the region, the subscription, the plan and the image "Office Proffesional 2013" that we provide.</span></span>
<span data-ttu-id="fdaca-115">![Cuadro de diálogo Crear](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span><span class="sxs-lookup"><span data-stu-id="fdaca-115">![Create Dialog](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span></span>

<span data-ttu-id="fdaca-116">Una vez que finalice el formulario, debería comenzar el proceso de creación de la colección.</span><span class="sxs-lookup"><span data-stu-id="fdaca-116">Once you finish the form the collection creation process should start.</span></span> <span data-ttu-id="fdaca-117">Esto puede tardar hasta una hora aproximadamente.</span><span class="sxs-lookup"><span data-stu-id="fdaca-117">This may take up to an hour or so.</span></span>

![En espera](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

<span data-ttu-id="fdaca-119">Cuando el proceso haya finalizado, tendrá un aspecto similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="fdaca-119">Once the process is done, it will look something like this.</span></span> <span data-ttu-id="fdaca-120">Si hacemos clic en **Publicación** , podemos ver que ya publicamos la mayoría de las aplicaciones de Office.</span><span class="sxs-lookup"><span data-stu-id="fdaca-120">If we click **Publishing** we can see that most Office applications have been published for us already.</span></span>
<span data-ttu-id="fdaca-121">![Colección creada](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span><span class="sxs-lookup"><span data-stu-id="fdaca-121">![Collection created](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span></span>

![Aplicaciones publicadas](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

<span data-ttu-id="fdaca-123">En este momento puede agregar también otros usuarios que tengan acceso a esta colección haciendo clic en **Acceso de usuario**.</span><span class="sxs-lookup"><span data-stu-id="fdaca-123">At this point you can also add more users that have access to this collection by clicking **User Access**.</span></span>
<span data-ttu-id="fdaca-124">![Configurar el acceso del usuario](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span><span class="sxs-lookup"><span data-stu-id="fdaca-124">![Configure user access](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span></span>

<span data-ttu-id="fdaca-125">Ahora vamos a intentar la conexión a Office 365.</span><span class="sxs-lookup"><span data-stu-id="fdaca-125">Now let's try out connecting to Office 365!</span></span>

## <a name="connect-to-office-365"></a><span data-ttu-id="fdaca-126">Conectarse a Office 365</span><span class="sxs-lookup"><span data-stu-id="fdaca-126">Connect to Office 365</span></span>
<span data-ttu-id="fdaca-127">Iremos a [https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), nos desplazaremos hacia abajo y haremos clic en **Descargar clientes** para instalar el cliente de Azure RemoteApp en el dispositivo en que se encuentre.</span><span class="sxs-lookup"><span data-stu-id="fdaca-127">We'll head over to [https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** to install the Azure RemoteApp client on the device you're on.</span></span> <span data-ttu-id="fdaca-128">Las capturas de pantalla siguientes corresponden a Windows.</span><span class="sxs-lookup"><span data-stu-id="fdaca-128">The screenshots below are for Windows.</span></span>

<span data-ttu-id="fdaca-129">Cuando se inicie la aplicación, se le pedirá que inicie sesión con su cuenta Microsoft (antes llamada "Live ID"); por ahora, use la misma cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="fdaca-129">Once the application starts you'll be asked to sign in with your Microsoft account (formerly called a "Live ID"), use the same one as your Azure account for now.</span></span> <span data-ttu-id="fdaca-130">Tras iniciar sesión, debe ver una notificación sobre nuevas invitaciones, haga clic en ella y verá una lista como la siguiente.</span><span class="sxs-lookup"><span data-stu-id="fdaca-130">When you're signed in you should see a notification about new invitations, click there and you should see a list like one below.</span></span> <span data-ttu-id="fdaca-131">Acepte la invitación dirigida al correo electrónico del propietario de su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="fdaca-131">Accept the invitation that matches your Azure account owner email.</span></span>

![Nueva invitación](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

<span data-ttu-id="fdaca-133">Este es lo que aparece cuando hay invitaciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="fdaca-133">What it looks like when there are new invitations.</span></span>

![Aceptar una aplicación](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

<span data-ttu-id="fdaca-135">Después de aceptar la invitación, debe ver todas las aplicaciones de Office en el cliente de Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fdaca-135">Once you accept the invitation you should see all the Office apps in the Azure RemoteApp client.</span></span>

![Lista de aplicaciones](./media/remoteapp-tutorial-o365anywhere/9-work.png)

<span data-ttu-id="fdaca-137">Al hacer clic en cualquiera de las aplicaciones, esta debe iniciarse en la máquina virtual de Azure y, con ello, todo estará configurado.</span><span class="sxs-lookup"><span data-stu-id="fdaca-137">When you click on any of these the application should start on the Azure virtual machine and you should be all set!</span></span> <span data-ttu-id="fdaca-138">¡Disfrute!</span><span class="sxs-lookup"><span data-stu-id="fdaca-138">Enjoy!</span></span>

![iniciando](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![powerpoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

