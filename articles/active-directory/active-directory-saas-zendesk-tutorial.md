---
title: "Tutorial: Integración de Azure Active Directory con Zendesk | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Zendesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 46ccd57a4adeb810af459caaa1e592cf2b62cb8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="404f6-103">Tutorial: Integración de Azure Active Directory con Zendesk</span><span class="sxs-lookup"><span data-stu-id="404f6-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="404f6-104">En este tutorial, aprenderá cómo toointegrate Zendesk con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="404f6-104">In this tutorial, you learn how toointegrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="404f6-105">Integración de Zendesk con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="404f6-105">Integrating Zendesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="404f6-106">Puede controlar en Azure AD que tenga acceso tooZendesk</span><span class="sxs-lookup"><span data-stu-id="404f6-106">You can control in Azure AD who has access tooZendesk</span></span>
- <span data-ttu-id="404f6-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooZendesk (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="404f6-107">You can enable your users tooautomatically get signed-on tooZendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="404f6-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="404f6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="404f6-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="404f6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="404f6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="404f6-110">Prerequisites</span></span>

<span data-ttu-id="404f6-111">integración de Azure AD con Zendesk tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="404f6-111">tooconfigure Azure AD integration with Zendesk, you need hello following items:</span></span>

- <span data-ttu-id="404f6-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="404f6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="404f6-113">Una suscripción habilitada para el inicio de sesión único en Zendesk</span><span class="sxs-lookup"><span data-stu-id="404f6-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="404f6-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="404f6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="404f6-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="404f6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="404f6-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="404f6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="404f6-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="404f6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="404f6-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="404f6-118">Scenario description</span></span>
<span data-ttu-id="404f6-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="404f6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="404f6-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="404f6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="404f6-121">Agregar Zendesk desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="404f6-121">Adding Zendesk from hello gallery</span></span>
2. <span data-ttu-id="404f6-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="404f6-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-hello-gallery"></a><span data-ttu-id="404f6-123">Agregar Zendesk desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="404f6-123">Adding Zendesk from hello gallery</span></span>
<span data-ttu-id="404f6-124">integración de hello tooconfigure de Zendesk en Azure AD, deberá tooadd Zendesk de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="404f6-124">tooconfigure hello integration of Zendesk into Azure AD, you need tooadd Zendesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="404f6-125">**tooadd Zendesk de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="404f6-125">**tooadd Zendesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="404f6-126">Hola  **[Portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="404f6-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="404f6-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="404f6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="404f6-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="404f6-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="404f6-131">Haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="404f6-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="404f6-133">En el cuadro de búsqueda de hello, escriba **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="404f6-133">In hello search box, type **Zendesk**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="404f6-135">En el panel de resultados de hello, seleccione **Zendesk**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="404f6-135">In hello results panel, select **Zendesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="404f6-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="404f6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="404f6-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Zendesk con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="404f6-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="404f6-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Zendesk es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="404f6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zendesk is tooa user in Azure AD.</span></span> <span data-ttu-id="404f6-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Zendesk debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="404f6-140">In other words, a link relationship between an Azure AD user and hello related user in Zendesk needs toobe established.</span></span>

<span data-ttu-id="404f6-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Zendesk.</span><span class="sxs-lookup"><span data-stu-id="404f6-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zendesk.</span></span>

<span data-ttu-id="404f6-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Zendesk, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="404f6-142">tooconfigure and test Azure AD single sign-on with Zendesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="404f6-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="404f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="404f6-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="404f6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="404f6-145">**[Crear un usuario de prueba de Zendesk](#creating-a-zendesk-test-user)**  -toohave un equivalente de Britta Simon en Zendesk que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="404f6-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - toohave a counterpart of Britta Simon in Zendesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="404f6-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="404f6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="404f6-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="404f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="404f6-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="404f6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="404f6-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Zendesk.</span><span class="sxs-lookup"><span data-stu-id="404f6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="404f6-150">**inicio de sesión único en tooconfigure Azure AD con Zendesk, realice Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="404f6-150">**tooconfigure Azure AD single sign-on with Zendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="404f6-151">En el portal de Azure, en Hola Hola **Zendesk** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="404f6-151">In hello Azure portal, on hello **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="404f6-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="404f6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="404f6-155">En hello **Zendesk dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="404f6-155">On hello **Zendesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="404f6-157">a.</span><span class="sxs-lookup"><span data-stu-id="404f6-157">a.</span></span> <span data-ttu-id="404f6-158">Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello mediante Hola sigue el patrón:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="404f6-158">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="404f6-159">b.</span><span class="sxs-lookup"><span data-stu-id="404f6-159">b.</span></span> <span data-ttu-id="404f6-160">Hola **identificador** cuadro de texto, valor de tipo hello mediante Hola sigue el patrón:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="404f6-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="404f6-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="404f6-161">These values are not real.</span></span> <span data-ttu-id="404f6-162">Actualizar estos valores con la URL de inicio de sesión real de Hola y dirección URL de identificación.</span><span class="sxs-lookup"><span data-stu-id="404f6-162">Update these values with hello actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="404f6-163">Póngase en contacto con [equipo de soporte técnico de Zendesk](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="404f6-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget these values.</span></span> 

4. <span data-ttu-id="404f6-164">Zendesk espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="404f6-164">Zendesk expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="404f6-165">No hay ningún atributo SAML obligatorio, pero si lo desea puede agregar un atributo de **atributos de usuario** sección por hello siguiente pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="404f6-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following hello below steps:</span></span> 

     ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="404f6-167">a.</span><span class="sxs-lookup"><span data-stu-id="404f6-167">a.</span></span> <span data-ttu-id="404f6-168">Haga clic en hello **ver y editar Hola otros atributos** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="404f6-168">Click hello **View and edit all hello other attributes** check box.</span></span>
     
    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="404f6-170">b.</span><span class="sxs-lookup"><span data-stu-id="404f6-170">b.</span></span> <span data-ttu-id="404f6-171">Haga clic en hello **Agregar atributo** tooopen **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="404f6-171">Click hello **Add Attribute** tooopen **Add attribute** dialog.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="404f6-173">c.</span><span class="sxs-lookup"><span data-stu-id="404f6-173">c.</span></span> <span data-ttu-id="404f6-174">Hola **nombre** cuadro de texto, el nombre del atributo de tipo hello (por ejemplo **emailaddress**).</span><span class="sxs-lookup"><span data-stu-id="404f6-174">In hello **Name** textbox, type hello attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="404f6-175">d.</span><span class="sxs-lookup"><span data-stu-id="404f6-175">d.</span></span> <span data-ttu-id="404f6-176">De hello **valor** lista, el valor del atributo de hello seleccione (como **user.mail**).</span><span class="sxs-lookup"><span data-stu-id="404f6-176">From hello **Value** list, select hello attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="404f6-177">e.</span><span class="sxs-lookup"><span data-stu-id="404f6-177">e.</span></span> <span data-ttu-id="404f6-178">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="404f6-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="404f6-179">Usar atributos de tooadd de atributos de extensión que no están en Azure AD de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="404f6-179">You use extension attributes tooadd attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="404f6-180">Haga clic en [atributos de usuario que se pueden establecer en SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget Hola completa lista de SAML atributos que **Zendesk** acepta.</span><span class="sxs-lookup"><span data-stu-id="404f6-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="404f6-181">En hello **el certificado de firma de SAML** Hola de copia, en una sección **huella digital** el valor de certificado.</span><span class="sxs-lookup"><span data-stu-id="404f6-181">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="404f6-183">En hello **configuración de Zendesk** sección, haga clic en **configurar Zendesk** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="404f6-183">On hello **Zendesk Configuration** section, click **Configure Zendesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="404f6-184">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="404f6-184">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="404f6-186">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de Zendesk como administrador.</span><span class="sxs-lookup"><span data-stu-id="404f6-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="404f6-187">Haga clic en **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="404f6-187">Click **Admin**.</span></span>

9. <span data-ttu-id="404f6-188">En el panel de navegación izquierdo de hello, haga clic en **configuración**y, a continuación, haga clic en **seguridad**.</span><span class="sxs-lookup"><span data-stu-id="404f6-188">In hello left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="404f6-189">En hello **seguridad** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="404f6-189">On hello **Security** page, perform hello following steps:</span></span> 
   
     <span data-ttu-id="404f6-190">![Seguridad](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Seguridad")</span><span class="sxs-lookup"><span data-stu-id="404f6-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="404f6-191">![Inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="404f6-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="404f6-192">a.</span><span class="sxs-lookup"><span data-stu-id="404f6-192">a.</span></span> <span data-ttu-id="404f6-193">Haga clic en hello **Admin & agentes** ficha.</span><span class="sxs-lookup"><span data-stu-id="404f6-193">Click hello **Admin & Agents** tab.</span></span>

     <span data-ttu-id="404f6-194">b.</span><span class="sxs-lookup"><span data-stu-id="404f6-194">b.</span></span> <span data-ttu-id="404f6-195">Seleccione **Single sign-on (SSO) and SAML** (Inicio de sesión único (SSO) y SAML) y, luego, seleccione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="404f6-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="404f6-196">c.</span><span class="sxs-lookup"><span data-stu-id="404f6-196">c.</span></span> <span data-ttu-id="404f6-197">En **dirección URL SSO SAML** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="404f6-197">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="404f6-198">d.</span><span class="sxs-lookup"><span data-stu-id="404f6-198">d.</span></span> <span data-ttu-id="404f6-199">En **dirección URL de cierre de sesión remoto** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="404f6-199">In **Remote Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="404f6-200">e.</span><span class="sxs-lookup"><span data-stu-id="404f6-200">e.</span></span> <span data-ttu-id="404f6-201">En **huella digital de certificado** cuadro de texto, pegue hello **huella digital** el valor de certificado que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="404f6-201">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="404f6-202">f.</span><span class="sxs-lookup"><span data-stu-id="404f6-202">f.</span></span> <span data-ttu-id="404f6-203">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="404f6-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="404f6-204">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="404f6-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="404f6-205">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="404f6-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="404f6-207">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="404f6-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="404f6-208">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="404f6-208">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="404f6-210">lista de hello toodisplay de usuarios vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="404f6-210">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="404f6-212">En la parte superior de saludo del cuadro de diálogo de hello, haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="404f6-212">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="404f6-214">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="404f6-214">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="404f6-216">a.</span><span class="sxs-lookup"><span data-stu-id="404f6-216">a.</span></span> <span data-ttu-id="404f6-217">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="404f6-217">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="404f6-218">b.</span><span class="sxs-lookup"><span data-stu-id="404f6-218">b.</span></span> <span data-ttu-id="404f6-219">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="404f6-219">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="404f6-220">c.</span><span class="sxs-lookup"><span data-stu-id="404f6-220">c.</span></span> <span data-ttu-id="404f6-221">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="404f6-221">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="404f6-222">d.</span><span class="sxs-lookup"><span data-stu-id="404f6-222">d.</span></span> <span data-ttu-id="404f6-223">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="404f6-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="404f6-224">Creación de un usuario de prueba de Zendesk</span><span class="sxs-lookup"><span data-stu-id="404f6-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="404f6-225">toolog de los usuarios de Azure AD tooenable en **Zendesk**, se les deben aprovisionar en **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="404f6-225">tooenable Azure AD users toolog into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="404f6-226">Según el rol de hello asignado en aplicaciones de hello, Hola su comportamiento esperado:</span><span class="sxs-lookup"><span data-stu-id="404f6-226">Depending on hello role assigned in hello apps, it's hello expected behavior:</span></span>

 1. <span data-ttu-id="404f6-227">Las cuentas de **usuario final** se aprovisionan automáticamente al iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="404f6-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="404f6-228">**Agente** y **administración** las cuentas que necesitan toobe aprovisionado manualmente en **Zendesk** antes de iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="404f6-228">**Agent** and **Admin** accounts need toobe manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="404f6-229">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="404f6-229">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="404f6-230">Inicie sesión en tooyour **Zendesk** inquilino.</span><span class="sxs-lookup"><span data-stu-id="404f6-230">Log in tooyour **Zendesk** tenant.</span></span>

2. <span data-ttu-id="404f6-231">Seleccione hello **lista de clientes** ficha.</span><span class="sxs-lookup"><span data-stu-id="404f6-231">Select hello **Customer List** tab.</span></span>

3. <span data-ttu-id="404f6-232">Seleccione hello **usuario** ficha y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="404f6-232">Select hello **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="404f6-233">![Agregar usuario](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="404f6-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="404f6-234">Escriba la dirección de correo electrónico de Hola de una cuenta de Azure AD existente que desee tooprovision y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="404f6-234">Type hello email address of an existing Azure AD account you want tooprovision, and then click **Save**.</span></span>
   
    <span data-ttu-id="404f6-235">![Nuevo usuario](./media/active-directory-saas-zendesk-tutorial/ic773633.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="404f6-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="404f6-236">Puede usar cualquier otra Zendesk usuario cuenta herramienta de creación o las API proporcionadas por Zendesk tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="404f6-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk tooprovision AAD user accounts.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="404f6-237">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="404f6-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="404f6-238">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooZendesk.</span><span class="sxs-lookup"><span data-stu-id="404f6-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZendesk.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="404f6-240">**tooassign Britta Simon tooZendesk, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="404f6-240">**tooassign Britta Simon tooZendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="404f6-241">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="404f6-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="404f6-243">En la lista de aplicaciones de hello, seleccione **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="404f6-243">In hello applications list, select **Zendesk**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="404f6-245">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="404f6-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="404f6-247">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="404f6-247">Click **Add** button.</span></span> <span data-ttu-id="404f6-248">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="404f6-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="404f6-250">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="404f6-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="404f6-251">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="404f6-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="404f6-252">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="404f6-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="404f6-253">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="404f6-253">Testing single sign-on</span></span>

<span data-ttu-id="404f6-254">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="404f6-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="404f6-255">Al hacer clic en icono de Zendesk Hola Hola Panel de acceso, deberá obtener aplicaciones de Zendesk tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="404f6-255">When you click hello Zendesk tile in hello Access Panel, you should get automatically signed-on tooyour Zendesk application.</span></span>
<span data-ttu-id="404f6-256">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="404f6-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="404f6-257">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="404f6-257">Additional resources</span></span>

* [<span data-ttu-id="404f6-258">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="404f6-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="404f6-259">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="404f6-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
