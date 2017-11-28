---
title: "Tutorial: integración de Azure Active Directory con Egnyte | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Egnyte."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: d86fa28a1e7b23474cb76c08aef8539acadaf24d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="27d69-103">Tutorial: integración de Azure Active Directory con Egnyte</span><span class="sxs-lookup"><span data-stu-id="27d69-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>

<span data-ttu-id="27d69-104">En este tutorial, aprenderá cómo toointegrate Egnyte con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="27d69-104">In this tutorial, you learn how toointegrate Egnyte with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="27d69-105">Integración de Egnyte con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="27d69-105">Integrating Egnyte with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="27d69-106">Puede controlar en Azure AD que tenga acceso tooEgnyte</span><span class="sxs-lookup"><span data-stu-id="27d69-106">You can control in Azure AD who has access tooEgnyte</span></span>
- <span data-ttu-id="27d69-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooEgnyte (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27d69-107">You can enable your users tooautomatically get signed-on tooEgnyte (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="27d69-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="27d69-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="27d69-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="27d69-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27d69-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="27d69-110">Prerequisites</span></span>

<span data-ttu-id="27d69-111">integración de Azure AD con Egnyte tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="27d69-111">tooconfigure Azure AD integration with Egnyte, you need hello following items:</span></span>

- <span data-ttu-id="27d69-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27d69-112">An Azure AD subscription</span></span>
- <span data-ttu-id="27d69-113">Una suscripción habilitada para el inicio de sesión único en Egnyte</span><span class="sxs-lookup"><span data-stu-id="27d69-113">An Egnyte single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="27d69-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="27d69-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="27d69-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="27d69-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="27d69-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="27d69-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="27d69-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="27d69-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="27d69-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="27d69-118">Scenario description</span></span>
<span data-ttu-id="27d69-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="27d69-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="27d69-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="27d69-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="27d69-121">Agregar Egnyte desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="27d69-121">Adding Egnyte from hello gallery</span></span>
2. <span data-ttu-id="27d69-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27d69-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-egnyte-from-hello-gallery"></a><span data-ttu-id="27d69-123">Agregar Egnyte desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="27d69-123">Adding Egnyte from hello gallery</span></span>
<span data-ttu-id="27d69-124">integración de hello tooconfigure de Egnyte en Azure AD, deberá tooadd Egnyte de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="27d69-124">tooconfigure hello integration of Egnyte into Azure AD, you need tooadd Egnyte from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="27d69-125">**tooadd Egnyte de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="27d69-125">**tooadd Egnyte from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="27d69-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="27d69-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="27d69-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="27d69-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="27d69-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="27d69-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="27d69-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27d69-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="27d69-133">En el cuadro de búsqueda de hello, escriba **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="27d69-133">In hello search box, type **Egnyte**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. <span data-ttu-id="27d69-135">En el panel de resultados de hello, seleccione **Egnyte**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="27d69-135">In hello results panel, select **Egnyte**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="27d69-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27d69-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="27d69-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Egnyte con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="27d69-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="27d69-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Egnyte es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="27d69-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Egnyte is tooa user in Azure AD.</span></span> <span data-ttu-id="27d69-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Egnyte debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="27d69-140">In other words, a link relationship between an Azure AD user and hello related user in Egnyte needs toobe established.</span></span>

<span data-ttu-id="27d69-141">En Egnyte, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="27d69-141">In Egnyte, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="27d69-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Egnyte, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="27d69-142">tooconfigure and test Azure AD single sign-on with Egnyte, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="27d69-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="27d69-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="27d69-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="27d69-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="27d69-145">**[Creación de un usuario de prueba de Egnyte](#creating-an-egnyte-test-user)**  -toohave un equivalente de Britta Simon en Egnyte que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="27d69-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - toohave a counterpart of Britta Simon in Egnyte that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="27d69-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="27d69-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="27d69-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="27d69-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="27d69-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27d69-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="27d69-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Egnyte.</span><span class="sxs-lookup"><span data-stu-id="27d69-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Egnyte application.</span></span>

<span data-ttu-id="27d69-150">**inicio de sesión único en Azure AD tooconfigure con Egnyte, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="27d69-150">**tooconfigure Azure AD single sign-on with Egnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="27d69-151">En el portal de Azure, en Hola Hola **Egnyte** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="27d69-151">In hello Azure portal, on hello **Egnyte** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="27d69-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="27d69-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. <span data-ttu-id="27d69-155">En hello **Egnyte dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="27d69-155">On hello **Egnyte Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    <span data-ttu-id="27d69-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.egnyte.com`</span><span class="sxs-lookup"><span data-stu-id="27d69-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.egnyte.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="27d69-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="27d69-158">This value is not real.</span></span> <span data-ttu-id="27d69-159">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="27d69-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="27d69-160">Póngase en contacto con [equipo de soporte técnico de cliente de Egnyte](https://www.egnyte.com/corp/contact_egnyte.html) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="27d69-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="27d69-161">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="27d69-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. <span data-ttu-id="27d69-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="27d69-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="27d69-165">En hello **configuración de Egnyte** sección, haga clic en **configurar Egnyte** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="27d69-165">On hello **Egnyte Configuration** section, click **Configure Egnyte** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="27d69-166">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="27d69-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. <span data-ttu-id="27d69-168">En una ventana del explorador web diferente, inicie sesión en el sitio de la empresa tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="27d69-168">In a different web browser window, log in tooyour Egnyte company site as an administrator.</span></span>

8. <span data-ttu-id="27d69-169">Haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="27d69-169">Click **Settings**.</span></span>
   
   <span data-ttu-id="27d69-170">![Configuración](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="27d69-170">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Settings")</span></span>

9. <span data-ttu-id="27d69-171">En el menú de hello, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="27d69-171">In hello menu, click **Settings**.</span></span>

   <span data-ttu-id="27d69-172">![Configuración](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="27d69-172">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Settings")</span></span>

10. <span data-ttu-id="27d69-173">Haga clic en hello **configuración** ficha y, a continuación, haga clic en **seguridad**.</span><span class="sxs-lookup"><span data-stu-id="27d69-173">Click hello **Configuration** tab, and then click **Security**.</span></span>

    <span data-ttu-id="27d69-174">![Seguridad](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Seguridad")</span><span class="sxs-lookup"><span data-stu-id="27d69-174">![Security](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Security")</span></span>

11. <span data-ttu-id="27d69-175">Hola **autenticación de inicio de sesión único** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="27d69-175">In hello **Single Sign-On Authentication** section, perform hello following steps:</span></span>

    <span data-ttu-id="27d69-176">![Autenticación de inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Autenticación de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="27d69-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span></span>   
    
    <span data-ttu-id="27d69-177">a.</span><span class="sxs-lookup"><span data-stu-id="27d69-177">a.</span></span> <span data-ttu-id="27d69-178">En **Autenticación de inicio de sesión único**, seleccione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="27d69-178">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="27d69-179">b.</span><span class="sxs-lookup"><span data-stu-id="27d69-179">b.</span></span> <span data-ttu-id="27d69-180">En **Proveedor de identidades**, seleccione **AzureAD**.</span><span class="sxs-lookup"><span data-stu-id="27d69-180">As **Identity provider**, select **AzureAD**.</span></span>
   
    <span data-ttu-id="27d69-181">c.</span><span class="sxs-lookup"><span data-stu-id="27d69-181">c.</span></span> <span data-ttu-id="27d69-182">Pegar **SAML Single Sign-On dirección URL del servicio** copiados desde el portal de Azure en hello **URL de inicio de sesión del proveedor de identidades** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="27d69-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into hello **Identity provider login URL** textbox.</span></span>
   
    <span data-ttu-id="27d69-183">d.</span><span class="sxs-lookup"><span data-stu-id="27d69-183">d.</span></span> <span data-ttu-id="27d69-184">Pegar **Id. de entidad SAML** que haya copiado desde el portal de Azure en hello **Id. de entidad de proveedor de identidad** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="27d69-184">Paste **SAML Entity ID** which you have copied from Azure portal into hello **Identity provider entity ID** textbox.</span></span>
      
    <span data-ttu-id="27d69-185">e.</span><span class="sxs-lookup"><span data-stu-id="27d69-185">e.</span></span> <span data-ttu-id="27d69-186">Abra el certificado codificado en base 64 en el Bloc de notas que se descarga desde el portal de Azure, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado del proveedor de identidad** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="27d69-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>
   
    <span data-ttu-id="27d69-187">f.</span><span class="sxs-lookup"><span data-stu-id="27d69-187">f.</span></span> <span data-ttu-id="27d69-188">En **Asignación de usuario predeterminada**, seleccione **Dirección de correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="27d69-188">As **Default user mapping**, select **Email address**.</span></span>
   
    <span data-ttu-id="27d69-189">g.</span><span class="sxs-lookup"><span data-stu-id="27d69-189">g.</span></span> <span data-ttu-id="27d69-190">En **Usar valor de emisor específico del dominio**, seleccione **Deshabilitado**.</span><span class="sxs-lookup"><span data-stu-id="27d69-190">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   
    <span data-ttu-id="27d69-191">h.</span><span class="sxs-lookup"><span data-stu-id="27d69-191">h.</span></span> <span data-ttu-id="27d69-192">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="27d69-192">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="27d69-193">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="27d69-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="27d69-194">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="27d69-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="27d69-195">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="27d69-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="27d69-196">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27d69-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="27d69-197">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="27d69-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="27d69-199">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="27d69-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="27d69-200">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="27d69-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="27d69-202">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="27d69-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="27d69-204">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="27d69-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="27d69-206">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="27d69-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="27d69-208">a.</span><span class="sxs-lookup"><span data-stu-id="27d69-208">a.</span></span> <span data-ttu-id="27d69-209">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="27d69-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="27d69-210">b.</span><span class="sxs-lookup"><span data-stu-id="27d69-210">b.</span></span> <span data-ttu-id="27d69-211">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="27d69-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="27d69-212">c.</span><span class="sxs-lookup"><span data-stu-id="27d69-212">c.</span></span> <span data-ttu-id="27d69-213">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="27d69-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="27d69-214">d.</span><span class="sxs-lookup"><span data-stu-id="27d69-214">d.</span></span> <span data-ttu-id="27d69-215">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="27d69-215">Click **Create**.</span></span>
 
### <a name="creating-an-egnyte-test-user"></a><span data-ttu-id="27d69-216">Creación de un usuario de prueba de Egnyte</span><span class="sxs-lookup"><span data-stu-id="27d69-216">Creating an Egnyte test user</span></span>

<span data-ttu-id="27d69-217">toolog de los usuarios de Azure AD tooenable en tooEgnyte, se les deben aprovisionar en Egnyte.</span><span class="sxs-lookup"><span data-stu-id="27d69-217">tooenable Azure AD users toolog in tooEgnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="27d69-218">En caso de hello de Egnyte, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="27d69-218">In hello case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="27d69-219">**tooprovision una cuenta de usuario, realizar Hola lo siguiente:**</span><span class="sxs-lookup"><span data-stu-id="27d69-219">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="27d69-220">Inicie sesión en tooyour **Egnyte** como administrador.</span><span class="sxs-lookup"><span data-stu-id="27d69-220">Log in tooyour **Egnyte** company site as administrator.</span></span>

2. <span data-ttu-id="27d69-221">Vaya demasiado**configuración \> usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="27d69-221">Go too**Settings \> Users & Groups**.</span></span>

3. <span data-ttu-id="27d69-222">Haga clic en **Agregar nuevo usuario**y, a continuación, seleccione el tipo de saludo del usuario que desea tooadd.</span><span class="sxs-lookup"><span data-stu-id="27d69-222">Click **Add New User**, and then select hello type of user you want tooadd.</span></span>
   
   <span data-ttu-id="27d69-223">![Usuarios](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="27d69-223">![Users](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Users")</span></span>

4. <span data-ttu-id="27d69-224">Hola **nuevo usuario estándar** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="27d69-224">In hello **New Standard User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="27d69-225">![Nuevo usuario estándar](./media/active-directory-saas-egnyte-tutorial/ic787825.png "Nuevo usuario estándar")</span><span class="sxs-lookup"><span data-stu-id="27d69-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span></span>   

   <span data-ttu-id="27d69-226">a.</span><span class="sxs-lookup"><span data-stu-id="27d69-226">a.</span></span> <span data-ttu-id="27d69-227">Hola de tipo **correo electrónico**, **nombre de usuario**y otros detalles de una cuenta válida de Azure Active Directory que desee tooprovision.</span><span class="sxs-lookup"><span data-stu-id="27d69-227">Type hello **Email**, **Username**, and other details of a valid Azure Active Directory account you want tooprovision.</span></span>
   
   <span data-ttu-id="27d69-228">b.</span><span class="sxs-lookup"><span data-stu-id="27d69-228">b.</span></span> <span data-ttu-id="27d69-229">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="27d69-229">Click **Save**.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="27d69-230">titular de la cuenta de Hello Azure Active Directory recibirá un correo electrónico de notificación.</span><span class="sxs-lookup"><span data-stu-id="27d69-230">hello Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="27d69-231">Puede usar cualquier otra Egnyte usuario cuenta herramienta de creación o las API proporcionadas por Egnyte tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="27d69-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="27d69-232">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="27d69-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="27d69-233">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooEgnyte.</span><span class="sxs-lookup"><span data-stu-id="27d69-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEgnyte.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="27d69-235">**tooassign Britta Simon tooEgnyte, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="27d69-235">**tooassign Britta Simon tooEgnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="27d69-236">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="27d69-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="27d69-238">En la lista de aplicaciones de hello, seleccione **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="27d69-238">In hello applications list, select **Egnyte**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. <span data-ttu-id="27d69-240">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="27d69-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="27d69-242">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="27d69-242">Click **Add** button.</span></span> <span data-ttu-id="27d69-243">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="27d69-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="27d69-245">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="27d69-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="27d69-246">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="27d69-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="27d69-247">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="27d69-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="27d69-248">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="27d69-248">Testing single sign-on</span></span>

<span data-ttu-id="27d69-249">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="27d69-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="27d69-250">Al hacer clic en icono de Egnyte Hola Hola Panel de acceso, deberá obtener aplicaciones de Egnyte tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="27d69-250">When you click hello Egnyte tile in hello Access Panel, you should get automatically signed-on tooyour Egnyte application.</span></span>
<span data-ttu-id="27d69-251">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="27d69-251">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="27d69-252">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="27d69-252">Additional resources</span></span>

* [<span data-ttu-id="27d69-253">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="27d69-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="27d69-254">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="27d69-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

