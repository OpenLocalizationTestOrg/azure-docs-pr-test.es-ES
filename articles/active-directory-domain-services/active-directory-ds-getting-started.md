---
title: "Azure Active Directory Domain Services: introducción | Microsoft Docs"
description: Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure (vista previa)
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
ms.openlocfilehash: 79cbb21c4a50194f5ad8ca1a4a8493ee4a260a9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="8de92-103">Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure (vista previa)</span><span class="sxs-lookup"><span data-stu-id="8de92-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>
<span data-ttu-id="8de92-104">Este artículo muestra cómo tooenable Azure Active Directory Domain Services (Azure AD DS) con Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8de92-104">This article shows how tooenable Azure Active Directory Domain Services (Azure AD DS) using hello Azure portal.</span></span>


<span data-ttu-id="8de92-105">Hola toolaunch **servicios de dominio de AD de Azure permiten** Hola asistente, completar pasos:</span><span class="sxs-lookup"><span data-stu-id="8de92-105">toolaunch hello **Enable Azure AD Domain Services** wizard, complete hello following steps:</span></span>

1. <span data-ttu-id="8de92-106">Vaya toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8de92-106">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8de92-107">En el panel izquierdo de hello, haga clic en **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="8de92-107">In hello left pane, click on **New**.</span></span>
3. <span data-ttu-id="8de92-108">Hola **New** hoja, escriba **los servicios de dominio** en la barra de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="8de92-108">In hello **New** blade, type **Domain Services** into hello search bar.</span></span>

    ![Buscar servicios de dominio](./media/getting-started/search-domain-services.png)

4. <span data-ttu-id="8de92-110">Haga clic en tooselect **servicios de dominio de AD de Azure** de lista de Hola de sugerencias de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="8de92-110">Click tooselect **Azure AD Domain Services** from hello list of search suggestions.</span></span> <span data-ttu-id="8de92-111">En hello **servicios de dominio de AD de Azure** hoja, haga clic en hello **crear** botón.</span><span class="sxs-lookup"><span data-stu-id="8de92-111">On hello **Azure AD Domain Services** blade, click hello **Create** button.</span></span>

    ![Hoja Servicios de dominio](./media/getting-started/domain-services-blade.png)

5. <span data-ttu-id="8de92-113">Hola **servicios de dominio de AD de Azure permiten** se inicia el asistente.</span><span class="sxs-lookup"><span data-stu-id="8de92-113">hello **Enable Azure AD Domain Services** wizard is launched.</span></span>


## <a name="task-1-configure-basic-settings"></a><span data-ttu-id="8de92-114">Tarea 1: Configuración básica</span><span class="sxs-lookup"><span data-stu-id="8de92-114">Task 1: configure basic settings</span></span>
<span data-ttu-id="8de92-115">Hola **Fundamentos** página del Asistente para hello, puede especificar el nombre de dominio DNS de hello para el dominio administrado Hola.</span><span class="sxs-lookup"><span data-stu-id="8de92-115">In hello **Basics** page of hello wizard, you can specify hello DNS domain name for hello managed domain.</span></span> <span data-ttu-id="8de92-116">También puede elegir el grupo de recursos de Hola y dominio administrado de ubicación de Azure toowhich Hola debe implementarse.</span><span class="sxs-lookup"><span data-stu-id="8de92-116">You can also choose hello resource group and Azure location toowhich hello managed domain should be deployed.</span></span>

![Configurar conceptos básicos](./media/getting-started/domain-services-blade-basics.png)

1. <span data-ttu-id="8de92-118">Elija hello **nombre de dominio DNS** para el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="8de92-118">Choose hello **DNS domain name** for your managed domain.</span></span>

   * <span data-ttu-id="8de92-119">nombre de dominio predeterminado de Hello del directorio de hello (con un **. onmicrosoft.com** sufijo) se especifica de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="8de92-119">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is specified by default.</span></span>

   * <span data-ttu-id="8de92-120">También puede escribir un nombre de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="8de92-120">You can also type in a custom domain name.</span></span> <span data-ttu-id="8de92-121">En este ejemplo, es el nombre de dominio personalizado de hello *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="8de92-121">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="8de92-122">prefijo de Hola de su nombre de dominio especificado (por ejemplo, *contoso100* en hello *contoso100.com* nombre de dominio) debe contener 15 caracteres o menos.</span><span class="sxs-lookup"><span data-stu-id="8de92-122">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="8de92-123">No puede crear un dominio administrado con un prefijo de más de 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="8de92-123">You cannot create a managed domain with a prefix longer than 15 characters.</span></span>
     >
     >

2. <span data-ttu-id="8de92-124">Asegúrese de que ha elegido para hello administrado dominio todavía no existe en la red virtual de hello ese nombre de dominio DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="8de92-124">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="8de92-125">En concreto, compruebe si:</span><span class="sxs-lookup"><span data-stu-id="8de92-125">Specifically, check whether:</span></span>

   * <span data-ttu-id="8de92-126">Ya tiene un dominio con hello mismo nombre de dominio DNS de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="8de92-126">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="8de92-127">red virtual de Hola donde piensa tooenable Hola administrado dominio tiene una conexión VPN con la red local.</span><span class="sxs-lookup"><span data-stu-id="8de92-127">hello virtual network where you plan tooenable hello managed domain has a VPN connection with your on-premises network.</span></span> <span data-ttu-id="8de92-128">En este escenario, asegúrese de que no tiene un dominio con hello mismo nombre de dominio DNS de la red local.</span><span class="sxs-lookup"><span data-stu-id="8de92-128">In this scenario, ensure you don't have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="8de92-129">Tiene un servicio en la nube con ese nombre de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="8de92-129">You have an existing cloud service with that name on hello virtual network.</span></span>

3. <span data-ttu-id="8de92-130">Elija hello **tipo de red virtual**.</span><span class="sxs-lookup"><span data-stu-id="8de92-130">Choose hello **type of virtual network**.</span></span> <span data-ttu-id="8de92-131">De forma predeterminada, Hola **el Administrador de recursos** está seleccionado el tipo de red virtual.</span><span class="sxs-lookup"><span data-stu-id="8de92-131">By default, hello **Resource Manager** virtual network type is selected.</span></span> <span data-ttu-id="8de92-132">Se recomienda usar este tipo de red virtual para los dominios administrados recién creados.</span><span class="sxs-lookup"><span data-stu-id="8de92-132">We recommend using this type of virtual network for all newly created managed domains.</span></span>

4. <span data-ttu-id="8de92-133">Seleccione hello Azure **suscripción** en el que le gustaría toocreate Hola administrado dominio.</span><span class="sxs-lookup"><span data-stu-id="8de92-133">Select hello Azure **Subscription** in which you would like toocreate hello managed domain.</span></span>

5. <span data-ttu-id="8de92-134">Seleccione hello **grupo de recursos** toowhich Hola administrado dominio debe pertenecer.</span><span class="sxs-lookup"><span data-stu-id="8de92-134">Select hello **Resource group** toowhich hello managed domain should belong.</span></span> <span data-ttu-id="8de92-135">Puede elegir cualquier hello **crear nuevo** o **utilizar existente** grupo de recursos de opciones tooselect Hola.</span><span class="sxs-lookup"><span data-stu-id="8de92-135">You can choose either hello **Create new** or **Use existing** options tooselect hello resource group.</span></span>

6. <span data-ttu-id="8de92-136">Elija hello Azure **ubicación** en qué Hola se debe crear un dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="8de92-136">Choose hello Azure **Location** in which hello managed domain should be created.</span></span> <span data-ttu-id="8de92-137">En hello **red** página del Asistente para hello, verá que las redes virtuales solo pertenecen ubicación toohello ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="8de92-137">On hello **Network** page of hello wizard, you see only virtual networks that belong toohello location you have selected.</span></span>

7. <span data-ttu-id="8de92-138">Cuando haya terminado, haga clic en **Aceptar** toomove en toohello **red** página del Asistente para saludo.</span><span class="sxs-lookup"><span data-stu-id="8de92-138">When you are done, click **OK** toomove on toohello **Network** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="8de92-139">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="8de92-139">Next step</span></span>
[<span data-ttu-id="8de92-140">Tarea 2: Configuración de red</span><span class="sxs-lookup"><span data-stu-id="8de92-140">Task 2: configure network settings</span></span>](active-directory-ds-getting-started-network.md)
