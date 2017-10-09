---
title: "Tutorial: integración de Azure Active Directory con Workfront | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Workfront."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: e7249b9ec769f19cf5aa7d44ff6f58705df4020a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workfront"></a><span data-ttu-id="0dedd-103">Tutorial: integración de Azure Active Directory con Workfront</span><span class="sxs-lookup"><span data-stu-id="0dedd-103">Tutorial: Azure Active Directory integration with Workfront</span></span>

<span data-ttu-id="0dedd-104">En este tutorial, aprenderá cómo toointegrate Workfront con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0dedd-104">In this tutorial, you learn how toointegrate Workfront with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0dedd-105">Integración Workfront con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0dedd-105">Integrating Workfront with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0dedd-106">Puede controlar en Azure AD que tenga acceso tooWorkfront</span><span class="sxs-lookup"><span data-stu-id="0dedd-106">You can control in Azure AD who has access tooWorkfront</span></span>
- <span data-ttu-id="0dedd-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooWorkfront (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dedd-107">You can enable your users tooautomatically get signed-on tooWorkfront (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0dedd-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0dedd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0dedd-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0dedd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dedd-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0dedd-110">Prerequisites</span></span>

<span data-ttu-id="0dedd-111">integración de Azure AD con Workfront tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0dedd-111">tooconfigure Azure AD integration with Workfront, you need hello following items:</span></span>

- <span data-ttu-id="0dedd-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dedd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0dedd-113">Una suscripción habilitada para el inicio de sesión único en Workfront</span><span class="sxs-lookup"><span data-stu-id="0dedd-113">A Workfront single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0dedd-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0dedd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0dedd-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0dedd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0dedd-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0dedd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0dedd-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0dedd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0dedd-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0dedd-118">Scenario description</span></span>
<span data-ttu-id="0dedd-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0dedd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0dedd-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="0dedd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0dedd-121">Agregar Workfront desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0dedd-121">Adding Workfront from hello gallery</span></span>
2. <span data-ttu-id="0dedd-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dedd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workfront-from-hello-gallery"></a><span data-ttu-id="0dedd-123">Agregar Workfront desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0dedd-123">Adding Workfront from hello gallery</span></span>
<span data-ttu-id="0dedd-124">integración de hello tooconfigure de Workfront en Azure AD, deberá tooadd Workfront de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="0dedd-124">tooconfigure hello integration of Workfront into Azure AD, you need tooadd Workfront from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0dedd-125">**tooadd Workfront de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0dedd-125">**tooadd Workfront from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dedd-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0dedd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0dedd-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0dedd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0dedd-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0dedd-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0dedd-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0dedd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0dedd-133">En el cuadro de búsqueda de hello, escriba **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="0dedd-133">In hello search box, type **Workfront**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_search.png)

5. <span data-ttu-id="0dedd-135">En el panel de resultados de hello, seleccione **Workfront**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0dedd-135">In hello results panel, select **Workfront**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0dedd-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dedd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0dedd-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Workfront con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0dedd-138">In this section, you configure and test Azure AD single sign-on with Workfront based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0dedd-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Workfront es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0dedd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workfront is tooa user in Azure AD.</span></span> <span data-ttu-id="0dedd-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Workfront debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="0dedd-140">In other words, a link relationship between an Azure AD user and hello related user in Workfront needs toobe established.</span></span>

<span data-ttu-id="0dedd-141">En Workfront, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dedd-141">In Workfront, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0dedd-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Workfront, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0dedd-142">tooconfigure and test Azure AD single sign-on with Workfront, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0dedd-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="0dedd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0dedd-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0dedd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0dedd-145">**[Crear un usuario de prueba Workfront](#creating-a-workfront-test-user)**  -toohave un equivalente de Britta Simon en Workfront que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="0dedd-145">**[Creating a Workfront test user](#creating-a-workfront-test-user)** - toohave a counterpart of Britta Simon in Workfront that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0dedd-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0dedd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0dedd-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0dedd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0dedd-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dedd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0dedd-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Workfront.</span><span class="sxs-lookup"><span data-stu-id="0dedd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workfront application.</span></span>

<span data-ttu-id="0dedd-150">**inicio de sesión único en Azure AD tooconfigure con Workfront, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0dedd-150">**tooconfigure Azure AD single sign-on with Workfront, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dedd-151">En el portal de Azure, en Hola Hola **Workfront** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0dedd-151">In hello Azure portal, on hello **Workfront** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0dedd-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0dedd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_samlbase.png)

3. <span data-ttu-id="0dedd-155">En hello **Workfront dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0dedd-155">On hello **Workfront Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_url.png)

    <span data-ttu-id="0dedd-157">a.</span><span class="sxs-lookup"><span data-stu-id="0dedd-157">a.</span></span> <span data-ttu-id="0dedd-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.attask-ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="0dedd-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.attask-ondemand.com`</span></span>

    <span data-ttu-id="0dedd-159">b.</span><span class="sxs-lookup"><span data-stu-id="0dedd-159">b.</span></span> <span data-ttu-id="0dedd-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.attasksandbox.com/SAML2`</span><span class="sxs-lookup"><span data-stu-id="0dedd-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.attasksandbox.com/SAML2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0dedd-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="0dedd-161">These values are not real.</span></span> <span data-ttu-id="0dedd-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="0dedd-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0dedd-163">Póngase en contacto con [equipo de soporte técnico de cliente de Workfront](https://www.workfront.com/contact-us/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="0dedd-163">Contact [Workfront Client support team](https://www.workfront.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="0dedd-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0dedd-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_certificate.png) 

5. <span data-ttu-id="0dedd-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0dedd-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workfront-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0dedd-168">En hello **Workfront configuración** sección, haga clic en **configurar Workfront** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="0dedd-168">On hello **Workfront Configuration** section, click **Configure Workfront** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0dedd-169">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="0dedd-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_configure.png) 

7. <span data-ttu-id="0dedd-171">Sitio de empresa de Workfront tooyour de inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="0dedd-171">Sign-on tooyour Workfront company site as administrator.</span></span>

8. <span data-ttu-id="0dedd-172">Vaya demasiado**inicio de sesión único en la configuración**.</span><span class="sxs-lookup"><span data-stu-id="0dedd-172">Go too**Single Sign On Configuration**.</span></span>

9. <span data-ttu-id="0dedd-173">En hello **Single Sign-On** cuadro de diálogo, realizar pasos de Hola</span><span class="sxs-lookup"><span data-stu-id="0dedd-173">On hello **Single Sign-On** dialog, perform hello following steps</span></span>
    
    ![Configurar inicio de sesión único][23]
   
    <span data-ttu-id="0dedd-175">a.</span><span class="sxs-lookup"><span data-stu-id="0dedd-175">a.</span></span> <span data-ttu-id="0dedd-176">En **Tipo**, seleccione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="0dedd-176">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="0dedd-177">b.</span><span class="sxs-lookup"><span data-stu-id="0dedd-177">b.</span></span> <span data-ttu-id="0dedd-178">Seleccione **Service Provider ID** (Id. del proveedor de servicios).</span><span class="sxs-lookup"><span data-stu-id="0dedd-178">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="0dedd-179">c.</span><span class="sxs-lookup"><span data-stu-id="0dedd-179">c.</span></span> <span data-ttu-id="0dedd-180">Hola pegar **SAML Single Sign-On dirección URL del servicio** en hello **dirección URL del Portal de inicio de sesión** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0dedd-180">Paste hello **SAML Single Sign-On Service URL** into hello **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="0dedd-181">d.</span><span class="sxs-lookup"><span data-stu-id="0dedd-181">d.</span></span> <span data-ttu-id="0dedd-182">Pegar **dirección URL del servicio de cierre de sesión único** en hello **dirección URL de cierre de sesión** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0dedd-182">Paste **Single Sign-Out Service URL** into hello **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="0dedd-183">e.</span><span class="sxs-lookup"><span data-stu-id="0dedd-183">e.</span></span> <span data-ttu-id="0dedd-184">Pegar **cambiar dirección URL de contraseña** en hello **cambiar dirección URL de contraseña** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0dedd-184">Paste **Change Password URL** into hello **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="0dedd-185">f.</span><span class="sxs-lookup"><span data-stu-id="0dedd-185">f.</span></span> <span data-ttu-id="0dedd-186">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0dedd-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0dedd-187">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="0dedd-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0dedd-188">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="0dedd-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0dedd-189">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0dedd-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0dedd-190">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dedd-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="0dedd-191">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="0dedd-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0dedd-193">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0dedd-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dedd-194">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0dedd-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0dedd-196">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0dedd-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0dedd-198">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dedd-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0dedd-200">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="0dedd-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0dedd-202">a.</span><span class="sxs-lookup"><span data-stu-id="0dedd-202">a.</span></span> <span data-ttu-id="0dedd-203">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0dedd-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0dedd-204">b.</span><span class="sxs-lookup"><span data-stu-id="0dedd-204">b.</span></span> <span data-ttu-id="0dedd-205">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0dedd-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0dedd-206">c.</span><span class="sxs-lookup"><span data-stu-id="0dedd-206">c.</span></span> <span data-ttu-id="0dedd-207">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0dedd-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0dedd-208">d.</span><span class="sxs-lookup"><span data-stu-id="0dedd-208">d.</span></span> <span data-ttu-id="0dedd-209">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0dedd-209">Click **Create**.</span></span>
 
### <a name="creating-a-workfront-test-user"></a><span data-ttu-id="0dedd-210">Creación de usuario de prueba de Workfront</span><span class="sxs-lookup"><span data-stu-id="0dedd-210">Creating a Workfront test user</span></span>

<span data-ttu-id="0dedd-211">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Workfront toocreate.</span><span class="sxs-lookup"><span data-stu-id="0dedd-211">hello objective of this section is toocreate a user called Britta Simon in Workfront.</span></span>

<span data-ttu-id="0dedd-212">**toocreate un usuario llamado Britta Simon en Workfront, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0dedd-212">**toocreate a user called Britta Simon in Workfront, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dedd-213">Inicie sesión en tooyour Workfront sitio de su compañía como administrador.</span><span class="sxs-lookup"><span data-stu-id="0dedd-213">Sign on tooyour Workfront company site as administrator.</span></span>
2. <span data-ttu-id="0dedd-214">En el menú de hello en la parte superior de hello, haga clic en **personas**.</span><span class="sxs-lookup"><span data-stu-id="0dedd-214">In hello menu on hello top, click **People**.</span></span>
3. <span data-ttu-id="0dedd-215">Haga clic en **New Person**(Nueva persona).</span><span class="sxs-lookup"><span data-stu-id="0dedd-215">Click **New Person**.</span></span> 
4. <span data-ttu-id="0dedd-216">En el cuadro de diálogo de hello nueva persona, realice Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0dedd-216">On hello New Person dialog, perform hello following steps:</span></span>
   
    ![Crear un usuario de prueba en Workfront][21] 
   
    <span data-ttu-id="0dedd-218">a.</span><span class="sxs-lookup"><span data-stu-id="0dedd-218">a.</span></span> <span data-ttu-id="0dedd-219">Hola **nombre** cuadro de texto, escriba "Bárbara."</span><span class="sxs-lookup"><span data-stu-id="0dedd-219">In hello **First Name** textbox, type "Britta."</span></span>
   
    <span data-ttu-id="0dedd-220">b.</span><span class="sxs-lookup"><span data-stu-id="0dedd-220">b.</span></span> <span data-ttu-id="0dedd-221">Hola **Last Name** cuadro de texto, escriba "Simon".</span><span class="sxs-lookup"><span data-stu-id="0dedd-221">In hello **Last Name** textbox, type "Simon."</span></span>
   
    <span data-ttu-id="0dedd-222">c.</span><span class="sxs-lookup"><span data-stu-id="0dedd-222">c.</span></span> <span data-ttu-id="0dedd-223">Hola **dirección de correo electrónico** cuadro de texto, escriba la dirección de correo electrónico Britta Simon en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0dedd-223">In hello **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="0dedd-224">d.</span><span class="sxs-lookup"><span data-stu-id="0dedd-224">d.</span></span> <span data-ttu-id="0dedd-225">Haga clic en **Add Person**(Agregar persona).</span><span class="sxs-lookup"><span data-stu-id="0dedd-225">Click **Add Person**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0dedd-226">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dedd-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0dedd-227">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooWorkfront.</span><span class="sxs-lookup"><span data-stu-id="0dedd-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkfront.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0dedd-229">**tooassign Britta Simon tooWorkfront, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0dedd-229">**tooassign Britta Simon tooWorkfront, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dedd-230">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0dedd-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0dedd-232">En la lista de aplicaciones de hello, seleccione **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="0dedd-232">In hello applications list, select **Workfront**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_app.png) 

3. <span data-ttu-id="0dedd-234">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0dedd-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0dedd-236">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0dedd-236">Click **Add** button.</span></span> <span data-ttu-id="0dedd-237">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0dedd-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0dedd-239">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dedd-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0dedd-240">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0dedd-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0dedd-241">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0dedd-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0dedd-242">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="0dedd-242">Testing single sign-on</span></span>

<span data-ttu-id="0dedd-243">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0dedd-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0dedd-244">Al hacer clic en icono de Workfront Hola Hola Panel de acceso, deberá obtener la página de inicio de sesión de la aplicación Workfront.</span><span class="sxs-lookup"><span data-stu-id="0dedd-244">When you click hello Workfront tile in hello Access Panel, you should get login page of Workfront application.</span></span>
<span data-ttu-id="0dedd-245">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0dedd-245">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0dedd-246">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0dedd-246">Additional resources</span></span>

* [<span data-ttu-id="0dedd-247">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0dedd-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0dedd-248">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0dedd-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_04.png
[21]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_08.png
[23]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_06.png
[100]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_203.png

