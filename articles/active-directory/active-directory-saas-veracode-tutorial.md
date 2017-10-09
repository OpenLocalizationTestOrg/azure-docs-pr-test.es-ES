---
title: "Tutorial: Integración de Azure Active Directory con Veracode | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Veracode."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d17307b3864b7df8ee55f569d8f962e2e315b936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a><span data-ttu-id="f4acc-103">Tutorial: integración de Azure Active Directory con Veracode</span><span class="sxs-lookup"><span data-stu-id="f4acc-103">Tutorial: Azure Active Directory integration with Veracode</span></span>

<span data-ttu-id="f4acc-104">En este tutorial, aprenderá cómo toointegrate Veracode con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f4acc-104">In this tutorial, you learn how toointegrate Veracode with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f4acc-105">Integración Veracode con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="f4acc-105">Integrating Veracode with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f4acc-106">Puede controlar en Azure AD que tenga acceso tooVeracode.</span><span class="sxs-lookup"><span data-stu-id="f4acc-106">You can control in Azure AD who has access tooVeracode.</span></span>
- <span data-ttu-id="f4acc-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooVeracode (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4acc-107">You can enable your users tooautomatically get signed-on tooVeracode (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f4acc-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4acc-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="f4acc-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f4acc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4acc-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f4acc-110">Prerequisites</span></span>

<span data-ttu-id="f4acc-111">integración de Azure AD con Veracode tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f4acc-111">tooconfigure Azure AD integration with Veracode, you need hello following items:</span></span>

- <span data-ttu-id="f4acc-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4acc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f4acc-113">Una suscripción habilitada para el inicio de sesión único en Veracode</span><span class="sxs-lookup"><span data-stu-id="f4acc-113">A Veracode single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f4acc-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="f4acc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f4acc-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="f4acc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f4acc-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f4acc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f4acc-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f4acc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f4acc-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="f4acc-118">Scenario description</span></span>
<span data-ttu-id="f4acc-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="f4acc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f4acc-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="f4acc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f4acc-121">Agregar Veracode de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="f4acc-121">Add Veracode from hello gallery</span></span>
2. <span data-ttu-id="f4acc-122">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4acc-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-veracode-from-hello-gallery"></a><span data-ttu-id="f4acc-123">Agregar Veracode de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="f4acc-123">Add Veracode from hello gallery</span></span>
<span data-ttu-id="f4acc-124">integración de hello tooconfigure de Veracode en Azure AD, deberá tooadd Veracode de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="f4acc-124">tooconfigure hello integration of Veracode into Azure AD, you need tooadd Veracode from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f4acc-125">**tooadd Veracode de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f4acc-125">**tooadd Veracode from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4acc-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="f4acc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="f4acc-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f4acc-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="f4acc-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f4acc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="f4acc-133">En el cuadro de búsqueda de hello, escriba **Veracode**, seleccione **Veracode** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f4acc-133">In hello search box, type **Veracode**, select  **Veracode** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Veracode en la lista de resultados de Hola](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f4acc-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4acc-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f4acc-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Veracode con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f4acc-136">In this section, you configure and test Azure AD single sign-on with Veracode based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f4acc-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Veracode es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4acc-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Veracode is tooa user in Azure AD.</span></span> <span data-ttu-id="f4acc-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Veracode debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="f4acc-138">In other words, a link relationship between an Azure AD user and hello related user in Veracode needs toobe established.</span></span>

<span data-ttu-id="f4acc-139">En Veracode, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4acc-139">In Veracode, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f4acc-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Veracode, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="f4acc-140">tooconfigure and test Azure AD single sign-on with Veracode, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f4acc-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="f4acc-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f4acc-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f4acc-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f4acc-143">**[Crear un usuario de prueba Veracode](#create-a-veracode-test-user)**  -toohave un equivalente de Britta Simon en Veracode que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="f4acc-143">**[Create a Veracode test user](#create-a-veracode-test-user)** - toohave a counterpart of Britta Simon in Veracode that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f4acc-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f4acc-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f4acc-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="f4acc-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f4acc-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4acc-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f4acc-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Veracode.</span><span class="sxs-lookup"><span data-stu-id="f4acc-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Veracode application.</span></span>

<span data-ttu-id="f4acc-148">**inicio de sesión único en Azure AD tooconfigure con Veracode, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f4acc-148">**tooconfigure Azure AD single sign-on with Veracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4acc-149">En el portal de Azure, en Hola Hola **Veracode** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-149">In hello Azure portal, on hello **Veracode** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="f4acc-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f4acc-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. <span data-ttu-id="f4acc-153">En hello **Veracode dominio y las direcciones URL** sección, el usuario no tiene tooperform pasos como aplicación hello ya está integrado previamente con Azure.</span><span class="sxs-lookup"><span data-stu-id="f4acc-153">On hello **Veracode Domain and URLs** section, the user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. <span data-ttu-id="f4acc-155">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f4acc-155">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. <span data-ttu-id="f4acc-157">objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooVeracode con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4acc-157">hello objective of this section is toooutline how tooenable users tooauthenticate tooVeracode with their account in Azure AD using federation based on hello SAML protocol.</span></span>

    <span data-ttu-id="f4acc-158">La aplicación de Veracode espera las aserciones de SAML de hello en un formato específico, lo que requiere tooyour de asignaciones de atributo personalizado de tooadd **atributos de token saml** configuración.</span><span class="sxs-lookup"><span data-stu-id="f4acc-158">Your Veracode application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> <span data-ttu-id="f4acc-159">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="f4acc-159">hello following screenshot shows an example for this.</span></span>
    
    <span data-ttu-id="f4acc-160">![Atributos](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="f4acc-160">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributes")</span></span>

6. <span data-ttu-id="f4acc-161">asignaciones de atributos de tooadd Hola necesario, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="f4acc-161">tooadd hello required attribute mappings, perform hello following steps:</span></span>

    | <span data-ttu-id="f4acc-162">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="f4acc-162">Attribute Name</span></span> | <span data-ttu-id="f4acc-163">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="f4acc-163">Attribute Value</span></span> |
    |--- |--- |
    | <span data-ttu-id="f4acc-164">firstname</span><span class="sxs-lookup"><span data-stu-id="f4acc-164">firstname</span></span> |<span data-ttu-id="f4acc-165">User.givenname</span><span class="sxs-lookup"><span data-stu-id="f4acc-165">User.givenname</span></span> |
    | <span data-ttu-id="f4acc-166">lastname</span><span class="sxs-lookup"><span data-stu-id="f4acc-166">lastname</span></span> |<span data-ttu-id="f4acc-167">User.surname</span><span class="sxs-lookup"><span data-stu-id="f4acc-167">User.surname</span></span> |
    | <span data-ttu-id="f4acc-168">email</span><span class="sxs-lookup"><span data-stu-id="f4acc-168">email</span></span> |<span data-ttu-id="f4acc-169">User.mail</span><span class="sxs-lookup"><span data-stu-id="f4acc-169">User.mail</span></span> |
    
    <span data-ttu-id="f4acc-170">a.</span><span class="sxs-lookup"><span data-stu-id="f4acc-170">a.</span></span> <span data-ttu-id="f4acc-171">Para cada fila de datos de tabla de hello anterior, haga clic en **Agregar atributo de usuario**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-171">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="f4acc-172">![Atributos](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="f4acc-172">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributes")</span></span>
    
    <span data-ttu-id="f4acc-173">![Atributos](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="f4acc-173">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributes")</span></span>
    
    <span data-ttu-id="f4acc-174">b.</span><span class="sxs-lookup"><span data-stu-id="f4acc-174">b.</span></span> <span data-ttu-id="f4acc-175">Hola **nombre del atributo** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="f4acc-175">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="f4acc-176">c.</span><span class="sxs-lookup"><span data-stu-id="f4acc-176">c.</span></span> <span data-ttu-id="f4acc-177">Hola **valor del atributo** cuadro de texto, valor de atributo seleccione Hola se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="f4acc-177">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="f4acc-178">d.</span><span class="sxs-lookup"><span data-stu-id="f4acc-178">d.</span></span> <span data-ttu-id="f4acc-179">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-179">Click **Ok**.</span></span>

7. <span data-ttu-id="f4acc-180">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="f4acc-180">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f4acc-182">En hello **Veracode configuración** sección, haga clic en **configurar Veracode** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="f4acc-182">On hello **Veracode Configuration** section, click **Configure Veracode** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f4acc-183">Hola copia **Id. de entidad SAML** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="f4acc-183">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configuración de Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. <span data-ttu-id="f4acc-185">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de Veracode como administrador.</span><span class="sxs-lookup"><span data-stu-id="f4acc-185">In a different web browser window, log into your Veracode company site as an administrator.</span></span>

10. <span data-ttu-id="f4acc-186">En el menú de hello en la parte superior de hello, haga clic en **configuración**y, a continuación, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-186">In hello menu on hello top, click **Settings**, and then click **Admin**.</span></span>
   
    <span data-ttu-id="f4acc-187">![Administración](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="f4acc-187">![Administration](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administration")</span></span>

11. <span data-ttu-id="f4acc-188">Haga clic en hello **SAML** ficha.</span><span class="sxs-lookup"><span data-stu-id="f4acc-188">Click hello **SAML** tab.</span></span>

12. <span data-ttu-id="f4acc-189">Hola **configuración de SAML de la organización** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="f4acc-189">In hello **Organization SAML Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f4acc-190">![Administración](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="f4acc-190">![Administration](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administration")</span></span>
   
    <span data-ttu-id="f4acc-191">a.</span><span class="sxs-lookup"><span data-stu-id="f4acc-191">a.</span></span>  <span data-ttu-id="f4acc-192">En **emisor** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4acc-192">In  **Issuer** textbox, paste hello value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="f4acc-193">b.</span><span class="sxs-lookup"><span data-stu-id="f4acc-193">b.</span></span> <span data-ttu-id="f4acc-194">tooupload el certificado descargado del portal de Azure, haga clic en ejecutar **Elegir archivo**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-194">tooupload your downloaded certificate from Azure portal, click **Choose File**.</span></span>
   
    <span data-ttu-id="f4acc-195">c.</span><span class="sxs-lookup"><span data-stu-id="f4acc-195">c.</span></span> <span data-ttu-id="f4acc-196">Seleccione **Habilitar registro automático**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-196">Select **Enable Self Registration**.</span></span>

13. <span data-ttu-id="f4acc-197">Hola **configuración del registro de autoservicio** sección realizar pasos de Hola y, a continuación, haga clic en **guardar**:</span><span class="sxs-lookup"><span data-stu-id="f4acc-197">In hello **Self Registration Settings** section, perform hello following steps, and then click **Save**:</span></span>
   
    <span data-ttu-id="f4acc-198">![Administración](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="f4acc-198">![Administration](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administration")</span></span>
   
    <span data-ttu-id="f4acc-199">a.</span><span class="sxs-lookup"><span data-stu-id="f4acc-199">a.</span></span> <span data-ttu-id="f4acc-200">Como **Activación de nuevo usuario**, seleccione **No se requiere ninguna activación**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-200">As **New User Activation**, select **No Activation Required**.</span></span>
   
    <span data-ttu-id="f4acc-201">b.</span><span class="sxs-lookup"><span data-stu-id="f4acc-201">b.</span></span> <span data-ttu-id="f4acc-202">Como **Actualizaciones de datos de usuario**, seleccione **Datos de usuario de Veracode de preferencia**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-202">As **User Data Updates**, select **Preference Veracode User Data**.</span></span>
   
    <span data-ttu-id="f4acc-203">c.</span><span class="sxs-lookup"><span data-stu-id="f4acc-203">c.</span></span> <span data-ttu-id="f4acc-204">Para **detalles de atributos de SAML**, seleccione Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="f4acc-204">For **SAML Attribute Details**, select hello following:</span></span>
      * <span data-ttu-id="f4acc-205">**Roles de usuario**</span><span class="sxs-lookup"><span data-stu-id="f4acc-205">**User Roles**</span></span>
      * <span data-ttu-id="f4acc-206">**Administrador de directivas**</span><span class="sxs-lookup"><span data-stu-id="f4acc-206">**Policy Administrator**</span></span>
      * <span data-ttu-id="f4acc-207">**Revisor**</span><span class="sxs-lookup"><span data-stu-id="f4acc-207">**Reviewer**</span></span>
      * <span data-ttu-id="f4acc-208">**Principal de seguridad**</span><span class="sxs-lookup"><span data-stu-id="f4acc-208">**Security Lead**</span></span>
      * <span data-ttu-id="f4acc-209">**Ejecutivo**</span><span class="sxs-lookup"><span data-stu-id="f4acc-209">**Executive**</span></span>
      * <span data-ttu-id="f4acc-210">**Remitente**</span><span class="sxs-lookup"><span data-stu-id="f4acc-210">**Submitter**</span></span>
      * <span data-ttu-id="f4acc-211">**Creador**</span><span class="sxs-lookup"><span data-stu-id="f4acc-211">**Creator**</span></span>
      * <span data-ttu-id="f4acc-212">**Todos los tipos de detección**</span><span class="sxs-lookup"><span data-stu-id="f4acc-212">**All Scan Types**</span></span>
      * <span data-ttu-id="f4acc-213">**Pertenencias a equipos**</span><span class="sxs-lookup"><span data-stu-id="f4acc-213">**Team Memberships**</span></span>
      * <span data-ttu-id="f4acc-214">**Equipo predeterminado**</span><span class="sxs-lookup"><span data-stu-id="f4acc-214">**Default Team**</span></span>

> [!TIP]
> <span data-ttu-id="f4acc-215">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="f4acc-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f4acc-216">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="f4acc-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f4acc-217">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f4acc-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f4acc-218">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4acc-218">Create an Azure AD test user</span></span>

<span data-ttu-id="f4acc-219">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="f4acc-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="f4acc-221">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f4acc-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4acc-222">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="f4acc-222">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f4acc-224">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-224">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f4acc-226">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f4acc-226">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f4acc-228">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="f4acc-228">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f4acc-230">a.</span><span class="sxs-lookup"><span data-stu-id="f4acc-230">a.</span></span> <span data-ttu-id="f4acc-231">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-231">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f4acc-232">b.</span><span class="sxs-lookup"><span data-stu-id="f4acc-232">b.</span></span> <span data-ttu-id="f4acc-233">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f4acc-233">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="f4acc-234">c.</span><span class="sxs-lookup"><span data-stu-id="f4acc-234">c.</span></span> <span data-ttu-id="f4acc-235">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="f4acc-235">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="f4acc-236">d.</span><span class="sxs-lookup"><span data-stu-id="f4acc-236">d.</span></span> <span data-ttu-id="f4acc-237">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-237">Click **Create**.</span></span>
 
### <a name="create-a-veracode-test-user"></a><span data-ttu-id="f4acc-238">Creación de un usuario de prueba de Veracode</span><span class="sxs-lookup"><span data-stu-id="f4acc-238">Create a Veracode test user</span></span>
<span data-ttu-id="f4acc-239">En orden tooenable toolog de los usuarios de Azure AD en Veracode, se les deben aprovisionar en Veracode.</span><span class="sxs-lookup"><span data-stu-id="f4acc-239">In order tooenable Azure AD users toolog into Veracode, they must be provisioned into Veracode.</span></span> <span data-ttu-id="f4acc-240">En caso de hello de Veracode, el aprovisionamiento es una tarea automatizada.</span><span class="sxs-lookup"><span data-stu-id="f4acc-240">In hello case of Veracode, provisioning is an automated task.</span></span> <span data-ttu-id="f4acc-241">No hay ningún elemento de acción para usted.</span><span class="sxs-lookup"><span data-stu-id="f4acc-241">There is no action item for you.</span></span> <span data-ttu-id="f4acc-242">Los usuarios se crean automáticamente si es necesario durante Hola primer único inicio de sesión intento.</span><span class="sxs-lookup"><span data-stu-id="f4acc-242">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

> [!NOTE]
> <span data-ttu-id="f4acc-243">Puede usar cualquier otra Veracode usuario cuenta herramienta de creación o las API proporcionadas por Veracode tooprovision cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4acc-243">You can use any other Veracode user account creation tools or APIs provided by Veracode tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="f4acc-244">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4acc-244">Assign hello Azure AD test user</span></span>

<span data-ttu-id="f4acc-245">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooVeracode.</span><span class="sxs-lookup"><span data-stu-id="f4acc-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVeracode.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="f4acc-247">**tooassign Britta Simon tooVeracode, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f4acc-247">**tooassign Britta Simon tooVeracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4acc-248">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="f4acc-250">En la lista de aplicaciones de hello, seleccione **Veracode**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-250">In hello applications list, select **Veracode**.</span></span>

    ![vínculo de Veracode Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. <span data-ttu-id="f4acc-252">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="f4acc-254">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-254">Click **Add** button.</span></span> <span data-ttu-id="f4acc-255">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="f4acc-257">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4acc-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f4acc-258">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f4acc-259">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f4acc-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f4acc-260">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="f4acc-260">Test single sign-on</span></span>

<span data-ttu-id="f4acc-261">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="f4acc-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f4acc-262">Al hacer clic en icono de Veracode Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Veracode aplicación.</span><span class="sxs-lookup"><span data-stu-id="f4acc-262">When you click hello Veracode tile in hello Access Panel, you should get automatically signed-on tooyour Veracode application.</span></span>
<span data-ttu-id="f4acc-263">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f4acc-263">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f4acc-264">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f4acc-264">Additional resources</span></span>

* [<span data-ttu-id="f4acc-265">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4acc-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f4acc-266">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f4acc-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

