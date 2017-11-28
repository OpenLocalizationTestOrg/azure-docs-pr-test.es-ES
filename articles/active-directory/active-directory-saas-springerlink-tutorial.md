---
title: "Tutorial: Integración de Azure Active Directory con Springer Link | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Springer Link."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 58cdf029-bdc0-43c4-a469-b921c2a669bd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: jeedes
ms.openlocfilehash: b9aec6f8f293cdd31456a7f50e3efe792804c7c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springer-link"></a><span data-ttu-id="44e02-103">Tutorial: Integración de Azure Active Directory con Springer Link</span><span class="sxs-lookup"><span data-stu-id="44e02-103">Tutorial: Azure Active Directory integration with Springer Link</span></span>

<span data-ttu-id="44e02-104">En este tutorial, obtendrá información sobre cómo integrar Springer Link con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="44e02-104">In this tutorial, you learn how to integrate Springer Link with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44e02-105">La integración de Springer Link con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="44e02-105">Integrating Springer Link with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="44e02-106">Puede controlar en Azure AD quién tiene acceso a Springer Link.</span><span class="sxs-lookup"><span data-stu-id="44e02-106">You can control in Azure AD who has access to Springer Link.</span></span>
- <span data-ttu-id="44e02-107">Puede permitir que los usuarios inicien sesión automáticamente en Springer Link (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44e02-107">You can enable your users to automatically get signed-on to Springer Link (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="44e02-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="44e02-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="44e02-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="44e02-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44e02-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="44e02-110">Prerequisites</span></span>

<span data-ttu-id="44e02-111">Para configurar la integración de Azure AD con Springer Link, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="44e02-111">To configure Azure AD integration with Springer Link, you need the following items:</span></span>

- <span data-ttu-id="44e02-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="44e02-112">An Azure AD subscription</span></span>
- <span data-ttu-id="44e02-113">Una suscripción habilitada para el inicio de sesión único en Springer Link</span><span class="sxs-lookup"><span data-stu-id="44e02-113">A Springer Link single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="44e02-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="44e02-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="44e02-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="44e02-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="44e02-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="44e02-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="44e02-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44e02-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="44e02-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="44e02-118">Scenario description</span></span>
<span data-ttu-id="44e02-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="44e02-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="44e02-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="44e02-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="44e02-121">Incorporación de Springer Link desde la galería</span><span class="sxs-lookup"><span data-stu-id="44e02-121">Adding Springer Link from the gallery</span></span>
2. <span data-ttu-id="44e02-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="44e02-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springer-link-from-the-gallery"></a><span data-ttu-id="44e02-123">Incorporación de Springer Link desde la galería</span><span class="sxs-lookup"><span data-stu-id="44e02-123">Adding Springer Link from the gallery</span></span>
<span data-ttu-id="44e02-124">Para configurar la integración de Springer Link en Azure AD, hay que agregar Springer Link desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="44e02-124">To configure the integration of Springer Link into Azure AD, you need to add Springer Link from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="44e02-125">**Para agregar Springer Link desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="44e02-125">**To add Springer Link from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="44e02-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="44e02-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="44e02-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="44e02-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="44e02-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="44e02-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="44e02-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="44e02-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="44e02-133">En el cuadro de búsqueda, escriba **Springer Link**, seleccione **Springer Link** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="44e02-133">In the search box, type **Springer Link**, select **Springer Link** from result panel then click **Add** button to add the application.</span></span>

    ![Springer Link en la lista de resultados](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="44e02-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="44e02-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="44e02-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Springer Link con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="44e02-136">In this section, you configure and test Azure AD single sign-on with Springer Link based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="44e02-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Springer Link para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44e02-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Springer Link is to a user in Azure AD.</span></span> <span data-ttu-id="44e02-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Springer Link.</span><span class="sxs-lookup"><span data-stu-id="44e02-138">In other words, a link relationship between an Azure AD user and the related user in Springer Link needs to be established.</span></span>

<span data-ttu-id="44e02-139">Para establecer la relación de vínculo, en Springer Link asigne el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="44e02-139">In Springer Link, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="44e02-140">Para configurar y probar el inicio de sesión único de Azure AD con Springer Link, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="44e02-140">To configure and test Azure AD single sign-on with Springer Link, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="44e02-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="44e02-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="44e02-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44e02-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="44e02-143">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44e02-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
4. <span data-ttu-id="44e02-144">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="44e02-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="44e02-145">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="44e02-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="44e02-146">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Springer Link.</span><span class="sxs-lookup"><span data-stu-id="44e02-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Springer Link application.</span></span>

<span data-ttu-id="44e02-147">**Para configurar el inicio de sesión único de Azure AD con Springer Link, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="44e02-147">**To configure Azure AD single sign-on with Springer Link, perform the following steps:**</span></span>

1. <span data-ttu-id="44e02-148">En Azure Portal, en la página de integración de la aplicación **Springer Link**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="44e02-148">In the Azure portal, on the **Springer Link** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="44e02-150">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="44e02-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_samlbase.png)

3. <span data-ttu-id="44e02-152">Vaya a la sección **Dominio y direcciones URL de Springer Link**, si quiere configurar la aplicación en modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="44e02-152">On the **Springer Link Domain and URLs** section,  If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Información de inicio de sesión único de Dominio y direcciones URL de Springer Link](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url1.png)

    <span data-ttu-id="44e02-154">a.</span><span class="sxs-lookup"><span data-stu-id="44e02-154">a.</span></span> <span data-ttu-id="44e02-155">En el cuadro de texto **Identificador**, escriba la dirección URL: `https://fsso.springer.com`</span><span class="sxs-lookup"><span data-stu-id="44e02-155">In the **Identifier** textbox, type the URL: `https://fsso.springer.com`</span></span>

    <span data-ttu-id="44e02-156">b.</span><span class="sxs-lookup"><span data-stu-id="44e02-156">b.</span></span> <span data-ttu-id="44e02-157">En el cuadro de texto **URL de respuesta**, escriba la siguiente dirección URL: `https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="44e02-157">In the **Reply URL** textbox, type the URL: `https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

4. <span data-ttu-id="44e02-158">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="44e02-158">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="44e02-159">Si quiere volver a configurar la aplicación en modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="44e02-159">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Información de inicio de sesión único de Dominio y direcciones URL de Springer Link](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url.png)

    <span data-ttu-id="44e02-161">En el cuadro de texto **URL de inicio de sesión**, escriba la dirección URL: `https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="44e02-161">In the **Sign-on URL** textbox, type the URL : `https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

5. <span data-ttu-id="44e02-162">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="44e02-162">Click **Save** button.</span></span>

    ![Botón Configurar inicio de sesión único](./media/active-directory-saas-springerlink-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="44e02-164">Para generar la dirección URL de **Metadatos**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="44e02-164">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="44e02-165">a.</span><span class="sxs-lookup"><span data-stu-id="44e02-165">a.</span></span> <span data-ttu-id="44e02-166">Haga clic en **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="44e02-166">Click **App registrations**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appregistrations.png)
   
    <span data-ttu-id="44e02-168">b.</span><span class="sxs-lookup"><span data-stu-id="44e02-168">b.</span></span> <span data-ttu-id="44e02-169">Haga clic en **Puntos de conexión** para abrir el cuadro de diálogo **Puntos de conexión**.</span><span class="sxs-lookup"><span data-stu-id="44e02-169">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpointicon.png)

    <span data-ttu-id="44e02-171">c.</span><span class="sxs-lookup"><span data-stu-id="44e02-171">c.</span></span> <span data-ttu-id="44e02-172">Haga clic en el botón Copiar para copiar la dirección URL del **DOCUMENTO DE METADATOS DE FEDERACIÓN** y péguela en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="44e02-172">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpoint.png)
     
    <span data-ttu-id="44e02-174">d.</span><span class="sxs-lookup"><span data-stu-id="44e02-174">d.</span></span> <span data-ttu-id="44e02-175">Ahora, vaya a la página de propiedades de **Springer Link** y copie el **identificador de la aplicación** con el botón **Copiar** y péguelo en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="44e02-175">Now go to the property page of **Springer Link** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appid.png)

    <span data-ttu-id="44e02-177">e.</span><span class="sxs-lookup"><span data-stu-id="44e02-177">e.</span></span> <span data-ttu-id="44e02-178">Genere la **Dirección URL de metadatos** con el patrón siguiente: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="44e02-178">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="44e02-179">Para configurar el inicio de sesión único en **Springer Link**, hay que enviar la **URL de metadatos** generada al [equipo de soporte técnico de Springer Link](mailto:identity@springernature.com).</span><span class="sxs-lookup"><span data-stu-id="44e02-179">To configure single sign-on on **Springer Link** side, you need to send the generated **Metadata URL** to [Springer Link support team](mailto:identity@springernature.com).</span></span>

> [!TIP]
> <span data-ttu-id="44e02-180">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="44e02-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="44e02-181">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="44e02-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="44e02-182">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="44e02-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="44e02-183">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="44e02-183">Create an Azure AD test user</span></span>

<span data-ttu-id="44e02-184">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="44e02-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="44e02-186">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="44e02-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="44e02-187">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="44e02-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-springerlink-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="44e02-189">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="44e02-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-springerlink-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="44e02-191">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="44e02-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-springerlink-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="44e02-193">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="44e02-193">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-springerlink-tutorial/create_aaduser_04.png)

    <span data-ttu-id="44e02-195">a.</span><span class="sxs-lookup"><span data-stu-id="44e02-195">a.</span></span> <span data-ttu-id="44e02-196">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="44e02-196">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="44e02-197">b.</span><span class="sxs-lookup"><span data-stu-id="44e02-197">b.</span></span> <span data-ttu-id="44e02-198">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44e02-198">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="44e02-199">c.</span><span class="sxs-lookup"><span data-stu-id="44e02-199">c.</span></span> <span data-ttu-id="44e02-200">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="44e02-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="44e02-201">d.</span><span class="sxs-lookup"><span data-stu-id="44e02-201">d.</span></span> <span data-ttu-id="44e02-202">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="44e02-202">Click **Create**.</span></span>
 
### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="44e02-203">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="44e02-203">Assign the Azure AD test user</span></span>

<span data-ttu-id="44e02-204">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Springer Link.</span><span class="sxs-lookup"><span data-stu-id="44e02-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Springer Link.</span></span>

![Asignación de rol de usuario][200] 

<span data-ttu-id="44e02-206">**Para asignar Britta Simon a Springer Link, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="44e02-206">**To assign Britta Simon to Springer Link, perform the following steps:**</span></span>

1. <span data-ttu-id="44e02-207">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="44e02-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="44e02-209">En la lista de aplicaciones, seleccione **Springer Link**.</span><span class="sxs-lookup"><span data-stu-id="44e02-209">In the applications list, select **Springer Link**.</span></span>

    ![Vínculo Springer Link de la lista de aplicaciones](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_app.png)  

3. <span data-ttu-id="44e02-211">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="44e02-211">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="44e02-213">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="44e02-213">Click **Add** button.</span></span> <span data-ttu-id="44e02-214">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="44e02-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="44e02-216">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="44e02-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="44e02-217">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="44e02-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="44e02-218">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="44e02-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="44e02-219">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="44e02-219">Test single sign-on</span></span>

<span data-ttu-id="44e02-220">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="44e02-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="44e02-221">Al hacer clic en el icono de Springer Link en el panel de acceso, debería iniciar sesión automáticamente en la aplicación Springer Link.</span><span class="sxs-lookup"><span data-stu-id="44e02-221">When you click the Springer Link tile in the Access Panel, you should get automatically signed-on to your Springer Link application.</span></span>
<span data-ttu-id="44e02-222">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="44e02-222">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="44e02-223">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="44e02-223">Additional resources</span></span>

* [<span data-ttu-id="44e02-224">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44e02-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44e02-225">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="44e02-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_203.png

