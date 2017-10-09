---
title: "Tutorial: integración de Azure Active Directory con Allocadia | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Allocadia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c415fc55-6dc1-49f2-a8a2-2fc6e3790d65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: jeedes
ms.openlocfilehash: 9a01c232f9dc50e690dd348430899db9c13f1564
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-allocadia"></a><span data-ttu-id="37101-103">Tutorial: Integración de Azure Active Directory con Allocadia</span><span class="sxs-lookup"><span data-stu-id="37101-103">Tutorial: Azure Active Directory integration with Allocadia</span></span>

<span data-ttu-id="37101-104">En este tutorial, aprenderá cómo toointegrate Allocadia con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37101-104">In this tutorial, you learn how toointegrate Allocadia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="37101-105">Integración Allocadia con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="37101-105">Integrating Allocadia with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="37101-106">Puede controlar en Azure AD que tenga acceso tooAllocadia</span><span class="sxs-lookup"><span data-stu-id="37101-106">You can control in Azure AD who has access tooAllocadia</span></span>
- <span data-ttu-id="37101-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAllocadia (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="37101-107">You can enable your users tooautomatically get signed-on tooAllocadia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="37101-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="37101-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="37101-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="37101-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37101-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="37101-110">Prerequisites</span></span>

<span data-ttu-id="37101-111">integración de Azure AD con Allocadia tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="37101-111">tooconfigure Azure AD integration with Allocadia, you need hello following items:</span></span>

- <span data-ttu-id="37101-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="37101-112">An Azure AD subscription</span></span>
- <span data-ttu-id="37101-113">Una suscripción habilitada para el inicio de sesión único en Allocadia</span><span class="sxs-lookup"><span data-stu-id="37101-113">An Allocadia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="37101-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="37101-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="37101-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="37101-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="37101-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="37101-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="37101-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37101-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="37101-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="37101-118">Scenario description</span></span>
<span data-ttu-id="37101-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="37101-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="37101-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="37101-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="37101-121">Agregar Allocadia desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="37101-121">Adding Allocadia from hello gallery</span></span>
2. <span data-ttu-id="37101-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="37101-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-allocadia-from-hello-gallery"></a><span data-ttu-id="37101-123">Agregar Allocadia desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="37101-123">Adding Allocadia from hello gallery</span></span>
<span data-ttu-id="37101-124">integración de hello tooconfigure de Allocadia en Azure AD, deberá tooadd Allocadia de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="37101-124">tooconfigure hello integration of Allocadia into Azure AD, you need tooadd Allocadia from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="37101-125">**tooadd Allocadia de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="37101-125">**tooadd Allocadia from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="37101-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="37101-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="37101-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="37101-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="37101-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="37101-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="37101-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="37101-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="37101-133">En el cuadro de búsqueda de hello, escriba **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="37101-133">In hello search box, type **Allocadia**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_search.png)

5. <span data-ttu-id="37101-135">En el panel de resultados de hello, seleccione **Allocadia**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="37101-135">In hello results panel, select **Allocadia**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="37101-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="37101-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="37101-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Allocadia con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="37101-138">In this section, you configure and test Azure AD single sign-on with Allocadia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="37101-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Allocadia es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37101-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Allocadia is tooa user in Azure AD.</span></span> <span data-ttu-id="37101-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Allocadia debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="37101-140">In other words, a link relationship between an Azure AD user and hello related user in Allocadia needs toobe established.</span></span>

<span data-ttu-id="37101-141">En Allocadia, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="37101-141">In Allocadia, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="37101-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Allocadia, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="37101-142">tooconfigure and test Azure AD single sign-on with Allocadia, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="37101-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="37101-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="37101-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37101-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="37101-145">**[Creación de un usuario de prueba Allocadia](#creating-an-allocadia-test-user)**  -toohave un equivalente de Britta Simon en Allocadia que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="37101-145">**[Creating an Allocadia test user](#creating-an-allocadia-test-user)** - toohave a counterpart of Britta Simon in Allocadia that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="37101-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="37101-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="37101-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="37101-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="37101-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="37101-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="37101-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Allocadia.</span><span class="sxs-lookup"><span data-stu-id="37101-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Allocadia application.</span></span>

<span data-ttu-id="37101-150">**inicio de sesión único en Azure AD tooconfigure con Allocadia, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="37101-150">**tooconfigure Azure AD single sign-on with Allocadia, perform hello following steps:**</span></span>

1. <span data-ttu-id="37101-151">En el portal de Azure, en Hola Hola **Allocadia** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="37101-151">In hello Azure portal, on hello **Allocadia** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="37101-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="37101-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_samlbase.png)

3. <span data-ttu-id="37101-155">En hello **Allocadia dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="37101-155">On hello **Allocadia Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_url.png)

    <span data-ttu-id="37101-157">a.</span><span class="sxs-lookup"><span data-stu-id="37101-157">a.</span></span> <span data-ttu-id="37101-158">Hola **identificador** cuadro de texto, escriba una dirección URL con hello siguiendo patrones:</span><span class="sxs-lookup"><span data-stu-id="37101-158">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
       
     <span data-ttu-id="37101-159">Para el entorno de prueba - `https://na2standby.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="37101-159">For test environment -  `https://na2standby.allocadia.com`</span></span>
    
     <span data-ttu-id="37101-160">Para el entorno de producción - `https://na2.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="37101-160">For production environment - `https://na2.allocadia.com`</span></span>

    <span data-ttu-id="37101-161">b.</span><span class="sxs-lookup"><span data-stu-id="37101-161">b.</span></span> <span data-ttu-id="37101-162">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL con hello siguiendo patrones:</span><span class="sxs-lookup"><span data-stu-id="37101-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    
     <span data-ttu-id="37101-163">Para el entorno de prueba - `https://na2standby.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="37101-163">For test environment - `https://na2standby.allocadia.com/allocadia/saml/SSO`</span></span>
    
     <span data-ttu-id="37101-164">Para el entorno de producción - `https://na2.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="37101-164">For production environment - `https://na2.allocadia.com/allocadia/saml/SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="37101-165">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="37101-165">These values are not real.</span></span> <span data-ttu-id="37101-166">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="37101-166">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="37101-167">Póngase en contacto con [equipo de soporte técnico de Allocadia](mailTo:support@allocadia.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="37101-167">Contact [Allocadia support team](mailTo:support@allocadia.com) tooget these values.</span></span>

4. <span data-ttu-id="37101-168">Aplicación de Allocadia espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="37101-168">Allocadia application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="37101-169">Configurar Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="37101-169">Configure hello following claims for this application.</span></span> <span data-ttu-id="37101-170">Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="37101-170">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="37101-171">Hola siguiente captura de pantalla muestra un ejemplo de esta configuración.</span><span class="sxs-lookup"><span data-stu-id="37101-171">hello following screenshot shows an example for this configuration.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_attributes.png)
    
5. <span data-ttu-id="37101-173">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de Hola y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="37101-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="37101-174">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="37101-174">Attribute Name</span></span> | <span data-ttu-id="37101-175">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="37101-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="37101-176">firstname</span><span class="sxs-lookup"><span data-stu-id="37101-176">firstname</span></span> | <span data-ttu-id="37101-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="37101-177">user.givenname</span></span> |
    | <span data-ttu-id="37101-178">lastname</span><span class="sxs-lookup"><span data-stu-id="37101-178">lastname</span></span> | <span data-ttu-id="37101-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="37101-179">user.surname</span></span> |
    | <span data-ttu-id="37101-180">email</span><span class="sxs-lookup"><span data-stu-id="37101-180">email</span></span> | <span data-ttu-id="37101-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="37101-181">user.mail</span></span> |
    
    <span data-ttu-id="37101-182">a.</span><span class="sxs-lookup"><span data-stu-id="37101-182">a.</span></span> <span data-ttu-id="37101-183">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="37101-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="37101-185">b.</span><span class="sxs-lookup"><span data-stu-id="37101-185">b.</span></span> <span data-ttu-id="37101-186">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="37101-186">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="37101-188">c.</span><span class="sxs-lookup"><span data-stu-id="37101-188">c.</span></span> <span data-ttu-id="37101-189">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="37101-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>
 
    <span data-ttu-id="37101-190">d.</span><span class="sxs-lookup"><span data-stu-id="37101-190">d.</span></span> <span data-ttu-id="37101-191">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="37101-191">Click **Ok**.</span></span>



6. <span data-ttu-id="37101-192">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="37101-192">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_certificate.png) 


7. <span data-ttu-id="37101-194">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="37101-194">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-allocadia-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="37101-196">tooconfigure inicio de sesión único en **Allocadia** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de Allocadia](mailTo:support@allocadia.com).</span><span class="sxs-lookup"><span data-stu-id="37101-196">tooconfigure single sign-on on **Allocadia** side, you need toosend hello downloaded **Metadata XML** too[Allocadia support team](mailTo:support@allocadia.com).</span></span> <span data-ttu-id="37101-197">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="37101-197">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="37101-198">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="37101-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="37101-199">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="37101-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="37101-200">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="37101-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="37101-201">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="37101-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="37101-202">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="37101-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="37101-204">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="37101-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="37101-205">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="37101-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="37101-207">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="37101-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="37101-209">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="37101-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="37101-211">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="37101-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="37101-213">a.</span><span class="sxs-lookup"><span data-stu-id="37101-213">a.</span></span> <span data-ttu-id="37101-214">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="37101-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="37101-215">b.</span><span class="sxs-lookup"><span data-stu-id="37101-215">b.</span></span> <span data-ttu-id="37101-216">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="37101-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="37101-217">c.</span><span class="sxs-lookup"><span data-stu-id="37101-217">c.</span></span> <span data-ttu-id="37101-218">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="37101-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="37101-219">d.</span><span class="sxs-lookup"><span data-stu-id="37101-219">d.</span></span> <span data-ttu-id="37101-220">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="37101-220">Click **Create**.</span></span>
 
### <a name="creating-an-allocadia-test-user"></a><span data-ttu-id="37101-221">Creación de un usuario de prueba de Allocadia</span><span class="sxs-lookup"><span data-stu-id="37101-221">Creating an Allocadia test user</span></span>

<span data-ttu-id="37101-222">La aplicación admite aprovisionamiento de usuarios Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="37101-222">Application supports Just in time user provisioning.</span></span> <span data-ttu-id="37101-223">Después de la autenticación a los usuarios se crean automáticamente en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="37101-223">After authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="37101-224">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="37101-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="37101-225">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooAllocadia.</span><span class="sxs-lookup"><span data-stu-id="37101-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAllocadia.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="37101-227">**tooassign Britta Simon tooAllocadia, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="37101-227">**tooassign Britta Simon tooAllocadia, perform hello following steps:**</span></span>

1. <span data-ttu-id="37101-228">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="37101-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="37101-230">En la lista de aplicaciones de hello, seleccione **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="37101-230">In hello applications list, select **Allocadia**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_app.png) 

3. <span data-ttu-id="37101-232">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="37101-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="37101-234">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="37101-234">Click **Add** button.</span></span> <span data-ttu-id="37101-235">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="37101-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="37101-237">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="37101-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="37101-238">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="37101-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="37101-239">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="37101-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="37101-240">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="37101-240">Testing single sign-on</span></span>

<span data-ttu-id="37101-241">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="37101-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="37101-242">Al hacer clic en icono de Allocadia Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Allocadia aplicación.</span><span class="sxs-lookup"><span data-stu-id="37101-242">When you click hello Allocadia tile in hello Access Panel, you should get automatically signed-on tooyour Allocadia application.</span></span>
<span data-ttu-id="37101-243">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="37101-243">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37101-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="37101-244">Additional resources</span></span>

* [<span data-ttu-id="37101-245">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37101-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="37101-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="37101-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_203.png

