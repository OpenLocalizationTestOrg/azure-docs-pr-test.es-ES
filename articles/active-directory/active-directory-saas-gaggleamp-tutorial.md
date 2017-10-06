---
title: "Tutorial: Integración de Azure Active Directory con GaggleAMP | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y GaggleAMP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9cc1a4b7-964b-406b-9e0c-05cb1a7c9856
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9761019a79f935b6695a5ae1214c256c887df457
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gaggleamp"></a><span data-ttu-id="5b82f-103">Tutorial: integración de Azure Active Directory con GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="5b82f-103">Tutorial: Azure Active Directory integration with GaggleAMP</span></span>

<span data-ttu-id="5b82f-104">En este tutorial, aprenderá cómo toointegrate GaggleAMP con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5b82f-104">In this tutorial, you learn how toointegrate GaggleAMP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b82f-105">Integración GaggleAMP con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="5b82f-105">Integrating GaggleAMP with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5b82f-106">Puede controlar en Azure AD que tenga acceso tooGaggleAMP</span><span class="sxs-lookup"><span data-stu-id="5b82f-106">You can control in Azure AD who has access tooGaggleAMP</span></span>
- <span data-ttu-id="5b82f-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooGaggleAMP (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b82f-107">You can enable your users tooautomatically get signed-on tooGaggleAMP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5b82f-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5b82f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5b82f-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5b82f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b82f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5b82f-110">Prerequisites</span></span>

<span data-ttu-id="5b82f-111">integración de Azure AD con GaggleAMP tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="5b82f-111">tooconfigure Azure AD integration with GaggleAMP, you need hello following items:</span></span>

- <span data-ttu-id="5b82f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b82f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b82f-113">Una suscripción habilitada para inicio de sesión único en GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="5b82f-113">A GaggleAMP single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5b82f-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="5b82f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5b82f-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="5b82f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b82f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="5b82f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5b82f-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b82f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5b82f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="5b82f-118">Scenario description</span></span>
<span data-ttu-id="5b82f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="5b82f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b82f-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="5b82f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b82f-121">Agregar GaggleAMP desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="5b82f-121">Adding GaggleAMP from hello gallery</span></span>
2. <span data-ttu-id="5b82f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b82f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gaggleamp-from-hello-gallery"></a><span data-ttu-id="5b82f-123">Agregar GaggleAMP desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="5b82f-123">Adding GaggleAMP from hello gallery</span></span>
<span data-ttu-id="5b82f-124">integración de hello tooconfigure de GaggleAMP en Azure AD, deberá tooadd GaggleAMP de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="5b82f-124">tooconfigure hello integration of GaggleAMP into Azure AD, you need tooadd GaggleAMP from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5b82f-125">**tooadd GaggleAMP de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5b82f-125">**tooadd GaggleAMP from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b82f-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="5b82f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5b82f-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="5b82f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5b82f-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5b82f-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="5b82f-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5b82f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="5b82f-133">En el cuadro de búsqueda de hello, escriba **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="5b82f-133">In hello search box, type **GaggleAMP**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_search.png)

5. <span data-ttu-id="5b82f-135">En el panel de resultados de hello, seleccione **GaggleAMP**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5b82f-135">In hello results panel, select **GaggleAMP**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5b82f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b82f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5b82f-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con GaggleAMP con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5b82f-138">In this section, you configure and test Azure AD single sign-on with GaggleAMP based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5b82f-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en GaggleAMP es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b82f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in GaggleAMP is tooa user in Azure AD.</span></span> <span data-ttu-id="5b82f-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en GaggleAMP debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="5b82f-140">In other words, a link relationship between an Azure AD user and hello related user in GaggleAMP needs toobe established.</span></span>

<span data-ttu-id="5b82f-141">En GaggleAMP, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b82f-141">In GaggleAMP, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5b82f-142">tooconfigure y prueba de inicio de sesión único en Azure AD con GaggleAMP, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="5b82f-142">tooconfigure and test Azure AD single sign-on with GaggleAMP, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5b82f-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="5b82f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5b82f-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b82f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b82f-145">**[Crear un usuario de prueba GaggleAMP](#creating-a-gaggleamp-test-user)**  -toohave un equivalente de Britta Simon en GaggleAMP que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="5b82f-145">**[Creating a GaggleAMP test user](#creating-a-gaggleamp-test-user)** - toohave a counterpart of Britta Simon in GaggleAMP that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5b82f-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5b82f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5b82f-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="5b82f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5b82f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b82f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5b82f-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="5b82f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your GaggleAMP application.</span></span>

<span data-ttu-id="5b82f-150">**inicio de sesión único en Azure AD tooconfigure con GaggleAMP, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5b82f-150">**tooconfigure Azure AD single sign-on with GaggleAMP, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b82f-151">En el portal de Azure, en Hola Hola **GaggleAMP** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="5b82f-151">In hello Azure portal, on hello **GaggleAMP** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="5b82f-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5b82f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_samlbase.png)

3. <span data-ttu-id="5b82f-155">En hello **GaggleAMP dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="5b82f-155">On hello **GaggleAMP Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_url.png)

     <span data-ttu-id="5b82f-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.gaggleamp.com`</span><span class="sxs-lookup"><span data-stu-id="5b82f-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.gaggleamp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5b82f-158">valor de Hello no es real.</span><span class="sxs-lookup"><span data-stu-id="5b82f-158">hello value is not real.</span></span> <span data-ttu-id="5b82f-159">Valor de Hola de actualización con Hola dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="5b82f-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="5b82f-160">Póngase en contacto con [equipo de soporte técnico de GaggleAMP cliente](mailto:sales@gaggleamp.com) valor de hello tooget.</span><span class="sxs-lookup"><span data-stu-id="5b82f-160">Contact [GaggleAMP Client support team](mailto:sales@gaggleamp.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="5b82f-161">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="5b82f-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_certificate.png) 

5. <span data-ttu-id="5b82f-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="5b82f-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5b82f-165">En hello **GaggleAMP configuración** sección, haga clic en **configurar GaggleAMP** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="5b82f-165">On hello **GaggleAMP Configuration** section, click **Configure GaggleAMP** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5b82f-166">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="5b82f-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_configure.png) 

7. <span data-ttu-id="5b82f-168">En otra instancia del explorador, navegue toohello página de SSO de SAML creado para usted Hola conjunto equipo de soporte técnico (por ejemplo: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span><span class="sxs-lookup"><span data-stu-id="5b82f-168">In another browser instance, navigate toohello SAML SSO page created for you by hello Gaggle support team (for example: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span></span>

8. <span data-ttu-id="5b82f-169">En su **SSO de SAML** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="5b82f-169">On your **SAML SSO** page, perform hello following steps:</span></span>  
   
    ![Inicio de sesión único de GaggleAMP](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_06.png) 
 
    <span data-ttu-id="5b82f-171">a.</span><span class="sxs-lookup"><span data-stu-id="5b82f-171">a.</span></span> <span data-ttu-id="5b82f-172">Hola **emisor del proveedor de identidades** cuadro de texto, pegue Hola valo **dirección URL del emisor** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b82f-172">In hello **Identity Provider Issuer** textbox, paste hello value of **Issuer URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="5b82f-173">b.</span><span class="sxs-lookup"><span data-stu-id="5b82f-173">b.</span></span> <span data-ttu-id="5b82f-174">Hola **URL proveedor de identidades Single Sign-On** cuadro de texto, pegue Hola valo **URL de servicio de inicio de sesión único** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b82f-174">In hello **Identity Provider Single Sign-On URL** textbox, paste hello  value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="5b82f-175">c.</span><span class="sxs-lookup"><span data-stu-id="5b82f-175">c.</span></span> <span data-ttu-id="5b82f-176">Haga clic en **Guardar**</span><span class="sxs-lookup"><span data-stu-id="5b82f-176">Click **Save**</span></span>      

    <span data-ttu-id="5b82f-177">d.</span><span class="sxs-lookup"><span data-stu-id="5b82f-177">d.</span></span> <span data-ttu-id="5b82f-178">Enviar hello **certificado (Base64)** certificado tooyour [equipo de soporte técnico de GaggleAMP](mailto:sales@gaggleamp.com).</span><span class="sxs-lookup"><span data-stu-id="5b82f-178">Send hello **Certificate (Base64)** certificate tooyour [GaggleAMP support team](mailto:sales@gaggleamp.com).</span></span>

> [!TIP]
> <span data-ttu-id="5b82f-179">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="5b82f-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5b82f-180">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="5b82f-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5b82f-181">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5b82f-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5b82f-182">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b82f-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="5b82f-183">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="5b82f-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="5b82f-185">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5b82f-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b82f-186">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="5b82f-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5b82f-188">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5b82f-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5b82f-190">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b82f-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5b82f-192">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="5b82f-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5b82f-194">a.</span><span class="sxs-lookup"><span data-stu-id="5b82f-194">a.</span></span> <span data-ttu-id="5b82f-195">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5b82f-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b82f-196">b.</span><span class="sxs-lookup"><span data-stu-id="5b82f-196">b.</span></span> <span data-ttu-id="5b82f-197">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5b82f-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5b82f-198">c.</span><span class="sxs-lookup"><span data-stu-id="5b82f-198">c.</span></span> <span data-ttu-id="5b82f-199">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="5b82f-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5b82f-200">d.</span><span class="sxs-lookup"><span data-stu-id="5b82f-200">d.</span></span> <span data-ttu-id="5b82f-201">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5b82f-201">Click **Create**.</span></span>
 
### <a name="creating-a-gaggleamp-test-user"></a><span data-ttu-id="5b82f-202">Creación de un usuario de prueba de GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="5b82f-202">Creating a GaggleAMP test user</span></span>

<span data-ttu-id="5b82f-203">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en GaggleAMP toocreate.</span><span class="sxs-lookup"><span data-stu-id="5b82f-203">hello objective of this section is toocreate a user called Britta Simon in GaggleAMP.</span></span> <span data-ttu-id="5b82f-204">GaggleAMP admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5b82f-204">GaggleAMP supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="5b82f-205">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="5b82f-205">There is no action item for you in this section.</span></span> <span data-ttu-id="5b82f-206">Se crea un nuevo usuario durante un tooaccess intento GaggleAMP si no existe todavía.</span><span class="sxs-lookup"><span data-stu-id="5b82f-206">A new user is created during an attempt tooaccess GaggleAMP if it doesn't exist yet.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5b82f-207">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b82f-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5b82f-208">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooGaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="5b82f-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGaggleAMP.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="5b82f-210">**tooassign Britta Simon tooGaggleAMP, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5b82f-210">**tooassign Britta Simon tooGaggleAMP, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b82f-211">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5b82f-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="5b82f-213">En la lista de aplicaciones de hello, seleccione **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="5b82f-213">In hello applications list, select **GaggleAMP**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_app.png) 

3. <span data-ttu-id="5b82f-215">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5b82f-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="5b82f-217">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5b82f-217">Click **Add** button.</span></span> <span data-ttu-id="5b82f-218">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5b82f-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="5b82f-220">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b82f-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5b82f-221">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5b82f-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b82f-222">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5b82f-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5b82f-223">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="5b82f-223">Testing single sign-on</span></span>

<span data-ttu-id="5b82f-224">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="5b82f-224">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="5b82f-225">Al hacer clic en icono de GaggleAMP Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour GaggleAMP aplicación.</span><span class="sxs-lookup"><span data-stu-id="5b82f-225">When you click hello GaggleAMP tile in hello Access Panel, you should get automatically signed-on tooyour GaggleAMP application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5b82f-226">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="5b82f-226">Additional resources</span></span>

* [<span data-ttu-id="5b82f-227">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b82f-227">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b82f-228">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5b82f-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_203.png

