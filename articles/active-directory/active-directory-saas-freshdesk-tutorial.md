---
title: "Tutorial: Integración de Azure Active Directory con Freshdesk | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y FreshDesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="eeb89-103">Tutorial: Integración de Azure Active Directory con Freshdesk</span><span class="sxs-lookup"><span data-stu-id="eeb89-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="eeb89-104">En este tutorial, aprenderá cómo toointegrate FreshDesk con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eeb89-104">In this tutorial, you learn how toointegrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eeb89-105">Integración FreshDesk con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="eeb89-105">Integrating FreshDesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eeb89-106">Puede controlar en Azure AD que tenga acceso tooFreshDesk</span><span class="sxs-lookup"><span data-stu-id="eeb89-106">You can control in Azure AD who has access tooFreshDesk</span></span>
- <span data-ttu-id="eeb89-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooFreshDesk (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eeb89-107">You can enable your users tooautomatically get signed-on tooFreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eeb89-108">Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="eeb89-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="eeb89-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eeb89-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eeb89-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="eeb89-110">Prerequisites</span></span>

<span data-ttu-id="eeb89-111">integración de Azure AD con FreshDesk tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="eeb89-111">tooconfigure Azure AD integration with FreshDesk, you need hello following items:</span></span>

- <span data-ttu-id="eeb89-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eeb89-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eeb89-113">Una suscripción habilitada para el inicio de sesión único en FreshDesk</span><span class="sxs-lookup"><span data-stu-id="eeb89-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eeb89-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="eeb89-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eeb89-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="eeb89-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eeb89-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="eeb89-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="eeb89-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eeb89-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eeb89-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="eeb89-118">Scenario description</span></span>
<span data-ttu-id="eeb89-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="eeb89-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eeb89-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="eeb89-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eeb89-121">Agregar FreshDesk desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="eeb89-121">Adding FreshDesk from hello gallery</span></span>
2. <span data-ttu-id="eeb89-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eeb89-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-hello-gallery"></a><span data-ttu-id="eeb89-123">Agregar FreshDesk desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="eeb89-123">Adding FreshDesk from hello gallery</span></span>
<span data-ttu-id="eeb89-124">integración de hello tooconfigure de FreshDesk en Azure AD, deberá tooadd FreshDesk de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="eeb89-124">tooconfigure hello integration of FreshDesk into Azure AD, you need tooadd FreshDesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eeb89-125">**tooadd FreshDesk de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="eeb89-125">**tooadd FreshDesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eeb89-126">Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="eeb89-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eeb89-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eeb89-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="eeb89-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="eeb89-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="eeb89-133">En el cuadro de búsqueda de hello, escriba **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-133">In hello search box, type **FreshDesk**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="eeb89-135">En el panel de resultados de hello, seleccione **FreshDesk**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="eeb89-135">In hello results panel, select **FreshDesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eeb89-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eeb89-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eeb89-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con FreshDesk con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="eeb89-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eeb89-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en FreshDesk es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eeb89-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FreshDesk is tooa user in Azure AD.</span></span> <span data-ttu-id="eeb89-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en FreshDesk debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="eeb89-140">In other words, a link relationship between an Azure AD user and hello related user in FreshDesk needs toobe established.</span></span>

<span data-ttu-id="eeb89-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="eeb89-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FreshDesk.</span></span>

<span data-ttu-id="eeb89-142">tooconfigure y prueba de inicio de sesión único en Azure AD con FreshDesk, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="eeb89-142">tooconfigure and test Azure AD single sign-on with FreshDesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eeb89-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="eeb89-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eeb89-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eeb89-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eeb89-145">**[Crear un usuario de prueba de FreshDesk](#creating-a-freshdesk-test-user)**  -toohave un equivalente de Britta Simon en FreshDesk que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="eeb89-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - toohave a counterpart of Britta Simon in FreshDesk that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="eeb89-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="eeb89-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eeb89-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="eeb89-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eeb89-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eeb89-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eeb89-149">En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación Freshservice.</span><span class="sxs-lookup"><span data-stu-id="eeb89-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="eeb89-150">**inicio de sesión único en tooconfigure Azure AD con FreshDesk, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="eeb89-150">**tooconfigure Azure AD single sign-on with FreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="eeb89-151">En el portal de administración de Azure de hello, en hello **FreshDesk** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-151">In hello Azure Management portal, on hello **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="eeb89-153">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="eeb89-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="eeb89-155">En hello **FreshDesk dominio y las direcciones URL** sección, escriba Hola **dirección URL de inicio de sesión** como: `https://<tenant-name>.freshdesk.com` o cualquier otro valor que le sugiere Freshdesk.</span><span class="sxs-lookup"><span data-stu-id="eeb89-155">On hello **FreshDesk Domain and URLs** section, please enter hello **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="eeb89-157">Tenga en cuenta que este no es el valor real.</span><span class="sxs-lookup"><span data-stu-id="eeb89-157">Please note that this is not the real value.</span></span> <span data-ttu-id="eeb89-158">Tiene que actualizar este valor con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="eeb89-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="eeb89-159">Póngase en contacto con el [equipo de soporte técnico de FreshDesk](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="eeb89-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="eeb89-160">En hello **el certificado de firma de SAML** sección, haga clic en **certificado** y, a continuación, guarde el certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="eeb89-160">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="eeb89-162">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="eeb89-162">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eeb89-164">En hello **configuración de FreshDesk** sección, haga clic en **FreshDesk configurar** ventana tooopen configurar inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="eeb89-164">On hello **FreshDesk Configuration** section, click **Configure FreshDesk** tooopen Configure sign-on window.</span></span> <span data-ttu-id="eeb89-165">Copiar Hola SAML Single Sign-On dirección URL del servicio y la dirección URL de cierre de sesión de hello **referencia rápida** sección.</span><span class="sxs-lookup"><span data-stu-id="eeb89-165">Copy hello SAML Single Sign-On Service URL and Sign-Out URL from hello **Quick Reference** section.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="eeb89-167">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de Freshdesk como administrador.</span><span class="sxs-lookup"><span data-stu-id="eeb89-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="eeb89-168">En el menú de hello en la parte superior de hello, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-168">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="eeb89-169">![Administración](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="eeb89-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="eeb89-170">Hola **configuración General** , haga clic en **seguridad**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-170">In hello **General Settings** tab, click **Security**.</span></span>
   
   <span data-ttu-id="eeb89-171">![Seguridad](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Seguridad")</span><span class="sxs-lookup"><span data-stu-id="eeb89-171">![Security](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="eeb89-172">Hola **seguridad** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="eeb89-172">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="eeb89-173">![Inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="eeb89-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="eeb89-174">a.</span><span class="sxs-lookup"><span data-stu-id="eeb89-174">a.</span></span> <span data-ttu-id="eeb89-175">En **Inicio de sesión único (SSO)**, seleccione **Activado**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="eeb89-176">b.</span><span class="sxs-lookup"><span data-stu-id="eeb89-176">b.</span></span> <span data-ttu-id="eeb89-177">Seleccione **Inicio de sesión único de SAML**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="eeb89-178">c.</span><span class="sxs-lookup"><span data-stu-id="eeb89-178">c.</span></span> <span data-ttu-id="eeb89-179">Hola de tipo **SAML Single Sign-On dirección URL del servicio** copió desde el portal de Azure en hello **dirección URL de inicio de sesión de SAML** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="eeb89-179">Type hello **SAML Single Sign-On Service URL** you copied from Azure portal into hello **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="eeb89-180">d.</span><span class="sxs-lookup"><span data-stu-id="eeb89-180">d.</span></span> <span data-ttu-id="eeb89-181">Hola de tipo **dirección URL de cierre de sesión** copió desde el portal de Azure en hello **Logout URL** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="eeb89-181">Type hello **Sign-Out URL**  you copied from Azure portal into hello **Logout URL** textbox.</span></span>

    <span data-ttu-id="eeb89-182">e.</span><span class="sxs-lookup"><span data-stu-id="eeb89-182">e.</span></span> <span data-ttu-id="eeb89-183">Hola copia **huella digital** valor de certificado de hello descargado del portal de Azure y péguelo en hello **huella digital de certificado de seguridad** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="eeb89-183">Copy hello **Thumbprint** value from hello downloaded certificate from Azure portal and paste it into hello **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="eeb89-184">Para obtener más información, consulte [cómo tooretrieve valor de huella digital del certificado](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="eeb89-184">For more details, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="eeb89-185">f.</span><span class="sxs-lookup"><span data-stu-id="eeb89-185">f.</span></span> <span data-ttu-id="eeb89-186">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eeb89-187">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eeb89-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="eeb89-188">objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="eeb89-188">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="eeb89-190">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="eeb89-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eeb89-191">Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="eeb89-191">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eeb89-193">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="eeb89-193">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eeb89-195">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eeb89-195">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eeb89-197">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="eeb89-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eeb89-199">a.</span><span class="sxs-lookup"><span data-stu-id="eeb89-199">a.</span></span> <span data-ttu-id="eeb89-200">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eeb89-201">b.</span><span class="sxs-lookup"><span data-stu-id="eeb89-201">b.</span></span> <span data-ttu-id="eeb89-202">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eeb89-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eeb89-203">c.</span><span class="sxs-lookup"><span data-stu-id="eeb89-203">c.</span></span> <span data-ttu-id="eeb89-204">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eeb89-205">d.</span><span class="sxs-lookup"><span data-stu-id="eeb89-205">d.</span></span> <span data-ttu-id="eeb89-206">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="eeb89-207">Creación de un usuario de prueba de FreshDesk</span><span class="sxs-lookup"><span data-stu-id="eeb89-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="eeb89-208">En orden tooenable toolog de los usuarios de Azure AD en FreshDesk, se les deben aprovisionar en FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="eeb89-208">In order tooenable Azure AD users toolog into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="eeb89-209">En caso de hello de FreshDesk, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="eeb89-209">In hello case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="eeb89-210">**tooprovision una cuenta de usuario, realizar Hola lo siguiente:**</span><span class="sxs-lookup"><span data-stu-id="eeb89-210">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="eeb89-211">Inicie sesión en tooyour **Freshdesk** inquilino.</span><span class="sxs-lookup"><span data-stu-id="eeb89-211">Log in tooyour **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="eeb89-212">En el menú de hello en la parte superior de hello, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-212">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="eeb89-213">![Administración](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="eeb89-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="eeb89-214">Hola **configuración General** , haga clic en **agentes**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-214">In hello **General Settings** tab, click **Agents**.</span></span>
   
   <span data-ttu-id="eeb89-215">![Agentes](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agentes")</span><span class="sxs-lookup"><span data-stu-id="eeb89-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="eeb89-216">Haga clic en **Nuevo agente**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="eeb89-217">![Nuevo agente](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "Nuevo agente")</span><span class="sxs-lookup"><span data-stu-id="eeb89-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="eeb89-218">En el cuadro de diálogo de información de agentes de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="eeb89-218">On hello Agent Information dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="eeb89-219">![Información sobre agentes](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Información sobre agentes")</span><span class="sxs-lookup"><span data-stu-id="eeb89-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
   <span data-ttu-id="eeb89-220">a.</span><span class="sxs-lookup"><span data-stu-id="eeb89-220">a.</span></span> <span data-ttu-id="eeb89-221">Hola **nombre completo** cuadro de texto, nombre de cuenta de hello Azure AD que desee tooprovision Hola de tipo.</span><span class="sxs-lookup"><span data-stu-id="eeb89-221">In hello **Full Name** textbox, type hello name of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="eeb89-222">b.</span><span class="sxs-lookup"><span data-stu-id="eeb89-222">b.</span></span> <span data-ttu-id="eeb89-223">Hola **correo electrónico** cuadro de texto, hello Azure AD de tipo dirección de correo electrónico de cuenta de hello Azure AD que desea tooprovision.</span><span class="sxs-lookup"><span data-stu-id="eeb89-223">In hello **Email** textbox, type hello Azure AD email address of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="eeb89-224">c.</span><span class="sxs-lookup"><span data-stu-id="eeb89-224">c.</span></span> <span data-ttu-id="eeb89-225">Hola **título** cuadro de texto, escriba el título de cuenta de hello Azure AD que desea tooprovision Hola.</span><span class="sxs-lookup"><span data-stu-id="eeb89-225">In hello **Title** textbox, type hello title of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="eeb89-226">d.</span><span class="sxs-lookup"><span data-stu-id="eeb89-226">d.</span></span> <span data-ttu-id="eeb89-227">Seleccione **Agents role** (Rol de agentes) y luego haga clic en **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-227">Select **Agents role**, and then click **Assign**.</span></span>
       
   <span data-ttu-id="eeb89-228">e.</span><span class="sxs-lookup"><span data-stu-id="eeb89-228">e.</span></span> <span data-ttu-id="eeb89-229">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="eeb89-230">titular de cuenta de Hello Azure AD recibirá un correo electrónico que incluye una cuenta de hello tooconfirm vínculo antes de activarse.</span><span class="sxs-lookup"><span data-stu-id="eeb89-230">hello Azure AD account holder will get an email that includes a link tooconfirm hello account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="eeb89-231">Puede usar cualquier otra Freshdesk usuario cuenta herramienta de creación o las API proporcionadas por Freshdesk tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="eeb89-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk tooprovision AAD user accounts.</span></span> <span data-ttu-id="eeb89-232">tooFreshDesk.</span><span class="sxs-lookup"><span data-stu-id="eeb89-232">tooFreshDesk.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eeb89-233">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="eeb89-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eeb89-234">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su cuadro de herramientas de acceso.</span><span class="sxs-lookup"><span data-stu-id="eeb89-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooBox.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="eeb89-236">**tooassign Britta Simon tooFreshDesk, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="eeb89-236">**tooassign Britta Simon tooFreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="eeb89-237">En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-237">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="eeb89-239">En la lista de aplicaciones de hello, seleccione **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-239">In hello applications list, select **FreshDesk**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="eeb89-241">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="eeb89-243">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-243">Click **Add** button.</span></span> <span data-ttu-id="eeb89-244">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="eeb89-246">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="eeb89-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eeb89-247">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eeb89-248">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eeb89-249">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="eeb89-249">Testing single sign-on</span></span>

<span data-ttu-id="eeb89-250">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="eeb89-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="eeb89-251">Al hacer clic en icono de FreshDesk Hola Hola Panel de acceso, deberá obtener inicio de sesión página tooget ha iniciado sesión tooyour aplicación Freshservice.</span><span class="sxs-lookup"><span data-stu-id="eeb89-251">When you click hello FreshDesk tile in hello Access Panel, you should get login page tooget signed-on tooyour FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eeb89-252">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="eeb89-252">Additional resources</span></span>

* [<span data-ttu-id="eeb89-253">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eeb89-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eeb89-254">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eeb89-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

