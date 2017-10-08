---
title: "Tutorial: integración de Azure Active Directory con Freshservice | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Freshservice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d73624b87d058f66885ae72fda69a0aacc89c1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a><span data-ttu-id="66f0e-103">Tutorial: integración de Azure Active Directory con Freshservice</span><span class="sxs-lookup"><span data-stu-id="66f0e-103">Tutorial: Azure Active Directory integration with Freshservice</span></span>

<span data-ttu-id="66f0e-104">En este tutorial, aprenderá cómo toointegrate Freshservice con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="66f0e-104">In this tutorial, you learn how toointegrate Freshservice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="66f0e-105">Integración de Freshservice con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="66f0e-105">Integrating Freshservice with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="66f0e-106">Puede controlar en Azure AD que tenga acceso tooFreshservice</span><span class="sxs-lookup"><span data-stu-id="66f0e-106">You can control in Azure AD who has access tooFreshservice</span></span>
- <span data-ttu-id="66f0e-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooFreshservice (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66f0e-107">You can enable your users tooautomatically get signed-on tooFreshservice (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="66f0e-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="66f0e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="66f0e-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="66f0e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66f0e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="66f0e-110">Prerequisites</span></span>

<span data-ttu-id="66f0e-111">integración de Azure AD con Freshservice tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="66f0e-111">tooconfigure Azure AD integration with Freshservice, you need hello following items:</span></span>

- <span data-ttu-id="66f0e-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66f0e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="66f0e-113">Una suscripción habilitada para el inicio de sesión único en Freshservice</span><span class="sxs-lookup"><span data-stu-id="66f0e-113">A Freshservice single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="66f0e-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="66f0e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="66f0e-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="66f0e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="66f0e-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="66f0e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="66f0e-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="66f0e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="66f0e-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="66f0e-118">Scenario description</span></span>
<span data-ttu-id="66f0e-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="66f0e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="66f0e-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="66f0e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="66f0e-121">Agregar Freshservice desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="66f0e-121">Adding Freshservice from hello gallery</span></span>
2. <span data-ttu-id="66f0e-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66f0e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshservice-from-hello-gallery"></a><span data-ttu-id="66f0e-123">Agregar Freshservice desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="66f0e-123">Adding Freshservice from hello gallery</span></span>
<span data-ttu-id="66f0e-124">integración de hello tooconfigure de Freshservice en Azure AD, deberá tooadd Freshservice de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="66f0e-124">tooconfigure hello integration of Freshservice into Azure AD, you need tooadd Freshservice from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="66f0e-125">**tooadd Freshservice de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="66f0e-125">**tooadd Freshservice from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="66f0e-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="66f0e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="66f0e-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="66f0e-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="66f0e-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="66f0e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="66f0e-133">En el cuadro de búsqueda de hello, escriba **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-133">In hello search box, type **Freshservice**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. <span data-ttu-id="66f0e-135">En el panel de resultados de hello, seleccione **Freshservice**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="66f0e-135">In hello results panel, select **Freshservice**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="66f0e-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66f0e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="66f0e-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Freshservice con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="66f0e-138">In this section, you configure and test Azure AD single sign-on with Freshservice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="66f0e-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Freshservice es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66f0e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Freshservice is tooa user in Azure AD.</span></span> <span data-ttu-id="66f0e-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Freshservice debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="66f0e-140">In other words, a link relationship between an Azure AD user and hello related user in Freshservice needs toobe established.</span></span>

<span data-ttu-id="66f0e-141">En Freshservice, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="66f0e-141">In Freshservice, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="66f0e-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Freshservice, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="66f0e-142">tooconfigure and test Azure AD single sign-on with Freshservice, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="66f0e-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="66f0e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="66f0e-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="66f0e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="66f0e-145">**[Crear un usuario de prueba de Freshservice](#creating-a-freshservice-test-user)**  -toohave un equivalente de Britta Simon en Freshservice que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="66f0e-145">**[Creating a Freshservice test user](#creating-a-freshservice-test-user)** - toohave a counterpart of Britta Simon in Freshservice that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="66f0e-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="66f0e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="66f0e-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="66f0e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="66f0e-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66f0e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="66f0e-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Freshservice.</span><span class="sxs-lookup"><span data-stu-id="66f0e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Freshservice application.</span></span>

<span data-ttu-id="66f0e-150">**inicio de sesión único en Azure AD tooconfigure con Freshservice, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="66f0e-150">**tooconfigure Azure AD single sign-on with Freshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="66f0e-151">En el portal de Azure, en Hola Hola **Freshservice** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-151">In hello Azure portal, on hello **Freshservice** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="66f0e-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="66f0e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. <span data-ttu-id="66f0e-155">En hello **Freshservice dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="66f0e-155">On hello **Freshservice Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    <span data-ttu-id="66f0e-157">a.</span><span class="sxs-lookup"><span data-stu-id="66f0e-157">a.</span></span> <span data-ttu-id="66f0e-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="66f0e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    <span data-ttu-id="66f0e-159">b.</span><span class="sxs-lookup"><span data-stu-id="66f0e-159">b.</span></span> <span data-ttu-id="66f0e-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="66f0e-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="66f0e-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="66f0e-161">These values are not real.</span></span> <span data-ttu-id="66f0e-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="66f0e-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="66f0e-163">Póngase en contacto con [equipo de soporte técnico de cliente de Freshservice](https://support.freshservice.com/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="66f0e-163">Contact [Freshservice Client support team](https://support.freshservice.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="66f0e-164">En hello **el certificado de firma de SAML** sección, copie **huella digital** el valor de certificado.</span><span class="sxs-lookup"><span data-stu-id="66f0e-164">On hello **SAML Signing Certificate** section, copy **THUMBPRINT** value of certificate.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. <span data-ttu-id="66f0e-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="66f0e-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="66f0e-168">En hello **configuración de Freshservice** sección, haga clic en **configurar Freshservice** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="66f0e-168">On hello **Freshservice Configuration** section, click **Configure Freshservice** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="66f0e-169">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="66f0e-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. <span data-ttu-id="66f0e-171">En una ventana del explorador web diferente, inicie sesión en el sitio de la empresa tooyour Freshservice como administrador.</span><span class="sxs-lookup"><span data-stu-id="66f0e-171">In a different web browser window, log in tooyour Freshservice company site as an administrator.</span></span>

8. <span data-ttu-id="66f0e-172">En el menú de hello en la parte superior de hello, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="66f0e-173">![Administración](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="66f0e-173">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

9. <span data-ttu-id="66f0e-174">Hola **Portal del cliente**, haga clic en **seguridad**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-174">In hello **Customer Portal**, click **Security**.</span></span>
   
    <span data-ttu-id="66f0e-175">![Seguridad](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Seguridad")</span><span class="sxs-lookup"><span data-stu-id="66f0e-175">![Security](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Security")</span></span>

10. <span data-ttu-id="66f0e-176">Hola **seguridad** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="66f0e-176">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="66f0e-177">![Inicio de sesión único](./media/active-directory-saas-freshservice-tutorial/ic790816.png "inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="66f0e-177">![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")</span></span>
   
    <span data-ttu-id="66f0e-178">a.</span><span class="sxs-lookup"><span data-stu-id="66f0e-178">a.</span></span> <span data-ttu-id="66f0e-179">Cambie a **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-179">Switch **Single Sign On**.</span></span>

    <span data-ttu-id="66f0e-180">b.</span><span class="sxs-lookup"><span data-stu-id="66f0e-180">b.</span></span> <span data-ttu-id="66f0e-181">Seleccione **Inicio de sesión único de SAML**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-181">Select **SAML SSO**.</span></span>

    <span data-ttu-id="66f0e-182">c.</span><span class="sxs-lookup"><span data-stu-id="66f0e-182">c.</span></span> <span data-ttu-id="66f0e-183">Hola **dirección URL de inicio de sesión de SAML** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="66f0e-183">In hello **SAML Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="66f0e-184">d.</span><span class="sxs-lookup"><span data-stu-id="66f0e-184">d.</span></span> <span data-ttu-id="66f0e-185">Hola **Logout URL** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="66f0e-185">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="66f0e-186">e.</span><span class="sxs-lookup"><span data-stu-id="66f0e-186">e.</span></span> <span data-ttu-id="66f0e-187">En **huella digital de certificado de seguridad** cuadro de texto, pegue hello **huella digital** el valor de certificado que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="66f0e-187">In **Security Certificate Fingerprint** textbox, paste hello **THUMBPRINT** value of certificate which you have copied from Azure portal.</span></span>

    <span data-ttu-id="66f0e-188">f.</span><span class="sxs-lookup"><span data-stu-id="66f0e-188">f.</span></span> <span data-ttu-id="66f0e-189">Haga clic en **Guardar**</span><span class="sxs-lookup"><span data-stu-id="66f0e-189">Click **Save**</span></span>
   
> [!TIP]
> <span data-ttu-id="66f0e-190">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="66f0e-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="66f0e-191">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="66f0e-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="66f0e-192">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="66f0e-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="66f0e-193">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66f0e-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="66f0e-194">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="66f0e-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="66f0e-196">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="66f0e-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="66f0e-197">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="66f0e-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="66f0e-199">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="66f0e-201">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="66f0e-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="66f0e-203">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="66f0e-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="66f0e-205">a.</span><span class="sxs-lookup"><span data-stu-id="66f0e-205">a.</span></span> <span data-ttu-id="66f0e-206">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="66f0e-207">b.</span><span class="sxs-lookup"><span data-stu-id="66f0e-207">b.</span></span> <span data-ttu-id="66f0e-208">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="66f0e-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="66f0e-209">c.</span><span class="sxs-lookup"><span data-stu-id="66f0e-209">c.</span></span> <span data-ttu-id="66f0e-210">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="66f0e-211">d.</span><span class="sxs-lookup"><span data-stu-id="66f0e-211">d.</span></span> <span data-ttu-id="66f0e-212">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-212">Click **Create**.</span></span>
 
### <a name="creating-a-freshservice-test-user"></a><span data-ttu-id="66f0e-213">Creación de un usuario de prueba de Freshservice</span><span class="sxs-lookup"><span data-stu-id="66f0e-213">Creating a Freshservice test user</span></span>

<span data-ttu-id="66f0e-214">toolog de los usuarios de Azure AD tooenable en tooFreshService, se les deben aprovisionar en FreshService.</span><span class="sxs-lookup"><span data-stu-id="66f0e-214">tooenable Azure AD users toolog in tooFreshService, they must be provisioned into FreshService.</span></span> <span data-ttu-id="66f0e-215">En caso de hello de FreshService, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="66f0e-215">In hello case of FreshService, provisioning is a manual task.</span></span>

<span data-ttu-id="66f0e-216">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="66f0e-216">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="66f0e-217">Inicie sesión en tooyour **FreshService** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="66f0e-217">Log in tooyour **FreshService** company site as an administrator.</span></span>

2. <span data-ttu-id="66f0e-218">En el menú de hello en la parte superior de hello, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-218">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="66f0e-219">![Administración](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="66f0e-219">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

3. <span data-ttu-id="66f0e-220">Hola **administración de usuarios** sección, haga clic en **los solicitantes**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-220">In hello **User Management** section, click **Requesters**.</span></span>
   
    <span data-ttu-id="66f0e-221">![Solicitantes](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Solicitantes")</span><span class="sxs-lookup"><span data-stu-id="66f0e-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span></span>

4. <span data-ttu-id="66f0e-222">Haga clic en **Nuevo solicitante**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-222">Click **New Requester**.</span></span>
   
    <span data-ttu-id="66f0e-223">![Nuevos solicitantes](./media/active-directory-saas-freshservice-tutorial/ic790819.png "Nuevos solicitantes")</span><span class="sxs-lookup"><span data-stu-id="66f0e-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span></span>

5. <span data-ttu-id="66f0e-224">Hola **nuevo solicitante** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="66f0e-224">In hello **New Requester** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="66f0e-225">![Nuevo solicitante](./media/active-directory-saas-freshservice-tutorial/ic790820.png "Nuevo solicitante")</span><span class="sxs-lookup"><span data-stu-id="66f0e-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span></span>   

    <span data-ttu-id="66f0e-226">a.</span><span class="sxs-lookup"><span data-stu-id="66f0e-226">a.</span></span> <span data-ttu-id="66f0e-227">Escriba hello **nombre** y **correo electrónico** atributos de una cuenta válida de Azure Active Directory que quiera tooprovision en hello relacionados con cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="66f0e-227">Enter hello **First Name** and **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="66f0e-228">b.</span><span class="sxs-lookup"><span data-stu-id="66f0e-228">b.</span></span> <span data-ttu-id="66f0e-229">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-229">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="66f0e-230">titular de la cuenta de Hello Azure Active Directory Obtiene un correo electrónico con una cuenta de hello tooconfirm vínculo antes de activarla</span><span class="sxs-lookup"><span data-stu-id="66f0e-230">hello Azure Active Directory account holder gets an email including a link tooconfirm hello account before it becomes active</span></span>
    >  

>[!NOTE]
><span data-ttu-id="66f0e-231">Puede usar cualquier otra FreshService usuario cuenta herramienta de creación o las API proporcionadas por FreshService tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="66f0e-231">You can use any other FreshService user account creation tools or APIs provided by FreshService tooprovision AAD user accounts.</span></span>
>  

![Asignar usuario][200] 

<span data-ttu-id="66f0e-233">**tooassign Britta Simon tooFreshservice, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="66f0e-233">**tooassign Britta Simon tooFreshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="66f0e-234">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="66f0e-236">En la lista de aplicaciones de hello, seleccione **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-236">In hello applications list, select **Freshservice**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. <span data-ttu-id="66f0e-238">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="66f0e-240">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-240">Click **Add** button.</span></span> <span data-ttu-id="66f0e-241">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="66f0e-243">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="66f0e-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="66f0e-244">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="66f0e-245">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="66f0e-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="66f0e-246">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="66f0e-246">Testing single sign-on</span></span>

<span data-ttu-id="66f0e-247">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="66f0e-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="66f0e-248">Al hacer clic en icono de Freshservice Hola Hola Panel de acceso, deberá obtener aplicaciones de Freshservice tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="66f0e-248">When you click hello Freshservice tile in hello Access Panel, you should get automatically signed-on tooyour Freshservice application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="66f0e-249">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="66f0e-249">Additional resources</span></span>

* [<span data-ttu-id="66f0e-250">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="66f0e-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="66f0e-251">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="66f0e-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

