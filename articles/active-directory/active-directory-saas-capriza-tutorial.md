---
title: "Tutorial: Integración de Azure Active Directory con Capriza Platform | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y Capriza Platform."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48d92247-f00a-47b9-8d4e-137028d9e200
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 668c094d5330be1c5f71d51d2e76170dc69d1bce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-capriza-platform"></a><span data-ttu-id="d3ce6-103">Tutorial: Integración de Azure Active Directory con Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="d3ce6-103">Tutorial: Azure Active Directory integration with Capriza Platform</span></span>

<span data-ttu-id="d3ce6-104">En este tutorial, obtendrá información sobre cómo integrar Capriza Platform con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d3ce6-104">In this tutorial, you learn how to integrate Capriza Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d3ce6-105">La integración de Capriza Platform con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d3ce6-105">Integrating Capriza Platform with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d3ce6-106">En Azure AD puede controlar quién tiene acceso a Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="d3ce6-106">You can control in Azure AD who has access to Capriza Platform</span></span>
- <span data-ttu-id="d3ce6-107">Puede permitir que los usuarios inicien sesión automáticamente en Capriza Platform (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3ce6-107">You can enable your users to automatically get signed-on to Capriza Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d3ce6-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d3ce6-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d3ce6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3ce6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d3ce6-110">Prerequisites</span></span>

<span data-ttu-id="d3ce6-111">Para configurar la integración de Azure AD con Capriza Platform, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d3ce6-111">To configure Azure AD integration with Capriza Platform, you need the following items:</span></span>

- <span data-ttu-id="d3ce6-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3ce6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d3ce6-113">Una suscripción habilitada para inicio de sesión único en Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="d3ce6-113">A Capriza Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d3ce6-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d3ce6-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="d3ce6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d3ce6-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d3ce6-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d3ce6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d3ce6-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="d3ce6-118">Scenario description</span></span>
<span data-ttu-id="d3ce6-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d3ce6-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="d3ce6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d3ce6-121">Incorporación de Capriza Platform desde la galería</span><span class="sxs-lookup"><span data-stu-id="d3ce6-121">Adding Capriza Platform from the gallery</span></span>
2. <span data-ttu-id="d3ce6-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3ce6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-capriza-platform-from-the-gallery"></a><span data-ttu-id="d3ce6-123">Incorporación de Capriza Platform desde la galería</span><span class="sxs-lookup"><span data-stu-id="d3ce6-123">Adding Capriza Platform from the gallery</span></span>
<span data-ttu-id="d3ce6-124">Para configurar la integración de Capriza Platform en Azure AD, deberá agregar Capriza Platform desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-124">To configure the integration of Capriza Platform into Azure AD, you need to add Capriza Platform from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d3ce6-125">**Para agregar Capriza Platform desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d3ce6-125">**To add Capriza Platform from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d3ce6-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d3ce6-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d3ce6-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="d3ce6-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="d3ce6-133">En el cuadro de búsqueda, escriba **Capriza Platform**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-133">In the search box, type **Capriza Platform**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_search.png)

5. <span data-ttu-id="d3ce6-135">En el panel de resultados, seleccione **Capriza Platform** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-135">In the results panel, select **Capriza Platform**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d3ce6-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3ce6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d3ce6-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Capriza Platform con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d3ce6-138">In this section, you configure and test Azure AD single sign-on with Capriza Platform based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d3ce6-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Capriza Platform para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Capriza Platform is to a user in Azure AD.</span></span> <span data-ttu-id="d3ce6-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Capriza Platform.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-140">In other words, a link relationship between an Azure AD user and the related user in Capriza Platform needs to be established.</span></span>

<span data-ttu-id="d3ce6-141">Para establecer la relación de vínculo, en Capriza Platform, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-141">In Capriza Platform, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d3ce6-142">Para configurar y probar el inicio de sesión único de Azure AD con Capriza Platform, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d3ce6-142">To configure and test Azure AD single sign-on with Capriza Platform, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d3ce6-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d3ce6-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d3ce6-145">**[Creación de un usuario de prueba de Capriza Platform](#creating-a-capriza-platform-test-user)**: para tener un homólogo de Britta Simon en Capriza Platform que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-145">**[Creating a Capriza Platform test user](#creating-a-capriza-platform-test-user)** - to have a counterpart of Britta Simon in Capriza Platform that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d3ce6-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d3ce6-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d3ce6-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3ce6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d3ce6-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Capriza Platform.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Capriza Platform application.</span></span>

<span data-ttu-id="d3ce6-150">**Para configurar el inicio de sesión único de Azure AD con Capriza Platform, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d3ce6-150">**To configure Azure AD single sign-on with Capriza Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="d3ce6-151">En Azure Portal, en la página de integración de la aplicación **Capriza Platform**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-151">In the Azure portal, on the **Capriza Platform** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="d3ce6-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_samlbase.png)

3. <span data-ttu-id="d3ce6-155">En la sección **Dominio y direcciones URL de Capriza Platform**, lleve a cabo los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="d3ce6-155">On the **Capriza Platform Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_url.png)

    <span data-ttu-id="d3ce6-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.capriza.com/<tenantid>`.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.capriza.com/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d3ce6-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-158">This value is not real.</span></span> <span data-ttu-id="d3ce6-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="d3ce6-160">Póngase en contacto con el [equipo de soporte técnico de cliente de Capriza Platform](mailTo:support@capriza.com) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-160">Contact [Capriza Platform Client support team](mailTo:support@capriza.com) to get this value.</span></span> 

4. <span data-ttu-id="d3ce6-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_certificate.png) 

5. <span data-ttu-id="d3ce6-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="d3ce6-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-capriza-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d3ce6-165">En la sección **Configuración de Capriza Platform**, haga clic en **Configurar Capriza Platform** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-165">On the **Capriza Platform Configuration** section, click **Configure Capriza Platform** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d3ce6-166">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_configure.png) 

7. <span data-ttu-id="d3ce6-168">Para configurar el inicio de sesión único en **Capriza Platform**, es preciso enviar el **certificado** descargado, la **dirección URL de cierre de sesión**, el **identificador de identidad de SAML** y la **dirección URL del servicio de inicio de sesión único de SAML** al [equipo de soporte técnico de Capriza Platform](mailTo:support@capriza.com).</span><span class="sxs-lookup"><span data-stu-id="d3ce6-168">To configure single sign-on on **Capriza Platform** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [Capriza Platform support team](mailTo:support@capriza.com).</span></span> <span data-ttu-id="d3ce6-169">Ellos se encargan de realizar esta configuración para que la conexión de SSO de SAML esté establecida correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d3ce6-170">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d3ce6-171">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d3ce6-172">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d3ce6-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d3ce6-173">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3ce6-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="d3ce6-174">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d3ce6-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="d3ce6-176">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="d3ce6-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d3ce6-177">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d3ce6-179">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d3ce6-181">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d3ce6-183">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="d3ce6-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d3ce6-185">a.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-185">a.</span></span> <span data-ttu-id="d3ce6-186">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d3ce6-187">b.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-187">b.</span></span> <span data-ttu-id="d3ce6-188">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d3ce6-189">c.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-189">c.</span></span> <span data-ttu-id="d3ce6-190">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d3ce6-191">d.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-191">d.</span></span> <span data-ttu-id="d3ce6-192">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-192">Click **Create**.</span></span>
 
### <a name="creating-a-capriza-platform-test-user"></a><span data-ttu-id="d3ce6-193">Creación de un usuario de prueba de Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="d3ce6-193">Creating a Capriza Platform test user</span></span>

<span data-ttu-id="d3ce6-194">El objetivo de esta sección es crear un usuario llamado Britta Simon en Capriza.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-194">The objective of this section is to create a user called Britta Simon in Capriza.</span></span> <span data-ttu-id="d3ce6-195">Capriza admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-195">Capriza supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="d3ce6-196">**Asegúrese de que el nombre de dominio está configurado con Capriza Platform para el aprovisionamiento de usuarios. Después de eso solo el aprovisionamiento de usuarios Just-In-Time funcionará.**</span><span class="sxs-lookup"><span data-stu-id="d3ce6-196">**Please make sure that your domain name is configured with Capriza for user provisioning. After that only the just-in-time user provisioning will work.**</span></span>

<span data-ttu-id="d3ce6-197">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-197">There is no action item for you in this section.</span></span> <span data-ttu-id="d3ce6-198">Durante un intento de acceder a Capriza se creará un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-198">A new user will be created during an attempt to access Capriza if it doesn't exist yet.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d3ce6-199">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3ce6-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d3ce6-200">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Capriza Platform.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Capriza Platform.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="d3ce6-202">**Para asignar a Britta Simon a Capriza Platform, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d3ce6-202">**To assign Britta Simon to Capriza Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="d3ce6-203">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="d3ce6-205">En la lista de aplicaciones, seleccione **Capriza Platform**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-205">In the applications list, select **Capriza Platform**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_app.png) 

3. <span data-ttu-id="d3ce6-207">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="d3ce6-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-209">Click **Add** button.</span></span> <span data-ttu-id="d3ce6-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="d3ce6-212">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d3ce6-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d3ce6-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d3ce6-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="d3ce6-215">Testing single sign-on</span></span>

<span data-ttu-id="d3ce6-216">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d3ce6-217">Al hacer clic en el icono de Capriza Platform en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Capriza Platform.</span><span class="sxs-lookup"><span data-stu-id="d3ce6-217">When you click the Capriza Platform tile in the Access Panel, you should get automatically signed-on to your Capriza application.</span></span> <span data-ttu-id="d3ce6-218">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d3ce6-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d3ce6-219">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d3ce6-219">Additional resources</span></span>

* [<span data-ttu-id="d3ce6-220">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d3ce6-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d3ce6-221">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d3ce6-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_203.png

