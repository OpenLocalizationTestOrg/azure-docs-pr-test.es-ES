---
title: aaaGet a trabajar con acceso condicional en Active Directory de Azure | Documentos de Microsoft
description: "Probar el acceso condicional con una condición de ubicación."
services: active-directory
keywords: tooapps de acceso condicional, el acceso condicional con Azure AD, proteger el acceso toocompany recursos, las directivas de acceso condicional
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="bb598-104">Introducción al acceso condicional en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb598-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="bb598-105">Acceso condicional es una capacidad de Azure Active Directory que permite toodefine las condiciones en las que los usuarios autorizados pueden tener acceso a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bb598-105">Conditional access is a capability of Azure Active Directory that enables you toodefine conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="bb598-106">En este tema se proporcionan instrucciones para probar un acceso condicional basado en una condición de ubicación en su entorno.</span><span class="sxs-lookup"><span data-stu-id="bb598-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="bb598-107">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="bb598-107">Scenario description</span></span>

<span data-ttu-id="bb598-108">Un requisito común en muchas organizaciones es tooonly requerir la autenticación multifactor para tooapps de acceso que no se realiza desde la intranet corporativa de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb598-108">One common requirement in many organizations is tooonly require multi-factor authentication for access tooapps that is not performed from hello corporate intranet.</span></span> <span data-ttu-id="bb598-109">Con Azure Active Directory, puede conseguir este objetivo fácilmente mediante la configuración de una directiva de acceso condicional basado en la ubicación.</span><span class="sxs-lookup"><span data-stu-id="bb598-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="bb598-110">En este tema se proporcionan instrucciones detalladas para configurar esta directiva.</span><span class="sxs-lookup"><span data-stu-id="bb598-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="bb598-111">Hola aprovecha la directiva [IP de confianza](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish entre los intentos de acceso de hello corporativa de la intranet y todas las demás ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="bb598-111">hello policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish between access attempts made from hello corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="bb598-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bb598-112">Prerequisites</span></span>

<span data-ttu-id="bb598-113">Hello escenario descrito en este tema se da por supuesto que está familiarizado con conceptos de Hola que se describen en [acceso condicional de Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bb598-113">hello scenario outlined in this topic assumes that you are familiar with hello concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="bb598-114">tootest este escenario, necesita:</span><span class="sxs-lookup"><span data-stu-id="bb598-114">tootest this scenario, you need to:</span></span>

- <span data-ttu-id="bb598-115">Crear un usuario de prueba</span><span class="sxs-lookup"><span data-stu-id="bb598-115">Create a test user</span></span> 

- <span data-ttu-id="bb598-116">Asignar a un usuario de prueba de toohello de licencia de Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="bb598-116">Assign an Azure AD Premium license toohello test user</span></span>

- <span data-ttu-id="bb598-117">Configurar una aplicación administrada y asignar su tooit de usuario de prueba</span><span class="sxs-lookup"><span data-stu-id="bb598-117">Configure a managed app and assign your test user tooit</span></span>

- <span data-ttu-id="bb598-118">Configurar direcciones IP de confianza</span><span class="sxs-lookup"><span data-stu-id="bb598-118">Configure trusted IPs</span></span>

<span data-ttu-id="bb598-119">Si necesita obtener más información acerca de las direcciones IP de confianza, consulte [Direcciones IP de confianza](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="bb598-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="bb598-120">Pasos de la configuración de la directiva</span><span class="sxs-lookup"><span data-stu-id="bb598-120">Policy configuration steps</span></span>

<span data-ttu-id="bb598-121">**tooconfigure la directiva de acceso condicional, hacer:**</span><span class="sxs-lookup"><span data-stu-id="bb598-121">**tooconfigure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="bb598-122">Hola portal de Azure, en la barra de navegación izquierdo de hello, haga clic en **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bb598-122">In hello Azure portal, on hello left navbar, click **Azure Active Directory**.</span></span> 

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="bb598-124">En hello **Azure Active Directory** hoja en hello **administrar** sección, haga clic en **acceso condicional**.</span><span class="sxs-lookup"><span data-stu-id="bb598-124">On hello **Azure Active Directory** blade, in hello **Manage** section, click **Conditional access**.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="bb598-126">En hello **acceso condicional** hoja, hello tooopen **New** hoja, en la barra de herramientas de hello en la parte superior de hello, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="bb598-126">On hello **Conditional Access** blade, tooopen hello **New** blade, in hello toolbar on hello top, click **Add**.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="bb598-128">En hello **New** hoja en hello **nombre** cuadro de texto, escriba un nombre para la directiva.</span><span class="sxs-lookup"><span data-stu-id="bb598-128">On hello **New** blade, in hello **Name** textbox, type a name for your policy.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="bb598-130">Hola **asignación** sección, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bb598-130">In hello **Assignment** section, click **Users and groups**.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="bb598-132">En hello **usuarios y grupos** hoja, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="bb598-132">On hello **Users and groups** blade, perform hello following steps:</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="bb598-134">a.</span><span class="sxs-lookup"><span data-stu-id="bb598-134">a.</span></span> <span data-ttu-id="bb598-135">Haga clic en **Seleccionar usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bb598-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="bb598-136">b.</span><span class="sxs-lookup"><span data-stu-id="bb598-136">b.</span></span> <span data-ttu-id="bb598-137">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="bb598-137">Click **Select**.</span></span>

    <span data-ttu-id="bb598-138">c.</span><span class="sxs-lookup"><span data-stu-id="bb598-138">c.</span></span> <span data-ttu-id="bb598-139">En hello **seleccione** hoja, seleccione el usuario de prueba y, a continuación, haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="bb598-139">On hello **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="bb598-140">d.</span><span class="sxs-lookup"><span data-stu-id="bb598-140">d.</span></span> <span data-ttu-id="bb598-141">En hello **usuarios y grupos** hoja, haga clic en **realiza**.</span><span class="sxs-lookup"><span data-stu-id="bb598-141">On hello **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="bb598-142">En hello **New** hoja, hello tooopen **las aplicaciones de nube** hoja en hello **asignación** sección, haga clic en **las aplicaciones de nube**.</span><span class="sxs-lookup"><span data-stu-id="bb598-142">On hello **New** blade, tooopen hello **Cloud apps** blade, in hello **Assignment** section, click **Cloud apps**.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="bb598-144">En hello **las aplicaciones de nube** hoja, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="bb598-144">On hello **Cloud apps** blade, perform hello following steps:</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="bb598-146">a.</span><span class="sxs-lookup"><span data-stu-id="bb598-146">a.</span></span> <span data-ttu-id="bb598-147">Haga clic en **Seleccionar aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bb598-147">Click **Select apps**.</span></span>

    <span data-ttu-id="bb598-148">b.</span><span class="sxs-lookup"><span data-stu-id="bb598-148">b.</span></span> <span data-ttu-id="bb598-149">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="bb598-149">Click **Select**.</span></span>

    <span data-ttu-id="bb598-150">c.</span><span class="sxs-lookup"><span data-stu-id="bb598-150">c.</span></span> <span data-ttu-id="bb598-151">En hello **seleccione** hoja, seleccione la aplicación en la nube y, a continuación, haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="bb598-151">On hello **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="bb598-152">d.</span><span class="sxs-lookup"><span data-stu-id="bb598-152">d.</span></span> <span data-ttu-id="bb598-153">En hello **las aplicaciones de nube** hoja, haga clic en **realiza**.</span><span class="sxs-lookup"><span data-stu-id="bb598-153">On hello **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="bb598-154">En hello **New** hoja, hello tooopen **condiciones** hoja en hello **asignación** sección, haga clic en **condiciones**.</span><span class="sxs-lookup"><span data-stu-id="bb598-154">On hello **New** blade, tooopen hello **Conditions** blade, in hello **Assignment** section, click **Conditions**.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="bb598-156">En hello **condiciones** hoja, hello tooopen **ubicaciones** hoja, haga clic en **ubicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bb598-156">On hello **Conditions** blade, tooopen hello **Locations** blade, click **Locations**.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="bb598-158">En hello **ubicaciones** hoja, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="bb598-158">On hello **Locations** blade, perform hello following steps:</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="bb598-160">a.</span><span class="sxs-lookup"><span data-stu-id="bb598-160">a.</span></span> <span data-ttu-id="bb598-161">En **Configurar**, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="bb598-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="bb598-162">b.</span><span class="sxs-lookup"><span data-stu-id="bb598-162">b.</span></span> <span data-ttu-id="bb598-163">En **Incluir**, haga clic en **Todas las ubicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bb598-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="bb598-164">c.</span><span class="sxs-lookup"><span data-stu-id="bb598-164">c.</span></span> <span data-ttu-id="bb598-165">Haga clic en **Excluir** y, después, haga clic en **Todas las direcciones IP de confianza**.</span><span class="sxs-lookup"><span data-stu-id="bb598-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="bb598-167">d.</span><span class="sxs-lookup"><span data-stu-id="bb598-167">d.</span></span> <span data-ttu-id="bb598-168">Haga clic en **Done**(Listo).</span><span class="sxs-lookup"><span data-stu-id="bb598-168">Click **Done**.</span></span>

12. <span data-ttu-id="bb598-169">En hello **condiciones** hoja, haga clic en **realiza**.</span><span class="sxs-lookup"><span data-stu-id="bb598-169">On hello **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="bb598-170">En hello **New** hoja, hello tooopen **Grant** hoja en hello **controles** sección, haga clic en **Grant**.</span><span class="sxs-lookup"><span data-stu-id="bb598-170">On hello **New** blade, tooopen hello **Grant** blade, in hello **Controls** section, click **Grant**.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="bb598-172">En hello **Grant** hoja, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="bb598-172">On hello **Grant** blade, perform hello following steps:</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="bb598-174">a.</span><span class="sxs-lookup"><span data-stu-id="bb598-174">a.</span></span> <span data-ttu-id="bb598-175">Seleccione **Requerir autenticación multifactor**.</span><span class="sxs-lookup"><span data-stu-id="bb598-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="bb598-176">b.</span><span class="sxs-lookup"><span data-stu-id="bb598-176">b.</span></span> <span data-ttu-id="bb598-177">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="bb598-177">Click **Select**.</span></span>

15. <span data-ttu-id="bb598-178">En hello **New** hoja, en **habilitar Directiva de**, haga clic en **en**.</span><span class="sxs-lookup"><span data-stu-id="bb598-178">On hello **New** blade, under **Enable policy**, click **On**.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="bb598-180">En hello **New** hoja, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="bb598-180">On hello **New** blade, click **Create**.</span></span>


## <a name="testing-hello-policy"></a><span data-ttu-id="bb598-181">Probar directiva Hola</span><span class="sxs-lookup"><span data-stu-id="bb598-181">Testing hello policy</span></span>

<span data-ttu-id="bb598-182">tootest la directiva, debe tener acceso a la aplicación desde un dispositivo que:</span><span class="sxs-lookup"><span data-stu-id="bb598-182">tootest your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="bb598-183">Tener una dirección IP que esté dentro de las direcciones IP de confianza configuradas.</span><span class="sxs-lookup"><span data-stu-id="bb598-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="bb598-184">Tener una dirección IP que no esté dentro de las direcciones IP de confianza configuradas.</span><span class="sxs-lookup"><span data-stu-id="bb598-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="bb598-185">La autenticación multifactor solo se requerirá durante un intento de conexión realizado desde un dispositivo que no está dentro de las direcciones IP de confianza configuradas.</span><span class="sxs-lookup"><span data-stu-id="bb598-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="bb598-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bb598-186">Next steps</span></span>

<span data-ttu-id="bb598-187">Si desea que toolearn más sobre el acceso condicional, consulte [acceso condicional de Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bb598-187">If you would like toolearn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

