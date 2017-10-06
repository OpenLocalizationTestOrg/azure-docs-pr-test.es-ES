---
title: ubicaciones de aaaNamed en Azure Active Directory | Documentos de Microsoft
description: "Mediante la configuración de ubicaciones con nombre, puede evitar tener IP direcciones que pertenecen a su organización generan falsos positivos para ubicaciones de hello viaje imposible tooatypical el riesgo de tipo de evento."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a><span data-ttu-id="61f36-103">Ubicaciones con nombre en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="61f36-103">Named locations in Azure Active Directory</span></span>

<span data-ttu-id="61f36-104">Con hello con el nombre de característica de ubicaciones de Azure Active Directory, puede etiquetar los intervalos de direcciones IP de confianza en su organización.</span><span class="sxs-lookup"><span data-stu-id="61f36-104">With hello named locations feature of Azure Active Directory, you can label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="61f36-105">En su entorno, puede usar ubicaciones con nombre en el contexto de hello de la detección de Hola de [el riesgo de eventos](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="61f36-105">In your environment, you can use named locations in hello context of hello detection of [risk events](active-directory-reporting-risk-events.md).</span></span> <span data-ttu-id="61f36-106">característica de Hello ayuda a reducir el número de Hola de notificado falsos positivos para hello *ubicaciones de viaje imposible tooatypical* el riesgo de tipo de evento.</span><span class="sxs-lookup"><span data-stu-id="61f36-106">hello feature helps reduce hello number of reported false positives for hello *Impossible travel tooatypical locations* risk event type.</span></span> 

## <a name="configuration"></a><span data-ttu-id="61f36-107">Configuración</span><span class="sxs-lookup"><span data-stu-id="61f36-107">Configuration</span></span>

<span data-ttu-id="61f36-108">tooconfigure una ubicación con nombre:</span><span class="sxs-lookup"><span data-stu-id="61f36-108">tooconfigure a named location:</span></span>

1. <span data-ttu-id="61f36-109">Inicie sesión en toohello [portal de Azure](https://portal.azure.com) como administrador global.</span><span class="sxs-lookup"><span data-stu-id="61f36-109">Sign in toohello [Azure portal](https://portal.azure.com) as global administrator.</span></span>

2. <span data-ttu-id="61f36-110">En el panel izquierdo de hello, haga clic en **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="61f36-110">In hello left pane, click **Azure Active Directory**.</span></span>

    ![vínculo de Azure Active Directory Hello en el panel izquierdo de Hola](./media/active-directory-named-locations/01.png)

3. <span data-ttu-id="61f36-112">En hello **Azure Active Directory** hoja en hello **seguridad** sección, haga clic en **acceso condicional**.</span><span class="sxs-lookup"><span data-stu-id="61f36-112">On hello **Azure Active Directory** blade, in hello **Security** section, click **Conditional access**.</span></span>

    ![Hola comando de acceso condicional](./media/active-directory-named-locations/05.png)


4. <span data-ttu-id="61f36-114">En hello **acceso condicional** hoja en hello **administrar** sección, haga clic en **ubicaciones con nombre**.</span><span class="sxs-lookup"><span data-stu-id="61f36-114">On hello **Conditional Access** blade, in hello **Manage** section, click **Named locations**.</span></span>

    ![Hola comando de ubicaciones con nombre](./media/active-directory-named-locations/06.png)


5. <span data-ttu-id="61f36-116">En hello **denominada ubicaciones** hoja, haga clic en **nueva ubicación**.</span><span class="sxs-lookup"><span data-stu-id="61f36-116">On hello **Named locations** blade, click **New location**.</span></span>

    ![Hola nuevo comando de ubicación](./media/active-directory-named-locations/07.png)


6. <span data-ttu-id="61f36-118">En hello **New** hoja, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="61f36-118">On hello **New** blade, do hello following:</span></span>

    ![Nueva hoja de Hola](./media/active-directory-named-locations/08.png)

    <span data-ttu-id="61f36-120">a.</span><span class="sxs-lookup"><span data-stu-id="61f36-120">a.</span></span> <span data-ttu-id="61f36-121">Hola **nombre** , escriba un nombre para la ubicación con nombre.</span><span class="sxs-lookup"><span data-stu-id="61f36-121">In hello **Name** box, type a name for your named location.</span></span>

    <span data-ttu-id="61f36-122">b.</span><span class="sxs-lookup"><span data-stu-id="61f36-122">b.</span></span> <span data-ttu-id="61f36-123">Hola **intervalos IP** , escriba un intervalo de IP.</span><span class="sxs-lookup"><span data-stu-id="61f36-123">In hello **IP ranges** box, type an IP range.</span></span> <span data-ttu-id="61f36-124">intervalo IP de Hello necesita toobe Hola *enrutamiento de interdominios sin clase* formato (CIDR).</span><span class="sxs-lookup"><span data-stu-id="61f36-124">hello IP range needs toobe in hello *Classless Inter-Domain Routing* (CIDR) format.</span></span>  

    <span data-ttu-id="61f36-125">c.</span><span class="sxs-lookup"><span data-stu-id="61f36-125">c.</span></span> <span data-ttu-id="61f36-126">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="61f36-126">Click **Create**.</span></span>



## <a name="what-you-should-know"></a><span data-ttu-id="61f36-127">Qué debería saber</span><span class="sxs-lookup"><span data-stu-id="61f36-127">What you should know</span></span>

<span data-ttu-id="61f36-128">**Actualización masiva**: al crear o actualizar las ubicaciones con nombre, para las actualizaciones masivas, puede cargar o descargar un archivo CSV con intervalos IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="61f36-128">**Bulk updates**: When you create or update named locations, for bulk updates, you can upload or download a CSV file with hello IP ranges.</span></span> <span data-ttu-id="61f36-129">Una carga agrega intervalos IP de hello en lista de hello archivos toohello en lugar de sobrescribir la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="61f36-129">An upload adds hello IP ranges in hello file toohello list instead of overwriting hello list.</span></span>

![Hola, cargar y descargar vínculos](./media/active-directory-named-locations/09.png)


<span data-ttu-id="61f36-131">**Limitaciones**: puede definir un máximo de 60 ubicaciones con nombre, con un tooeach de rango asignado de IP de ellos.</span><span class="sxs-lookup"><span data-stu-id="61f36-131">**Limitations**: You can define a maximum of 60 named locations, with one IP range assigned tooeach of them.</span></span> <span data-ttu-id="61f36-132">Si tiene una sola ubicación con nombre configurada, puede definir intervalos IP too500 para él.</span><span class="sxs-lookup"><span data-stu-id="61f36-132">If you have just one named location configured, you can define up too500 IP ranges for it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="61f36-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="61f36-133">Next steps</span></span>

<span data-ttu-id="61f36-134">toolearn más información acerca de los eventos de riesgo, vea [eventos de riesgo de Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="61f36-134">toolearn more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>

