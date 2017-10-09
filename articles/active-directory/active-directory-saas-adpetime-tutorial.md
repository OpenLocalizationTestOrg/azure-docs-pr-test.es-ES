---
title: "Tutorial: integración de Azure Active Directory con ADP eTime | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y eTime ADP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a5c7d14a18220f8c7a5b14055c30662ecd8f14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="387e5-103">Tutorial: Integración de Azure Active Directory con ADP eTime</span><span class="sxs-lookup"><span data-stu-id="387e5-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="387e5-104">En este tutorial, aprenderá cómo eTime toointegrate ADP con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="387e5-104">In this tutorial, you learn how toointegrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="387e5-105">Integración ADP eTime con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="387e5-105">Integrating ADP eTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="387e5-106">Puede controlar en Azure AD que tenga acceso tooADP eTime</span><span class="sxs-lookup"><span data-stu-id="387e5-106">You can control in Azure AD who has access tooADP eTime</span></span>
- <span data-ttu-id="387e5-107">Puede habilitar los usuarios tooautomatically get tooADP ha iniciado sesión eTime (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="387e5-107">You can enable your users tooautomatically get signed-on tooADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="387e5-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="387e5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="387e5-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="387e5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="387e5-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="387e5-110">Prerequisites</span></span>

<span data-ttu-id="387e5-111">integración de Azure AD con ADP eTime tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="387e5-111">tooconfigure Azure AD integration with ADP eTime, you need hello following items:</span></span>

- <span data-ttu-id="387e5-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="387e5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="387e5-113">Una suscripción habilitada para el inicio de sesión único en ADP eTime</span><span class="sxs-lookup"><span data-stu-id="387e5-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="387e5-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="387e5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="387e5-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="387e5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="387e5-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="387e5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="387e5-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="387e5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="387e5-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="387e5-118">Scenario description</span></span>
<span data-ttu-id="387e5-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="387e5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="387e5-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="387e5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="387e5-121">Agregar ADP eTime desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="387e5-121">Adding ADP eTime from hello gallery</span></span>
2. <span data-ttu-id="387e5-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="387e5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-hello-gallery"></a><span data-ttu-id="387e5-123">Agregar ADP eTime desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="387e5-123">Adding ADP eTime from hello gallery</span></span>
<span data-ttu-id="387e5-124">integración de hello tooconfigure de ADP eTime en Azure AD, deberá tooadd ADP eTime de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="387e5-124">tooconfigure hello integration of ADP eTime into Azure AD, you need tooadd ADP eTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="387e5-125">**tooadd ADP eTime desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="387e5-125">**tooadd ADP eTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="387e5-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="387e5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="387e5-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="387e5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="387e5-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="387e5-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="387e5-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="387e5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="387e5-133">En el cuadro de búsqueda de hello, escriba **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="387e5-133">In hello search box, type **ADP eTime**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="387e5-135">En el panel de resultados de hello, seleccione **ADP eTime**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="387e5-135">In hello results panel, select **ADP eTime**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="387e5-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="387e5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="387e5-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ADP eTime con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="387e5-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="387e5-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en ADP eTime es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="387e5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ADP eTime is tooa user in Azure AD.</span></span> <span data-ttu-id="387e5-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en ADP eTime debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="387e5-140">In other words, a link relationship between an Azure AD user and hello related user in ADP eTime needs toobe established.</span></span>

<span data-ttu-id="387e5-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en eTime ADP.</span><span class="sxs-lookup"><span data-stu-id="387e5-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ADP eTime.</span></span>

<span data-ttu-id="387e5-142">tooconfigure y prueba de inicio de sesión único en Azure AD con ADP eTime, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="387e5-142">tooconfigure and test Azure AD single sign-on with ADP eTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="387e5-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="387e5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="387e5-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="387e5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="387e5-145">**[Creación de un usuario de prueba de ADP eTime](#creating-an-adp-etime-test-user)**  -toohave un equivalente de Britta Simon en eTime ADP que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="387e5-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - toohave a counterpart of Britta Simon in ADP eTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="387e5-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="387e5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="387e5-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="387e5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="387e5-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="387e5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="387e5-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de eTime ADP.</span><span class="sxs-lookup"><span data-stu-id="387e5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="387e5-150">**inicio de sesión único en tooconfigure Azure AD con ADP eTime, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="387e5-150">**tooconfigure Azure AD single sign-on with ADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="387e5-151">En el portal de Azure, en Hola Hola **ADP eTime** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="387e5-151">In hello Azure portal, on hello **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="387e5-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="387e5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="387e5-155">En hello **ADP eTime dominio y las direcciones URL** sección, lleve a cabo Hola siguiendo el paso:</span><span class="sxs-lookup"><span data-stu-id="387e5-155">On hello **ADP eTime Domain and URLs** section, perform hello following step:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="387e5-157">a.</span><span class="sxs-lookup"><span data-stu-id="387e5-157">a.</span></span> <span data-ttu-id="387e5-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<servername>.adp.com`</span><span class="sxs-lookup"><span data-stu-id="387e5-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="387e5-159">b.</span><span class="sxs-lookup"><span data-stu-id="387e5-159">b.</span></span> <span data-ttu-id="387e5-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="387e5-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="387e5-161">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="387e5-161">These values are not hello real.</span></span> <span data-ttu-id="387e5-162">Actualizar estos valores con dirección URL de respuesta real Hola y el identificador.</span><span class="sxs-lookup"><span data-stu-id="387e5-162">Update these values with hello actual Reply URL and Identifier.</span></span> <span data-ttu-id="387e5-163">Póngase en contacto con [equipo de soporte técnico de ADP eTime](https://www.adp.com/contact-us/overview.aspx) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="387e5-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooget these values.</span></span>

4. <span data-ttu-id="387e5-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="387e5-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="387e5-166">Hola aplicación eTime de ADP espera las aserciones de SAML de hello en un formato específico, lo que requiere tooadd atributo personalizado tooyour SAML atributos de token configuración de asignaciones.</span><span class="sxs-lookup"><span data-stu-id="387e5-166">hello ADP eTime application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="387e5-167">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="387e5-167">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="387e5-168">Hello notificación nombre será siempre **"PersonImmutableID"** y de que hemos asignado tooExtensionAttribute2 que contiene el valor de Hola Hola EmployeeID del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="387e5-168">hello claim name will always be **"PersonImmutableID"** and hello value of which we have mapped tooExtensionAttribute2 which contains hello EmployeeID of hello user.</span></span> 

    <span data-ttu-id="387e5-169">Aquí se realizará la asignación de usuario de Hola desde Azure AD tooADP eTime en hello EmployeeID, pero se puede asignar este valor diferente de tooa también teniendo en cuenta la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="387e5-169">Here hello user mapping from Azure AD tooADP eTime will be done on hello EmployeeID but you can map this tooa different value also based on your application settings.</span></span> <span data-ttu-id="387e5-170">Así pues, el trabajo con [equipo de soporte técnico de ADP eTime](https://www.adp.com/contact-us/overview.aspx) toouse primera Hola identificador correcto de un usuario y asignar ese valor con hello **"PersonImmutableID"** de notificación.</span><span class="sxs-lookup"><span data-stu-id="387e5-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first toouse hello correct identifier of a user and map that value with hello **"PersonImmutableID"** claim.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="387e5-172">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de Hola y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="387e5-172">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="387e5-173">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="387e5-173">Attribute Name</span></span> | <span data-ttu-id="387e5-174">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="387e5-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="387e5-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="387e5-175">PersonImmutableID</span></span> | <span data-ttu-id="387e5-176">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="387e5-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="387e5-177">a.</span><span class="sxs-lookup"><span data-stu-id="387e5-177">a.</span></span> <span data-ttu-id="387e5-178">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="387e5-178">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="387e5-181">b.</span><span class="sxs-lookup"><span data-stu-id="387e5-181">b.</span></span> <span data-ttu-id="387e5-182">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="387e5-182">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="387e5-183">c.</span><span class="sxs-lookup"><span data-stu-id="387e5-183">c.</span></span> <span data-ttu-id="387e5-184">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="387e5-184">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="387e5-185">d.</span><span class="sxs-lookup"><span data-stu-id="387e5-185">d.</span></span> <span data-ttu-id="387e5-186">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="387e5-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="387e5-187">Para poder configurar la aserción de SAML de hello, necesita toocontact su [equipo de soporte técnico de ADP eTime](https://www.adp.com/contact-us/overview.aspx) y solicite el valor de Hola de atributo del identificador único de hello para el inquilino.</span><span class="sxs-lookup"><span data-stu-id="387e5-187">Before you can configure hello SAML assertion, you need toocontact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="387e5-188">Necesita esta notificación personalizada de valor tooconfigure hello para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="387e5-188">You need this value tooconfigure hello custom claim for your application.</span></span> 

7. <span data-ttu-id="387e5-189">En hello **ADP eTime configuración** sección, haga clic en **configurar ADP eTime** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="387e5-189">On hello **ADP eTime Configuration** section, click **Configure ADP eTime** tooopen **Configure sign-on** window.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="387e5-191">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="387e5-191">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="387e5-193">tooconfigure inicio de sesión único en **ADP eTime** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de ADP eTime](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="387e5-193">tooconfigure single sign-on on **ADP eTime** side, you need toosend hello downloaded **Metadata XML** too[ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="387e5-194">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="387e5-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="387e5-195">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="387e5-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="387e5-196">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="387e5-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="387e5-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="387e5-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="387e5-198">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="387e5-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="387e5-200">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="387e5-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="387e5-201">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="387e5-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="387e5-203">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="387e5-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="387e5-205">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="387e5-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="387e5-207">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="387e5-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="387e5-209">a.</span><span class="sxs-lookup"><span data-stu-id="387e5-209">a.</span></span> <span data-ttu-id="387e5-210">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="387e5-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="387e5-211">b.</span><span class="sxs-lookup"><span data-stu-id="387e5-211">b.</span></span> <span data-ttu-id="387e5-212">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="387e5-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="387e5-213">c.</span><span class="sxs-lookup"><span data-stu-id="387e5-213">c.</span></span> <span data-ttu-id="387e5-214">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="387e5-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="387e5-215">d.</span><span class="sxs-lookup"><span data-stu-id="387e5-215">d.</span></span> <span data-ttu-id="387e5-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="387e5-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="387e5-217">Creación de un usuario de prueba de ADP eTime</span><span class="sxs-lookup"><span data-stu-id="387e5-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="387e5-218">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en eTime ADP.</span><span class="sxs-lookup"><span data-stu-id="387e5-218">hello objective of this section is toocreate a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="387e5-219">Trabajar con [equipo de soporte técnico de ADP eTime](https://www.adp.com/contact-us/overview.aspx) a los usuarios de tooadd hello en la cuenta de hello ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="387e5-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooadd hello users in hello ADP eTime account.</span></span> 
   
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="387e5-220">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="387e5-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="387e5-221">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooADP eTime.</span><span class="sxs-lookup"><span data-stu-id="387e5-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooADP eTime.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="387e5-223">**tooassign Britta Simon tooADP eTime, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="387e5-223">**tooassign Britta Simon tooADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="387e5-224">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="387e5-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="387e5-226">En la lista de aplicaciones de hello, seleccione **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="387e5-226">In hello applications list, select **ADP eTime**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="387e5-228">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="387e5-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="387e5-230">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="387e5-230">Click **Add** button.</span></span> <span data-ttu-id="387e5-231">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="387e5-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="387e5-233">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="387e5-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="387e5-234">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="387e5-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="387e5-235">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="387e5-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="387e5-236">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="387e5-236">Testing single sign-on</span></span>

<span data-ttu-id="387e5-237">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="387e5-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="387e5-238">Al hacer clic en icono Hola ADP eTime Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour ADP eTime aplicación.</span><span class="sxs-lookup"><span data-stu-id="387e5-238">When you click hello ADP eTime tile in hello Access Panel, you should get automatically signed-on tooyour ADP eTime application.</span></span>
<span data-ttu-id="387e5-239">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="387e5-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="387e5-240">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="387e5-240">Additional resources</span></span>

* [<span data-ttu-id="387e5-241">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="387e5-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="387e5-242">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="387e5-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

