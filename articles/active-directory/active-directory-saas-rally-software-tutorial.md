---
title: "Tutorial: Integración de Azure Active Directory con Rally Software | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y Rally Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: 6481c9ef0ca71419ccfa6f7956f4702985743df3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="908cd-103">Tutorial: Integración de Azure Active Directory con Rally Software</span><span class="sxs-lookup"><span data-stu-id="908cd-103">Tutorial: Azure Active Directory integration with Rally Software</span></span>

<span data-ttu-id="908cd-104">En este tutorial, obtendrá información sobre cómo integrar Rally Software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="908cd-104">In this tutorial, you learn how to integrate Rally Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="908cd-105">La integración de Rally Software con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="908cd-105">Integrating Rally Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="908cd-106">En Azure AD puede controlar quién tiene acceso a Rally Software.</span><span class="sxs-lookup"><span data-stu-id="908cd-106">You can control in Azure AD who has access to Rally Software.</span></span>
- <span data-ttu-id="908cd-107">Puede permitir que los usuarios inicien sesión automáticamente en Rally Software (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="908cd-107">You can enable your users to automatically get signed-on to Rally Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="908cd-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="908cd-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="908cd-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="908cd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="908cd-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="908cd-110">Prerequisites</span></span>

<span data-ttu-id="908cd-111">Para configurar la integración de Azure AD con Rally Software, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="908cd-111">To configure Azure AD integration with Rally Software, you need the following items:</span></span>

- <span data-ttu-id="908cd-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="908cd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="908cd-113">Una suscripción habilitada para el inicio de sesión único en Rally Software</span><span class="sxs-lookup"><span data-stu-id="908cd-113">A Rally Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="908cd-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="908cd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="908cd-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="908cd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="908cd-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="908cd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="908cd-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="908cd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="908cd-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="908cd-118">Scenario description</span></span>
<span data-ttu-id="908cd-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="908cd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="908cd-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="908cd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="908cd-121">Incorporación de Rally Software desde la galería</span><span class="sxs-lookup"><span data-stu-id="908cd-121">Adding Rally Software from the gallery</span></span>
2. <span data-ttu-id="908cd-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="908cd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rally-software-from-the-gallery"></a><span data-ttu-id="908cd-123">Incorporación de Rally Software desde la galería</span><span class="sxs-lookup"><span data-stu-id="908cd-123">Adding Rally Software from the gallery</span></span>
<span data-ttu-id="908cd-124">Para configurar la integración de Rally Software en Azure AD, deberá agregarlo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="908cd-124">To configure the integration of Rally Software into Azure AD, you need to add Rally Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="908cd-125">**Para agregar Rally Software desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="908cd-125">**To add Rally Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="908cd-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="908cd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="908cd-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="908cd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="908cd-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="908cd-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="908cd-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="908cd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="908cd-133">En el cuadro de búsqueda, escriba **Rally Software**, seleccione **Rally Software** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="908cd-133">In the search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button to add the application.</span></span>

    ![Rally Software en la lista de resultados](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="908cd-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="908cd-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="908cd-136">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Rally Software con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="908cd-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="908cd-137">Para que el inicio de sesión único funcione, es preciso que Azure AD sepa cuál es el usuario homólogo en Rally Software de un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="908cd-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Rally Software is to a user in Azure AD.</span></span> <span data-ttu-id="908cd-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Rally Software.</span><span class="sxs-lookup"><span data-stu-id="908cd-138">In other words, a link relationship between an Azure AD user and the related user in Rally Software needs to be established.</span></span>

<span data-ttu-id="908cd-139">En Rally Software, asigne el valor del **nombre de usuario** en Azure AD como valor de **nombre de usuario** para establecer la relación de vínculo.</span><span class="sxs-lookup"><span data-stu-id="908cd-139">In Rally Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="908cd-140">Para configurar y probar el inicio de sesión único de Azure AD con Rally Software, debe completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="908cd-140">To configure and test Azure AD single sign-on with Rally Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="908cd-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="908cd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="908cd-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="908cd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="908cd-143">**[Creación de un usuario de prueba de Rally Software](#create-a-rally-software-test-user)**: para tener un homólogo de Britta Simon en Rally Software que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="908cd-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - to have a counterpart of Britta Simon in Rally Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="908cd-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="908cd-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="908cd-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="908cd-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="908cd-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="908cd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="908cd-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Rally Software.</span><span class="sxs-lookup"><span data-stu-id="908cd-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rally Software application.</span></span>

<span data-ttu-id="908cd-148">**Para configurar el inicio de sesión único de Azure AD con Rally Software, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="908cd-148">**To configure Azure AD single sign-on with Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="908cd-149">En Azure Portal, en la página de integración de la aplicación **Rally Software**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="908cd-149">In the Azure portal, on the **Rally Software** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="908cd-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="908cd-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. <span data-ttu-id="908cd-153">En la sección **Dominio y direcciones URL de Rally Software**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="908cd-153">On the **Rally Software Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    <span data-ttu-id="908cd-155">a.</span><span class="sxs-lookup"><span data-stu-id="908cd-155">a.</span></span> <span data-ttu-id="908cd-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<tenant-name>.rally.com`.</span><span class="sxs-lookup"><span data-stu-id="908cd-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    <span data-ttu-id="908cd-157">b.</span><span class="sxs-lookup"><span data-stu-id="908cd-157">b.</span></span> <span data-ttu-id="908cd-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="908cd-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="908cd-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="908cd-159">These values are not real.</span></span> <span data-ttu-id="908cd-160">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="908cd-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="908cd-161">Póngase en contacto con el [equipo de soporte de cliente de Rally Software](https://help.rallydev.com/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="908cd-161">Contact [Rally Software Client support team](https://help.rallydev.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="908cd-162">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="908cd-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. <span data-ttu-id="908cd-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="908cd-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="908cd-166">En la sección **Configuración de Rally Software**, haga clic en **Configurar Rally Software** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="908cd-166">On the **Rally Software Configuration** section, click **Configure Rally Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="908cd-167">Copie los valores de **Sign-Out URL (Dirección URL de cierre de sesión) y SAML Entity ID (Identificador de entidad de SAML)** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="908cd-167">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configuración de Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. <span data-ttu-id="908cd-169">Inicie sesión en su inquilino de **Rally Software** .</span><span class="sxs-lookup"><span data-stu-id="908cd-169">Log in to your **Rally Software** tenant.</span></span>

8. <span data-ttu-id="908cd-170">En la barra de herramientas de la parte superior, haga clic en **Configuración** y seleccione **Suscripción**.</span><span class="sxs-lookup"><span data-stu-id="908cd-170">In the toolbar on the top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="908cd-171">![Suscripción](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Suscripción")</span><span class="sxs-lookup"><span data-stu-id="908cd-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span></span>

9. <span data-ttu-id="908cd-172">Haga clic en el botón **Acción**.</span><span class="sxs-lookup"><span data-stu-id="908cd-172">Click the **Action** button.</span></span> <span data-ttu-id="908cd-173">Seleccione **Editar suscripción** en la parte superior derecha de la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="908cd-173">Select **Edit Subscription** at the top right side of the toolbar.</span></span>

10. <span data-ttu-id="908cd-174">En la página de diálogo **Suscripción**, realice los pasos siguientes y haga clic en **Guardar y cerrar**:</span><span class="sxs-lookup"><span data-stu-id="908cd-174">On the **Subscription** dialog page, perform the following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="908cd-175">![Autenticación](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Autenticación")</span><span class="sxs-lookup"><span data-stu-id="908cd-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span></span>
   
    <span data-ttu-id="908cd-176">a.</span><span class="sxs-lookup"><span data-stu-id="908cd-176">a.</span></span> <span data-ttu-id="908cd-177">Seleccione **Rally o autenticación de SSO** en la lista desplegable de autenticación.</span><span class="sxs-lookup"><span data-stu-id="908cd-177">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>

    <span data-ttu-id="908cd-178">b.</span><span class="sxs-lookup"><span data-stu-id="908cd-178">b.</span></span> <span data-ttu-id="908cd-179">En el cuadro de texto **Identity provider URL** (Dirección URL del proveedor de identidad), pegue el valor del **identificador de entidad de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="908cd-179">In the **Identity provider URL** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="908cd-180">c.</span><span class="sxs-lookup"><span data-stu-id="908cd-180">c.</span></span> <span data-ttu-id="908cd-181">En el cuadro de texto **SSO Logout** (Dirección URL de inicio de sesión), pegue el valor de **dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="908cd-181">In the **SSO Logout** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="908cd-182">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="908cd-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="908cd-183">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="908cd-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="908cd-184">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="908cd-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="908cd-185">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="908cd-185">Create an Azure AD test user</span></span>

<span data-ttu-id="908cd-186">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="908cd-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="908cd-188">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="908cd-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="908cd-189">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="908cd-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="908cd-191">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="908cd-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="908cd-193">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="908cd-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="908cd-195">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="908cd-195">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    <span data-ttu-id="908cd-197">a.</span><span class="sxs-lookup"><span data-stu-id="908cd-197">a.</span></span> <span data-ttu-id="908cd-198">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="908cd-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="908cd-199">b.</span><span class="sxs-lookup"><span data-stu-id="908cd-199">b.</span></span> <span data-ttu-id="908cd-200">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="908cd-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="908cd-201">c.</span><span class="sxs-lookup"><span data-stu-id="908cd-201">c.</span></span> <span data-ttu-id="908cd-202">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="908cd-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="908cd-203">d.</span><span class="sxs-lookup"><span data-stu-id="908cd-203">d.</span></span> <span data-ttu-id="908cd-204">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="908cd-204">Click **Create**.</span></span>
 
### <a name="create-a-rally-software-test-user"></a><span data-ttu-id="908cd-205">Creación de un usuario de prueba de Rally Software</span><span class="sxs-lookup"><span data-stu-id="908cd-205">Create a Rally Software test user</span></span>

<span data-ttu-id="908cd-206">Para que los usuarios de Azure AD puedan inician sesión, deben aprovisionarse para la aplicación Rally Software con sus nombres de usuario de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="908cd-206">For Azure AD users to be able to sign in, they must be provisioned to the Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="908cd-207">**Siga estos pasos para configurar el aprovisionamiento de usuario:**</span><span class="sxs-lookup"><span data-stu-id="908cd-207">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="908cd-208">Inicie sesión en su inquilino de Rally Software.</span><span class="sxs-lookup"><span data-stu-id="908cd-208">Log in to your Rally Software tenant.</span></span>

2. <span data-ttu-id="908cd-209">Vaya a **Configuración \> USUARIOS** y haga clic en **+ Agregar nuevo**.</span><span class="sxs-lookup"><span data-stu-id="908cd-209">Go to **Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="908cd-210">![Usuarios](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="908cd-210">![Users](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Users")</span></span>

3. <span data-ttu-id="908cd-211">Escriba el nombre en el cuadro de texto Nuevo usuario y luego haga clic en **Agregar con detalles**.</span><span class="sxs-lookup"><span data-stu-id="908cd-211">Type the name in the New User textbox, and then click **Add with Details**.</span></span>

4. <span data-ttu-id="908cd-212">En la sección **Crear usuario** , lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="908cd-212">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="908cd-213">![Creación de usuarios](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Creación de usuarios")</span><span class="sxs-lookup"><span data-stu-id="908cd-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span></span>

    <span data-ttu-id="908cd-214">a.</span><span class="sxs-lookup"><span data-stu-id="908cd-214">a.</span></span> <span data-ttu-id="908cd-215">En el cuadro de texto **Nombre de usuario**, escriba el nombre de un usuario, por ejemplo, **Brittsimon**.</span><span class="sxs-lookup"><span data-stu-id="908cd-215">In the **User Name** textbox, type the name of user like **Brittsimon**.</span></span>
   
    <span data-ttu-id="908cd-216">b.</span><span class="sxs-lookup"><span data-stu-id="908cd-216">b.</span></span> <span data-ttu-id="908cd-217">En el cuadro de texto **Email address** (Dirección de correo electrónico), escriba el correo electrónico del usuario, en este caso, **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="908cd-217">In **E-mail Address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="908cd-218">c.</span><span class="sxs-lookup"><span data-stu-id="908cd-218">c.</span></span> <span data-ttu-id="908cd-219">En el cuadro de texto **First Name** (Nombre), escriba el nombre de usuario, en este caso **Britta**.</span><span class="sxs-lookup"><span data-stu-id="908cd-219">In **First Name** text box, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="908cd-220">d.</span><span class="sxs-lookup"><span data-stu-id="908cd-220">d.</span></span> <span data-ttu-id="908cd-221">En el cuadro de texto **Last Name** (Apellidos), escriba el nombre de usuario, en este caso **Simon**.</span><span class="sxs-lookup"><span data-stu-id="908cd-221">In **Last Name** text box, enter the last name of user like **Simon**.</span></span>

    <span data-ttu-id="908cd-222">e.</span><span class="sxs-lookup"><span data-stu-id="908cd-222">e.</span></span> <span data-ttu-id="908cd-223">Haga clic en **Guardar y cerrar**.</span><span class="sxs-lookup"><span data-stu-id="908cd-223">Click **Save & Close**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="908cd-224">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Rally Software ofrecida por Rally Software para aprovisionar cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="908cd-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="908cd-225">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="908cd-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="908cd-226">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Rally Software.</span><span class="sxs-lookup"><span data-stu-id="908cd-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rally Software.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="908cd-228">**Para asignar un usuario llamado Britta Simon a Rally Software, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="908cd-228">**To assign Britta Simon to Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="908cd-229">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="908cd-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="908cd-231">En la lista de aplicaciones, seleccione **Rally Software**.</span><span class="sxs-lookup"><span data-stu-id="908cd-231">In the applications list, select **Rally Software**.</span></span>

    ![Vínculo a Rally Software en la lista de aplicaciones](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. <span data-ttu-id="908cd-233">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="908cd-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="908cd-235">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="908cd-235">Click **Add** button.</span></span> <span data-ttu-id="908cd-236">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="908cd-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="908cd-238">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="908cd-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="908cd-239">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="908cd-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="908cd-240">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="908cd-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="908cd-241">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="908cd-241">Test single sign-on</span></span>

<span data-ttu-id="908cd-242">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="908cd-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="908cd-243">Al hacer clic en el icono de Rally Software en el panel de acceso, debería iniciar sesión automáticamente en su aplicación de Rally Software.</span><span class="sxs-lookup"><span data-stu-id="908cd-243">When you click the Rally Software tile in the Access Panel, you should get automatically signed-on to your Rally Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="908cd-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="908cd-244">Additional resources</span></span>

* [<span data-ttu-id="908cd-245">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="908cd-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="908cd-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="908cd-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

