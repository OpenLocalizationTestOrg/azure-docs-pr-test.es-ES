---
title: "Tutorial: Integración de Azure Active Directory con Moxtra | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Moxtra."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 82e2fcc390ba508e86a3992ec1c81d0a0ffed96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="46bdd-103">Tutorial: Integración de Azure Active Directory con Moxtra</span><span class="sxs-lookup"><span data-stu-id="46bdd-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="46bdd-104">En este tutorial, aprenderá cómo toointegrate Moxtra con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="46bdd-104">In this tutorial, you learn how toointegrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="46bdd-105">Integración Moxtra con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="46bdd-105">Integrating Moxtra with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="46bdd-106">Puede controlar en Azure AD que tenga acceso tooMoxtra</span><span class="sxs-lookup"><span data-stu-id="46bdd-106">You can control in Azure AD who has access tooMoxtra</span></span>
- <span data-ttu-id="46bdd-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooMoxtra (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="46bdd-107">You can enable your users tooautomatically get signed-on tooMoxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="46bdd-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="46bdd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="46bdd-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="46bdd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46bdd-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="46bdd-110">Prerequisites</span></span>

<span data-ttu-id="46bdd-111">integración de Azure AD con Moxtra tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="46bdd-111">tooconfigure Azure AD integration with Moxtra, you need hello following items:</span></span>

- <span data-ttu-id="46bdd-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="46bdd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="46bdd-113">Una suscripción habilitada para el inicio de sesión único en Moxtra</span><span class="sxs-lookup"><span data-stu-id="46bdd-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="46bdd-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="46bdd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="46bdd-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="46bdd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="46bdd-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="46bdd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="46bdd-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="46bdd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="46bdd-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="46bdd-118">Scenario description</span></span>
<span data-ttu-id="46bdd-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="46bdd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="46bdd-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="46bdd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="46bdd-121">Agregar Moxtra desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="46bdd-121">Adding Moxtra from hello gallery</span></span>
2. <span data-ttu-id="46bdd-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="46bdd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-hello-gallery"></a><span data-ttu-id="46bdd-123">Agregar Moxtra desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="46bdd-123">Adding Moxtra from hello gallery</span></span>
<span data-ttu-id="46bdd-124">integración de hello tooconfigure de Moxtra en Azure AD, deberá tooadd Moxtra de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="46bdd-124">tooconfigure hello integration of Moxtra into Azure AD, you need tooadd Moxtra from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="46bdd-125">**tooadd Moxtra de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="46bdd-125">**tooadd Moxtra from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="46bdd-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="46bdd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="46bdd-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="46bdd-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="46bdd-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="46bdd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="46bdd-133">En el cuadro de búsqueda de hello, escriba **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-133">In hello search box, type **Moxtra**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="46bdd-135">En el panel de resultados de hello, seleccione **Moxtra**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="46bdd-135">In hello results panel, select **Moxtra**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="46bdd-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="46bdd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="46bdd-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Moxtra con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="46bdd-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="46bdd-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Moxtra es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="46bdd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Moxtra is tooa user in Azure AD.</span></span> <span data-ttu-id="46bdd-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Moxtra debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="46bdd-140">In other words, a link relationship between an Azure AD user and hello related user in Moxtra needs toobe established.</span></span>

<span data-ttu-id="46bdd-141">En Moxtra, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="46bdd-141">In Moxtra, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="46bdd-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Moxtra, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="46bdd-142">tooconfigure and test Azure AD single sign-on with Moxtra, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="46bdd-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="46bdd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="46bdd-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="46bdd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="46bdd-145">**[Crear un usuario de prueba Moxtra](#creating-a-moxtra-test-user)**  -toohave un equivalente de Britta Simon en Moxtra que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="46bdd-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - toohave a counterpart of Britta Simon in Moxtra that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="46bdd-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="46bdd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="46bdd-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="46bdd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="46bdd-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="46bdd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="46bdd-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Moxtra.</span><span class="sxs-lookup"><span data-stu-id="46bdd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="46bdd-150">**inicio de sesión único en Azure AD tooconfigure con Moxtra, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="46bdd-150">**tooconfigure Azure AD single sign-on with Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="46bdd-151">En el portal de Azure, en Hola Hola **Moxtra** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-151">In hello Azure portal, on hello **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="46bdd-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="46bdd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="46bdd-155">En hello **Moxtra dominio y las direcciones URL** sección, lleve a cabo Hola siguiendo el paso:</span><span class="sxs-lookup"><span data-stu-id="46bdd-155">On hello **Moxtra Domain and URLs** section, perform hello following step:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="46bdd-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL como:`https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="46bdd-157">In hello **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="46bdd-158">Aplicación de Moxtra espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="46bdd-158">Moxtra application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="46bdd-159">Configurar Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="46bdd-159">Configure hello following claims for this application.</span></span> <span data-ttu-id="46bdd-160">Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="46bdd-160">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="46bdd-161">Hola siguiente captura de pantalla muestra un ejemplo de esta configuración.</span><span class="sxs-lookup"><span data-stu-id="46bdd-161">hello following screenshot shows an example for this configuration.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="46bdd-163">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de Hola y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="46bdd-163">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="46bdd-164">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="46bdd-164">Attribute Name</span></span> | <span data-ttu-id="46bdd-165">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="46bdd-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="46bdd-166">firstname</span><span class="sxs-lookup"><span data-stu-id="46bdd-166">firstname</span></span> | <span data-ttu-id="46bdd-167">user.givenname</span><span class="sxs-lookup"><span data-stu-id="46bdd-167">user.givenname</span></span> |
    | <span data-ttu-id="46bdd-168">lastname</span><span class="sxs-lookup"><span data-stu-id="46bdd-168">lastname</span></span> | <span data-ttu-id="46bdd-169">user.surname</span><span class="sxs-lookup"><span data-stu-id="46bdd-169">user.surname</span></span> |
    | <span data-ttu-id="46bdd-170">idpid</span><span class="sxs-lookup"><span data-stu-id="46bdd-170">idpid</span></span>    | <span data-ttu-id="46bdd-171">< SAML Entity ID ></span><span class="sxs-lookup"><span data-stu-id="46bdd-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="46bdd-172">Hola valo **idpid** atributo no es real.</span><span class="sxs-lookup"><span data-stu-id="46bdd-172">hello value of **idpid** attribute is not real.</span></span> <span data-ttu-id="46bdd-173">Puede obtener valor real de Hola de **referencia rápida** sección bajo **Moxtra configuración**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-173">You can get hello actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="46bdd-174">a.</span><span class="sxs-lookup"><span data-stu-id="46bdd-174">a.</span></span> <span data-ttu-id="46bdd-175">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="46bdd-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="46bdd-177">b.</span><span class="sxs-lookup"><span data-stu-id="46bdd-177">b.</span></span> <span data-ttu-id="46bdd-178">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="46bdd-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="46bdd-180">c.</span><span class="sxs-lookup"><span data-stu-id="46bdd-180">c.</span></span> <span data-ttu-id="46bdd-181">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="46bdd-181">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="46bdd-182">d.</span><span class="sxs-lookup"><span data-stu-id="46bdd-182">d.</span></span> <span data-ttu-id="46bdd-183">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="46bdd-184">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="46bdd-184">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="46bdd-186">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="46bdd-186">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="46bdd-188">En hello **Moxtra configuración** sección, haga clic en **configurar Moxtra** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="46bdd-188">On hello **Moxtra Configuration** section, click **Configure Moxtra** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="46bdd-189">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="46bdd-189">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="46bdd-191">En otra ventana del explorador, inicie sesión en el sitio de empresa de tooyour Moxtra como administrador.</span><span class="sxs-lookup"><span data-stu-id="46bdd-191">In another browser window, sign on tooyour Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="46bdd-192">En la barra de herramientas de Hola Hola izquierda, haga clic en **consola de administración > SAML Single Sign-on**y, a continuación, haga clic en **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-192">In hello toolbar on hello left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="46bdd-194">En hello **SAML** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="46bdd-194">On hello **SAML** page, perform hello following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="46bdd-196">a.</span><span class="sxs-lookup"><span data-stu-id="46bdd-196">a.</span></span> <span data-ttu-id="46bdd-197">Hola **nombre** cuadro de texto, escriba un nombre para la configuración (p. ej.: *SAML*).</span><span class="sxs-lookup"><span data-stu-id="46bdd-197">In hello **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="46bdd-198">b.</span><span class="sxs-lookup"><span data-stu-id="46bdd-198">b.</span></span> <span data-ttu-id="46bdd-199">Hola **Id. de entidad IdP** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="46bdd-199">In hello **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="46bdd-200">c.</span><span class="sxs-lookup"><span data-stu-id="46bdd-200">c.</span></span> <span data-ttu-id="46bdd-201">En **dirección URL de inicio de sesión** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="46bdd-201">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="46bdd-202">d.</span><span class="sxs-lookup"><span data-stu-id="46bdd-202">d.</span></span> <span data-ttu-id="46bdd-203">Hola **AuthnContextClassRef** cuadro de texto, tipo **urn: oasis: nombres: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-203">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="46bdd-204">e.</span><span class="sxs-lookup"><span data-stu-id="46bdd-204">e.</span></span> <span data-ttu-id="46bdd-205">Hola **NameID Format** cuadro de texto, tipo **urn: oasis: nombres: tc: SAML:1.1:nameid-formato: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-205">In hello **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="46bdd-206">f.</span><span class="sxs-lookup"><span data-stu-id="46bdd-206">f.</span></span> <span data-ttu-id="46bdd-207">Abrir el certificado que ha descargado desde el portal de Azure en el Bloc de notas, copie el contenido de hello y, a continuación, péguelo en hello **certificado** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="46bdd-207">Open certificate which you have downloaded from Azure portal in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="46bdd-208">g.</span><span class="sxs-lookup"><span data-stu-id="46bdd-208">g.</span></span> <span data-ttu-id="46bdd-209">En el cuadro de dominio de correo electrónico SAML de hello, escriba el dominio de correo electrónico SAML.</span><span class="sxs-lookup"><span data-stu-id="46bdd-209">In hello SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="46bdd-210">dominio de toosee Hola pasos tooverify hello, haga clic en hello "****" a continuación.</span><span class="sxs-lookup"><span data-stu-id="46bdd-210">toosee hello steps tooverify hello domain, click hello "**i**" below.</span></span>

    <span data-ttu-id="46bdd-211">h.</span><span class="sxs-lookup"><span data-stu-id="46bdd-211">h.</span></span> <span data-ttu-id="46bdd-212">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="46bdd-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="46bdd-213">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="46bdd-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="46bdd-214">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="46bdd-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="46bdd-215">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="46bdd-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="46bdd-216">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="46bdd-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="46bdd-217">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="46bdd-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="46bdd-219">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="46bdd-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="46bdd-220">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="46bdd-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="46bdd-222">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="46bdd-224">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="46bdd-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="46bdd-226">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="46bdd-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="46bdd-228">a.</span><span class="sxs-lookup"><span data-stu-id="46bdd-228">a.</span></span> <span data-ttu-id="46bdd-229">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="46bdd-230">b.</span><span class="sxs-lookup"><span data-stu-id="46bdd-230">b.</span></span> <span data-ttu-id="46bdd-231">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="46bdd-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="46bdd-232">c.</span><span class="sxs-lookup"><span data-stu-id="46bdd-232">c.</span></span> <span data-ttu-id="46bdd-233">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="46bdd-234">d.</span><span class="sxs-lookup"><span data-stu-id="46bdd-234">d.</span></span> <span data-ttu-id="46bdd-235">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="46bdd-236">Creación de un usuario de prueba de Moxtra</span><span class="sxs-lookup"><span data-stu-id="46bdd-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="46bdd-237">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Moxtra toocreate.</span><span class="sxs-lookup"><span data-stu-id="46bdd-237">hello objective of this section is toocreate a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="46bdd-238">**toocreate un usuario llamado Britta Simon en Moxtra, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="46bdd-238">**toocreate a user called Britta Simon in Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="46bdd-239">Inicie sesión en tooyour Moxtra sitio de su compañía como administrador.</span><span class="sxs-lookup"><span data-stu-id="46bdd-239">Sign on tooyour Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="46bdd-240">En la barra de herramientas de Hola Hola izquierda, haga clic en **consola de administración > Administración de usuarios**y, a continuación, **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-240">In hello toolbar on hello left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="46bdd-242">En hello **Agregar usuario** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="46bdd-242">On hello **Add User** dialog, perform hello following steps:</span></span>
  
    <span data-ttu-id="46bdd-243">a.</span><span class="sxs-lookup"><span data-stu-id="46bdd-243">a.</span></span> <span data-ttu-id="46bdd-244">Hola **nombre** cuadro de texto, tipo **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-244">In hello **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="46bdd-245">b.</span><span class="sxs-lookup"><span data-stu-id="46bdd-245">b.</span></span> <span data-ttu-id="46bdd-246">Hola **Last Name** cuadro de texto, tipo **Simon**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-246">In hello **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="46bdd-247">c.</span><span class="sxs-lookup"><span data-stu-id="46bdd-247">c.</span></span> <span data-ttu-id="46bdd-248">Hola **correo electrónico** cuadro de texto, tipo de Bárbara dirección de correo electrónico igual que en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="46bdd-248">In hello **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="46bdd-249">d.</span><span class="sxs-lookup"><span data-stu-id="46bdd-249">d.</span></span> <span data-ttu-id="46bdd-250">Hola **división** cuadro de texto, tipo **desarrollo**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-250">In hello **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="46bdd-251">e.</span><span class="sxs-lookup"><span data-stu-id="46bdd-251">e.</span></span> <span data-ttu-id="46bdd-252">Hola **departamento** cuadro de texto, tipo **TI**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-252">In hello **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="46bdd-253">f.</span><span class="sxs-lookup"><span data-stu-id="46bdd-253">f.</span></span> <span data-ttu-id="46bdd-254">Seleccione **Administrator** (Administrador).</span><span class="sxs-lookup"><span data-stu-id="46bdd-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="46bdd-255">g.</span><span class="sxs-lookup"><span data-stu-id="46bdd-255">g.</span></span> <span data-ttu-id="46bdd-256">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-256">Click **Add**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="46bdd-257">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="46bdd-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="46bdd-258">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooMoxtra.</span><span class="sxs-lookup"><span data-stu-id="46bdd-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMoxtra.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="46bdd-260">**tooassign Britta Simon tooMoxtra, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="46bdd-260">**tooassign Britta Simon tooMoxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="46bdd-261">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="46bdd-263">En la lista de aplicaciones de hello, seleccione **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-263">In hello applications list, select **Moxtra**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="46bdd-265">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="46bdd-267">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-267">Click **Add** button.</span></span> <span data-ttu-id="46bdd-268">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="46bdd-270">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="46bdd-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="46bdd-271">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="46bdd-272">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="46bdd-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="46bdd-273">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="46bdd-273">Testing single sign-on</span></span>

<span data-ttu-id="46bdd-274">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="46bdd-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="46bdd-275">Al hacer clic en icono de Moxtra Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Moxtra aplicación.</span><span class="sxs-lookup"><span data-stu-id="46bdd-275">When you click hello Moxtra tile in hello Access Panel, you should get automatically signed-on tooyour Moxtra application.</span></span>
<span data-ttu-id="46bdd-276">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="46bdd-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="46bdd-277">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="46bdd-277">Additional resources</span></span>

* [<span data-ttu-id="46bdd-278">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46bdd-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="46bdd-279">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="46bdd-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

