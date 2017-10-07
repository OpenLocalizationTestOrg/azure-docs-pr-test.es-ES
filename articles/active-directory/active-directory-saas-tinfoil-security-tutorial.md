---
title: "Tutorial: Integración de Azure Active Directory con TINFOIL SECURITY | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y TINFOIL SECURITY."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a3fa9880d9e026c2d6d6548188df2269ff69139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="5752d-103">Tutorial: Integración de Azure Active Directory con TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="5752d-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span></span>

<span data-ttu-id="5752d-104">En este tutorial, aprenderá cómo toointegrate TINFOIL SECURITY con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5752d-104">In this tutorial, you learn how toointegrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5752d-105">Integración de TINFOIL SECURITY con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="5752d-105">Integrating TINFOIL SECURITY with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5752d-106">Puede controlar en Azure AD que tenga acceso tooTINFOIL seguridad</span><span class="sxs-lookup"><span data-stu-id="5752d-106">You can control in Azure AD who has access tooTINFOIL SECURITY</span></span>
- <span data-ttu-id="5752d-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTINFOIL seguridad (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5752d-107">You can enable your users tooautomatically get signed-on tooTINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5752d-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5752d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5752d-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5752d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5752d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5752d-110">Prerequisites</span></span>

<span data-ttu-id="5752d-111">integración de Azure AD con TINFOIL SECURITY tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="5752d-111">tooconfigure Azure AD integration with TINFOIL SECURITY, you need hello following items:</span></span>

- <span data-ttu-id="5752d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5752d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5752d-113">Una suscripción habilitada para el inicio de sesión único en TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="5752d-113">A TINFOIL SECURITY single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5752d-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="5752d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5752d-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="5752d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5752d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="5752d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5752d-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5752d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5752d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="5752d-118">Scenario description</span></span>
<span data-ttu-id="5752d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="5752d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5752d-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="5752d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5752d-121">Agregar TINFOIL SECURITY de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="5752d-121">Add TINFOIL SECURITY from hello gallery</span></span>
2. <span data-ttu-id="5752d-122">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="5752d-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tinfoil-security-from-hello-gallery"></a><span data-ttu-id="5752d-123">Agregar TINFOIL SECURITY de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="5752d-123">Add TINFOIL SECURITY from hello gallery</span></span>
<span data-ttu-id="5752d-124">integración de hello tooconfigure de TINFOIL SECURITY en Azure AD, deberá tooadd TINFOIL SECURITY de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="5752d-124">tooconfigure hello integration of TINFOIL SECURITY into Azure AD, you need tooadd TINFOIL SECURITY from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5752d-125">**tooadd TINFOIL SECURITY de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5752d-125">**tooadd TINFOIL SECURITY from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5752d-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="5752d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5752d-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="5752d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5752d-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5752d-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="5752d-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5752d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="5752d-133">En el cuadro de búsqueda de hello, escriba **TINFOIL SECURITY**, seleccione **TINFOIL SECURITY** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5752d-133">In hello search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button tooadd hello application.</span></span>

    ![TINFOIL SECURITY desde la galería](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5752d-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="5752d-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="5752d-136">En esta sección, configurará y probará el inicio de sesión único de Azure AD con TINFOIL SECURITY con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5752d-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5752d-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en TINFOIL SECURITY es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5752d-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TINFOIL SECURITY is tooa user in Azure AD.</span></span> <span data-ttu-id="5752d-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en TINFOIL SECURITY debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="5752d-138">In other words, a link relationship between an Azure AD user and hello related user in TINFOIL SECURITY needs toobe established.</span></span>

<span data-ttu-id="5752d-139">En TINFOIL SECURITY, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5752d-139">In TINFOIL SECURITY, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5752d-140">tooconfigure y prueba de inicio de sesión único en Azure AD con TINFOIL SECURITY, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="5752d-140">tooconfigure and test Azure AD single sign-on with TINFOIL SECURITY, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5752d-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="5752d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5752d-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5752d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5752d-143">**[Crear un usuario de prueba de TINFOIL SECURITY](#create-a-tinfoil-security-test-user)**  -toohave un equivalente de Britta Simon en TINFOIL SECURITY que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="5752d-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - toohave a counterpart of Britta Simon in TINFOIL SECURITY that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5752d-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5752d-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5752d-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="5752d-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5752d-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5752d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5752d-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="5752d-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span></span>

<span data-ttu-id="5752d-148">**inicio de sesión único en tooconfigure AD de Azure con TINFOIL SECURITY, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5752d-148">**tooconfigure Azure AD single sign-on with TINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="5752d-149">En el portal de Azure, en Hola Hola **TINFOIL SECURITY** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="5752d-149">In hello Azure portal, on hello **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="5752d-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5752d-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Inicio de sesión basado en SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. <span data-ttu-id="5752d-153">En hello **TINFOIL SECURITY dominio y las direcciones URL** sección, hello usuario no tiene tooperform todos los pasos tal y como aplicación hello ya está integrado previamente con Azure.</span><span class="sxs-lookup"><span data-stu-id="5752d-153">On hello **TINFOIL SECURITY Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. <span data-ttu-id="5752d-155">En hello **el certificado de firma de SAML** Hola de copia, en una sección **huella digital** valor.</span><span class="sxs-lookup"><span data-stu-id="5752d-155">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value.</span></span>

    ![Sección Certificado de firma SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. <span data-ttu-id="5752d-157">asignaciones de atributos de tooadd Hola necesario, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="5752d-157">tooadd hello required attribute mappings, perform hello following steps:</span></span>
    
    <span data-ttu-id="5752d-158">![Atributos](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="5752d-158">![Attributes](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span></span>
    
    | <span data-ttu-id="5752d-159">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="5752d-159">Attribute Name</span></span>    |   <span data-ttu-id="5752d-160">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="5752d-160">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="5752d-161">accountid</span><span class="sxs-lookup"><span data-stu-id="5752d-161">accountid</span></span> | <span data-ttu-id="5752d-162">UXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="5752d-162">UXXXXXXXXXXXXX</span></span> |
    
    <span data-ttu-id="5752d-163">a.</span><span class="sxs-lookup"><span data-stu-id="5752d-163">a.</span></span> <span data-ttu-id="5752d-164">Haga clic en **agregar atributo de usuario**.</span><span class="sxs-lookup"><span data-stu-id="5752d-164">Click **add user attribute**.</span></span>
    
    <span data-ttu-id="5752d-165">![AGREGAR atributo](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="5752d-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span></span>
    
    <span data-ttu-id="5752d-166">![AGREGAR atributo](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="5752d-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span></span>
    
    <span data-ttu-id="5752d-167">b.</span><span class="sxs-lookup"><span data-stu-id="5752d-167">b.</span></span> <span data-ttu-id="5752d-168">Hola **nombre del atributo** cuadro de texto, tipo **accountid**.</span><span class="sxs-lookup"><span data-stu-id="5752d-168">In hello **Attribute Name** textbox, type **accountid**.</span></span>
    
    <span data-ttu-id="5752d-169">c.</span><span class="sxs-lookup"><span data-stu-id="5752d-169">c.</span></span> <span data-ttu-id="5752d-170">Hola **valor del atributo** cuadro de texto, valor de identificador de cuenta de hello de pegar que obtendrá más adelante en el tutorial de Hola.</span><span class="sxs-lookup"><span data-stu-id="5752d-170">In hello **Attribute Value** textbox, paste hello account ID value which you will get later on hello tutorial.</span></span>
    
    <span data-ttu-id="5752d-171">d.</span><span class="sxs-lookup"><span data-stu-id="5752d-171">d.</span></span> <span data-ttu-id="5752d-172">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5752d-172">Click **Ok**.</span></span>    

6. <span data-ttu-id="5752d-173">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="5752d-173">Click **Save** button.</span></span>

    ![Botón Guardar](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5752d-175">En hello **configuración de seguridad de TINFOIL** sección, haga clic en **configurar TINFOIL SECURITY** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="5752d-175">On hello **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5752d-176">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="5752d-176">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. <span data-ttu-id="5752d-178">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="5752d-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span></span>

9. <span data-ttu-id="5752d-179">En la barra de herramientas de hello en la parte superior de hello, haga clic en **mi cuenta**.</span><span class="sxs-lookup"><span data-stu-id="5752d-179">In hello toolbar on hello top, click **My Account**.</span></span>
   
    <span data-ttu-id="5752d-180">![Panel](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Panel")</span><span class="sxs-lookup"><span data-stu-id="5752d-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span></span>

10. <span data-ttu-id="5752d-181">Haga clic en **Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="5752d-181">Click **Security**.</span></span>
   
    <span data-ttu-id="5752d-182">![Seguridad](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Seguridad")</span><span class="sxs-lookup"><span data-stu-id="5752d-182">![Security](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Security")</span></span>

11. <span data-ttu-id="5752d-183">En hello **Single Sign-On** configuración, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="5752d-183">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="5752d-184">![Inicio de sesión único](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="5752d-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="5752d-185">a.</span><span class="sxs-lookup"><span data-stu-id="5752d-185">a.</span></span> <span data-ttu-id="5752d-186">Seleccione **Habilitar SAML**.</span><span class="sxs-lookup"><span data-stu-id="5752d-186">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="5752d-187">b.</span><span class="sxs-lookup"><span data-stu-id="5752d-187">b.</span></span> <span data-ttu-id="5752d-188">Haga clic en **Configuración manual**.</span><span class="sxs-lookup"><span data-stu-id="5752d-188">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="5752d-189">c.</span><span class="sxs-lookup"><span data-stu-id="5752d-189">c.</span></span> <span data-ttu-id="5752d-190">En **dirección URL de Post SAML** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5752d-190">In **SAML Post URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span></span>
   
    <span data-ttu-id="5752d-191">d.</span><span class="sxs-lookup"><span data-stu-id="5752d-191">d.</span></span> <span data-ttu-id="5752d-192">En **huella digital de certificado SAML** cuadro de texto, pegue Hola valo **huella digital** que haya copiado desde **el certificado de firma de SAML** sección.</span><span class="sxs-lookup"><span data-stu-id="5752d-192">In **SAML Certificate Fingerprint** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span>
  
    <span data-ttu-id="5752d-193">e.</span><span class="sxs-lookup"><span data-stu-id="5752d-193">e.</span></span> <span data-ttu-id="5752d-194">Copia **su Id. de cuenta** valor y pegue el valor de hello en **valor del atributo** en el cuadro de texto **Agregar atributo** sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="5752d-194">Copy **Your Account ID** value and paste hello value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span></span>
   
    <span data-ttu-id="5752d-195">f.</span><span class="sxs-lookup"><span data-stu-id="5752d-195">f.</span></span> <span data-ttu-id="5752d-196">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="5752d-196">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5752d-197">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="5752d-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5752d-198">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="5752d-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5752d-199">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5752d-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5752d-200">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5752d-200">Create an Azure AD test user</span></span>
<span data-ttu-id="5752d-201">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="5752d-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="5752d-203">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5752d-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5752d-204">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="5752d-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5752d-206">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5752d-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![<span data-ttu-id="5752d-207">Usuarios y grupos -> Todos los usuarios</span><span class="sxs-lookup"><span data-stu-id="5752d-207">Users and groups -> All users</span></span> ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5752d-208">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5752d-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Usuario](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5752d-210">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="5752d-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5752d-212">a.</span><span class="sxs-lookup"><span data-stu-id="5752d-212">a.</span></span> <span data-ttu-id="5752d-213">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5752d-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5752d-214">b.</span><span class="sxs-lookup"><span data-stu-id="5752d-214">b.</span></span> <span data-ttu-id="5752d-215">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5752d-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5752d-216">c.</span><span class="sxs-lookup"><span data-stu-id="5752d-216">c.</span></span> <span data-ttu-id="5752d-217">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="5752d-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5752d-218">d.</span><span class="sxs-lookup"><span data-stu-id="5752d-218">d.</span></span> <span data-ttu-id="5752d-219">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5752d-219">Click **Create**.</span></span>
 
### <a name="create-a-tinfoil-security-test-user"></a><span data-ttu-id="5752d-220">Creación de un usuario de prueba de TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="5752d-220">Create a TINFOIL SECURITY test user</span></span>

<span data-ttu-id="5752d-221">En orden tooenable toolog de los usuarios de Azure AD en TINFOIL SECURITY, se les deben aprovisionar en TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="5752d-221">In order tooenable Azure AD users toolog into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span></span> <span data-ttu-id="5752d-222">En caso de hello de TINFOIL SECURITY, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="5752d-222">In hello case of TINFOIL SECURITY, provisioning is a manual task.</span></span>

<span data-ttu-id="5752d-223">**tooget un usuario aprovisionado, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5752d-223">**tooget a user provisioned, perform hello following steps:**</span></span>

1. <span data-ttu-id="5752d-224">Si el usuario de hello forma parte de una cuenta de empresa, deberá demasiado[póngase en contacto con el equipo de soporte técnico de TINFOIL SECURITY hello](https://www.tinfoilsecurity.com/contact) cuenta de usuario de hello tooget creada.</span><span class="sxs-lookup"><span data-stu-id="5752d-224">If hello user is a part of an Enterprise account, you need too[contact hello TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) tooget hello user account created.</span></span>

2. <span data-ttu-id="5752d-225">Si hello es un usuario de TINFOIL SECURITY SaaS regular, usuario Hola puede agregar un tooany de colaborador de sitios del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="5752d-225">If hello user is a regular TINFOIL SECURITY SaaS user, then hello user can add a collaborator tooany of hello user’s sites.</span></span> <span data-ttu-id="5752d-226">Este desencadena un toosend de proceso especificado un toohello de invitación de correo electrónico toocreate una nueva cuenta de usuario de TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="5752d-226">This triggers a process toosend an invitation toohello specified email toocreate a new TINFOIL SECURITY user account.</span></span>

> [!NOTE]
> <span data-ttu-id="5752d-227">Puede usar cualquier otra TINFOIL SECURITY usuario cuenta herramienta de creación o las API proporcionadas por TINFOIL SECURITY tooprovision cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5752d-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY tooprovision Azure AD user accounts.</span></span>
> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5752d-228">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5752d-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="5752d-229">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooTINFOIL seguridad.</span><span class="sxs-lookup"><span data-stu-id="5752d-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTINFOIL SECURITY.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="5752d-231">**tooassign Britta Simon tooTINFOIL seguridad, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="5752d-231">**tooassign Britta Simon tooTINFOIL SECURITY, perform hello following steps:**</span></span>

1. <span data-ttu-id="5752d-232">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5752d-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="5752d-234">En la lista de aplicaciones de hello, seleccione **TINFOIL SECURITY**.</span><span class="sxs-lookup"><span data-stu-id="5752d-234">In hello applications list, select **TINFOIL SECURITY**.</span></span>

    ![Selección de TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. <span data-ttu-id="5752d-236">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5752d-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="5752d-238">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5752d-238">Click **Add** button.</span></span> <span data-ttu-id="5752d-239">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5752d-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="5752d-241">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="5752d-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5752d-242">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5752d-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5752d-243">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5752d-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5752d-244">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="5752d-244">Test single sign-on</span></span>

<span data-ttu-id="5752d-245">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="5752d-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5752d-246">Al hacer clic en icono de TINFOIL SECURITY Hola Hola Panel de acceso, deberá obtener la aplicación de TINFOIL SECURITY tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="5752d-246">When you click hello TINFOIL SECURITY tile in hello Access Panel, you should get automatically signed-on tooyour TINFOIL SECURITY application.</span></span> <span data-ttu-id="5752d-247">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5752d-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5752d-248">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="5752d-248">Additional resources</span></span>

* [<span data-ttu-id="5752d-249">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5752d-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5752d-250">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5752d-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

