---
title: "Tutorial: Integración de Azure Active Directory con Lifesize Cloud | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Lifesize en la nube."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ae599907e872571b3220de7122006c7db8db4a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="8e761-103">Tutorial: Integración de Azure Active Directory con Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="8e761-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>

<span data-ttu-id="8e761-104">En este tutorial, aprenderá cómo toointegrate Lifesize en la nube con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8e761-104">In this tutorial, you learn how toointegrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8e761-105">Integración Lifesize en la nube con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="8e761-105">Integrating Lifesize Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8e761-106">Puede controlar en Azure AD que tenga acceso tooLifesize en la nube</span><span class="sxs-lookup"><span data-stu-id="8e761-106">You can control in Azure AD who has access tooLifesize Cloud</span></span>
- <span data-ttu-id="8e761-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLifesize en la nube (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e761-107">You can enable your users tooautomatically get signed-on tooLifesize Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8e761-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8e761-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8e761-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8e761-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e761-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8e761-110">Prerequisites</span></span>

<span data-ttu-id="8e761-111">tooconfigure integración de Azure AD con Lifesize en la nube, debe Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8e761-111">tooconfigure Azure AD integration with Lifesize Cloud, you need hello following items:</span></span>

- <span data-ttu-id="8e761-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e761-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8e761-113">Una suscripción habilitada para el inicio de sesión único en Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="8e761-113">A Lifesize Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8e761-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="8e761-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8e761-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="8e761-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8e761-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8e761-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8e761-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8e761-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8e761-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="8e761-118">Scenario description</span></span>
<span data-ttu-id="8e761-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="8e761-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8e761-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="8e761-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8e761-121">Agregar Lifesize en la nube desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="8e761-121">Adding Lifesize Cloud from hello gallery</span></span>
2. <span data-ttu-id="8e761-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e761-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lifesize-cloud-from-hello-gallery"></a><span data-ttu-id="8e761-123">Agregar Lifesize en la nube desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="8e761-123">Adding Lifesize Cloud from hello gallery</span></span>
<span data-ttu-id="8e761-124">integración de hello tooconfigure de Lifesize en la nube en Azure AD, deberá tooadd Lifesize en la nube de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="8e761-124">tooconfigure hello integration of Lifesize Cloud into Azure AD, you need tooadd Lifesize Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8e761-125">**tooadd Lifesize en la nube de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8e761-125">**tooadd Lifesize Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e761-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8e761-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8e761-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="8e761-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8e761-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8e761-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="8e761-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8e761-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="8e761-133">En el cuadro de búsqueda de hello, escriba **Lifesize nube**.</span><span class="sxs-lookup"><span data-stu-id="8e761-133">In hello search box, type **Lifesize Cloud**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. <span data-ttu-id="8e761-135">En el panel de resultados de hello, seleccione **Lifesize nube**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8e761-135">In hello results panel, select **Lifesize Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8e761-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e761-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8e761-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Lifesize Cloud con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8e761-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8e761-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en nube Lifesize es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e761-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lifesize Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="8e761-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en nube Lifesize debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="8e761-140">In other words, a link relationship between an Azure AD user and hello related user in Lifesize Cloud needs toobe established.</span></span>

<span data-ttu-id="8e761-141">En la nube Lifesize, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e761-141">In Lifesize Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8e761-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Lifesize en la nube, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="8e761-142">tooconfigure and test Azure AD single sign-on with Lifesize Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8e761-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="8e761-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8e761-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e761-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8e761-145">**[Crear un usuario de prueba en la nube Lifesize](#creating-a-lifesize-cloud-test-user) ** -toohave un equivalente de Britta Simon en nube de Lifesize que es la representación en forma de toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="8e761-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - toohave a counterpart of Britta Simon in Lifesize Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8e761-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8e761-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8e761-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="8e761-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8e761-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e761-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8e761-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Lifesize en la nube.</span><span class="sxs-lookup"><span data-stu-id="8e761-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="8e761-150">**inicio de sesión único en tooconfigure Azure AD con Lifesize en la nube, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8e761-150">**tooconfigure Azure AD single sign-on with Lifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e761-151">En el portal de Azure, en Hola Hola **Lifesize nube** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="8e761-151">In hello Azure portal, on hello **Lifesize Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="8e761-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8e761-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. <span data-ttu-id="8e761-155">En hello **Lifesize nube dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8e761-155">On hello **Lifesize Cloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    <span data-ttu-id="8e761-157">a.</span><span class="sxs-lookup"><span data-stu-id="8e761-157">a.</span></span> <span data-ttu-id="8e761-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://login.lifesizecloud.com/ls/?acs`</span><span class="sxs-lookup"><span data-stu-id="8e761-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/ls/?acs`</span></span>

    <span data-ttu-id="8e761-159">b.</span><span class="sxs-lookup"><span data-stu-id="8e761-159">b.</span></span> <span data-ttu-id="8e761-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://login.lifesizecloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="8e761-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/<companyname>`</span></span>

     
4. <span data-ttu-id="8e761-161">Comprobar **mostrar avanzadas de configuración de direcciones URL**, realizar Hola siguiendo el paso:</span><span class="sxs-lookup"><span data-stu-id="8e761-161">Check **Show advanced URL settings**, perform hello following step:</span></span>  
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    <span data-ttu-id="8e761-163">Hola **estado de retransmisión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://webapp.lifesizecloud.com/?ent=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="8e761-163">In hello **Relay state** textbox, type a URL using hello following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span></span>
   
   > [!NOTE] 
   ><span data-ttu-id="8e761-164">Tenga en cuenta que estos no son los valores reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e761-164">Please note that these are not hello real values.</span></span> <span data-ttu-id="8e761-165">tiene estos valores con hello tooupdate real identificador, estado de la transmisión y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="8e761-165">you have tooupdate these values with hello actual Sign-On URL, Relay State, and Identifier.</span></span> <span data-ttu-id="8e761-166">Póngase en contacto con [equipo de soporte técnico de cliente de la nube de Lifesize](https://www.lifesize.com/support) tooget URL de inicio de sesión y los valores de identificador y se puede obtener el valor de estado de la transmisión de configuración de SSO que se explica más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="8e761-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) tooget Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in hello tutorial.</span></span>

4. <span data-ttu-id="8e761-167">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8e761-167">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. <span data-ttu-id="8e761-169">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="8e761-169">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8e761-171">En hello **configuración de la nube de Lifesize** sección, haga clic en **configurar en la nube Lifesize** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="8e761-171">On hello **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8e761-172">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="8e761-172">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. <span data-ttu-id="8e761-174">tooget SSO configurado para la aplicación, el inicio de sesión en hello aplicación en la nube de Lifesize con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="8e761-174">tooget SSO configured for your application, login into hello Lifesize Cloud application with Admin privileges.</span></span>

8. <span data-ttu-id="8e761-175">En hello esquina superior derecha, haga clic en su nombre y, a continuación, haga clic en hello **configuración de adelanto**.</span><span class="sxs-lookup"><span data-stu-id="8e761-175">In hello top right corner click on your name and then click on hello **Advance Settings**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. <span data-ttu-id="8e761-177">Hola adelanto ahora haga clic en hello **configuración de SSO** vínculo.</span><span class="sxs-lookup"><span data-stu-id="8e761-177">In hello Advance Settings now click on hello **SSO Configuration** link.</span></span> <span data-ttu-id="8e761-178">Se abrirá la página de configuración de SSO de hello para la instancia.</span><span class="sxs-lookup"><span data-stu-id="8e761-178">It will open hello SSO Configuration page for your instance.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. <span data-ttu-id="8e761-180">Configurar ahora Hola después de valores de configuración de SSO de hello interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="8e761-180">Now configure hello following values in hello SSO configuration UI.</span></span>    
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    <span data-ttu-id="8e761-182">a.</span><span class="sxs-lookup"><span data-stu-id="8e761-182">a.</span></span> <span data-ttu-id="8e761-183">En **emisor del proveedor de identidades** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8e761-183">In **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8e761-184">b.</span><span class="sxs-lookup"><span data-stu-id="8e761-184">b.</span></span>  <span data-ttu-id="8e761-185">En **dirección URL de inicio de sesión** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8e761-185">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8e761-186">c.</span><span class="sxs-lookup"><span data-stu-id="8e761-186">c.</span></span> <span data-ttu-id="8e761-187">Abra el certificado codificado en base 64 en el Bloc de notas que se descarga desde el portal de Azure, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado X.509** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="8e761-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="8e761-188">d.</span><span class="sxs-lookup"><span data-stu-id="8e761-188">d.</span></span> <span data-ttu-id="8e761-189">Hola atributo SAML asignaciones para el cuadro de texto Nombre de hello escriba Hola valor **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span><span class="sxs-lookup"><span data-stu-id="8e761-189">In hello SAML Attribute mappings for hello First Name text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
    
    <span data-ttu-id="8e761-190">e.</span><span class="sxs-lookup"><span data-stu-id="8e761-190">e.</span></span> <span data-ttu-id="8e761-191">En la asignación de atributo de SAML de Hola para hello **Last Name** cuadro de texto escriba Hola valor **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span><span class="sxs-lookup"><span data-stu-id="8e761-191">In hello SAML Attribute mapping for hello **Last Name** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
    
    <span data-ttu-id="8e761-192">f.</span><span class="sxs-lookup"><span data-stu-id="8e761-192">f.</span></span> <span data-ttu-id="8e761-193">En la asignación de atributo de SAML de Hola para hello **correo electrónico** cuadro de texto escriba Hola valor **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span><span class="sxs-lookup"><span data-stu-id="8e761-193">In hello SAML Attribute mapping for hello **Email** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>

11. <span data-ttu-id="8e761-194">configuración de hello toocheck puede hacer clic en hello **prueba** botón.</span><span class="sxs-lookup"><span data-stu-id="8e761-194">toocheck hello configuration you can click on hello **Test** button.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="8e761-195">Para probar correctamente necesita el Asistente para configuración de hello toocomplete en Azure AD y también proporcionan acceso toousers o grupos que pueden realizar pruebas de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e761-195">For successful testing you need toocomplete hello configuration wizard in Azure AD and also provide access toousers or groups who can perform hello test.</span></span>

12. <span data-ttu-id="8e761-196">Habilitar Hola SSO mediante la comprobación de hello **habilitar SSO** botón.</span><span class="sxs-lookup"><span data-stu-id="8e761-196">Enable hello SSO by checking on hello **Enable SSO** button.</span></span>

13. <span data-ttu-id="8e761-197">Ahora haga clic en hello **actualización** botón para que se guardan todas las configuraciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e761-197">Now click on hello **Update** button so that all hello settings are saved.</span></span> <span data-ttu-id="8e761-198">Esto generará el valor de RelayState Hola.</span><span class="sxs-lookup"><span data-stu-id="8e761-198">This will generate hello RelayState value.</span></span> <span data-ttu-id="8e761-199">Hola de copiar valor de RelayState, que se genera en el cuadro de texto hello, péguelo en hello **estado de retransmisión** en el cuadro de texto **Lifesize nube dominio y las direcciones URL** sección.</span><span class="sxs-lookup"><span data-stu-id="8e761-199">Copy hello RelayState value, which is generated in hello text box, paste it in hello **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span></span> 

> [!TIP]
> <span data-ttu-id="8e761-200">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="8e761-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8e761-201">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="8e761-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8e761-202">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8e761-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8e761-203">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e761-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="8e761-204">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="8e761-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="8e761-206">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8e761-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e761-207">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8e761-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8e761-209">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="8e761-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8e761-211">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e761-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8e761-213">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="8e761-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8e761-215">a.</span><span class="sxs-lookup"><span data-stu-id="8e761-215">a.</span></span> <span data-ttu-id="8e761-216">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8e761-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8e761-217">b.</span><span class="sxs-lookup"><span data-stu-id="8e761-217">b.</span></span> <span data-ttu-id="8e761-218">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8e761-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8e761-219">c.</span><span class="sxs-lookup"><span data-stu-id="8e761-219">c.</span></span> <span data-ttu-id="8e761-220">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="8e761-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8e761-221">d.</span><span class="sxs-lookup"><span data-stu-id="8e761-221">d.</span></span> <span data-ttu-id="8e761-222">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8e761-222">Click **Create**.</span></span>
 
### <a name="creating-a-lifesize-cloud-test-user"></a><span data-ttu-id="8e761-223">Creación de un usuario de prueba de Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="8e761-223">Creating a Lifesize Cloud test user</span></span>

<span data-ttu-id="8e761-224">En esta sección, creará el usuario Britta Simon en Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="8e761-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="8e761-225">Lifesize Cloud no admite el aprovisionamiento de usuarios automático.</span><span class="sxs-lookup"><span data-stu-id="8e761-225">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="8e761-226">Después de autenticarse correctamente en Azure AD, usuario Hola se automáticamente aprovisionará en aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="8e761-226">After successful authentication at Azure AD, hello user will be automatically provisioned in hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8e761-227">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e761-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8e761-228">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooLifesize en la nube.</span><span class="sxs-lookup"><span data-stu-id="8e761-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLifesize Cloud.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="8e761-230">**tooassign Britta Simon tooLifesize en la nube, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8e761-230">**tooassign Britta Simon tooLifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e761-231">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8e761-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="8e761-233">En la lista de aplicaciones de hello, seleccione **Lifesize nube**.</span><span class="sxs-lookup"><span data-stu-id="8e761-233">In hello applications list, select **Lifesize Cloud**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. <span data-ttu-id="8e761-235">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8e761-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="8e761-237">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8e761-237">Click **Add** button.</span></span> <span data-ttu-id="8e761-238">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8e761-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="8e761-240">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e761-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8e761-241">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8e761-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8e761-242">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8e761-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8e761-243">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="8e761-243">Testing single sign-on</span></span>

<span data-ttu-id="8e761-244">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="8e761-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8e761-245">Al hacer clic en hello en la nube Lifesize el icono Hola Panel de acceso, deberá obtener la página de inicio de sesión de la aplicación en la nube de Lifesize.</span><span class="sxs-lookup"><span data-stu-id="8e761-245">When you click hello Lifesize Cloud tile in hello Access Panel, you should get login page of Lifesize Cloud application.</span></span>
<span data-ttu-id="8e761-246">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8e761-246">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8e761-247">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8e761-247">Additional resources</span></span>

* [<span data-ttu-id="8e761-248">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e761-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8e761-249">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8e761-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

