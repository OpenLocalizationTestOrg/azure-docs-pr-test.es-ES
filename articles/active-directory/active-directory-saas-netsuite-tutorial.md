---
title: "Tutorial: Integración de Azure Active Directory con NetSuite | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="e8331-103">Tutorial: Integración de Azure Active Directory con NetSuite</span><span class="sxs-lookup"><span data-stu-id="e8331-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="e8331-104">En este tutorial, aprenderá cómo toointegrate Netsuite con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e8331-104">In this tutorial, you learn how toointegrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e8331-105">Integración Netsuite con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e8331-105">Integrating Netsuite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e8331-106">Puede controlar en Azure AD que tenga acceso tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="e8331-106">You can control in Azure AD who has access tooNetsuite</span></span>
- <span data-ttu-id="e8331-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooNetsuite (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8331-107">You can enable your users tooautomatically get signed-on tooNetsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e8331-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e8331-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e8331-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e8331-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8331-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e8331-110">Prerequisites</span></span>

<span data-ttu-id="e8331-111">integración de Azure AD con Netsuite tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e8331-111">tooconfigure Azure AD integration with Netsuite, you need hello following items:</span></span>

- <span data-ttu-id="e8331-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8331-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e8331-113">Una suscripción habilitada para el inicio de sesión único en NetSuite</span><span class="sxs-lookup"><span data-stu-id="e8331-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e8331-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e8331-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e8331-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e8331-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e8331-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e8331-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e8331-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e8331-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e8331-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e8331-118">Scenario description</span></span>
<span data-ttu-id="e8331-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e8331-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e8331-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="e8331-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e8331-121">Agregar Netsuite desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e8331-121">Adding Netsuite from hello gallery</span></span>
2. <span data-ttu-id="e8331-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8331-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-hello-gallery"></a><span data-ttu-id="e8331-123">Agregar Netsuite desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e8331-123">Adding Netsuite from hello gallery</span></span>
<span data-ttu-id="e8331-124">integración de hello tooconfigure de Netsuite en Azure AD, deberá tooadd Netsuite de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="e8331-124">tooconfigure hello integration of Netsuite into Azure AD, you need tooadd Netsuite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e8331-125">**tooadd Netsuite de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e8331-125">**tooadd Netsuite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8331-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="e8331-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e8331-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e8331-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e8331-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e8331-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e8331-131">Haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8331-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e8331-133">En el cuadro de búsqueda de hello, escriba **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="e8331-133">In hello search box, type **Netsuite**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="e8331-135">En el panel de resultados de hello, seleccione **Netsuite**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e8331-135">In hello results panel, select **Netsuite**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e8331-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8331-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e8331-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con NetSuite con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e8331-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e8331-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Netsuite es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8331-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Netsuite is tooa user in Azure AD.</span></span> <span data-ttu-id="e8331-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Netsuite debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="e8331-140">In other words, a link relationship between an Azure AD user and hello related user in Netsuite needs toobe established.</span></span>

<span data-ttu-id="e8331-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Netsuite.</span><span class="sxs-lookup"><span data-stu-id="e8331-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Netsuite.</span></span>

<span data-ttu-id="e8331-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Netsuite, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e8331-142">tooconfigure and test Azure AD single sign-on with Netsuite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e8331-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="e8331-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e8331-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e8331-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e8331-145">**[Crear un usuario de prueba de Netsuite](#creating-a-netsuite-test-user)**  -toohave un equivalente de Britta Simon en Netsuite que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="e8331-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - toohave a counterpart of Britta Simon in Netsuite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e8331-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e8331-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e8331-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e8331-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e8331-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8331-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e8331-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Netsuite.</span><span class="sxs-lookup"><span data-stu-id="e8331-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="e8331-150">**inicio de sesión único en Azure AD tooconfigure con Netsuite, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e8331-150">**tooconfigure Azure AD single sign-on with Netsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8331-151">En el portal de Azure, en Hola Hola **Netsuite** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e8331-151">In hello Azure portal, on hello **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e8331-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e8331-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="e8331-155">En hello **Netsuite dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e8331-155">On hello **Netsuite Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="e8331-157">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="e8331-157">In hello **Reply URL** textbox, type a URL using hello following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e8331-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="e8331-158">This value is not real value.</span></span> <span data-ttu-id="e8331-159">Valor de Hola de actualización con Hola dirección URL de respuesta real.</span><span class="sxs-lookup"><span data-stu-id="e8331-159">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="e8331-160">Póngase en contacto con [equipo de soporte técnico de Netsuite](http://www.netsuite.com/portal/services/support.shtml) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="e8331-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) tooget this value.</span></span>
 
4. <span data-ttu-id="e8331-161">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e8331-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="e8331-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e8331-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e8331-165">En hello **configuración de Netsuite** sección, haga clic en **configurar Netsuite** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="e8331-165">On hello **Netsuite Configuration** section, click **Configure Netsuite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e8331-166">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="e8331-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="e8331-168">Abra una nueva pestaña en el explorador e inicie sesión en el sitio de la empresa Netsuite como administrador.</span><span class="sxs-lookup"><span data-stu-id="e8331-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="e8331-169">En la barra de herramientas de hello al principio de Hola de página de hello, haga clic en **el programa de instalación**, a continuación, haga clic en **el Administrador de instalación**.</span><span class="sxs-lookup"><span data-stu-id="e8331-169">In hello toolbar at hello top of hello page, click **Setup**, then click **Setup Manager**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="e8331-171">De hello **tareas de configuración** lista, seleccione **integración**.</span><span class="sxs-lookup"><span data-stu-id="e8331-171">From hello **Setup Tasks** list, select **Integration**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="e8331-173">Hola **administrar autenticación** sección, haga clic en **SAML Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e8331-173">In hello **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="e8331-175">En hello **configuración de SAML** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="e8331-175">On hello **SAML Setup** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="e8331-176">a.</span><span class="sxs-lookup"><span data-stu-id="e8331-176">a.</span></span> <span data-ttu-id="e8331-177">Hola copia **SAML Single Sign-On dirección URL del servicio** valor de **referencia rápida** sección de **configurar inicio de sesión** y péguelo en hello **proveedor de identidades Página de inicio de sesión** campo en Netsuite.</span><span class="sxs-lookup"><span data-stu-id="e8331-177">Copy hello **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into hello **Identity Provider Login Page** field in Netsuite.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="e8331-179">b.</span><span class="sxs-lookup"><span data-stu-id="e8331-179">b.</span></span> <span data-ttu-id="e8331-180">En NetSuite, seleccione **Primary Authentication Method** (Método de autenticación principal).</span><span class="sxs-lookup"><span data-stu-id="e8331-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="e8331-181">c.</span><span class="sxs-lookup"><span data-stu-id="e8331-181">c.</span></span> <span data-ttu-id="e8331-182">Para la etiqueta de campo de hello **metadatos del proveedor de identidad de SAMLV2**, seleccione **cargar archivo de metadatos de IDP**.</span><span class="sxs-lookup"><span data-stu-id="e8331-182">For hello field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="e8331-183">A continuación, haga clic en **examinar** archivo de metadatos de hello tooupload que descargó del portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e8331-183">Then click **Browse** tooupload hello metadata file that you downloaded from Azure portal.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="e8331-185">d.</span><span class="sxs-lookup"><span data-stu-id="e8331-185">d.</span></span> <span data-ttu-id="e8331-186">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="e8331-186">Click **Submit**.</span></span>

12. <span data-ttu-id="e8331-187">En Azure AD, haga clic en la casilla **Ver y editar todos los atributos de usuario** y agregue el atributo.</span><span class="sxs-lookup"><span data-stu-id="e8331-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="e8331-189">Para hello **nombre del atributo** , escriba en `account`.</span><span class="sxs-lookup"><span data-stu-id="e8331-189">For hello **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="e8331-190">Para hello **valor del atributo** , escriba en el identificador de cuenta de Netsuite. Este valor es constante y cambiar con la cuenta.</span><span class="sxs-lookup"><span data-stu-id="e8331-190">For hello **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="e8331-191">Instrucciones sobre cómo toofind tu identificador de cuenta se incluyen a continuación:</span><span class="sxs-lookup"><span data-stu-id="e8331-191">Instructions on how toofind your account ID are included below:</span></span>

      ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="e8331-193">a.</span><span class="sxs-lookup"><span data-stu-id="e8331-193">a.</span></span> <span data-ttu-id="e8331-194">En Netsuite, haga clic en **el programa de instalación** desde el menú de navegación superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8331-194">In Netsuite, click **Setup** from hello top navigation menu.</span></span>

    <span data-ttu-id="e8331-195">b.</span><span class="sxs-lookup"><span data-stu-id="e8331-195">b.</span></span> <span data-ttu-id="e8331-196">A continuación, haga clic en hello **tareas de configuración** sección del menú de navegación izquierdo de hello, seleccione hello **integración** sección y haga clic en **preferencias de servicios Web**.</span><span class="sxs-lookup"><span data-stu-id="e8331-196">Then click under hello **Setup Tasks** section of hello left navigation menu, select hello **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="e8331-197">c.</span><span class="sxs-lookup"><span data-stu-id="e8331-197">c.</span></span> <span data-ttu-id="e8331-198">Copie su ID de cuenta de Netsuite y pegarlos en hello **valor del atributo** campo en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8331-198">Copy your Netsuite Account ID and paste it into hello **Attribute Value** field in Azure AD.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="e8331-200">Antes de que los usuarios pueden realizar un inicio de sesión único en Netsuite, que deben asignarse en primer lugar los permisos adecuados de hello en Netsuite.</span><span class="sxs-lookup"><span data-stu-id="e8331-200">Before users can perform single sign-on into Netsuite, they must first be assigned hello appropriate permissions in Netsuite.</span></span> <span data-ttu-id="e8331-201">Siga instrucciones hello tooassign estos permisos.</span><span class="sxs-lookup"><span data-stu-id="e8331-201">Follow hello instructions below tooassign these permissions.</span></span>

    <span data-ttu-id="e8331-202">a.</span><span class="sxs-lookup"><span data-stu-id="e8331-202">a.</span></span> <span data-ttu-id="e8331-203">En el menú de navegación superior de hello, haga clic en **el programa de instalación**, a continuación, haga clic en **el Administrador de instalación**.</span><span class="sxs-lookup"><span data-stu-id="e8331-203">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="e8331-205">b.</span><span class="sxs-lookup"><span data-stu-id="e8331-205">b.</span></span> <span data-ttu-id="e8331-206">En el menú de navegación izquierdo de hello, seleccione **usuarios/Roles**, a continuación, haga clic en **administrar funciones**.</span><span class="sxs-lookup"><span data-stu-id="e8331-206">On hello left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="e8331-208">c.</span><span class="sxs-lookup"><span data-stu-id="e8331-208">c.</span></span> <span data-ttu-id="e8331-209">Haga clic en **Nuevo rol**.</span><span class="sxs-lookup"><span data-stu-id="e8331-209">Click **New Role**.</span></span>

    <span data-ttu-id="e8331-210">d.</span><span class="sxs-lookup"><span data-stu-id="e8331-210">d.</span></span> <span data-ttu-id="e8331-211">Escriba un **nombre** para el nuevo rol, seleccione hello y **Single Sign-On solo** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="e8331-211">Type in a **Name** for your new role, and select hello **Single Sign-On Only** checkbox.</span></span>
      
      ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="e8331-213">e.</span><span class="sxs-lookup"><span data-stu-id="e8331-213">e.</span></span> <span data-ttu-id="e8331-214">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e8331-214">Click **Save**.</span></span>

    <span data-ttu-id="e8331-215">f.</span><span class="sxs-lookup"><span data-stu-id="e8331-215">f.</span></span> <span data-ttu-id="e8331-216">En el menú de hello en la parte superior de hello, haga clic en **permisos**.</span><span class="sxs-lookup"><span data-stu-id="e8331-216">In hello menu on hello top, click **Permissions**.</span></span> <span data-ttu-id="e8331-217">A continuación, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="e8331-217">Then click **Setup**.</span></span>
      
       ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="e8331-219">g.</span><span class="sxs-lookup"><span data-stu-id="e8331-219">g.</span></span> <span data-ttu-id="e8331-220">Seleccione **Configurar inicio de sesión único de SAM** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e8331-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="e8331-221">h.</span><span class="sxs-lookup"><span data-stu-id="e8331-221">h.</span></span> <span data-ttu-id="e8331-222">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e8331-222">Click **Save**.</span></span>

    <span data-ttu-id="e8331-223">i.</span><span class="sxs-lookup"><span data-stu-id="e8331-223">i.</span></span> <span data-ttu-id="e8331-224">En el menú de navegación superior de hello, haga clic en **el programa de instalación**, a continuación, haga clic en **el Administrador de instalación**.</span><span class="sxs-lookup"><span data-stu-id="e8331-224">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="e8331-226">j.</span><span class="sxs-lookup"><span data-stu-id="e8331-226">j.</span></span> <span data-ttu-id="e8331-227">En el menú de navegación izquierdo de hello, seleccione **usuarios/Roles**, a continuación, haga clic en **administrar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e8331-227">On hello left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="e8331-229">k.</span><span class="sxs-lookup"><span data-stu-id="e8331-229">k.</span></span> <span data-ttu-id="e8331-230">Seleccione un usuario de prueba.</span><span class="sxs-lookup"><span data-stu-id="e8331-230">Select a test user.</span></span> <span data-ttu-id="e8331-231">A continuación, haga clic en **Editar**.</span><span class="sxs-lookup"><span data-stu-id="e8331-231">Then click **Edit**.</span></span>
      
       ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="e8331-233">l.</span><span class="sxs-lookup"><span data-stu-id="e8331-233">l.</span></span> <span data-ttu-id="e8331-234">En el cuadro de diálogo de Roles de hello, seleccione el rol de Hola que ha creado y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="e8331-234">On hello Roles dialog, select hello role that you have created and click **Add**.</span></span>
      
       ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="e8331-236">m.</span><span class="sxs-lookup"><span data-stu-id="e8331-236">m.</span></span> <span data-ttu-id="e8331-237">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e8331-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="e8331-238">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="e8331-238">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e8331-239">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="e8331-239">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e8331-240">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e8331-240">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e8331-241">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8331-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="e8331-242">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="e8331-242">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="e8331-244">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e8331-244">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8331-245">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="e8331-245">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="e8331-247">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e8331-247">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e8331-249">En la parte superior de saludo del cuadro de diálogo de hello, haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e8331-249">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e8331-251">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="e8331-251">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e8331-253">a.</span><span class="sxs-lookup"><span data-stu-id="e8331-253">a.</span></span> <span data-ttu-id="e8331-254">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e8331-254">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e8331-255">b.</span><span class="sxs-lookup"><span data-stu-id="e8331-255">b.</span></span> <span data-ttu-id="e8331-256">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e8331-256">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e8331-257">c.</span><span class="sxs-lookup"><span data-stu-id="e8331-257">c.</span></span> <span data-ttu-id="e8331-258">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e8331-258">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e8331-259">d.</span><span class="sxs-lookup"><span data-stu-id="e8331-259">d.</span></span> <span data-ttu-id="e8331-260">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e8331-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="e8331-261">Creación de un usuario de prueba de NetSuite</span><span class="sxs-lookup"><span data-stu-id="e8331-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="e8331-262">En esta sección se creará un usuario llamado Britta Simon en NetSuite.</span><span class="sxs-lookup"><span data-stu-id="e8331-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="e8331-263">NetSuite admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e8331-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="e8331-264">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="e8331-264">There is no action item for you in this section.</span></span> <span data-ttu-id="e8331-265">Si un usuario ya no existe en Netsuite, se crea uno nuevo cuando intente tooaccess Netsuite.</span><span class="sxs-lookup"><span data-stu-id="e8331-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt tooaccess Netsuite.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e8331-266">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8331-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e8331-267">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="e8331-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetsuite.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="e8331-269">**tooassign Britta Simon tooNetsuite, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e8331-269">**tooassign Britta Simon tooNetsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8331-270">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e8331-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e8331-272">En la lista de aplicaciones de hello, seleccione **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="e8331-272">In hello applications list, select **Netsuite**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="e8331-274">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e8331-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="e8331-276">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e8331-276">Click **Add** button.</span></span> <span data-ttu-id="e8331-277">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e8331-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="e8331-279">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8331-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e8331-280">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e8331-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e8331-281">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e8331-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e8331-282">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="e8331-282">Testing single sign-on</span></span>

<span data-ttu-id="e8331-283">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e8331-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e8331-284">tootest Hola de su inicio de sesión configuración de inicio único, abra Panel de acceso en [https://myapps.microsoft.com](https://myapps.microsoft.com/), inicie sesión en la cuenta de prueba de Hola y haga clic en **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="e8331-284">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into hello test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e8331-285">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e8331-285">Additional resources</span></span>

* [<span data-ttu-id="e8331-286">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e8331-286">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e8331-287">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e8331-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="e8331-288">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="e8331-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

