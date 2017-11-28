---
title: "Tutorial: Integración de Azure Active Directory con Amazon Web Services (AWS) | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Amazon Web Services (AWS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="27b2d-103">Tutorial: integración de Azure Active Directory con Amazon Web Service (AWS)</span><span class="sxs-lookup"><span data-stu-id="27b2d-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="27b2d-104">En este tutorial, aprenderá cómo toointegrate Amazon Web Services (AWS) con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="27b2d-104">In this tutorial, you learn how toointegrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="27b2d-105">Integración de Amazon Web Services (AWS) con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="27b2d-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="27b2d-106">Puede controlar en Azure AD que tenga acceso tooAmazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="27b2d-106">You can control in Azure AD who has access tooAmazon Web Services (AWS)</span></span>
- <span data-ttu-id="27b2d-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAmazon Web Services (AWS) (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27b2d-107">You can enable your users tooautomatically get signed-on tooAmazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="27b2d-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="27b2d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="27b2d-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="27b2d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="27b2d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="27b2d-110">Prerequisites</span></span>

<span data-ttu-id="27b2d-111">tooconfigure integración de Azure AD con Amazon Web Services (AWS), necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="27b2d-111">tooconfigure Azure AD integration with Amazon Web Services (AWS), you need hello following items:</span></span>

- <span data-ttu-id="27b2d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27b2d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="27b2d-113">Suscripción habilitada para el inicio de sesión único en Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="27b2d-113">Amazon Web Services (AWS) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="27b2d-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="27b2d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="27b2d-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="27b2d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="27b2d-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="27b2d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="27b2d-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="27b2d-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="27b2d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="27b2d-118">Scenario description</span></span>
<span data-ttu-id="27b2d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="27b2d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="27b2d-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="27b2d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="27b2d-121">Adición de Amazon Web Services (AWS) desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="27b2d-121">Adding Amazon Web Services (AWS) from hello gallery</span></span>
2. <span data-ttu-id="27b2d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27b2d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a><span data-ttu-id="27b2d-123">Adición de Amazon Web Services (AWS) desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="27b2d-123">Adding Amazon Web Services (AWS) from hello gallery</span></span>
<span data-ttu-id="27b2d-124">integración de hello tooconfigure de Amazon Web Services (AWS) en Azure AD, deberá tooadd Amazon Web Services (AWS) de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="27b2d-124">tooconfigure hello integration of Amazon Web Services (AWS) into Azure AD, you need tooadd Amazon Web Services (AWS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="27b2d-125">**tooadd Amazon Web Services (AWS) desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="27b2d-125">**tooadd Amazon Web Services (AWS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="27b2d-126">Hola  **[Portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="27b2d-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="27b2d-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="27b2d-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="27b2d-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="27b2d-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="27b2d-133">En el cuadro de búsqueda de hello, escriba **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-133">In hello search box, type **Amazon Web Services (AWS)**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. <span data-ttu-id="27b2d-135">En el panel de resultados de hello, seleccione **Amazon Web Services (AWS)**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="27b2d-135">In hello results panel, select **Amazon Web Services (AWS)**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="27b2d-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27b2d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="27b2d-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Amazon Web Services (AWS) con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="27b2d-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="27b2d-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Amazon Web Services (AWS) es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="27b2d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Amazon Web Services (AWS) is tooa user in Azure AD.</span></span> <span data-ttu-id="27b2d-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Amazon Web Services (AWS) debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="27b2d-140">In other words, a link relationship between an Azure AD user and hello related user in Amazon Web Services (AWS) needs toobe established.</span></span>

<span data-ttu-id="27b2d-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="27b2d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="27b2d-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Amazon Web Services (AWS), deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="27b2d-142">tooconfigure and test Azure AD single sign-on with Amazon Web Services (AWS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="27b2d-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="27b2d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="27b2d-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="27b2d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="27b2d-145">**[Creación de un usuario de prueba de Amazon Web Services](#creating-an-amazon-web-services-test-user)**  -toohave un equivalente de Britta Simon en Amazon Web Services (AWS) que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="27b2d-145">**[Creating an Amazon Web Services test user](#creating-an-amazon-web-services-test-user)** - toohave a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="27b2d-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="27b2d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="27b2d-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="27b2d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="27b2d-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27b2d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="27b2d-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="27b2d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="27b2d-150">**tooconfigure inicio de sesión único en Azure AD con Amazon Web Services (AWS), lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="27b2d-150">**tooconfigure Azure AD single sign-on with Amazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="27b2d-151">Hola Portal de Azure, en hello **Amazon Web Services (AWS)** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-151">In hello Azure Portal, on hello **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="27b2d-153">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="27b2d-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. <span data-ttu-id="27b2d-155">En hello **Amazon Web Services (AWS) dominio y las direcciones URL** sección, hello usuario no tiene tooperform todos los pasos tal y como aplicación hello ya está integrado previamente con Azure.</span><span class="sxs-lookup"><span data-stu-id="27b2d-155">On hello **Amazon Web Services (AWS) Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. <span data-ttu-id="27b2d-157">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="27b2d-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. <span data-ttu-id="27b2d-159">Hola aplicación de Software de Amazon Web Services (AWS) espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="27b2d-159">hello Amazon Web Services (AWS) Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="27b2d-160">Configure Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="27b2d-160">Please configure hello following claims for this application.</span></span> <span data-ttu-id="27b2d-161">Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="27b2d-161">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="27b2d-162">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="27b2d-162">hello following screenshot shows an example for this.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. <span data-ttu-id="27b2d-164">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de hello anterior y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="27b2d-164">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="27b2d-165">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="27b2d-165">Attribute Name</span></span>  | <span data-ttu-id="27b2d-166">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="27b2d-166">Attribute Value</span></span> | <span data-ttu-id="27b2d-167">Espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="27b2d-167">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="27b2d-168">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="27b2d-168">RoleSessionName</span></span> | <span data-ttu-id="27b2d-169">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="27b2d-169">user.userprincipalname</span></span> | <span data-ttu-id="27b2d-170">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="27b2d-170">https://aws.amazon.com/SAML/Attributes</span></span> |
    | <span data-ttu-id="27b2d-171">Rol</span><span class="sxs-lookup"><span data-stu-id="27b2d-171">Role</span></span>            | <span data-ttu-id="27b2d-172">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="27b2d-172">user.assignedroles</span></span> |  <span data-ttu-id="27b2d-173">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="27b2d-173">https://aws.amazon.com/SAML/Attributes</span></span> |
    
    >[!TIP]
    ><span data-ttu-id="27b2d-174">Necesita tooconfigure Hola aprovisionamiento de usuarios en Azure AD toofetch todos los roles de Hola desde la consola de AWS.</span><span class="sxs-lookup"><span data-stu-id="27b2d-174">You need tooconfigure hello user provisioning in Azure AD toofetch all hello roles from AWS Console.</span></span> <span data-ttu-id="27b2d-175">Consulte Hola pasos de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="27b2d-175">Please refer hello provisioning steps below.</span></span>

    <span data-ttu-id="27b2d-176">a.</span><span class="sxs-lookup"><span data-stu-id="27b2d-176">a.</span></span> <span data-ttu-id="27b2d-177">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27b2d-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="27b2d-179">b.</span><span class="sxs-lookup"><span data-stu-id="27b2d-179">b.</span></span> <span data-ttu-id="27b2d-180">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="27b2d-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="27b2d-182">c.</span><span class="sxs-lookup"><span data-stu-id="27b2d-182">c.</span></span> <span data-ttu-id="27b2d-183">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="27b2d-183">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="27b2d-184">Agregue el valor de Namespace de hello tal como se indica anteriormente.</span><span class="sxs-lookup"><span data-stu-id="27b2d-184">Add hello Namespace value as given above.</span></span>
    
    <span data-ttu-id="27b2d-185">d.</span><span class="sxs-lookup"><span data-stu-id="27b2d-185">d.</span></span> <span data-ttu-id="27b2d-186">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-186">Click **Ok**.</span></span>

7. <span data-ttu-id="27b2d-187">Haga clic en **guardar** botón Configuración de hello toosave en Azure.</span><span class="sxs-lookup"><span data-stu-id="27b2d-187">Click **Save** button toosave hello settings on Azure.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="27b2d-189">En otra ventana del explorador, sitio de empresa de Amazon Web Services (AWS) tooyour de inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="27b2d-189">In a different browser window, sign-on tooyour Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="27b2d-190">Haga clic en **Página principal de la consola**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-190">Click **Console Home**.</span></span>
   
    ![Configurar inicio de sesión único][11]

10. <span data-ttu-id="27b2d-192">Haga clic en **IAM** en el servicio **Security, Identity & Compliance** (Seguridad, identidad y cumplimiento).</span><span class="sxs-lookup"><span data-stu-id="27b2d-192">Click **IAM** from **Security, Identity & Compliance** service.</span></span>
   
    ![Configurar inicio de sesión único][12]

11. <span data-ttu-id="27b2d-194">Haga clic en **Proveedores de identidades** y, después, en **Create Provider** (Crear proveedor).</span><span class="sxs-lookup"><span data-stu-id="27b2d-194">Click **Identity Providers**, and then click **Create Provider**.</span></span>
   
    ![Configurar inicio de sesión único][13]

12. <span data-ttu-id="27b2d-196">En hello **Configurar proveedor** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="27b2d-196">On hello **Configure Provider** dialog page, perform hello following steps:</span></span>
   
    ![Configurar inicio de sesión único][14]
 
    <span data-ttu-id="27b2d-198">a.</span><span class="sxs-lookup"><span data-stu-id="27b2d-198">a.</span></span> <span data-ttu-id="27b2d-199">En **Tipo de proveedor**, seleccione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-199">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="27b2d-200">b.</span><span class="sxs-lookup"><span data-stu-id="27b2d-200">b.</span></span> <span data-ttu-id="27b2d-201">Hola **nombre de proveedor** cuadro de texto, escriba un nombre de proveedor (p. ej.: *WAAD*).</span><span class="sxs-lookup"><span data-stu-id="27b2d-201">In hello **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>

    <span data-ttu-id="27b2d-202">c.</span><span class="sxs-lookup"><span data-stu-id="27b2d-202">c.</span></span> <span data-ttu-id="27b2d-203">tooupload el archivo de metadatos descargado, haga clic en **Elegir archivo**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-203">tooupload your downloaded metadata file, click **Choose File**.</span></span>

    <span data-ttu-id="27b2d-204">d.</span><span class="sxs-lookup"><span data-stu-id="27b2d-204">d.</span></span> <span data-ttu-id="27b2d-205">Haga clic en **Siguiente paso**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-205">Click **Next Step**.</span></span>

13. <span data-ttu-id="27b2d-206">En hello **Compruebe la información de proveedor** página del cuadro de diálogo, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-206">On hello **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![Configurar inicio de sesión único][15]

14. <span data-ttu-id="27b2d-208">Haga clic en **Roles** y, después, en **Crear nuevo rol**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-208">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![Configurar inicio de sesión único][16]

15. <span data-ttu-id="27b2d-210">En hello **establecer el nombre de rol** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="27b2d-210">On hello **Set Role Name** dialog, perform hello following steps:</span></span> 
    
    ![Configurar inicio de sesión único][17] 

    <span data-ttu-id="27b2d-212">a.</span><span class="sxs-lookup"><span data-stu-id="27b2d-212">a.</span></span> <span data-ttu-id="27b2d-213">Hola **nombre de la función** cuadro de texto, escriba un nombre de rol (p. ej.: *TestUser*).</span><span class="sxs-lookup"><span data-stu-id="27b2d-213">In hello **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 

    <span data-ttu-id="27b2d-214">b.</span><span class="sxs-lookup"><span data-stu-id="27b2d-214">b.</span></span> <span data-ttu-id="27b2d-215">Haga clic en **Siguiente paso**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-215">Click **Next Step**.</span></span>

16. <span data-ttu-id="27b2d-216">En hello **Seleccionar tipo de rol** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="27b2d-216">On hello **Select Role Type** dialog, perform hello following steps:</span></span> 
    
    ![Configurar inicio de sesión único][18] 

    <span data-ttu-id="27b2d-218">a.</span><span class="sxs-lookup"><span data-stu-id="27b2d-218">a.</span></span> <span data-ttu-id="27b2d-219">Seleccione **Rol de acceso del proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-219">Select **Role For Identity Provider Access**.</span></span> 

    <span data-ttu-id="27b2d-220">b.</span><span class="sxs-lookup"><span data-stu-id="27b2d-220">b.</span></span> <span data-ttu-id="27b2d-221">Hola **Grant Web Single Sign-On (WebSSO) tooSAML proveedores de acceso a** sección, haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-221">In hello **Grant Web Single Sign-On (WebSSO) access tooSAML providers** section, click **Select**.</span></span>

17. <span data-ttu-id="27b2d-222">En hello **establecer confianza** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="27b2d-222">On hello **Establish Trust** dialog, perform hello following steps:</span></span>  
    
    ![Configurar inicio de sesión único][19] 

    <span data-ttu-id="27b2d-224">a.</span><span class="sxs-lookup"><span data-stu-id="27b2d-224">a.</span></span> <span data-ttu-id="27b2d-225">Como proveedor SAML, seleccione el proveedor SAML de Hola que haya creado previamente (p. ej.: *WAAD*)</span><span class="sxs-lookup"><span data-stu-id="27b2d-225">As SAML provider, select hello SAML provider you have created previously (e.g.: *WAAD*)</span></span>
  
    <span data-ttu-id="27b2d-226">b.</span><span class="sxs-lookup"><span data-stu-id="27b2d-226">b.</span></span> <span data-ttu-id="27b2d-227">Haga clic en **Siguiente paso**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-227">Click **Next Step**.</span></span>

18. <span data-ttu-id="27b2d-228">En hello **comprobar confiar en rol** cuadro de diálogo, haga clic en **siguiente paso**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-228">On hello **Verify Role Trust** dialog, click **Next Step**.</span></span>
    
    ![Configurar inicio de sesión único][32]

19. <span data-ttu-id="27b2d-230">En hello **asociar directiva** cuadro de diálogo, haga clic en **siguiente paso**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-230">On hello **Attach Policy** dialog, click **Next Step**.</span></span>
    
    ![Configurar inicio de sesión único][33]

20. <span data-ttu-id="27b2d-232">En hello **revisión** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="27b2d-232">On hello **Review** dialog, perform hello following steps:</span></span>
    
    ![Configurar inicio de sesión único][34]
 
    <span data-ttu-id="27b2d-234">a.</span><span class="sxs-lookup"><span data-stu-id="27b2d-234">a.</span></span> <span data-ttu-id="27b2d-235">Haga clic en **Crear rol**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-235">Click **Create Role**.</span></span>

    <span data-ttu-id="27b2d-236">b.</span><span class="sxs-lookup"><span data-stu-id="27b2d-236">b.</span></span> <span data-ttu-id="27b2d-237">Cree tantos roles según sea necesario y asignarlos toohello proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="27b2d-237">Create as many roles as needed and map them toohello Identity Provider.</span></span>

21. <span data-ttu-id="27b2d-238">Configurar todos los roles de Hola de AWS toofetch el aprovisionamiento de usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="27b2d-238">Now configure hello user provisioning toofetch all hello roles from AWS</span></span>

    <span data-ttu-id="27b2d-239">a.</span><span class="sxs-lookup"><span data-stu-id="27b2d-239">a.</span></span> <span data-ttu-id="27b2d-240">En el inicio de sesión de consola de AWS de Hola con la cuenta raíz</span><span class="sxs-lookup"><span data-stu-id="27b2d-240">In hello AWS Console login with your root account</span></span>

    <span data-ttu-id="27b2d-241">b.</span><span class="sxs-lookup"><span data-stu-id="27b2d-241">b.</span></span> <span data-ttu-id="27b2d-242">En hello esquina superior derecha, haga clic en su nombre y, a continuación, haga clic en hello **mis credenciales de seguridad** opción.</span><span class="sxs-lookup"><span data-stu-id="27b2d-242">In hello top right corner click your name and then click hello **My Security Credentials** option.</span></span> <span data-ttu-id="27b2d-243">Se abrirá una pantalla como un mensaje de advertencia.</span><span class="sxs-lookup"><span data-stu-id="27b2d-243">This will open up a screen as a warning message.</span></span> <span data-ttu-id="27b2d-244">Haga clic en el botón de hello **las credenciales de seguridad** toopass botón Hola pantalla.</span><span class="sxs-lookup"><span data-stu-id="27b2d-244">Click hello button **Security Credentials** button toopass hello screen.</span></span>
        
       ![Configurar inicio de sesión único][36]

       ![Configurar inicio de sesión único][37]

    <span data-ttu-id="27b2d-247">c.</span><span class="sxs-lookup"><span data-stu-id="27b2d-247">c.</span></span> <span data-ttu-id="27b2d-248">Hola claves de acceso de sección, haga clic en hello **crear una nueva clave de acceso** botón.</span><span class="sxs-lookup"><span data-stu-id="27b2d-248">In hello Access Keys section click hello **Create New Access Key** button.</span></span> <span data-ttu-id="27b2d-249">Esto genera hello Id. de clave de acceso y un valor de token.</span><span class="sxs-lookup"><span data-stu-id="27b2d-249">This generates hello Access Key ID and a token value.</span></span>
    
       ![Configurar inicio de sesión único][38]

    <span data-ttu-id="27b2d-251">d.</span><span class="sxs-lookup"><span data-stu-id="27b2d-251">d.</span></span> <span data-ttu-id="27b2d-252">Copie estos dos valores y descárguelos para no perderlos.</span><span class="sxs-lookup"><span data-stu-id="27b2d-252">Copy both these values and also download it, so that you don't lose it.</span></span>

    <span data-ttu-id="27b2d-253">e.</span><span class="sxs-lookup"><span data-stu-id="27b2d-253">e.</span></span> <span data-ttu-id="27b2d-254">Hola Portal de Azure, en la página de integración de aplicaciones de Amazon Web Services (AWS) hello, haga clic en **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-254">In hello Azure Portal, on hello Amazon Web Services (AWS) application integration page, click **Provisioning**.</span></span>
        
       ![Configurar inicio de sesión único][35]

    <span data-ttu-id="27b2d-256">f.</span><span class="sxs-lookup"><span data-stu-id="27b2d-256">f.</span></span> <span data-ttu-id="27b2d-257">Establecer el modo de aprovisionamiento de hello demasiado**automática**</span><span class="sxs-lookup"><span data-stu-id="27b2d-257">Set hello Provisioning mode too**Automatic**</span></span>
        
       ![Configurar inicio de sesión único][39]

    <span data-ttu-id="27b2d-259">g.</span><span class="sxs-lookup"><span data-stu-id="27b2d-259">g.</span></span> <span data-ttu-id="27b2d-260">Ahora en hello **clientsecret** y **secreto Token** pegue los valores correspondientes de hello, que han copiado desde la consola de AWS.</span><span class="sxs-lookup"><span data-stu-id="27b2d-260">Now in hello **clientsecret** and **Secret Token** paste hello corresponding values, which you have copied from AWS Console.</span></span>
    
    <span data-ttu-id="27b2d-261">h.</span><span class="sxs-lookup"><span data-stu-id="27b2d-261">h.</span></span> <span data-ttu-id="27b2d-262">Puede hacer clic en hello **Probar conexión** botón conectividad de hello tootest.</span><span class="sxs-lookup"><span data-stu-id="27b2d-262">You can click hello **Test Connection** button tootest hello connectivity.</span></span> <span data-ttu-id="27b2d-263">Una vez que es correcta, a continuación, puede empezar a Hola aprovisionamiento conector.</span><span class="sxs-lookup"><span data-stu-id="27b2d-263">Once that is successful then you can start hello provisioning connector.</span></span>
       
       ![Configurar inicio de sesión único][40]

    <span data-ttu-id="27b2d-265">i.</span><span class="sxs-lookup"><span data-stu-id="27b2d-265">i.</span></span> <span data-ttu-id="27b2d-266">Ahora habilitar Hola estado de aprovisionamiento demasiado**en**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-266">Now enable hello Provisioning Status too**On**.</span></span> <span data-ttu-id="27b2d-267">Esto inicia capturar roles Hola de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="27b2d-267">This starts fetching hello roles from hello application.</span></span>

       ![Configurar inicio de sesión único][41]

    > [!NOTE]
    > <span data-ttu-id="27b2d-269">Azure se ejecuta el servicio AD aprovisionamiento cada después de algunos roles de hello toosync de tiempo de AWS.</span><span class="sxs-lookup"><span data-stu-id="27b2d-269">Azure AD Provisioning service runs every after some time toosync hello roles from AWS.</span></span> <span data-ttu-id="27b2d-270">Debería ver Hola todos los proveedor de identidades adjunta roles AWS en Azure AD y se puede utilizar al asignar Hola aplicación toousers o grupos.</span><span class="sxs-lookup"><span data-stu-id="27b2d-270">You should see all hello Identity Provider attached AWS roles into Azure AD and you can use them while assigning hello application toousers or groups.</span></span>

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="27b2d-271">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="27b2d-271">Creating an Azure AD test user</span></span>
<span data-ttu-id="27b2d-272">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="27b2d-272">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="27b2d-274">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="27b2d-274">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="27b2d-275">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="27b2d-275">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="27b2d-277">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="27b2d-277">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="27b2d-279">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27b2d-279">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="27b2d-281">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="27b2d-281">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="27b2d-283">a.</span><span class="sxs-lookup"><span data-stu-id="27b2d-283">a.</span></span> <span data-ttu-id="27b2d-284">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-284">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="27b2d-285">b.</span><span class="sxs-lookup"><span data-stu-id="27b2d-285">b.</span></span> <span data-ttu-id="27b2d-286">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="27b2d-286">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="27b2d-287">c.</span><span class="sxs-lookup"><span data-stu-id="27b2d-287">c.</span></span> <span data-ttu-id="27b2d-288">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-288">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="27b2d-289">d.</span><span class="sxs-lookup"><span data-stu-id="27b2d-289">d.</span></span> <span data-ttu-id="27b2d-290">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-290">Click **Create**.</span></span>
 
### <a name="creating-an-amazon-web-services-test-user"></a><span data-ttu-id="27b2d-291">Creación de un usuario de prueba de Amazon Web Services</span><span class="sxs-lookup"><span data-stu-id="27b2d-291">Creating an Amazon Web Services test user</span></span>

<span data-ttu-id="27b2d-292">En orden tooenable toolog de los usuarios de Azure AD en tooAmazon Web Services (AWS), se les deben aprovisionar en Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="27b2d-292">In order tooenable Azure AD users toolog in tooAmazon Web Services (AWS), they must be provisioned into Amazon Web Services (AWS).</span></span> <span data-ttu-id="27b2d-293">En caso de hello de Amazon Web Services (AWS), el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="27b2d-293">In hello case of Amazon Web Services (AWS), provisioning is a manual task.</span></span>

<span data-ttu-id="27b2d-294">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="27b2d-294">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="27b2d-295">Inicie sesión en tooyour **Amazon Web Services (AWS)** como administrador.</span><span class="sxs-lookup"><span data-stu-id="27b2d-295">Log in tooyour **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="27b2d-296">Haga clic en hello **inicial de la consola** icono.</span><span class="sxs-lookup"><span data-stu-id="27b2d-296">Click hello **Console Home** icon.</span></span> 
   
    ![Configurar inicio de sesión único][11]

3. <span data-ttu-id="27b2d-298">Haga clic en Administración de identidades y acceso.</span><span class="sxs-lookup"><span data-stu-id="27b2d-298">Click Identity and Access Management.</span></span> 
   
    ![Configurar inicio de sesión único][28]

4. <span data-ttu-id="27b2d-300">Hola panel, haga clic en **usuarios**y, a continuación, haga clic en **crear nuevos usuarios**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-300">In hello Dashboard, click **Users**, and then click **Create New Users**.</span></span> 
   
    ![Configurar inicio de sesión único][29]

5. <span data-ttu-id="27b2d-302">En el cuadro de diálogo de hello Create User, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="27b2d-302">On hello Create User dialog, perform hello following steps:</span></span> 
   
    ![Configurar inicio de sesión único][30]   
    
    <span data-ttu-id="27b2d-304">a.</span><span class="sxs-lookup"><span data-stu-id="27b2d-304">a.</span></span> <span data-ttu-id="27b2d-305">Hola **escriba los nombres de usuario** cuadros de texto, escriba el nombre de usuario de Brita Simon (userprincipalname) en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="27b2d-305">In hello **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span>

    <span data-ttu-id="27b2d-306">b.</span><span class="sxs-lookup"><span data-stu-id="27b2d-306">b.</span></span> <span data-ttu-id="27b2d-307">Haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="27b2d-307">Click **Create.**</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="27b2d-308">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="27b2d-308">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="27b2d-309">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooAmazon de acceso Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="27b2d-309">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAmazon Web Services (AWS).</span></span>

![Asignar usuario][200] 

<span data-ttu-id="27b2d-311">**tooassign Britta Simon tooAmazon Web Services (AWS), lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="27b2d-311">**tooassign Britta Simon tooAmazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="27b2d-312">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-312">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="27b2d-314">En la lista de aplicaciones de hello, seleccione **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-314">In hello applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. <span data-ttu-id="27b2d-316">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-316">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="27b2d-318">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-318">Click **Add** button.</span></span> <span data-ttu-id="27b2d-319">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-319">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="27b2d-321">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="27b2d-321">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="27b2d-322">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-322">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="27b2d-323">En **Seleccionar rol** ficha, seleccione Hola un rol adecuado para el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="27b2d-323">On **Select Role** tab, select hello appropriate role for hello user.</span></span> <span data-ttu-id="27b2d-324">Todas estas funciones se muestran con el nombre de la función de Hola y el nombre del proveedor de identidad.</span><span class="sxs-lookup"><span data-stu-id="27b2d-324">All these roles are shown with hello role name and identity provider name.</span></span> <span data-ttu-id="27b2d-325">De esta forma que puede identificar fácilmente los roles de Hola de AWS.</span><span class="sxs-lookup"><span data-stu-id="27b2d-325">This way you can easily identify hello roles from AWS.</span></span>

8. <span data-ttu-id="27b2d-326">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="27b2d-326">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="27b2d-327">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="27b2d-327">Testing single sign-on</span></span>

<span data-ttu-id="27b2d-328">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="27b2d-328">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="27b2d-329">Al hacer clic en hello Amazon Web Services (AWS) el icono Panel de acceso de hello, deberá obtener tooyour automáticamente firmado en aplicaciones de Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="27b2d-329">When you click hello Amazon Web Services (AWS) tile in hello Access Panel, you should get automatically signed-on tooyour Amazon Web Services (AWS) application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="27b2d-330">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="27b2d-330">Additional resources</span></span>

* [<span data-ttu-id="27b2d-331">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="27b2d-331">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="27b2d-332">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="27b2d-332">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
