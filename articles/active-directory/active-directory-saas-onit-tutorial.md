---
title: "Tutorial: Integración de Azure Active Directory con Onit | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Onit."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bc479a28-8fcd-493f-ac53-681975a5149c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 9e12449e5bf7f169b3cadfaa12438ac5d52ed8f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-onit"></a><span data-ttu-id="bf0b2-103">Tutorial: Integración de Azure Active Directory con Onit</span><span class="sxs-lookup"><span data-stu-id="bf0b2-103">Tutorial: Azure Active Directory integration with Onit</span></span>

<span data-ttu-id="bf0b2-104">En este tutorial, aprenderá cómo toointegrate Onit con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bf0b2-104">In this tutorial, you learn how toointegrate Onit with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bf0b2-105">Integración de Onit con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="bf0b2-105">Integrating Onit with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bf0b2-106">Puede controlar en Azure AD que tenga acceso tooOnit.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-106">You can control in Azure AD who has access tooOnit.</span></span>
- <span data-ttu-id="bf0b2-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooOnit (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-107">You can enable your users tooautomatically get signed-on tooOnit (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="bf0b2-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="bf0b2-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bf0b2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf0b2-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bf0b2-110">Prerequisites</span></span>

<span data-ttu-id="bf0b2-111">integración de Azure AD con Onit tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="bf0b2-111">tooconfigure Azure AD integration with Onit, you need hello following items:</span></span>

- <span data-ttu-id="bf0b2-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf0b2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bf0b2-113">Una suscripción habilitada para el inicio de sesión único en Onit</span><span class="sxs-lookup"><span data-stu-id="bf0b2-113">An Onit single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bf0b2-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bf0b2-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="bf0b2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bf0b2-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bf0b2-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bf0b2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bf0b2-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="bf0b2-118">Scenario description</span></span>

<span data-ttu-id="bf0b2-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bf0b2-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="bf0b2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bf0b2-121">Agregar Onit desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="bf0b2-121">Adding Onit from hello gallery</span></span>
2. <span data-ttu-id="bf0b2-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf0b2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-onit-from-hello-gallery"></a><span data-ttu-id="bf0b2-123">Agregar Onit desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="bf0b2-123">Adding Onit from hello gallery</span></span>
<span data-ttu-id="bf0b2-124">integración de hello tooconfigure de Onit en Azure AD, deberá tooadd Onit de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-124">tooconfigure hello integration of Onit into Azure AD, you need tooadd Onit from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bf0b2-125">**tooadd Onit de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bf0b2-125">**tooadd Onit from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf0b2-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="bf0b2-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bf0b2-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="bf0b2-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="bf0b2-133">En el cuadro de búsqueda de hello, escriba **Onit**, seleccione **Onit** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-133">In hello search box, type **Onit**, select **Onit** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados de Onit Hola](./media/active-directory-saas-onit-tutorial/tutorial_onit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bf0b2-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf0b2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="bf0b2-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Onit con un usuario de prueba llamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="bf0b2-136">In this section, you configure and test Azure AD single sign-on with Onit based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bf0b2-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Onit es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Onit is tooa user in Azure AD.</span></span> <span data-ttu-id="bf0b2-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Onit debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-138">In other words, a link relationship between an Azure AD user and hello related user in Onit needs toobe established.</span></span>

<span data-ttu-id="bf0b2-139">En Onit, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-139">In Onit, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bf0b2-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Onit, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="bf0b2-140">tooconfigure and test Azure AD single sign-on with Onit, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bf0b2-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bf0b2-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bf0b2-143">**[Crear un usuario de prueba de Onit](#create-an-onit-test-user)**  -toohave un equivalente de Britta Simon en Onit que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-143">**[Create an Onit test user](#create-an-onit-test-user)** - toohave a counterpart of Britta Simon in Onit that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bf0b2-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bf0b2-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-145">**[Test single sign-on](#test-single-sign-on)** tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bf0b2-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf0b2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bf0b2-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Onit.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Onit application.</span></span>

<span data-ttu-id="bf0b2-148">**inicio de sesión único en Azure AD tooconfigure con Onit, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bf0b2-148">**tooconfigure Azure AD single sign-on with Onit, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf0b2-149">En el portal de Azure, en Hola Hola **Onit** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-149">In hello Azure portal, on hello **Onit** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="bf0b2-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-onit-tutorial/tutorial_onit_samlbase.png)

3. <span data-ttu-id="bf0b2-153">En hello **Onit dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="bf0b2-153">On hello **Onit Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_url.png)

    <span data-ttu-id="bf0b2-155">a.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-155">a.</span></span> <span data-ttu-id="bf0b2-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="bf0b2-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub-domain>.onit.com`</span></span>

    <span data-ttu-id="bf0b2-157">b.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-157">b.</span></span> <span data-ttu-id="bf0b2-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="bf0b2-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<sub-domain>.onit.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bf0b2-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-159">These values are not real.</span></span> <span data-ttu-id="bf0b2-160">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bf0b2-161">Póngase en contacto con [equipo de soporte técnico de cliente de Onit](https://www.onit.com/support) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-161">Contact [Onit Client support team](https://www.onit.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="bf0b2-162">En hello **el certificado de firma de SAML** Hola de copia, en una sección **huella digital** el valor de certificado.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-162">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-onit-tutorial/tutorial_onit_certificate.png) 

5. <span data-ttu-id="bf0b2-164">Aplicación de Onit espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-164">Onit application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="bf0b2-165">Configure Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-165">Please configure hello following claims for this application.</span></span> <span data-ttu-id="bf0b2-166">Puede administrar valores de hello de estos atributos de hello **"Atrribute"** pestaña de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-166">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="bf0b2-167">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-167">hello following screenshot shows an example for this.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-onit-tutorial/tutorial_onit_attribute.png) 

6. <span data-ttu-id="bf0b2-169">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de Hola y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="bf0b2-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="bf0b2-170">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="bf0b2-170">Attribute Name</span></span> | <span data-ttu-id="bf0b2-171">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="bf0b2-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="bf0b2-172">email</span><span class="sxs-lookup"><span data-stu-id="bf0b2-172">email</span></span> | <span data-ttu-id="bf0b2-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="bf0b2-173">user.mail</span></span> |
    
    <span data-ttu-id="bf0b2-174">a.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-174">a.</span></span> <span data-ttu-id="bf0b2-175">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-onit-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-onit-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="bf0b2-178">b.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-178">b.</span></span> <span data-ttu-id="bf0b2-179">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-179">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="bf0b2-180">c.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-180">c.</span></span> <span data-ttu-id="bf0b2-181">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-181">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="bf0b2-182">d.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-182">d.</span></span> <span data-ttu-id="bf0b2-183">Deje hello **Namespace** en blanco.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-183">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="bf0b2-184">e.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-184">e.</span></span> <span data-ttu-id="bf0b2-185">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-185">Click **Ok**.</span></span>

7. <span data-ttu-id="bf0b2-186">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="bf0b2-186">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-onit-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="bf0b2-188">En hello **configuración de Onit** sección, haga clic en **configurar Onit** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-188">On hello **Onit Configuration** section, click **Configure Onit** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bf0b2-189">Hola copia **dirección URL de cierre de sesión, SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="bf0b2-189">Copy hello **Sign-Out URL, SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_configure.png)

9. <span data-ttu-id="bf0b2-191">En otra ventana del explorador web, inicie sesión en como administrador en el sitio de Onit de la compañía.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-191">In a different web browser window, log into your Onit company site as an administrator.</span></span>

10. <span data-ttu-id="bf0b2-192">En el menú de hello en la parte superior de hello, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-192">In hello menu on hello top, click **Administration**.</span></span>
   
   <span data-ttu-id="bf0b2-193">![Administración](./media/active-directory-saas-onit-tutorial/IC791174.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="bf0b2-193">![Administration](./media/active-directory-saas-onit-tutorial/IC791174.png "Administration")</span></span>
11. <span data-ttu-id="bf0b2-194">Haga clic en **Edit Corporation**(Editar corporación).</span><span class="sxs-lookup"><span data-stu-id="bf0b2-194">Click **Edit Corporation**.</span></span>
   
   <span data-ttu-id="bf0b2-195">![Editar corporación](./media/active-directory-saas-onit-tutorial/IC791175.png "Editar corporación")</span><span class="sxs-lookup"><span data-stu-id="bf0b2-195">![Edit Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "Edit Corporation")</span></span>
   
12. <span data-ttu-id="bf0b2-196">Haga clic en hello **seguridad** ficha.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-196">Click hello **Security** tab.</span></span>
    
    <span data-ttu-id="bf0b2-197">![Editar información de la compañía](./media/active-directory-saas-onit-tutorial/IC791176.png "Editar información de la compañía")</span><span class="sxs-lookup"><span data-stu-id="bf0b2-197">![Edit Company Information](./media/active-directory-saas-onit-tutorial/IC791176.png "Edit Company Information")</span></span>

13. <span data-ttu-id="bf0b2-198">En hello **seguridad** , realice los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="bf0b2-198">On hello **Security** tab, perform hello following steps:</span></span>

    <span data-ttu-id="bf0b2-199">![Inicio de sesión único](./media/active-directory-saas-onit-tutorial/IC791177.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="bf0b2-199">![Single Sign-On](./media/active-directory-saas-onit-tutorial/IC791177.png "Single Sign-On")</span></span>

    <span data-ttu-id="bf0b2-200">a.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-200">a.</span></span> <span data-ttu-id="bf0b2-201">Como **Estrategia de autenticación**, seleccione **Inicio de sesión único y contraseña**.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-201">As **Authentication Strategy**, select **Single Sign On and Password**.</span></span>
    
    <span data-ttu-id="bf0b2-202">b.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-202">b.</span></span> <span data-ttu-id="bf0b2-203">En **Idp Target URL** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-203">In **Idp Target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bf0b2-204">c.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-204">c.</span></span> <span data-ttu-id="bf0b2-205">En **Idp logout URL** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-205">In **Idp logout URL** textbox, paste hello value of  **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bf0b2-206">d.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-206">d.</span></span> <span data-ttu-id="bf0b2-207">En **Idp Cert Fingerprint (SHA1)** cuadro de texto, pegue hello **huella digital** valor de certificado en el que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-207">In **Idp Cert Fingerprint (SHA1)** textbox, paste hello  **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="bf0b2-208">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="bf0b2-208">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bf0b2-209">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-209">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bf0b2-210">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bf0b2-210">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bf0b2-211">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf0b2-211">Create an Azure AD test user</span></span>

<span data-ttu-id="bf0b2-212">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-212">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="bf0b2-214">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bf0b2-214">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf0b2-215">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-215">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-onit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="bf0b2-217">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-217">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-onit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="bf0b2-219">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-219">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-onit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="bf0b2-221">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="bf0b2-221">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-onit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="bf0b2-223">a.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-223">a.</span></span> <span data-ttu-id="bf0b2-224">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-224">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bf0b2-225">b.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-225">b.</span></span> <span data-ttu-id="bf0b2-226">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-226">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="bf0b2-227">c.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-227">c.</span></span> <span data-ttu-id="bf0b2-228">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-228">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="bf0b2-229">d.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-229">d.</span></span> <span data-ttu-id="bf0b2-230">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-230">Click **Create**.</span></span>
 
### <a name="create-an-onit-test-user"></a><span data-ttu-id="bf0b2-231">Creación de un usuario de prueba de Onit</span><span class="sxs-lookup"><span data-stu-id="bf0b2-231">Create an Onit test user</span></span>

<span data-ttu-id="bf0b2-232">En orden tooenable toolog de los usuarios de Azure AD en Onit, se les deben aprovisionar en Onit.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-232">In order tooenable Azure AD users toolog into Onit, they must be provisioned into Onit.</span></span>  

<span data-ttu-id="bf0b2-233">En caso de hello de Onit, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-233">In hello case of Onit, provisioning is a manual task.</span></span>

<span data-ttu-id="bf0b2-234">**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bf0b2-234">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf0b2-235">Inicio de sesión tooyour **Onit** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-235">Sign on tooyour **Onit** company site as an administrator.</span></span>
2. <span data-ttu-id="bf0b2-236">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-236">Click **Add User**.</span></span>
   
   <span data-ttu-id="bf0b2-237">![Administración](./media/active-directory-saas-onit-tutorial/IC791180.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="bf0b2-237">![Administration](./media/active-directory-saas-onit-tutorial/IC791180.png "Administration")</span></span>
3. <span data-ttu-id="bf0b2-238">En hello **Agregar usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="bf0b2-238">On hello **Add User** dialog page, perform hello following steps:</span></span>
   
   <span data-ttu-id="bf0b2-239">![Agregar usuario](./media/active-directory-saas-onit-tutorial/IC791181.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="bf0b2-239">![Add User](./media/active-directory-saas-onit-tutorial/IC791181.png "Add User")</span></span>
   
  1. <span data-ttu-id="bf0b2-240">Hola de tipo **nombre** hello y **dirección de correo electrónico** de un Azure válida cuadros de texto relacionados con la cuenta de AD que quiera tooprovision en Hola.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-240">Type hello **Name** and hello **Email Address** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span>
  2. <span data-ttu-id="bf0b2-241">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-241">Click **Create**.</span></span>    
   
 > [!NOTE]
 > <span data-ttu-id="bf0b2-242">titular de la cuenta de Hello Azure Active Directory recibe un correo electrónico y sigue un vínculo tooconfirm su cuenta antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-242">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="bf0b2-243">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf0b2-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="bf0b2-244">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooOnit.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOnit.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="bf0b2-246">**tooassign Britta Simon tooOnit, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bf0b2-246">**tooassign Britta Simon tooOnit, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf0b2-247">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="bf0b2-249">En la lista de aplicaciones de hello, seleccione **Onit**.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-249">In hello applications list, select **Onit**.</span></span>

    ![vínculo de Onit Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-onit-tutorial/tutorial_onit_app.png)  

3. <span data-ttu-id="bf0b2-251">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="bf0b2-253">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-253">Click **Add** button.</span></span> <span data-ttu-id="bf0b2-254">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="bf0b2-256">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bf0b2-257">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bf0b2-258">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bf0b2-259">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="bf0b2-259">Test single sign-on</span></span>

<span data-ttu-id="bf0b2-260">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bf0b2-261">Al hacer clic en icono de Onit Hola Hola Panel de acceso, deberá obtener la aplicación de Onit tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-261">When you click hello Onit tile in hello Access Panel, you should get automatically signed-on tooyour Onit application.</span></span>
<span data-ttu-id="bf0b2-262">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bf0b2-262">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bf0b2-263">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="bf0b2-263">Additional resources</span></span>

* [<span data-ttu-id="bf0b2-264">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bf0b2-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bf0b2-265">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bf0b2-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-onit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-onit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-onit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-onit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-onit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-onit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-onit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-onit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-onit-tutorial/tutorial_general_203.png

