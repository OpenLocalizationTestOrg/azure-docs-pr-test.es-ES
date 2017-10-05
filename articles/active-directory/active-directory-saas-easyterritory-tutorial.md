---
title: "Tutorial: integración de Azure Active Directory con EasyTerritory | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory e EasyTerritory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d29b362d-e986-4f67-8ff2-e158e49353aa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 46f99496397e2ed39b1d9410453dac7983ced612
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-easyterritory"></a><span data-ttu-id="17d93-103">Tutorial: Integración de Azure Active Directory con EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="17d93-103">Tutorial: Azure Active Directory integration with EasyTerritory</span></span>

<span data-ttu-id="17d93-104">En este tutorial, obtendrá información sobre cómo integrar EasyTerritory con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="17d93-104">In this tutorial, you learn how to integrate EasyTerritory with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17d93-105">La integración de EasyTerritory con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="17d93-105">Integrating EasyTerritory with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="17d93-106">Puede controlar en Azure AD quién tiene acceso a EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="17d93-106">You can control in Azure AD who has access to EasyTerritory.</span></span>
- <span data-ttu-id="17d93-107">Puede habilitar a los usuarios para que inicien sesión automáticamente en EasyTerritory (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17d93-107">You can enable your users to automatically get signed-on to EasyTerritory (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="17d93-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="17d93-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="17d93-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="17d93-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17d93-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="17d93-110">Prerequisites</span></span>

<span data-ttu-id="17d93-111">Para configurar la integración de Azure AD con EasyTerritory, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="17d93-111">To configure Azure AD integration with EasyTerritory, you need the following items:</span></span>

- <span data-ttu-id="17d93-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17d93-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17d93-113">Una suscripción habilitada para el inicio de sesión único en EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="17d93-113">A EasyTerritory single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17d93-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="17d93-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17d93-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="17d93-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17d93-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="17d93-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="17d93-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17d93-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17d93-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="17d93-118">Scenario description</span></span>
<span data-ttu-id="17d93-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="17d93-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17d93-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="17d93-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17d93-121">Agregar EasyTerritory desde la galería</span><span class="sxs-lookup"><span data-stu-id="17d93-121">Adding EasyTerritory from the gallery</span></span>
2. <span data-ttu-id="17d93-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17d93-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-easyterritory-from-the-gallery"></a><span data-ttu-id="17d93-123">Agregar EasyTerritory desde la galería</span><span class="sxs-lookup"><span data-stu-id="17d93-123">Adding EasyTerritory from the gallery</span></span>
<span data-ttu-id="17d93-124">Para configurar la integración de EasyTerritory en Azure AD, deberá agregar EasyTerritory desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="17d93-124">To configure the integration of EasyTerritory into Azure AD, you need to add EasyTerritory from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="17d93-125">**Para agregar EasyTerritory desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="17d93-125">**To add EasyTerritory from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="17d93-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="17d93-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="17d93-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="17d93-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="17d93-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="17d93-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="17d93-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="17d93-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="17d93-133">En el cuadro de búsqueda, escriba **EasyTerritory**, seleccione **EasyTerritory** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="17d93-133">In the search box, type **EasyTerritory**, select **EasyTerritory** from result panel then click **Add** button to add the application.</span></span>

    ![EasyTerritory en la lista de resultados](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="17d93-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="17d93-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="17d93-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con EasyTerritory con un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="17d93-136">In this section, you configure and test Azure AD single sign-on with EasyTerritory based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="17d93-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de EasyTerritory para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17d93-137">For single sign-on to work, Azure AD needs to know what the counterpart user in EasyTerritory is to a user in Azure AD.</span></span> <span data-ttu-id="17d93-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="17d93-138">In other words, a link relationship between an Azure AD user and the related user in EasyTerritory needs to be established.</span></span>

<span data-ttu-id="17d93-139">Para establecer la relación de vínculo, en EasyTerritory, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="17d93-139">In EasyTerritory, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="17d93-140">Para configurar y probar el inicio de sesión único de Azure AD con EasyTerritory, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="17d93-140">To configure and test Azure AD single sign-on with EasyTerritory, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="17d93-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="17d93-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="17d93-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17d93-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="17d93-143">**[Creación de un usuario de prueba de EasyTerritory](#create-a-easyterritory-test-user)**: para tener un homólogo de Britta Simon en EasyTerritory que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17d93-143">**[Create a EasyTerritory test user](#create-a-easyterritory-test-user)** - to have a counterpart of Britta Simon in EasyTerritory that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="17d93-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17d93-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="17d93-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="17d93-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="17d93-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17d93-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="17d93-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="17d93-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EasyTerritory application.</span></span>

<span data-ttu-id="17d93-148">**Para configurar el inicio de sesión único de Azure AD con EasyTerritory, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="17d93-148">**To configure Azure AD single sign-on with EasyTerritory, perform the following steps:**</span></span>

1. <span data-ttu-id="17d93-149">En Azure Portal, en la página de integración de la aplicación **EasyTerritory**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="17d93-149">In the Azure portal, on the **EasyTerritory** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="17d93-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="17d93-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_samlbase.png)

3. <span data-ttu-id="17d93-153">En la sección **Dominio y direcciones URL de EasyTerritory**, si quiere configurar la aplicación en el modo iniciado por IDP, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="17d93-153">On the **EasyTerritory Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de EasyTerritory](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url.png)

    <span data-ttu-id="17d93-155">a.</span><span class="sxs-lookup"><span data-stu-id="17d93-155">a.</span></span> <span data-ttu-id="17d93-156">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://apps.easyterritory.com/<tenant id>/dev/`</span><span class="sxs-lookup"><span data-stu-id="17d93-156">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/dev/`</span></span>

    <span data-ttu-id="17d93-157">b.</span><span class="sxs-lookup"><span data-stu-id="17d93-157">b.</span></span> <span data-ttu-id="17d93-158">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`.</span><span class="sxs-lookup"><span data-stu-id="17d93-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span></span>

4. <span data-ttu-id="17d93-159">Active **Mostrar configuración avanzada de URL** y siga estos pasos si desea configurar la aplicación en el modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="17d93-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de EasyTerritory](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url1.png)

    <span data-ttu-id="17d93-161">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<company name>.easyterritory.com/`.</span><span class="sxs-lookup"><span data-stu-id="17d93-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.easyterritory.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="17d93-162">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="17d93-162">These values are not real.</span></span> <span data-ttu-id="17d93-163">Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="17d93-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="17d93-164">Póngase en contacto con el [equipo de soporte técnico al cliente de EasyTerritory](mailto:sales@easyterritory.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="17d93-164">Contact [EasyTerritory Client support team](mailto:sales@easyterritory.com) to get these values.</span></span> 

5. <span data-ttu-id="17d93-165">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="17d93-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_certificate.png) 

6. <span data-ttu-id="17d93-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="17d93-167">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-easyterritory-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="17d93-169">Para configurar el inicio de sesión único en el lado de **EasyTerritory**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico al cliente de EasyTerritory](mailto:sales@easyterritory.com).</span><span class="sxs-lookup"><span data-stu-id="17d93-169">To configure single sign-on on **EasyTerritory** side, you need to send the downloaded **Metadata XML** to [EasyTerritory support team](mailto:sales@easyterritory.com).</span></span> <span data-ttu-id="17d93-170">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="17d93-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="17d93-171">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="17d93-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="17d93-172">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="17d93-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="17d93-173">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="17d93-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="17d93-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17d93-174">Create an Azure AD test user</span></span>

<span data-ttu-id="17d93-175">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="17d93-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="17d93-177">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="17d93-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="17d93-178">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="17d93-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="17d93-180">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="17d93-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="17d93-182">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="17d93-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="17d93-184">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="17d93-184">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_04.png)

    <span data-ttu-id="17d93-186">a.</span><span class="sxs-lookup"><span data-stu-id="17d93-186">a.</span></span> <span data-ttu-id="17d93-187">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="17d93-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17d93-188">b.</span><span class="sxs-lookup"><span data-stu-id="17d93-188">b.</span></span> <span data-ttu-id="17d93-189">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17d93-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="17d93-190">c.</span><span class="sxs-lookup"><span data-stu-id="17d93-190">c.</span></span> <span data-ttu-id="17d93-191">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="17d93-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="17d93-192">d.</span><span class="sxs-lookup"><span data-stu-id="17d93-192">d.</span></span> <span data-ttu-id="17d93-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="17d93-193">Click **Create**.</span></span>
 
### <a name="create-a-easyterritory-test-user"></a><span data-ttu-id="17d93-194">Creación de un usuario de prueba de EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="17d93-194">Create a EasyTerritory test user</span></span>

<span data-ttu-id="17d93-195">En esta sección, creará una usuaria llamada Britta Simon en EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="17d93-195">In this section, you create a user called Britta Simon in EasyTerritory.</span></span> <span data-ttu-id="17d93-196">Trabaje con el [equipo de soporte técnico de EasyTerritory](mailto:sales@easyterritory.com) para agregar los usuarios a la plataforma de EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="17d93-196">Please work with [EasyTerritory support team](mailto:sales@easyterritory.com) to add the users in the EasyTerritory platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="17d93-197">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="17d93-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="17d93-198">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="17d93-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EasyTerritory.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="17d93-200">**Para asignar Britta Simon a EasyTerritory, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="17d93-200">**To assign Britta Simon to EasyTerritory, perform the following steps:**</span></span>

1. <span data-ttu-id="17d93-201">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="17d93-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="17d93-203">En la lista de aplicaciones, seleccione **EasyTerritory**.</span><span class="sxs-lookup"><span data-stu-id="17d93-203">In the applications list, select **EasyTerritory**.</span></span>

    ![El vínculo EasyTerritory en la lista de aplicaciones](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_app.png)  

3. <span data-ttu-id="17d93-205">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="17d93-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="17d93-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="17d93-207">Click **Add** button.</span></span> <span data-ttu-id="17d93-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="17d93-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="17d93-210">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="17d93-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="17d93-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="17d93-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17d93-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="17d93-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="17d93-213">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="17d93-213">Test single sign-on</span></span>

<span data-ttu-id="17d93-214">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="17d93-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="17d93-215">Al hacer clic en el icono de EasyTerritory en el panel de acceso, debe iniciar sesión automáticamente en su aplicación de EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="17d93-215">When you click the EasyTerritory tile in the Access Panel, you should get automatically signed-on to your EasyTerritory application.</span></span>
<span data-ttu-id="17d93-216">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="17d93-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="17d93-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="17d93-217">Additional resources</span></span>

* [<span data-ttu-id="17d93-218">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17d93-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="17d93-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="17d93-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)




<!--Image references-->

[1]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_203.png

