---
title: "Tutorial: Integración de Azure Active Directory con Mimecast Personal Portal | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el Portal Personal de Mimecast."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ee2a8edcab36f295732ac1ebe641ed7fcfc1f2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="30174-103">Tutorial: Integración de Azure Active Directory con Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="30174-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="30174-104">En este tutorial, aprenderá cómo toointegrate Portal Personal de Mimecast con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="30174-104">In this tutorial, you learn how toointegrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="30174-105">Integración de Portal Personal de Mimecast con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="30174-105">Integrating Mimecast Personal Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="30174-106">Puede controlar en Azure AD que tenga acceso tooMimecast Portal Personal</span><span class="sxs-lookup"><span data-stu-id="30174-106">You can control in Azure AD who has access tooMimecast Personal Portal</span></span>
- <span data-ttu-id="30174-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooMimecast Portal Personal (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="30174-107">You can enable your users tooautomatically get signed-on tooMimecast Personal Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="30174-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="30174-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="30174-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="30174-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30174-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="30174-110">Prerequisites</span></span>

<span data-ttu-id="30174-111">integración de Azure AD con el Portal Personal de Mimecast tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="30174-111">tooconfigure Azure AD integration with Mimecast Personal Portal, you need hello following items:</span></span>

- <span data-ttu-id="30174-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="30174-112">An Azure AD subscription</span></span>
- <span data-ttu-id="30174-113">Un suscripción habilitada para inicio de sesión único en Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="30174-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="30174-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="30174-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="30174-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="30174-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="30174-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="30174-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="30174-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="30174-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="30174-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="30174-118">Scenario description</span></span>
<span data-ttu-id="30174-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="30174-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="30174-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="30174-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="30174-121">Agregar Portal Personal de Mimecast desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="30174-121">Adding Mimecast Personal Portal from hello gallery</span></span>
2. <span data-ttu-id="30174-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="30174-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-hello-gallery"></a><span data-ttu-id="30174-123">Agregar Portal Personal de Mimecast desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="30174-123">Adding Mimecast Personal Portal from hello gallery</span></span>
<span data-ttu-id="30174-124">integración de hello tooconfigure del Portal Personal de Mimecast en Azure AD, deberá tooadd Portal Personal de Mimecast de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="30174-124">tooconfigure hello integration of Mimecast Personal Portal into Azure AD, you need tooadd Mimecast Personal Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="30174-125">**tooadd Portal Personal de Mimecast desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="30174-125">**tooadd Mimecast Personal Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="30174-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="30174-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="30174-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="30174-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="30174-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="30174-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="30174-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="30174-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="30174-133">En el cuadro de búsqueda de hello, escriba **Portal Personal de Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="30174-133">In hello search box, type **Mimecast Personal Portal**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. <span data-ttu-id="30174-135">En el panel de resultados de hello, seleccione **Portal Personal de Mimecast**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="30174-135">In hello results panel, select **Mimecast Personal Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="30174-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="30174-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="30174-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Mimecast Personal Portal con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="30174-138">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="30174-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el Portal Personal de Mimecast es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30174-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Personal Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="30174-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el Portal Personal de Mimecast debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="30174-140">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Personal Portal needs toobe established.</span></span>

<span data-ttu-id="30174-141">En el Portal Personal de Mimecast, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="30174-141">In Mimecast Personal Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="30174-142">tooconfigure y prueba de inicio de sesión único en Azure AD con el Portal Personal de Mimecast, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="30174-142">tooconfigure and test Azure AD single sign-on with Mimecast Personal Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="30174-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="30174-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="30174-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="30174-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="30174-145">**[Crear un usuario de prueba del Portal Personal de Mimecast](#creating-a-mimecast-personal-portal-test-user)**  -toohave un equivalente de Britta Simon en el Portal Personal de Mimecast que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="30174-145">**[Creating a Mimecast Personal Portal test user](#creating-a-mimecast-personal-portal-test-user)** - toohave a counterpart of Britta Simon in Mimecast Personal Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="30174-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="30174-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="30174-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="30174-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="30174-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="30174-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="30174-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Portal Personal de Mimecast.</span><span class="sxs-lookup"><span data-stu-id="30174-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="30174-150">**tooconfigure inicio de sesión único en Azure AD con el Portal Personal de Mimecast, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="30174-150">**tooconfigure Azure AD single sign-on with Mimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="30174-151">En el portal de Azure, en Hola Hola **Portal Personal de Mimecast** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="30174-151">In hello Azure portal, on hello **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="30174-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="30174-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. <span data-ttu-id="30174-155">En hello **dominio Portal Personal de Mimecast y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="30174-155">On hello **Mimecast Personal Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="30174-157">a.</span><span class="sxs-lookup"><span data-stu-id="30174-157">a.</span></span> <span data-ttu-id="30174-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="30174-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    <span data-ttu-id="30174-159">b.</span><span class="sxs-lookup"><span data-stu-id="30174-159">b.</span></span> <span data-ttu-id="30174-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="30174-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > <span data-ttu-id="30174-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="30174-161">These values are not real.</span></span> <span data-ttu-id="30174-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="30174-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="30174-163">Póngase en contacto con [equipo de soporte técnico de cliente de Portal Personal de Mimecast](https://www.mimecast.com/customer-success/technical-support/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="30174-163">Contact [Mimecast Personal Portal Client support team](https://www.mimecast.com/customer-success/technical-support/) tooget these values.</span></span> 
 


4. <span data-ttu-id="30174-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="30174-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. <span data-ttu-id="30174-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="30174-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="30174-168">En hello **configuración del Portal Personal de Mimecast** sección, haga clic en **configurar el Portal Personal de Mimecast** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="30174-168">On hello **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="30174-169">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="30174-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. <span data-ttu-id="30174-171">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="30174-171">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

8. <span data-ttu-id="30174-172">Vaya demasiado**servicios \> aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="30174-172">Go too**Services \> Applications**.</span></span>
   
    <span data-ttu-id="30174-173">![Aplicaciones](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="30174-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

9. <span data-ttu-id="30174-174">Haga clic en **Authentication Profiles**(Perfiles de autenticación).</span><span class="sxs-lookup"><span data-stu-id="30174-174">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="30174-175">![Authentication Profiles (Perfiles de autenticación)](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles (Perfiles de autenticación)")</span><span class="sxs-lookup"><span data-stu-id="30174-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

10. <span data-ttu-id="30174-176">Haga clic en **New Authentication Profile**(Nuevo perfil de autenticación).</span><span class="sxs-lookup"><span data-stu-id="30174-176">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="30174-177">![New Authentication Profile (Nuevo perfil de autenticación)](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile (Nuevo perfil de autenticación)")</span><span class="sxs-lookup"><span data-stu-id="30174-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

11. <span data-ttu-id="30174-178">Hola **perfil de autenticación** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="30174-178">In hello **Authentication Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="30174-179">![Authentication Profile (Perfil de autenticación)](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile (Perfil de autenticación)")</span><span class="sxs-lookup"><span data-stu-id="30174-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="30174-180">a.</span><span class="sxs-lookup"><span data-stu-id="30174-180">a.</span></span> <span data-ttu-id="30174-181">Hola **descripción** cuadro de texto, escriba un nombre para la configuración.</span><span class="sxs-lookup"><span data-stu-id="30174-181">In hello **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="30174-182">b.</span><span class="sxs-lookup"><span data-stu-id="30174-182">b.</span></span> <span data-ttu-id="30174-183">Seleccione **Aplicar la autenticación SAML a Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="30174-183">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="30174-184">c.</span><span class="sxs-lookup"><span data-stu-id="30174-184">c.</span></span> <span data-ttu-id="30174-185">Como **Provider** (Proveedor), seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="30174-185">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="30174-186">d.</span><span class="sxs-lookup"><span data-stu-id="30174-186">d.</span></span> <span data-ttu-id="30174-187">En **dirección URL del emisor** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="30174-187">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="30174-188">e.</span><span class="sxs-lookup"><span data-stu-id="30174-188">e.</span></span> <span data-ttu-id="30174-189">En **dirección URL de inicio de sesión** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="30174-189">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="30174-190">f.</span><span class="sxs-lookup"><span data-stu-id="30174-190">f.</span></span> <span data-ttu-id="30174-191">En **Logout URL** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="30174-191">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="30174-192">g.</span><span class="sxs-lookup"><span data-stu-id="30174-192">g.</span></span> <span data-ttu-id="30174-193">Abra su **base-64** codificado certificado en el Bloc de notas que se descarga desde el portal de Azure, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado del proveedor de identidades (metadatos)** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="30174-193">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="30174-194">h.</span><span class="sxs-lookup"><span data-stu-id="30174-194">h.</span></span> <span data-ttu-id="30174-195">Seleccione **Permitir inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="30174-195">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="30174-196">i.</span><span class="sxs-lookup"><span data-stu-id="30174-196">i.</span></span> <span data-ttu-id="30174-197">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="30174-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="30174-198">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="30174-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="30174-199">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="30174-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="30174-200">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="30174-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="30174-201">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="30174-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="30174-202">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="30174-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="30174-204">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="30174-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="30174-205">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="30174-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="30174-207">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="30174-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="30174-209">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="30174-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="30174-211">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="30174-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="30174-213">a.</span><span class="sxs-lookup"><span data-stu-id="30174-213">a.</span></span> <span data-ttu-id="30174-214">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="30174-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="30174-215">b.</span><span class="sxs-lookup"><span data-stu-id="30174-215">b.</span></span> <span data-ttu-id="30174-216">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="30174-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="30174-217">c.</span><span class="sxs-lookup"><span data-stu-id="30174-217">c.</span></span> <span data-ttu-id="30174-218">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="30174-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="30174-219">d.</span><span class="sxs-lookup"><span data-stu-id="30174-219">d.</span></span> <span data-ttu-id="30174-220">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="30174-220">Click **Create**.</span></span>
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="30174-221">Creación de un usuario de prueba de Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="30174-221">Creating a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="30174-222">En orden tooenable toolog de los usuarios de Azure AD en el Portal Personal de Mimecast, se les deben aprovisionar en el Portal Personal de Mimecast.</span><span class="sxs-lookup"><span data-stu-id="30174-222">In order tooenable Azure AD users toolog into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="30174-223">En caso de hello del Portal Personal de Mimecast, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="30174-223">In hello case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="30174-224">Deberá tooregister un dominio para poder crear los usuarios.</span><span class="sxs-lookup"><span data-stu-id="30174-224">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="30174-225">**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="30174-225">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="30174-226">Inicio de sesión tooyour **Portal Personal de Mimecast** como administrador.</span><span class="sxs-lookup"><span data-stu-id="30174-226">Sign on tooyour **Mimecast Personal Portal** as administrator.</span></span>

2. <span data-ttu-id="30174-227">Vaya demasiado**directorios \> interno**.</span><span class="sxs-lookup"><span data-stu-id="30174-227">Go too**Directories \> Internal**.</span></span>
   
    <span data-ttu-id="30174-228">![Directories (Directorios)](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories (Directorios)")</span><span class="sxs-lookup"><span data-stu-id="30174-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

3. <span data-ttu-id="30174-229">Haga clic en **Register New Domain**(Registrar nuevo dominio).</span><span class="sxs-lookup"><span data-stu-id="30174-229">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="30174-230">![Register New Domain (Registrar nuevo dominio)](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain (Registrar nuevo dominio)")</span><span class="sxs-lookup"><span data-stu-id="30174-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

4. <span data-ttu-id="30174-231">Una vez creado el nuevo dominio, haga clic en **New Address**(Nueva dirección).</span><span class="sxs-lookup"><span data-stu-id="30174-231">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="30174-232">![New Address (Nueva dirección)](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address (Nueva dirección)")</span><span class="sxs-lookup"><span data-stu-id="30174-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

5. <span data-ttu-id="30174-233">Hola dirección cuadro de diálogo nuevo, realizar Hola siguiendo los pasos de un Azure válida que desee tooprovision de cuenta de AD:</span><span class="sxs-lookup"><span data-stu-id="30174-233">In hello new address dialog, perform hello following steps of a valid Azure AD account you want tooprovision:</span></span>
   
    <span data-ttu-id="30174-234">![Guardar](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Guardar")</span><span class="sxs-lookup"><span data-stu-id="30174-234">![Save](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="30174-235">a.</span><span class="sxs-lookup"><span data-stu-id="30174-235">a.</span></span> <span data-ttu-id="30174-236">Hola **dirección de correo electrónico** cuadro de texto, tipo **dirección de correo electrónico** del usuario de hello como  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="30174-236">In hello **Email Address** textbox, type **Email Address** of hello user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="30174-237">b.</span><span class="sxs-lookup"><span data-stu-id="30174-237">b.</span></span> <span data-ttu-id="30174-238">Hola **nombre Global** cuadro de texto, hello tipo **nombre de usuario** como **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="30174-238">In hello **Global Name** textbox, type hello **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="30174-239">c.</span><span class="sxs-lookup"><span data-stu-id="30174-239">c.</span></span> <span data-ttu-id="30174-240">Hola **contraseña**, y **Confirmar contraseña** cuadros de texto, hello tipo **contraseña** del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="30174-240">In hello **Password**, and **Confirm Password** textboxes, type hello **Password** of hello user.</span></span>
   
    <span data-ttu-id="30174-241">b.</span><span class="sxs-lookup"><span data-stu-id="30174-241">b.</span></span> <span data-ttu-id="30174-242">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="30174-242">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="30174-243">Puede usar cualquier otra herramienta de creación de cuentas de usuario de Portal Personal de Mimecast o las API proporcionadas por las cuentas de usuario de Azure AD de Portal Personal de Mimecast tooprovision.</span><span class="sxs-lookup"><span data-stu-id="30174-243">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="30174-244">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="30174-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="30174-245">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooMimecast Portal Personal.</span><span class="sxs-lookup"><span data-stu-id="30174-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Personal Portal.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="30174-247">**tooassign Britta Simon tooMimecast Portal Personal, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="30174-247">**tooassign Britta Simon tooMimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="30174-248">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="30174-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="30174-250">En la lista de aplicaciones de hello, seleccione **Portal Personal de Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="30174-250">In hello applications list, select **Mimecast Personal Portal**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. <span data-ttu-id="30174-252">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="30174-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="30174-254">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="30174-254">Click **Add** button.</span></span> <span data-ttu-id="30174-255">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="30174-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="30174-257">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="30174-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="30174-258">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="30174-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="30174-259">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="30174-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="30174-260">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="30174-260">Testing single sign-on</span></span>
<span data-ttu-id="30174-261">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="30174-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="30174-262">Al hacer clic en icono de Portal Personal de Mimecast Hola Hola Panel de acceso, deberá obtener la aplicación de Portal Personal de Mimecast tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="30174-262">When you click hello Mimecast Personal Portal tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Personal Portal application.</span></span> <span data-ttu-id="30174-263">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="30174-263">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="30174-264">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="30174-264">Additional resources</span></span>

* [<span data-ttu-id="30174-265">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="30174-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="30174-266">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="30174-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

