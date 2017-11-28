---
title: "Tutorial: integración de Azure Active Directory con Litmos | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Litmos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 026fd10058760f2d63d185ef4aa9d7de3b82525e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a><span data-ttu-id="91870-103">Tutorial: Integración de Azure Active Directory con Litmos</span><span class="sxs-lookup"><span data-stu-id="91870-103">Tutorial: Azure Active Directory integration with Litmos</span></span>

<span data-ttu-id="91870-104">En este tutorial, aprenderá cómo toointegrate Litmos con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="91870-104">In this tutorial, you learn how toointegrate Litmos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="91870-105">Integración Litmos con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="91870-105">Integrating Litmos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="91870-106">Puede controlar en Azure AD que tenga acceso tooLitmos.</span><span class="sxs-lookup"><span data-stu-id="91870-106">You can control in Azure AD who has access tooLitmos.</span></span>
- <span data-ttu-id="91870-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLitmos (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91870-107">You can enable your users tooautomatically get signed-on tooLitmos (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="91870-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="91870-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="91870-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="91870-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91870-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="91870-110">Prerequisites</span></span>

<span data-ttu-id="91870-111">integración de Azure AD con Litmos tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="91870-111">tooconfigure Azure AD integration with Litmos, you need hello following items:</span></span>

- <span data-ttu-id="91870-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="91870-112">An Azure AD subscription</span></span>
- <span data-ttu-id="91870-113">Una suscripción habilitada para el inicio de sesión único en Litmos</span><span class="sxs-lookup"><span data-stu-id="91870-113">A Litmos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="91870-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="91870-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="91870-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="91870-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="91870-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="91870-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="91870-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="91870-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="91870-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="91870-118">Scenario description</span></span>
<span data-ttu-id="91870-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="91870-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="91870-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="91870-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="91870-121">Agregar Litmos desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="91870-121">Adding Litmos from hello gallery</span></span>
2. <span data-ttu-id="91870-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="91870-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-litmos-from-hello-gallery"></a><span data-ttu-id="91870-123">Agregar Litmos desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="91870-123">Adding Litmos from hello gallery</span></span>
<span data-ttu-id="91870-124">integración de hello tooconfigure de Litmos en Azure AD, deberá tooadd Litmos de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="91870-124">tooconfigure hello integration of Litmos into Azure AD, you need tooadd Litmos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="91870-125">**tooadd Litmos de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="91870-125">**tooadd Litmos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="91870-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="91870-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="91870-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="91870-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="91870-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="91870-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="91870-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="91870-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="91870-133">En el cuadro de búsqueda de hello, escriba **Litmos**, seleccione **Litmos** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="91870-133">In hello search box, type **Litmos**, select **Litmos** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Litmos en la lista de resultados de Hola](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="91870-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="91870-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="91870-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Litmos con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="91870-136">In this section, you configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="91870-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Litmos es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91870-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Litmos is tooa user in Azure AD.</span></span> <span data-ttu-id="91870-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Litmos debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="91870-138">In other words, a link relationship between an Azure AD user and hello related user in Litmos needs toobe established.</span></span>

<span data-ttu-id="91870-139">En Litmos, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="91870-139">In Litmos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="91870-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Litmos, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="91870-140">tooconfigure and test Azure AD single sign-on with Litmos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="91870-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="91870-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="91870-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91870-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="91870-143">**[Crear un usuario de prueba Litmos](#create-a-litmos-test-user)**  -toohave un equivalente de Britta Simon en Litmos que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="91870-143">**[Create a Litmos test user](#create-a-litmos-test-user)** - toohave a counterpart of Britta Simon in Litmos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="91870-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="91870-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="91870-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="91870-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="91870-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="91870-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="91870-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Litmos.</span><span class="sxs-lookup"><span data-stu-id="91870-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Litmos application.</span></span>

<span data-ttu-id="91870-148">**inicio de sesión único en Azure AD tooconfigure con Litmos, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="91870-148">**tooconfigure Azure AD single sign-on with Litmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="91870-149">En el portal de Azure, en Hola Hola **Litmos** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="91870-149">In hello Azure portal, on hello **Litmos** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="91870-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="91870-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. <span data-ttu-id="91870-153">En hello **Litmos dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="91870-153">On hello **Litmos Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Litmos](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    <span data-ttu-id="91870-155">a.</span><span class="sxs-lookup"><span data-stu-id="91870-155">a.</span></span> <span data-ttu-id="91870-156">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.litmos.com/account/Login`</span><span class="sxs-lookup"><span data-stu-id="91870-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.litmos.com/account/Login`</span></span>

    <span data-ttu-id="91870-157">b.</span><span class="sxs-lookup"><span data-stu-id="91870-157">b.</span></span> <span data-ttu-id="91870-158">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.litmos.com/integration/samllogin`</span><span class="sxs-lookup"><span data-stu-id="91870-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.litmos.com/integration/samllogin`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="91870-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="91870-159">These values are not real.</span></span> <span data-ttu-id="91870-160">Actualizar estos valores con URL real de identificador y la respuesta de hello, que se explican más adelante en el tutorial o póngase en contacto con [equipo de soporte técnico Litmos](https://www.litmos.com/contact-us/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="91870-160">Update these values with hello actual Identifier and Reply URL, which are explained later in tutorial or contact [Litmos support team](https://www.litmos.com/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="91870-161">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="91870-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. <span data-ttu-id="91870-163">Como parte de la configuración de hello, necesita hello toocustomize **atributos de Token SAML** para la aplicación Litmos.</span><span class="sxs-lookup"><span data-stu-id="91870-163">As part of hello configuration, you need toocustomize hello **SAML Token Attributes** for your Litmos application.</span></span>

    ![Sección atributos](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | <span data-ttu-id="91870-165">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="91870-165">Attribute Name</span></span>   | <span data-ttu-id="91870-166">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="91870-166">Attribute Value</span></span> |   
    | ---------------  | ----------------|
    | <span data-ttu-id="91870-167">Nombre</span><span class="sxs-lookup"><span data-stu-id="91870-167">FirstName</span></span> |<span data-ttu-id="91870-168">user.givenname</span><span class="sxs-lookup"><span data-stu-id="91870-168">user.givenname</span></span> |
    | <span data-ttu-id="91870-169">Apellidos</span><span class="sxs-lookup"><span data-stu-id="91870-169">LastName</span></span>  |<span data-ttu-id="91870-170">user.surname</span><span class="sxs-lookup"><span data-stu-id="91870-170">user.surname</span></span> |
    | <span data-ttu-id="91870-171">Email</span><span class="sxs-lookup"><span data-stu-id="91870-171">Email</span></span> |<span data-ttu-id="91870-172">user.mail</span><span class="sxs-lookup"><span data-stu-id="91870-172">user.mail</span></span> |

    <span data-ttu-id="91870-173">a.</span><span class="sxs-lookup"><span data-stu-id="91870-173">a.</span></span> <span data-ttu-id="91870-174">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="91870-174">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Agregar atributo](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![Cuadro de diálogo Agregar atributo](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="91870-177">b.</span><span class="sxs-lookup"><span data-stu-id="91870-177">b.</span></span> <span data-ttu-id="91870-178">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="91870-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="91870-179">c.</span><span class="sxs-lookup"><span data-stu-id="91870-179">c.</span></span> <span data-ttu-id="91870-180">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="91870-180">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="91870-181">d.</span><span class="sxs-lookup"><span data-stu-id="91870-181">d.</span></span> <span data-ttu-id="91870-182">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="91870-182">Click **Ok**.</span></span>     

6. <span data-ttu-id="91870-183">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="91870-183">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="91870-185">En otra ventana del explorador, inicio de sesión tooyour Litmos el sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="91870-185">In a different browser window, sign-on tooyour Litmos company site as administrator.</span></span>

8. <span data-ttu-id="91870-186">En la barra de navegación de hello en el lado izquierdo de hello, haga clic en **cuentas**.</span><span class="sxs-lookup"><span data-stu-id="91870-186">In hello navigation bar on hello left side, click **Accounts**.</span></span>
   
    ![Sección Cuentas en la aplicación][22] 

9. <span data-ttu-id="91870-188">Haga clic en hello **integraciones** ficha.</span><span class="sxs-lookup"><span data-stu-id="91870-188">Click hello **Integrations** tab.</span></span>
   
    ![Pestaña Integración][23] 

10. <span data-ttu-id="91870-190">En hello **integraciones** ficha, desplácese hacia abajo demasiado**3rd integraciones de entidad**y, a continuación, haga clic en **SAML 2.0** ficha.</span><span class="sxs-lookup"><span data-stu-id="91870-190">On hello **Integrations** tab, scroll down too**3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![Sección SAML 2.0][24] 

11. <span data-ttu-id="91870-192">Copiar valor de hello en **Hola extremo de SAML para litmos es:** y péguelo en hello **dirección URL de respuesta** cuadro de texto en hello **Litmos dominio y las direcciones URL** sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="91870-192">Copy hello value under **hello SAML endpoint for litmos is:** and paste it into hello **Reply URL** textbox in hello **Litmos Domain and URLs** section in Azure portal.</span></span> 
   
    ![Punto de conexión de SAML][26] 

12. <span data-ttu-id="91870-194">En su **Litmos** aplicación, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="91870-194">In your **Litmos** application, perform hello following steps:</span></span>
    
     ![Aplicación Litmos][25] 
     
     <span data-ttu-id="91870-196">a.</span><span class="sxs-lookup"><span data-stu-id="91870-196">a.</span></span> <span data-ttu-id="91870-197">Haga clic en **Enable SAML**(Habilitar SAML).</span><span class="sxs-lookup"><span data-stu-id="91870-197">Click **Enable SAML**.</span></span>
    
     <span data-ttu-id="91870-198">b.</span><span class="sxs-lookup"><span data-stu-id="91870-198">b.</span></span> <span data-ttu-id="91870-199">Abra el certificado codificado en base 64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado X.509 de SAML** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="91870-199">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **SAML X.509 Certificate** textbox.</span></span>
     
     <span data-ttu-id="91870-200">c.</span><span class="sxs-lookup"><span data-stu-id="91870-200">c.</span></span> <span data-ttu-id="91870-201">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="91870-201">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="91870-202">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="91870-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="91870-203">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="91870-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="91870-204">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="91870-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="91870-205">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="91870-205">Create an Azure AD test user</span></span>

<span data-ttu-id="91870-206">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="91870-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="91870-208">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="91870-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="91870-209">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="91870-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="91870-211">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="91870-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="91870-213">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="91870-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="91870-215">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="91870-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    <span data-ttu-id="91870-217">a.</span><span class="sxs-lookup"><span data-stu-id="91870-217">a.</span></span> <span data-ttu-id="91870-218">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="91870-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="91870-219">b.</span><span class="sxs-lookup"><span data-stu-id="91870-219">b.</span></span> <span data-ttu-id="91870-220">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91870-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="91870-221">c.</span><span class="sxs-lookup"><span data-stu-id="91870-221">c.</span></span> <span data-ttu-id="91870-222">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="91870-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="91870-223">d.</span><span class="sxs-lookup"><span data-stu-id="91870-223">d.</span></span> <span data-ttu-id="91870-224">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="91870-224">Click **Create**.</span></span>
  
### <a name="create-a-litmos-test-user"></a><span data-ttu-id="91870-225">Creación de un usuario de prueba en Litmos</span><span class="sxs-lookup"><span data-stu-id="91870-225">Create a Litmos test user</span></span>

<span data-ttu-id="91870-226">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Litmos toocreate.</span><span class="sxs-lookup"><span data-stu-id="91870-226">hello objective of this section is toocreate a user called Britta Simon in Litmos.</span></span>  
<span data-ttu-id="91870-227">Hola Litmos aplicación admite Just-in-Time de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="91870-227">hello Litmos application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="91870-228">Esto significa que, una cuenta de usuario se crea automáticamente si es necesario durante una aplicación de Hola de tooaccess intento con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="91870-228">This means, a user account is automatically created if necessary during an attempt tooaccess hello application using hello Access Panel.</span></span>

<span data-ttu-id="91870-229">**toocreate un usuario llamado Britta Simon en Litmos, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="91870-229">**toocreate a user called Britta Simon in Litmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="91870-230">En otra ventana del explorador, inicio de sesión tooyour Litmos el sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="91870-230">In a different browser window, sign-on tooyour Litmos company site as administrator.</span></span>

2. <span data-ttu-id="91870-231">En la barra de navegación de hello en el lado izquierdo de hello, haga clic en **cuentas**.</span><span class="sxs-lookup"><span data-stu-id="91870-231">In hello navigation bar on hello left side, click **Accounts**.</span></span>
   
    ![Sección Cuentas en la aplicación][22] 

3. <span data-ttu-id="91870-233">Haga clic en hello **integraciones** ficha.</span><span class="sxs-lookup"><span data-stu-id="91870-233">Click hello **Integrations** tab.</span></span>
   
    ![Pestaña Integraciones][23] 

4. <span data-ttu-id="91870-235">En hello **integraciones** ficha, desplácese hacia abajo demasiado**3rd integraciones de entidad**y, a continuación, haga clic en **SAML 2.0** ficha.</span><span class="sxs-lookup"><span data-stu-id="91870-235">On hello **Integrations** tab, scroll down too**3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0][24] 
    
5. <span data-ttu-id="91870-237">Seleccione **Autogenerate Users**(Generar usuarios automáticamente)</span><span class="sxs-lookup"><span data-stu-id="91870-237">Select **Autogenerate Users**</span></span>
   
    ![Generar usuarios automáticamente][27] 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="91870-239">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="91870-239">Assign hello Azure AD test user</span></span>

<span data-ttu-id="91870-240">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooLitmos.</span><span class="sxs-lookup"><span data-stu-id="91870-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLitmos.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="91870-242">**tooassign Britta Simon tooLitmos, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="91870-242">**tooassign Britta Simon tooLitmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="91870-243">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="91870-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="91870-245">En la lista de aplicaciones de hello, seleccione **Litmos**.</span><span class="sxs-lookup"><span data-stu-id="91870-245">In hello applications list, select **Litmos**.</span></span>

    ![vínculo de Litmos Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. <span data-ttu-id="91870-247">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="91870-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="91870-249">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="91870-249">Click **Add** button.</span></span> <span data-ttu-id="91870-250">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="91870-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="91870-252">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="91870-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="91870-253">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="91870-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="91870-254">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="91870-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="91870-255">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="91870-255">Test single sign-on</span></span>

<span data-ttu-id="91870-256">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="91870-256">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="91870-257">Al hacer clic en hello Litmos el icono Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour Litmos aplicación.</span><span class="sxs-lookup"><span data-stu-id="91870-257">When you click hello Litmos tile in hello Access Panel, you should get automatically signed-on tooyour Litmos application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="91870-258">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="91870-258">Additional resources</span></span>

* [<span data-ttu-id="91870-259">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="91870-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="91870-260">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="91870-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

