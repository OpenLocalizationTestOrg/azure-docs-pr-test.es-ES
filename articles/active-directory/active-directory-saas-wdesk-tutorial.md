---
title: "Tutorial: integración de Azure Active Directory con Wdesk | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Wdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 2c278a5e4f50cc362663efc0f826ff0c0fcf6e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a><span data-ttu-id="c9f51-103">Tutorial: integración de Azure Active Directory con Wdesk</span><span class="sxs-lookup"><span data-stu-id="c9f51-103">Tutorial: Azure Active Directory integration with Wdesk</span></span>

<span data-ttu-id="c9f51-104">En este tutorial, aprenderá cómo toointegrate Wdesk con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c9f51-104">In this tutorial, you learn how toointegrate Wdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c9f51-105">Integración Wdesk con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c9f51-105">Integrating Wdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c9f51-106">Puede controlar en Azure AD que tenga acceso tooWdesk</span><span class="sxs-lookup"><span data-stu-id="c9f51-106">You can control in Azure AD who has access tooWdesk</span></span>
- <span data-ttu-id="c9f51-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooWdesk (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9f51-107">You can enable your users tooautomatically get signed-on tooWdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c9f51-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c9f51-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c9f51-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte.</span><span class="sxs-lookup"><span data-stu-id="c9f51-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="c9f51-110">[¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="c9f51-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9f51-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c9f51-111">Prerequisites</span></span>

<span data-ttu-id="c9f51-112">integración de Azure AD con Wdesk tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c9f51-112">tooconfigure Azure AD integration with Wdesk, you need hello following items:</span></span>

- <span data-ttu-id="c9f51-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9f51-113">An Azure AD subscription</span></span>
- <span data-ttu-id="c9f51-114">Una suscripción habilitada para el inicio de sesión único en Wdesk</span><span class="sxs-lookup"><span data-stu-id="c9f51-114">A Wdesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c9f51-115">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c9f51-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c9f51-116">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c9f51-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c9f51-117">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c9f51-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c9f51-118">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c9f51-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c9f51-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c9f51-119">Scenario description</span></span>
<span data-ttu-id="c9f51-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c9f51-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c9f51-121">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="c9f51-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c9f51-122">Agregar Wdesk desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c9f51-122">Adding Wdesk from hello gallery</span></span>
2. <span data-ttu-id="c9f51-123">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9f51-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wdesk-from-hello-gallery"></a><span data-ttu-id="c9f51-124">Agregar Wdesk desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c9f51-124">Adding Wdesk from hello gallery</span></span>
<span data-ttu-id="c9f51-125">integración de hello tooconfigure de Wdesk en Azure AD, deberá tooadd Wdesk de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="c9f51-125">tooconfigure hello integration of Wdesk into Azure AD, you need tooadd Wdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c9f51-126">**tooadd Wdesk de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c9f51-126">**tooadd Wdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9f51-127">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c9f51-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c9f51-129">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c9f51-130">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-130">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c9f51-132">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c9f51-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c9f51-134">En el cuadro de búsqueda de hello, escriba **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-134">In hello search box, type **Wdesk**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. <span data-ttu-id="c9f51-136">En el panel de resultados de hello, seleccione **Wdesk**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c9f51-136">In hello results panel, select **Wdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c9f51-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9f51-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c9f51-139">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Wdesk con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c9f51-139">In this section, you configure and test Azure AD single sign-on with Wdesk based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c9f51-140">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Wdesk es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9f51-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="c9f51-141">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Wdesk debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="c9f51-141">In other words, a link relationship between an Azure AD user and hello related user in Wdesk needs toobe established.</span></span>

<span data-ttu-id="c9f51-142">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Wdesk.</span><span class="sxs-lookup"><span data-stu-id="c9f51-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wdesk.</span></span>

<span data-ttu-id="c9f51-143">tooconfigure y prueba de inicio de sesión único en Azure AD con Wdesk, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c9f51-143">tooconfigure and test Azure AD single sign-on with Wdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c9f51-144">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="c9f51-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c9f51-145">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9f51-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c9f51-146">**[Crear un usuario de prueba Wdesk](#creating-a-wdesk-test-user) ** -toohave un equivalente de Britta Simon en Wdesk que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="c9f51-146">**[Creating a Wdesk test user](#creating-a-wdesk-test-user)** - toohave a counterpart of Britta Simon in Wdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c9f51-147">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c9f51-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c9f51-148">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c9f51-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c9f51-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9f51-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c9f51-150">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Wdesk.</span><span class="sxs-lookup"><span data-stu-id="c9f51-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wdesk application.</span></span>

<span data-ttu-id="c9f51-151">**inicio de sesión único en Azure AD tooconfigure con Wdesk, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c9f51-151">**tooconfigure Azure AD single sign-on with Wdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9f51-152">En el portal de Azure, en Hola Hola **Wdesk** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-152">In hello Azure portal, on hello **Wdesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c9f51-154">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c9f51-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. <span data-ttu-id="c9f51-156">En hello **Wdesk dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **IDP** modo iniciado realiza Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c9f51-156">On hello **Wdesk Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    <span data-ttu-id="c9f51-158">a.</span><span class="sxs-lookup"><span data-stu-id="c9f51-158">a.</span></span> <span data-ttu-id="c9f51-159">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="c9f51-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span></span>

    <span data-ttu-id="c9f51-160">b.</span><span class="sxs-lookup"><span data-stu-id="c9f51-160">b.</span></span> <span data-ttu-id="c9f51-161">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="c9f51-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span></span>

4. <span data-ttu-id="c9f51-162">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="c9f51-163">Si desea que aplicación de hello tooconfigure en **SP** inicia el modo, realizar Hola siguiendo el paso:</span><span class="sxs-lookup"><span data-stu-id="c9f51-163">If you wish tooconfigure hello application in **SP** initiated mode, perform hello following step:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    <span data-ttu-id="c9f51-165">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="c9f51-165">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="c9f51-166">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="c9f51-166">These values are not real.</span></span> <span data-ttu-id="c9f51-167">Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="c9f51-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="c9f51-168">Estos valores se obtienen de portal WDesk al configurar Hola SSO.</span><span class="sxs-lookup"><span data-stu-id="c9f51-168">You get these values from WDesk portal when you configure hello SSO.</span></span> 
  
5. <span data-ttu-id="c9f51-169">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c9f51-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. <span data-ttu-id="c9f51-171">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c9f51-171">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="c9f51-173">En una ventana del explorador web diferente, tooWdesk de inicio de sesión como un administrador de seguridad.</span><span class="sxs-lookup"><span data-stu-id="c9f51-173">In a different web browser window, login tooWdesk as a Security Administrator.</span></span>

8. <span data-ttu-id="c9f51-174">En hello parte inferior izquierda, haga clic en **administración** y elija **Administrador de la cuenta**:</span><span class="sxs-lookup"><span data-stu-id="c9f51-174">In hello bottom left, click **Admin** and choose **Account Admin**:</span></span>
 
     ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. <span data-ttu-id="c9f51-176">En Wdesk administrador, navegue demasiado**seguridad**, a continuación, **SAML** > **configuración SAML**:</span><span class="sxs-lookup"><span data-stu-id="c9f51-176">In Wdesk Admin, navigate too**Security**, then **SAML** > **SAML Settings**:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. <span data-ttu-id="c9f51-178">En **configuración General**, comprobar hello **habilitar SAML Single Sign On**:</span><span class="sxs-lookup"><span data-stu-id="c9f51-178">Under **General Settings**, check hello **Enable SAML Single Sign On**:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. <span data-ttu-id="c9f51-180">En **detalles del proveedor de servicio**, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c9f51-180">Under **Service Provider Details**, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      <span data-ttu-id="c9f51-182">a.</span><span class="sxs-lookup"><span data-stu-id="c9f51-182">a.</span></span> <span data-ttu-id="c9f51-183">Hola copia **dirección URL de inicio de sesión** y péguelo en **dirección Url de inicio de sesión** cuadro de texto en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9f51-183">Copy hello **Login URL** and paste it in **Sign-on Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="c9f51-184">b.</span><span class="sxs-lookup"><span data-stu-id="c9f51-184">b.</span></span> <span data-ttu-id="c9f51-185">Hola copia **dirección Url de metadatos** y péguelo en **identificador** cuadro de texto en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9f51-185">Copy hello **Metadata Url** and paste it in **Identifier** textbox on Azure portal.</span></span>
       
      <span data-ttu-id="c9f51-186">c.</span><span class="sxs-lookup"><span data-stu-id="c9f51-186">c.</span></span> <span data-ttu-id="c9f51-187">Hola copia **dirección url de consumidor** y péguelo en **dirección Url de respuesta** cuadro de texto en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9f51-187">Copy hello **Consumer url** and paste it in **Reply Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="c9f51-188">d.</span><span class="sxs-lookup"><span data-stu-id="c9f51-188">d.</span></span> <span data-ttu-id="c9f51-189">Haga clic en **guardar** sobre los cambios de hello toosave de portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9f51-189">Click **Save** on Azure portal toosave hello changes.</span></span>      

12. <span data-ttu-id="c9f51-190">Haga clic en **configurar opciones de IdP** tooopen **modificar configuración de IdP** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c9f51-190">Click **Configure IdP Settings** tooopen **Edit IdP Settings** dialog.</span></span> <span data-ttu-id="c9f51-191">Haga clic en **Elegir archivo** toolocate hello **Metadata.xml** archivo que guardó en el portal de Azure, a continuación, cargarlo.</span><span class="sxs-lookup"><span data-stu-id="c9f51-191">Click **Choose File** toolocate hello **Metadata.xml** file you saved from Azure portal, then upload it.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. <span data-ttu-id="c9f51-193">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-193">Click **Save changes**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> <span data-ttu-id="c9f51-195">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="c9f51-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c9f51-196">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="c9f51-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c9f51-197">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c9f51-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c9f51-198">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9f51-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="c9f51-199">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="c9f51-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c9f51-201">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c9f51-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9f51-202">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c9f51-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c9f51-204">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c9f51-206">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9f51-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c9f51-208">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c9f51-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c9f51-210">a.</span><span class="sxs-lookup"><span data-stu-id="c9f51-210">a.</span></span> <span data-ttu-id="c9f51-211">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c9f51-212">b.</span><span class="sxs-lookup"><span data-stu-id="c9f51-212">b.</span></span> <span data-ttu-id="c9f51-213">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c9f51-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c9f51-214">c.</span><span class="sxs-lookup"><span data-stu-id="c9f51-214">c.</span></span> <span data-ttu-id="c9f51-215">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c9f51-216">d.</span><span class="sxs-lookup"><span data-stu-id="c9f51-216">d.</span></span> <span data-ttu-id="c9f51-217">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-217">Click **Create**.</span></span>
 
### <a name="creating-a-wdesk-test-user"></a><span data-ttu-id="c9f51-218">Creación de usuario de prueba de Wdesk</span><span class="sxs-lookup"><span data-stu-id="c9f51-218">Creating a Wdesk test user</span></span>

<span data-ttu-id="c9f51-219">toolog de los usuarios de Azure AD tooenable en tooWdesk, se les deben aprovisionar en Wdesk.</span><span class="sxs-lookup"><span data-stu-id="c9f51-219">tooenable Azure AD users toolog in tooWdesk, they must be provisioned into Wdesk.</span></span> <span data-ttu-id="c9f51-220">En el caso de Wdesk, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="c9f51-220">In Wdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="c9f51-221">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c9f51-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9f51-222">Inicie sesión en tooWdesk como un administrador de seguridad.</span><span class="sxs-lookup"><span data-stu-id="c9f51-222">Log in tooWdesk as a Security Administrator.</span></span>
2. <span data-ttu-id="c9f51-223">Navegue demasiado**administración** > **Administrador de la cuenta**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-223">Navigate too**Admin** > **Account Admin**.</span></span>

     ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. <span data-ttu-id="c9f51-225">Haga clic en **Members** (Miembros) en **People** (Contactos).</span><span class="sxs-lookup"><span data-stu-id="c9f51-225">Click **Members** under **People**.</span></span>

4. <span data-ttu-id="c9f51-226">Ahora haga clic en **Agregar miembro** tooopen **Agregar miembro** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c9f51-226">Now click **Add Member** tooopen **Add Member** dialog box.</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. <span data-ttu-id="c9f51-228">En **usuario** texto cuadro, escriba el nombre de usuario de saludo del usuario como ** brittasimon@contoso.com ** y haga clic en **continuar** botón.</span><span class="sxs-lookup"><span data-stu-id="c9f51-228">In **User** text box, enter hello username of user like **brittasimon@contoso.com** and click **Continue** button.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  <span data-ttu-id="c9f51-230">Especifique los detalles de hello tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="c9f51-230">Enter hello details as shown below:</span></span>
  
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    <span data-ttu-id="c9f51-232">a.</span><span class="sxs-lookup"><span data-stu-id="c9f51-232">a.</span></span> <span data-ttu-id="c9f51-233">En **correo electrónico** texto cuadro, escriba el correo electrónico de saludo del usuario como ** brittasimon@contoso.com **.</span><span class="sxs-lookup"><span data-stu-id="c9f51-233">In **E-mail** text box, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="c9f51-234">b.</span><span class="sxs-lookup"><span data-stu-id="c9f51-234">b.</span></span> <span data-ttu-id="c9f51-235">En **nombre** texto cuadro, escriba Hola nombre de usuario como **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-235">In **First Name** text box, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="c9f51-236">c.</span><span class="sxs-lookup"><span data-stu-id="c9f51-236">c.</span></span> <span data-ttu-id="c9f51-237">En **Last Name** texto cuadro, escriba Hola último nombre de usuario como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-237">In **Last Name** text box, enter hello last name of user like **Simon**.</span></span>

7. <span data-ttu-id="c9f51-238">Haga clic en el botón **Save Member** (Guardar miembro).</span><span class="sxs-lookup"><span data-stu-id="c9f51-238">Click **Save Member** button.</span></span>  

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c9f51-240">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9f51-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c9f51-241">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooWdesk.</span><span class="sxs-lookup"><span data-stu-id="c9f51-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWdesk.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c9f51-243">**tooassign Britta Simon tooWdesk, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c9f51-243">**tooassign Britta Simon tooWdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9f51-244">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c9f51-246">En la lista de aplicaciones de hello, seleccione **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-246">In hello applications list, select **Wdesk**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. <span data-ttu-id="c9f51-248">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c9f51-250">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-250">Click **Add** button.</span></span> <span data-ttu-id="c9f51-251">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c9f51-253">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9f51-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c9f51-254">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c9f51-255">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c9f51-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c9f51-256">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c9f51-256">Testing single sign-on</span></span>

<span data-ttu-id="c9f51-257">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c9f51-257">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c9f51-258">Al hacer clic en icono de Wdesk Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Wdesk aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9f51-258">When you click hello Wdesk tile in hello Access Panel, you should get automatically signed-on tooyour Wdesk application.</span></span>
<span data-ttu-id="c9f51-259">Para más información sobre el Panel de acceso, vea la [introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c9f51-259">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c9f51-260">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c9f51-260">Additional resources</span></span>

* [<span data-ttu-id="c9f51-261">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9f51-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c9f51-262">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c9f51-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

