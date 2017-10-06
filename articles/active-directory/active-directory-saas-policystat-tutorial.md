---
title: "Tutorial: Integración de Azure Active Directory con PolicyStat | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y PolicyStat."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 868053cd0d37359fd9b4aeb93dba42cbbaa09845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="87370-103">Tutorial: Integración de Azure Active Directory con PolicyStat</span><span class="sxs-lookup"><span data-stu-id="87370-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="87370-104">En este tutorial, aprenderá cómo toointegrate PolicyStat con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="87370-104">In this tutorial, you learn how toointegrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="87370-105">Integración PolicyStat con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="87370-105">Integrating PolicyStat with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="87370-106">Puede controlar en Azure AD que tenga acceso tooPolicyStat</span><span class="sxs-lookup"><span data-stu-id="87370-106">You can control in Azure AD who has access tooPolicyStat</span></span>
- <span data-ttu-id="87370-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooPolicyStat (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="87370-107">You can enable your users tooautomatically get signed-on tooPolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="87370-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="87370-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="87370-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="87370-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87370-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="87370-110">Prerequisites</span></span>

<span data-ttu-id="87370-111">integración de Azure AD con PolicyStat tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="87370-111">tooconfigure Azure AD integration with PolicyStat, you need hello following items:</span></span>

- <span data-ttu-id="87370-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="87370-112">An Azure AD subscription</span></span>
- <span data-ttu-id="87370-113">Una suscripción habilitada para el inicio de sesión único en PolicyStat</span><span class="sxs-lookup"><span data-stu-id="87370-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="87370-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="87370-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="87370-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="87370-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="87370-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="87370-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="87370-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="87370-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="87370-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="87370-118">Scenario description</span></span>
<span data-ttu-id="87370-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="87370-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="87370-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="87370-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="87370-121">Agregar PolicyStat desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="87370-121">Adding PolicyStat from hello gallery</span></span>
2. <span data-ttu-id="87370-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="87370-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-hello-gallery"></a><span data-ttu-id="87370-123">Agregar PolicyStat desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="87370-123">Adding PolicyStat from hello gallery</span></span>
<span data-ttu-id="87370-124">integración de hello tooconfigure de PolicyStat en Azure AD, deberá tooadd PolicyStat de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="87370-124">tooconfigure hello integration of PolicyStat into Azure AD, you need tooadd PolicyStat from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="87370-125">**tooadd PolicyStat de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="87370-125">**tooadd PolicyStat from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="87370-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="87370-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="87370-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="87370-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="87370-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="87370-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="87370-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="87370-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="87370-133">En el cuadro de búsqueda de hello, escriba **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="87370-133">In hello search box, type **PolicyStat**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. <span data-ttu-id="87370-135">En el panel de resultados de hello, seleccione **PolicyStat**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="87370-135">In hello results panel, select **PolicyStat**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="87370-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="87370-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="87370-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con PolicyStat con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="87370-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="87370-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en PolicyStat es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87370-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PolicyStat is tooa user in Azure AD.</span></span> <span data-ttu-id="87370-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en PolicyStat debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="87370-140">In other words, a link relationship between an Azure AD user and hello related user in PolicyStat needs toobe established.</span></span>

<span data-ttu-id="87370-141">En PolicyStat, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="87370-141">In PolicyStat, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="87370-142">tooconfigure y prueba de inicio de sesión único en Azure AD con PolicyStat, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="87370-142">tooconfigure and test Azure AD single sign-on with PolicyStat, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="87370-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="87370-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="87370-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="87370-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="87370-145">**[Crear un usuario de prueba PolicyStat](#creating-a-policystat-test-user)**  -toohave un equivalente de Britta Simon en PolicyStat que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="87370-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - toohave a counterpart of Britta Simon in PolicyStat that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="87370-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="87370-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="87370-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="87370-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="87370-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="87370-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="87370-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="87370-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="87370-150">**inicio de sesión único en Azure AD tooconfigure con PolicyStat, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="87370-150">**tooconfigure Azure AD single sign-on with PolicyStat, perform hello following steps:**</span></span>

1. <span data-ttu-id="87370-151">En el portal de Azure, en Hola Hola **PolicyStat** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="87370-151">In hello Azure portal, on hello **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="87370-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="87370-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. <span data-ttu-id="87370-155">En hello **PolicyStat dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="87370-155">On hello **PolicyStat Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="87370-157">a.</span><span class="sxs-lookup"><span data-stu-id="87370-157">a.</span></span> <span data-ttu-id="87370-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.policystat.com`</span><span class="sxs-lookup"><span data-stu-id="87370-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="87370-159">b.</span><span class="sxs-lookup"><span data-stu-id="87370-159">b.</span></span> <span data-ttu-id="87370-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.policystat.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="87370-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="87370-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="87370-161">These values are not real.</span></span> <span data-ttu-id="87370-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="87370-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="87370-163">Póngase en contacto con [equipo de soporte técnico de cliente de PolicyStat](http://www.policystat.com/support/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="87370-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="87370-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="87370-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. <span data-ttu-id="87370-166">objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooPolicyStat con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.</span><span class="sxs-lookup"><span data-stu-id="87370-166">hello objective of this section is toooutline how tooenable users tooauthenticate tooPolicyStat with their account in Azure AD using federation based on hello SAML protocol.</span></span>

    <span data-ttu-id="87370-167">Hola PolicyStat aplicación espera las aserciones de SAML de hello en un formato específico, lo que requiere tooyour de asignaciones de atributo personalizado de tooadd **atributos de Token SAML** configuración.</span><span class="sxs-lookup"><span data-stu-id="87370-167">hello PolicyStat application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="87370-168">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="87370-168">hello following screenshot shows an example of this.</span></span>

     <span data-ttu-id="87370-169">![Atributos](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="87370-169">![Attributes](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

6. <span data-ttu-id="87370-170">asignaciones de atributos de tooadd Hola necesario, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="87370-170">tooadd hello required attribute mappings, perform hello following steps:</span></span>

    | <span data-ttu-id="87370-171">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="87370-171">Attribute Name</span></span>    |   <span data-ttu-id="87370-172">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="87370-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="87370-173">uid</span><span class="sxs-lookup"><span data-stu-id="87370-173">uid</span></span> | <span data-ttu-id="87370-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="87370-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="87370-175">a.</span><span class="sxs-lookup"><span data-stu-id="87370-175">a.</span></span> <span data-ttu-id="87370-176">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="87370-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="87370-179">b.</span><span class="sxs-lookup"><span data-stu-id="87370-179">b.</span></span> <span data-ttu-id="87370-180">Hola **nombre del atributo** cuadro de texto, tipo **uid**.</span><span class="sxs-lookup"><span data-stu-id="87370-180">In hello **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="87370-181">c.</span><span class="sxs-lookup"><span data-stu-id="87370-181">c.</span></span> <span data-ttu-id="87370-182">Hola **valor del atributo** cuadro de texto, seleccione **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="87370-182">In hello **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="87370-183">d.</span><span class="sxs-lookup"><span data-stu-id="87370-183">d.</span></span> <span data-ttu-id="87370-184">De hello **correo** lista, seleccione **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="87370-184">From hello **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="87370-185">e.</span><span class="sxs-lookup"><span data-stu-id="87370-185">e.</span></span> <span data-ttu-id="87370-186">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="87370-186">Click **Ok**</span></span>

7. <span data-ttu-id="87370-187">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="87370-187">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="87370-189">En otra ventana del explorador web, inicie sesión en el sitio de la compañía PolicyStat como administrador.</span><span class="sxs-lookup"><span data-stu-id="87370-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

9. <span data-ttu-id="87370-190">Haga clic en hello **administración** ficha y, a continuación, haga clic en **configuración de inicio de sesión único** en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="87370-190">Click hello **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="87370-191">![Menú Administrator](./media/active-directory-saas-policystat-tutorial/ic808633.png "Menú Administrator")</span><span class="sxs-lookup"><span data-stu-id="87370-191">![Administrator Menu](./media/active-directory-saas-policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

10. <span data-ttu-id="87370-192">Hola **el programa de instalación** sección, seleccione **integración de inicio de sesión único habilitar**.</span><span class="sxs-lookup"><span data-stu-id="87370-192">In hello **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="87370-193">![Configuración de inicio de sesión único](./media/active-directory-saas-policystat-tutorial/ic808634.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="87370-193">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

11. <span data-ttu-id="87370-194">Haga clic en **configurar los atributos de**y, a continuación, en hello **configurar los atributos** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="87370-194">Click **Configure Attributes**, and then, in hello **Configure Attributes** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="87370-195">![Configuración de inicio de sesión único](./media/active-directory-saas-policystat-tutorial/ic808635.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="87370-195">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="87370-196">a.</span><span class="sxs-lookup"><span data-stu-id="87370-196">a.</span></span> <span data-ttu-id="87370-197">Hola **atributo Username** cuadro de texto, tipo **uid**.</span><span class="sxs-lookup"><span data-stu-id="87370-197">In hello **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="87370-198">b.</span><span class="sxs-lookup"><span data-stu-id="87370-198">b.</span></span> <span data-ttu-id="87370-199">Hola **atributo de nombre** cuadro de texto, tipo **firstname** del usuario **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="87370-199">In hello **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="87370-200">c.</span><span class="sxs-lookup"><span data-stu-id="87370-200">c.</span></span> <span data-ttu-id="87370-201">Hola **último atributo de nombre** cuadro de texto, tipo **lastname** del usuario **Simon**.</span><span class="sxs-lookup"><span data-stu-id="87370-201">In hello **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="87370-202">d.</span><span class="sxs-lookup"><span data-stu-id="87370-202">d.</span></span> <span data-ttu-id="87370-203">Hola **atributo de correo electrónico** cuadro de texto, tipo **emailaddress** del usuario  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="87370-203">In hello **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="87370-204">e.</span><span class="sxs-lookup"><span data-stu-id="87370-204">e.</span></span> <span data-ttu-id="87370-205">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="87370-205">Click **Save Changes**.</span></span>

12. <span data-ttu-id="87370-206">Haga clic en **los metadatos de IDP**y, a continuación, en hello **los metadatos de IDP** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="87370-206">Click **Your IDP Metadata**, and then, in hello **Your IDP Metadata** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="87370-207">![Configuración de inicio de sesión único](./media/active-directory-saas-policystat-tutorial/ic808636.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="87370-207">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="87370-208">a.</span><span class="sxs-lookup"><span data-stu-id="87370-208">a.</span></span> <span data-ttu-id="87370-209">Abra el archivo de metadatos descargado, Hola copia contenido y, a continuación, péguelo en hello **los metadatos del proveedor de identidad** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="87370-209">Open your downloaded metadata file, copy hello content, and  then paste it into hello **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="87370-210">b.</span><span class="sxs-lookup"><span data-stu-id="87370-210">b.</span></span> <span data-ttu-id="87370-211">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="87370-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="87370-212">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="87370-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="87370-213">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="87370-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="87370-214">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="87370-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="87370-215">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="87370-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="87370-216">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="87370-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="87370-218">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="87370-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="87370-219">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="87370-219">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="87370-221">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="87370-221">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="87370-223">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="87370-223">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="87370-225">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="87370-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="87370-227">a.</span><span class="sxs-lookup"><span data-stu-id="87370-227">a.</span></span> <span data-ttu-id="87370-228">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="87370-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="87370-229">b.</span><span class="sxs-lookup"><span data-stu-id="87370-229">b.</span></span> <span data-ttu-id="87370-230">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="87370-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="87370-231">c.</span><span class="sxs-lookup"><span data-stu-id="87370-231">c.</span></span> <span data-ttu-id="87370-232">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="87370-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="87370-233">d.</span><span class="sxs-lookup"><span data-stu-id="87370-233">d.</span></span> <span data-ttu-id="87370-234">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="87370-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="87370-235">Creación de un usuario de prueba de PolicyStat</span><span class="sxs-lookup"><span data-stu-id="87370-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="87370-236">En orden tooenable toolog de los usuarios de Azure AD en PolicyStat, se les deben aprovisionar en PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="87370-236">In order tooenable Azure AD users toolog into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="87370-237">PolicyStat admite aprovisionamiento de usuarios justo a tiempo.</span><span class="sxs-lookup"><span data-stu-id="87370-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="87370-238">Esto significa, no es necesario a los usuarios de tooadd Hola manualmente tooPolicyStat.</span><span class="sxs-lookup"><span data-stu-id="87370-238">This means, you do not need tooadd hello users manually tooPolicyStat.</span></span> <span data-ttu-id="87370-239">los usuarios de Hola se agregarán automáticamente su primer inicio de sesión a través de SSO.</span><span class="sxs-lookup"><span data-stu-id="87370-239">hello users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="87370-240">Puede usar cualquier otra PolicyStat usuario cuenta herramienta de creación o las API proporcionadas por PolicyStat tooprovision cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87370-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="87370-241">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="87370-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="87370-242">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooPolicyStat.</span><span class="sxs-lookup"><span data-stu-id="87370-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPolicyStat.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="87370-244">**tooassign Britta Simon tooPolicyStat, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="87370-244">**tooassign Britta Simon tooPolicyStat, perform hello following steps:**</span></span>

1. <span data-ttu-id="87370-245">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="87370-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="87370-247">En la lista de aplicaciones de hello, seleccione **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="87370-247">In hello applications list, select **PolicyStat**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. <span data-ttu-id="87370-249">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="87370-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="87370-251">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="87370-251">Click **Add** button.</span></span> <span data-ttu-id="87370-252">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="87370-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="87370-254">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="87370-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="87370-255">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="87370-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="87370-256">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="87370-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="87370-257">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="87370-257">Testing single sign-on</span></span>

<span data-ttu-id="87370-258">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="87370-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="87370-259">Al hacer clic en icono de PolicyStat Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour PolicyStat aplicación.</span><span class="sxs-lookup"><span data-stu-id="87370-259">When you click hello PolicyStat tile in hello Access Panel, you should get automatically signed-on tooyour PolicyStat application.</span></span>
<span data-ttu-id="87370-260">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="87370-260">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="87370-261">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="87370-261">Additional resources</span></span>

* [<span data-ttu-id="87370-262">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87370-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="87370-263">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="87370-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

