---
title: Ubicaciones con nombre en Azure Active Directory | Microsoft Docs
description: "Al configurar ubicaciones con nombre, puede evitar el hecho de tener direcciones IP pertenecientes a su organización que generan falsos positivos para el tipo de evento de riesgo Viaje imposible a ubicaciones inusuales."
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
ms.openlocfilehash: ff31ded1d9d60e47e0ae5f01119de78cd7f2df38
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="named-locations-in-azure-active-directory"></a><span data-ttu-id="2febc-103">Ubicaciones con nombre en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2febc-103">Named locations in Azure Active Directory</span></span>

<span data-ttu-id="2febc-104">Gracias a las ubicaciones con nombre de Azure Active Directory puede etiquetar intervalos de direcciones IP de confianza en sus organizaciones.</span><span class="sxs-lookup"><span data-stu-id="2febc-104">With the named locations feature of Azure Active Directory, you can label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="2febc-105">En su entorno, puede usar las ubicaciones con nombre en el contexto de la detección de [eventos de riesgo](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="2febc-105">In your environment, you can use named locations in the context of the detection of [risk events](active-directory-reporting-risk-events.md).</span></span> <span data-ttu-id="2febc-106">La característica ayuda a reducir el número de falsos positivos incluidos para el tipo de evento de riesgo de *Viaje imposible a ubicaciones inusuales*.</span><span class="sxs-lookup"><span data-stu-id="2febc-106">The feature helps reduce the number of reported false positives for the *Impossible travel to atypical locations* risk event type.</span></span> 

## <a name="configuration"></a><span data-ttu-id="2febc-107">Configuración</span><span class="sxs-lookup"><span data-stu-id="2febc-107">Configuration</span></span>

<span data-ttu-id="2febc-108">Para configurar una ubicación con nombre:</span><span class="sxs-lookup"><span data-stu-id="2febc-108">To configure a named location:</span></span>

1. <span data-ttu-id="2febc-109">Inicie sesión en [Azure Portal](https://portal.azure.com) como administrador global.</span><span class="sxs-lookup"><span data-stu-id="2febc-109">Sign in to the [Azure portal](https://portal.azure.com) as global administrator.</span></span>

2. <span data-ttu-id="2febc-110">En el panel izquierdo, haga clic en **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2febc-110">In the left pane, click **Azure Active Directory**.</span></span>

    ![El vínculo Azure Active Directory en el panel izquierdo](./media/active-directory-named-locations/01.png)

3. <span data-ttu-id="2febc-112">En la hoja **Azure Active Directory**, en la sección **Seguridad**, haga clic en **Acceso condicional**.</span><span class="sxs-lookup"><span data-stu-id="2febc-112">On the **Azure Active Directory** blade, in the **Security** section, click **Conditional access**.</span></span>

    ![El comando Acceso condicional](./media/active-directory-named-locations/05.png)


4. <span data-ttu-id="2febc-114">En la hoja **Acceso condicional**, en la sección **Administrar**, haga clic en **Ubicaciones con nombre**.</span><span class="sxs-lookup"><span data-stu-id="2febc-114">On the **Conditional Access** blade, in the **Manage** section, click **Named locations**.</span></span>

    ![El comando Ubicaciones con nombre](./media/active-directory-named-locations/06.png)


5. <span data-ttu-id="2febc-116">En la hoja **Ubicaciones con nombre**, haga clic en **Nueva ubicación**.</span><span class="sxs-lookup"><span data-stu-id="2febc-116">On the **Named locations** blade, click **New location**.</span></span>

    ![El comando Nueva ubicación](./media/active-directory-named-locations/07.png)


6. <span data-ttu-id="2febc-118">En la hoja **Nuevo**, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2febc-118">On the **New** blade, do the following:</span></span>

    ![La hoja Nuevo](./media/active-directory-named-locations/08.png)

    <span data-ttu-id="2febc-120">a.</span><span class="sxs-lookup"><span data-stu-id="2febc-120">a.</span></span> <span data-ttu-id="2febc-121">En el cuadro **Nombre**, escriba el nombre de la ubicación con nombre.</span><span class="sxs-lookup"><span data-stu-id="2febc-121">In the **Name** box, type a name for your named location.</span></span>

    <span data-ttu-id="2febc-122">b.</span><span class="sxs-lookup"><span data-stu-id="2febc-122">b.</span></span> <span data-ttu-id="2febc-123">En el cuadro **Intervalo IP**, escriba un intervalo IP.</span><span class="sxs-lookup"><span data-stu-id="2febc-123">In the **IP ranges** box, type an IP range.</span></span> <span data-ttu-id="2febc-124">El intervalo de IP debe estar en el formato *Enrutamiento de interdominios sin clases*  (CIDR).</span><span class="sxs-lookup"><span data-stu-id="2febc-124">The IP range needs to be in the *Classless Inter-Domain Routing* (CIDR) format.</span></span>  

    <span data-ttu-id="2febc-125">c.</span><span class="sxs-lookup"><span data-stu-id="2febc-125">c.</span></span> <span data-ttu-id="2febc-126">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2febc-126">Click **Create**.</span></span>



## <a name="what-you-should-know"></a><span data-ttu-id="2febc-127">Qué debería saber</span><span class="sxs-lookup"><span data-stu-id="2febc-127">What you should know</span></span>

<span data-ttu-id="2febc-128">**Actualizaciones masivas**: al crear o actualizar ubicaciones con nombre, en el caso de las actualizaciones masivas, puede cargar o descargar un archivo CSV con los intervalos de IP.</span><span class="sxs-lookup"><span data-stu-id="2febc-128">**Bulk updates**: When you create or update named locations, for bulk updates, you can upload or download a CSV file with the IP ranges.</span></span> <span data-ttu-id="2febc-129">Una carga permite agregar los intervalos IP del archivo a la lista en lugar de sobrescribir la lista.</span><span class="sxs-lookup"><span data-stu-id="2febc-129">An upload adds the IP ranges in the file to the list instead of overwriting the list.</span></span>

![Los vínculos de carga y descarga](./media/active-directory-named-locations/09.png)


<span data-ttu-id="2febc-131">**Limitaciones:** puede definir un máximo de 60 ubicaciones con nombre con un intervalo de IP asignado a cada una de ellas.</span><span class="sxs-lookup"><span data-stu-id="2febc-131">**Limitations**: You can define a maximum of 60 named locations, with one IP range assigned to each of them.</span></span> <span data-ttu-id="2febc-132">Si tiene una sola ubicación con nombre configurada, puede definir hasta 500 intervalos IP para ella.</span><span class="sxs-lookup"><span data-stu-id="2febc-132">If you have just one named location configured, you can define up to 500 IP ranges for it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2febc-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2febc-133">Next steps</span></span>

<span data-ttu-id="2febc-134">Para más información acerca de los eventos de riesgo, consulte [Eventos de riesgo de Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="2febc-134">To learn more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>

