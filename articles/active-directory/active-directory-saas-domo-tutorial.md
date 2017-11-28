---
title: "Tutorial: Integración de Azure Active Directory con Domo | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Domo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 058626e4-73b3-4dc2-86ca-b060d002d70a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: cc70f8e5013f864d275762bbc1f84bd9677e8c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-domo"></a><span data-ttu-id="52f4a-103">Tutorial: integración de Azure Active Directory con Domo</span><span class="sxs-lookup"><span data-stu-id="52f4a-103">Tutorial: Azure Active Directory integration with Domo</span></span>

<span data-ttu-id="52f4a-104">En este tutorial, aprenderá cómo toointegrate Domo con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52f4a-104">In this tutorial, you learn how toointegrate Domo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="52f4a-105">Integración Domo con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="52f4a-105">Integrating Domo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="52f4a-106">Puede controlar en Azure AD que tenga acceso tooDomo</span><span class="sxs-lookup"><span data-stu-id="52f4a-106">You can control in Azure AD who has access tooDomo</span></span>
- <span data-ttu-id="52f4a-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooDomo (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52f4a-107">You can enable your users tooautomatically get signed-on tooDomo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="52f4a-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="52f4a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="52f4a-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="52f4a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52f4a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="52f4a-110">Prerequisites</span></span>

<span data-ttu-id="52f4a-111">integración de Azure AD con Domo tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="52f4a-111">tooconfigure Azure AD integration with Domo, you need hello following items:</span></span>

- <span data-ttu-id="52f4a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52f4a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="52f4a-113">Una suscripción habilitada para el inicio de sesión único en Domo</span><span class="sxs-lookup"><span data-stu-id="52f4a-113">A Domo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="52f4a-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="52f4a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="52f4a-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="52f4a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="52f4a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="52f4a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="52f4a-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52f4a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="52f4a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="52f4a-118">Scenario description</span></span>
<span data-ttu-id="52f4a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="52f4a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="52f4a-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="52f4a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="52f4a-121">Agregar Domo desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="52f4a-121">Adding Domo from hello gallery</span></span>
2. <span data-ttu-id="52f4a-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52f4a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-domo-from-hello-gallery"></a><span data-ttu-id="52f4a-123">Agregar Domo desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="52f4a-123">Adding Domo from hello gallery</span></span>
<span data-ttu-id="52f4a-124">integración de hello tooconfigure de Domo en Azure AD, deberá tooadd Domo de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="52f4a-124">tooconfigure hello integration of Domo into Azure AD, you need tooadd Domo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="52f4a-125">**tooadd Domo de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="52f4a-125">**tooadd Domo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="52f4a-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="52f4a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="52f4a-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="52f4a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="52f4a-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="52f4a-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="52f4a-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="52f4a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="52f4a-133">En el cuadro de búsqueda de hello, escriba **Domo**.</span><span class="sxs-lookup"><span data-stu-id="52f4a-133">In hello search box, type **Domo**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-domo-tutorial/tutorial_domo_search.png)

5. <span data-ttu-id="52f4a-135">En el panel de resultados de hello, seleccione **Domo**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="52f4a-135">In hello results panel, select **Domo**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-domo-tutorial/tutorial_domo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="52f4a-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52f4a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="52f4a-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Domo con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="52f4a-138">In this section, you configure and test Azure AD single sign-on with Domo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="52f4a-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Domo es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52f4a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Domo is tooa user in Azure AD.</span></span> <span data-ttu-id="52f4a-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Domo debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="52f4a-140">In other words, a link relationship between an Azure AD user and hello related user in Domo needs toobe established.</span></span>

<span data-ttu-id="52f4a-141">En Domo, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="52f4a-141">In Domo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="52f4a-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Domo, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="52f4a-142">tooconfigure and test Azure AD single sign-on with Domo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="52f4a-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="52f4a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="52f4a-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52f4a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="52f4a-145">**[Crear un usuario de prueba Domo](#creating-a-domo-test-user)**  -toohave un equivalente de Britta Simon en Domo que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="52f4a-145">**[Creating a Domo test user](#creating-a-domo-test-user)** - toohave a counterpart of Britta Simon in Domo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="52f4a-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="52f4a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="52f4a-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="52f4a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="52f4a-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52f4a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="52f4a-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Domo.</span><span class="sxs-lookup"><span data-stu-id="52f4a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Domo application.</span></span>

<span data-ttu-id="52f4a-150">**inicio de sesión único en Azure AD tooconfigure con Domo, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="52f4a-150">**tooconfigure Azure AD single sign-on with Domo, perform hello following steps:**</span></span>

1. <span data-ttu-id="52f4a-151">En el portal de Azure, en Hola Hola **Domo** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="52f4a-151">In hello Azure portal, on hello **Domo** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="52f4a-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="52f4a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-domo-tutorial/tutorial_domo_samlbase.png)

3. <span data-ttu-id="52f4a-155">En hello **Domo dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="52f4a-155">On hello **Domo Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-domo-tutorial/tutorial_domo_url.png)

    <span data-ttu-id="52f4a-157">a.</span><span class="sxs-lookup"><span data-stu-id="52f4a-157">a.</span></span> <span data-ttu-id="52f4a-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.domo.com`</span><span class="sxs-lookup"><span data-stu-id="52f4a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.domo.com`</span></span>

    <span data-ttu-id="52f4a-159">b.</span><span class="sxs-lookup"><span data-stu-id="52f4a-159">b.</span></span> <span data-ttu-id="52f4a-160">Hola **identificador** cuadro de texto, escriba una dirección URL con hello siguiendo patrones:</span><span class="sxs-lookup"><span data-stu-id="52f4a-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>     

    | |
    |--|    
    | `https://<companyname>.domo.com` |
    | `https://<companyname>.beta.domo.com` |
    | `https://<companyname>.demo.domo.com` |
    | `https://<companyname>.dev.domo.com` | 
    | `https://<companyname>.fastage1.domo.com` |       
    | `https://<companyname>.frdev.domo.com` |       
    | `https://<companyname>.gastage.domo.com` |       
    | `https://<companyname>.load.domo.com` |       
    | `https://<companyname>.local.domo.com` |       
    | `https://<companyname>.qa.domo.com` |
    | `https://<companyname>.stage.domo.com` |
    
    > [!NOTE] 
    > <span data-ttu-id="52f4a-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="52f4a-161">These values are not real.</span></span> <span data-ttu-id="52f4a-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="52f4a-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="52f4a-163">Póngase en contacto con [equipo de soporte técnico de cliente Domo](mailto:support@domo.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="52f4a-163">Contact [Domo Client support team](mailto:support@domo.com) tooget these values.</span></span>

4. <span data-ttu-id="52f4a-164">Aplicación de domo espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="52f4a-164">Domo application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="52f4a-165">Configurar Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="52f4a-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="52f4a-166">Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="52f4a-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="52f4a-167">Hola siguiente captura de pantalla muestra un ejemplo de esta configuración.</span><span class="sxs-lookup"><span data-stu-id="52f4a-167">hello following screenshot shows an example for this configuration.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-domo-tutorial/tutorial_domo_attributes.png)
    
5. <span data-ttu-id="52f4a-169">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de Hola y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="52f4a-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="52f4a-170">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="52f4a-170">Attribute Name</span></span> | <span data-ttu-id="52f4a-171">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="52f4a-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="52f4a-172">name</span><span class="sxs-lookup"><span data-stu-id="52f4a-172">name</span></span> | <span data-ttu-id="52f4a-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="52f4a-173">user.displayname</span></span> |
    | <span data-ttu-id="52f4a-174">email</span><span class="sxs-lookup"><span data-stu-id="52f4a-174">email</span></span> | <span data-ttu-id="52f4a-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="52f4a-175">user.mail</span></span> |
    
    <span data-ttu-id="52f4a-176">a.</span><span class="sxs-lookup"><span data-stu-id="52f4a-176">a.</span></span> <span data-ttu-id="52f4a-177">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="52f4a-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-domo-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-domo-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="52f4a-180">b.</span><span class="sxs-lookup"><span data-stu-id="52f4a-180">b.</span></span> <span data-ttu-id="52f4a-181">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="52f4a-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="52f4a-182">c.</span><span class="sxs-lookup"><span data-stu-id="52f4a-182">c.</span></span> <span data-ttu-id="52f4a-183">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="52f4a-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="52f4a-184">d.</span><span class="sxs-lookup"><span data-stu-id="52f4a-184">d.</span></span> <span data-ttu-id="52f4a-185">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="52f4a-185">Click **Ok**.</span></span> 
 
6. <span data-ttu-id="52f4a-186">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="52f4a-186">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-domo-tutorial/tutorial_domo_certificate.png) 

7. <span data-ttu-id="52f4a-188">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="52f4a-188">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-domo-tutorial/tutorial_general_400.png)


8. <span data-ttu-id="52f4a-190">En hello **configuración Domo** sección, haga clic en **configurar Domo** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="52f4a-190">On hello **Domo Configuration** section, click **Configure Domo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="52f4a-191">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="52f4a-191">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

   ![Configurar inicio de sesión único](./media/active-directory-saas-domo-tutorial/tutorial_domo_configure.png) 

9. <span data-ttu-id="52f4a-193">tooconfigure inicio de sesión único en **Domo** lado, necesita hello toosend descargado **certificado**, **Id. de entidad SAML**, hello **servicio de inicio de sesión único de SAML Dirección URL** hello y **dirección URL de cierre de sesión** demasiado[equipo de soporte técnico de Domo](mailto:support@domo.com).</span><span class="sxs-lookup"><span data-stu-id="52f4a-193">tooconfigure single sign-on on **Domo** side, you need toosend hello downloaded **Certificate**, **SAML Entity ID**, hello **SAML Single Sign-On Service URL** and hello **Sign-Out URL** too[Domo support team](mailto:support@domo.com).</span></span> <span data-ttu-id="52f4a-194">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="52f4a-194">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="52f4a-195">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="52f4a-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="52f4a-196">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="52f4a-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="52f4a-197">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="52f4a-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="52f4a-198">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="52f4a-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="52f4a-199">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="52f4a-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="52f4a-201">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="52f4a-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="52f4a-202">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="52f4a-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="52f4a-204">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="52f4a-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="52f4a-206">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="52f4a-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="52f4a-208">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="52f4a-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="52f4a-210">a.</span><span class="sxs-lookup"><span data-stu-id="52f4a-210">a.</span></span> <span data-ttu-id="52f4a-211">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="52f4a-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="52f4a-212">b.</span><span class="sxs-lookup"><span data-stu-id="52f4a-212">b.</span></span> <span data-ttu-id="52f4a-213">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="52f4a-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="52f4a-214">c.</span><span class="sxs-lookup"><span data-stu-id="52f4a-214">c.</span></span> <span data-ttu-id="52f4a-215">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="52f4a-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="52f4a-216">d.</span><span class="sxs-lookup"><span data-stu-id="52f4a-216">d.</span></span> <span data-ttu-id="52f4a-217">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="52f4a-217">Click **Create**.</span></span>
 
### <a name="creating-a-domo-test-user"></a><span data-ttu-id="52f4a-218">Creación de usuario de prueba de Domo</span><span class="sxs-lookup"><span data-stu-id="52f4a-218">Creating a Domo test user</span></span>

<span data-ttu-id="52f4a-219">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Domo toocreate.</span><span class="sxs-lookup"><span data-stu-id="52f4a-219">hello objective of this section is toocreate a user called Britta Simon in Domo.</span></span> <span data-ttu-id="52f4a-220">Domo admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="52f4a-220">Domo supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="52f4a-221">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="52f4a-221">There is no action item for you in this section.</span></span> <span data-ttu-id="52f4a-222">Si no existe todavía, se crea un usuario nuevo durante un tooaccess intento Domo.</span><span class="sxs-lookup"><span data-stu-id="52f4a-222">A new user is created during an attempt tooaccess Domo if it doesn't exist yet.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="52f4a-223">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="52f4a-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="52f4a-224">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooDomo.</span><span class="sxs-lookup"><span data-stu-id="52f4a-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDomo.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="52f4a-226">**tooassign Britta Simon tooDomo, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="52f4a-226">**tooassign Britta Simon tooDomo, perform hello following steps:**</span></span>

1. <span data-ttu-id="52f4a-227">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="52f4a-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="52f4a-229">En la lista de aplicaciones de hello, seleccione **Domo**.</span><span class="sxs-lookup"><span data-stu-id="52f4a-229">In hello applications list, select **Domo**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-domo-tutorial/tutorial_domo_app.png) 

3. <span data-ttu-id="52f4a-231">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="52f4a-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="52f4a-233">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="52f4a-233">Click **Add** button.</span></span> <span data-ttu-id="52f4a-234">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="52f4a-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="52f4a-236">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="52f4a-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="52f4a-237">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="52f4a-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="52f4a-238">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="52f4a-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="52f4a-239">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="52f4a-239">Testing single sign-on</span></span>

<span data-ttu-id="52f4a-240">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="52f4a-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="52f4a-241">Al hacer clic en icono de Domo Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Domo aplicación.</span><span class="sxs-lookup"><span data-stu-id="52f4a-241">When you click hello Domo tile in hello Access Panel, you should get automatically signed-on tooyour Domo application.</span></span>

<span data-ttu-id="52f4a-242">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="52f4a-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="52f4a-243">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="52f4a-243">Additional resources</span></span>

* [<span data-ttu-id="52f4a-244">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52f4a-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="52f4a-245">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="52f4a-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-domo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-domo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-domo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-domo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-domo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-domo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-domo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-domo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-domo-tutorial/tutorial_general_203.png

