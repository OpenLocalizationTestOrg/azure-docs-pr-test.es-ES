---
title: "Tutorial: integración de Azure Active Directory con Thoughtworks Mingle | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Thoughtworks Mingle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 268ae5affb88a718f68c08daa94fe7aba4a99c11
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="ae2e6-103">Tutorial: Integración de Azure Active Directory con Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="ae2e6-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>

<span data-ttu-id="ae2e6-104">En este tutorial, aprenderá a integrar Thoughtworks Mingle con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae2e6-104">In this tutorial, you learn how to integrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae2e6-105">La integración de Thoughtworks Mingle con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ae2e6-105">Integrating Thoughtworks Mingle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ae2e6-106">Puede controlar en Azure AD quién tiene acceso a Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="ae2e6-106">You can control in Azure AD who has access to Thoughtworks Mingle</span></span>
- <span data-ttu-id="ae2e6-107">Puede permitir que los usuarios inicien sesión automáticamente en Thoughtworks Mingle (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae2e6-107">You can enable your users to automatically get signed-on to Thoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae2e6-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ae2e6-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ae2e6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae2e6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ae2e6-110">Prerequisites</span></span>

<span data-ttu-id="ae2e6-111">Para configurar la integración de Azure AD con Thoughtworks Mingle, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ae2e6-111">To configure Azure AD integration with Thoughtworks Mingle, you need the following items:</span></span>

- <span data-ttu-id="ae2e6-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae2e6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae2e6-113">Una suscripción habilitada para el inicio de sesión único en Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="ae2e6-113">A Thoughtworks Mingle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae2e6-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ae2e6-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ae2e6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae2e6-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae2e6-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae2e6-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae2e6-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="ae2e6-118">Scenario description</span></span>
<span data-ttu-id="ae2e6-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae2e6-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="ae2e6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae2e6-121">Agregación de Thoughtworks Mingle desde la galería</span><span class="sxs-lookup"><span data-stu-id="ae2e6-121">Adding Thoughtworks Mingle from the gallery</span></span>
2. <span data-ttu-id="ae2e6-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae2e6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thoughtworks-mingle-from-the-gallery"></a><span data-ttu-id="ae2e6-123">Agregación de Thoughtworks Mingle desde la galería</span><span class="sxs-lookup"><span data-stu-id="ae2e6-123">Adding Thoughtworks Mingle from the gallery</span></span>
<span data-ttu-id="ae2e6-124">Para configurar la integración de Thoughtworks Mingle en Azure AD, deberá agregar Thoughtworks Mingle desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-124">To configure the integration of Thoughtworks Mingle into Azure AD, you need to add Thoughtworks Mingle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ae2e6-125">**Para agregar Thoughtworks Mingle desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="ae2e6-125">**To add Thoughtworks Mingle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ae2e6-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="ae2e6-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ae2e6-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="ae2e6-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="ae2e6-133">En el cuadro de búsqueda, escriba **Thoughtworks Mingle**, seleccione **Thoughtworks Mingle** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-133">In the search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button to add the application.</span></span>

    ![Thoughtworks Mingle en la lista de resultados](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ae2e6-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae2e6-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="ae2e6-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Thoughtworks Mingle con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ae2e6-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ae2e6-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Thoughtworks Mingle para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Thoughtworks Mingle is to a user in Azure AD.</span></span> <span data-ttu-id="ae2e6-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-138">In other words, a link relationship between an Azure AD user and the related user in Thoughtworks Mingle needs to be established.</span></span>

<span data-ttu-id="ae2e6-139">Para establecer la relación de vínculo, en Thoughtworks Mingle, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-139">In Thoughtworks Mingle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ae2e6-140">Para configurar y probar el inicio de sesión único de Azure AD con Thoughtworks Mingle, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ae2e6-140">To configure and test Azure AD single sign-on with Thoughtworks Mingle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ae2e6-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ae2e6-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ae2e6-143">**[Creación de un usuario de prueba de Thoughtworks Mingle](#create-a-thoughtworks-mingle-test-user)**: para tener un homólogo de Britta Simon en Thoughtworks Mingle que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - to have a counterpart of Britta Simon in Thoughtworks Mingle that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ae2e6-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ae2e6-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ae2e6-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae2e6-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ae2e6-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span></span>

<span data-ttu-id="ae2e6-148">**Para configurar el inicio de sesión único de Azure AD con Thoughtworks Mingle, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="ae2e6-148">**To configure Azure AD single sign-on with Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="ae2e6-149">En la página de integración de la aplicación **Thoughtworks Mingle** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-149">In the Azure portal, on the **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="ae2e6-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. <span data-ttu-id="ae2e6-153">En la sección **Dominio y direcciones URL de Thoughtworks Mingle**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ae2e6-153">On the **Thoughtworks Mingle Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Thoughtworks Mingle](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    <span data-ttu-id="ae2e6-155">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.mingle.thoughtworks.com`.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mingle.thoughtworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ae2e6-156">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-156">The value is not real.</span></span> <span data-ttu-id="ae2e6-157">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-157">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="ae2e6-158">Póngase en contacto con el [equipo de soporte técnico de Thoughtworks Mingle](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) to get the value.</span></span> 
 
4. <span data-ttu-id="ae2e6-159">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. <span data-ttu-id="ae2e6-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="ae2e6-161">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ae2e6-163">Inicie sesión en su sitio de compañía de **Thoughtworks Mingle** como administrador.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-163">Log in to your **Thoughtworks Mingle** company site as administrator.</span></span>

7. <span data-ttu-id="ae2e6-164">Haga clic en la pestaña **Admin** (Administrador) y, luego, en **SSO Config** (Configuración de SSO).</span><span class="sxs-lookup"><span data-stu-id="ae2e6-164">Click the **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="ae2e6-165">![Pestaña de administrador](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "Configuración de SSO")</span><span class="sxs-lookup"><span data-stu-id="ae2e6-165">![Admin tab](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span></span>

8. <span data-ttu-id="ae2e6-166">En la sección **Configuración de SSO** , lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ae2e6-166">In the **SSO Config** section, perform the following steps:</span></span>
   
    <span data-ttu-id="ae2e6-167">![Configuración de SSO](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "Configuración de SSO")</span><span class="sxs-lookup"><span data-stu-id="ae2e6-167">![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span></span>
    
    <span data-ttu-id="ae2e6-168">a.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-168">a.</span></span> <span data-ttu-id="ae2e6-169">Para cargar el archivo de metadatos, haga clic en **Elegir archivo**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-169">To upload the metadata file, click **Choose file**.</span></span> 

    <span data-ttu-id="ae2e6-170">b.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-170">b.</span></span> <span data-ttu-id="ae2e6-171">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-171">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="ae2e6-172">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ae2e6-173">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ae2e6-174">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ae2e6-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ae2e6-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae2e6-175">Create an Azure AD test user</span></span>
<span data-ttu-id="ae2e6-176">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ae2e6-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="ae2e6-178">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="ae2e6-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ae2e6-179">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ae2e6-181">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ae2e6-183">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Botón Agregar](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ae2e6-185">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="ae2e6-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Cuadro de diálogo Usuario](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae2e6-187">a.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-187">a.</span></span> <span data-ttu-id="ae2e6-188">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae2e6-189">b.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-189">b.</span></span> <span data-ttu-id="ae2e6-190">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae2e6-191">c.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-191">c.</span></span> <span data-ttu-id="ae2e6-192">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ae2e6-193">d.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-193">d.</span></span> <span data-ttu-id="ae2e6-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-194">Click **Create**.</span></span>
 
### <a name="create-a-thoughtworks-mingle-test-user"></a><span data-ttu-id="ae2e6-195">Creación de un usuario de prueba de Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="ae2e6-195">Create a Thoughtworks Mingle test user</span></span>

<span data-ttu-id="ae2e6-196">Para que los usuarios de Azure AD puedan iniciar sesión, deben aprovisionarse en la aplicación Thoughtworks Mingle con sus nombres de usuario de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-196">For Azure AD users to be able to sign in, they must be provisioned to the Thoughtworks Mingle application using their Azure Active Directory user names.</span></span> <span data-ttu-id="ae2e6-197">En el caso de Thoughtworks Mingle, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-197">In the case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="ae2e6-198">**Siga estos pasos para configurar el aprovisionamiento de usuario:**</span><span class="sxs-lookup"><span data-stu-id="ae2e6-198">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="ae2e6-199">Inicie sesión en su sitio de compañía de Thoughtworks Mingle como administrador.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-199">Log in to your Thoughtworks Mingle company site as administrator.</span></span>

2. <span data-ttu-id="ae2e6-200">Haga clic en **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-200">Click **Profile**.</span></span>
   
    <span data-ttu-id="ae2e6-201">![Su primer proyecto](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Su primer proyecto")</span><span class="sxs-lookup"><span data-stu-id="ae2e6-201">![Your First Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span></span>

3. <span data-ttu-id="ae2e6-202">Haga clic en la pestaña **Admin** (Administrador) y, luego, en **Users** (Usuarios).</span><span class="sxs-lookup"><span data-stu-id="ae2e6-202">Click the **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="ae2e6-203">![Usuarios](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="ae2e6-203">![Users](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Users")</span></span>

4. <span data-ttu-id="ae2e6-204">Haga clic en **Nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-204">Click **New User**.</span></span>
   
    <span data-ttu-id="ae2e6-205">![Nuevo usuario](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="ae2e6-205">![New User](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "New User")</span></span>

5. <span data-ttu-id="ae2e6-206">En la página del cuadro de diálogo **Nuevo usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ae2e6-206">On the **New User** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="ae2e6-207">![Cuadro de diálogo Nuevo usuario](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="ae2e6-207">![New User dialog](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "New User")</span></span>  
 
    <span data-ttu-id="ae2e6-208">a.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-208">a.</span></span> <span data-ttu-id="ae2e6-209">En los cuadros de texto **Sign-in name** (Nombre de inicio de sesión), **Display name** (Nombre para mostrar), **Choose password** (Elegir contraseña) y **Confirm password** (Confirmar contraseña), escriba la información pertinente de una cuenta de Azure AD válida que desee aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-209">Type the **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want to provision into the related textboxes.</span></span> 

    <span data-ttu-id="ae2e6-210">b.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-210">b.</span></span> <span data-ttu-id="ae2e6-211">En **User type** (Tipo de usuario), seleccione **Full user** (Usuario completo).</span><span class="sxs-lookup"><span data-stu-id="ae2e6-211">As **User type**, select **Full user**.</span></span>

    <span data-ttu-id="ae2e6-212">c.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-212">c.</span></span> <span data-ttu-id="ae2e6-213">Haga clic en **Crear este perfil**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-213">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="ae2e6-214">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Thoughtworks Mingle ofrecida por Thoughtworks Mingle para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle to provision AAD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ae2e6-215">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae2e6-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="ae2e6-216">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Thoughtworks Mingle.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="ae2e6-218">**Para asignar a Britta Simon a Thoughtworks Mingle, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="ae2e6-218">**To assign Britta Simon to Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="ae2e6-219">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="ae2e6-221">En la lista de aplicaciones, seleccione **Thoughtworks Mingle**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-221">In the applications list, select **Thoughtworks Mingle**.</span></span>

    ![Vínculo a Thoughtworks Mingle en la lista de aplicaciones](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. <span data-ttu-id="ae2e6-223">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202] 

4. <span data-ttu-id="ae2e6-225">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-225">Click **Add** button.</span></span> <span data-ttu-id="ae2e6-226">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="ae2e6-228">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ae2e6-229">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ae2e6-230">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ae2e6-231">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="ae2e6-231">Test single sign-on</span></span>

<span data-ttu-id="ae2e6-232">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ae2e6-233">Al hacer clic en el icono de Thoughtworks Mingle en el panel de acceso, debería iniciar sesión automáticamente en la aplicación Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="ae2e6-233">When you click the Thoughtworks Mingle tile in the Access Panel, you should get automatically signed-on to your Thoughtworks Mingle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae2e6-234">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ae2e6-234">Additional resources</span></span>

* [<span data-ttu-id="ae2e6-235">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae2e6-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae2e6-236">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ae2e6-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

