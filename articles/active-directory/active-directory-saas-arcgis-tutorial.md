---
title: "Tutorial: Integración de Azure Active Directory con ArcGIS Online | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y ArcGIS Online."
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
ms.openlocfilehash: df72270ca6443b456c079b22425f1660aa522389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="3de9d-103">Tutorial: Integración de Azure Active Directory con ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="3de9d-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="3de9d-104">En este tutorial, obtendrá información sobre cómo integrar ArcGIS Online con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3de9d-104">In this tutorial, you learn how to integrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3de9d-105">La integración de ArcGIS Online con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3de9d-105">Integrating ArcGIS Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3de9d-106">En Azure AD puede controlar quién tiene acceso a ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="3de9d-106">You can control in Azure AD who has access to ArcGIS Online</span></span>
- <span data-ttu-id="3de9d-107">Puede permitir que los usuarios inicien sesión automáticamente en ArcGIS Online (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3de9d-107">You can enable your users to automatically get signed-on to ArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3de9d-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3de9d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3de9d-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3de9d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with ArcGIS Online, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="3de9d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3de9d-110">Prerequisites</span></span>

<span data-ttu-id="3de9d-111">Para configurar la integración de Azure AD con ArcGIS Online, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3de9d-111">To configure Azure AD integration with ArcGIS Online, you need the following items:</span></span>

- <span data-ttu-id="3de9d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3de9d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3de9d-113">Una suscripción habilitada para el inicio de sesión único en ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="3de9d-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3de9d-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3de9d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3de9d-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3de9d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3de9d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3de9d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3de9d-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3de9d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3de9d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3de9d-118">Scenario description</span></span>
<span data-ttu-id="3de9d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3de9d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3de9d-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="3de9d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3de9d-121">Incorporación de ArcGIS Online desde la galería</span><span class="sxs-lookup"><span data-stu-id="3de9d-121">Adding ArcGIS Online from the gallery</span></span>
2. <span data-ttu-id="3de9d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3de9d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-the-gallery"></a><span data-ttu-id="3de9d-123">Incorporación de ArcGIS Online desde la galería</span><span class="sxs-lookup"><span data-stu-id="3de9d-123">Adding ArcGIS Online from the gallery</span></span>
<span data-ttu-id="3de9d-124">Para configurar la integración de ArcGIS Online en Azure AD, deberá agregar ArcGIS Online desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="3de9d-124">To configure the integration of ArcGIS Online into Azure AD, you need to add ArcGIS Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3de9d-125">**Para agregar ArcGIS Online desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="3de9d-125">**To add ArcGIS Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3de9d-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3de9d-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3de9d-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="3de9d-131">Haga clic en el botón **Nueva aplicación** en la parte superior del cuadro de diálogo para agregar la nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="3de9d-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="3de9d-133">En el cuadro de búsqueda, escriba **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-133">In the search box, type **ArcGIS Online**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="3de9d-135">En el panel de resultados, seleccione **ArcGIS Online** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3de9d-135">In the results panel, select **ArcGIS Online**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3de9d-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3de9d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3de9d-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ArcGIS Online con un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3de9d-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3de9d-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de ArcGIS Online para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3de9d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ArcGIS Online is to a user in Azure AD.</span></span> <span data-ttu-id="3de9d-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="3de9d-140">In other words, a link relationship between an Azure AD user and the related user in ArcGIS Online needs to be established.</span></span>

<span data-ttu-id="3de9d-141">Para establecer la relación de vínculo, en ArcGIS Online, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="3de9d-142">Para configurar y probar el inicio de sesión único de Azure AD con ArcGIS Online, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3de9d-142">To configure and test Azure AD single sign-on with ArcGIS Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3de9d-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="3de9d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3de9d-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3de9d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3de9d-145">**[Creación de un usuario de prueba de ArcGIS Online](#creating-an-arcgis-online-test-user)**: para tener un homólogo de Britta Simon en ArcGIS Online que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3de9d-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - to have a counterpart of Britta Simon in ArcGIS Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3de9d-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3de9d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3de9d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3de9d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3de9d-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3de9d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3de9d-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="3de9d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="3de9d-150">**Para configurar el inicio de sesión único de Azure AD con ArcGIS Online, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="3de9d-150">**To configure Azure AD single sign-on with ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="3de9d-151">En Azure Portal, en la página de integración de la aplicación **ArcGIS Online**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-151">In the Azure portal, on the **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="3de9d-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3de9d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="3de9d-155">En la sección **Dominio y direcciones URL de ArcGIS Online**, lleve a cabo el paso siguiente:</span><span class="sxs-lookup"><span data-stu-id="3de9d-155">On the **ArcGIS Online Domain and URLs** section, perform the following step:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="3de9d-157">En el cuadro de texto **URL de inicio de sesión**, escriba el valor con el siguiente patrón: `https://<company>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="3de9d-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3de9d-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="3de9d-158">This value is not the real.</span></span> <span data-ttu-id="3de9d-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="3de9d-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="3de9d-160">Póngase en contacto con el [equipo de soporte técnico de ArcGIS Online](http://support.esri.com/) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="3de9d-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) to get this value.</span></span> 

4. <span data-ttu-id="3de9d-161">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3de9d-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="3de9d-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3de9d-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3de9d-165">En otra ventana del explorador web, inicie sesión en como administrador en el sitio de la compañía de ArcGIS.</span><span class="sxs-lookup"><span data-stu-id="3de9d-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="3de9d-166">Haga clic en **EDITAR CONFIGURACIÓN**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="3de9d-167">![Editar configuración](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Editar configuración")</span><span class="sxs-lookup"><span data-stu-id="3de9d-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="3de9d-168">Haga clic en **Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-168">Click **Security**.</span></span>

    <span data-ttu-id="3de9d-169">![Seguridad](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Seguridad")</span><span class="sxs-lookup"><span data-stu-id="3de9d-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="3de9d-170">En **Inicios de sesión de la empresa**, haga clic en **ESTABLECER PROVEEDOR DE IDENTIDADES**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="3de9d-171">![Enterprise Logins (Inicios de sesión de la empresa)](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins (Inicios de sesión de la empresa)")</span><span class="sxs-lookup"><span data-stu-id="3de9d-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="3de9d-172">En la sección **Configurar proveedor de identidades** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3de9d-172">On the **Set Identity Provider** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="3de9d-173">![Set Identity Provider (Establecer proveedor de identidades)](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider (Establecer proveedor de identidades)")</span><span class="sxs-lookup"><span data-stu-id="3de9d-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="3de9d-174">a.</span><span class="sxs-lookup"><span data-stu-id="3de9d-174">a.</span></span> <span data-ttu-id="3de9d-175">En el cuadro de texto **Nombre**, escriba el nombre de la organización.</span><span class="sxs-lookup"><span data-stu-id="3de9d-175">In the **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="3de9d-176">b.</span><span class="sxs-lookup"><span data-stu-id="3de9d-176">b.</span></span> <span data-ttu-id="3de9d-177">En **Metadata for the Enterprise Identity Provider will be supplied using** (Los metadatos para el proveedor de identidades de la empresa se proporcionarán con), seleccione **A File** (Un archivo).</span><span class="sxs-lookup"><span data-stu-id="3de9d-177">For **Metadata for the Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="3de9d-178">c.</span><span class="sxs-lookup"><span data-stu-id="3de9d-178">c.</span></span> <span data-ttu-id="3de9d-179">Haga clic en **Choose file**(Elegir archivo) para cargar el archivo de metadatos descargado.</span><span class="sxs-lookup"><span data-stu-id="3de9d-179">To upload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="3de9d-180">d.</span><span class="sxs-lookup"><span data-stu-id="3de9d-180">d.</span></span> <span data-ttu-id="3de9d-181">Haga clic en **ESTABLECER PROVEEDOR DE IDENTIDADES**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="3de9d-182">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3de9d-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3de9d-183">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3de9d-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3de9d-184">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3de9d-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3de9d-185">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3de9d-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="3de9d-186">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3de9d-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="3de9d-188">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="3de9d-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3de9d-189">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3de9d-191">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="3de9d-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3de9d-193">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3de9d-195">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="3de9d-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3de9d-197">a.</span><span class="sxs-lookup"><span data-stu-id="3de9d-197">a.</span></span> <span data-ttu-id="3de9d-198">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3de9d-199">b.</span><span class="sxs-lookup"><span data-stu-id="3de9d-199">b.</span></span> <span data-ttu-id="3de9d-200">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3de9d-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="3de9d-201">c.</span><span class="sxs-lookup"><span data-stu-id="3de9d-201">c.</span></span> <span data-ttu-id="3de9d-202">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3de9d-203">d.</span><span class="sxs-lookup"><span data-stu-id="3de9d-203">d.</span></span> <span data-ttu-id="3de9d-204">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="3de9d-205">Creación de un usuario de prueba de ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="3de9d-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="3de9d-206">Para permitir que los usuarios de Azure AD inicien sesión en ArcGIS Online, tienen que aprovisionarse en ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="3de9d-206">In order to enable Azure AD users to log into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="3de9d-207">En el caso de ArcGIS Online, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="3de9d-207">In the case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="3de9d-208">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="3de9d-208">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="3de9d-209">Inicie sesión en su inquilino de **ArcGIS** .</span><span class="sxs-lookup"><span data-stu-id="3de9d-209">Log in to your **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="3de9d-210">Haga clic en **INVITAR A MIEMBROS**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="3de9d-211">![Invitar a miembros](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invitar a miembros")</span><span class="sxs-lookup"><span data-stu-id="3de9d-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="3de9d-212">Seleccione **Agregar miembros automáticamente sin enviar un correo electrónico** y luego haga clic en **SIGUIENTE**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="3de9d-213">![Agregar miembros automáticamente](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Agregar miembros automáticamente")</span><span class="sxs-lookup"><span data-stu-id="3de9d-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="3de9d-214">En la página de diálogo **Miembros** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3de9d-214">On the **Members** dialog page, perform the following steps:</span></span>
   
     <span data-ttu-id="3de9d-215">![Agregar y revisar](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Agregar y revisar")</span><span class="sxs-lookup"><span data-stu-id="3de9d-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="3de9d-216">a.</span><span class="sxs-lookup"><span data-stu-id="3de9d-216">a.</span></span> <span data-ttu-id="3de9d-217">Escriba los valores de **correo electrónico**, **nombre** y **apellido** de una cuenta de AAD válida que desea aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="3de9d-217">Enter the **Email**, **First Name**, and **Last Name** of a valid AAD account you want to provision.</span></span>
  
     <span data-ttu-id="3de9d-218">b.</span><span class="sxs-lookup"><span data-stu-id="3de9d-218">b.</span></span> <span data-ttu-id="3de9d-219">Haga clic en **AGREGAR Y REVISAR**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="3de9d-220">Revise los datos que ha escrito y luego haga clic en **AGREGAR MIEMBROS**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-220">Review the data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="3de9d-221">![Agregar miembros](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Agregar miembros")</span><span class="sxs-lookup"><span data-stu-id="3de9d-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="3de9d-222">El titular de la cuenta de Azure Active Directory recibirá un mensaje de correo y seguirá un vínculo para confirmar su cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="3de9d-222">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3de9d-223">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3de9d-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3de9d-224">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="3de9d-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ArcGIS Online.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3de9d-226">**Para asignar a Britta Simon a ArcGIS Online, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="3de9d-226">**To assign Britta Simon to ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="3de9d-227">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3de9d-229">En la lista de aplicaciones. seleccione **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-229">In the applications list, select **ArcGIS Online**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="3de9d-231">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3de9d-233">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-233">Click **Add** button.</span></span> <span data-ttu-id="3de9d-234">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3de9d-236">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="3de9d-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3de9d-237">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3de9d-238">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3de9d-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3de9d-239">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3de9d-239">Testing single sign-on</span></span>

<span data-ttu-id="3de9d-240">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3de9d-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3de9d-241">Al hacer clic en el icono de ArcGIS Online en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="3de9d-241">When you click the ArcGIS Online tile in the Access Panel, you should get automatically signed-on to your ArcGIS Online application.</span></span>
<span data-ttu-id="3de9d-242">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3de9d-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3de9d-243">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3de9d-243">Additional resources</span></span>

* [<span data-ttu-id="3de9d-244">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3de9d-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3de9d-245">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3de9d-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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

