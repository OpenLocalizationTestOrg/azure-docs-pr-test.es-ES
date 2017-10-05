---
title: "Tutorial: Integración de Azure Active Directory con Synergi | Microsoft Docs"
description: "Aprenda cómo configurar el inicio de sesión único entre Azure Active Directory y Synergi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 73c970e1-f1ba-420b-b225-414fdf93b140
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: dedbe96fbb26bc34c4d7e213892b318f0e6fef12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-synergi"></a><span data-ttu-id="15e40-103">Tutorial: integración de Azure Active Directory con Synergi</span><span class="sxs-lookup"><span data-stu-id="15e40-103">Tutorial: Azure Active Directory integration with Synergi</span></span>

<span data-ttu-id="15e40-104">En este tutorial, aprenderá cómo integrar Synergi con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="15e40-104">In this tutorial, you learn how to integrate Synergi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="15e40-105">Integrar Synergi con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="15e40-105">Integrating Synergi with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="15e40-106">En Azure AD puede controlar quién tiene acceso a Synergi.</span><span class="sxs-lookup"><span data-stu-id="15e40-106">You can control in Azure AD who has access to Synergi.</span></span>
- <span data-ttu-id="15e40-107">Puede permitir que los usuarios inicien sesión automáticamente en Synergi (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15e40-107">You can enable your users to automatically get signed-on to Synergi (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="15e40-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="15e40-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="15e40-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="15e40-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15e40-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="15e40-110">Prerequisites</span></span>

<span data-ttu-id="15e40-111">Para configurar la integración de Azure AD con Synergi se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="15e40-111">To configure Azure AD integration with Synergi, you need the following items:</span></span>

- <span data-ttu-id="15e40-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="15e40-112">An Azure AD subscription</span></span>
- <span data-ttu-id="15e40-113">Una suscripción habilitada para el inicio de sesión único en Synergi</span><span class="sxs-lookup"><span data-stu-id="15e40-113">A Synergi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="15e40-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="15e40-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="15e40-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="15e40-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="15e40-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="15e40-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="15e40-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="15e40-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="15e40-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="15e40-118">Scenario description</span></span>
<span data-ttu-id="15e40-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="15e40-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="15e40-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="15e40-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="15e40-121">Incorporación de Synergi desde la galería</span><span class="sxs-lookup"><span data-stu-id="15e40-121">Adding Synergi from the gallery</span></span>
2. <span data-ttu-id="15e40-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="15e40-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-synergi-from-the-gallery"></a><span data-ttu-id="15e40-123">Incorporación de Synergi desde la galería</span><span class="sxs-lookup"><span data-stu-id="15e40-123">Adding Synergi from the gallery</span></span>
<span data-ttu-id="15e40-124">Para configurar la integración de Synergi en Azure AD, deberá agregar Synergi desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="15e40-124">To configure the integration of Synergi into Azure AD, you need to add Synergi from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="15e40-125">**Para agregar Synergi desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="15e40-125">**To add Synergi from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="15e40-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="15e40-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="15e40-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="15e40-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="15e40-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="15e40-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="15e40-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="15e40-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="15e40-133">En el cuadro de búsqueda, escriba **Synergi**, seleccione **Synergi** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="15e40-133">In the search box, type **Synergi**, select **Synergi** from result panel then click **Add** button to add the application.</span></span>

    ![Synergi en la lista de resultados](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="15e40-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="15e40-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="15e40-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Synergi con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="15e40-136">In this section, you configure and test Azure AD single sign-on with Synergi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="15e40-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Synergi para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15e40-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Synergi is to a user in Azure AD.</span></span> <span data-ttu-id="15e40-138">En otras palabras, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Synergi.</span><span class="sxs-lookup"><span data-stu-id="15e40-138">In other words, a link relationship between an Azure AD user and the related user in Synergi needs to be established.</span></span>

<span data-ttu-id="15e40-139">Para establecer la relación de vínculo, en Synergi, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="15e40-139">In Synergi, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="15e40-140">Para configurar y probar el inicio de sesión único de Azure AD con Synergi, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="15e40-140">To configure and test Azure AD single sign-on with Synergi, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="15e40-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="15e40-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="15e40-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="15e40-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="15e40-143">**[Creación de un usuario de prueba de Synergi](#create-a-synergi-test-user)**: para tener un homólogo de Britta Simon en Synergi que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15e40-143">**[Create a Synergi test user](#create-a-synergi-test-user)** - to have a counterpart of Britta Simon in Synergi that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="15e40-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15e40-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="15e40-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="15e40-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="15e40-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="15e40-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="15e40-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Synergi.</span><span class="sxs-lookup"><span data-stu-id="15e40-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Synergi application.</span></span>

<span data-ttu-id="15e40-148">**Para configurar el inicio de sesión único de Azure AD con Synergi, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="15e40-148">**To configure Azure AD single sign-on with Synergi, perform the following steps:**</span></span>

1. <span data-ttu-id="15e40-149">En Azure Portal, en la página de integración de la aplicación **Synergi**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="15e40-149">In the Azure portal, on the **Synergi** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="15e40-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="15e40-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_samlbase.png)

3. <span data-ttu-id="15e40-153">En la sección **Dominio y direcciones URL de Synergi**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="15e40-153">On the **Synergi Domain and URLs** section, perform the following steps:</span></span>

    ![Información sobre dominio y direcciones URL de inicio de sesión único de Synergi](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_url.png)

    <span data-ttu-id="15e40-155">a.</span><span class="sxs-lookup"><span data-stu-id="15e40-155">a.</span></span> <span data-ttu-id="15e40-156">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<company name>.irmsecurity.com`</span><span class="sxs-lookup"><span data-stu-id="15e40-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.irmsecurity.com`</span></span>

    <span data-ttu-id="15e40-157">b.</span><span class="sxs-lookup"><span data-stu-id="15e40-157">b.</span></span> <span data-ttu-id="15e40-158">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<company name>.irmsecurity.com/sso/<organization id>`.</span><span class="sxs-lookup"><span data-stu-id="15e40-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.irmsecurity.com/sso/<organization id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="15e40-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="15e40-159">These values are not real.</span></span> <span data-ttu-id="15e40-160">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="15e40-160">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="15e40-161">Póngase en contacto con el [equipo de soporte técnico de Synergi](https://www.irmsecurity.com/contact/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="15e40-161">Contact [Synergi support team](https://www.irmsecurity.com/contact/) to get these values.</span></span>

4. <span data-ttu-id="15e40-162">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="15e40-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_certificate.png) 

5. <span data-ttu-id="15e40-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="15e40-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-synergi-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="15e40-166">En la sección **Configuración de Synergi**, haga clic en **Configurar Synergi** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="15e40-166">On the **Synergi Configuration** section, click **Configure Synergi** to open **Configure sign-on** window.</span></span> <span data-ttu-id="15e40-167">Copie los valores de **Sign-Out URL and SAML Entity ID** (Dirección URL de cierre de sesión e identificador de entidad de SAML) de la **sección Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="15e40-167">Copy the **Sign-Out URL and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configuración de Synergi](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_configure.png) 

7. <span data-ttu-id="15e40-169">Para configurar el inicio de sesión único en **Synergi**, debe enviar el **certificado (Base64) descargado y la dirección URL de cierre de sesión y el identificador de entidad de SAML** al [equipo de soporte técnico de Synergi](https://www.irmsecurity.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="15e40-169">To configure single sign-on on **Synergi** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, and SAML Entity ID** to [Synergi support team](https://www.irmsecurity.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="15e40-170">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="15e40-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="15e40-171">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="15e40-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="15e40-172">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="15e40-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="15e40-173">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="15e40-173">Create an Azure AD test user</span></span>

<span data-ttu-id="15e40-174">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="15e40-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="15e40-176">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="15e40-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="15e40-177">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="15e40-177">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-synergi-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="15e40-179">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="15e40-179">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-synergi-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="15e40-181">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="15e40-181">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-synergi-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="15e40-183">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="15e40-183">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-synergi-tutorial/create_aaduser_04.png)

    <span data-ttu-id="15e40-185">a.</span><span class="sxs-lookup"><span data-stu-id="15e40-185">a.</span></span> <span data-ttu-id="15e40-186">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="15e40-186">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="15e40-187">b.</span><span class="sxs-lookup"><span data-stu-id="15e40-187">b.</span></span> <span data-ttu-id="15e40-188">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="15e40-188">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="15e40-189">c.</span><span class="sxs-lookup"><span data-stu-id="15e40-189">c.</span></span> <span data-ttu-id="15e40-190">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="15e40-190">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="15e40-191">d.</span><span class="sxs-lookup"><span data-stu-id="15e40-191">d.</span></span> <span data-ttu-id="15e40-192">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="15e40-192">Click **Create**.</span></span>
  
### <a name="create-a-synergi-test-user"></a><span data-ttu-id="15e40-193">Creación de un usuario de prueba de Synergi</span><span class="sxs-lookup"><span data-stu-id="15e40-193">Create a Synergi test user</span></span>

<span data-ttu-id="15e40-194">En esta sección, creará un usuario llamado Britta Simon en Synergi.</span><span class="sxs-lookup"><span data-stu-id="15e40-194">In this section, you create a user called Britta Simon in Synergi.</span></span> <span data-ttu-id="15e40-195">Trabaje con el [equipo de soporte técnico de Synergi](https://www.irmsecurity.com/contact/) para agregar los usuarios a la plataforma Synergi.</span><span class="sxs-lookup"><span data-stu-id="15e40-195">Work with [Synergi support team](https://www.irmsecurity.com/contact/) to add the users in the Synergi platform.</span></span> <span data-ttu-id="15e40-196">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="15e40-196">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="15e40-197">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="15e40-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="15e40-198">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Synergi.</span><span class="sxs-lookup"><span data-stu-id="15e40-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Synergi.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="15e40-200">**Para asignar a Britta Simon a Synergi, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="15e40-200">**To assign Britta Simon to Synergi, perform the following steps:**</span></span>

1. <span data-ttu-id="15e40-201">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="15e40-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="15e40-203">En la lista de aplicaciones, seleccione **Synergi**.</span><span class="sxs-lookup"><span data-stu-id="15e40-203">In the applications list, select **Synergi**.</span></span>

    ![Vínculo de Synergi en la lista de aplicaciones](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_app.png)  

3. <span data-ttu-id="15e40-205">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="15e40-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="15e40-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="15e40-207">Click **Add** button.</span></span> <span data-ttu-id="15e40-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="15e40-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="15e40-210">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="15e40-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="15e40-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="15e40-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="15e40-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="15e40-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="15e40-213">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="15e40-213">Test single sign-on</span></span>

<span data-ttu-id="15e40-214">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="15e40-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="15e40-215">Al hacer clic en el icono de Synergi del panel de acceso, debería iniciar sesión automáticamente en su aplicación Synergi.</span><span class="sxs-lookup"><span data-stu-id="15e40-215">When you click the Synergi tile in the Access Panel, you should get automatically signed-on to your Synergi application.</span></span>
<span data-ttu-id="15e40-216">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="15e40-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="15e40-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="15e40-217">Additional resources</span></span>

* [<span data-ttu-id="15e40-218">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="15e40-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="15e40-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="15e40-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_203.png

