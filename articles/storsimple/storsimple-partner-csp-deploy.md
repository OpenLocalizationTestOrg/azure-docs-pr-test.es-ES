---
title: "Introducción a Microsoft Azure StorSimple y el programa de proveedores de soluciones en la nube | Microsoft Docs"
description: "Introducción a StorSimple y CSP para asociados de StorSimple."
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
ms.openlocfilehash: c8cb51093142146fc7d43b51a62d949f6cc38988
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a><span data-ttu-id="8b063-103">Implementación de StorSimple Virtual Array para el programa de proveedores de soluciones en la nube</span><span class="sxs-lookup"><span data-stu-id="8b063-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span></span>

## <a name="overview"></a><span data-ttu-id="8b063-104">Información general</span><span class="sxs-lookup"><span data-stu-id="8b063-104">Overview</span></span>

<span data-ttu-id="8b063-105">Los asociados del programa de proveedores de soluciones en la nube (CSP) pueden implementar StorSimple Virtual Array para sus clientes.</span><span class="sxs-lookup"><span data-stu-id="8b063-105">StorSimple Virtual Array can be deployed by the Cloud Solution Provider (CSP) partners for their customers.</span></span> <span data-ttu-id="8b063-106">Un asociado de CSP puede crear un servicio StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="8b063-106">A CSP partner can create a StorSimple Device Manager service.</span></span> <span data-ttu-id="8b063-107">Este servicio luego se puede usar para implementar y administrar StorSimple Virtual Array y los recursos compartidos, volúmenes y copias de seguridad asociados.</span><span class="sxs-lookup"><span data-stu-id="8b063-107">This service can then be used to deploy and manage StorSimple Virtual Array and the associated shares, volumes, and backups.</span></span>

<span data-ttu-id="8b063-108">En este artículo se describe cómo un asociado de CSP puede agregar un cliente o una suscripción nueva a un cliente existente y, luego, crear un servicio para implementar una instancia de StorSimple Virtual Array en CSP.</span><span class="sxs-lookup"><span data-stu-id="8b063-108">This article describes how a CSP partner can add a customer or a new subscription to an existing customer and then create a service to deploy a StorSimple Virtual Array in CSP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b063-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8b063-109">Prerequisites</span></span>

<span data-ttu-id="8b063-110">Antes de comenzar, asegúrese de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8b063-110">Before you begin, ensure that:</span></span>

- <span data-ttu-id="8b063-111">Está inscrito en el programa CSP.</span><span class="sxs-lookup"><span data-stu-id="8b063-111">You are enrolled under the CSP program.</span></span>
- <span data-ttu-id="8b063-112">Tiene credenciales válidas de inicio de sesión en el [Centro de partners](http://partnercenter.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="8b063-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span></span> <span data-ttu-id="8b063-113">Las credenciales le permiten iniciar sesión en el portal para asociados para agregar clientes nuevos, buscar clientes o navegar a la cuenta de un cliente desde el Panel del asociado.</span><span class="sxs-lookup"><span data-stu-id="8b063-113">The credentials enable you to sign in to the Partner portal to add new customers, search for customers, or navigate to a customer account from the Partner dashboard.</span></span> <span data-ttu-id="8b063-114">CSP puede funcionar como administrador de StorSimple en nombre del cliente en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="8b063-114">The CSP can function as a StorSimple administrator on behalf of the customer in the Azure portal.</span></span>
                             
## <a name="add-a-customer"></a><span data-ttu-id="8b063-115">Agregar un cliente</span><span class="sxs-lookup"><span data-stu-id="8b063-115">Add a customer</span></span>

<span data-ttu-id="8b063-116">Si agrega un cliente, se crea automáticamente una suscripción.</span><span class="sxs-lookup"><span data-stu-id="8b063-116">If you add a customer, a subscription is automatically created.</span></span> <span data-ttu-id="8b063-117">Para agregar un cliente (y crear automáticamente una suscripción), lleve a cabo estos pasos en el portal para asociados.</span><span class="sxs-lookup"><span data-stu-id="8b063-117">To add a customer (and automatically create a subscription), perform the following steps in the Partner portal.</span></span>

1. <span data-ttu-id="8b063-118">Vaya al [Centro de partners](http://partnercenter.microsoft.com/) e inicie sesión con sus credenciales de CSP.</span><span class="sxs-lookup"><span data-stu-id="8b063-118">Go to the [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="8b063-119">Haga clic en **Panel**.</span><span class="sxs-lookup"><span data-stu-id="8b063-119">Click **Dashboard**.</span></span>

     ![Panel del Centro de partners](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="8b063-121">En el panel de la izquierda, haga clic en **Clientes**.</span><span class="sxs-lookup"><span data-stu-id="8b063-121">In the left-pane, click **Customers**.</span></span> <span data-ttu-id="8b063-122">En el panel de la derecha, haga clic en **Agregar clientes**.</span><span class="sxs-lookup"><span data-stu-id="8b063-122">In the right-pane, click **Add customers**.</span></span> <span data-ttu-id="8b063-123">Escriba los detalles del cliente.</span><span class="sxs-lookup"><span data-stu-id="8b063-123">Enter the details of the customer.</span></span> <span data-ttu-id="8b063-124">Haga clic en **Next: Subscriptions** (Siguiente: suscripciones) para crear una suscripción de cliente.</span><span class="sxs-lookup"><span data-stu-id="8b063-124">Click **Next: Subscriptions** to create a customer subscription.</span></span>

    ![Agregar un cliente](./media/storsimple-partner-csp-deploy/image2.png)

3.  <span data-ttu-id="8b063-126">Seleccione la oferta de **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="8b063-126">Select **Microsoft Azure** offer.</span></span> <span data-ttu-id="8b063-127">Desplácese a la parte inferior de la página y haga clic en **Revisar**.</span><span class="sxs-lookup"><span data-stu-id="8b063-127">Scroll to the bottom of the page and click **Review**.</span></span>

    ![Revisar la información de la suscripción](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. <span data-ttu-id="8b063-129">Revise la información y haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="8b063-129">Review the information and click **Submit**.</span></span>

    ![Enviar la suscripción](./media/storsimple-partner-csp-deploy/image4.png)

5. <span data-ttu-id="8b063-131">Guarde la información de confirmación para consultarla en el futuro.</span><span class="sxs-lookup"><span data-stu-id="8b063-131">Save the confirmation information for future reference.</span></span>

    ![Guardar la confirmación](./media/storsimple-partner-csp-deploy/image5.png)

6. <span data-ttu-id="8b063-133">Busque o vaya al cliente que acaba de agregar.</span><span class="sxs-lookup"><span data-stu-id="8b063-133">Find or navigate to the customer you just added.</span></span> <span data-ttu-id="8b063-134">Haga clic en el **nombre de la empresa** para explorar en profundidad los detalles.</span><span class="sxs-lookup"><span data-stu-id="8b063-134">Click the **Company name** to drill down into the details.</span></span>

    ![Buscar el cliente](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="8b063-136">En el panel de la izquierda, seleccione **Administración de servicios**.</span><span class="sxs-lookup"><span data-stu-id="8b063-136">In the left-pane, select **Service management**.</span></span> <span data-ttu-id="8b063-137">En el panel de la derecha, en **Administer services** (Administrar servicios), haga clic en **Portal de administración de Microsoft Azure** para iniciar sesión como el administrador de Azure del cliente.</span><span class="sxs-lookup"><span data-stu-id="8b063-137">In the right-pane, under **Administer services**, click **Microsoft Azure Management Portal** to sign in as an Azure administrator for your customer.</span></span>

    ![Iniciar sesión en Azure Portal](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="8b063-139">Para crear una instancia de StorSimple Device Manager, haga clic en **+ Nuevo** y busque **StorSimple Virtual Device Series** (Serie de dispositivos virtuales de StorSimple) o vaya a esa opción.</span><span class="sxs-lookup"><span data-stu-id="8b063-139">To create a StorSimple Device Manager, click **+ New** and search for or navigate to **StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="8b063-140">Para más información, vaya a [Implementación del servicio StorSimple Device Manager](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="8b063-140">For more information, go to [Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Crear el servicio StorSimple Device Manager](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a><span data-ttu-id="8b063-142">Agregar una suscripción</span><span class="sxs-lookup"><span data-stu-id="8b063-142">Add a subscription</span></span>

<span data-ttu-id="8b063-143">En algunos casos, es posible que tenga un cliente existente y que necesite agregar una suscripción.</span><span class="sxs-lookup"><span data-stu-id="8b063-143">In some instances, you may have an existing customer, and you need to add a subscription.</span></span> <span data-ttu-id="8b063-144">Para agregar una suscripción a un cliente existente, lleve a cabo estos pasos en el portal para asociados.</span><span class="sxs-lookup"><span data-stu-id="8b063-144">To add a subscription to an existing customer, perform the following steps in the Partner portal.</span></span>

1. <span data-ttu-id="8b063-145">Vaya al [Centro de partners](http://partnercenter.microsoft.com/) e inicie sesión con sus credenciales de CSP.</span><span class="sxs-lookup"><span data-stu-id="8b063-145">Go to the [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="8b063-146">Haga clic en **Panel**.</span><span class="sxs-lookup"><span data-stu-id="8b063-146">Click **Dashboard**.</span></span>

     ![Panel del Centro de partners](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="8b063-148">En el panel de la izquierda, haga clic en **Clientes**.</span><span class="sxs-lookup"><span data-stu-id="8b063-148">In the left-pane, click **Customers**.</span></span> <span data-ttu-id="8b063-149">Busque o vaya al cliente al que desea agregar una suscripción.</span><span class="sxs-lookup"><span data-stu-id="8b063-149">Find or navigate to the customer you want to add a subscription to.</span></span> <span data-ttu-id="8b063-150">Haga clic en el icono ![Expand check icon](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) (Expandir icono de marca de verificación) para expandir la fila del nombre de la empresa del cliente.</span><span class="sxs-lookup"><span data-stu-id="8b063-150">Click the ![Expand check icon](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon to expand the row for the company name for your customer.</span></span> <span data-ttu-id="8b063-151">En los detalles, haga clic en **Agregar suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="8b063-151">In the details, click **Add subscriptions**.</span></span>

    ![Clientes](./media/storsimple-partner-csp-deploy/image10.png)

3. <span data-ttu-id="8b063-153">Active **Microsoft Azure** en las **ofertas preferidas** de la suscripción y haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="8b063-153">Check **Microsoft Azure** for the **Top offers** in the subscription and click **Submit**.</span></span> <span data-ttu-id="8b063-154">De esta forma se crea una suscripción nueva.</span><span class="sxs-lookup"><span data-stu-id="8b063-154">This creates a new subscription.</span></span>

    ![Agregar nueva suscripción](./media/storsimple-partner-csp-deploy/image11.png)

6. <span data-ttu-id="8b063-156">Una vez que se crea una suscripción nueva, haga clic en **<-- Clientes** en el panel de la izquierda para volver a la página **Clientes**.</span><span class="sxs-lookup"><span data-stu-id="8b063-156">After a new subscription is created, click **<-- Customers** in the left-pane to return to the **Customers** page.</span></span> <span data-ttu-id="8b063-157">Busque el cliente para el que acaba de crear una suscripción.</span><span class="sxs-lookup"><span data-stu-id="8b063-157">Search for the customer for whom you just created a subscription.</span></span> <span data-ttu-id="8b063-158">Haga clic en el **nombre de la empresa** para explorar en profundidad los detalles.</span><span class="sxs-lookup"><span data-stu-id="8b063-158">Click the **Company name** to drill down into the details.</span></span>

    ![Buscar el cliente](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="8b063-160">En el panel de la izquierda, seleccione **Administración de servicios**.</span><span class="sxs-lookup"><span data-stu-id="8b063-160">In the left-pane, select **Service management**.</span></span> <span data-ttu-id="8b063-161">En el panel de la derecha, en **Administer services** (Administrar servicios), haga clic en **Portal de administración de Microsoft Azure** para iniciar sesión como el administrador de Azure del cliente.</span><span class="sxs-lookup"><span data-stu-id="8b063-161">In the right-pane, under **Administer services**, click **Microsoft Azure Management Portal** to sign in as an Azure administrator for your customer.</span></span>

    ![Iniciar sesión en Azure Portal](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="8b063-163">Para crear una instancia de StorSimple Device Manager, haga clic en **+ Nuevo** y busque **StorSimple Virtual Device Series** (Serie de dispositivos virtuales de StorSimple) o vaya a esa opción.</span><span class="sxs-lookup"><span data-stu-id="8b063-163">To create a StorSimple Device Manager, click **+ New** and search for or navigate to **StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="8b063-164">Para más información, vaya a [Implementación del servicio StorSimple Device Manager](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="8b063-164">For more information, go to [Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Crear el servicio StorSimple Device Manager](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a><span data-ttu-id="8b063-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8b063-166">Next steps</span></span>

- <span data-ttu-id="8b063-167">Si tiene más preguntas sobre StorSimple en CSP, vaya a [StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md) (StorSimple en CSP: preguntas más frecuentes).</span><span class="sxs-lookup"><span data-stu-id="8b063-167">If you have more questions regarding the StorSimple in CSP, go to [StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span></span>
- <span data-ttu-id="8b063-168">Si está listo para implementar StorSimple, vaya a [Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md) (Implementación de StorSimple en CSP).</span><span class="sxs-lookup"><span data-stu-id="8b063-168">If you are ready to deploy your StorSimple, go to [Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span></span>
