---
title: "Tutorial: integración de Azure Active Directory con Clever | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Clever."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 24430e1e6c750efa5787561aa151201b1fe7d428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="4c077-103">Tutorial: integración de Azure Active Directory con Clever</span><span class="sxs-lookup"><span data-stu-id="4c077-103">Tutorial: Azure Active Directory integration with Clever</span></span>

<span data-ttu-id="4c077-104">En este tutorial, aprenderá cómo toointegrate Clever con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4c077-104">In this tutorial, you learn how toointegrate Clever with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4c077-105">Integración Clever con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="4c077-105">Integrating Clever with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4c077-106">Puede controlar en Azure AD que tenga acceso tooClever.</span><span class="sxs-lookup"><span data-stu-id="4c077-106">You can control in Azure AD who has access tooClever.</span></span>
- <span data-ttu-id="4c077-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooClever (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c077-107">You can enable your users tooautomatically get signed-on tooClever (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4c077-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4c077-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="4c077-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4c077-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c077-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4c077-110">Prerequisites</span></span>

<span data-ttu-id="4c077-111">integración de Azure AD con Clever tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="4c077-111">tooconfigure Azure AD integration with Clever, you need hello following items:</span></span>

- <span data-ttu-id="4c077-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c077-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4c077-113">Una suscripción habilitada para el inicio de sesión único en Clever</span><span class="sxs-lookup"><span data-stu-id="4c077-113">A Clever single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4c077-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="4c077-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4c077-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="4c077-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4c077-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4c077-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4c077-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c077-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4c077-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="4c077-118">Scenario description</span></span>
<span data-ttu-id="4c077-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="4c077-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4c077-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="4c077-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4c077-121">Agregar Clever desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="4c077-121">Adding Clever from hello gallery</span></span>
2. <span data-ttu-id="4c077-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c077-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clever-from-hello-gallery"></a><span data-ttu-id="4c077-123">Agregar Clever desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="4c077-123">Adding Clever from hello gallery</span></span>
<span data-ttu-id="4c077-124">integración de hello tooconfigure de Clever en Azure AD, deberá tooadd Clever de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="4c077-124">tooconfigure hello integration of Clever into Azure AD, you need tooadd Clever from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4c077-125">**tooadd Clever de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4c077-125">**tooadd Clever from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c077-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="4c077-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="4c077-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="4c077-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4c077-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4c077-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="4c077-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c077-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="4c077-133">En el cuadro de búsqueda de hello, escriba **Clever**, seleccione **Clever** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4c077-133">In hello search box, type **Clever**, select **Clever** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Inteligente en la lista de resultados de Hola](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4c077-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c077-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4c077-136">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Clever con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4c077-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4c077-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Clever es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c077-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clever is tooa user in Azure AD.</span></span> <span data-ttu-id="4c077-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Clever debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="4c077-138">In other words, a link relationship between an Azure AD user and hello related user in Clever needs toobe established.</span></span>

<span data-ttu-id="4c077-139">En Clever, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c077-139">In Clever, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4c077-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Clever, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="4c077-140">tooconfigure and test Azure AD single sign-on with Clever, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4c077-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="4c077-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4c077-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c077-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4c077-143">**[Crear un usuario de prueba inteligente](#create-a-clever-test-user)**  -toohave un equivalente de Britta Simon en Clever que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="4c077-143">**[Create a Clever test user](#create-a-clever-test-user)** - toohave a counterpart of Britta Simon in Clever that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4c077-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4c077-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4c077-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="4c077-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4c077-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c077-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4c077-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación inteligente.</span><span class="sxs-lookup"><span data-stu-id="4c077-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clever application.</span></span>

<span data-ttu-id="4c077-148">**inicio de sesión único en Azure AD tooconfigure con Clever, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4c077-148">**tooconfigure Azure AD single sign-on with Clever, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c077-149">En el portal de Azure, en Hola Hola **Clever** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="4c077-149">In hello Azure portal, on hello **Clever** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="4c077-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4c077-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. <span data-ttu-id="4c077-153">En hello **tanto de esos dominios y direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4c077-153">On hello **Clever Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Clever](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    <span data-ttu-id="4c077-155">a.</span><span class="sxs-lookup"><span data-stu-id="4c077-155">a.</span></span> <span data-ttu-id="4c077-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://clever.com/in/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="4c077-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://clever.com/in/<companyname>`</span></span>

    <span data-ttu-id="4c077-157">b.</span><span class="sxs-lookup"><span data-stu-id="4c077-157">b.</span></span> <span data-ttu-id="4c077-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://clever.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="4c077-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://clever.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4c077-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="4c077-159">These values are not real.</span></span> <span data-ttu-id="4c077-160">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="4c077-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4c077-161">Póngase en contacto con [equipo de soporte técnico de cliente inteligente](https://clever.com/about/contact/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="4c077-161">Contact [Clever Client support team](https://clever.com/about/contact/) tooget these values.</span></span>

4. <span data-ttu-id="4c077-162">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4c077-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. <span data-ttu-id="4c077-164">Hola aplicación inteligente espera las aserciones de SAML de hello en un formato específico, lo que requiere tooyour de asignaciones de atributo personalizado de tooadd **atributos de Token SAML** configuración.</span><span class="sxs-lookup"><span data-stu-id="4c077-164">hello Clever application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span>

    <span data-ttu-id="4c077-165">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="4c077-165">hello following screenshot shows an example for this.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. <span data-ttu-id="4c077-167">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de hello anterior y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4c077-167">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="4c077-168">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="4c077-168">Attribute Name</span></span>  | <span data-ttu-id="4c077-169">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="4c077-169">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="4c077-170">clever.student.credentials.district\_username</span><span class="sxs-lookup"><span data-stu-id="4c077-170">clever.student.credentials.district\_username</span></span>  | <span data-ttu-id="4c077-171">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="4c077-171">user.userprincipalname</span></span> |
    | <span data-ttu-id="4c077-172">Firstname</span><span class="sxs-lookup"><span data-stu-id="4c077-172">Firstname</span></span>  | <span data-ttu-id="4c077-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="4c077-173">user.givenname</span></span> |
    | <span data-ttu-id="4c077-174">Lastname</span><span class="sxs-lookup"><span data-stu-id="4c077-174">Lastname</span></span>  | <span data-ttu-id="4c077-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="4c077-175">user.surname</span></span> |    

    <span data-ttu-id="4c077-176">a.</span><span class="sxs-lookup"><span data-stu-id="4c077-176">a.</span></span> <span data-ttu-id="4c077-177">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c077-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="4c077-180">b.</span><span class="sxs-lookup"><span data-stu-id="4c077-180">b.</span></span> <span data-ttu-id="4c077-181">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="4c077-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="4c077-182">c.</span><span class="sxs-lookup"><span data-stu-id="4c077-182">c.</span></span> <span data-ttu-id="4c077-183">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="4c077-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="4c077-184">d.</span><span class="sxs-lookup"><span data-stu-id="4c077-184">d.</span></span> <span data-ttu-id="4c077-185">Deje hello **Namespace** cuadro de texto en blanco.</span><span class="sxs-lookup"><span data-stu-id="4c077-185">Leave hello **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="4c077-186">d.</span><span class="sxs-lookup"><span data-stu-id="4c077-186">d.</span></span> <span data-ttu-id="4c077-187">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4c077-187">Click **Ok**.</span></span>     

5. <span data-ttu-id="4c077-188">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="4c077-188">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="4c077-190">Hola toogenerate **metadatos** dirección url, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4c077-190">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="4c077-191">a.</span><span class="sxs-lookup"><span data-stu-id="4c077-191">a.</span></span> <span data-ttu-id="4c077-192">Haga clic en **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4c077-192">Click **App registrations**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    <span data-ttu-id="4c077-194">b.</span><span class="sxs-lookup"><span data-stu-id="4c077-194">b.</span></span> <span data-ttu-id="4c077-195">Haga clic en **extremos** tooopen **extremos** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c077-195">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    <span data-ttu-id="4c077-197">c.</span><span class="sxs-lookup"><span data-stu-id="4c077-197">c.</span></span> <span data-ttu-id="4c077-198">Haga clic en hello copia botón toocopy **documento de metadatos de federación** dirección url y péguela en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="4c077-198">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    <span data-ttu-id="4c077-200">d.</span><span class="sxs-lookup"><span data-stu-id="4c077-200">d.</span></span> <span data-ttu-id="4c077-201">Ahora vaya toohello página de propiedades de **Clever** copia hello y **Id. de aplicación** con **copia** botón y péguelo en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="4c077-201">Now go toohello property page of **Clever** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    <span data-ttu-id="4c077-203">e.</span><span class="sxs-lookup"><span data-stu-id="4c077-203">e.</span></span> <span data-ttu-id="4c077-204">Generar hello **dirección URL de metadatos** con hello sigue el patrón:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="4c077-204">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>   

9. <span data-ttu-id="4c077-205">En una ventana del explorador web diferente, inicie sesión en el sitio de su compañía tanto de esos tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="4c077-205">In a different web browser window, log in tooyour Clever company site as an administrator.</span></span>

10. <span data-ttu-id="4c077-206">En la barra de herramientas de hello, haga clic en **inicio de sesión instantáneo**.</span><span class="sxs-lookup"><span data-stu-id="4c077-206">In hello toolbar, click **Instant Login**.</span></span>

    <span data-ttu-id="4c077-207">![Inicio de sesión instantáneo](./media/active-directory-saas-clever-tutorial/ic798984.png "Inicio de sesión instantáneo")</span><span class="sxs-lookup"><span data-stu-id="4c077-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span></span>

11. <span data-ttu-id="4c077-208">En hello **inicio de sesión instantáneo** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="4c077-208">On hello **Instant Login** page, perform hello following steps:</span></span>
      
      <span data-ttu-id="4c077-209">![Inicio de sesión instantáneo](./media/active-directory-saas-clever-tutorial/ic798985.png "Inicio de sesión instantáneo")</span><span class="sxs-lookup"><span data-stu-id="4c077-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span></span>
      
      <span data-ttu-id="4c077-210">a.</span><span class="sxs-lookup"><span data-stu-id="4c077-210">a.</span></span> <span data-ttu-id="4c077-211">Hola de tipo **dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="4c077-211">Type hello **Login URL**.</span></span>
      
      >[!NOTE]
      ><span data-ttu-id="4c077-212">Hola **dirección URL de inicio de sesión** es un valor personalizado.</span><span class="sxs-lookup"><span data-stu-id="4c077-212">hello **Login URL** is a custom value.</span></span> <span data-ttu-id="4c077-213">Póngase en contacto con [equipo de soporte técnico de cliente inteligente](https://clever.com/about/contact/) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="4c077-213">Contact [Clever Client support team](https://clever.com/about/contact/) tooget this value.</span></span>
      
      <span data-ttu-id="4c077-214">b.</span><span class="sxs-lookup"><span data-stu-id="4c077-214">b.</span></span> <span data-ttu-id="4c077-215">En **Identity System** (Sistema de identidades), seleccione **ADFS**.</span><span class="sxs-lookup"><span data-stu-id="4c077-215">As **Identity System**, select **ADFS**.</span></span>

      <span data-ttu-id="4c077-216">c.</span><span class="sxs-lookup"><span data-stu-id="4c077-216">c.</span></span> <span data-ttu-id="4c077-217">Hola de tipo **dirección URL de metadatos** en hello **dirección URL de metadatos** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="4c077-217">Type hello **Metadata URL** in hello **Metadata URL** textbox.</span></span>
      
      <span data-ttu-id="4c077-218">d.</span><span class="sxs-lookup"><span data-stu-id="4c077-218">d.</span></span> <span data-ttu-id="4c077-219">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4c077-219">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4c077-220">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="4c077-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4c077-221">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="4c077-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4c077-222">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4c077-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4c077-223">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c077-223">Create an Azure AD test user</span></span>

<span data-ttu-id="4c077-224">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="4c077-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="4c077-226">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4c077-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c077-227">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="4c077-227">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4c077-229">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4c077-229">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4c077-231">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c077-231">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4c077-233">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4c077-233">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4c077-235">a.</span><span class="sxs-lookup"><span data-stu-id="4c077-235">a.</span></span> <span data-ttu-id="4c077-236">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4c077-236">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4c077-237">b.</span><span class="sxs-lookup"><span data-stu-id="4c077-237">b.</span></span> <span data-ttu-id="4c077-238">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c077-238">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="4c077-239">c.</span><span class="sxs-lookup"><span data-stu-id="4c077-239">c.</span></span> <span data-ttu-id="4c077-240">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="4c077-240">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="4c077-241">d.</span><span class="sxs-lookup"><span data-stu-id="4c077-241">d.</span></span> <span data-ttu-id="4c077-242">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4c077-242">Click **Create**.</span></span>
 
### <a name="create-a-clever-test-user"></a><span data-ttu-id="4c077-243">Creación de un usuario de prueba de Clever</span><span class="sxs-lookup"><span data-stu-id="4c077-243">Create a Clever test user</span></span>

<span data-ttu-id="4c077-244">toolog de los usuarios de Azure AD tooenable en tooClever, se les deben aprovisionar en Clever.</span><span class="sxs-lookup"><span data-stu-id="4c077-244">tooenable Azure AD users toolog in tooClever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="4c077-245">En el caso de Clever, trabajar con [equipo de soporte técnico de cliente inteligente](https://clever.com/about/contact/) para agregar usuarios de Hola de plataforma inteligente Hola.</span><span class="sxs-lookup"><span data-stu-id="4c077-245">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add hello users in hello Clever platform.</span></span> <span data-ttu-id="4c077-246">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4c077-246">Users must be created and activated before you use single sign-on.</span></span> 

>[!NOTE]
><span data-ttu-id="4c077-247">Puede usar cualquier otra herramienta de creación de cuentas de usuario tanto de esos o las API proporcionadas por tooprovision inteligente cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c077-247">You can use any other Clever user account creation tools or APIs provided by Clever tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4c077-248">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c077-248">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4c077-249">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooClever.</span><span class="sxs-lookup"><span data-stu-id="4c077-249">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooClever.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="4c077-251">**tooassign Britta Simon tooClever, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4c077-251">**tooassign Britta Simon tooClever, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c077-252">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4c077-252">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="4c077-254">En la lista de aplicaciones de hello, seleccione **Clever**.</span><span class="sxs-lookup"><span data-stu-id="4c077-254">In hello applications list, select **Clever**.</span></span>

    ![Hola Clever vínculo en la lista de aplicaciones de Hola](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. <span data-ttu-id="4c077-256">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4c077-256">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="4c077-258">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4c077-258">Click **Add** button.</span></span> <span data-ttu-id="4c077-259">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4c077-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="4c077-261">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c077-261">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4c077-262">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4c077-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4c077-263">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4c077-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4c077-264">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="4c077-264">Test single sign-on</span></span>

<span data-ttu-id="4c077-265">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4c077-265">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4c077-266">Al hacer clic en icono inteligente hello en Hola Panel de acceso, deberá obtener aplicaciones tanto de esos tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="4c077-266">When you click hello Clever tile in hello Access Panel, you should get automatically signed-on tooyour Clever application.</span></span>
<span data-ttu-id="4c077-267">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4c077-267">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4c077-268">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4c077-268">Additional resources</span></span>

* [<span data-ttu-id="4c077-269">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c077-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4c077-270">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4c077-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

