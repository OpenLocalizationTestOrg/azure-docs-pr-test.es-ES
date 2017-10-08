---
title: "Tutorial: Integración de Azure Active Directory con O.C. Tanner - AppreciateHub | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y O.C. Tanner - AppreciateHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 45052cf56e35746d7df5910162e40e3bbcad1aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a><span data-ttu-id="8eb6f-105">Tutorial: Integración de Azure Active Directory con O.C.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-105">Tutorial: Azure Active Directory integration with O.C.</span></span> <span data-ttu-id="8eb6f-106">C. Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="8eb6f-106">Tanner - AppreciateHub</span></span>

<span data-ttu-id="8eb6f-107">En este tutorial, aprenderá cómo toointegrate O.C.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-107">In this tutorial, you learn how toointegrate O.C.</span></span> <span data-ttu-id="8eb6f-108">Tanner - AppreciateHub con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8eb6f-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8eb6f-109">Integración de O.C.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-109">Integrating O.C.</span></span> <span data-ttu-id="8eb6f-110">Díaz - AppreciateHub con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="8eb6f-110">Tanner - AppreciateHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8eb6f-111">Puede controlar en Azure AD que tenga acceso tooO.C.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-111">You can control in Azure AD who has access tooO.C.</span></span> <span data-ttu-id="8eb6f-112">C. Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="8eb6f-112">Tanner - AppreciateHub</span></span>
- <span data-ttu-id="8eb6f-113">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooO.C.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-113">You can enable your users tooautomatically get signed-on tooO.C.</span></span> <span data-ttu-id="8eb6f-114">Tanner - AppreciateHub (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8eb6f-115">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8eb6f-115">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8eb6f-116">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8eb6f-116">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8eb6f-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8eb6f-117">Prerequisites</span></span>

<span data-ttu-id="8eb6f-118">integración de Azure AD con O.C. tooconfigure</span><span class="sxs-lookup"><span data-stu-id="8eb6f-118">tooconfigure Azure AD integration with O.C.</span></span> <span data-ttu-id="8eb6f-119">Díaz - AppreciateHub, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8eb6f-119">Tanner - AppreciateHub, you need hello following items:</span></span>

- <span data-ttu-id="8eb6f-120">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8eb6f-120">An Azure AD subscription</span></span>
- <span data-ttu-id="8eb6f-121">Una suscripción habilitada para el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="8eb6f-121">A O.C.</span></span> <span data-ttu-id="8eb6f-122">Una suscripción habilitada para el inicio de sesión único en Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="8eb6f-122">Tanner - AppreciateHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8eb6f-123">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-123">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8eb6f-124">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="8eb6f-124">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8eb6f-125">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-125">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8eb6f-126">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8eb6f-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8eb6f-127">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="8eb6f-127">Scenario description</span></span>
<span data-ttu-id="8eb6f-128">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8eb6f-129">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="8eb6f-129">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8eb6f-130">Agregar O.C.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-130">Adding O.C.</span></span> <span data-ttu-id="8eb6f-131">Díaz - AppreciateHub de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="8eb6f-131">Tanner - AppreciateHub from hello gallery</span></span>
2. <span data-ttu-id="8eb6f-132">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8eb6f-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-hello-gallery"></a><span data-ttu-id="8eb6f-133">Agregar O.C.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-133">Adding O.C.</span></span> <span data-ttu-id="8eb6f-134">Díaz - AppreciateHub de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="8eb6f-134">Tanner - AppreciateHub from hello gallery</span></span>
<span data-ttu-id="8eb6f-135">integración de hello tooconfigure de O.C.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-135">tooconfigure hello integration of O.C.</span></span> <span data-ttu-id="8eb6f-136">Díaz - AppreciateHub en Azure AD, necesita tooadd O.C.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-136">Tanner - AppreciateHub into Azure AD, you need tooadd O.C.</span></span> <span data-ttu-id="8eb6f-137">Díaz - AppreciateHub de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-137">Tanner - AppreciateHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8eb6f-138">**tooadd O.C. Díaz - AppreciateHub de galería de hello, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8eb6f-138">**tooadd O.C. Tanner - AppreciateHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8eb6f-139">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-139">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8eb6f-141">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-141">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8eb6f-142">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-142">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="8eb6f-144">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-144">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="8eb6f-146">En el cuadro de búsqueda de hello, escriba **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-146">In hello search box, type **O.C. Tanner - AppreciateHub**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. <span data-ttu-id="8eb6f-148">En el panel de resultados de hello, seleccione **O.C. Díaz - AppreciateHub**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-148">In hello results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8eb6f-150">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8eb6f-150">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8eb6f-151">En esta sección, configurará y probará el inicio de sesión único de Azure AD con O.C.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-151">In this section, you configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="8eb6f-152">Tanner - AppreciateHub en función de un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8eb6f-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8eb6f-153">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en O.C.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-153">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in O.C.</span></span> <span data-ttu-id="8eb6f-154">Díaz - AppreciateHub es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-154">Tanner - AppreciateHub is tooa user in Azure AD.</span></span> <span data-ttu-id="8eb6f-155">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en O.C.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-155">In other words, a link relationship between an Azure AD user and hello related user in O.C.</span></span> <span data-ttu-id="8eb6f-156">Díaz - AppreciateHub debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-156">Tanner - AppreciateHub needs toobe established.</span></span>

<span data-ttu-id="8eb6f-157">Para establecer</span><span class="sxs-lookup"><span data-stu-id="8eb6f-157">In O.C.</span></span> <span data-ttu-id="8eb6f-158">Díaz - AppreciateHub, asignar Hola valo hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-158">Tanner - AppreciateHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8eb6f-159">tooconfigure y prueba de inicio de sesión único en Azure AD con O.C.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-159">tooconfigure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="8eb6f-160">Díaz - AppreciateHub, necesita hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="8eb6f-160">Tanner - AppreciateHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8eb6f-161">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8eb6f-162">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8eb6f-163">**[Creación de un usuario de prueba de O.C. Díaz - usuario de prueba de AppreciateHub](#creating-a-oc-tanner---appreciatehub-test-user)**  -toohave un equivalente de Britta Simon en O.C.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - toohave a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="8eb6f-164">Díaz - AppreciateHub que está vinculado toohello representación de Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-164">Tanner - AppreciateHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8eb6f-165">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-165">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8eb6f-166">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-166">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8eb6f-167">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8eb6f-167">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8eb6f-168">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en su O.C.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-168">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your O.C.</span></span> <span data-ttu-id="8eb6f-169">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-169">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="8eb6f-170">**inicio de sesión único en Azure AD tooconfigure con O.C. Díaz - AppreciateHub, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8eb6f-170">**tooconfigure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="8eb6f-171">En el portal de Azure, en Hola Hola **O.C. Tanner - AppreciateHub**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-171">In hello Azure portal, on hello **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="8eb6f-173">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-173">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. <span data-ttu-id="8eb6f-175">En hello **O.C. Díaz - AppreciateHub dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8eb6f-175">On hello **O.C. Tanner - AppreciateHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    <span data-ttu-id="8eb6f-177">a.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-177">a.</span></span> <span data-ttu-id="8eb6f-178">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span><span class="sxs-lookup"><span data-stu-id="8eb6f-178">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8eb6f-179">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-179">This value is not real.</span></span> <span data-ttu-id="8eb6f-180">Actualizar este valor con la dirección URL de respuesta real Hola.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-180">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="8eb6f-181">Póngase en contacto con el [equipo de soporte Díaz - equipo de soporte técnico de AppreciateHub](mailto:sso@octanner.com) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) tooget this value.</span></span>

    <span data-ttu-id="8eb6f-182">b.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-182">b.</span></span> <span data-ttu-id="8eb6f-183">Archivo de metadatos de hello abierto con hello siguiente vínculo: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span><span class="sxs-lookup"><span data-stu-id="8eb6f-183">Open hello metadata file using hello following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
    <span data-ttu-id="8eb6f-184">c.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-184">c.</span></span> <span data-ttu-id="8eb6f-185">Busque hello **md:AssertionConsumerService** nodo.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-185">Locate hello **md:AssertionConsumerService** node.</span></span> 
   
    <span data-ttu-id="8eb6f-186">d.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-186">d.</span></span> <span data-ttu-id="8eb6f-187">Copiar valor de Hola de hello **ubicación** atributo.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-187">Copy hello value of hello **Location** attribute.</span></span> 
   
    ![Configurar las opciones de la aplicación][12]
   
    <span data-ttu-id="8eb6f-189">e.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-189">e.</span></span> <span data-ttu-id="8eb6f-190">Hola **dirección URL de inicio de sesión** cuadro de texto, más allá valor Hola ha obtenido en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-190">In hello **Sign On URL** textbox, past hello value you have obtained in hello previous step.</span></span>

4. <span data-ttu-id="8eb6f-191">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-191">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. <span data-ttu-id="8eb6f-193">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="8eb6f-193">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8eb6f-195">inicio de sesión único en tooconfigure en **O.C. Díaz - AppreciateHub** lado, necesita hello toosend descargado **Metadata XML** demasiado[O.C. de O.C. Tanner - AppreciateHub](mailto:sso@octanner.com).</span><span class="sxs-lookup"><span data-stu-id="8eb6f-195">tooconfigure single sign-on on **O.C. Tanner - AppreciateHub** side, you need toosend hello downloaded **Metadata XML** too[O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span></span>

> [!TIP]
> <span data-ttu-id="8eb6f-196">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="8eb6f-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8eb6f-197">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8eb6f-198">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8eb6f-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8eb6f-199">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8eb6f-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="8eb6f-200">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="8eb6f-202">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8eb6f-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8eb6f-203">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8eb6f-205">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8eb6f-207">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8eb6f-209">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="8eb6f-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8eb6f-211">a.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-211">a.</span></span> <span data-ttu-id="8eb6f-212">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8eb6f-213">b.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-213">b.</span></span> <span data-ttu-id="8eb6f-214">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8eb6f-215">c.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-215">c.</span></span> <span data-ttu-id="8eb6f-216">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8eb6f-217">d.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-217">d.</span></span> <span data-ttu-id="8eb6f-218">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-218">Click **Create**.</span></span>
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="8eb6f-219">Creación de un usuario de prueba de O.C.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-219">Creating a O.C.</span></span> <span data-ttu-id="8eb6f-220">C. Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="8eb6f-220">Tanner - AppreciateHub test user</span></span>

<span data-ttu-id="8eb6f-221">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en O.C. toocreate</span><span class="sxs-lookup"><span data-stu-id="8eb6f-221">hello objective of this section is toocreate a user called Britta Simon in O.C.</span></span> <span data-ttu-id="8eb6f-222">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-222">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="8eb6f-223">**toocreate un usuario denominado a Britta Simon en O.C. Díaz - AppreciateHub, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8eb6f-223">**toocreate a user called Britta Simon in O.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

<span data-ttu-id="8eb6f-224">Consulte al [equipo de soporte técnico de O.C. Díaz - equipo de soporte técnico de AppreciateHub](mailto:sso@octanner.com) toocreate un usuario que tenga como Hola de atributo nameID mismo valor que el nombre de usuario de Hola de Britta Simon en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) toocreate a user that has as nameID attribute hello same value as hello user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8eb6f-225">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8eb6f-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8eb6f-226">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooO.C.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooO.C.</span></span> <span data-ttu-id="8eb6f-227">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-227">Tanner - AppreciateHub.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="8eb6f-229">**tooassign Britta Simon tooO.C. Díaz - AppreciateHub, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8eb6f-229">**tooassign Britta Simon tooO.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="8eb6f-230">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="8eb6f-232">En la lista de aplicaciones de hello, seleccione **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-232">In hello applications list, select **O.C. Tanner - AppreciateHub**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. <span data-ttu-id="8eb6f-234">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="8eb6f-236">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-236">Click **Add** button.</span></span> <span data-ttu-id="8eb6f-237">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="8eb6f-239">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8eb6f-240">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8eb6f-241">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8eb6f-242">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="8eb6f-242">Testing single sign-on</span></span>

<span data-ttu-id="8eb6f-243">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="8eb6f-244">Al hacer clic en hello O.C.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-244">When you click hello O.C.</span></span> <span data-ttu-id="8eb6f-245">Díaz - icono de AppreciateHub en Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour O.C.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-245">Tanner - AppreciateHub tile in hello Access Panel, you should get automatically signed-on tooyour O.C.</span></span> <span data-ttu-id="8eb6f-246">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="8eb6f-246">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8eb6f-247">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8eb6f-247">Additional resources</span></span>

* [<span data-ttu-id="8eb6f-248">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8eb6f-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8eb6f-249">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8eb6f-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png

