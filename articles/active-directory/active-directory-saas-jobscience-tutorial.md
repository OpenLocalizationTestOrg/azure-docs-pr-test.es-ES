---
title: "Tutorial: Integración de Azure Active Directory con Jobscience | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Jobscience."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4a4c78aad6d324795a15a9569542afc23b4716d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="2ddd1-103">Tutorial: Integración de Azure Active Directory con Jobscience</span><span class="sxs-lookup"><span data-stu-id="2ddd1-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="2ddd1-104">En este tutorial, aprenderá cómo toointegrate Jobscience con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2ddd1-104">In this tutorial, you learn how toointegrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2ddd1-105">Integración Jobscience con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="2ddd1-105">Integrating Jobscience with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2ddd1-106">Puede controlar en Azure AD que tenga acceso tooJobscience</span><span class="sxs-lookup"><span data-stu-id="2ddd1-106">You can control in Azure AD who has access tooJobscience</span></span>
- <span data-ttu-id="2ddd1-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooJobscience (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ddd1-107">You can enable your users tooautomatically get signed-on tooJobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2ddd1-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="2ddd1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2ddd1-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2ddd1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ddd1-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2ddd1-110">Prerequisites</span></span>

<span data-ttu-id="2ddd1-111">integración de Azure AD con Jobscience tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2ddd1-111">tooconfigure Azure AD integration with Jobscience, you need hello following items:</span></span>

- <span data-ttu-id="2ddd1-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ddd1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2ddd1-113">Una suscripción habilitada para inicio de sesión único en Jobscience</span><span class="sxs-lookup"><span data-stu-id="2ddd1-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2ddd1-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2ddd1-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="2ddd1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2ddd1-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2ddd1-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2ddd1-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2ddd1-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="2ddd1-118">Scenario description</span></span>
<span data-ttu-id="2ddd1-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2ddd1-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="2ddd1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2ddd1-121">Agregar Jobscience desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="2ddd1-121">Adding Jobscience from hello gallery</span></span>
2. <span data-ttu-id="2ddd1-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ddd1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-hello-gallery"></a><span data-ttu-id="2ddd1-123">Agregar Jobscience desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="2ddd1-123">Adding Jobscience from hello gallery</span></span>
<span data-ttu-id="2ddd1-124">integración de hello tooconfigure de Jobscience en Azure AD, deberá tooadd Jobscience de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-124">tooconfigure hello integration of Jobscience into Azure AD, you need tooadd Jobscience from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2ddd1-125">**tooadd Jobscience de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2ddd1-125">**tooadd Jobscience from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ddd1-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2ddd1-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2ddd1-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="2ddd1-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="2ddd1-133">En el cuadro de búsqueda de hello, escriba **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-133">In hello search box, type **Jobscience**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="2ddd1-135">En el panel de resultados de hello, seleccione **Jobscience**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-135">In hello results panel, select **Jobscience**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2ddd1-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ddd1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2ddd1-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Jobscience con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2ddd1-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2ddd1-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Jobscience es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jobscience is tooa user in Azure AD.</span></span> <span data-ttu-id="2ddd1-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Jobscience debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-140">In other words, a link relationship between an Azure AD user and hello related user in Jobscience needs toobe established.</span></span>

<span data-ttu-id="2ddd1-141">En Jobscience, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-141">In Jobscience, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2ddd1-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Jobscience, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="2ddd1-142">tooconfigure and test Azure AD single sign-on with Jobscience, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2ddd1-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2ddd1-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2ddd1-145">**[Crear un usuario de prueba de Jobscience](#creating-a-jobscience-test-user)**  -toohave un equivalente de Britta Simon en Jobscience que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - toohave a counterpart of Britta Simon in Jobscience that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2ddd1-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2ddd1-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2ddd1-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ddd1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2ddd1-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Jobscience.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="2ddd1-150">**inicio de sesión único en tooconfigure Azure AD con Jobscience, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2ddd1-150">**tooconfigure Azure AD single sign-on with Jobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ddd1-151">En el portal de Azure, en Hola Hola **Jobscience** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-151">In hello Azure portal, on hello **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="2ddd1-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="2ddd1-155">En hello **Jobscience dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2ddd1-155">On hello **Jobscience Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="2ddd1-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="2ddd1-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="2ddd1-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-158">This value is not real.</span></span> <span data-ttu-id="2ddd1-159">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="2ddd1-160">Obtener este valor [equipo de soporte técnico de Jobscience cliente](https://www.jobscience.com/support) o del perfil SSO de hello creará que se explica más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from hello SSO profile you will create which is explained later in hello tutorial.</span></span> 
 
4. <span data-ttu-id="2ddd1-161">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="2ddd1-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="2ddd1-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2ddd1-165">En hello **configuración de Jobscience** sección, haga clic en **configurar Jobscience** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-165">On hello **Jobscience Configuration** section, click **Configure Jobscience** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2ddd1-166">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="2ddd1-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="2ddd1-168">Inicie sesión en tooyour sitio de la compañía Jobscience como administrador.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-168">Log in tooyour Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="2ddd1-169">Vaya demasiado**el programa de instalación**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-169">Go too**Setup**.</span></span>
   
   <span data-ttu-id="2ddd1-170">![Instalación](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Instalación")</span><span class="sxs-lookup"><span data-stu-id="2ddd1-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="2ddd1-171">En el panel de navegación izquierdo de hello, Hola **administrar** sección, haga clic en **Domain Management** tooexpand Hola sección relacionada y, a continuación, haga clic en **mi dominio** tooopen hello  **Mi dominio** página.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
   <span data-ttu-id="2ddd1-172">![Mi dominio](./media/active-directory-saas-jobscience-tutorial/ic767825.png "Mi dominio")</span><span class="sxs-lookup"><span data-stu-id="2ddd1-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="2ddd1-173">tooverify que el dominio se ha configurado correctamente, asegúrese de que se encuentra en "**paso 4 implementado tooUsers**" y revise el "**mi configuración de dominio**".</span><span class="sxs-lookup"><span data-stu-id="2ddd1-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="2ddd1-174">![Dominio implementado tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "tooUser implementadas de dominio")</span><span class="sxs-lookup"><span data-stu-id="2ddd1-174">![Domain Deployed tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="2ddd1-175">En el sitio de la compañía de Jobscience hello, haga clic en **controles de seguridad**y, a continuación, haga clic en **configuración de inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-175">On hello Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="2ddd1-176">![Controles de seguridad](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Controles de seguridad")</span><span class="sxs-lookup"><span data-stu-id="2ddd1-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="2ddd1-177">Hola **configuración de inicio de sesión único** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2ddd1-177">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="2ddd1-178">![Configuración de inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="2ddd1-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="2ddd1-179">a.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-179">a.</span></span> <span data-ttu-id="2ddd1-180">Seleccione **SAML habilitado**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="2ddd1-181">b.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-181">b.</span></span> <span data-ttu-id="2ddd1-182">Haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-182">Click **New**.</span></span>

13. <span data-ttu-id="2ddd1-183">En hello **SAML Single Sign-On editar la configuración de** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2ddd1-183">On hello **SAML Single Sign-On Setting Edit** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="2ddd1-184">![Inicio de sesión único SAML](./media/active-directory-saas-jobscience-tutorial/ic784365.png "Inicio de sesión único SAML")</span><span class="sxs-lookup"><span data-stu-id="2ddd1-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="2ddd1-185">a.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-185">a.</span></span> <span data-ttu-id="2ddd1-186">Hola **nombre** cuadro de texto, escriba un nombre para la configuración.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-186">In hello **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="2ddd1-187">b.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-187">b.</span></span> <span data-ttu-id="2ddd1-188">En **emisor** cuadro de texto, pegue Hola valo **Id. de entidad SAML**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-188">In **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2ddd1-189">c.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-189">c.</span></span> <span data-ttu-id="2ddd1-190">Hola **Id. de entidad** cuadro de texto, tipo`https://salesforce-jobscience.com`</span><span class="sxs-lookup"><span data-stu-id="2ddd1-190">In hello **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="2ddd1-191">d.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-191">d.</span></span> <span data-ttu-id="2ddd1-192">Haga clic en **examinar** tooupload su certificado de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-192">Click **Browse** tooupload your Azure AD certificate.</span></span>

    <span data-ttu-id="2ddd1-193">e.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-193">e.</span></span> <span data-ttu-id="2ddd1-194">Como **tipo de identidad SAML**, seleccione **la aserción contiene Hola Id. de federación del objeto de usuario de hello**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-194">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>

    <span data-ttu-id="2ddd1-195">f.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-195">f.</span></span> <span data-ttu-id="2ddd1-196">Como **ubicación de identidad SAML**, seleccione **identidad está en el elemento NameIdentifier de Hola de hello instrucción Subject**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-196">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>

    <span data-ttu-id="2ddd1-197">g.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-197">g.</span></span> <span data-ttu-id="2ddd1-198">En **URL de inicio de sesión del proveedor de identidades** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-198">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2ddd1-199">h.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-199">h.</span></span> <span data-ttu-id="2ddd1-200">En **URL de cierre de sesión del proveedor de identidades** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-200">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2ddd1-201">i.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-201">i.</span></span> <span data-ttu-id="2ddd1-202">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-202">Click **Save**.</span></span>

14. <span data-ttu-id="2ddd1-203">En el panel de navegación izquierdo de hello, Hola **administrar** sección, haga clic en **Domain Management** tooexpand Hola sección relacionada y, a continuación, haga clic en **mi dominio** tooopen hello  **Mi dominio** página.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-203">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="2ddd1-204">![Mi dominio](./media/active-directory-saas-jobscience-tutorial/ic767825.png "Mi dominio")</span><span class="sxs-lookup"><span data-stu-id="2ddd1-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="2ddd1-205">En hello **mi dominio** página Hola **personalización de la página de inicio de sesión** sección, haga clic en **editar**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-205">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="2ddd1-206">![Personalización de marca de página de inicio de sesión](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Personalización de marca de página de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="2ddd1-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="2ddd1-207">En hello **personalización de la página de inicio de sesión** página Hola **servicio de autenticación** sección, el nombre de Hola de su **configuración de SSO de SAML** se muestra.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-207">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="2ddd1-208">Selecciónelo y luego haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="2ddd1-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="2ddd1-209">![Personalización de marca de página de inicio de sesión](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Personalización de marca de página de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="2ddd1-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="2ddd1-210">Hola tooget SP iniciado por el inicio de sesión único en la dirección URL de inicio de sesión, haga clic en hello **configuración de inicio de sesión único** en hello **controles de seguridad** sección de menú.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-210">tooget hello SP initiated Single Sign on Login URL click on hello **Single Sign On settings** in hello **Security Controls** menu section.</span></span>

    <span data-ttu-id="2ddd1-211">![Controles de seguridad](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Controles de seguridad")</span><span class="sxs-lookup"><span data-stu-id="2ddd1-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="2ddd1-212">Haga clic en el perfil SSO de Hola que haya creado en el paso de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-212">Click hello SSO profile you have created in hello step above.</span></span> <span data-ttu-id="2ddd1-213">Esta página muestra hello inicio de sesión único en la dirección URL de su empresa (por ejemplo, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span><span class="sxs-lookup"><span data-stu-id="2ddd1-213">This page shows hello Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="2ddd1-214">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="2ddd1-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2ddd1-215">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2ddd1-216">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2ddd1-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2ddd1-217">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ddd1-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="2ddd1-218">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="2ddd1-220">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2ddd1-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ddd1-221">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2ddd1-223">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2ddd1-225">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2ddd1-227">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="2ddd1-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2ddd1-229">a.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-229">a.</span></span> <span data-ttu-id="2ddd1-230">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2ddd1-231">b.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-231">b.</span></span> <span data-ttu-id="2ddd1-232">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2ddd1-233">c.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-233">c.</span></span> <span data-ttu-id="2ddd1-234">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2ddd1-235">d.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-235">d.</span></span> <span data-ttu-id="2ddd1-236">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="2ddd1-237">Creación de un usuario de prueba de Jobscience</span><span class="sxs-lookup"><span data-stu-id="2ddd1-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="2ddd1-238">En orden tooenable toolog de los usuarios de Azure AD en tooJobscience, se les deben aprovisionar en Jobscience.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-238">In order tooenable Azure AD users toolog in tooJobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="2ddd1-239">En caso de hello de Jobscience, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-239">In hello case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="2ddd1-240">Puede usar cualquier otra Jobscience usuario cuenta herramienta de creación o las API proporcionadas por Jobscience tooprovision Azure Active Directory las cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience tooprovision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="2ddd1-241">**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2ddd1-241">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ddd1-242">Inicie sesión en tooyour **Jobscience** como administrador.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-242">Log in tooyour **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="2ddd1-243">Vaya tooSetup.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-243">Go tooSetup.</span></span>
   
   <span data-ttu-id="2ddd1-244">![Instalación](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Instalación")</span><span class="sxs-lookup"><span data-stu-id="2ddd1-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="2ddd1-245">Vaya demasiado**administrar usuarios \> usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-245">Go too**Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="2ddd1-246">![Usuarios](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="2ddd1-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="2ddd1-247">Haga clic en **Nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-247">Click **New User**.</span></span>
   
   <span data-ttu-id="2ddd1-248">![Todos los usuarios](./media/active-directory-saas-jobscience-tutorial/ic784370.png "Todos los usuarios")</span><span class="sxs-lookup"><span data-stu-id="2ddd1-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="2ddd1-249">En hello **Editar usuario** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2ddd1-249">On hello **Edit User** dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="2ddd1-250">![Edición de usuario](./media/active-directory-saas-jobscience-tutorial/ic784371.png "Edición de usuario")</span><span class="sxs-lookup"><span data-stu-id="2ddd1-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="2ddd1-251">a.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-251">a.</span></span> <span data-ttu-id="2ddd1-252">Hola **nombre** cuadro de texto, escriba un nombre de usuario de hello como Bárbara.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-252">In hello **First Name** textbox, type a first name of hello user like Britta.</span></span>
   
   <span data-ttu-id="2ddd1-253">b.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-253">b.</span></span> <span data-ttu-id="2ddd1-254">Hola **Last Name** cuadro de texto, escriba los apellidos del usuario de hello como Simon.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-254">In hello **Last Name** textbox, type a last name of hello user like Simon.</span></span>
   
   <span data-ttu-id="2ddd1-255">c.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-255">c.</span></span> <span data-ttu-id="2ddd1-256">Hola **Alias** cuadro de texto, escriba un nombre de alias de usuario de hello como brittas.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-256">In hello **Alias** textbox, type an alias name of hello user like brittas.</span></span>

   <span data-ttu-id="2ddd1-257">d.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-257">d.</span></span> <span data-ttu-id="2ddd1-258">Hola **correo electrónico** tipo hello dirección de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-258">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="2ddd1-259">e.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-259">e.</span></span> <span data-ttu-id="2ddd1-260">Hola **nombre de usuario** cuadro de texto, escriba un nombre de usuario del usuario como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-260">In hello **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="2ddd1-261">f.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-261">f.</span></span> <span data-ttu-id="2ddd1-262">Hola **nombre Nick** cuadro de texto, escriba un nombre de nick del usuario como Simon.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-262">In hello **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="2ddd1-263">g.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-263">g.</span></span> <span data-ttu-id="2ddd1-264">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="2ddd1-265">titular de la cuenta de Hello Azure Active Directory recibe un correo electrónico y sigue un vínculo tooconfirm su cuenta antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-265">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2ddd1-266">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ddd1-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2ddd1-267">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooJobscience.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJobscience.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="2ddd1-269">**tooassign Britta Simon tooJobscience, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2ddd1-269">**tooassign Britta Simon tooJobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ddd1-270">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="2ddd1-272">En la lista de aplicaciones de hello, seleccione **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-272">In hello applications list, select **Jobscience**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="2ddd1-274">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="2ddd1-276">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-276">Click **Add** button.</span></span> <span data-ttu-id="2ddd1-277">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="2ddd1-279">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2ddd1-280">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2ddd1-281">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2ddd1-282">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="2ddd1-282">Testing single sign-on</span></span>

<span data-ttu-id="2ddd1-283">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2ddd1-284">Al hacer clic en icono de Jobscience Hola Hola Panel de acceso, deberá obtener aplicaciones de Jobscience tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="2ddd1-284">When you click hello Jobscience tile in hello Access Panel, you should get automatically signed-on tooyour Jobscience application.</span></span>
<span data-ttu-id="2ddd1-285">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2ddd1-285">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2ddd1-286">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2ddd1-286">Additional resources</span></span>

* [<span data-ttu-id="2ddd1-287">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ddd1-287">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2ddd1-288">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2ddd1-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

