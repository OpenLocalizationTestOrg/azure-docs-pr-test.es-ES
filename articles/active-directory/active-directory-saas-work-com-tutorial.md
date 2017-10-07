---
title: "Tutorial: Integración de Azure Active Directory con Work.com | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Active Directory de Azure y Work.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: dcdc51c884abd78c945b649de99f942d32373cf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="1771f-103">Tutorial: Integración de Azure Active Directory con Work.com</span><span class="sxs-lookup"><span data-stu-id="1771f-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="1771f-104">En este tutorial, aprenderá cómo toointegrate Work.com con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1771f-104">In this tutorial, you learn how toointegrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1771f-105">Integración Work.com con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="1771f-105">Integrating Work.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1771f-106">Puede controlar en Azure AD que tenga acceso tooWork.com</span><span class="sxs-lookup"><span data-stu-id="1771f-106">You can control in Azure AD who has access tooWork.com</span></span>
- <span data-ttu-id="1771f-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooWork.com (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1771f-107">You can enable your users tooautomatically get signed-on tooWork.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1771f-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1771f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1771f-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1771f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1771f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1771f-110">Prerequisites</span></span>

<span data-ttu-id="1771f-111">integración de Azure AD con Work.com tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1771f-111">tooconfigure Azure AD integration with Work.com, you need hello following items:</span></span>

- <span data-ttu-id="1771f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1771f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1771f-113">Una suscripción habilitada para el inicio de sesión único en Work.com</span><span class="sxs-lookup"><span data-stu-id="1771f-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1771f-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="1771f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1771f-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="1771f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1771f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1771f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1771f-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1771f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1771f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="1771f-118">Scenario description</span></span>
<span data-ttu-id="1771f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="1771f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1771f-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="1771f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1771f-121">Agregar Work.com de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="1771f-121">Add Work.com from hello gallery</span></span>
2. <span data-ttu-id="1771f-122">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="1771f-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-hello-gallery"></a><span data-ttu-id="1771f-123">Agregar Work.com de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="1771f-123">Add Work.com from hello gallery</span></span>
<span data-ttu-id="1771f-124">integración de hello tooconfigure de Work.com en Azure AD, deberá tooadd Work.com de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="1771f-124">tooconfigure hello integration of Work.com into Azure AD, you need tooadd Work.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1771f-125">**tooadd Work.com de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1771f-125">**tooadd Work.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1771f-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="1771f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1771f-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="1771f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1771f-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1771f-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="1771f-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1771f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="1771f-133">En el cuadro de búsqueda de hello, escriba **Work.com**, seleccione **Work.com** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1771f-133">In hello search box, type **Work.com**, select **Work.com** from results panel then click **Add** button tooadd hello application.</span></span>

    ![Incorporación desde la galería](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1771f-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="1771f-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="1771f-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Work.com con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1771f-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1771f-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Work.com es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1771f-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Work.com is tooa user in Azure AD.</span></span> <span data-ttu-id="1771f-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Work.com debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="1771f-138">In other words, a link relationship between an Azure AD user and hello related user in Work.com needs toobe established.</span></span>

<span data-ttu-id="1771f-139">En Work.com, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1771f-139">In Work.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1771f-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Work.com, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="1771f-140">tooconfigure and test Azure AD single sign-on with Work.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1771f-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="1771f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1771f-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1771f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1771f-143">**[Crear un usuario de prueba de Work.com](#create-a-workcom-test-user)**  -toohave un equivalente de Britta Simon en Work.com que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="1771f-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - toohave a counterpart of Britta Simon in Work.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1771f-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1771f-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1771f-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="1771f-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1771f-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1771f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1771f-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Work.com.</span><span class="sxs-lookup"><span data-stu-id="1771f-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="1771f-148">tooconfigure inicio de sesión único, es necesario un nombre de dominio personalizado de Work.com toosetup aún.</span><span class="sxs-lookup"><span data-stu-id="1771f-148">tooconfigure single sign-on, you need toosetup a custom Work.com domain name yet.</span></span> <span data-ttu-id="1771f-149">Necesita toodefine al menos un dominio nombre, el nombre de dominio de prueba e impleméntelo tooyour toda la organización.</span><span class="sxs-lookup"><span data-stu-id="1771f-149">You need toodefine at least a domain name, test your domain name, and deploy it tooyour entire organization.</span></span>

<span data-ttu-id="1771f-150">**inicio de sesión único en Azure AD tooconfigure con Work.com, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1771f-150">**tooconfigure Azure AD single sign-on with Work.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="1771f-151">En el portal de Azure, en Hola Hola **Work.com** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1771f-151">In hello Azure portal, on hello **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="1771f-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1771f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Inicio de sesión basado en SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="1771f-155">En hello **Work.com dominio y las direcciones URL** sección, realice Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="1771f-155">On hello **Work.com Domain and URLs** section, perform hello following:</span></span>

    ![Sección Dominio y direcciones URL de Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="1771f-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`http://<companyname>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="1771f-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1771f-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="1771f-158">This value is not real.</span></span> <span data-ttu-id="1771f-159">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="1771f-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="1771f-160">Póngase en contacto con [equipo de soporte técnico de cliente de Work.com](https://help.salesforce.com/articleView?id=000159855&type=3) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="1771f-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) tooget this value.</span></span> 

4. <span data-ttu-id="1771f-161">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="1771f-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Sección Certificado de firma SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="1771f-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="1771f-163">Click **Save** button.</span></span>

    ![Botón Guardar](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1771f-165">En hello **configuración de Work.com** sección, haga clic en **configurar Work.com** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="1771f-165">On hello **Work.com Configuration** section, click **Configure Work.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1771f-166">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="1771f-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Sección de configuración de Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="1771f-168">Inicie sesión en tooyour inquilino de Work.com como administrador.</span><span class="sxs-lookup"><span data-stu-id="1771f-168">Log in tooyour Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="1771f-169">Vaya demasiado**el programa de instalación**.</span><span class="sxs-lookup"><span data-stu-id="1771f-169">Go too**Setup**.</span></span>
   
    <span data-ttu-id="1771f-170">![Instalación](./media/active-directory-saas-work-com-tutorial/ic794108.png "Instalación")</span><span class="sxs-lookup"><span data-stu-id="1771f-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="1771f-171">En el panel de navegación izquierdo de hello, Hola **administrar** sección, haga clic en **Domain Management** tooexpand Hola sección relacionada y, a continuación, haga clic en **mi dominio** tooopen hello  **Mi dominio** página.</span><span class="sxs-lookup"><span data-stu-id="1771f-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
    <span data-ttu-id="1771f-172">![Mi dominio](./media/active-directory-saas-work-com-tutorial/ic767825.png "Mi dominio")</span><span class="sxs-lookup"><span data-stu-id="1771f-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="1771f-173">tooverify que el dominio se ha configurado correctamente, asegúrese de que se encuentra en "**paso 4 implementado tooUsers**" y revise el "**mi configuración de dominio**".</span><span class="sxs-lookup"><span data-stu-id="1771f-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="1771f-174">![Dominio implementado tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "tooUser implementadas de dominio")</span><span class="sxs-lookup"><span data-stu-id="1771f-174">![Domain Deployed tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="1771f-175">Inicie sesión en tooyour inquilino de Work.com.</span><span class="sxs-lookup"><span data-stu-id="1771f-175">Log in tooyour Work.com tenant.</span></span>

12. <span data-ttu-id="1771f-176">Vaya demasiado**el programa de instalación**.</span><span class="sxs-lookup"><span data-stu-id="1771f-176">Go too**Setup**.</span></span>
    
    <span data-ttu-id="1771f-177">![Instalación](./media/active-directory-saas-work-com-tutorial/ic794108.png "Instalación")</span><span class="sxs-lookup"><span data-stu-id="1771f-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="1771f-178">Expanda hello **controles de seguridad** menú y, a continuación, haga clic en **configuración de inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1771f-178">Expand hello **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="1771f-179">![Configuración de inicio de sesión único](./media/active-directory-saas-work-com-tutorial/ic794113.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="1771f-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="1771f-180">En hello **configuración de inicio de sesión único** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="1771f-180">On hello **Single Sign-On Settings** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="1771f-181">![SAML habilitado](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML habilitado")</span><span class="sxs-lookup"><span data-stu-id="1771f-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="1771f-182">a.</span><span class="sxs-lookup"><span data-stu-id="1771f-182">a.</span></span> <span data-ttu-id="1771f-183">Seleccione **SAML habilitado**.</span><span class="sxs-lookup"><span data-stu-id="1771f-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="1771f-184">b.</span><span class="sxs-lookup"><span data-stu-id="1771f-184">b.</span></span> <span data-ttu-id="1771f-185">Haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="1771f-185">Click **New**.</span></span>

15. <span data-ttu-id="1771f-186">Hola **configuración de inicio de sesión único de SAML** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="1771f-186">In hello **SAML Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="1771f-187">![Inicio de sesión único SAML](./media/active-directory-saas-work-com-tutorial/ic794114.png "Inicio de sesión único SAML")</span><span class="sxs-lookup"><span data-stu-id="1771f-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="1771f-188">a.</span><span class="sxs-lookup"><span data-stu-id="1771f-188">a.</span></span> <span data-ttu-id="1771f-189">Hola **nombre** cuadro de texto, escriba un nombre para la configuración.</span><span class="sxs-lookup"><span data-stu-id="1771f-189">In hello **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="1771f-190">Proporciona un valor para **nombre** rellenar automáticamente hello **nombre de la API** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="1771f-190">Providing a value for **Name** does automatically populate hello **API Name** textbox.</span></span>
    
    <span data-ttu-id="1771f-191">b.</span><span class="sxs-lookup"><span data-stu-id="1771f-191">b.</span></span> <span data-ttu-id="1771f-192">En **emisor** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1771f-192">In **Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="1771f-193">c.</span><span class="sxs-lookup"><span data-stu-id="1771f-193">c.</span></span> <span data-ttu-id="1771f-194">tooupload Hola Descargar certificado desde el portal de Azure, haga clic en **examinar**.</span><span class="sxs-lookup"><span data-stu-id="1771f-194">tooupload hello downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="1771f-195">d.</span><span class="sxs-lookup"><span data-stu-id="1771f-195">d.</span></span> <span data-ttu-id="1771f-196">Hola **Id. de entidad** cuadro de texto, tipo `https://salesforce-work.com`.</span><span class="sxs-lookup"><span data-stu-id="1771f-196">In hello **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="1771f-197">e.</span><span class="sxs-lookup"><span data-stu-id="1771f-197">e.</span></span> <span data-ttu-id="1771f-198">Como **tipo de identidad SAML**, seleccione **la aserción contiene Hola Id. de federación del objeto de usuario de hello**.</span><span class="sxs-lookup"><span data-stu-id="1771f-198">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
    
    <span data-ttu-id="1771f-199">f.</span><span class="sxs-lookup"><span data-stu-id="1771f-199">f.</span></span> <span data-ttu-id="1771f-200">Como **ubicación de identidad SAML**, seleccione **identidad está en el elemento NameIdentifier de Hola de hello instrucción Subject**.</span><span class="sxs-lookup"><span data-stu-id="1771f-200">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>
    
    <span data-ttu-id="1771f-201">g.</span><span class="sxs-lookup"><span data-stu-id="1771f-201">g.</span></span> <span data-ttu-id="1771f-202">En **URL de inicio de sesión del proveedor de identidades** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1771f-202">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1771f-203">h.</span><span class="sxs-lookup"><span data-stu-id="1771f-203">h.</span></span> <span data-ttu-id="1771f-204">En **URL de cierre de sesión del proveedor de identidades** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1771f-204">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="1771f-205">i.</span><span class="sxs-lookup"><span data-stu-id="1771f-205">i.</span></span> <span data-ttu-id="1771f-206">Para **Service Provider Initiated Request Binding** (Enlace de solicitud iniciada por el proveedor de servicio), seleccione **HTTP Post** (Método HTTP Post).</span><span class="sxs-lookup"><span data-stu-id="1771f-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="1771f-207">j.</span><span class="sxs-lookup"><span data-stu-id="1771f-207">j.</span></span> <span data-ttu-id="1771f-208">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1771f-208">Click **Save**.</span></span>

16. <span data-ttu-id="1771f-209">En el portal clásico de Work.com, en el panel de navegación izquierdo de hello, haga clic en **Domain Management** tooexpand Hola sección relacionada y, a continuación, haga clic en **mi dominio** tooopen hello **mi dominio**página.</span><span class="sxs-lookup"><span data-stu-id="1771f-209">In your Work.com classic portal, on hello left navigation pane, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="1771f-210">![Mi dominio](./media/active-directory-saas-work-com-tutorial/ic794115.png "Mi dominio")</span><span class="sxs-lookup"><span data-stu-id="1771f-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="1771f-211">En hello **mi dominio** página Hola **personalización de la página de inicio de sesión** sección, haga clic en **editar**.</span><span class="sxs-lookup"><span data-stu-id="1771f-211">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="1771f-212">![Personalización de marca de página de inicio de sesión](./media/active-directory-saas-work-com-tutorial/ic767826.png "Personalización de marca de página de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="1771f-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="1771f-213">En hello **personalización de la página de inicio de sesión** página Hola **servicio de autenticación** sección, el nombre de Hola de su **configuración de SSO de SAML** se muestra.</span><span class="sxs-lookup"><span data-stu-id="1771f-213">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="1771f-214">Selecciónelo y luego haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="1771f-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="1771f-215">![Personalización de marca de página de inicio de sesión](./media/active-directory-saas-work-com-tutorial/ic784366.png "Personalización de marca de página de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="1771f-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="1771f-216">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="1771f-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1771f-217">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="1771f-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1771f-218">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1771f-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1771f-219">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1771f-219">Create an Azure AD test user</span></span>
<span data-ttu-id="1771f-220">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="1771f-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="1771f-222">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1771f-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1771f-223">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="1771f-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1771f-225">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1771f-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Usuarios y grupos -> Todos los usuarios](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1771f-227">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1771f-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Sumar](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1771f-229">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="1771f-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Página del cuadro de diálogo Usuario](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1771f-231">a.</span><span class="sxs-lookup"><span data-stu-id="1771f-231">a.</span></span> <span data-ttu-id="1771f-232">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1771f-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1771f-233">b.</span><span class="sxs-lookup"><span data-stu-id="1771f-233">b.</span></span> <span data-ttu-id="1771f-234">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1771f-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1771f-235">c.</span><span class="sxs-lookup"><span data-stu-id="1771f-235">c.</span></span> <span data-ttu-id="1771f-236">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="1771f-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1771f-237">d.</span><span class="sxs-lookup"><span data-stu-id="1771f-237">d.</span></span> <span data-ttu-id="1771f-238">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1771f-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="1771f-239">Creación de un usuario de prueba de Work.com</span><span class="sxs-lookup"><span data-stu-id="1771f-239">Create a Work.com test user</span></span>
<span data-ttu-id="1771f-240">Para Azure Active Directory a los usuarios toobe puede toosign en, deben ser tooWork.com aprovisionado. En caso de hello de Work.com, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="1771f-240">For Azure Active Directory users toobe able toosign in, they must be provisioned tooWork.com. In hello case of Work.com, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="1771f-241">tooconfigure aprovisionamiento de usuario, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="1771f-241">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="1771f-242">Inicie sesión en tooyour sitio de empresa de Work.com como administrador.</span><span class="sxs-lookup"><span data-stu-id="1771f-242">Sign on tooyour Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="1771f-243">Vaya demasiado**el programa de instalación**.</span><span class="sxs-lookup"><span data-stu-id="1771f-243">Go too**Setup**.</span></span>
   
    <span data-ttu-id="1771f-244">![Instalación](./media/active-directory-saas-work-com-tutorial/IC794108.png "Instalación")</span><span class="sxs-lookup"><span data-stu-id="1771f-244">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="1771f-245">Vaya demasiado**administrar usuarios \> usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1771f-245">Go too**Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="1771f-246">![Administración de usuarios](./media/active-directory-saas-work-com-tutorial/IC784369.png "Administración de usuarios")</span><span class="sxs-lookup"><span data-stu-id="1771f-246">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="1771f-247">Haga clic en **Nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="1771f-247">Click **New User**.</span></span>
   
    <span data-ttu-id="1771f-248">![Todos los usuarios](./media/active-directory-saas-work-com-tutorial/IC794117.png "Todos los usuarios")</span><span class="sxs-lookup"><span data-stu-id="1771f-248">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="1771f-249">En la sección Editar usuarios hello, realizar Hola siguiendo los pasos, en los atributos de un Azure válida cuadros de texto relacionados con la cuenta de AD que quiera tooprovision en hello:</span><span class="sxs-lookup"><span data-stu-id="1771f-249">In hello User Edit section, perform hello following steps, in attributes of a valid Azure AD account you want tooprovision into hello related textboxes:</span></span>
   
    <span data-ttu-id="1771f-250">![Edición de usuario](./media/active-directory-saas-work-com-tutorial/ic794118.png "Edición de usuario")</span><span class="sxs-lookup"><span data-stu-id="1771f-250">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="1771f-251">a.</span><span class="sxs-lookup"><span data-stu-id="1771f-251">a.</span></span> <span data-ttu-id="1771f-252">Hola **nombre** cuadro de texto, hello tipo **nombre** del usuario de hello **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="1771f-252">In hello **First Name** textbox, type hello **first name** of hello user **Britta**.</span></span>
    
    <span data-ttu-id="1771f-253">b.</span><span class="sxs-lookup"><span data-stu-id="1771f-253">b.</span></span> <span data-ttu-id="1771f-254">Hola **Last Name** cuadro de texto, hello tipo **apellidos** del usuario de hello **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1771f-254">In hello **Last Name** textbox, type hello **last name** of hello user **Simon**.</span></span>
    
    <span data-ttu-id="1771f-255">c.</span><span class="sxs-lookup"><span data-stu-id="1771f-255">c.</span></span> <span data-ttu-id="1771f-256">Hola **Alias** cuadro de texto, hello tipo **nombre** del usuario de hello **BrittaS**.</span><span class="sxs-lookup"><span data-stu-id="1771f-256">In hello **Alias** textbox, type hello **name** of hello user **BrittaS**.</span></span>
    
    <span data-ttu-id="1771f-257">d.</span><span class="sxs-lookup"><span data-stu-id="1771f-257">d.</span></span> <span data-ttu-id="1771f-258">Hola **correo electrónico** cuadro de texto, hello tipo **dirección de correo electrónico** del usuario  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="1771f-258">In hello **Email** textbox, type hello **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="1771f-259">e.</span><span class="sxs-lookup"><span data-stu-id="1771f-259">e.</span></span> <span data-ttu-id="1771f-260">Hola **nombre de usuario** cuadro de texto, escriba un nombre de usuario del usuario como  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="1771f-260">In hello **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="1771f-261">f.</span><span class="sxs-lookup"><span data-stu-id="1771f-261">f.</span></span> <span data-ttu-id="1771f-262">Hola **nombre Nick** cuadro de texto, escriba un **nombre nick** del usuario **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1771f-262">In hello **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="1771f-263">g.</span><span class="sxs-lookup"><span data-stu-id="1771f-263">g.</span></span> <span data-ttu-id="1771f-264">Seleccione **Role** (Rol), **User License** (Licencia de usuario) y **Profile** (Perfil).</span><span class="sxs-lookup"><span data-stu-id="1771f-264">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="1771f-265">h.</span><span class="sxs-lookup"><span data-stu-id="1771f-265">h.</span></span> <span data-ttu-id="1771f-266">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1771f-266">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="1771f-267">titular de cuenta de Hello Azure AD recibirá un correo electrónico con una cuenta de hello tooconfirm vínculo antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="1771f-267">hello Azure AD account holder will get an email including a link tooconfirm hello account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1771f-268">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1771f-268">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1771f-269">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooWork.com.</span><span class="sxs-lookup"><span data-stu-id="1771f-269">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWork.com.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="1771f-271">**tooassign Britta Simon tooWork.com, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1771f-271">**tooassign Britta Simon tooWork.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="1771f-272">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1771f-272">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="1771f-274">En la lista de aplicaciones de hello, seleccione **Work.com**.</span><span class="sxs-lookup"><span data-stu-id="1771f-274">In hello applications list, select **Work.com**.</span></span>

    ![Work.com en la lista de la aplicación](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="1771f-276">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1771f-276">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="1771f-278">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1771f-278">Click **Add** button.</span></span> <span data-ttu-id="1771f-279">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1771f-279">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="1771f-281">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="1771f-281">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1771f-282">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1771f-282">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1771f-283">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1771f-283">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1771f-284">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="1771f-284">Test single sign-on</span></span>

<span data-ttu-id="1771f-285">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="1771f-285">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1771f-286">Al hacer clic en icono de Work.com Hola Hola Panel de acceso, deberá obtener aplicaciones de Work.com tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="1771f-286">When you click hello Work.com tile in hello Access Panel, you should get automatically signed-on tooyour Work.com application.</span></span>
<span data-ttu-id="1771f-287">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1771f-287">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1771f-288">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="1771f-288">Additional resources</span></span>

* [<span data-ttu-id="1771f-289">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1771f-289">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1771f-290">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1771f-290">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

