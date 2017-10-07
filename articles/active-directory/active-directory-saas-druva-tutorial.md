---
title: "Tutorial: Integración de Azure Active Directory con Druva | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Druva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: a1c36c06d6d005e0aa363fbf34efe630e4cca1ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a><span data-ttu-id="e7288-103">Tutorial: Integración de Azure Active Directory con Druva</span><span class="sxs-lookup"><span data-stu-id="e7288-103">Tutorial: Azure Active Directory integration with Druva</span></span>

<span data-ttu-id="e7288-104">En este tutorial, aprenderá cómo toointegrate Druva con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e7288-104">In this tutorial, you learn how toointegrate Druva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e7288-105">Integración de Druva con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e7288-105">Integrating Druva with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e7288-106">Puede controlar en Azure AD que tenga acceso tooDruva.</span><span class="sxs-lookup"><span data-stu-id="e7288-106">You can control in Azure AD who has access tooDruva.</span></span>
- <span data-ttu-id="e7288-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooDruva (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7288-107">You can enable your users tooautomatically get signed-on tooDruva (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e7288-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7288-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="e7288-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e7288-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7288-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e7288-110">Prerequisites</span></span>

<span data-ttu-id="e7288-111">integración de Azure AD con Druva tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e7288-111">tooconfigure Azure AD integration with Druva, you need hello following items:</span></span>

- <span data-ttu-id="e7288-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7288-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e7288-113">Una suscripción habilitada para el inicio de sesión único en Druva</span><span class="sxs-lookup"><span data-stu-id="e7288-113">A Druva single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e7288-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e7288-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e7288-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e7288-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e7288-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e7288-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e7288-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7288-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e7288-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e7288-118">Scenario description</span></span>
<span data-ttu-id="e7288-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e7288-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e7288-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="e7288-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e7288-121">Agregar Druva desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e7288-121">Adding Druva from hello gallery</span></span>
2. <span data-ttu-id="e7288-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7288-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-druva-from-hello-gallery"></a><span data-ttu-id="e7288-123">Agregar Druva desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e7288-123">Adding Druva from hello gallery</span></span>
<span data-ttu-id="e7288-124">integración de hello tooconfigure de Druva en Azure AD, deberá tooadd Druva de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="e7288-124">tooconfigure hello integration of Druva into Azure AD, you need tooadd Druva from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e7288-125">**tooadd Druva de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e7288-125">**tooadd Druva from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7288-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="e7288-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="e7288-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e7288-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e7288-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e7288-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="e7288-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e7288-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="e7288-133">En el cuadro de búsqueda de hello, escriba **Druva**, seleccione **Druva** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e7288-133">In hello search box, type **Druva**, select **Druva** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados de Druva Hola](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e7288-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7288-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e7288-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Druva con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e7288-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e7288-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Druva es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7288-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Druva is tooa user in Azure AD.</span></span> <span data-ttu-id="e7288-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Druva debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="e7288-138">In other words, a link relationship between an Azure AD user and hello related user in Druva needs toobe established.</span></span>

<span data-ttu-id="e7288-139">En Druva, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7288-139">In Druva, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e7288-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Druva, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e7288-140">tooconfigure and test Azure AD single sign-on with Druva, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e7288-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="e7288-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e7288-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7288-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e7288-143">**[Crear un usuario de prueba de Druva](#create-a-druva-test-user)**  -toohave un equivalente de Britta Simon en Druva que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="e7288-143">**[Create a Druva test user](#create-a-druva-test-user)** - toohave a counterpart of Britta Simon in Druva that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e7288-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e7288-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e7288-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e7288-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e7288-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7288-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e7288-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Druva.</span><span class="sxs-lookup"><span data-stu-id="e7288-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Druva application.</span></span>

<span data-ttu-id="e7288-148">**inicio de sesión único en Azure AD tooconfigure con Druva, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e7288-148">**tooconfigure Azure AD single sign-on with Druva, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7288-149">En el portal de Azure, en Hola Hola **Druva** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e7288-149">In hello Azure portal, on hello **Druva** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="e7288-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e7288-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. <span data-ttu-id="e7288-153">En hello **Druva dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e7288-153">On hello **Druva Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    <span data-ttu-id="e7288-155">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL hello:`https://cloud.druva.com/home`</span><span class="sxs-lookup"><span data-stu-id="e7288-155">In hello **Sign-on URL** textbox, type hello URL: `https://cloud.druva.com/home`</span></span>

4. <span data-ttu-id="e7288-156">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e7288-156">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. <span data-ttu-id="e7288-158">La aplicación Druva espera las aserciones de SAML de hello en un formato específico, lo que requiere tooyour de asignaciones de atributo personalizado de tooadd **atributos de Token SAML** configuración.</span><span class="sxs-lookup"><span data-stu-id="e7288-158">Your Druva application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. <span data-ttu-id="e7288-160">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en hello delante de la imagen y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e7288-160">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>

    | <span data-ttu-id="e7288-161">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="e7288-161">Attribute Name</span></span>      | <span data-ttu-id="e7288-162">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="e7288-162">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="e7288-163">insync\_auth\_token</span><span class="sxs-lookup"><span data-stu-id="e7288-163">insync\_auth\_token</span></span> |<span data-ttu-id="e7288-164">Escriba Hola token generado valor</span><span class="sxs-lookup"><span data-stu-id="e7288-164">Enter hello token generated value</span></span> |
    
    <span data-ttu-id="e7288-165">a.</span><span class="sxs-lookup"><span data-stu-id="e7288-165">a.</span></span> <span data-ttu-id="e7288-166">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e7288-166">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="e7288-169">b.</span><span class="sxs-lookup"><span data-stu-id="e7288-169">b.</span></span> <span data-ttu-id="e7288-170">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="e7288-170">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="e7288-171">c.</span><span class="sxs-lookup"><span data-stu-id="e7288-171">c.</span></span> <span data-ttu-id="e7288-172">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="e7288-172">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="e7288-173">valor del token generado Hola se explica más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="e7288-173">hello token generated value is explained later in tutorial.</span></span>
    
    <span data-ttu-id="e7288-174">d.</span><span class="sxs-lookup"><span data-stu-id="e7288-174">d.</span></span> <span data-ttu-id="e7288-175">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e7288-175">Click **Ok**.</span></span>    

7. <span data-ttu-id="e7288-176">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e7288-176">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e7288-178">En hello **configuración de Druva** sección, haga clic en **configurar Druva** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="e7288-178">On hello **Druva Configuration** section, click **Configure Druva** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e7288-179">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="e7288-179">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. <span data-ttu-id="e7288-181">En una ventana del explorador web diferente, inicie sesión en el sitio de empresa de Druva tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="e7288-181">In a different web browser window, log in tooyour Druva company site as an administrator.</span></span>

10. <span data-ttu-id="e7288-182">Vaya demasiado**administrar \> configuración**.</span><span class="sxs-lookup"><span data-stu-id="e7288-182">Go too**Manage \> Settings**.</span></span>

    <span data-ttu-id="e7288-183">![Configuración](./media/active-directory-saas-druva-tutorial/ic795091.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="e7288-183">![Settings](./media/active-directory-saas-druva-tutorial/ic795091.png "Settings")</span></span>

11. <span data-ttu-id="e7288-184">En el cuadro de diálogo de configuración de inicio de sesión único de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e7288-184">On hello Single Sign-On Settings dialog, perform hello following steps:</span></span>

    <span data-ttu-id="e7288-185">![Configuración de inicio de sesión único](./media/active-directory-saas-druva-tutorial/ic795092.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="e7288-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="e7288-186">a.</span><span class="sxs-lookup"><span data-stu-id="e7288-186">a.</span></span> <span data-ttu-id="e7288-187">Pegar **SAML Single Sign-On dirección URL del servicio** valor, que haya copiado desde Hola portal de Azure en hello **dirección URL de inicio de sesión de Id. de proveedor** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="e7288-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **ID Provider Login URL** textbox.</span></span>
    
    <span data-ttu-id="e7288-188">b.</span><span class="sxs-lookup"><span data-stu-id="e7288-188">b.</span></span> <span data-ttu-id="e7288-189">Pegar **dirección URL de cierre de sesión** valor, que haya copiado desde Hola portal de Azure en hello **dirección URL de cierre de sesión de Id. de proveedor** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="e7288-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **ID Provider Logout URL** textbox.</span></span>
    
     <span data-ttu-id="e7288-190">c.</span><span class="sxs-lookup"><span data-stu-id="e7288-190">c.</span></span> <span data-ttu-id="e7288-191">Abra el certificado codificado en base 64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **Id. de proveedor certificado** cuadro de texto</span><span class="sxs-lookup"><span data-stu-id="e7288-191">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **ID Provider Certificate** textbox</span></span>
     
     <span data-ttu-id="e7288-192">d.</span><span class="sxs-lookup"><span data-stu-id="e7288-192">d.</span></span> <span data-ttu-id="e7288-193">Hola tooopen **configuración** página, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="e7288-193">tooopen hello **Settings** page, click **Save**.</span></span>

12. <span data-ttu-id="e7288-194">En hello **configuración** página, haga clic en **generar Token de SSO**.</span><span class="sxs-lookup"><span data-stu-id="e7288-194">On hello **Settings** page, click **Generate SSO Token**.</span></span>

    <span data-ttu-id="e7288-195">![Configuración](./media/active-directory-saas-druva-tutorial/ic795093.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="e7288-195">![Settings](./media/active-directory-saas-druva-tutorial/ic795093.png "Settings")</span></span>

13. <span data-ttu-id="e7288-196">En hello **único inicio de sesión autenticación de Token** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e7288-196">On hello **Single Sign-on Authentication Token** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="e7288-197">![Token de SSO](./media/active-directory-saas-druva-tutorial/ic795094.png "Token de SSO")</span><span class="sxs-lookup"><span data-stu-id="e7288-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span></span>
    
    <span data-ttu-id="e7288-198">a.</span><span class="sxs-lookup"><span data-stu-id="e7288-198">a.</span></span> <span data-ttu-id="e7288-199">Haga clic en **copia**, pegar copia valor en hello **valor** cuadro de texto en hello **Agregar atributo** sección.</span><span class="sxs-lookup"><span data-stu-id="e7288-199">Click **Copy**, Paste copied value in hello **Value** textbox in hello **Add Attribute** section.</span></span>
    
    <span data-ttu-id="e7288-200">b.</span><span class="sxs-lookup"><span data-stu-id="e7288-200">b.</span></span> <span data-ttu-id="e7288-201">Haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="e7288-201">Click **Close**.</span></span>

> [!TIP]
> <span data-ttu-id="e7288-202">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="e7288-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e7288-203">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="e7288-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e7288-204">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e7288-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e7288-205">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7288-205">Create an Azure AD test user</span></span>

<span data-ttu-id="e7288-206">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="e7288-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="e7288-208">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e7288-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7288-209">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="e7288-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e7288-211">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e7288-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e7288-213">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e7288-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e7288-215">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e7288-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e7288-217">a.</span><span class="sxs-lookup"><span data-stu-id="e7288-217">a.</span></span> <span data-ttu-id="e7288-218">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7288-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e7288-219">b.</span><span class="sxs-lookup"><span data-stu-id="e7288-219">b.</span></span> <span data-ttu-id="e7288-220">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7288-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="e7288-221">c.</span><span class="sxs-lookup"><span data-stu-id="e7288-221">c.</span></span> <span data-ttu-id="e7288-222">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="e7288-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="e7288-223">d.</span><span class="sxs-lookup"><span data-stu-id="e7288-223">d.</span></span> <span data-ttu-id="e7288-224">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e7288-224">Click **Create**.</span></span>
 
### <a name="create-a-druva-test-user"></a><span data-ttu-id="e7288-225">Crear un usuario de prueba de Druva</span><span class="sxs-lookup"><span data-stu-id="e7288-225">Create a Druva test user</span></span>

<span data-ttu-id="e7288-226">En orden tooenable toolog de los usuarios de Azure AD en tooDruva, se les deben aprovisionar en Druva.</span><span class="sxs-lookup"><span data-stu-id="e7288-226">In order tooenable Azure AD users toolog in tooDruva, they must be provisioned into Druva.</span></span> <span data-ttu-id="e7288-227">En caso de hello de Druva, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="e7288-227">In hello case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="e7288-228">**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e7288-228">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7288-229">Inicie sesión en tooyour **Druva** como administrador.</span><span class="sxs-lookup"><span data-stu-id="e7288-229">Log in tooyour **Druva** company site as administrator.</span></span>

2. <span data-ttu-id="e7288-230">Vaya demasiado**administrar \> usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e7288-230">Go too**Manage \> Users**.</span></span>
   
   <span data-ttu-id="e7288-231">![Administración de usuarios](./media/active-directory-saas-druva-tutorial/ic795097.png "Administración de usuarios")</span><span class="sxs-lookup"><span data-stu-id="e7288-231">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795097.png "Manage Users")</span></span>

3. <span data-ttu-id="e7288-232">Haga clic en **Create New**.</span><span class="sxs-lookup"><span data-stu-id="e7288-232">Click **Create New**.</span></span>
   
   <span data-ttu-id="e7288-233">![Administración de usuarios](./media/active-directory-saas-druva-tutorial/ic795098.png "Administración de usuarios")</span><span class="sxs-lookup"><span data-stu-id="e7288-233">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795098.png "Manage Users")</span></span>

4. <span data-ttu-id="e7288-234">En cuadro de diálogo Crear nuevo usuario de hello realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e7288-234">On hello Create New User dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="e7288-235">![Creación de un nuevo usuario](./media/active-directory-saas-druva-tutorial/ic795099.png "Creación de un nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="e7288-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span></span>
   
   <span data-ttu-id="e7288-236">a.</span><span class="sxs-lookup"><span data-stu-id="e7288-236">a.</span></span> <span data-ttu-id="e7288-237">Hola **dirección de correo electrónico** cuadro de texto, escriba el correo electrónico de saludo del usuario como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="e7288-237">In hello **Email address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="e7288-238">b.</span><span class="sxs-lookup"><span data-stu-id="e7288-238">b.</span></span> <span data-ttu-id="e7288-239">Hola **nombre** cuadro de texto, escriba Hola nombre de usuario como **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7288-239">In hello **Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="e7288-240">c.</span><span class="sxs-lookup"><span data-stu-id="e7288-240">c.</span></span> <span data-ttu-id="e7288-241">Haga clic en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="e7288-241">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="e7288-242">Puede usar cualquier otra Druva usuario cuenta herramienta de creación o las API proporcionadas por Druva tooprovision cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7288-242">You can use any other Druva user account creation tools or APIs provided by Druva tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e7288-243">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7288-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e7288-244">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooDruva.</span><span class="sxs-lookup"><span data-stu-id="e7288-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDruva.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="e7288-246">**tooassign Britta Simon tooDruva, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e7288-246">**tooassign Britta Simon tooDruva, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7288-247">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e7288-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e7288-249">En la lista de aplicaciones de hello, seleccione **Druva**.</span><span class="sxs-lookup"><span data-stu-id="e7288-249">In hello applications list, select **Druva**.</span></span>

    ![vínculo de Druva Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. <span data-ttu-id="e7288-251">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e7288-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="e7288-253">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e7288-253">Click **Add** button.</span></span> <span data-ttu-id="e7288-254">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e7288-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="e7288-256">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7288-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e7288-257">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e7288-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e7288-258">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e7288-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e7288-259">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="e7288-259">Test single sign-on</span></span>

<span data-ttu-id="e7288-260">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e7288-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e7288-261">Al hacer clic en icono de Druva Hola Hola Panel de acceso, deberá obtener la aplicación de Druva tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="e7288-261">When you click hello Druva tile in hello Access Panel, you should get automatically signed-on tooyour Druva application.</span></span>
<span data-ttu-id="e7288-262">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e7288-262">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e7288-263">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e7288-263">Additional resources</span></span>

* [<span data-ttu-id="e7288-264">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7288-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e7288-265">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e7288-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

