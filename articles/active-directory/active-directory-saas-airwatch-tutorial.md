---
title: "Tutorial: Integración de Azure Active Directory con AirWatch | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y AirWatch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e5230d5a36824778a4d9804dadf9f13a0d11a68d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="70bcc-103">Tutorial: Integración de Azure Active Directory con AirWatch</span><span class="sxs-lookup"><span data-stu-id="70bcc-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>

<span data-ttu-id="70bcc-104">En este tutorial, aprenderá cómo toointegrate AirWatch con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="70bcc-104">In this tutorial, you learn how toointegrate AirWatch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="70bcc-105">Integración de AirWatch con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="70bcc-105">Integrating AirWatch with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="70bcc-106">Puede controlar en Azure AD que tenga acceso tooAirWatch</span><span class="sxs-lookup"><span data-stu-id="70bcc-106">You can control in Azure AD who has access tooAirWatch</span></span>
- <span data-ttu-id="70bcc-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAirWatch (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="70bcc-107">You can enable your users tooautomatically get signed-on tooAirWatch (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="70bcc-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="70bcc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="70bcc-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="70bcc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70bcc-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="70bcc-110">Prerequisites</span></span>

<span data-ttu-id="70bcc-111">integración de Azure AD con AirWatch tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="70bcc-111">tooconfigure Azure AD integration with AirWatch, you need hello following items:</span></span>

- <span data-ttu-id="70bcc-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="70bcc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="70bcc-113">Una suscripción habilitada para el inicio de sesión único en AirWatch</span><span class="sxs-lookup"><span data-stu-id="70bcc-113">An AirWatch single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="70bcc-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="70bcc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="70bcc-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="70bcc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="70bcc-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="70bcc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="70bcc-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70bcc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="70bcc-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="70bcc-118">Scenario description</span></span>
<span data-ttu-id="70bcc-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="70bcc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="70bcc-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="70bcc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="70bcc-121">Agregar AirWatch desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="70bcc-121">Adding AirWatch from hello gallery</span></span>
2. <span data-ttu-id="70bcc-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="70bcc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-airwatch-from-hello-gallery"></a><span data-ttu-id="70bcc-123">Agregar AirWatch desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="70bcc-123">Adding AirWatch from hello gallery</span></span>
<span data-ttu-id="70bcc-124">integración de hello tooconfigure de AirWatch en Azure AD, deberá tooadd AirWatch de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="70bcc-124">tooconfigure hello integration of AirWatch into Azure AD, you need tooadd AirWatch from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="70bcc-125">**tooadd AirWatch de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="70bcc-125">**tooadd AirWatch from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="70bcc-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="70bcc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="70bcc-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="70bcc-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="70bcc-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="70bcc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="70bcc-133">En el cuadro de búsqueda de hello, escriba **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-133">In hello search box, type **AirWatch**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. <span data-ttu-id="70bcc-135">En el panel de resultados de hello, seleccione **AirWatch**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="70bcc-135">In hello results panel, select **AirWatch**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="70bcc-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="70bcc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="70bcc-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con AirWatch con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="70bcc-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="70bcc-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en AirWatch es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70bcc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AirWatch is tooa user in Azure AD.</span></span> <span data-ttu-id="70bcc-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en AirWatch debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="70bcc-140">In other words, a link relationship between an Azure AD user and hello related user in AirWatch needs toobe established.</span></span>

<span data-ttu-id="70bcc-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en AirWatch.</span><span class="sxs-lookup"><span data-stu-id="70bcc-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in AirWatch.</span></span>

<span data-ttu-id="70bcc-142">tooconfigure y prueba de inicio de sesión único en Azure AD con AirWatch, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="70bcc-142">tooconfigure and test Azure AD single sign-on with AirWatch, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="70bcc-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="70bcc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="70bcc-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="70bcc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="70bcc-145">**[Crear un usuario de prueba de AirWatch](#creating-a-airwatch-test-user)**  -toohave un equivalente de Britta Simon en AirWatch que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="70bcc-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - toohave a counterpart of Britta Simon in AirWatch that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="70bcc-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="70bcc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="70bcc-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="70bcc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="70bcc-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="70bcc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="70bcc-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación AirWatch.</span><span class="sxs-lookup"><span data-stu-id="70bcc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AirWatch application.</span></span>

<span data-ttu-id="70bcc-150">**inicio de sesión único en Azure AD tooconfigure con AirWatch, realice Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="70bcc-150">**tooconfigure Azure AD single sign-on with AirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="70bcc-151">En el portal de Azure, en Hola Hola **AirWatch** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-151">In hello Azure portal, on hello **AirWatch** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="70bcc-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="70bcc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. <span data-ttu-id="70bcc-155">En hello **AirWatch dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="70bcc-155">On hello **AirWatch Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    <span data-ttu-id="70bcc-157">a.</span><span class="sxs-lookup"><span data-stu-id="70bcc-157">a.</span></span> <span data-ttu-id="70bcc-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span><span class="sxs-lookup"><span data-stu-id="70bcc-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span></span>

    <span data-ttu-id="70bcc-159">b.</span><span class="sxs-lookup"><span data-stu-id="70bcc-159">b.</span></span> <span data-ttu-id="70bcc-160">Hola **identificador** cuadro de texto, valor de tipo hello como`AirWatch`</span><span class="sxs-lookup"><span data-stu-id="70bcc-160">In hello **Identifier** textbox, type hello value as `AirWatch`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="70bcc-161">Este valor no es hello real.</span><span class="sxs-lookup"><span data-stu-id="70bcc-161">This value is not hello real.</span></span> <span data-ttu-id="70bcc-162">Actualizar este valor con la URL de inicio de sesión real de Hola.</span><span class="sxs-lookup"><span data-stu-id="70bcc-162">Update this value with hello actual Sign-on URL.</span></span> <span data-ttu-id="70bcc-163">Póngase en contacto con [equipo de soporte técnico de cliente de AirWatch](http://www.air-watch.com/company/contact-us/) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="70bcc-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) tooget this value.</span></span> 
 
4. <span data-ttu-id="70bcc-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="70bcc-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. <span data-ttu-id="70bcc-166">En hello **configuración de AirWatch** sección, haga clic en **configurar AirWatch** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="70bcc-166">On hello **AirWatch Configuration** section, click **Configure AirWatch** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="70bcc-167">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="70bcc-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. <span data-ttu-id="70bcc-169">Haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-169">Click **Save** button.</span></span>

    <span data-ttu-id="70bcc-170">![Configuración del inicio de sesión único](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="70bcc-170">![Configure Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span></span>
7. <span data-ttu-id="70bcc-171">En una ventana del explorador web diferente, inicie sesión en el sitio de la empresa tooyour AirWatch como administrador.</span><span class="sxs-lookup"><span data-stu-id="70bcc-171">In a different web browser window, log in tooyour AirWatch company site as an administrator.</span></span>

8. <span data-ttu-id="70bcc-172">En el panel de navegación izquierdo de hello, haga clic en **cuentas**y, a continuación, haga clic en **administradores**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-172">In hello left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="70bcc-173">![Administradores](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administradores")</span><span class="sxs-lookup"><span data-stu-id="70bcc-173">![Administrators](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrators")</span></span>

9. <span data-ttu-id="70bcc-174">Expanda hello **configuración** menú y, a continuación, haga clic en **servicios de directorio**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-174">Expand hello **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="70bcc-175">![Configuración](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="70bcc-175">![Settings](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Settings")</span></span>

10. <span data-ttu-id="70bcc-176">Haga clic en hello **usuario** ficha Hola **DN Base** cuadro de texto, escriba el nombre de dominio y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-176">Click hello **User** tab, in hello **Base DN** textbox, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="70bcc-177">![Usuario](./media/active-directory-saas-airwatch-tutorial/ic791922.png "Usuario")</span><span class="sxs-lookup"><span data-stu-id="70bcc-177">![User](./media/active-directory-saas-airwatch-tutorial/ic791922.png "User")</span></span>

11. <span data-ttu-id="70bcc-178">Haga clic en hello **Server** ficha.</span><span class="sxs-lookup"><span data-stu-id="70bcc-178">Click hello **Server** tab.</span></span>
   
   <span data-ttu-id="70bcc-179">![Servidor](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Servidor")</span><span class="sxs-lookup"><span data-stu-id="70bcc-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span></span>

12. <span data-ttu-id="70bcc-180">Lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="70bcc-180">Perform hello following steps:</span></span>
    
    <span data-ttu-id="70bcc-181">![Cargar](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Cargar")</span><span class="sxs-lookup"><span data-stu-id="70bcc-181">![Upload](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Upload")</span></span>   
    
    <span data-ttu-id="70bcc-182">a.</span><span class="sxs-lookup"><span data-stu-id="70bcc-182">a.</span></span> <span data-ttu-id="70bcc-183">En **Directory Type** (Tipo de directorio), seleccione **None** (Ninguno).</span><span class="sxs-lookup"><span data-stu-id="70bcc-183">As **Directory Type**, select **None**.</span></span>

    <span data-ttu-id="70bcc-184">b.</span><span class="sxs-lookup"><span data-stu-id="70bcc-184">b.</span></span> <span data-ttu-id="70bcc-185">Seleccione **Use SAML For Authentication**(Usar SAML para autenticación).</span><span class="sxs-lookup"><span data-stu-id="70bcc-185">Select **Use SAML For Authentication**.</span></span>

    <span data-ttu-id="70bcc-186">c.</span><span class="sxs-lookup"><span data-stu-id="70bcc-186">c.</span></span> <span data-ttu-id="70bcc-187">tooupload Hola certificado descargado, haga clic en **cargar**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-187">tooupload hello downloaded certificate, click **Upload**.</span></span>

13. <span data-ttu-id="70bcc-188">Hola **solicitar** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="70bcc-188">In hello **Request** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="70bcc-189">![Solicitud](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Solicitud")</span><span class="sxs-lookup"><span data-stu-id="70bcc-189">![Request](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Request")</span></span>  

    <span data-ttu-id="70bcc-190">a.</span><span class="sxs-lookup"><span data-stu-id="70bcc-190">a.</span></span> <span data-ttu-id="70bcc-191">En **Request Binding Type** (Tipo de enlace de solicitud), seleccione **POST**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-191">As **Request Binding Type**, select **POST**.</span></span>

    <span data-ttu-id="70bcc-192">b.</span><span class="sxs-lookup"><span data-stu-id="70bcc-192">b.</span></span> <span data-ttu-id="70bcc-193">En el portal de Azure, en Hola Hola **configurar inicio de sesión único en Airwatch** página de diálogo, Hola copia **SAML Single Sign-On dirección URL del servicio** valor y, a continuación, péguelo en hello **proveedor de identidades Solo la dirección URL de inicio de sesión** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="70bcc-193">In hello Azure portal, on hello **Configure single sign-on at Airwatch** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Identity Provider Single Sign On URL** textbox.</span></span>

    <span data-ttu-id="70bcc-194">c.</span><span class="sxs-lookup"><span data-stu-id="70bcc-194">c.</span></span> <span data-ttu-id="70bcc-195">En la lista **NameID Format** (Formato de NameID), seleccione **Email address** (Dirección de correo electrónico).</span><span class="sxs-lookup"><span data-stu-id="70bcc-195">As **NameID Format**, select **Email Address**.</span></span>

    <span data-ttu-id="70bcc-196">d.</span><span class="sxs-lookup"><span data-stu-id="70bcc-196">d.</span></span> <span data-ttu-id="70bcc-197">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-197">Click **Save**.</span></span>

14. <span data-ttu-id="70bcc-198">Haga clic en hello **usuario** ficha de nuevo.</span><span class="sxs-lookup"><span data-stu-id="70bcc-198">Click hello **User** tab again.</span></span>
    
    <span data-ttu-id="70bcc-199">![Usuario](./media/active-directory-saas-airwatch-tutorial/ic791926.png "Usuario")</span><span class="sxs-lookup"><span data-stu-id="70bcc-199">![User](./media/active-directory-saas-airwatch-tutorial/ic791926.png "User")</span></span>

15. <span data-ttu-id="70bcc-200">Hola **atributo** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="70bcc-200">In hello **Attribute** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="70bcc-201">![Atributo](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Atributo")</span><span class="sxs-lookup"><span data-stu-id="70bcc-201">![Attribute](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribute")</span></span>

    <span data-ttu-id="70bcc-202">a.</span><span class="sxs-lookup"><span data-stu-id="70bcc-202">a.</span></span> <span data-ttu-id="70bcc-203">Hola **identificador de objeto** cuadro de texto, tipo **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-203">In hello **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>

    <span data-ttu-id="70bcc-204">b.</span><span class="sxs-lookup"><span data-stu-id="70bcc-204">b.</span></span> <span data-ttu-id="70bcc-205">Hola **nombre de usuario** cuadro de texto, tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-205">In hello **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="70bcc-206">c.</span><span class="sxs-lookup"><span data-stu-id="70bcc-206">c.</span></span> <span data-ttu-id="70bcc-207">Hola **nombre para mostrar** cuadro de texto, tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-207">In hello **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="70bcc-208">d.</span><span class="sxs-lookup"><span data-stu-id="70bcc-208">d.</span></span> <span data-ttu-id="70bcc-209">Hola **nombre** cuadro de texto, tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-209">In hello **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="70bcc-210">e.</span><span class="sxs-lookup"><span data-stu-id="70bcc-210">e.</span></span> <span data-ttu-id="70bcc-211">Hola **Last Name** cuadro de texto, tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-211">In hello **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

    <span data-ttu-id="70bcc-212">f.</span><span class="sxs-lookup"><span data-stu-id="70bcc-212">f.</span></span> <span data-ttu-id="70bcc-213">Hola **correo electrónico** cuadro de texto, tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-213">In hello **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="70bcc-214">g.</span><span class="sxs-lookup"><span data-stu-id="70bcc-214">g.</span></span> <span data-ttu-id="70bcc-215">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-215">Click **Save**.</span></span>

<CE>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="70bcc-216">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="70bcc-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="70bcc-217">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="70bcc-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="70bcc-219">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="70bcc-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="70bcc-220">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="70bcc-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="70bcc-222">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="70bcc-224">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="70bcc-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="70bcc-226">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="70bcc-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="70bcc-228">a.</span><span class="sxs-lookup"><span data-stu-id="70bcc-228">a.</span></span> <span data-ttu-id="70bcc-229">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="70bcc-230">b.</span><span class="sxs-lookup"><span data-stu-id="70bcc-230">b.</span></span> <span data-ttu-id="70bcc-231">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="70bcc-231">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="70bcc-232">c.</span><span class="sxs-lookup"><span data-stu-id="70bcc-232">c.</span></span> <span data-ttu-id="70bcc-233">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="70bcc-234">d.</span><span class="sxs-lookup"><span data-stu-id="70bcc-234">d.</span></span> <span data-ttu-id="70bcc-235">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-235">Click **Create**.</span></span>
 
### <a name="creating-a-airwatch-test-user"></a><span data-ttu-id="70bcc-236">Creación de un usuario de prueba de AirWatch</span><span class="sxs-lookup"><span data-stu-id="70bcc-236">Creating a AirWatch test user</span></span>

<span data-ttu-id="70bcc-237">toolog de los usuarios de Azure AD tooenable en tooAirWatch, se les deben aprovisionar en tooAirWatch.</span><span class="sxs-lookup"><span data-stu-id="70bcc-237">tooenable Azure AD users toolog in tooAirWatch, they must be provisioned in tooAirWatch.</span></span>

* <span data-ttu-id="70bcc-238">En el caso de AirWatch, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="70bcc-238">When AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="70bcc-239">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="70bcc-239">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="70bcc-240">Inicie sesión en tooyour **AirWatch** como administrador.</span><span class="sxs-lookup"><span data-stu-id="70bcc-240">Log in tooyour **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="70bcc-241">En el panel de navegación de hello en el lado izquierdo de hello, haga clic en **cuentas**y, a continuación, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-241">In hello navigation pane on hello left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="70bcc-242">![Usuarios](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="70bcc-242">![Users](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Users")</span></span>
3. <span data-ttu-id="70bcc-243">Hola **usuarios** menú, haga clic en **vista de lista**y, a continuación, haga clic en **agregar \> Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-243">In hello **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="70bcc-244">![Agregar usuario](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="70bcc-244">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Add User")</span></span>
4. <span data-ttu-id="70bcc-245">En hello **Agregar / Editar usuario** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="70bcc-245">On hello **Add / Edit User** dialog, perform hello following steps:</span></span>

   <span data-ttu-id="70bcc-246">![Agregar usuario](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="70bcc-246">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Add User")</span></span>   
   1. <span data-ttu-id="70bcc-247">Hola de tipo **nombre de usuario**, **contraseña**, **Confirmar contraseña**, **nombre**, **Last Name**,  **Dirección de correo electrónico** de un Azure válida cuadros de texto relacionadas con la cuenta de Active Directory que quiera tooprovision en Hola.</span><span class="sxs-lookup"><span data-stu-id="70bcc-247">Type hello **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="70bcc-248">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-248">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="70bcc-249">Puede usar cualquier otra AirWatch usuario cuenta herramienta de creación o las API proporcionadas por AirWatch tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="70bcc-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="70bcc-250">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="70bcc-250">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="70bcc-251">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooAirWatch.</span><span class="sxs-lookup"><span data-stu-id="70bcc-251">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAirWatch.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="70bcc-253">**tooassign Britta Simon tooAirWatch, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="70bcc-253">**tooassign Britta Simon tooAirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="70bcc-254">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-254">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="70bcc-256">En la lista de aplicaciones de hello, seleccione **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-256">In hello applications list, select **AirWatch**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. <span data-ttu-id="70bcc-258">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-258">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="70bcc-260">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-260">Click **Add** button.</span></span> <span data-ttu-id="70bcc-261">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-261">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="70bcc-263">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="70bcc-263">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="70bcc-264">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-264">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="70bcc-265">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-265">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="70bcc-266">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="70bcc-266">Testing single sign-on</span></span>

<span data-ttu-id="70bcc-267">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="70bcc-267">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="70bcc-268">Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="70bcc-268">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="70bcc-269">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="70bcc-269">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="70bcc-270">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="70bcc-270">Additional resources</span></span>

* [<span data-ttu-id="70bcc-271">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70bcc-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="70bcc-272">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="70bcc-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

