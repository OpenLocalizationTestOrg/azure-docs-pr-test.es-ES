---
title: "Tutorial: Integración de Azure Active Directory con TeamSeer | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y TeamSeer."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 876d13e446115acd50b01c7f44db99357045e429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a><span data-ttu-id="e87a5-103">Tutorial: integración de Azure Active Directory con TeamSeer</span><span class="sxs-lookup"><span data-stu-id="e87a5-103">Tutorial: Azure Active Directory integration with TeamSeer</span></span>

<span data-ttu-id="e87a5-104">En este tutorial, aprenderá cómo toointegrate TeamSeer con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e87a5-104">In this tutorial, you learn how toointegrate TeamSeer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e87a5-105">Integración TeamSeer con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e87a5-105">Integrating TeamSeer with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e87a5-106">Puede controlar en Azure AD que tenga acceso tooTeamSeer</span><span class="sxs-lookup"><span data-stu-id="e87a5-106">You can control in Azure AD who has access tooTeamSeer</span></span>
- <span data-ttu-id="e87a5-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTeamSeer (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e87a5-107">You can enable your users tooautomatically get signed-on tooTeamSeer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e87a5-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e87a5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e87a5-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e87a5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e87a5-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e87a5-110">Prerequisites</span></span>

<span data-ttu-id="e87a5-111">integración de Azure AD con TeamSeer tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e87a5-111">tooconfigure Azure AD integration with TeamSeer, you need hello following items:</span></span>

- <span data-ttu-id="e87a5-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e87a5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e87a5-113">Una suscripción habilitada para el inicio de sesión único en TeamSeer</span><span class="sxs-lookup"><span data-stu-id="e87a5-113">A TeamSeer single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e87a5-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e87a5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e87a5-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e87a5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e87a5-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e87a5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e87a5-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e87a5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e87a5-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e87a5-118">Scenario description</span></span>
<span data-ttu-id="e87a5-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e87a5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e87a5-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="e87a5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e87a5-121">Agregar TeamSeer desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e87a5-121">Adding TeamSeer from hello gallery</span></span>
2. <span data-ttu-id="e87a5-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e87a5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamseer-from-hello-gallery"></a><span data-ttu-id="e87a5-123">Agregar TeamSeer desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e87a5-123">Adding TeamSeer from hello gallery</span></span>
<span data-ttu-id="e87a5-124">integración de hello tooconfigure de TeamSeer en tooAzure AD, deberá tooadd TeamSeer de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="e87a5-124">tooconfigure hello integration of TeamSeer in tooAzure AD, you need tooadd TeamSeer from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e87a5-125">**tooadd TeamSeer de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e87a5-125">**tooadd TeamSeer from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e87a5-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="e87a5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e87a5-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e87a5-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e87a5-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e87a5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e87a5-133">En el cuadro de búsqueda de hello, escriba **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-133">In hello search box, type **TeamSeer**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. <span data-ttu-id="e87a5-135">En el panel de resultados de hello, seleccione **TeamSeer**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e87a5-135">In hello results panel, select **TeamSeer**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e87a5-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e87a5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e87a5-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con TeamSeer con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e87a5-138">In this section, you configure and test Azure AD single sign-on with TeamSeer based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e87a5-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en TeamSeer es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e87a5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TeamSeer is tooa user in Azure AD.</span></span> <span data-ttu-id="e87a5-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en TeamSeer debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="e87a5-140">In other words, a link relationship between an Azure AD user and hello related user in TeamSeer needs toobe established.</span></span>

<span data-ttu-id="e87a5-141">En TeamSeer, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e87a5-141">In TeamSeer, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e87a5-142">tooconfigure y prueba de inicio de sesión único en Azure AD con TeamSeer, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e87a5-142">tooconfigure and test Azure AD single sign-on with TeamSeer, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e87a5-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="e87a5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e87a5-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e87a5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e87a5-145">**[Crear un usuario de prueba de TeamSeer](#creating-a-teamseer-test-user)**  -toohave un equivalente de Britta Simon en TeamSeer que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="e87a5-145">**[Creating a TeamSeer test user](#creating-a-teamseer-test-user)** - toohave a counterpart of Britta Simon in TeamSeer that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e87a5-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e87a5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e87a5-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e87a5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e87a5-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e87a5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e87a5-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="e87a5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TeamSeer application.</span></span>

<span data-ttu-id="e87a5-150">**inicio de sesión único en Azure AD tooconfigure con TeamSeer, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e87a5-150">**tooconfigure Azure AD single sign-on with TeamSeer, perform hello following steps:**</span></span>

1. <span data-ttu-id="e87a5-151">En el portal de Azure, en Hola Hola **TeamSeer** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-151">In hello Azure portal, on hello **TeamSeer** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e87a5-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e87a5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. <span data-ttu-id="e87a5-155">En hello **TeamSeer dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e87a5-155">On hello **TeamSeer Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     <span data-ttu-id="e87a5-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.teamseer.com/<companyid>`</span><span class="sxs-lookup"><span data-stu-id="e87a5-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.teamseer.com/<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e87a5-158">valor de Hello no es real.</span><span class="sxs-lookup"><span data-stu-id="e87a5-158">hello value is not real.</span></span> <span data-ttu-id="e87a5-159">Valor de Hola de actualización con Hola dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="e87a5-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="e87a5-160">Póngase en contacto con [equipo de soporte técnico de TeamSeer cliente](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) valor de hello tooget.</span><span class="sxs-lookup"><span data-stu-id="e87a5-160">Contact [TeamSeer Client support team](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) tooget hello value.</span></span> 
 
4. <span data-ttu-id="e87a5-161">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e87a5-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. <span data-ttu-id="e87a5-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e87a5-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e87a5-165">En hello **configuración de TeamSeer** sección, haga clic en **configurar TeamSeer** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="e87a5-165">On hello **TeamSeer Configuration** section, click **Configure TeamSeer** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e87a5-166">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="e87a5-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. <span data-ttu-id="e87a5-168">En una ventana del explorador web diferente, inicie sesión en el sitio de la compañía TeamSeer tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="e87a5-168">In a different web browser window, log in tooyour TeamSeer company site as an administrator.</span></span>

8. <span data-ttu-id="e87a5-169">Vaya demasiado**administración de recursos humanos**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-169">Go too**HR Admin**.</span></span>
   
    <span data-ttu-id="e87a5-170">![Administración de RR. HH.](./media/active-directory-saas-teamseer-tutorial/ic789634.png "Administración de RR. HH.")</span><span class="sxs-lookup"><span data-stu-id="e87a5-170">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR Admin")</span></span>

9. <span data-ttu-id="e87a5-171">Haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-171">Click **Setup**.</span></span>
   
    <span data-ttu-id="e87a5-172">![Instalación](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Instalación")</span><span class="sxs-lookup"><span data-stu-id="e87a5-172">![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")</span></span>

10. <span data-ttu-id="e87a5-173">Haga clic en **Configurar detalles del proveedor SAML**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-173">Click **Set up SAML provider details**.</span></span>
   
    <span data-ttu-id="e87a5-174">![Configuración de SAML](./media/active-directory-saas-teamseer-tutorial/ic789636.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="e87a5-174">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML Settings")</span></span>

11. <span data-ttu-id="e87a5-175">En la sección de detalles del proveedor SAML hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e87a5-175">In hello SAML provider details section, perform hello following steps:</span></span>
   
    <span data-ttu-id="e87a5-176">![Configuración de SAML](./media/active-directory-saas-teamseer-tutorial/ic789637.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="e87a5-176">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML Settings")</span></span>   

    <span data-ttu-id="e87a5-177">a.</span><span class="sxs-lookup"><span data-stu-id="e87a5-177">a.</span></span> <span data-ttu-id="e87a5-178">Hola pegar **URL de servicio de inicio de sesión único** valor en toohello **URL** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="e87a5-178">Paste hello **Single Sign-On Service URL** value in toohello **URL** textbox.</span></span>
          
    <span data-ttu-id="e87a5-179">b.</span><span class="sxs-lookup"><span data-stu-id="e87a5-179">b.</span></span> <span data-ttu-id="e87a5-180">Abra el certificado codificado en base 64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles de tooyour y, a continuación, péguelo toohello **certificado público IdP** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="e87a5-180">Open your base-64 encoded certificate in notepad, copy hello content of it in tooyour clipboard, and then paste it toohello **IdP Public Certificate** textbox.</span></span>

12. <span data-ttu-id="e87a5-181">Hola toocomplete configuración del proveedor SAML, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e87a5-181">toocomplete hello SAML provider configuration, perform hello following steps:</span></span>
    
    <span data-ttu-id="e87a5-182">![Configuración de SAML](./media/active-directory-saas-teamseer-tutorial/ic789638.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="e87a5-182">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML Settings")</span></span> 

    <span data-ttu-id="e87a5-183">a.</span><span class="sxs-lookup"><span data-stu-id="e87a5-183">a.</span></span> <span data-ttu-id="e87a5-184">Hola **direcciones de correo electrónico de prueba**, escriba la dirección de correo electrónico del usuario de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="e87a5-184">In hello **Test Email Addresses**, type hello test user’s email address.</span></span> 
  
    <span data-ttu-id="e87a5-185">b.</span><span class="sxs-lookup"><span data-stu-id="e87a5-185">b.</span></span> <span data-ttu-id="e87a5-186">Hola **emisor** cuadro de texto, hello de tipo dirección URL del emisor del proveedor de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="e87a5-186">In hello **Issuer** textbox, type hello Issuer URL of hello service provider.</span></span> 
  
    <span data-ttu-id="e87a5-187">c.</span><span class="sxs-lookup"><span data-stu-id="e87a5-187">c.</span></span> <span data-ttu-id="e87a5-188">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e87a5-189">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="e87a5-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e87a5-190">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="e87a5-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e87a5-191">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e87a5-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e87a5-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e87a5-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="e87a5-193">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="e87a5-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="e87a5-195">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e87a5-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e87a5-196">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="e87a5-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e87a5-198">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e87a5-200">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e87a5-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e87a5-202">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="e87a5-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e87a5-204">a.</span><span class="sxs-lookup"><span data-stu-id="e87a5-204">a.</span></span> <span data-ttu-id="e87a5-205">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e87a5-206">b.</span><span class="sxs-lookup"><span data-stu-id="e87a5-206">b.</span></span> <span data-ttu-id="e87a5-207">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e87a5-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e87a5-208">c.</span><span class="sxs-lookup"><span data-stu-id="e87a5-208">c.</span></span> <span data-ttu-id="e87a5-209">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e87a5-210">d.</span><span class="sxs-lookup"><span data-stu-id="e87a5-210">d.</span></span> <span data-ttu-id="e87a5-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-211">Click **Create**.</span></span>
 
### <a name="creating-a-teamseer-test-user"></a><span data-ttu-id="e87a5-212">Creación de un usuario de prueba de TeamSeer</span><span class="sxs-lookup"><span data-stu-id="e87a5-212">Creating a TeamSeer test user</span></span>

<span data-ttu-id="e87a5-213">toolog de los usuarios de Azure AD tooenable en tooTeamSeer, se les deben aprovisionar en tooShiftPlanning.</span><span class="sxs-lookup"><span data-stu-id="e87a5-213">tooenable Azure AD users toolog in tooTeamSeer, they must be provisioned in tooShiftPlanning.</span></span> <span data-ttu-id="e87a5-214">En caso de hello de TeamSeer, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="e87a5-214">In hello case of TeamSeer, provisioning is a manual task.</span></span>

<span data-ttu-id="e87a5-215">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e87a5-215">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="e87a5-216">Inicie sesión en tooyour **TeamSeer** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="e87a5-216">Log in tooyour **TeamSeer** company site as an administrator.</span></span>

2. <span data-ttu-id="e87a5-217">Lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e87a5-217">Perform hello following steps:</span></span>
   
    <span data-ttu-id="e87a5-218">![Administración de RR. HH.](./media/active-directory-saas-teamseer-tutorial/ic789640.png "Administración de RR. HH.")</span><span class="sxs-lookup"><span data-stu-id="e87a5-218">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR Admin")</span></span>  
 
    <span data-ttu-id="e87a5-219">a.</span><span class="sxs-lookup"><span data-stu-id="e87a5-219">a.</span></span> <span data-ttu-id="e87a5-220">Vaya demasiado**administración de recursos humanos \> usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-220">Go too**HR Admin \> Users**.</span></span>
  
    <span data-ttu-id="e87a5-221">b.</span><span class="sxs-lookup"><span data-stu-id="e87a5-221">b.</span></span> <span data-ttu-id="e87a5-222">Haga clic en **ejecutar el Asistente para nuevo usuario de hello**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-222">Click **Run hello New User wizard**.</span></span>

3. <span data-ttu-id="e87a5-223">Hola **detalles del usuario** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e87a5-223">In hello **User Details** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="e87a5-224">![Detalles del usuario](./media/active-directory-saas-teamseer-tutorial/ic789641.png "Detalles del usuario")</span><span class="sxs-lookup"><span data-stu-id="e87a5-224">![User Details](./media/active-directory-saas-teamseer-tutorial/ic789641.png "User Details")</span></span>

    <span data-ttu-id="e87a5-225">a.</span><span class="sxs-lookup"><span data-stu-id="e87a5-225">a.</span></span> <span data-ttu-id="e87a5-226">Hola de tipo **nombre**, **apellido**, **nombre de usuario (dirección de correo electrónico)** de una cuenta válida de AAD que desee tooprovision en toohello relacionados con cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="e87a5-226">Type hello **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want tooprovision in toohello related textboxes.</span></span>
  
    <span data-ttu-id="e87a5-227">b.</span><span class="sxs-lookup"><span data-stu-id="e87a5-227">b.</span></span> <span data-ttu-id="e87a5-228">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-228">Click **Next**.</span></span>

4. <span data-ttu-id="e87a5-229">Siga hello en pantalla instrucciones para agregar un nuevo usuario y haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-229">Follow hello on-screen instructions for adding a new user, and click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="e87a5-230">Puede usar cualquier otra TeamSeer usuario cuenta herramienta de creación o las API proporcionadas por TeamSeer tooprovision cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e87a5-230">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e87a5-231">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e87a5-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e87a5-232">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooTeamSeer.</span><span class="sxs-lookup"><span data-stu-id="e87a5-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTeamSeer.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="e87a5-234">**tooassign Britta Simon tooTeamSeer, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e87a5-234">**tooassign Britta Simon tooTeamSeer, perform hello following steps:**</span></span>

1. <span data-ttu-id="e87a5-235">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e87a5-237">En la lista de aplicaciones de hello, seleccione **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-237">In hello applications list, select **TeamSeer**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. <span data-ttu-id="e87a5-239">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="e87a5-241">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-241">Click **Add** button.</span></span> <span data-ttu-id="e87a5-242">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="e87a5-244">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="e87a5-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e87a5-245">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e87a5-246">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e87a5-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e87a5-247">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="e87a5-247">Testing single sign-on</span></span>

<span data-ttu-id="e87a5-248">Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e87a5-248">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="e87a5-249">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e87a5-249">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e87a5-250">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e87a5-250">Additional resources</span></span>

* [<span data-ttu-id="e87a5-251">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e87a5-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e87a5-252">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e87a5-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

