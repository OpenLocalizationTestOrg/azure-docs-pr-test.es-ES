---
title: "Tutorial: Integración de Azure Active Directory con Tableau Online | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Tableau Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 443fab1198a91a4d5749e6421f7b8603fc75a81e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="9989c-103">Tutorial: Integración de Azure Active Directory con Tableau Online</span><span class="sxs-lookup"><span data-stu-id="9989c-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="9989c-104">En este tutorial, obtendrá información sobre cómo integrar Tableau Online con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9989c-104">In this tutorial, you learn how to integrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9989c-105">Integrar Tableau Online con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9989c-105">Integrating Tableau Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9989c-106">Puede controlar en Azure AD quién tiene acceso a Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="9989c-106">You can control in Azure AD who has access to Tableau Online</span></span>
- <span data-ttu-id="9989c-107">Puede permitir que los usuarios inicien sesión automáticamente en Tableau Online (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9989c-107">You can enable your users to automatically get signed-on to Tableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9989c-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9989c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9989c-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9989c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9989c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9989c-110">Prerequisites</span></span>

<span data-ttu-id="9989c-111">Para configurar la integración de Azure AD con Tableau Online, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9989c-111">To configure Azure AD integration with Tableau Online, you need the following items:</span></span>

- <span data-ttu-id="9989c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9989c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9989c-113">Una suscripción habilitada para el inicio de sesión único en Tableau Online</span><span class="sxs-lookup"><span data-stu-id="9989c-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9989c-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9989c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9989c-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9989c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9989c-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9989c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9989c-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9989c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9989c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9989c-118">Scenario description</span></span>
<span data-ttu-id="9989c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9989c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9989c-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="9989c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9989c-121">Incorporación de Tableau Online desde la galería</span><span class="sxs-lookup"><span data-stu-id="9989c-121">Adding Tableau Online from the gallery</span></span>
2. <span data-ttu-id="9989c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9989c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-the-gallery"></a><span data-ttu-id="9989c-123">Incorporación de Tableau Online desde la galería</span><span class="sxs-lookup"><span data-stu-id="9989c-123">Adding Tableau Online from the gallery</span></span>
<span data-ttu-id="9989c-124">Para configurar la integración de Tableau Online en Azure AD, será preciso que agregue Tableau Online desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="9989c-124">To configure the integration of Tableau Online into Azure AD, you need to add Tableau Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9989c-125">**Para agregar Tableau Online desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9989c-125">**To add Tableau Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9989c-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9989c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9989c-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9989c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9989c-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9989c-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9989c-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9989c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9989c-133">En el cuadro de búsqueda, escriba **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="9989c-133">In the search box, type **Tableau Online**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. <span data-ttu-id="9989c-135">En el panel de resultados, seleccione **Tableau Online** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9989c-135">In the results panel, select **Tableau Online**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9989c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9989c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9989c-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Tableau Online con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9989c-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9989c-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Tableau Online para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9989c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Online is to a user in Azure AD.</span></span> <span data-ttu-id="9989c-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="9989c-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Online needs to be established.</span></span>

<span data-ttu-id="9989c-141">Para establecer la relación de vínculo, en Tableau Online, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="9989c-141">In Tableau Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9989c-142">Para configurar y probar el inicio de sesión único de Azure AD con Tableau Online, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9989c-142">To configure and test Azure AD single sign-on with Tableau Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9989c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="9989c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9989c-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9989c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9989c-145">**[Creación de un usuario de prueba de Tableau Online](#creating-a-tableau-online-test-user)** : para tener un homólogo de Britta Simon en Tableau Online vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9989c-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - to have a counterpart of Britta Simon in Tableau Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9989c-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9989c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9989c-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9989c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9989c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9989c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9989c-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="9989c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="9989c-150">**Para configurar el inicio de sesión único de Azure AD con Tableau Online, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9989c-150">**To configure Azure AD single sign-on with Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="9989c-151">En Azure Portal, en la página de integración de la aplicación **Tableau Online**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9989c-151">In the Azure portal, on the **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9989c-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9989c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. <span data-ttu-id="9989c-155">En la sección **Tableau Online Domain and URLs** (Dominio y direcciones URL de Tableau Online), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9989c-155">On the **Tableau Online Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="9989c-157">a.</span><span class="sxs-lookup"><span data-stu-id="9989c-157">a.</span></span> <span data-ttu-id="9989c-158">En el cuadro de texto **URL de inicio de sesión**, escriba la dirección URL: `https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="9989c-158">In the **Sign-on URL** textbox, type the URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="9989c-159">b.</span><span class="sxs-lookup"><span data-stu-id="9989c-159">b.</span></span> <span data-ttu-id="9989c-160">En el cuadro de texto **Identificador**, escriba la dirección URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="9989c-160">In the **Identifier** textbox, type the URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span></span>

4. <span data-ttu-id="9989c-161">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9989c-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. <span data-ttu-id="9989c-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9989c-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9989c-165">En una ventana de explorador diferente, inicie sesión en su aplicación de Tableau Online como administrador.</span><span class="sxs-lookup"><span data-stu-id="9989c-165">In a different browser window, sign-on to your Tableau Online application.</span></span> <span data-ttu-id="9989c-166">Vaya a **Settings** (Configuración) y luego a **Authentication** (Autenticación).</span><span class="sxs-lookup"><span data-stu-id="9989c-166">Go to **Settings** and then **Authentication**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. <span data-ttu-id="9989c-168">Para habilitar SAML, en la sección **Tipos de autenticación**,</span><span class="sxs-lookup"><span data-stu-id="9989c-168">To enable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="9989c-169">marque la casilla **Inicio de sesión único con SAML**.</span><span class="sxs-lookup"><span data-stu-id="9989c-169">Check the **Single sign-on with SAML** checkbox.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. <span data-ttu-id="9989c-171">Desplácese hacia abajo hasta la sección **Importar archivo de metadatos en Tableau Online** .</span><span class="sxs-lookup"><span data-stu-id="9989c-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="9989c-172">Haga clic en Examinar e importe el archivo de metadatos que ha descargado desde Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9989c-172">Click Browse and import the metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="9989c-173">A continuación, haga clic en **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="9989c-173">Then, click **Apply**.</span></span>
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. <span data-ttu-id="9989c-175">En la sección **Match assertions** (Aserciones de coincidencia), inserte el nombre de aserción del proveedor de identidades correspondiente para la **dirección de correo electrónico**, el **nombre** y los **apellidos**.</span><span class="sxs-lookup"><span data-stu-id="9989c-175">In the **Match assertions** section, insert the corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="9989c-176">Para obtener esta información a partir de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="9989c-176">To get this information from Azure AD:</span></span> 
  
    <span data-ttu-id="9989c-177">a.</span><span class="sxs-lookup"><span data-stu-id="9989c-177">a.</span></span> <span data-ttu-id="9989c-178">Vaya a la página de integración de aplicaciones de **Tableau Online** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9989c-178">In the Azure portal, go on the **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="9989c-179">b.</span><span class="sxs-lookup"><span data-stu-id="9989c-179">b.</span></span> <span data-ttu-id="9989c-180">En la sección de atributos, seleccione la casilla **"Ver y editar todos los demás atributos de usuario"**.</span><span class="sxs-lookup"><span data-stu-id="9989c-180">In the attributes section, Select the **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="9989c-182">c.</span><span class="sxs-lookup"><span data-stu-id="9989c-182">c.</span></span> <span data-ttu-id="9989c-183">Copie el valor del espacio de nombres de estos atributos: givenname, email y surname mediante los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9989c-183">Copy the namespace value for these attributes: givenname, email and surname by using the following steps:</span></span>

   ![Inicio de sesión único de Azure AD ](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="9989c-185">d.</span><span class="sxs-lookup"><span data-stu-id="9989c-185">d.</span></span> <span data-ttu-id="9989c-186">Haga clic en el valor **user.givenname**</span><span class="sxs-lookup"><span data-stu-id="9989c-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="9989c-187">e.</span><span class="sxs-lookup"><span data-stu-id="9989c-187">e.</span></span> <span data-ttu-id="9989c-188">Copie el valor del cuadro de texto **espacio de nombres**.</span><span class="sxs-lookup"><span data-stu-id="9989c-188">Copy the value from the **namespace** textbox.</span></span>

   ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="9989c-190">f.</span><span class="sxs-lookup"><span data-stu-id="9989c-190">f.</span></span> <span data-ttu-id="9989c-191">Para copiar los valores del espacio de nombres del correo electrónico y el apellido, siga los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="9989c-191">To copy the namesapce values for the email and surname follow the preceding steps.</span></span>

    <span data-ttu-id="9989c-192">g.</span><span class="sxs-lookup"><span data-stu-id="9989c-192">g.</span></span> <span data-ttu-id="9989c-193">Abra la aplicación Tableau Online y establezca la sección **Tableau Online Attributes** (Atributos de Tableau Online) como sigue:</span><span class="sxs-lookup"><span data-stu-id="9989c-193">Switch to the Tableau Online application, then set the **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="9989c-194">Correo electrónico: **mail** o **userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="9989c-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="9989c-195">Nombre: **givenname**</span><span class="sxs-lookup"><span data-stu-id="9989c-195">First name: **givenname**</span></span>
     * <span data-ttu-id="9989c-196">Apellidos: **surname**</span><span class="sxs-lookup"><span data-stu-id="9989c-196">Last name: **surname**</span></span>
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> <span data-ttu-id="9989c-198">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9989c-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9989c-199">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="9989c-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9989c-200">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9989c-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9989c-201">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9989c-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="9989c-202">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9989c-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9989c-204">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="9989c-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9989c-205">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9989c-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9989c-207">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9989c-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9989c-209">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9989c-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9989c-211">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9989c-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9989c-213">a.</span><span class="sxs-lookup"><span data-stu-id="9989c-213">a.</span></span> <span data-ttu-id="9989c-214">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9989c-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9989c-215">b.</span><span class="sxs-lookup"><span data-stu-id="9989c-215">b.</span></span> <span data-ttu-id="9989c-216">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9989c-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9989c-217">c.</span><span class="sxs-lookup"><span data-stu-id="9989c-217">c.</span></span> <span data-ttu-id="9989c-218">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9989c-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9989c-219">d.</span><span class="sxs-lookup"><span data-stu-id="9989c-219">d.</span></span> <span data-ttu-id="9989c-220">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9989c-220">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="9989c-221">Crear un usuario de prueba de Tableau Online</span><span class="sxs-lookup"><span data-stu-id="9989c-221">Creating a Tableau Online test user</span></span>

<span data-ttu-id="9989c-222">En esta sección, creará una usuaria llamada Britta Simon en Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="9989c-222">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="9989c-223">En **Tableau Online**, haga clic en **Settings** (Configuración) y en la sección **Authentication** (Autenticación).</span><span class="sxs-lookup"><span data-stu-id="9989c-223">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="9989c-224">Desplácese hacia abajo a la sección **Seleccionar usuarios** .</span><span class="sxs-lookup"><span data-stu-id="9989c-224">Scroll down to **Select Users** section.</span></span> <span data-ttu-id="9989c-225">Haga clic en **Add users** (Agregar usuarios) y en **Enter Email Addresses** (Especificar direcciones de correo electrónico).</span><span class="sxs-lookup"><span data-stu-id="9989c-225">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="9989c-227">Seleccione **Add users for single sign-on (SSO) authentication**[Agregar usuarios para la autenticación mediante inicio de sesión único (SSO)].</span><span class="sxs-lookup"><span data-stu-id="9989c-227">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="9989c-228">En el cuadro de texto **Especificar direcciones de correo electrónico** agregue britta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="9989c-228">In the **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="9989c-230">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9989c-230">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9989c-231">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9989c-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9989c-232">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="9989c-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Online.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9989c-234">**Para asignar Britta Simon a Tableau Online, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9989c-234">**To assign Britta Simon to Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="9989c-235">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9989c-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9989c-237">En la lista de aplicaciones, seleccione **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="9989c-237">In the applications list, select **Tableau Online**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. <span data-ttu-id="9989c-239">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9989c-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9989c-241">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9989c-241">Click **Add** button.</span></span> <span data-ttu-id="9989c-242">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9989c-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9989c-244">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="9989c-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9989c-245">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9989c-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9989c-246">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9989c-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9989c-247">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9989c-247">Testing single sign-on</span></span>

<span data-ttu-id="9989c-248">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9989c-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="9989c-249">Al hacer clic en el icono de Tableau Online en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="9989c-249">When you click the Tableau Online tile in the Access Panel, you should get automatically signed-on to your Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9989c-250">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9989c-250">Additional resources</span></span>

* [<span data-ttu-id="9989c-251">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9989c-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9989c-252">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9989c-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

