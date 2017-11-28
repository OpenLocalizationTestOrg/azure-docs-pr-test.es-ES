---
title: "Tutorial: Integración de Azure Active Directory con Sugar CRM | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Sugar CRM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 108d2f8125e410743ee7bc48883a1d0b00602615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a><span data-ttu-id="0bda1-103">Tutorial: Integración de Azure Active Directory con Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="0bda1-103">Tutorial: Azure Active Directory integration with Sugar CRM</span></span>

<span data-ttu-id="0bda1-104">En este tutorial, aprenderá cómo toointegrate Sugar CRM con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0bda1-104">In this tutorial, you learn how toointegrate Sugar CRM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0bda1-105">Integración de Sugar CRM con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0bda1-105">Integrating Sugar CRM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0bda1-106">Puede controlar en Azure AD que tenga acceso tooSugar CRM</span><span class="sxs-lookup"><span data-stu-id="0bda1-106">You can control in Azure AD who has access tooSugar CRM</span></span>
- <span data-ttu-id="0bda1-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSugar CRM (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0bda1-107">You can enable your users tooautomatically get signed-on tooSugar CRM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0bda1-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0bda1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0bda1-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0bda1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bda1-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0bda1-110">Prerequisites</span></span>

<span data-ttu-id="0bda1-111">tooconfigure integración de Azure AD con Sugar CRM, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0bda1-111">tooconfigure Azure AD integration with Sugar CRM, you need hello following items:</span></span>

- <span data-ttu-id="0bda1-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0bda1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0bda1-113">Un suscripción habilitada para el inicio de sesión único en SugarCRM</span><span class="sxs-lookup"><span data-stu-id="0bda1-113">A Sugar CRM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0bda1-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0bda1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0bda1-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0bda1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0bda1-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0bda1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0bda1-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0bda1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0bda1-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0bda1-118">Scenario description</span></span>
<span data-ttu-id="0bda1-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0bda1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0bda1-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="0bda1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0bda1-121">Agregar Sugar CRM desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="0bda1-121">Adding Sugar CRM from hello gallery</span></span>
2. <span data-ttu-id="0bda1-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0bda1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sugar-crm-from-hello-gallery"></a><span data-ttu-id="0bda1-123">Agregar Sugar CRM desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="0bda1-123">Adding Sugar CRM from hello gallery</span></span>
<span data-ttu-id="0bda1-124">integración de hello tooconfigure de Sugar CRM en Azure AD, deberá tooadd Sugar CRM de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="0bda1-124">tooconfigure hello integration of Sugar CRM into Azure AD, you need tooadd Sugar CRM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0bda1-125">**tooadd Sugar CRM de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0bda1-125">**tooadd Sugar CRM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bda1-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0bda1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0bda1-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0bda1-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0bda1-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0bda1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0bda1-133">En el cuadro de búsqueda de hello, escriba **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-133">In hello search box, type **Sugar CRM**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. <span data-ttu-id="0bda1-135">En el panel de resultados de hello, seleccione **Sugar CRM**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0bda1-135">In hello results panel, select **Sugar CRM**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0bda1-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0bda1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0bda1-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Sugar CRM con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0bda1-138">In this section, you configure and test Azure AD single sign-on with Sugar CRM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0bda1-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Sugar CRM es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0bda1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sugar CRM is tooa user in Azure AD.</span></span> <span data-ttu-id="0bda1-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Sugar CRM debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="0bda1-140">In other words, a link relationship between an Azure AD user and hello related user in Sugar CRM needs toobe established.</span></span>

<span data-ttu-id="0bda1-141">En Sugar CRM, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bda1-141">In Sugar CRM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0bda1-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Sugar CRM, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0bda1-142">tooconfigure and test Azure AD single sign-on with Sugar CRM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0bda1-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="0bda1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0bda1-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0bda1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0bda1-145">**[Crear un usuario de prueba de Sugar CRM](#creating-a-sugar-crm-test-user)**  -toohave un equivalente de Britta Simon en Sugar CRM que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="0bda1-145">**[Creating a Sugar CRM test user](#creating-a-sugar-crm-test-user)** - toohave a counterpart of Britta Simon in Sugar CRM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0bda1-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0bda1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0bda1-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0bda1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0bda1-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0bda1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0bda1-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="0bda1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sugar CRM application.</span></span>

<span data-ttu-id="0bda1-150">**inicio de sesión único en Azure AD tooconfigure con Sugar CRM, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0bda1-150">**tooconfigure Azure AD single sign-on with Sugar CRM, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bda1-151">En el portal de Azure, en Hola Hola **Sugar CRM** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-151">In hello Azure portal, on hello **Sugar CRM** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0bda1-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0bda1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. <span data-ttu-id="0bda1-155">En hello **Sugar CRM dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0bda1-155">On hello **Sugar CRM Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    <span data-ttu-id="0bda1-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="0bda1-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > <span data-ttu-id="0bda1-158">valor de Hello no es real.</span><span class="sxs-lookup"><span data-stu-id="0bda1-158">hello value is not real.</span></span> <span data-ttu-id="0bda1-159">Valor de Hola de actualización con Hola dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="0bda1-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="0bda1-160">Póngase en contacto con [equipo de soporte técnico de Sugar CRM cliente](https://support.sugarcrm.com/) valor de hello tooget.</span><span class="sxs-lookup"><span data-stu-id="0bda1-160">Contact [Sugar CRM Client support team](https://support.sugarcrm.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="0bda1-161">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0bda1-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. <span data-ttu-id="0bda1-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0bda1-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0bda1-165">En hello **Sugar CRM configuración** sección, haga clic en **configurar Sugar CRM** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="0bda1-165">On hello **Sugar CRM Configuration** section, click **Configure Sugar CRM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0bda1-166">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="0bda1-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. <span data-ttu-id="0bda1-168">En una ventana del explorador web diferente, inicie sesión en el sitio de empresa de Sugar CRM tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="0bda1-168">In a different web browser window, log in tooyour Sugar CRM company site as an administrator.</span></span>

8. <span data-ttu-id="0bda1-169">Vaya demasiado**administración**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-169">Go too**Admin**.</span></span>
   
    <span data-ttu-id="0bda1-170">![Administración](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="0bda1-170">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

9. <span data-ttu-id="0bda1-171">Hola **administración** sección, haga clic en **administración de contraseñas**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-171">In hello **Administration** section, click **Password Management**.</span></span>
   
    <span data-ttu-id="0bda1-172">![Administración](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="0bda1-172">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administration")</span></span>

10. <span data-ttu-id="0bda1-173">Seleccione **Habilitar autenticación SAML**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-173">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="0bda1-174">![Administración](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="0bda1-174">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administration")</span></span>

11. <span data-ttu-id="0bda1-175">Hola **autenticación SAML** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0bda1-175">In hello **SAML Authentication** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="0bda1-176">![Autenticación SAML](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "Autenticación SAML")</span><span class="sxs-lookup"><span data-stu-id="0bda1-176">![SAML Authentication](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML Authentication")</span></span>  
 
    <span data-ttu-id="0bda1-177">a.</span><span class="sxs-lookup"><span data-stu-id="0bda1-177">a.</span></span> <span data-ttu-id="0bda1-178">Hola **dirección URL de inicio de sesión** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0bda1-178">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="0bda1-179">b.</span><span class="sxs-lookup"><span data-stu-id="0bda1-179">b.</span></span> <span data-ttu-id="0bda1-180">Hola **dirección URL de SLO** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0bda1-180">In hello **SLO URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="0bda1-181">c.</span><span class="sxs-lookup"><span data-stu-id="0bda1-181">c.</span></span> <span data-ttu-id="0bda1-182">Abra el certificado codificado en base 64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, pegue Hola certificado completo en **certificado X.509** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0bda1-182">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="0bda1-183">d.</span><span class="sxs-lookup"><span data-stu-id="0bda1-183">d.</span></span> <span data-ttu-id="0bda1-184">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0bda1-185">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="0bda1-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0bda1-186">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="0bda1-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0bda1-187">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0bda1-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0bda1-188">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0bda1-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="0bda1-189">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="0bda1-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0bda1-191">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0bda1-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bda1-192">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0bda1-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0bda1-194">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0bda1-196">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bda1-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0bda1-198">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="0bda1-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0bda1-200">a.</span><span class="sxs-lookup"><span data-stu-id="0bda1-200">a.</span></span> <span data-ttu-id="0bda1-201">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0bda1-202">b.</span><span class="sxs-lookup"><span data-stu-id="0bda1-202">b.</span></span> <span data-ttu-id="0bda1-203">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0bda1-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0bda1-204">c.</span><span class="sxs-lookup"><span data-stu-id="0bda1-204">c.</span></span> <span data-ttu-id="0bda1-205">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0bda1-206">d.</span><span class="sxs-lookup"><span data-stu-id="0bda1-206">d.</span></span> <span data-ttu-id="0bda1-207">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-207">Click **Create**.</span></span>
 
### <a name="creating-a-sugar-crm-test-user"></a><span data-ttu-id="0bda1-208">Creación de un usuario de prueba de Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="0bda1-208">Creating a Sugar CRM test user</span></span>

<span data-ttu-id="0bda1-209">En orden tooenable toolog de los usuarios de Azure AD en tooSugar CRM, deben ser aprovisionado tooSugar CRM.</span><span class="sxs-lookup"><span data-stu-id="0bda1-209">In order tooenable Azure AD users toolog in tooSugar CRM, they must be provisioned tooSugar CRM.</span></span>

<span data-ttu-id="0bda1-210">En caso de hello de Sugar CRM, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="0bda1-210">In hello case of Sugar CRM, provisioning is a manual task.</span></span>

<span data-ttu-id="0bda1-211">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0bda1-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bda1-212">Inicie sesión en tooyour **Sugar CRM** como administrador.</span><span class="sxs-lookup"><span data-stu-id="0bda1-212">Log in tooyour **Sugar CRM** company site as administrator.</span></span>

2. <span data-ttu-id="0bda1-213">Vaya demasiado**administración**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-213">Go too**Admin**.</span></span>
   
    <span data-ttu-id="0bda1-214">![Administración](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="0bda1-214">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

3. <span data-ttu-id="0bda1-215">Hola **administración** sección, haga clic en **administración de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-215">In hello **Administration** section, click **User Management**.</span></span>
   
    <span data-ttu-id="0bda1-216">![Administración](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="0bda1-216">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administration")</span></span>

4. <span data-ttu-id="0bda1-217">Vaya demasiado**usuarios \> crear nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-217">Go too**Users \> Create New User**.</span></span>
   
    <span data-ttu-id="0bda1-218">![Creación de nuevos usuarios](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Creación de nuevos usuarios")</span><span class="sxs-lookup"><span data-stu-id="0bda1-218">![Create New User](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Create New User")</span></span>

5. <span data-ttu-id="0bda1-219">En hello **perfil de usuario** , realice los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="0bda1-219">On hello **User Profile** tab, perform hello following steps:</span></span>
   
    <span data-ttu-id="0bda1-220">![Nuevo usuario](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="0bda1-220">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "New User")</span></span>

    <span data-ttu-id="0bda1-221">a.</span><span class="sxs-lookup"><span data-stu-id="0bda1-221">a.</span></span> <span data-ttu-id="0bda1-222">Hola de tipo **nombre de usuario**, **apellidos**, y **dirección de correo electrónico** de un usuario de Azure Active Directory válido en hello relacionados con cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="0bda1-222">Type hello **user name**, **last name**, and **email address** of a valid Azure Active Directory user into hello related textboxes.</span></span>
  
6. <span data-ttu-id="0bda1-223">Como **Estado**, seleccione **Activo**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-223">As **Status**, select **Active**.</span></span>

7. <span data-ttu-id="0bda1-224">En la ficha contraseña de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0bda1-224">On hello Password tab, perform hello following steps:</span></span>
   
    <span data-ttu-id="0bda1-225">![Nuevo usuario](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="0bda1-225">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "New User")</span></span>

    <span data-ttu-id="0bda1-226">a.</span><span class="sxs-lookup"><span data-stu-id="0bda1-226">a.</span></span> <span data-ttu-id="0bda1-227">Escriba la contraseña de hello en hello relacionado con cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0bda1-227">Type hello password into hello related textbox.</span></span>

    <span data-ttu-id="0bda1-228">b.</span><span class="sxs-lookup"><span data-stu-id="0bda1-228">b.</span></span> <span data-ttu-id="0bda1-229">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-229">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="0bda1-230">Puede usar cualquier otra Sugar CRM usuario cuenta herramienta de creación o las API proporcionadas por Sugar CRM tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="0bda1-230">You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0bda1-231">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0bda1-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0bda1-232">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSugar CRM.</span><span class="sxs-lookup"><span data-stu-id="0bda1-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSugar CRM.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0bda1-234">**tooassign Britta Simon tooSugar CRM, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0bda1-234">**tooassign Britta Simon tooSugar CRM, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bda1-235">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0bda1-237">En la lista de aplicaciones de hello, seleccione **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-237">In hello applications list, select **Sugar CRM**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. <span data-ttu-id="0bda1-239">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0bda1-241">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-241">Click **Add** button.</span></span> <span data-ttu-id="0bda1-242">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0bda1-244">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bda1-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0bda1-245">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0bda1-246">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0bda1-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0bda1-247">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="0bda1-247">Testing single sign-on</span></span>

<span data-ttu-id="0bda1-248">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0bda1-248">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0bda1-249">Al hacer clic en icono de Sugar CRM Hola Hola Panel de acceso, deberá obtener la aplicación de Sugar CRM tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="0bda1-249">When you click hello Sugar CRM tile in hello Access Panel, you should get automatically signed-on tooyour Sugar CRM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0bda1-250">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0bda1-250">Additional resources</span></span>

* [<span data-ttu-id="0bda1-251">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0bda1-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0bda1-252">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0bda1-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

