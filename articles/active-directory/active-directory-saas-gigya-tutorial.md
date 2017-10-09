---
title: "Tutorial: Integración de Azure Active Directory con Gigya | Microsoft Doc"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Gigya."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 1992c5ad09b097563377a488fbf5a375f6511020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a><span data-ttu-id="3586b-103">Tutorial: integración de Azure Active Directory con Gigya</span><span class="sxs-lookup"><span data-stu-id="3586b-103">Tutorial: Azure Active Directory integration with Gigya</span></span>

<span data-ttu-id="3586b-104">En este tutorial, aprenderá cómo toointegrate Gigya con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3586b-104">In this tutorial, you learn how toointegrate Gigya with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3586b-105">Integración de Gigya con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3586b-105">Integrating Gigya with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3586b-106">Puede controlar en Azure AD que tenga acceso tooGigya</span><span class="sxs-lookup"><span data-stu-id="3586b-106">You can control in Azure AD who has access tooGigya</span></span>
- <span data-ttu-id="3586b-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooGigya (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3586b-107">You can enable your users tooautomatically get signed-on tooGigya (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3586b-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3586b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3586b-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3586b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3586b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3586b-110">Prerequisites</span></span>

<span data-ttu-id="3586b-111">integración de Azure AD con Gigya tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3586b-111">tooconfigure Azure AD integration with Gigya, you need hello following items:</span></span>

- <span data-ttu-id="3586b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3586b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3586b-113">Una suscripción habilitada para el inicio de sesión único en Gigya</span><span class="sxs-lookup"><span data-stu-id="3586b-113">A Gigya single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3586b-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3586b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3586b-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3586b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3586b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3586b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3586b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3586b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3586b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3586b-118">Scenario description</span></span>
<span data-ttu-id="3586b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3586b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3586b-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="3586b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3586b-121">Agregar Gigya desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="3586b-121">Adding Gigya from hello gallery</span></span>
2. <span data-ttu-id="3586b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3586b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gigya-from-hello-gallery"></a><span data-ttu-id="3586b-123">Agregar Gigya desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="3586b-123">Adding Gigya from hello gallery</span></span>
<span data-ttu-id="3586b-124">integración de hello tooconfigure de Gigya en Azure AD, deberá tooadd Gigya de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="3586b-124">tooconfigure hello integration of Gigya into Azure AD, you need tooadd Gigya from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3586b-125">**tooadd Gigya de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3586b-125">**tooadd Gigya from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3586b-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="3586b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3586b-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3586b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3586b-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3586b-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="3586b-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3586b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="3586b-133">En el cuadro de búsqueda de hello, escriba **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="3586b-133">In hello search box, type **Gigya**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_search.png)

5. <span data-ttu-id="3586b-135">En el panel de resultados de hello, seleccione **Gigya**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3586b-135">In hello results panel, select **Gigya**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3586b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3586b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3586b-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Gigya con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3586b-138">In this section, you configure and test Azure AD single sign-on with Gigya based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3586b-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Gigya es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3586b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Gigya is tooa user in Azure AD.</span></span> <span data-ttu-id="3586b-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Gigya debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="3586b-140">In other words, a link relationship between an Azure AD user and hello related user in Gigya needs toobe established.</span></span>

<span data-ttu-id="3586b-141">En Gigya, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3586b-141">In Gigya, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3586b-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Gigya, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3586b-142">tooconfigure and test Azure AD single sign-on with Gigya, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3586b-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="3586b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3586b-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3586b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3586b-145">**[Crear un usuario de prueba de Gigya](#creating-a-gigya-test-user)**  -toohave un equivalente de Britta Simon en Gigya que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="3586b-145">**[Creating a Gigya test user](#creating-a-gigya-test-user)** - toohave a counterpart of Britta Simon in Gigya that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3586b-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3586b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3586b-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3586b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3586b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3586b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3586b-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Gigya.</span><span class="sxs-lookup"><span data-stu-id="3586b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Gigya application.</span></span>

<span data-ttu-id="3586b-150">**inicio de sesión único en Azure AD tooconfigure con Gigya, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3586b-150">**tooconfigure Azure AD single sign-on with Gigya, perform hello following steps:**</span></span>

1. <span data-ttu-id="3586b-151">En el portal de Azure, en Hola Hola **Gigya** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3586b-151">In hello Azure portal, on hello **Gigya** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="3586b-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3586b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_samlbase.png)

3. <span data-ttu-id="3586b-155">En hello **Gigya dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3586b-155">On hello **Gigya Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_url.png)

    <span data-ttu-id="3586b-157">a.</span><span class="sxs-lookup"><span data-stu-id="3586b-157">a.</span></span> <span data-ttu-id="3586b-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`http://<companyname>.gigya.com`</span><span class="sxs-lookup"><span data-stu-id="3586b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<companyname>.gigya.com`</span></span>

    <span data-ttu-id="3586b-159">b.</span><span class="sxs-lookup"><span data-stu-id="3586b-159">b.</span></span> <span data-ttu-id="3586b-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://fidm.gigya.com/saml/v2.0/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="3586b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3586b-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="3586b-161">These values are not real.</span></span> <span data-ttu-id="3586b-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="3586b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3586b-163">Póngase en contacto con [equipo de soporte técnico de cliente de Gigya](https://www.gigya.com/support-policy/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="3586b-163">Contact [Gigya Client support team](https://www.gigya.com/support-policy/) tooget these values.</span></span> 
 
4. <span data-ttu-id="3586b-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3586b-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_certificate.png) 

5. <span data-ttu-id="3586b-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3586b-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gigya-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3586b-168">En hello **configuración de Gigya** sección, haga clic en **configurar Gigya** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="3586b-168">On hello **Gigya Configuration** section, click **Configure Gigya** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3586b-169">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="3586b-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_configure.png) 

7. <span data-ttu-id="3586b-171">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de Gigya como administrador.</span><span class="sxs-lookup"><span data-stu-id="3586b-171">In a different web browser window, log into your Gigya company site as an administrator.</span></span>

8. <span data-ttu-id="3586b-172">Vaya demasiado**configuración \> inicio de sesión SAML**y, a continuación, haga clic en hello **agregar** botón.</span><span class="sxs-lookup"><span data-stu-id="3586b-172">Go too**Settings \> SAML Login**, and then click hello **Add** button.</span></span>
   
    <span data-ttu-id="3586b-173">![Inicio de sesión SAML](./media/active-directory-saas-gigya-tutorial/ic789532.png "Inicio de sesión SAML")</span><span class="sxs-lookup"><span data-stu-id="3586b-173">![SAML Login](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML Login")</span></span>

9. <span data-ttu-id="3586b-174">Hola **inicio de sesión SAML** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3586b-174">In hello **SAML Login** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="3586b-175">![Configuración de SAML](./media/active-directory-saas-gigya-tutorial/ic789533.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="3586b-175">![SAML Configuration](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML Configuration")</span></span>
   
    <span data-ttu-id="3586b-176">a.</span><span class="sxs-lookup"><span data-stu-id="3586b-176">a.</span></span> <span data-ttu-id="3586b-177">Hola **nombre** cuadro de texto, escriba un nombre para la configuración.</span><span class="sxs-lookup"><span data-stu-id="3586b-177">In hello **Name** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="3586b-178">b.</span><span class="sxs-lookup"><span data-stu-id="3586b-178">b.</span></span> <span data-ttu-id="3586b-179">En **emisor** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3586b-179">In **Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure Portal.</span></span> 
   
    <span data-ttu-id="3586b-180">c.</span><span class="sxs-lookup"><span data-stu-id="3586b-180">c.</span></span> <span data-ttu-id="3586b-181">En **URL de servicio de inicio de sesión único** cuadro de texto, pegue Hola valo **URL de servicio de inicio de sesión único** que haya copiado desde el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3586b-181">In **Single Sign-On Service URL** textbox, paste hello value of **Single Sign-On Service URL** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="3586b-182">d.</span><span class="sxs-lookup"><span data-stu-id="3586b-182">d.</span></span> <span data-ttu-id="3586b-183">En **formato de Id. de nombre** cuadro de texto, pegue Hola valo **formato de nombre de identificador** que haya copiado desde el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3586b-183">In **Name ID Format** textbox, paste hello value of **Name Identifier Format** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="3586b-184">e.</span><span class="sxs-lookup"><span data-stu-id="3586b-184">e.</span></span> <span data-ttu-id="3586b-185">Abra el certificado codificado en base 64 en el Bloc de notas que se descarga desde el portal de Azure, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado X.509** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3586b-185">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="3586b-186">f.</span><span class="sxs-lookup"><span data-stu-id="3586b-186">f.</span></span> <span data-ttu-id="3586b-187">Haga clic en **Guardar configuración**.</span><span class="sxs-lookup"><span data-stu-id="3586b-187">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="3586b-188">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="3586b-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3586b-189">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="3586b-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3586b-190">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3586b-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3586b-191">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3586b-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="3586b-192">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="3586b-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="3586b-194">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3586b-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3586b-195">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="3586b-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3586b-197">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3586b-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3586b-199">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3586b-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3586b-201">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="3586b-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3586b-203">a.</span><span class="sxs-lookup"><span data-stu-id="3586b-203">a.</span></span> <span data-ttu-id="3586b-204">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3586b-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3586b-205">b.</span><span class="sxs-lookup"><span data-stu-id="3586b-205">b.</span></span> <span data-ttu-id="3586b-206">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3586b-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3586b-207">c.</span><span class="sxs-lookup"><span data-stu-id="3586b-207">c.</span></span> <span data-ttu-id="3586b-208">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3586b-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3586b-209">d.</span><span class="sxs-lookup"><span data-stu-id="3586b-209">d.</span></span> <span data-ttu-id="3586b-210">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3586b-210">Click **Create**.</span></span>
 
### <a name="creating-a-gigya-test-user"></a><span data-ttu-id="3586b-211">Creación de usuario de prueba de Gigya</span><span class="sxs-lookup"><span data-stu-id="3586b-211">Creating a Gigya test user</span></span>

<span data-ttu-id="3586b-212">En orden tooenable toolog de los usuarios de Azure AD en Gigya, se les deben aprovisionar en Gigya.</span><span class="sxs-lookup"><span data-stu-id="3586b-212">In order tooenable Azure AD users toolog into Gigya, they must be provisioned into Gigya.</span></span>  
<span data-ttu-id="3586b-213">En caso de hello de Gigya, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="3586b-213">In hello case of Gigya, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="3586b-214">tooprovision una cuenta de usuario, realizar Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3586b-214">tooprovision a user accounts, perform hello following steps:</span></span>

1. <span data-ttu-id="3586b-215">Inicie sesión en tooyour **Gigya** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="3586b-215">Log in tooyour **Gigya** company site as an administrator.</span></span>

2. <span data-ttu-id="3586b-216">Vaya demasiado**administración \> administrar usuarios**y, a continuación, haga clic en **invitar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3586b-216">Go too**Admin \> Manage Users**, and then click **Invite Users**.</span></span>
   
    <span data-ttu-id="3586b-217">![Administración de usuarios](./media/active-directory-saas-gigya-tutorial/ic789535.png "Administración de usuarios")</span><span class="sxs-lookup"><span data-stu-id="3586b-217">![Manage Users](./media/active-directory-saas-gigya-tutorial/ic789535.png "Manage Users")</span></span>

3. <span data-ttu-id="3586b-218">En cuadro de diálogo Invitar usuarios de hello realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3586b-218">On hello Invite Users dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="3586b-219">![Invitación de usuarios](./media/active-directory-saas-gigya-tutorial/ic789536.png "Invitación de usuarios")</span><span class="sxs-lookup"><span data-stu-id="3586b-219">![Invite Users](./media/active-directory-saas-gigya-tutorial/ic789536.png "Invite Users")</span></span>
   
    <span data-ttu-id="3586b-220">a.</span><span class="sxs-lookup"><span data-stu-id="3586b-220">a.</span></span> <span data-ttu-id="3586b-221">Hola **correo electrónico** cuadro de texto, alias de correo electrónico de tipo hello de una cuenta válida de Azure Active Directory que desee tooprovision.</span><span class="sxs-lookup"><span data-stu-id="3586b-221">In hello **Email** textbox, type hello email alias of a valid Azure Active Directory account you want tooprovision.</span></span>
    
    <span data-ttu-id="3586b-222">b.</span><span class="sxs-lookup"><span data-stu-id="3586b-222">b.</span></span> <span data-ttu-id="3586b-223">Haga clic en **Invitar a usuario**.</span><span class="sxs-lookup"><span data-stu-id="3586b-223">Click **Invite User**.</span></span>
      
    > [!NOTE]
    > <span data-ttu-id="3586b-224">titular de la cuenta de Hello Azure Active Directory recibirá un correo electrónico que incluye una cuenta de hello tooconfirm vínculo antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="3586b-224">hello Azure Active Directory account holder will receive an email that includes a link tooconfirm hello account before it becomes active.</span></span>
    > 
    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3586b-225">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3586b-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3586b-226">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooGigya.</span><span class="sxs-lookup"><span data-stu-id="3586b-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGigya.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3586b-228">**tooassign Britta Simon tooGigya, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3586b-228">**tooassign Britta Simon tooGigya, perform hello following steps:**</span></span>

1. <span data-ttu-id="3586b-229">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3586b-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3586b-231">En la lista de aplicaciones de hello, seleccione **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="3586b-231">In hello applications list, select **Gigya**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_app.png) 

3. <span data-ttu-id="3586b-233">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3586b-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3586b-235">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3586b-235">Click **Add** button.</span></span> <span data-ttu-id="3586b-236">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3586b-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3586b-238">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="3586b-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3586b-239">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3586b-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3586b-240">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3586b-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3586b-241">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3586b-241">Testing single sign-on</span></span>

<span data-ttu-id="3586b-242">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3586b-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="3586b-243">Al hacer clic en icono de Gigya Hola Hola Panel de acceso, deberá obtener aplicaciones de Gigya tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="3586b-243">When you click hello Gigya tile in hello Access Panel, you should get automatically signed-on tooyour Gigya application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3586b-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3586b-244">Additional resources</span></span>

* [<span data-ttu-id="3586b-245">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3586b-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3586b-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3586b-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_203.png

