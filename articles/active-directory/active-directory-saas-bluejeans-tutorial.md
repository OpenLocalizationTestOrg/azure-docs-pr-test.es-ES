---
title: "Tutorial: integración de Azure Active Directory con BlueJeans | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y BlueJeans."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 67613303a9f854afbf4619418cc1607d329caf94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a><span data-ttu-id="4218b-103">Tutorial: Integración de Azure Active Directory con BlueJeans</span><span class="sxs-lookup"><span data-stu-id="4218b-103">Tutorial: Azure Active Directory integration with BlueJeans</span></span>

<span data-ttu-id="4218b-104">En este tutorial, aprenderá cómo toointegrate BlueJeans con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4218b-104">In this tutorial, you learn how toointegrate BlueJeans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4218b-105">Integración BlueJeans con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="4218b-105">Integrating BlueJeans with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4218b-106">Puede controlar en Azure AD que tenga acceso tooBlueJeans</span><span class="sxs-lookup"><span data-stu-id="4218b-106">You can control in Azure AD who has access tooBlueJeans</span></span>
- <span data-ttu-id="4218b-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooBlueJeans (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4218b-107">You can enable your users tooautomatically get signed-on tooBlueJeans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4218b-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4218b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4218b-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4218b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4218b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4218b-110">Prerequisites</span></span>

<span data-ttu-id="4218b-111">integración de Azure AD con BlueJeans tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="4218b-111">tooconfigure Azure AD integration with BlueJeans, you need hello following items:</span></span>

- <span data-ttu-id="4218b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4218b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4218b-113">Una suscripción habilitada para el inicio de sesión único en BlueJeans</span><span class="sxs-lookup"><span data-stu-id="4218b-113">A BlueJeans single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4218b-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="4218b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4218b-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="4218b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4218b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4218b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4218b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4218b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4218b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="4218b-118">Scenario description</span></span>
<span data-ttu-id="4218b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="4218b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4218b-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="4218b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4218b-121">Agregar BlueJeans desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="4218b-121">Adding BlueJeans from hello gallery</span></span>
2. <span data-ttu-id="4218b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4218b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bluejeans-from-hello-gallery"></a><span data-ttu-id="4218b-123">Agregar BlueJeans desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="4218b-123">Adding BlueJeans from hello gallery</span></span>
<span data-ttu-id="4218b-124">integración de hello tooconfigure de BlueJeans en Azure AD, deberá tooadd BlueJeans de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="4218b-124">tooconfigure hello integration of BlueJeans into Azure AD, you need tooadd BlueJeans from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4218b-125">**tooadd BlueJeans de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4218b-125">**tooadd BlueJeans from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4218b-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="4218b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4218b-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="4218b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4218b-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4218b-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="4218b-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4218b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="4218b-133">En el cuadro de búsqueda de hello, escriba **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="4218b-133">In hello search box, type **BlueJeans**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. <span data-ttu-id="4218b-135">En el panel de resultados de hello, seleccione **BlueJeans**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4218b-135">In hello results panel, select **BlueJeans**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4218b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4218b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4218b-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con BlueJeans con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4218b-138">In this section, you configure and test Azure AD single sign-on with BlueJeans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4218b-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en BlueJeans es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4218b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BlueJeans is tooa user in Azure AD.</span></span> <span data-ttu-id="4218b-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en BlueJeans debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="4218b-140">In other words, a link relationship between an Azure AD user and hello related user in BlueJeans needs toobe established.</span></span>

<span data-ttu-id="4218b-141">En BlueJeans, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4218b-141">In BlueJeans, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4218b-142">tooconfigure y prueba de inicio de sesión único en Azure AD con BlueJeans, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="4218b-142">tooconfigure and test Azure AD single sign-on with BlueJeans, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4218b-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="4218b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4218b-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4218b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4218b-145">**[Crear un usuario de prueba de BlueJeans](#creating-a-bluejeans-test-user)**  -toohave un equivalente de Britta Simon en BlueJeans que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="4218b-145">**[Creating a BlueJeans test user](#creating-a-bluejeans-test-user)** - toohave a counterpart of Britta Simon in BlueJeans that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4218b-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4218b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4218b-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="4218b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4218b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4218b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4218b-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="4218b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BlueJeans application.</span></span>

<span data-ttu-id="4218b-150">**inicio de sesión único en tooconfigure Azure AD con BlueJeans, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4218b-150">**tooconfigure Azure AD single sign-on with BlueJeans, perform hello following steps:**</span></span>

1. <span data-ttu-id="4218b-151">En el portal de Azure, en Hola Hola **BlueJeans** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="4218b-151">In hello Azure portal, on hello **BlueJeans** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="4218b-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4218b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. <span data-ttu-id="4218b-155">En hello **BlueJeans dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4218b-155">On hello **BlueJeans Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    <span data-ttu-id="4218b-157">a.</span><span class="sxs-lookup"><span data-stu-id="4218b-157">a.</span></span> <span data-ttu-id="4218b-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="4218b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    <span data-ttu-id="4218b-159">b.</span><span class="sxs-lookup"><span data-stu-id="4218b-159">b.</span></span> <span data-ttu-id="4218b-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="4218b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4218b-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="4218b-161">These values are not real.</span></span> <span data-ttu-id="4218b-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="4218b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4218b-163">Póngase en contacto con [equipo de soporte técnico de cliente de BlueJeans](https://support.bluejeans.com/contact) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="4218b-163">Contact [BlueJeans Client support team](https://support.bluejeans.com/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="4218b-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4218b-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. <span data-ttu-id="4218b-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="4218b-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4218b-168">En hello **configuración de BlueJeans** sección, haga clic en **configurar BlueJeans** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="4218b-168">On hello **BlueJeans Configuration** section, click **Configure BlueJeans** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4218b-169">Hola copia **dirección URL de cierre de sesión, cambiar dirección URL de contraseña y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="4218b-169">Copy hello **Sign-Out URL, Change Password URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. <span data-ttu-id="4218b-171">En una ventana del explorador web diferente, inicie sesión en tooyour **BlueJeans** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="4218b-171">In a different web browser window, log in tooyour **BlueJeans** company site as an administrator.</span></span>

8. <span data-ttu-id="4218b-172">Vaya demasiado**administración \> configuración del grupo de \> seguridad**.</span><span class="sxs-lookup"><span data-stu-id="4218b-172">Go too**ADMIN \> Group Settings \> Security**.</span></span>
   
   <span data-ttu-id="4218b-173">![Administración](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="4218b-173">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span></span>

9. <span data-ttu-id="4218b-174">Hola **seguridad** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4218b-174">In hello **Security** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="4218b-175">![Inicio de sesión único de SAML](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "Inicio de sesión único de SAML")</span><span class="sxs-lookup"><span data-stu-id="4218b-175">![SAML Single Sign On](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span></span>   
   
   <span data-ttu-id="4218b-176">a.</span><span class="sxs-lookup"><span data-stu-id="4218b-176">a.</span></span> <span data-ttu-id="4218b-177">Seleccione **SAML Single Sign On**(Inicio de sesión único de SAML).</span><span class="sxs-lookup"><span data-stu-id="4218b-177">Select **SAML Single Sign On**.</span></span>
  
   <span data-ttu-id="4218b-178">b.</span><span class="sxs-lookup"><span data-stu-id="4218b-178">b.</span></span> <span data-ttu-id="4218b-179">Seleccione **Enable automatic provisioning**(Habilitar aprovisionamiento automático).</span><span class="sxs-lookup"><span data-stu-id="4218b-179">Select **Enable automatic provisioning**.</span></span>

10. <span data-ttu-id="4218b-180">Continúe con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="4218b-180">Move on with hello following steps:</span></span>

    <span data-ttu-id="4218b-181">![Ruta del certificado](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Ruta del certificado")</span><span class="sxs-lookup"><span data-stu-id="4218b-181">![Certificate Path](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Certificate Path")</span></span>
    
    <span data-ttu-id="4218b-182">a.</span><span class="sxs-lookup"><span data-stu-id="4218b-182">a.</span></span> <span data-ttu-id="4218b-183">Haga clic en **Elegir archivo**y, a continuación, cargar el certificado de hello descargado.</span><span class="sxs-lookup"><span data-stu-id="4218b-183">Click **Choose File**, and then upload hello downloaded certificate.</span></span>
   
    <span data-ttu-id="4218b-184">b.</span><span class="sxs-lookup"><span data-stu-id="4218b-184">b.</span></span> <span data-ttu-id="4218b-185">Pegar **SAML Single Sign-On dirección URL del servicio** en hello **dirección URL de inicio de sesión** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="4218b-185">Paste **SAML Single Sign-On Service URL** into hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="4218b-186">c.</span><span class="sxs-lookup"><span data-stu-id="4218b-186">c.</span></span> <span data-ttu-id="4218b-187">Pegar **cambiar dirección URL de contraseña** en hello **dirección URL de cambio de contraseña** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="4218b-187">Paste **Change Password URL** into hello **Password Change URL** textbox.</span></span>
   
    <span data-ttu-id="4218b-188">d.</span><span class="sxs-lookup"><span data-stu-id="4218b-188">d.</span></span> <span data-ttu-id="4218b-189">Pegar **dirección URL de cierre de sesión** en hello **Logout URL** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="4218b-189">Paste **Sign-Out URL** into hello **Logout URL** textbox.</span></span>

11. <span data-ttu-id="4218b-190">Continúe con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="4218b-190">Move on with hello following steps:</span></span>
    
    <span data-ttu-id="4218b-191">![Guardar cambios](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Guardar cambios")</span><span class="sxs-lookup"><span data-stu-id="4218b-191">![Save Changes](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Save Changes")</span></span>
    
    <span data-ttu-id="4218b-192">a.</span><span class="sxs-lookup"><span data-stu-id="4218b-192">a.</span></span> <span data-ttu-id="4218b-193">Hola **Id. de usuario** cuadro de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="4218b-193">In hello **User id** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="4218b-194">b.</span><span class="sxs-lookup"><span data-stu-id="4218b-194">b.</span></span> <span data-ttu-id="4218b-195">Hola **correo electrónico** cuadro de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="4218b-195">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="4218b-196">c.</span><span class="sxs-lookup"><span data-stu-id="4218b-196">c.</span></span> <span data-ttu-id="4218b-197">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="4218b-197">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="4218b-198">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="4218b-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4218b-199">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="4218b-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4218b-200">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4218b-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4218b-201">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4218b-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="4218b-202">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="4218b-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="4218b-204">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4218b-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4218b-205">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="4218b-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4218b-207">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4218b-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4218b-209">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4218b-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4218b-211">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="4218b-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4218b-213">a.</span><span class="sxs-lookup"><span data-stu-id="4218b-213">a.</span></span> <span data-ttu-id="4218b-214">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4218b-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4218b-215">b.</span><span class="sxs-lookup"><span data-stu-id="4218b-215">b.</span></span> <span data-ttu-id="4218b-216">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4218b-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4218b-217">c.</span><span class="sxs-lookup"><span data-stu-id="4218b-217">c.</span></span> <span data-ttu-id="4218b-218">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="4218b-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4218b-219">d.</span><span class="sxs-lookup"><span data-stu-id="4218b-219">d.</span></span> <span data-ttu-id="4218b-220">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4218b-220">Click **Create**.</span></span>
 
### <a name="creating-a-bluejeans-test-user"></a><span data-ttu-id="4218b-221">Creación de un usuario de prueba de BlueJeans</span><span class="sxs-lookup"><span data-stu-id="4218b-221">Creating a BlueJeans test user</span></span>

<span data-ttu-id="4218b-222">toolog de los usuarios de Azure AD tooenable en tooBlueJeans, se les deben aprovisionar en BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="4218b-222">tooenable Azure AD users toolog in tooBlueJeans, they must be provisioned into BlueJeans.</span></span>  

<span data-ttu-id="4218b-223">En el caso de BlueJeans, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="4218b-223">In case of BlueJeans, provisioning is a manual task.</span></span>

<span data-ttu-id="4218b-224">**tooprovision una cuenta de usuario, realizar Hola lo siguiente:**</span><span class="sxs-lookup"><span data-stu-id="4218b-224">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="4218b-225">Inicie sesión en tooyour **BlueJeans** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="4218b-225">Log in tooyour **BlueJeans** company site as an administrator.</span></span>

2. <span data-ttu-id="4218b-226">Vaya demasiado**administración \> administrar usuarios \> Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="4218b-226">Go too**ADMIN \> Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="4218b-227">![Administración](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="4218b-227">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span></span>
   
   >[!IMPORTANT]
   ><span data-ttu-id="4218b-228">Hola **Agregar usuario** ficha solo está disponible si es, en hello **ficha seguridad**, **habilitar el aprovisionamiento automático** está desactivada.</span><span class="sxs-lookup"><span data-stu-id="4218b-228">hello **Add User** tab is only available if, in hello **Security tab**, **Enable automatic provisioning** is unchecked.</span></span> 
   
3. <span data-ttu-id="4218b-229">Hola **Agregar usuario** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4218b-229">In hello **Add User** section, perform hello following steps:</span></span>

    <span data-ttu-id="4218b-230">![Agregar usuario](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="4218b-230">![Add User](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Add User")</span></span>
    
    <span data-ttu-id="4218b-231">a.</span><span class="sxs-lookup"><span data-stu-id="4218b-231">a.</span></span> <span data-ttu-id="4218b-232">Escriba un **nombre de usuario de BlueJeans**, **dirección de correo electrónico**, un **Id. de reunión BlueJeans**, **código de acceso de moderador**, un **nombre completo** , hello **empresa** de una cuenta válida de AAD que quiera tooprovision en hello relacionados con cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="4218b-232">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, hello **Company** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
    
    <span data-ttu-id="4218b-233">b.</span><span class="sxs-lookup"><span data-stu-id="4218b-233">b.</span></span> <span data-ttu-id="4218b-234">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="4218b-234">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="4218b-235">Puede usar cualquier otra BlueJeans usuario cuenta herramienta de creación o las API proporcionadas por BlueJeans tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="4218b-235">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4218b-236">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4218b-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4218b-237">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooBlueJeans.</span><span class="sxs-lookup"><span data-stu-id="4218b-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlueJeans.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="4218b-239">**tooassign Britta Simon tooBlueJeans, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4218b-239">**tooassign Britta Simon tooBlueJeans, perform hello following steps:**</span></span>

1. <span data-ttu-id="4218b-240">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4218b-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="4218b-242">En la lista de aplicaciones de hello, seleccione **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="4218b-242">In hello applications list, select **BlueJeans**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. <span data-ttu-id="4218b-244">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4218b-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="4218b-246">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4218b-246">Click **Add** button.</span></span> <span data-ttu-id="4218b-247">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4218b-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="4218b-249">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="4218b-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4218b-250">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4218b-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4218b-251">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4218b-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4218b-252">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="4218b-252">Testing single sign-on</span></span>

<span data-ttu-id="4218b-253">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4218b-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4218b-254">Al hacer clic en hello BlueJeans disponer en mosaico en el Panel de acceso de hello, deberá obtener la página de inicio de sesión de aplicación de BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="4218b-254">When you click hello BlueJeans tile in hello Access Panel, you should get login page of BlueJeans application.</span></span>
<span data-ttu-id="4218b-255">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4218b-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4218b-256">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4218b-256">Additional resources</span></span>

* [<span data-ttu-id="4218b-257">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4218b-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4218b-258">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4218b-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

