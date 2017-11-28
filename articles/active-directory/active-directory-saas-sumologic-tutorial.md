---
title: "Tutorial: Integración de Azure Active Directory con SumoLogic | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Active Directory de Azure y SumoLogic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 2ef1bd329f5db8899f0b57744e4c0f6eed1c532f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="0d3d0-103">Tutorial: Integración de Azure Active Directory con SumoLogic</span><span class="sxs-lookup"><span data-stu-id="0d3d0-103">Tutorial: Azure Active Directory integration with SumoLogic</span></span>

<span data-ttu-id="0d3d0-104">En este tutorial, aprenderá cómo toointegrate SumoLogic con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0d3d0-104">In this tutorial, you learn how toointegrate SumoLogic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0d3d0-105">Integración SumoLogic con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0d3d0-105">Integrating SumoLogic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0d3d0-106">Puede controlar en Azure AD que tenga acceso tooSumoLogic</span><span class="sxs-lookup"><span data-stu-id="0d3d0-106">You can control in Azure AD who has access tooSumoLogic</span></span>
- <span data-ttu-id="0d3d0-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSumoLogic (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d3d0-107">You can enable your users tooautomatically get signed-on tooSumoLogic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0d3d0-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0d3d0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0d3d0-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0d3d0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d3d0-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0d3d0-110">Prerequisites</span></span>

<span data-ttu-id="0d3d0-111">integración de Azure AD con SumoLogic tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0d3d0-111">tooconfigure Azure AD integration with SumoLogic, you need hello following items:</span></span>

- <span data-ttu-id="0d3d0-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d3d0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0d3d0-113">Una suscripción habilitada para el inicio de sesión único en SumoLogic</span><span class="sxs-lookup"><span data-stu-id="0d3d0-113">A SumoLogic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0d3d0-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0d3d0-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0d3d0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0d3d0-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0d3d0-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0d3d0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0d3d0-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0d3d0-118">Scenario description</span></span>
<span data-ttu-id="0d3d0-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0d3d0-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="0d3d0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0d3d0-121">Agregar SumoLogic desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0d3d0-121">Adding SumoLogic from hello gallery</span></span>
2. <span data-ttu-id="0d3d0-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d3d0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumologic-from-hello-gallery"></a><span data-ttu-id="0d3d0-123">Agregar SumoLogic desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0d3d0-123">Adding SumoLogic from hello gallery</span></span>
<span data-ttu-id="0d3d0-124">integración de hello tooconfigure de SumoLogic en Azure AD, deberá tooadd SumoLogic de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-124">tooconfigure hello integration of SumoLogic into Azure AD, you need tooadd SumoLogic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0d3d0-125">**tooadd SumoLogic de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0d3d0-125">**tooadd SumoLogic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d3d0-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0d3d0-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0d3d0-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0d3d0-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0d3d0-133">En el cuadro de búsqueda de hello, escriba **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-133">In hello search box, type **SumoLogic**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. <span data-ttu-id="0d3d0-135">En el panel de resultados de hello, seleccione **SumoLogic**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-135">In hello results panel, select **SumoLogic**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0d3d0-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d3d0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0d3d0-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SumoLogic con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0d3d0-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0d3d0-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en SumoLogic es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SumoLogic is tooa user in Azure AD.</span></span> <span data-ttu-id="0d3d0-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SumoLogic debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-140">In other words, a link relationship between an Azure AD user and hello related user in SumoLogic needs toobe established.</span></span>

<span data-ttu-id="0d3d0-141">En SumoLogic, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-141">In SumoLogic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0d3d0-142">tooconfigure y prueba de inicio de sesión único en Azure AD con SumoLogic, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0d3d0-142">tooconfigure and test Azure AD single sign-on with SumoLogic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0d3d0-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0d3d0-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0d3d0-145">**[Crear un usuario de prueba de SumoLogic](#creating-a-sumologic-test-user)**  -toohave un equivalente de Britta Simon en SumoLogic que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - toohave a counterpart of Britta Simon in SumoLogic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0d3d0-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0d3d0-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0d3d0-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d3d0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0d3d0-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SumoLogic application.</span></span>

<span data-ttu-id="0d3d0-150">**inicio de sesión único en tooconfigure Azure AD con SumoLogic, realice Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0d3d0-150">**tooconfigure Azure AD single sign-on with SumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d3d0-151">En el portal de Azure, en Hola Hola **SumoLogic** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-151">In hello Azure portal, on hello **SumoLogic** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0d3d0-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. <span data-ttu-id="0d3d0-155">En hello **SumoLogic dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0d3d0-155">On hello **SumoLogic Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    <span data-ttu-id="0d3d0-157">a.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-157">a.</span></span> <span data-ttu-id="0d3d0-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenantname>.SumoLogic.com`</span><span class="sxs-lookup"><span data-stu-id="0d3d0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.SumoLogic.com`</span></span>

    <span data-ttu-id="0d3d0-159">b.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-159">b.</span></span> <span data-ttu-id="0d3d0-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="0d3d0-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > <span data-ttu-id="0d3d0-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-161">These values are not real.</span></span> <span data-ttu-id="0d3d0-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0d3d0-163">Póngase en contacto con [equipo de soporte técnico de cliente de SumoLogic](https://www.sumologic.com/contact-us/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="0d3d0-164">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. <span data-ttu-id="0d3d0-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0d3d0-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0d3d0-168">En hello **configuración de SumoLogic** sección, haga clic en **configurar SumoLogic** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-168">On hello **SumoLogic Configuration** section, click **Configure SumoLogic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0d3d0-169">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="0d3d0-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. <span data-ttu-id="0d3d0-171">En una ventana del explorador web diferente, inicie sesión en el sitio de la compañía SumoLogic tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-171">In a different web browser window, log in tooyour SumoLogic company site as an administrator.</span></span>

8. <span data-ttu-id="0d3d0-172">Vaya demasiado**administrar \> seguridad**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-172">Go too**Manage \> Security**.</span></span>
   
    <span data-ttu-id="0d3d0-173">![Administración](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="0d3d0-173">![Manage](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Manage")</span></span>

9. <span data-ttu-id="0d3d0-174">Haga clic en **SAML**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-174">Click **SAML**.</span></span>
   
    <span data-ttu-id="0d3d0-175">![Configuración de seguridad global](./media/active-directory-saas-sumologic-tutorial/ic778557.png "configuración de seguridad global")</span><span class="sxs-lookup"><span data-stu-id="0d3d0-175">![Global security settings](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Global security settings")</span></span>

10. <span data-ttu-id="0d3d0-176">De hello **seleccionar una configuración o cree uno nuevo** seleccione **Azure AD**y, a continuación, haga clic en **configurar**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-176">From hello **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="0d3d0-177">![Configuración de SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configuración de SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="0d3d0-177">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span></span>

11. <span data-ttu-id="0d3d0-178">En hello **configurar SAML 2.0** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0d3d0-178">On hello **Configure SAML 2.0** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="0d3d0-179">![Configuración de SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configuración de SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="0d3d0-179">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span></span>
   
    <span data-ttu-id="0d3d0-180">a.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-180">a.</span></span> <span data-ttu-id="0d3d0-181">Hola **nombre de configuración** cuadro de texto, tipo **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-181">In hello **Configuration Name** textbox, type **Azure AD**.</span></span> 

    <span data-ttu-id="0d3d0-182">b.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-182">b.</span></span> <span data-ttu-id="0d3d0-183">Seleccione **Modo de depuración**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-183">Select **Debug Mode**.</span></span>

    <span data-ttu-id="0d3d0-184">c.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-184">c.</span></span> <span data-ttu-id="0d3d0-185">Hola **emisor** cuadro de texto, pegue Hola valo **Id. de entidad SAML**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-185">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="0d3d0-186">d.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-186">d.</span></span> <span data-ttu-id="0d3d0-187">Hola **Authn Request URL** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-187">In hello **Authn Request URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0d3d0-188">e.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-188">e.</span></span> <span data-ttu-id="0d3d0-189">Abra el certificado codificado en base 64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, pegue Hola certificado completo en **certificado X.509** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="0d3d0-190">f.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-190">f.</span></span> <span data-ttu-id="0d3d0-191">Como **Atributo de correo electrónico**, seleccione **Usar SAML Subject**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-191">As **Email Attribute**, select **Use SAML subject**.</span></span>  

    <span data-ttu-id="0d3d0-192">g.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-192">g.</span></span> <span data-ttu-id="0d3d0-193">Seleccione **Configuración de inicio de sesión iniciada por el SP**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-193">Select **SP initiated Login Configuration**.</span></span>

    <span data-ttu-id="0d3d0-194">h.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-194">h.</span></span> <span data-ttu-id="0d3d0-195">Hola **ruta de acceso de inicio de sesión** cuadro de texto, tipo **Azure** y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-195">In hello **Login Path** textbox, type **Azure** and click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0d3d0-196">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="0d3d0-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0d3d0-197">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0d3d0-198">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0d3d0-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0d3d0-199">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d3d0-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="0d3d0-200">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0d3d0-202">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0d3d0-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d3d0-203">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0d3d0-205">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0d3d0-207">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0d3d0-209">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="0d3d0-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0d3d0-211">a.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-211">a.</span></span> <span data-ttu-id="0d3d0-212">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0d3d0-213">b.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-213">b.</span></span> <span data-ttu-id="0d3d0-214">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0d3d0-215">c.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-215">c.</span></span> <span data-ttu-id="0d3d0-216">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0d3d0-217">d.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-217">d.</span></span> <span data-ttu-id="0d3d0-218">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-218">Click **Create**.</span></span>
 
### <a name="creating-a-sumologic-test-user"></a><span data-ttu-id="0d3d0-219">Creación de un usuario de prueba de SumoLogic</span><span class="sxs-lookup"><span data-stu-id="0d3d0-219">Creating a SumoLogic test user</span></span>

<span data-ttu-id="0d3d0-220">En orden tooenable toolog de los usuarios de Azure AD en tooSumoLogic, deben ser tooSumoLogic aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-220">In order tooenable Azure AD users toolog in tooSumoLogic, they must be provisioned tooSumoLogic.</span></span>  

* <span data-ttu-id="0d3d0-221">En caso de hello de SumoLogic, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-221">In hello case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="0d3d0-222">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0d3d0-222">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d3d0-223">Inicie sesión en tooyour **SumoLogic** inquilino.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-223">Log in tooyour **SumoLogic** tenant.</span></span>

2. <span data-ttu-id="0d3d0-224">Vaya demasiado**administrar \> usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-224">Go too**Manage \> Users**.</span></span>
   
    <span data-ttu-id="0d3d0-225">![Usuarios](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="0d3d0-225">![Users](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Users")</span></span>

3. <span data-ttu-id="0d3d0-226">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-226">Click **Add**.</span></span>
   
    <span data-ttu-id="0d3d0-227">![Usuarios](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="0d3d0-227">![Users](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Users")</span></span>

4. <span data-ttu-id="0d3d0-228">En hello **nuevo usuario** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0d3d0-228">On hello **New User** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="0d3d0-229">![Nuevo usuario](./media/active-directory-saas-sumologic-tutorial/ic778563.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="0d3d0-229">![New User](./media/active-directory-saas-sumologic-tutorial/ic778563.png "New User")</span></span> 
 
    <span data-ttu-id="0d3d0-230">a.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-230">a.</span></span> <span data-ttu-id="0d3d0-231">Hola de tipo relacionados con la información de cuenta de hello Azure AD que quiera tooprovision en hello **nombre**, **Last Name**, y **correo electrónico** cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-231">Type hello related information of hello Azure AD account you want tooprovision into hello **First Name**, **Last Name**, and **Email** textboxes.</span></span>
  
    <span data-ttu-id="0d3d0-232">b.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-232">b.</span></span> <span data-ttu-id="0d3d0-233">Seleccione un rol.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-233">Select a role.</span></span>
  
    <span data-ttu-id="0d3d0-234">c.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-234">c.</span></span> <span data-ttu-id="0d3d0-235">Como **Estado**, seleccione **Activo**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-235">As **Status**, select **Active**.</span></span>
  
    <span data-ttu-id="0d3d0-236">d.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-236">d.</span></span> <span data-ttu-id="0d3d0-237">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-237">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="0d3d0-238">Puede usar cualquier otra SumoLogic usuario cuenta herramienta de creación o las API proporcionadas por SumoLogic tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0d3d0-239">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d3d0-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0d3d0-240">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSumoLogic.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSumoLogic.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0d3d0-242">**tooassign Britta Simon tooSumoLogic, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0d3d0-242">**tooassign Britta Simon tooSumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d3d0-243">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0d3d0-245">En la lista de aplicaciones de hello, seleccione **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-245">In hello applications list, select **SumoLogic**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. <span data-ttu-id="0d3d0-247">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0d3d0-249">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-249">Click **Add** button.</span></span> <span data-ttu-id="0d3d0-250">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0d3d0-252">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0d3d0-253">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0d3d0-254">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0d3d0-255">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="0d3d0-255">Testing single sign-on</span></span>

<span data-ttu-id="0d3d0-256">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-256">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0d3d0-257">Al hacer clic en icono de SumoLogic Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour SumoLogic aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d3d0-257">When you click hello SumoLogic tile in hello Access Panel, you should get automatically signed-on tooyour SumoLogic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0d3d0-258">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0d3d0-258">Additional resources</span></span>

* [<span data-ttu-id="0d3d0-259">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d3d0-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0d3d0-260">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0d3d0-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

