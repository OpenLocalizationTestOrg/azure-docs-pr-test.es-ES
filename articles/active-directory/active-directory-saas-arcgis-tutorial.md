---
title: "Tutorial: Integración de Azure Active Directory con ArcGIS Online | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ArcGIS en línea."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: f3dd55d798cf3256fb2758e011f33946baa405ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="d828b-103">Tutorial: Integración de Azure Active Directory con ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="d828b-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="d828b-104">En este tutorial, aprenderá cómo toointegrate ArcGIS Online con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d828b-104">In this tutorial, you learn how toointegrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d828b-105">Integración de ArcGIS Online con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d828b-105">Integrating ArcGIS Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d828b-106">Puede controlar en Azure AD que tenga acceso tooArcGIS en línea</span><span class="sxs-lookup"><span data-stu-id="d828b-106">You can control in Azure AD who has access tooArcGIS Online</span></span>
- <span data-ttu-id="d828b-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooArcGIS en línea (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d828b-107">You can enable your users tooautomatically get signed-on tooArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d828b-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d828b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d828b-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d828b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with ArcGIS Online, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="d828b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d828b-110">Prerequisites</span></span>

<span data-ttu-id="d828b-111">tooconfigure integración de Azure AD con ArcGIS en línea, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d828b-111">tooconfigure Azure AD integration with ArcGIS Online, you need hello following items:</span></span>

- <span data-ttu-id="d828b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d828b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d828b-113">Una suscripción habilitada para el inicio de sesión único en ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="d828b-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d828b-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="d828b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d828b-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="d828b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d828b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d828b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d828b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d828b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d828b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="d828b-118">Scenario description</span></span>
<span data-ttu-id="d828b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="d828b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d828b-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="d828b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d828b-121">Agregar ArcGIS en línea desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="d828b-121">Adding ArcGIS Online from hello gallery</span></span>
2. <span data-ttu-id="d828b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d828b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-hello-gallery"></a><span data-ttu-id="d828b-123">Agregar ArcGIS en línea desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="d828b-123">Adding ArcGIS Online from hello gallery</span></span>
<span data-ttu-id="d828b-124">integración de hello tooconfigure de ArcGIS en línea en Azure AD, deberá tooadd ArcGIS en pantalla de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="d828b-124">tooconfigure hello integration of ArcGIS Online into Azure AD, you need tooadd ArcGIS Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d828b-125">**tooadd ArcGIS en línea desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d828b-125">**tooadd ArcGIS Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d828b-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="d828b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d828b-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="d828b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d828b-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d828b-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="d828b-131">Haga clic en **nueva aplicación** botón en la parte superior de Hola de nueva aplicación de hello diálogo tooadd.</span><span class="sxs-lookup"><span data-stu-id="d828b-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="d828b-133">En el cuadro de búsqueda de hello, escriba **ArcGIS en línea**.</span><span class="sxs-lookup"><span data-stu-id="d828b-133">In hello search box, type **ArcGIS Online**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="d828b-135">En el panel de resultados de hello, seleccione **ArcGIS en línea**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d828b-135">In hello results panel, select **ArcGIS Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d828b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d828b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d828b-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ArcGIS Online con un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d828b-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d828b-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en ArcGIS en línea es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d828b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ArcGIS Online is tooa user in Azure AD.</span></span> <span data-ttu-id="d828b-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en ArcGIS en línea debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="d828b-140">In other words, a link relationship between an Azure AD user and hello related user in ArcGIS Online needs toobe established.</span></span>

<span data-ttu-id="d828b-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en ArcGIS en línea.</span><span class="sxs-lookup"><span data-stu-id="d828b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="d828b-142">tooconfigure y prueba de inicio de sesión único en Azure AD con ArcGIS en línea, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d828b-142">tooconfigure and test Azure AD single sign-on with ArcGIS Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d828b-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="d828b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d828b-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d828b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d828b-145">**[Creación de un usuario de prueba en pantalla de ArcGIS](#creating-an-arcgis-online-test-user)**  -toohave un equivalente de Britta Simon en ArcGIS Online que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="d828b-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - toohave a counterpart of Britta Simon in ArcGIS Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d828b-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d828b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d828b-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="d828b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d828b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d828b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d828b-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación ArcGIS en línea.</span><span class="sxs-lookup"><span data-stu-id="d828b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="d828b-150">**inicio de sesión único en tooconfigure Azure AD con ArcGIS Online, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d828b-150">**tooconfigure Azure AD single sign-on with ArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="d828b-151">En el portal de Azure, en Hola Hola **ArcGIS en línea** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d828b-151">In hello Azure portal, on hello **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="d828b-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d828b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="d828b-155">En hello **ArcGIS en pantalla de dominio y las direcciones URL** sección, lleve a cabo Hola siguiendo el paso:</span><span class="sxs-lookup"><span data-stu-id="d828b-155">On hello **ArcGIS Online Domain and URLs** section, perform hello following step:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="d828b-157">Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello mediante Hola sigue el patrón:`https://<company>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="d828b-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d828b-158">Este valor no es hello real.</span><span class="sxs-lookup"><span data-stu-id="d828b-158">This value is not hello real.</span></span> <span data-ttu-id="d828b-159">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="d828b-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="d828b-160">Póngase en contacto con [equipo de soporte técnico de cliente en línea de ArcGIS](http://support.esri.com/) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="d828b-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) tooget this value.</span></span> 

4. <span data-ttu-id="d828b-161">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d828b-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="d828b-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="d828b-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d828b-165">En otra ventana del explorador web, inicie sesión en como administrador en el sitio de la compañía de ArcGIS.</span><span class="sxs-lookup"><span data-stu-id="d828b-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="d828b-166">Haga clic en **EDITAR CONFIGURACIÓN**.</span><span class="sxs-lookup"><span data-stu-id="d828b-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="d828b-167">![Editar configuración](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Editar configuración")</span><span class="sxs-lookup"><span data-stu-id="d828b-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="d828b-168">Haga clic en **Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="d828b-168">Click **Security**.</span></span>

    <span data-ttu-id="d828b-169">![Seguridad](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Seguridad")</span><span class="sxs-lookup"><span data-stu-id="d828b-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="d828b-170">En **Inicios de sesión de la empresa**, haga clic en **ESTABLECER PROVEEDOR DE IDENTIDADES**.</span><span class="sxs-lookup"><span data-stu-id="d828b-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="d828b-171">![Enterprise Logins (Inicios de sesión de la empresa)](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins (Inicios de sesión de la empresa)")</span><span class="sxs-lookup"><span data-stu-id="d828b-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="d828b-172">En hello **definir proveedor de identidades** configuración, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="d828b-172">On hello **Set Identity Provider** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="d828b-173">![Set Identity Provider (Establecer proveedor de identidades)](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider (Establecer proveedor de identidades)")</span><span class="sxs-lookup"><span data-stu-id="d828b-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="d828b-174">a.</span><span class="sxs-lookup"><span data-stu-id="d828b-174">a.</span></span> <span data-ttu-id="d828b-175">Hola **nombre** cuadro de texto, escriba el nombre de su organización.</span><span class="sxs-lookup"><span data-stu-id="d828b-175">In hello **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="d828b-176">b.</span><span class="sxs-lookup"><span data-stu-id="d828b-176">b.</span></span> <span data-ttu-id="d828b-177">Para **metadatos para hello proveedor de identidades de empresa se proporcionarán mediante**, seleccione **un archivo**.</span><span class="sxs-lookup"><span data-stu-id="d828b-177">For **Metadata for hello Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="d828b-178">c.</span><span class="sxs-lookup"><span data-stu-id="d828b-178">c.</span></span> <span data-ttu-id="d828b-179">tooupload el archivo de metadatos descargado, haga clic en **Elegir archivo**.</span><span class="sxs-lookup"><span data-stu-id="d828b-179">tooupload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="d828b-180">d.</span><span class="sxs-lookup"><span data-stu-id="d828b-180">d.</span></span> <span data-ttu-id="d828b-181">Haga clic en **ESTABLECER PROVEEDOR DE IDENTIDADES**.</span><span class="sxs-lookup"><span data-stu-id="d828b-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="d828b-182">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="d828b-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d828b-183">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="d828b-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d828b-184">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d828b-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d828b-185">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d828b-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="d828b-186">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="d828b-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="d828b-188">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d828b-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d828b-189">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="d828b-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d828b-191">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="d828b-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d828b-193">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d828b-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d828b-195">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="d828b-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d828b-197">a.</span><span class="sxs-lookup"><span data-stu-id="d828b-197">a.</span></span> <span data-ttu-id="d828b-198">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d828b-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d828b-199">b.</span><span class="sxs-lookup"><span data-stu-id="d828b-199">b.</span></span> <span data-ttu-id="d828b-200">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d828b-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="d828b-201">c.</span><span class="sxs-lookup"><span data-stu-id="d828b-201">c.</span></span> <span data-ttu-id="d828b-202">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="d828b-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d828b-203">d.</span><span class="sxs-lookup"><span data-stu-id="d828b-203">d.</span></span> <span data-ttu-id="d828b-204">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d828b-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="d828b-205">Creación de un usuario de prueba de ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="d828b-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="d828b-206">En orden tooenable toolog de los usuarios de Azure AD en ArcGIS en línea, se les deben aprovisionar en ArcGIS en línea.</span><span class="sxs-lookup"><span data-stu-id="d828b-206">In order tooenable Azure AD users toolog into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="d828b-207">En caso de hello de ArcGIS en línea, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="d828b-207">In hello case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="d828b-208">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d828b-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="d828b-209">Inicie sesión en tooyour **ArcGIS** inquilino.</span><span class="sxs-lookup"><span data-stu-id="d828b-209">Log in tooyour **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="d828b-210">Haga clic en **INVITAR A MIEMBROS**.</span><span class="sxs-lookup"><span data-stu-id="d828b-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="d828b-211">![Invitar a miembros](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invitar a miembros")</span><span class="sxs-lookup"><span data-stu-id="d828b-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="d828b-212">Seleccione **Agregar miembros automáticamente sin enviar un correo electrónico** y luego haga clic en **SIGUIENTE**.</span><span class="sxs-lookup"><span data-stu-id="d828b-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="d828b-213">![Agregar miembros automáticamente](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Agregar miembros automáticamente")</span><span class="sxs-lookup"><span data-stu-id="d828b-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="d828b-214">En hello **miembros** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="d828b-214">On hello **Members** dialog page, perform hello following steps:</span></span>
   
     <span data-ttu-id="d828b-215">![Agregar y revisar](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Agregar y revisar")</span><span class="sxs-lookup"><span data-stu-id="d828b-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="d828b-216">a.</span><span class="sxs-lookup"><span data-stu-id="d828b-216">a.</span></span> <span data-ttu-id="d828b-217">Escriba hello **correo electrónico**, **nombre**, y **Last Name** de una cuenta válida de AAD que desee tooprovision.</span><span class="sxs-lookup"><span data-stu-id="d828b-217">Enter hello **Email**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision.</span></span>
  
     <span data-ttu-id="d828b-218">b.</span><span class="sxs-lookup"><span data-stu-id="d828b-218">b.</span></span> <span data-ttu-id="d828b-219">Haga clic en **AGREGAR Y REVISAR**.</span><span class="sxs-lookup"><span data-stu-id="d828b-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="d828b-220">Revisar los datos de Hola que ha escrito y, a continuación, haga clic en **agregar miembros**.</span><span class="sxs-lookup"><span data-stu-id="d828b-220">Review hello data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="d828b-221">![Agregar miembros](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Agregar miembros")</span><span class="sxs-lookup"><span data-stu-id="d828b-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="d828b-222">titular de la cuenta de Hello Azure Active Directory recibirá un correo electrónico y seguir un vínculo tooconfirm su cuenta antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="d828b-222">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d828b-223">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d828b-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d828b-224">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooArcGIS en línea.</span><span class="sxs-lookup"><span data-stu-id="d828b-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooArcGIS Online.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="d828b-226">**tooassign Britta Simon tooArcGIS en línea, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d828b-226">**tooassign Britta Simon tooArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="d828b-227">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d828b-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="d828b-229">En la lista de aplicaciones de hello, seleccione **ArcGIS en línea**.</span><span class="sxs-lookup"><span data-stu-id="d828b-229">In hello applications list, select **ArcGIS Online**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="d828b-231">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d828b-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="d828b-233">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d828b-233">Click **Add** button.</span></span> <span data-ttu-id="d828b-234">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d828b-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="d828b-236">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="d828b-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d828b-237">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d828b-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d828b-238">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d828b-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d828b-239">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="d828b-239">Testing single sign-on</span></span>

<span data-ttu-id="d828b-240">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d828b-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d828b-241">Al hacer clic en icono ArcGIS Online Hola Hola Panel de acceso, deberá obtener aplicación ArcGIS Online tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="d828b-241">When you click hello ArcGIS Online tile in hello Access Panel, you should get automatically signed-on tooyour ArcGIS Online application.</span></span>
<span data-ttu-id="d828b-242">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d828b-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d828b-243">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d828b-243">Additional resources</span></span>

* [<span data-ttu-id="d828b-244">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d828b-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d828b-245">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d828b-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

