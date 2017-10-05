---
title: "Tutorial: integración de Azure Active Directory con Predictix Assortment Planning | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Predictix Assortment Planning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 37e686ff-f8e5-40b1-9d7e-f64b076917b7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: cc7ad4aa5260276e26406b6b79c039372e5ee69f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-assortment-planning"></a><span data-ttu-id="eed79-103">Tutorial: Integración de Azure Active Directory con Predictix Assortment Planning</span><span class="sxs-lookup"><span data-stu-id="eed79-103">Tutorial: Azure Active Directory integration with Predictix Assortment Planning</span></span>

<span data-ttu-id="eed79-104">En este tutorial, obtendrá información sobre cómo integrar Predictix Assortment Planning con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eed79-104">In this tutorial, you learn how to integrate Predictix Assortment Planning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eed79-105">Integrar Predictix Assortment Planning con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="eed79-105">Integrating Predictix Assortment Planning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="eed79-106">En Azure AD puede controlar quién tiene acceso a Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="eed79-106">You can control in Azure AD who has access to Predictix Assortment Planning.</span></span>
- <span data-ttu-id="eed79-107">Puede permitir que los usuarios inicien sesión automáticamente en Predictix Assortment Planning (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eed79-107">You can enable your users to automatically get signed-on to Predictix Assortment Planning (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="eed79-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="eed79-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="eed79-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eed79-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eed79-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="eed79-110">Prerequisites</span></span>

<span data-ttu-id="eed79-111">Para configurar la integración de Azure AD con Predictix Assortment Planning, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="eed79-111">To configure Azure AD integration with Predictix Assortment Planning, you need the following items:</span></span>

- <span data-ttu-id="eed79-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eed79-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eed79-113">Una suscripción habilitada para el inicio de sesión único en Predictix Assortment Planning</span><span class="sxs-lookup"><span data-stu-id="eed79-113">A Predictix Assortment Planning single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eed79-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="eed79-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eed79-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="eed79-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eed79-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="eed79-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eed79-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eed79-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eed79-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="eed79-118">Scenario description</span></span>
<span data-ttu-id="eed79-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="eed79-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eed79-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="eed79-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eed79-121">Incorporación de Predictix Assortment Planning desde la galería</span><span class="sxs-lookup"><span data-stu-id="eed79-121">Adding Predictix Assortment Planning from the gallery</span></span>
2. <span data-ttu-id="eed79-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eed79-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-assortment-planning-from-the-gallery"></a><span data-ttu-id="eed79-123">Incorporación de Predictix Assortment Planning desde la galería</span><span class="sxs-lookup"><span data-stu-id="eed79-123">Adding Predictix Assortment Planning from the gallery</span></span>
<span data-ttu-id="eed79-124">Para configurar la integración de Predictix Assortment Planning en Azure AD, deberá agregar Predictix Assortment Planning desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="eed79-124">To configure the integration of Predictix Assortment Planning into Azure AD, you need to add Predictix Assortment Planning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="eed79-125">**Para agregar Predictix Assortment Planning desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="eed79-125">**To add Predictix Assortment Planning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="eed79-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="eed79-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="eed79-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="eed79-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="eed79-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="eed79-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="eed79-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eed79-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="eed79-133">En el cuadro de búsqueda, escriba **Predictix Assortment Planning**, seleccione **Predictix Assortment Planning** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="eed79-133">In the search box, type **Predictix Assortment Planning**, select **Predictix Assortment Planning** from result panel then click **Add** button to add the application.</span></span>

    ![Predictix Assortment Planning en la lista de resultados](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="eed79-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="eed79-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="eed79-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Predictix Assortment Planning con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="eed79-136">In this section, you configure and test Azure AD single sign-on with Predictix Assortment Planning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="eed79-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Predictix Assortment Planning para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eed79-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Predictix Assortment Planning is to a user in Azure AD.</span></span> <span data-ttu-id="eed79-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="eed79-138">In other words, a link relationship between an Azure AD user and the related user in Predictix Assortment Planning needs to be established.</span></span>

<span data-ttu-id="eed79-139">Para establecer la relación de vínculo, en Predictix Assortment Planning, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="eed79-139">In Predictix Assortment Planning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="eed79-140">Para configurar y probar el inicio de sesión único de Azure AD con Predictix Assortment Planning, es preciso completar los siguientes pasos preliminares:</span><span class="sxs-lookup"><span data-stu-id="eed79-140">To configure and test Azure AD single sign-on with Predictix Assortment Planning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="eed79-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="eed79-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="eed79-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eed79-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eed79-143">**[Creación de un usuario de prueba de Predictix Assortment Planning](#create-a-predictix-assortment-planning-test-user)**: para tener un homólogo de Britta Simon en Predictix Assortment Planning que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eed79-143">**[Create a Predictix Assortment Planning test user](#create-a-predictix-assortment-planning-test-user)** - to have a counterpart of Britta Simon in Predictix Assortment Planning that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="eed79-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eed79-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eed79-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="eed79-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="eed79-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eed79-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="eed79-147">En esta sección, se habilita el inicio de sesión único de Azure AD en Azure Portal y se configura el inicio de sesión único en la aplicación Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="eed79-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Predictix Assortment Planning application.</span></span>

<span data-ttu-id="eed79-148">**Para configurar el inicio de sesión único de Azure AD con Predictix Assortment Planning, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="eed79-148">**To configure Azure AD single sign-on with Predictix Assortment Planning, perform the following steps:**</span></span>

1. <span data-ttu-id="eed79-149">En la página de integración de la aplicación **Predictix Assortment Planning** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="eed79-149">In the Azure portal, on the **Predictix Assortment Planning** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="eed79-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="eed79-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_samlbase.png)

3. <span data-ttu-id="eed79-153">En la sección **Dominio y direcciones URL de Predictix Assortment Planning**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="eed79-153">On the **Predictix Assortment Planning Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Predictix Assortment Planning](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_url.png)

    <span data-ttu-id="eed79-155">a.</span><span class="sxs-lookup"><span data-stu-id="eed79-155">a.</span></span> <span data-ttu-id="eed79-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="eed79-156">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|--|
    | `https://<sub-domain>.ap.predictix.com/sso/request`|
    | `https://<sub-domain>.dev.ap.predictix.com/`|

    <span data-ttu-id="eed79-157">b.</span><span class="sxs-lookup"><span data-stu-id="eed79-157">b.</span></span> <span data-ttu-id="eed79-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="eed79-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|--|
    | `https://<sub-domain>.ap.predictix.com`|
    | `https://<sub-domain>.dev.ap.predictix.com`|
    
    > [!NOTE] 
    > <span data-ttu-id="eed79-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="eed79-159">These values are not real.</span></span> <span data-ttu-id="eed79-160">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="eed79-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="eed79-161">Póngase en contacto con el [equipo de soporte técnico de Predictix Assortment Planning](http://www.infor.com/support) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="eed79-161">Contact [Predictix Assortment Planning Client support team](http://www.infor.com/support) to get these values.</span></span> 
 


4. <span data-ttu-id="eed79-162">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="eed79-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_certificate.png) 

5. <span data-ttu-id="eed79-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="eed79-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eed79-166">En la sección **Configuración de Predictix Assortment Planning**, haga clic en **Configurar Predictix Assortment Planning** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="eed79-166">On the **Predictix Assortment Planning Configuration** section, click **Configure Predictix Assortment Planning** to open **Configure sign-on** window.</span></span> <span data-ttu-id="eed79-167">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="eed79-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de Predictix Assortment Planning](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_configure.png) 

7. <span data-ttu-id="eed79-169">Para configurar el inicio de sesión único en **Predictix Assortment Planning**, es preciso enviar el **Certificado (Base64)** descargado, el **identificador de entidad de SAML**, la **dirección URL del servicio de inicio de sesión de SAML** y la **dirección URL del servicio de cierre de sesión** al [equipo de soporte técnico de Predictix Assortment Planning](http://www.infor.com/support).</span><span class="sxs-lookup"><span data-stu-id="eed79-169">To configure single sign-on on **Predictix Assortment Planning** side, you need to send the downloaded **Certificate(Base64)**, **SAML Entity ID**, **SAML Single Sign-On Service URL**, and **Sign-Out URL**  to [Predictix Assortment Planning support team](http://www.infor.com/support).</span></span> <span data-ttu-id="eed79-170">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="eed79-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="eed79-171">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="eed79-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="eed79-172">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="eed79-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="eed79-173">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eed79-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="eed79-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eed79-174">Create an Azure AD test user</span></span>

<span data-ttu-id="eed79-175">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="eed79-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="eed79-177">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="eed79-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="eed79-178">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="eed79-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="eed79-180">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="eed79-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="eed79-182">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="eed79-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="eed79-184">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="eed79-184">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_04.png)

    <span data-ttu-id="eed79-186">a.</span><span class="sxs-lookup"><span data-stu-id="eed79-186">a.</span></span> <span data-ttu-id="eed79-187">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eed79-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eed79-188">b.</span><span class="sxs-lookup"><span data-stu-id="eed79-188">b.</span></span> <span data-ttu-id="eed79-189">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eed79-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="eed79-190">c.</span><span class="sxs-lookup"><span data-stu-id="eed79-190">c.</span></span> <span data-ttu-id="eed79-191">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="eed79-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="eed79-192">d.</span><span class="sxs-lookup"><span data-stu-id="eed79-192">d.</span></span> <span data-ttu-id="eed79-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="eed79-193">Click **Create**.</span></span>
 
### <a name="create-a-predictix-assortment-planning-test-user"></a><span data-ttu-id="eed79-194">Creación de un usuario de prueba de Predictix Assortment Planning</span><span class="sxs-lookup"><span data-stu-id="eed79-194">Create a Predictix Assortment Planning test user</span></span>

<span data-ttu-id="eed79-195">En esta sección, creará un usuario llamado Britta Simon en Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="eed79-195">In this section, you create a user called Britta Simon in Predictix Assortment Planning.</span></span> <span data-ttu-id="eed79-196">Trabaje con el [equipo de soporte técnico de Predictix Assortment Planning](http://www.infor.com/contact/) para agregar usuarios a la plataforma de Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="eed79-196">Please work with [Predictix Assortment Planning support team](http://www.infor.com/contact/) to add the users in the Predictix Assortment Planning platform.</span></span>
 > [!NOTE]
 > <span data-ttu-id="eed79-197">El titular de la cuenta de Azure Active Directory recibirá un mensaje de correo y seguirá un vínculo para confirmar su cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="eed79-197">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="eed79-198">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eed79-198">Assign the Azure AD test user</span></span>

<span data-ttu-id="eed79-199">En esta sección, permitirá que Britta Simon use el inicio de sesión único de Azure concediéndole acceso a Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="eed79-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Predictix Assortment Planning.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="eed79-201">**Para asignar a Britta Simon a Predictix Assortment Planning, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="eed79-201">**To assign Britta Simon to Predictix Assortment Planning, perform the following steps:**</span></span>

1. <span data-ttu-id="eed79-202">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="eed79-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="eed79-204">En la lista de aplicaciones, seleccione **Predictix Assortment Planning**.</span><span class="sxs-lookup"><span data-stu-id="eed79-204">In the applications list, select **Predictix Assortment Planning**.</span></span>

    ![Vínculo de Predictix Assortment Planning en la lista de aplicaciones](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_app.png)  

3. <span data-ttu-id="eed79-206">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="eed79-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="eed79-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="eed79-208">Click **Add** button.</span></span> <span data-ttu-id="eed79-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="eed79-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="eed79-211">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="eed79-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="eed79-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="eed79-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eed79-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="eed79-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="eed79-214">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="eed79-214">Test single sign-on</span></span>

<span data-ttu-id="eed79-215">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="eed79-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="eed79-216">Al hacer clic en el icono de Predictix Assortment Planning en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="eed79-216">When you click the Predictix Assortment Planning tile in the Access Panel, you should get automatically signed-on to your Predictix Assortment Planning application.</span></span>
<span data-ttu-id="eed79-217">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eed79-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="eed79-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="eed79-218">Additional resources</span></span>

* [<span data-ttu-id="eed79-219">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eed79-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eed79-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eed79-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_203.png

