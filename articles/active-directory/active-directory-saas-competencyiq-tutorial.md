---
title: "Tutorial: Integración de Azure Active Directory con CompetencyIQ | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y CompetencyIQ."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e262bf7e-cc7d-4d0e-aea7-861f00d8837d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: ad3cec3de9034ddab2161952620d31540ae51978
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-competencyiq"></a><span data-ttu-id="d919a-103">Tutorial: Integración de Azure Active Directory con CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="d919a-103">Tutorial: Azure Active Directory integration with CompetencyIQ</span></span>

<span data-ttu-id="d919a-104">En este tutorial, aprenderá a integrar CompetencyIQ con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d919a-104">In this tutorial, you learn how to integrate CompetencyIQ with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d919a-105">Integrar CompetencyIQ con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d919a-105">Integrating CompetencyIQ with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d919a-106">Puede controlar en Azure AD quién tiene acceso a CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="d919a-106">You can control in Azure AD who has access to CompetencyIQ</span></span>
- <span data-ttu-id="d919a-107">Puede permitir que los usuarios inicien sesión automáticamente en CompetencyIQ (Inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d919a-107">You can enable your users to automatically get signed-on to CompetencyIQ (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d919a-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d919a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d919a-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d919a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d919a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d919a-110">Prerequisites</span></span>

<span data-ttu-id="d919a-111">Para configurar la integración de Azure AD con CompetencyIQ, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d919a-111">To configure Azure AD integration with CompetencyIQ, you need the following items:</span></span>

- <span data-ttu-id="d919a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d919a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d919a-113">Una suscripción habilitada para el inicio de sesión único en CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="d919a-113">A CompetencyIQ single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d919a-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="d919a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d919a-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="d919a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d919a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d919a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d919a-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d919a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d919a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="d919a-118">Scenario description</span></span>
<span data-ttu-id="d919a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="d919a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d919a-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="d919a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d919a-121">Agregar CompetencyIQ desde la galería</span><span class="sxs-lookup"><span data-stu-id="d919a-121">Adding CompetencyIQ from the gallery</span></span>
2. <span data-ttu-id="d919a-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d919a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-competencyiq-from-the-gallery"></a><span data-ttu-id="d919a-123">Agregar CompetencyIQ desde la galería</span><span class="sxs-lookup"><span data-stu-id="d919a-123">Adding CompetencyIQ from the gallery</span></span>
<span data-ttu-id="d919a-124">Para configurar la integración de CompetencyIQ en Azure AD, debe agregar CompetencyIQ desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="d919a-124">To configure the integration of CompetencyIQ into Azure AD, you need to add CompetencyIQ from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d919a-125">**Para agregar CompetencyIQ desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d919a-125">**To add CompetencyIQ from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d919a-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d919a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d919a-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="d919a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d919a-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d919a-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="d919a-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d919a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="d919a-133">En el cuadro de búsqueda, escriba **CompetencyIQ**.</span><span class="sxs-lookup"><span data-stu-id="d919a-133">In the search box, type **CompetencyIQ**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_search.png)

5. <span data-ttu-id="d919a-135">En el panel de resultados, seleccione **CompetencyIQ** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d919a-135">In the results panel, select **CompetencyIQ**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d919a-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d919a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d919a-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con CompetencyIQ con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d919a-138">In this section, you configure and test Azure AD single sign-on with CompetencyIQ based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d919a-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de CompetencyIQ para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d919a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CompetencyIQ is to a user in Azure AD.</span></span> <span data-ttu-id="d919a-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="d919a-140">In other words, a link relationship between an Azure AD user and the related user in CompetencyIQ needs to be established.</span></span>

<span data-ttu-id="d919a-141">Para establecer la relación de vínculo, en CompetencyIQ, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="d919a-141">In CompetencyIQ, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d919a-142">Para configurar y probar el inicio de sesión único de Azure AD con CompetencyIQ, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d919a-142">To configure and test Azure AD single sign-on with CompetencyIQ, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d919a-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="d919a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d919a-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d919a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d919a-145">**[Creación de un usuario de prueba de CompetencyIQ](#creating-a-competencyiq-test-user)**: para tener un homólogo de Britta Simon en CompetencyIQ que esté vinculado a la representación de Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="d919a-145">**[Creating a CompetencyIQ test user](#creating-a-competencyiq-test-user)** - to have a counterpart of Britta Simon in CompetencyIQ that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d919a-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d919a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d919a-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="d919a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d919a-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d919a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d919a-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="d919a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CompetencyIQ application.</span></span>

<span data-ttu-id="d919a-150">**Para configurar el inicio de sesión único de Azure AD con CompetencyIQ, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d919a-150">**To configure Azure AD single sign-on with CompetencyIQ, perform the following steps:**</span></span>

1. <span data-ttu-id="d919a-151">En Azure Portal, en la página de integración de la aplicación **CompetencyIQ**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d919a-151">In the Azure portal, on the **CompetencyIQ** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="d919a-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d919a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_samlbase.png)

3. <span data-ttu-id="d919a-155">En la sección **Dominio y direcciones URL de CompetencyIQ**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d919a-155">On the **CompetencyIQ Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_url1.png)

    <span data-ttu-id="d919a-157">a.</span><span class="sxs-lookup"><span data-stu-id="d919a-157">a.</span></span> <span data-ttu-id="d919a-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<customer>.competencyiq.com/`.</span><span class="sxs-lookup"><span data-stu-id="d919a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<customer>.competencyiq.com/`</span></span>
    
    <span data-ttu-id="d919a-159">b.</span><span class="sxs-lookup"><span data-stu-id="d919a-159">b.</span></span> <span data-ttu-id="d919a-160">En el cuadro de texto **Identificador**, escriba la dirección URL: `https://www.competencyiq.com/`</span><span class="sxs-lookup"><span data-stu-id="d919a-160">In the **Identifier** textbox, type the URL: `https://www.competencyiq.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d919a-161">El valor de la dirección URL de inicio de sesión no es real de modo que debe actualizarla con esta.</span><span class="sxs-lookup"><span data-stu-id="d919a-161">The Sign-on URL value is not real so update this with actual Sign-On URL.</span></span> <span data-ttu-id="d919a-162">Póngase en contacto con el [equipo de soporte técnico de CompetencyIQ](https://www.competencyiq.com/) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="d919a-162">Contact [CompetencyIQ Client support team](https://www.competencyiq.com/) to get this.</span></span> 
 
4. <span data-ttu-id="d919a-163">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d919a-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_certificate.png) 

5. <span data-ttu-id="d919a-165">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="d919a-165">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-competencyiq-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d919a-167">En la sección **Configuración de CompetencyIQ**, haga clic en **Configurar CompetencyIQ** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="d919a-167">On the **CompetencyIQ Configuration** section, click **Configure CompetencyIQ** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d919a-168">Copie el **Identificador de entidad en SAML** y la **Dirección URL de inicio de sesión único de SAML** de la **sección Referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="d919a-168">Copy the **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_configure.png) 

7. <span data-ttu-id="d919a-170">Para configurar el inicio de sesión único en **CompetencyIQ**, debe enviar los datos descargados de **XML de metadatos**, **SAML Entity ID** (Identificador de entidad de SAML) y **SAML Single Sign-On Service URL** (Dirección URL de servicio de inicio de sesión de SAML) al [equipo de soporte técnico de CompetencyIQ](https://www.competencyiq.com/).</span><span class="sxs-lookup"><span data-stu-id="d919a-170">To configure single sign-on on **CompetencyIQ** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [CompetencyIQ support team](https://www.competencyiq.com/).</span></span> <span data-ttu-id="d919a-171">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="d919a-171">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d919a-172">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d919a-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d919a-173">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="d919a-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d919a-174">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d919a-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d919a-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d919a-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="d919a-176">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d919a-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="d919a-178">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="d919a-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d919a-179">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d919a-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d919a-181">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d919a-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d919a-183">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d919a-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d919a-185">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="d919a-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d919a-187">a.</span><span class="sxs-lookup"><span data-stu-id="d919a-187">a.</span></span> <span data-ttu-id="d919a-188">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d919a-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d919a-189">b.</span><span class="sxs-lookup"><span data-stu-id="d919a-189">b.</span></span> <span data-ttu-id="d919a-190">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d919a-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d919a-191">c.</span><span class="sxs-lookup"><span data-stu-id="d919a-191">c.</span></span> <span data-ttu-id="d919a-192">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="d919a-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d919a-193">d.</span><span class="sxs-lookup"><span data-stu-id="d919a-193">d.</span></span> <span data-ttu-id="d919a-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d919a-194">Click **Create**.</span></span>
 
### <a name="creating-a-competencyiq-test-user"></a><span data-ttu-id="d919a-195">Creación de un usuario de prueba de CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="d919a-195">Creating a CompetencyIQ test user</span></span>

<span data-ttu-id="d919a-196">Para permitir que los usuarios de Azure AD inicien sesión en CompetencyIQ, es necesario que se aprovisionen en CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="d919a-196">To enable Azure AD users to log in to CompetencyIQ, they must be provisioned into CompetencyIQ.</span></span> <span data-ttu-id="d919a-197">Póngase en contacto con [equipo de soporte técnico de CompetencyIQ](https://www.competencyiq.com/) para crear usuarios en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d919a-197">Contact [CompetencyIQ support team](https://www.competencyiq.com/) to create users in the application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d919a-198">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d919a-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d919a-199">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="d919a-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CompetencyIQ.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="d919a-201">**Para asignar a Britta Simon a CompetencyIQ, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d919a-201">**To assign Britta Simon to CompetencyIQ, perform the following steps:**</span></span>

1. <span data-ttu-id="d919a-202">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d919a-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="d919a-204">En la lista de aplicaciones, seleccione **CompetencyIQ**.</span><span class="sxs-lookup"><span data-stu-id="d919a-204">In the applications list, select **CompetencyIQ**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_app.png) 

3. <span data-ttu-id="d919a-206">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d919a-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="d919a-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d919a-208">Click **Add** button.</span></span> <span data-ttu-id="d919a-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d919a-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="d919a-211">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="d919a-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d919a-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d919a-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d919a-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d919a-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d919a-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="d919a-214">Testing single sign-on</span></span>

<span data-ttu-id="d919a-215">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d919a-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d919a-216">Al hacer clic en el icono de CompetencyIQ en el panel de acceso, debería iniciar sesión automáticamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d919a-216">When you click the CompetencyIQ tile in the Access Panel, you should get automatically logged into the application.</span></span>
<span data-ttu-id="d919a-217">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d919a-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d919a-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d919a-218">Additional resources</span></span>

* [<span data-ttu-id="d919a-219">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d919a-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d919a-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d919a-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_203.png

