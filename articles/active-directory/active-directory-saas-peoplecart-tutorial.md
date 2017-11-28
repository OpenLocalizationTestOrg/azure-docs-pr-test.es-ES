---
title: "Tutorial: Integración de Azure Active Directory con Peoplecart | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Peoplecart."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c83b5d9d-2638-4689-b9f0-f56a9159e7a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: b83a1621263cac0b23bbd35a49fda213d2e4271a
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-peoplecart"></a><span data-ttu-id="37fac-103">Tutorial: Integración de Azure Active Directory con Peoplecart</span><span class="sxs-lookup"><span data-stu-id="37fac-103">Tutorial: Azure Active Directory integration with Peoplecart</span></span>

<span data-ttu-id="37fac-104">En este tutorial, aprenderá a integrar Peoplecart con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37fac-104">In this tutorial, you learn how to integrate Peoplecart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="37fac-105">La integración de Peoplecart con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="37fac-105">Integrating Peoplecart with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="37fac-106">Puede controlar en Azure AD quién tiene acceso a Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="37fac-106">You can control in Azure AD who has access to Peoplecart</span></span>
- <span data-ttu-id="37fac-107">Puede permitir que los usuarios inicien sesión automáticamente en Peoplecart (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37fac-107">You can enable your users to automatically get signed-on to Peoplecart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="37fac-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="37fac-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="37fac-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="37fac-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37fac-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="37fac-110">Prerequisites</span></span>

<span data-ttu-id="37fac-111">Para configurar la integración de Azure AD con Peoplecart, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="37fac-111">To configure Azure AD integration with Peoplecart, you need the following items:</span></span>

- <span data-ttu-id="37fac-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="37fac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="37fac-113">Una suscripción habilitada para el inicio de sesión único en Peoplecart</span><span class="sxs-lookup"><span data-stu-id="37fac-113">A Peoplecart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="37fac-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="37fac-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="37fac-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="37fac-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="37fac-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="37fac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="37fac-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37fac-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="37fac-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="37fac-118">Scenario description</span></span>
<span data-ttu-id="37fac-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="37fac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="37fac-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="37fac-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="37fac-121">Agregar Peoplecart desde la galería</span><span class="sxs-lookup"><span data-stu-id="37fac-121">Adding Peoplecart from the gallery</span></span>
2. <span data-ttu-id="37fac-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="37fac-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-peoplecart-from-the-gallery"></a><span data-ttu-id="37fac-123">Agregar Peoplecart desde la galería</span><span class="sxs-lookup"><span data-stu-id="37fac-123">Adding Peoplecart from the gallery</span></span>
<span data-ttu-id="37fac-124">Para configurar la integración de Peoplecart en Azure AD, es preciso agregar Peoplecart desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="37fac-124">To configure the integration of Peoplecart into Azure AD, you need to add Peoplecart from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="37fac-125">**Para agregar Peoplecart desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="37fac-125">**To add Peoplecart from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="37fac-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="37fac-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="37fac-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="37fac-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="37fac-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="37fac-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="37fac-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="37fac-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="37fac-133">En el cuadro de búsqueda, escriba **Peoplecart**, seleccione **Peoplecart** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="37fac-133">In the search box, type **Peoplecart**, select **Peoplecart** from result panel then click **Add** button to add the application.</span></span>

    ![Peoplecart en la lista de resultados](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="37fac-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="37fac-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="37fac-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Peoplecart con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="37fac-136">In this section, you configure and test Azure AD single sign-on with Peoplecart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="37fac-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Peoplecart para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37fac-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Peoplecart is to a user in Azure AD.</span></span> <span data-ttu-id="37fac-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="37fac-138">In other words, a link relationship between an Azure AD user and the related user in Peoplecart needs to be established.</span></span>

<span data-ttu-id="37fac-139">Para establecer la relación de vínculo, en Peoplecart, asigne el valor del **nombre de usuario** de Azure AD como el valor del **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="37fac-139">In Peoplecart, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="37fac-140">Para configurar y probar el inicio de sesión único de Azure AD con Peoplecart, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="37fac-140">To configure and test Azure AD single sign-on with Peoplecart, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="37fac-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="37fac-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="37fac-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37fac-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="37fac-143">**[Creación de un usuario de prueba en Peoplecart](#create-a-peoplecart-test-user)**: para tener un homólogo de Britta Simon en Peoplecart que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37fac-143">**[Create a Peoplecart test user](#create-a-peoplecart-test-user)** - to have a counterpart of Britta Simon in Peoplecart that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="37fac-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37fac-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="37fac-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="37fac-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="37fac-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="37fac-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="37fac-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="37fac-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Peoplecart application.</span></span>

<span data-ttu-id="37fac-148">**Para configurar el inicio de sesión único de Azure AD con Peoplecart, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="37fac-148">**To configure Azure AD single sign-on with Peoplecart, perform the following steps:**</span></span>

1. <span data-ttu-id="37fac-149">En Azure Portal, en la página de integración de la aplicación **Peoplecart**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="37fac-149">In the Azure portal, on the **Peoplecart** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="37fac-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="37fac-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_samlbase.png)

3. <span data-ttu-id="37fac-153">En la sección **Dominio y direcciones URL de Peoplecart**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="37fac-153">On the **Peoplecart Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Peoplecart](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_url.png)

    <span data-ttu-id="37fac-155">a.</span><span class="sxs-lookup"><span data-stu-id="37fac-155">a.</span></span> <span data-ttu-id="37fac-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<tenantname>.peoplecart.com/SignIn.aspx`.</span><span class="sxs-lookup"><span data-stu-id="37fac-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.peoplecart.com/SignIn.aspx`</span></span>

    <span data-ttu-id="37fac-157">b.</span><span class="sxs-lookup"><span data-stu-id="37fac-157">b.</span></span> <span data-ttu-id="37fac-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<tenantname>.peoplecart.com`</span><span class="sxs-lookup"><span data-stu-id="37fac-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.peoplecart.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="37fac-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="37fac-159">These values are not real.</span></span> <span data-ttu-id="37fac-160">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="37fac-160">Update these values with the actual Sign-On URL, and Identifier.</span></span> <span data-ttu-id="37fac-161">Póngase en contacto con el [equipo de soporte técnico de Peoplecart](https://peoplecart.com/ContactUs.aspx) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="37fac-161">Contact [Peoplecart Client support team](https://peoplecart.com/ContactUs.aspx) to get these values.</span></span> 
 
4. <span data-ttu-id="37fac-162">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="37fac-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_certificate.png) 

5. <span data-ttu-id="37fac-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="37fac-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-peoplecart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="37fac-166">En la sección **Configuración de Peoplecart**, haga clic en **Configurar Peoplecart** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="37fac-166">On the **Peoplecart Configuration** section, click **Configure Peoplecart** to open **Configure sign-on** window.</span></span> <span data-ttu-id="37fac-167">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="37fac-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de Peoplecart](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_configure.png) 

7. <span data-ttu-id="37fac-169">Para configurar el inicio de sesión único en **Peoplecart**, es preciso enviar los datos descargados de **XML de metadatos**, **SAML Single Sign-On Service URL (Dirección URL del servicio de inicio de sesión único de SAML)** al [equipo de soporte técnico de Peoplecart](https://peoplecart.com/ContactUs.aspx).</span><span class="sxs-lookup"><span data-stu-id="37fac-169">To configure single sign-on on **Peoplecart** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Peoplecart support team](https://peoplecart.com/ContactUs.aspx).</span></span> <span data-ttu-id="37fac-170">El equipo de soporte técnico lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="37fac-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="37fac-171">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="37fac-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="37fac-172">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="37fac-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="37fac-173">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="37fac-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="37fac-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="37fac-174">Create an Azure AD test user</span></span>
<span data-ttu-id="37fac-175">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="37fac-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="37fac-177">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="37fac-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="37fac-178">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="37fac-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="37fac-180">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="37fac-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="37fac-182">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="37fac-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Botón Agregar](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="37fac-184">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="37fac-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Cuadro de diálogo Usuario](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="37fac-186">a.</span><span class="sxs-lookup"><span data-stu-id="37fac-186">a.</span></span> <span data-ttu-id="37fac-187">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="37fac-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="37fac-188">b.</span><span class="sxs-lookup"><span data-stu-id="37fac-188">b.</span></span> <span data-ttu-id="37fac-189">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37fac-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="37fac-190">c.</span><span class="sxs-lookup"><span data-stu-id="37fac-190">c.</span></span> <span data-ttu-id="37fac-191">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="37fac-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="37fac-192">d.</span><span class="sxs-lookup"><span data-stu-id="37fac-192">d.</span></span> <span data-ttu-id="37fac-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="37fac-193">Click **Create**.</span></span>
 
### <a name="create-a-peoplecart-test-user"></a><span data-ttu-id="37fac-194">Creación de un usuario de prueba de Peoplecart</span><span class="sxs-lookup"><span data-stu-id="37fac-194">Create a Peoplecart test user</span></span>

<span data-ttu-id="37fac-195">En esta sección, creará un usuario llamado "Britta Simon" en Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="37fac-195">In this section, you create a user called Britta Simon in Peoplecart.</span></span> <span data-ttu-id="37fac-196">Trabaje con el [equipo de soporte técnico de Peoplecart](https://peoplecart.com/ContactUs.aspx) para agregar los usuarios a la plataforma de Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="37fac-196">Work with [Peoplecart support team](https://peoplecart.com/ContactUs.aspx) to add the users in the Peoplecart platform.</span></span> <span data-ttu-id="37fac-197">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="37fac-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="37fac-198">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="37fac-198">Assign the Azure AD test user</span></span>

<span data-ttu-id="37fac-199">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="37fac-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Peoplecart.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="37fac-201">**Para asignar a Britta Simon a Peoplecart, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="37fac-201">**To assign Britta Simon to Peoplecart, perform the following steps:**</span></span>

1. <span data-ttu-id="37fac-202">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="37fac-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="37fac-204">En la lista de aplicaciones, seleccione **Peoplecart**.</span><span class="sxs-lookup"><span data-stu-id="37fac-204">In the applications list, select **Peoplecart**.</span></span>

    ![Vínculo a Peoplecart en la lista de aplicaciones](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_app.png) 

3. <span data-ttu-id="37fac-206">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="37fac-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202] 

4. <span data-ttu-id="37fac-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="37fac-208">Click **Add** button.</span></span> <span data-ttu-id="37fac-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="37fac-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="37fac-211">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="37fac-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="37fac-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="37fac-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="37fac-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="37fac-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="37fac-214">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="37fac-214">Test single sign-on</span></span>

<span data-ttu-id="37fac-215">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="37fac-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="37fac-216">Al hacer clic en el icono de Peoplecart del panel de acceso, debería entrar en la página de inicio de sesión de la aplicación Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="37fac-216">When you click the Peoplecart tile in the Access Panel, you should get login page of Peoplecart application.</span></span>
<span data-ttu-id="37fac-217">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="37fac-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37fac-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="37fac-218">Additional resources</span></span>

* [<span data-ttu-id="37fac-219">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37fac-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="37fac-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="37fac-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_203.png

