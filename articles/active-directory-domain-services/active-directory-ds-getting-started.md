---
title: "Azure Active Directory Domain Services: introducción | Microsoft Docs"
description: "Habilitación de Azure Active Directory Domain Services mediante Azure Portal (versión preliminar)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 47507096a6245d4f1ba57a652ddf5167b3776ae9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="1bf96-103">Habilitación de Azure Active Directory Domain Services mediante Azure Portal (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="1bf96-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>
<span data-ttu-id="1bf96-104">En este artículo se muestra cómo habilitar Azure Active Directory Domain Services (Azure AD DS) mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1bf96-104">This article shows how to enable Azure Active Directory Domain Services (Azure AD DS) using the Azure portal.</span></span>


<span data-ttu-id="1bf96-105">Para iniciar el Asistente para **habilitar Azure AD Domain Services**, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1bf96-105">To launch the **Enable Azure AD Domain Services** wizard, complete the following steps:</span></span>

1. <span data-ttu-id="1bf96-106">Vaya a [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1bf96-106">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1bf96-107">En el panel izquierdo, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="1bf96-107">In the left pane, click on **New**.</span></span>
3. <span data-ttu-id="1bf96-108">En la hoja **Nuevo**, escriba **Domain Services** en la barra de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="1bf96-108">In the **New** blade, type **Domain Services** into the search bar.</span></span>

    ![Buscar servicios de dominio](./media/getting-started/search-domain-services.png)

4. <span data-ttu-id="1bf96-110">Haga clic para seleccionar **Azure AD Domain Services** en la lista de sugerencias de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="1bf96-110">Click to select **Azure AD Domain Services** from the list of search suggestions.</span></span> <span data-ttu-id="1bf96-111">En la hoja **Azure AD Domain Services**, haga clic en el botón **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1bf96-111">On the **Azure AD Domain Services** blade, click the **Create** button.</span></span>

    ![Hoja Servicios de dominio](./media/getting-started/domain-services-blade.png)

5. <span data-ttu-id="1bf96-113">Se inicia el Asistente para **habilitar Azure AD Domain Services**.</span><span class="sxs-lookup"><span data-stu-id="1bf96-113">The **Enable Azure AD Domain Services** wizard is launched.</span></span>


## <a name="task-1-configure-basic-settings"></a><span data-ttu-id="1bf96-114">Tarea 1: Configuración básica</span><span class="sxs-lookup"><span data-stu-id="1bf96-114">Task 1: configure basic settings</span></span>
<span data-ttu-id="1bf96-115">En la página **Conceptos básicos** del asistente, puede especificar el nombre de dominio DNS del dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="1bf96-115">In the **Basics** page of the wizard, you can specify the DNS domain name for the managed domain.</span></span> <span data-ttu-id="1bf96-116">También puede elegir el grupo de recursos y la ubicación de Azure en la que se debe implementar el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="1bf96-116">You can also choose the resource group and Azure location to which the managed domain should be deployed.</span></span>

![Configurar conceptos básicos](./media/getting-started/domain-services-blade-basics.png)

1. <span data-ttu-id="1bf96-118">Elija el **nombre de dominio DNS** del dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="1bf96-118">Choose the **DNS domain name** for your managed domain.</span></span>

   * <span data-ttu-id="1bf96-119">De forma predeterminada, se especifica el nombre de dominio predeterminado del directorio (con el sufijo **.onmicrosoft.com**).</span><span class="sxs-lookup"><span data-stu-id="1bf96-119">The default domain name of the directory (with a **.onmicrosoft.com** suffix) is specified by default.</span></span>

   * <span data-ttu-id="1bf96-120">También puede escribir un nombre de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="1bf96-120">You can also type in a custom domain name.</span></span> <span data-ttu-id="1bf96-121">En este ejemplo, el nombre de dominio personalizado es *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="1bf96-121">In this example, the custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="1bf96-122">El prefijo del nombre de dominio especificado (por ejemplo, *contoso100* en el nombre de dominio *contoso100.com*) debe contener 15 caracteres o menos.</span><span class="sxs-lookup"><span data-stu-id="1bf96-122">The prefix of your specified domain name (for example, *contoso100* in the *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="1bf96-123">No puede crear un dominio administrado con un prefijo de más de 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="1bf96-123">You cannot create a managed domain with a prefix longer than 15 characters.</span></span>
     >
     >

2. <span data-ttu-id="1bf96-124">Asegúrese de que el nombre de dominio DNS que ha elegido para el dominio administrado no existe ya en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="1bf96-124">Ensure that the DNS domain name you have chosen for the managed domain does not already exist in the virtual network.</span></span> <span data-ttu-id="1bf96-125">En concreto, compruebe si:</span><span class="sxs-lookup"><span data-stu-id="1bf96-125">Specifically, check whether:</span></span>

   * <span data-ttu-id="1bf96-126">Ya tiene un dominio con el mismo nombre de dominio DNS en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="1bf96-126">You already have a domain with the same DNS domain name on the virtual network.</span></span>

   * <span data-ttu-id="1bf96-127">La red virtual en la que planea habilitar el dominio administrado tiene una conexión VPN con la red local.</span><span class="sxs-lookup"><span data-stu-id="1bf96-127">The virtual network where you plan to enable the managed domain has a VPN connection with your on-premises network.</span></span> <span data-ttu-id="1bf96-128">En este escenario, asegúrese de que no tiene un dominio con el mismo nombre de dominio DNS de la red local.</span><span class="sxs-lookup"><span data-stu-id="1bf96-128">In this scenario, ensure you don't have a domain with the same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="1bf96-129">Si ya dispone de un servicio en la nube con ese nombre en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="1bf96-129">You have an existing cloud service with that name on the virtual network.</span></span>

3. <span data-ttu-id="1bf96-130">Elija el **tipo de red virtual**.</span><span class="sxs-lookup"><span data-stu-id="1bf96-130">Choose the **type of virtual network**.</span></span> <span data-ttu-id="1bf96-131">De forma predeterminada, el tipo de red virtual del **Administrador de recursos** está seleccionado.</span><span class="sxs-lookup"><span data-stu-id="1bf96-131">By default, the **Resource Manager** virtual network type is selected.</span></span> <span data-ttu-id="1bf96-132">Se recomienda usar este tipo de red virtual para los dominios administrados recién creados.</span><span class="sxs-lookup"><span data-stu-id="1bf96-132">We recommend using this type of virtual network for all newly created managed domains.</span></span>

4. <span data-ttu-id="1bf96-133">Seleccione la **suscripción** de Azure en la que desea crear el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="1bf96-133">Select the Azure **Subscription** in which you would like to create the managed domain.</span></span>

5. <span data-ttu-id="1bf96-134">Seleccione el **grupo de recursos** al que debería pertenecer el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="1bf96-134">Select the **Resource group** to which the managed domain should belong.</span></span> <span data-ttu-id="1bf96-135">Puede elegir las opciones **Crear nuevo** o **Utilizar existente** para seleccionar el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1bf96-135">You can choose either the **Create new** or **Use existing** options to select the resource group.</span></span>

6. <span data-ttu-id="1bf96-136">Elija la **ubicación** de Azure en que se debe crear el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="1bf96-136">Choose the Azure **Location** in which the managed domain should be created.</span></span> <span data-ttu-id="1bf96-137">En la página **Red** del asistente, verá solo las redes virtuales que pertenecen a la ubicación que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="1bf96-137">On the **Network** page of the wizard, you see only virtual networks that belong to the location you have selected.</span></span>

7. <span data-ttu-id="1bf96-138">Cuando haya terminado, haga clic en **Aceptar** para ir a la página **Red** del asistente.</span><span class="sxs-lookup"><span data-stu-id="1bf96-138">When you are done, click **OK** to move on to the **Network** page of the wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="1bf96-139">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="1bf96-139">Next step</span></span>
[<span data-ttu-id="1bf96-140">Tarea 2: Configuración de red</span><span class="sxs-lookup"><span data-stu-id="1bf96-140">Task 2: configure network settings</span></span>](active-directory-ds-getting-started-network.md)
