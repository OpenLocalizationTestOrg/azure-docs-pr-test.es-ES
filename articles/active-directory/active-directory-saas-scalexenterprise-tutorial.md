---
title: "Tutorial: Integración de Azure Active Directory con ScaleX Enterprise | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ScaleX Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: e398b98d9e0957b5f92c82359651c345d22c3a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="bfb78-103">Tutorial: Integración de Azure Active Directory con ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="bfb78-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="bfb78-104">En este tutorial, aprenderá cómo toointegrate ScaleX Enterprise con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bfb78-104">In this tutorial, you learn how toointegrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bfb78-105">Integración ScaleX Enterprise con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="bfb78-105">Integrating ScaleX Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bfb78-106">Puede controlar en Azure AD que tenga acceso tooScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="bfb78-106">You can control in Azure AD who has access tooScaleX Enterprise</span></span>
- <span data-ttu-id="bfb78-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooScaleX Enterprise (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb78-107">You can enable your users tooautomatically get signed-on tooScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bfb78-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="bfb78-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bfb78-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte.</span><span class="sxs-lookup"><span data-stu-id="bfb78-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="bfb78-110">¿Qué es el acceso a aplicaciones y el inicio de sesión único con [Azure Active Directory](active-directory-appssoaccess-whatis.md)?</span><span class="sxs-lookup"><span data-stu-id="bfb78-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfb78-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bfb78-111">Prerequisites</span></span>

<span data-ttu-id="bfb78-112">integración de Azure AD con ScaleX Enterprise tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="bfb78-112">tooconfigure Azure AD integration with ScaleX Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="bfb78-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb78-113">An Azure AD subscription</span></span>
- <span data-ttu-id="bfb78-114">Una suscripción habilitada para el inicio de sesión único en ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="bfb78-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bfb78-115">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="bfb78-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bfb78-116">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="bfb78-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bfb78-117">No use su entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bfb78-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="bfb78-118">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bfb78-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bfb78-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="bfb78-119">Scenario description</span></span>
<span data-ttu-id="bfb78-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="bfb78-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bfb78-121">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="bfb78-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bfb78-122">Agregar ScaleX Enterprise desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="bfb78-122">Adding ScaleX Enterprise from hello gallery</span></span>
2. <span data-ttu-id="bfb78-123">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb78-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-hello-gallery"></a><span data-ttu-id="bfb78-124">Agregar ScaleX Enterprise desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="bfb78-124">Adding ScaleX Enterprise from hello gallery</span></span>
<span data-ttu-id="bfb78-125">integración de hello tooconfigure de ScaleX Enterprise en tooAzure AD, deberá tooadd ScaleX Enterprise de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="bfb78-125">tooconfigure hello integration of ScaleX Enterprise in tooAzure AD, you need tooadd ScaleX Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bfb78-126">**tooadd ScaleX Enterprise de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bfb78-126">**tooadd ScaleX Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfb78-127">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="bfb78-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bfb78-129">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="bfb78-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bfb78-130">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bfb78-130">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="bfb78-132">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfb78-132">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="bfb78-134">En el cuadro de búsqueda de hello, escriba **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="bfb78-134">In hello search box, type **ScaleX Enterprise**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="bfb78-136">En el panel de resultados de hello, seleccione **ScaleX Enterprise**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bfb78-136">In hello results panel, select **ScaleX Enterprise**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bfb78-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb78-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bfb78-139">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ScaleX Enterprise utilizando un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bfb78-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bfb78-140">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en ScaleX Enterprise es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bfb78-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScaleX Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="bfb78-141">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en ScaleX empresa necesita toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="bfb78-141">In other words, a link relationship between an Azure AD user and hello related user in ScaleX Enterprise needs toobe established.</span></span>

<span data-ttu-id="bfb78-142">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="bfb78-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="bfb78-143">tooconfigure y prueba de inicio de sesión único en Azure AD con ScaleX Enterprise, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="bfb78-143">tooconfigure and test Azure AD single sign-on with ScaleX Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bfb78-144">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="bfb78-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bfb78-145">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bfb78-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bfb78-146">**[Crear un usuario de prueba de ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)**  -toohave un equivalente de Britta Simon en ScaleX Enterprise que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="bfb78-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - toohave a counterpart of Britta Simon in ScaleX Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bfb78-147">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="bfb78-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bfb78-148">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="bfb78-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bfb78-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb78-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bfb78-150">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación empresarial de ScaleX.</span><span class="sxs-lookup"><span data-stu-id="bfb78-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="bfb78-151">**inicio de sesión único en tooconfigure AD de Azure con ScaleX Enterprise, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bfb78-151">**tooconfigure Azure AD single sign-on with ScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfb78-152">En el portal de Azure, en Hola Hola **ScaleX Enterprise** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="bfb78-152">In hello Azure portal, on hello **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="bfb78-154">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="bfb78-154">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="bfb78-156">En hello **ScaleX Enterprise dominio y las direcciones URL** sección, lleve a cabo Hola siguientes pasos si desea tooconfigure aplicación de hello en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="bfb78-156">On hello **ScaleX Enterprise Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="bfb78-158">a.</span><span class="sxs-lookup"><span data-stu-id="bfb78-158">a.</span></span> <span data-ttu-id="bfb78-159">Hola **identificador** cuadro de texto, valor de tipo hello mediante Hola sigue el patrón:`https://platform.rescale.com/saml2/<company id>/`</span><span class="sxs-lookup"><span data-stu-id="bfb78-159">In hello **Identifier** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="bfb78-160">b.</span><span class="sxs-lookup"><span data-stu-id="bfb78-160">b.</span></span> <span data-ttu-id="bfb78-161">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://platform.rescale.com/saml2/<company id>/acs/`</span><span class="sxs-lookup"><span data-stu-id="bfb78-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="bfb78-162">Comprobar **mostrar avanzadas de configuración de direcciones URL**, si lo desea tooconfigure aplicación de hello en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="bfb78-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="bfb78-164">Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello mediante Hola sigue el patrón:`https://platform.rescale.com/saml2/<company id>/sso/`</span><span class="sxs-lookup"><span data-stu-id="bfb78-164">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="bfb78-165">Estas no son valores reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfb78-165">These are not hello real values.</span></span> <span data-ttu-id="bfb78-166">Actualizar estos valores con hello identificador real, la dirección URL de respuesta o la dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="bfb78-166">Update these values with hello actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="bfb78-167">Póngase en contacto con [equipo de soporte técnico de cliente de empresa ScaleX](http://info.rescale.com/contact_sales) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="bfb78-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) tooget these values.</span></span> 

5. <span data-ttu-id="bfb78-168">La aplicación ScaleX espera las aserciones de SAML de hello en un formato específico, lo que requiere toomodify atributo personalizado tooyour SAML atributos de token configuración de asignaciones.</span><span class="sxs-lookup"><span data-stu-id="bfb78-168">Your ScaleX application expects hello SAML assertions in a specific format, which requires you toomodify custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="bfb78-169">Haga clic en **ver y editar todos los demás atributos de usuario** casilla tooopen Hola personalizado atributos de configuración.</span><span class="sxs-lookup"><span data-stu-id="bfb78-169">Click **View and edit all other user attributes** checkbox tooopen hello custom attributes settings.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="bfb78-171">a.</span><span class="sxs-lookup"><span data-stu-id="bfb78-171">a.</span></span> <span data-ttu-id="bfb78-172">Haga clic con el atributo de hello **nombre** y haga clic en eliminar.</span><span class="sxs-lookup"><span data-stu-id="bfb78-172">Right click hello attribute **name** and click delete.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="bfb78-174">b.</span><span class="sxs-lookup"><span data-stu-id="bfb78-174">b.</span></span> <span data-ttu-id="bfb78-175">Haga clic en **emailaddress** ventana Editar atributo de atributo tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="bfb78-175">Click **emailaddress** attribute tooopen hello Edit Attribute window.</span></span> <span data-ttu-id="bfb78-176">Cambie el valor de **user.mail** demasiado**user.userprincipalname** y haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="bfb78-176">Change its value from **user.mail** too**user.userprincipalname** and click Ok.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="bfb78-178">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="bfb78-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="bfb78-180">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="bfb78-180">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="bfb78-182">En hello **configuración de la empresa ScaleX** sección, haga clic en **configurar ScaleX Enterprise** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="bfb78-182">On hello **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bfb78-183">Hola copia **Id. de entidad SAML** y **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="bfb78-183">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="bfb78-185">inicio de sesión único en tooconfigure en **ScaleX Enterprise** lado, el sitio Web de Enterprise ScaleX empresa toohello de inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="bfb78-185">tooconfigure single sign-on on **ScaleX Enterprise** side, login toohello ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="bfb78-186">Haga clic en menú Hola Hola superior derecha y seleccione **Contoso administración**.</span><span class="sxs-lookup"><span data-stu-id="bfb78-186">Click hello menu in hello upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bfb78-187">Contoso solo es un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="bfb78-187">Contoso is just an example.</span></span> <span data-ttu-id="bfb78-188">Debería tratarse del nombre real de la empresa.</span><span class="sxs-lookup"><span data-stu-id="bfb78-188">This should be your actual Company Name.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="bfb78-190">Seleccione **integraciones** desde el menú superior de Hola y seleccione **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="bfb78-190">Select **Integrations** from hello top menu and select **Single Sign-On**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="bfb78-192">Complete el formulario de hello como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="bfb78-192">Complete hello form as follows:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="bfb78-194">a.</span><span class="sxs-lookup"><span data-stu-id="bfb78-194">a.</span></span> <span data-ttu-id="bfb78-195">Seleccione **"Create any user who can authenticate with SSO"** (Crear cualquier usuario que se pueda autenticar con SSO).</span><span class="sxs-lookup"><span data-stu-id="bfb78-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="bfb78-196">b.</span><span class="sxs-lookup"><span data-stu-id="bfb78-196">b.</span></span> <span data-ttu-id="bfb78-197">**Proveedor de servicios saml**: pegue el valor de hello ***urn: oasis: nombres: tc: SAML:2.0:nameid-formato: persistente***</span><span class="sxs-lookup"><span data-stu-id="bfb78-197">**Service Provider saml**: Paste hello value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="bfb78-198">c.</span><span class="sxs-lookup"><span data-stu-id="bfb78-198">c.</span></span> <span data-ttu-id="bfb78-199">**Nombre del campo de correo electrónico del proveedor de identidades en la respuesta de ACS**: pegue el valor de Hola`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="bfb78-199">**Name of Identity Provider email field in ACS response**: Paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="bfb78-200">d.</span><span class="sxs-lookup"><span data-stu-id="bfb78-200">d.</span></span> <span data-ttu-id="bfb78-201">**Id. de entidad EntityDescriptor de proveedor de identidad:** Hola pegar **Id. de entidad SAML** valor copiados de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bfb78-201">**Identity Provider EntityDescriptor Entity ID:** Paste hello **SAML Entity ID** value copied from hello Azure portal.</span></span>

    <span data-ttu-id="bfb78-202">e.</span><span class="sxs-lookup"><span data-stu-id="bfb78-202">e.</span></span> <span data-ttu-id="bfb78-203">**URL de SingleSignOnService del proveedor de identidades:** Hola pegar **SAML Single Sign-On dirección URL del servicio** de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bfb78-203">**Identity Provider SingleSignOnService URL:** Paste hello **SAML Single Sign-On Service URL** from hello Azure portal.</span></span>

    <span data-ttu-id="bfb78-204">f.</span><span class="sxs-lookup"><span data-stu-id="bfb78-204">f.</span></span> <span data-ttu-id="bfb78-205">**Certificado público X509 del proveedor de identidades:** descargar el certificado de hello abierto X509 de hello Azure en el Bloc de notas y pegue contenido de hello en este cuadro.</span><span class="sxs-lookup"><span data-stu-id="bfb78-205">**Identity Provider public X509 certificate:** Open hello X509 certificate downloaded from hello Azure in notepad and paste hello contents in this box.</span></span> <span data-ttu-id="bfb78-206">Asegúrese de que no haya que ningún saltos de línea hello intermedia del contenido del certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfb78-206">Ensure there are no line breaks in hello middle of hello certificate contents.</span></span>
    
    <span data-ttu-id="bfb78-207">g.</span><span class="sxs-lookup"><span data-stu-id="bfb78-207">g.</span></span> <span data-ttu-id="bfb78-208">Comprobar Hola siguiendo las casillas de verificación: **habilitado, cifrar NameID y AuthnRequests de inicio de sesión.**</span><span class="sxs-lookup"><span data-stu-id="bfb78-208">Check hello following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="bfb78-209">h.</span><span class="sxs-lookup"><span data-stu-id="bfb78-209">h.</span></span> <span data-ttu-id="bfb78-210">Haga clic en **configuración de SSO de actualización** configuración de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="bfb78-210">Click **Update SSO Settings** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="bfb78-211">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="bfb78-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bfb78-212">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="bfb78-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bfb78-213">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bfb78-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bfb78-214">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb78-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="bfb78-215">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="bfb78-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="bfb78-217">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bfb78-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfb78-218">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="bfb78-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bfb78-220">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="bfb78-220">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bfb78-222">En la parte superior de saludo del cuadro de diálogo de hello, haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bfb78-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bfb78-224">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="bfb78-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bfb78-226">a.</span><span class="sxs-lookup"><span data-stu-id="bfb78-226">a.</span></span> <span data-ttu-id="bfb78-227">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bfb78-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bfb78-228">b.</span><span class="sxs-lookup"><span data-stu-id="bfb78-228">b.</span></span> <span data-ttu-id="bfb78-229">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bfb78-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bfb78-230">c.</span><span class="sxs-lookup"><span data-stu-id="bfb78-230">c.</span></span> <span data-ttu-id="bfb78-231">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="bfb78-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bfb78-232">d.</span><span class="sxs-lookup"><span data-stu-id="bfb78-232">d.</span></span> <span data-ttu-id="bfb78-233">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bfb78-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="bfb78-234">Creación de un usuario de prueba de ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="bfb78-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="bfb78-235">toolog de los usuarios de Azure AD tooenable en tooScaleX Enterprise, se les deben aprovisionar en tooScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="bfb78-235">tooenable Azure AD users toolog in tooScaleX Enterprise, they must be provisioned in tooScaleX Enterprise.</span></span> <span data-ttu-id="bfb78-236">En caso de hello de ScaleX Enterprise, el aprovisionamiento es una tarea automática y no se requiere ningún paso manual.</span><span class="sxs-lookup"><span data-stu-id="bfb78-236">In hello case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="bfb78-237">Todos los usuarios que pueden autenticar correctamente con las credenciales SSO se aprovisionará automáticamente en hello ScaleX lado.</span><span class="sxs-lookup"><span data-stu-id="bfb78-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on hello ScaleX side.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bfb78-238">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb78-238">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bfb78-239">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de empresa de tooScaleX de acceso de usuarios.</span><span class="sxs-lookup"><span data-stu-id="bfb78-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting user access tooScaleX Enterprise.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="bfb78-241">**tooassign Britta Simon tooScaleX Enterprise, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bfb78-241">**tooassign Britta Simon tooScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfb78-242">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bfb78-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="bfb78-244">En la lista de aplicaciones de hello, seleccione **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="bfb78-244">In hello applications list, select **ScaleX Enterprise**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="bfb78-246">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bfb78-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="bfb78-248">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="bfb78-248">Click **Add** button.</span></span> <span data-ttu-id="bfb78-249">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bfb78-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="bfb78-251">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfb78-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bfb78-252">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bfb78-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bfb78-253">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bfb78-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="bfb78-254">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="bfb78-254">Testing single sign-on</span></span>

<span data-ttu-id="bfb78-255">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="bfb78-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bfb78-256">Haga clic en hello ScaleX Enterprise disponer en mosaico en hello Panel de acceso, obtendrá automáticamente ha iniciado sesión tooyour aplicación ScaleX empresarial.</span><span class="sxs-lookup"><span data-stu-id="bfb78-256">Click hello ScaleX Enterprise tile in hello Access Panel, you will get automatically signed-on tooyour ScaleX Enterprise application.</span></span> <span data-ttu-id="bfb78-257">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="bfb78-257">For more information about hello Access Panel, see [Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="bfb78-258">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="bfb78-258">Additional resources</span></span>

* [<span data-ttu-id="bfb78-259">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bfb78-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bfb78-260">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bfb78-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

