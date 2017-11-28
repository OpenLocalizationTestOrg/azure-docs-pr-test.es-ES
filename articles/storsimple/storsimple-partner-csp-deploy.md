---
title: "aaaMicrosoft StorSimple de Azure y la información general sobre el programa de proveedor de soluciones en la nube | Documentos de Microsoft"
description: "Información general sobre hello StorSimple y CSP para partners de StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/08/2017
ms.author: alkohli
ms.openlocfilehash: b5d999f2fbb9a27e7404ff454957b29dbef56af6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a><span data-ttu-id="8ef49-103">Implementación de StorSimple Virtual Array para el programa de proveedores de soluciones en la nube</span><span class="sxs-lookup"><span data-stu-id="8ef49-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span></span>

## <a name="overview"></a><span data-ttu-id="8ef49-104">Información general</span><span class="sxs-lookup"><span data-stu-id="8ef49-104">Overview</span></span>

<span data-ttu-id="8ef49-105">StorSimple Virtual Array se pueden implementar por asociados de proveedor de soluciones de nube (CSP) de Hola para sus clientes.</span><span class="sxs-lookup"><span data-stu-id="8ef49-105">StorSimple Virtual Array can be deployed by hello Cloud Solution Provider (CSP) partners for their customers.</span></span> <span data-ttu-id="8ef49-106">Un asociado de CSP puede crear un servicio StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="8ef49-106">A CSP partner can create a StorSimple Device Manager service.</span></span> <span data-ttu-id="8ef49-107">Este servicio, a continuación, puede ser usado toodeploy y administrar StorSimple Virtual Array y Hola asociadas recursos compartidos, los volúmenes y las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="8ef49-107">This service can then be used toodeploy and manage StorSimple Virtual Array and hello associated shares, volumes, and backups.</span></span>

<span data-ttu-id="8ef49-108">Este artículo describe cómo puede agregar un cliente o una nueva suscripción tooan existente y, a continuación, cree un servicio toodeploy una matriz Virtual de StorSimple en CSP un socio CSP.</span><span class="sxs-lookup"><span data-stu-id="8ef49-108">This article describes how a CSP partner can add a customer or a new subscription tooan existing customer and then create a service toodeploy a StorSimple Virtual Array in CSP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ef49-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8ef49-109">Prerequisites</span></span>

<span data-ttu-id="8ef49-110">Antes de comenzar, asegúrese de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8ef49-110">Before you begin, ensure that:</span></span>

- <span data-ttu-id="8ef49-111">Se inscriben en el programa de hello CSP.</span><span class="sxs-lookup"><span data-stu-id="8ef49-111">You are enrolled under hello CSP program.</span></span>
- <span data-ttu-id="8ef49-112">Tiene credenciales válidas de inicio de sesión en el [Centro de partners](http://partnercenter.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="8ef49-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span></span> <span data-ttu-id="8ef49-113">las credenciales de Hello permiten toosign en tooadd portal nuevos clientes de socio comercial de toohello, buscan los clientes o navegue tooa cuenta del cliente desde el panel de Partner de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ef49-113">hello credentials enable you toosign in toohello Partner portal tooadd new customers, search for customers, or navigate tooa customer account from hello Partner dashboard.</span></span> <span data-ttu-id="8ef49-114">Hola CSP puede funcionar como un administrador de StorSimple en nombre de cliente de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ef49-114">hello CSP can function as a StorSimple administrator on behalf of hello customer in hello Azure portal.</span></span>
                             
## <a name="add-a-customer"></a><span data-ttu-id="8ef49-115">Agregar un cliente</span><span class="sxs-lookup"><span data-stu-id="8ef49-115">Add a customer</span></span>

<span data-ttu-id="8ef49-116">Si agrega un cliente, se crea automáticamente una suscripción.</span><span class="sxs-lookup"><span data-stu-id="8ef49-116">If you add a customer, a subscription is automatically created.</span></span> <span data-ttu-id="8ef49-117">tooadd un cliente (y crear automáticamente una suscripción), realizar Hola siguiendo los pasos descritos en el portal de partners de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ef49-117">tooadd a customer (and automatically create a subscription), perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="8ef49-118">Vaya toohello [centro de partners de](http://partnercenter.microsoft.com/) e inicie sesión con sus credenciales CSP.</span><span class="sxs-lookup"><span data-stu-id="8ef49-118">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="8ef49-119">Haga clic en **Panel**.</span><span class="sxs-lookup"><span data-stu-id="8ef49-119">Click **Dashboard**.</span></span>

     ![Panel del Centro de partners](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="8ef49-121">En el panel izquierdo hello, haga clic en **clientes**.</span><span class="sxs-lookup"><span data-stu-id="8ef49-121">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="8ef49-122">En el panel derecho hello, haga clic en **agregar clientes**.</span><span class="sxs-lookup"><span data-stu-id="8ef49-122">In hello right-pane, click **Add customers**.</span></span> <span data-ttu-id="8ef49-123">Escriba los detalles de Hola de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ef49-123">Enter hello details of hello customer.</span></span> <span data-ttu-id="8ef49-124">Haga clic en **siguiente: suscripciones** toocreate una suscripción de cliente.</span><span class="sxs-lookup"><span data-stu-id="8ef49-124">Click **Next: Subscriptions** toocreate a customer subscription.</span></span>

    ![Agregar un cliente](./media/storsimple-partner-csp-deploy/image2.png)

3.  <span data-ttu-id="8ef49-126">Seleccione la oferta de **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="8ef49-126">Select **Microsoft Azure** offer.</span></span> <span data-ttu-id="8ef49-127">Desplazar hacia abajo de toohello de página de Hola y haga clic en **revisión**.</span><span class="sxs-lookup"><span data-stu-id="8ef49-127">Scroll toohello bottom of hello page and click **Review**.</span></span>

    ![Revisar la información de la suscripción](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. <span data-ttu-id="8ef49-129">Revise la información de Hola y haga clic en **enviar**.</span><span class="sxs-lookup"><span data-stu-id="8ef49-129">Review hello information and click **Submit**.</span></span>

    ![Enviar la suscripción](./media/storsimple-partner-csp-deploy/image4.png)

5. <span data-ttu-id="8ef49-131">Guardar información de confirmación de Hola para futuras referencias.</span><span class="sxs-lookup"><span data-stu-id="8ef49-131">Save hello confirmation information for future reference.</span></span>

    ![Guardar la confirmación](./media/storsimple-partner-csp-deploy/image5.png)

6. <span data-ttu-id="8ef49-133">Busque o navegue al cliente de toohello que acaba de agregar.</span><span class="sxs-lookup"><span data-stu-id="8ef49-133">Find or navigate toohello customer you just added.</span></span> <span data-ttu-id="8ef49-134">Haga clic en hello **nombre de la compañía** toodrill hacia abajo en los detalles de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ef49-134">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Busque al cliente hello](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="8ef49-136">En el panel izquierdo hello, seleccione **administración de servicios**.</span><span class="sxs-lookup"><span data-stu-id="8ef49-136">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="8ef49-137">En Hola panel derecho, en **administrar servicios**, haga clic en **Portal de administración de Microsoft Azure** toosign en como un administrador de Azure para su cliente.</span><span class="sxs-lookup"><span data-stu-id="8ef49-137">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![Inicie sesión en el portal de tooAzure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="8ef49-139">toocreate un dispositivo de StorSimple Manager, haga clic en **+ nuevo** y busque o navegue demasiado**serie de dispositivos virtuales StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="8ef49-139">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="8ef49-140">Para obtener más información, consulte demasiado[implementar un servicio de administrador de dispositivos de StorSimple](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="8ef49-140">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Crear el servicio StorSimple Device Manager](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a><span data-ttu-id="8ef49-142">Agregar una suscripción</span><span class="sxs-lookup"><span data-stu-id="8ef49-142">Add a subscription</span></span>

<span data-ttu-id="8ef49-143">En algunos casos, es posible que tenga un cliente existente y necesita tooadd una suscripción.</span><span class="sxs-lookup"><span data-stu-id="8ef49-143">In some instances, you may have an existing customer, and you need tooadd a subscription.</span></span> <span data-ttu-id="8ef49-144">tooadd un cliente existente tooan de suscripción, realizar Hola siguiendo los pasos descritos en el portal de partners de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ef49-144">tooadd a subscription tooan existing customer, perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="8ef49-145">Vaya toohello [centro de partners de](http://partnercenter.microsoft.com/) e inicie sesión con sus credenciales CSP.</span><span class="sxs-lookup"><span data-stu-id="8ef49-145">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="8ef49-146">Haga clic en **Panel**.</span><span class="sxs-lookup"><span data-stu-id="8ef49-146">Click **Dashboard**.</span></span>

     ![Panel del Centro de partners](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="8ef49-148">En el panel izquierdo hello, haga clic en **clientes**.</span><span class="sxs-lookup"><span data-stu-id="8ef49-148">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="8ef49-149">Busque o navegue a cliente toohello que desea tooadd una suscripción.</span><span class="sxs-lookup"><span data-stu-id="8ef49-149">Find or navigate toohello customer you want tooadd a subscription to.</span></span> <span data-ttu-id="8ef49-150">Haga clic en hello ![icono de verificación de expansión](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) fila de hello tooexpand de icono para el nombre de la compañía de Hola de cara al cliente.</span><span class="sxs-lookup"><span data-stu-id="8ef49-150">Click hello ![Expand check icon](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon tooexpand hello row for hello company name for your customer.</span></span> <span data-ttu-id="8ef49-151">En detalles de hello, haga clic en **agregar suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="8ef49-151">In hello details, click **Add subscriptions**.</span></span>

    ![Clientes](./media/storsimple-partner-csp-deploy/image10.png)

3. <span data-ttu-id="8ef49-153">Comprobar **Microsoft Azure** para hello **principales ofertas** suscripción hello y haga clic en **enviar**.</span><span class="sxs-lookup"><span data-stu-id="8ef49-153">Check **Microsoft Azure** for hello **Top offers** in hello subscription and click **Submit**.</span></span> <span data-ttu-id="8ef49-154">De esta forma se crea una suscripción nueva.</span><span class="sxs-lookup"><span data-stu-id="8ef49-154">This creates a new subscription.</span></span>

    ![Agregar nueva suscripción](./media/storsimple-partner-csp-deploy/image11.png)

6. <span data-ttu-id="8ef49-156">Después de crea una nueva suscripción, haga clic en **<--clientes** en hello panel izquierdo tooreturn toohello **clientes** página.</span><span class="sxs-lookup"><span data-stu-id="8ef49-156">After a new subscription is created, click **<-- Customers** in hello left-pane tooreturn toohello **Customers** page.</span></span> <span data-ttu-id="8ef49-157">Busque al cliente de hello para el que se acaba de crear una suscripción.</span><span class="sxs-lookup"><span data-stu-id="8ef49-157">Search for hello customer for whom you just created a subscription.</span></span> <span data-ttu-id="8ef49-158">Haga clic en hello **nombre de la compañía** toodrill hacia abajo en los detalles de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ef49-158">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Busque al cliente hello](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="8ef49-160">En el panel izquierdo hello, seleccione **administración de servicios**.</span><span class="sxs-lookup"><span data-stu-id="8ef49-160">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="8ef49-161">En Hola panel derecho, en **administrar servicios**, haga clic en **Portal de administración de Microsoft Azure** toosign en como un administrador de Azure para su cliente.</span><span class="sxs-lookup"><span data-stu-id="8ef49-161">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![Inicie sesión en el portal de tooAzure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="8ef49-163">toocreate un dispositivo de StorSimple Manager, haga clic en **+ nuevo** y busque o navegue demasiado**serie de dispositivos virtuales StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="8ef49-163">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="8ef49-164">Para obtener más información, consulte demasiado[implementar un servicio de administrador de dispositivos de StorSimple](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="8ef49-164">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Crear el servicio StorSimple Device Manager](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a><span data-ttu-id="8ef49-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8ef49-166">Next steps</span></span>

- <span data-ttu-id="8ef49-167">Si tiene más preguntas sobre hello StorSimple en CSP, vaya demasiado[StorSimple en el CSP: preguntas más frecuentes](storsimple-partner-csp-faq.md).</span><span class="sxs-lookup"><span data-stu-id="8ef49-167">If you have more questions regarding hello StorSimple in CSP, go too[StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span></span>
- <span data-ttu-id="8ef49-168">Si está listo toodeploy StorSimple, vaya demasiado[implementar StorSimple en CSP](storsimple-partner-csp-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="8ef49-168">If you are ready toodeploy your StorSimple, go too[Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span></span>
