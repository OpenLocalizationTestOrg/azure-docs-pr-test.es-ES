---
title: "Introducción al acceso condicional en Azure Active Directory | Microsoft Docs"
description: "Probar el acceso condicional con una condición de ubicación."
services: active-directory
keywords: acceso condicional a aplicaciones, acceso condicional con Azure AD, acceso seguro a recursos de empresa, directivas de acceso condicional
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
ms.openlocfilehash: cd53e8be32d1e98aaf9f72177895871dba69df86
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="2a667-104">Introducción al acceso condicional en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2a667-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="2a667-105">El acceso condicional es una funcionalidad de Azure Active Directory que permite definir las condiciones en las que los usuarios autorizados pueden acceder a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2a667-105">Conditional access is a capability of Azure Active Directory that enables you to define conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="2a667-106">En este tema se proporcionan instrucciones para probar un acceso condicional basado en una condición de ubicación en su entorno.</span><span class="sxs-lookup"><span data-stu-id="2a667-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="2a667-107">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="2a667-107">Scenario description</span></span>

<span data-ttu-id="2a667-108">En muchas organizaciones, un requisito habitual es requerir solo autenticación multifactor para el acceso a las aplicaciones que no se realiza desde la intranet corporativa.</span><span class="sxs-lookup"><span data-stu-id="2a667-108">One common requirement in many organizations is to only require multi-factor authentication for access to apps that is not performed from the corporate intranet.</span></span> <span data-ttu-id="2a667-109">Con Azure Active Directory, puede conseguir este objetivo fácilmente mediante la configuración de una directiva de acceso condicional basado en la ubicación.</span><span class="sxs-lookup"><span data-stu-id="2a667-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="2a667-110">En este tema se proporcionan instrucciones detalladas para configurar esta directiva.</span><span class="sxs-lookup"><span data-stu-id="2a667-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="2a667-111">La directiva aprovecha las [direcciones IP de confianza](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) para distinguir entre los intentos de acceso que se realizan desde la intranet corporativa y todas las demás ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="2a667-111">The policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) to distinguish between access attempts made from the corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="2a667-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2a667-112">Prerequisites</span></span>

<span data-ttu-id="2a667-113">En el escenario descrito en este tema se da por supuesto que está familiarizado con los conceptos que se describen en [Acceso condicional de Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2a667-113">The scenario outlined in this topic assumes that you are familiar with the concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="2a667-114">Para probar este escenario, deberá:</span><span class="sxs-lookup"><span data-stu-id="2a667-114">To test this scenario, you need to:</span></span>

- <span data-ttu-id="2a667-115">Crear un usuario de prueba</span><span class="sxs-lookup"><span data-stu-id="2a667-115">Create a test user</span></span> 

- <span data-ttu-id="2a667-116">Asignar una licencia de Azure AD Premium al usuario de prueba</span><span class="sxs-lookup"><span data-stu-id="2a667-116">Assign an Azure AD Premium license to the test user</span></span>

- <span data-ttu-id="2a667-117">Configurar una aplicación administrada y asignarle el usuario de prueba</span><span class="sxs-lookup"><span data-stu-id="2a667-117">Configure a managed app and assign your test user to it</span></span>

- <span data-ttu-id="2a667-118">Configurar direcciones IP de confianza</span><span class="sxs-lookup"><span data-stu-id="2a667-118">Configure trusted IPs</span></span>

<span data-ttu-id="2a667-119">Si necesita obtener más información acerca de las direcciones IP de confianza, consulte [Direcciones IP de confianza](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="2a667-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="2a667-120">Pasos de la configuración de la directiva</span><span class="sxs-lookup"><span data-stu-id="2a667-120">Policy configuration steps</span></span>

<span data-ttu-id="2a667-121">**Para configurar la directiva de acceso condicional, haga lo siguiente:**</span><span class="sxs-lookup"><span data-stu-id="2a667-121">**To configure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="2a667-122">En Azure Portal, en la barra de navegación izquierda, haga clic en **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2a667-122">In the Azure portal, on the left navbar, click **Azure Active Directory**.</span></span> 

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="2a667-124">En la hoja **Azure Active Directory**, en la sección **Administrar**, haga clic en **Acceso condicional**.</span><span class="sxs-lookup"><span data-stu-id="2a667-124">On the **Azure Active Directory** blade, in the **Manage** section, click **Conditional access**.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="2a667-126">En la hoja **Acceso condicional**, en la barra de herramientas de la parte superior, haga clic en **Agregar** para abrir la hoja **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="2a667-126">On the **Conditional Access** blade, to open the **New** blade, in the toolbar on the top, click **Add**.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="2a667-128">En la hoja **Nuevo**, en el cuadro de texto **Nombre**, escriba un nombre para la directiva.</span><span class="sxs-lookup"><span data-stu-id="2a667-128">On the **New** blade, in the **Name** textbox, type a name for your policy.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="2a667-130">En la sección **Asignación**, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2a667-130">In the **Assignment** section, click **Users and groups**.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="2a667-132">En la hoja **Usuarios y grupos**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="2a667-132">On the **Users and groups** blade, perform the following steps:</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="2a667-134">a.</span><span class="sxs-lookup"><span data-stu-id="2a667-134">a.</span></span> <span data-ttu-id="2a667-135">Haga clic en **Seleccionar usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2a667-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="2a667-136">b.</span><span class="sxs-lookup"><span data-stu-id="2a667-136">b.</span></span> <span data-ttu-id="2a667-137">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="2a667-137">Click **Select**.</span></span>

    <span data-ttu-id="2a667-138">c.</span><span class="sxs-lookup"><span data-stu-id="2a667-138">c.</span></span> <span data-ttu-id="2a667-139">En la hoja **Seleccionar**, seleccione el usuario de prueba y haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="2a667-139">On the **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="2a667-140">d.</span><span class="sxs-lookup"><span data-stu-id="2a667-140">d.</span></span> <span data-ttu-id="2a667-141">En la hoja **Usuarios y grupos**, haga clic en **Listo**.</span><span class="sxs-lookup"><span data-stu-id="2a667-141">On the **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="2a667-142">En la hoja **Nuevo**, en la sección **Asignación**, haga clic en **Aplicaciones en la nube** para abrir la hoja **Aplicaciones en la nube**.</span><span class="sxs-lookup"><span data-stu-id="2a667-142">On the **New** blade, to open the **Cloud apps** blade, in the **Assignment** section, click **Cloud apps**.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="2a667-144">En la hoja **Aplicaciones en la nube**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="2a667-144">On the **Cloud apps** blade, perform the following steps:</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="2a667-146">a.</span><span class="sxs-lookup"><span data-stu-id="2a667-146">a.</span></span> <span data-ttu-id="2a667-147">Haga clic en **Seleccionar aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2a667-147">Click **Select apps**.</span></span>

    <span data-ttu-id="2a667-148">b.</span><span class="sxs-lookup"><span data-stu-id="2a667-148">b.</span></span> <span data-ttu-id="2a667-149">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="2a667-149">Click **Select**.</span></span>

    <span data-ttu-id="2a667-150">c.</span><span class="sxs-lookup"><span data-stu-id="2a667-150">c.</span></span> <span data-ttu-id="2a667-151">En la hoja **Seleccionar**, seleccione la aplicación en la nube y haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="2a667-151">On the **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="2a667-152">d.</span><span class="sxs-lookup"><span data-stu-id="2a667-152">d.</span></span> <span data-ttu-id="2a667-153">En la hoja **Aplicaciones en la nube**, haga clic en **Listo**.</span><span class="sxs-lookup"><span data-stu-id="2a667-153">On the **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="2a667-154">En la hoja **Nuevo**, en la sección **Asignación**, haga clic en **Condiciones** para abrir la hoja **Condiciones**.</span><span class="sxs-lookup"><span data-stu-id="2a667-154">On the **New** blade, to open the **Conditions** blade, in the **Assignment** section, click **Conditions**.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="2a667-156">En la hoja **Condiciones**, haga clic en **Ubicaciones** para abrir la hoja **Ubicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2a667-156">On the **Conditions** blade, to open the **Locations** blade, click **Locations**.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="2a667-158">En la hoja **Ubicaciones**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="2a667-158">On the **Locations** blade, perform the following steps:</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="2a667-160">a.</span><span class="sxs-lookup"><span data-stu-id="2a667-160">a.</span></span> <span data-ttu-id="2a667-161">En **Configurar**, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="2a667-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="2a667-162">b.</span><span class="sxs-lookup"><span data-stu-id="2a667-162">b.</span></span> <span data-ttu-id="2a667-163">En **Incluir**, haga clic en **Todas las ubicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2a667-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="2a667-164">c.</span><span class="sxs-lookup"><span data-stu-id="2a667-164">c.</span></span> <span data-ttu-id="2a667-165">Haga clic en **Excluir** y, después, haga clic en **Todas las direcciones IP de confianza**.</span><span class="sxs-lookup"><span data-stu-id="2a667-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="2a667-167">d.</span><span class="sxs-lookup"><span data-stu-id="2a667-167">d.</span></span> <span data-ttu-id="2a667-168">Haga clic en **Done**(Listo).</span><span class="sxs-lookup"><span data-stu-id="2a667-168">Click **Done**.</span></span>

12. <span data-ttu-id="2a667-169">En la hoja **Condiciones**, haga clic en **Listo**.</span><span class="sxs-lookup"><span data-stu-id="2a667-169">On the **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="2a667-170">En la hoja **Nuevo**, en la sección **Controles**, haga clic en **Conceder** para abrir la hoja **Conceder**.</span><span class="sxs-lookup"><span data-stu-id="2a667-170">On the **New** blade, to open the **Grant** blade, in the **Controls** section, click **Grant**.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="2a667-172">En la hoja **Conceder**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="2a667-172">On the **Grant** blade, perform the following steps:</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="2a667-174">a.</span><span class="sxs-lookup"><span data-stu-id="2a667-174">a.</span></span> <span data-ttu-id="2a667-175">Seleccione **Requerir autenticación multifactor**.</span><span class="sxs-lookup"><span data-stu-id="2a667-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="2a667-176">b.</span><span class="sxs-lookup"><span data-stu-id="2a667-176">b.</span></span> <span data-ttu-id="2a667-177">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="2a667-177">Click **Select**.</span></span>

15. <span data-ttu-id="2a667-178">En la hoja **Nuevo**, en **Habilitar directiva**, haga clic en **Activar**.</span><span class="sxs-lookup"><span data-stu-id="2a667-178">On the **New** blade, under **Enable policy**, click **On**.</span></span>

    ![Acceso condicional](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="2a667-180">En la hoja **Nuevo**, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2a667-180">On the **New** blade, click **Create**.</span></span>


## <a name="testing-the-policy"></a><span data-ttu-id="2a667-181">Prueba de la directiva</span><span class="sxs-lookup"><span data-stu-id="2a667-181">Testing the policy</span></span>

<span data-ttu-id="2a667-182">Para probar la directiva, debe acceder a la aplicación desde un dispositivo que cumpla estas condiciones:</span><span class="sxs-lookup"><span data-stu-id="2a667-182">To test your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="2a667-183">Tener una dirección IP que esté dentro de las direcciones IP de confianza configuradas.</span><span class="sxs-lookup"><span data-stu-id="2a667-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="2a667-184">Tener una dirección IP que no esté dentro de las direcciones IP de confianza configuradas.</span><span class="sxs-lookup"><span data-stu-id="2a667-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="2a667-185">La autenticación multifactor solo se requerirá durante un intento de conexión realizado desde un dispositivo que no está dentro de las direcciones IP de confianza configuradas.</span><span class="sxs-lookup"><span data-stu-id="2a667-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="2a667-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2a667-186">Next steps</span></span>

<span data-ttu-id="2a667-187">Para más información sobre el acceso condicional, consulte [Acceso condicional de Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2a667-187">If you would like to learn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

