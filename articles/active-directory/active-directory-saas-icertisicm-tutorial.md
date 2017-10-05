---
title: "Tutorial: Integración de Azure Active Directory con Icertis Contract Management Platform | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory e Icertis Contract Management Platform."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6627e6dd-f559-4cd4-a509-f6d9a4961b49
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 9dd002f71b7a960338071db869f7c8cf88071342
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icertis-contract-management-platform"></a><span data-ttu-id="72190-103">Tutorial: Integración de Azure Active Directory con Icertis Contract Management Platform</span><span class="sxs-lookup"><span data-stu-id="72190-103">Tutorial: Azure Active Directory integration with Icertis Contract Management Platform</span></span>

<span data-ttu-id="72190-104">En este tutorial, aprenderá a integrar Icertis Contract Management Platform con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="72190-104">In this tutorial, you learn how to integrate Icertis Contract Management Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="72190-105">Integrar Icertis Contract Management Platform con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="72190-105">Integrating Icertis Contract Management Platform with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="72190-106">Puede controlar en Azure AD quién tiene acceso a Icertis Contract Management Platform</span><span class="sxs-lookup"><span data-stu-id="72190-106">You can control in Azure AD who has access to Icertis Contract Management Platform</span></span>
- <span data-ttu-id="72190-107">Puede permitir que los usuarios inicien sesión automáticamente en Icertis Contract Management Platform (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72190-107">You can enable your users to automatically get signed-on to Icertis Contract Management Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="72190-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="72190-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="72190-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="72190-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72190-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="72190-110">Prerequisites</span></span>

<span data-ttu-id="72190-111">Para configurar la integración de Azure AD con Icertis Contract Management Platform, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="72190-111">To configure Azure AD integration with Icertis Contract Management Platform, you need the following items:</span></span>

- <span data-ttu-id="72190-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="72190-112">An Azure AD subscription</span></span>
- <span data-ttu-id="72190-113">Una suscripción habilitada para el inicio de sesión único de Icertis Contract Management Platform</span><span class="sxs-lookup"><span data-stu-id="72190-113">An Icertis Contract Management Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="72190-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="72190-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="72190-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="72190-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="72190-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="72190-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="72190-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="72190-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="72190-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="72190-118">Scenario description</span></span>
<span data-ttu-id="72190-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="72190-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="72190-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="72190-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="72190-121">Adición de Icertis Contract Management Platform desde la galería</span><span class="sxs-lookup"><span data-stu-id="72190-121">Adding Icertis Contract Management Platform from the gallery</span></span>
2. <span data-ttu-id="72190-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="72190-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icertis-contract-management-platform-from-the-gallery"></a><span data-ttu-id="72190-123">Adición de Icertis Contract Management Platform desde la galería</span><span class="sxs-lookup"><span data-stu-id="72190-123">Adding Icertis Contract Management Platform from the gallery</span></span>
<span data-ttu-id="72190-124">Para configurar la integración de Icertis Contract Management Platform en Azure AD, debe agregar Icertis Contract Management Platform de la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="72190-124">To configure the integration of Icertis Contract Management Platform into Azure AD, you need to add Icertis Contract Management Platform from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="72190-125">**Para agregar Icertis Contract Management Platform de la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="72190-125">**To add Icertis Contract Management Platform from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="72190-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="72190-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="72190-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="72190-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="72190-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="72190-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="72190-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72190-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="72190-133">En el cuadro de búsqueda, escriba **Icertis Contract Management Platform**.</span><span class="sxs-lookup"><span data-stu-id="72190-133">In the search box, type **Icertis Contract Management Platform**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_search.png)

5. <span data-ttu-id="72190-135">En el panel de resultados, seleccione **Icertis Contract Management Platform** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="72190-135">In the results panel, select **Icertis Contract Management Platform**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="72190-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="72190-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="72190-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Icertis Contract Management Platform con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="72190-138">In this section, you configure and test Azure AD single sign-on with Icertis Contract Management Platform based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="72190-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Icertis Contract Management Platform para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72190-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Icertis Contract Management Platform is to a user in Azure AD.</span></span> <span data-ttu-id="72190-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Icertis Contract Management Platform.</span><span class="sxs-lookup"><span data-stu-id="72190-140">In other words, a link relationship between an Azure AD user and the related user in Icertis Contract Management Platform needs to be established.</span></span>

<span data-ttu-id="72190-141">Para establecer la relación de vínculo, en Icertis Contract Management Platform, asigne el valor del **nombre de usuario** en Azure AD como valor del **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="72190-141">In Icertis Contract Management Platform, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="72190-142">Para configurar y probar el inicio de sesión único de Azure AD con Icertis Contract Management Platform, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="72190-142">To configure and test Azure AD single sign-on with Icertis Contract Management Platform, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="72190-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="72190-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="72190-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="72190-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="72190-145">**[Creación de un usuario de prueba de Icertis Contract Management Platform](#creating-an-icertis-contract-management-platform-test-user)**: para que en Icertis Contract Management Platform haya un homólogo de Britta Simon que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72190-145">**[Creating an Icertis Contract Management Platform test user](#creating-an-icertis-contract-management-platform-test-user)** - to have a counterpart of Britta Simon in Icertis Contract Management Platform that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="72190-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72190-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="72190-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="72190-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="72190-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="72190-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="72190-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Icertis Contract Management Platform.</span><span class="sxs-lookup"><span data-stu-id="72190-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Icertis Contract Management Platform application.</span></span>

<span data-ttu-id="72190-150">**Para configurar el inicio de sesión único de Azure AD con Icertis Contract Management Platform, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="72190-150">**To configure Azure AD single sign-on with Icertis Contract Management Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="72190-151">En el Azure Portal, en la página de integración de la aplicación **Icertis Contract Management Platform**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="72190-151">In the Azure portal, on the **Icertis Contract Management Platform** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="72190-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="72190-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_samlbase.png)

3. <span data-ttu-id="72190-155">En la sección **Dominio y direcciones URL de Icertis Contract Management Platform**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="72190-155">On the **Icertis Contract Management Platform Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_url.png)

    <span data-ttu-id="72190-157">a.</span><span class="sxs-lookup"><span data-stu-id="72190-157">a.</span></span> <span data-ttu-id="72190-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<company name>.icertis.com`.</span><span class="sxs-lookup"><span data-stu-id="72190-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.icertis.com`</span></span>

    <span data-ttu-id="72190-159">b.</span><span class="sxs-lookup"><span data-stu-id="72190-159">b.</span></span> <span data-ttu-id="72190-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<company name>.icertis.com`</span><span class="sxs-lookup"><span data-stu-id="72190-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.icertis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="72190-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="72190-161">These values are not real.</span></span> <span data-ttu-id="72190-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="72190-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="72190-163">Para obtener estos valores, póngase en contacto con el [equipo de soporte técnico de clientes de Icertis Contract Management Platform](https://www.icertis.com/company/contact/).</span><span class="sxs-lookup"><span data-stu-id="72190-163">Contact [Icertis Contract Management Platform Client support team](https://www.icertis.com/company/contact/) to get these values.</span></span> 

4. <span data-ttu-id="72190-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="72190-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_certificate.png) 

5. <span data-ttu-id="72190-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="72190-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-icertisicm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="72190-168">En la sección **Configuración de Icertis Contract Management Platform**, haga clic en **Configurar Icertis Contract Management Platform** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="72190-168">On the **Icertis Contract Management Platform Configuration** section, click **Configure Icertis Contract Management Platform** to open **Configure sign-on** window.</span></span> <span data-ttu-id="72190-169">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="72190-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_configure.png) 

7. <span data-ttu-id="72190-171">Para configurar el inicio de sesión único en **Icertis Contract Management Platform**, es preciso enviar los valores descargados de **XML de metadatos**, **Dirección URL de cierre de sesión, SAML Entity ID (Identificador de entidad de SAML) y SAML Single Sign-On Service URL (Dirección URL del servicio de inicio de sesión único de SAML)** al [equipo de soporte técnico de Icertis Contract Management Platform](https://www.icertis.com/company/contact/).</span><span class="sxs-lookup"><span data-stu-id="72190-171">To configure single sign-on on **Icertis Contract Management Platform** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="72190-172">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="72190-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="72190-173">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="72190-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="72190-174">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="72190-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="72190-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="72190-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="72190-176">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="72190-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="72190-178">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="72190-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="72190-179">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="72190-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="72190-181">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="72190-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="72190-183">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72190-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="72190-185">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="72190-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="72190-187">a.</span><span class="sxs-lookup"><span data-stu-id="72190-187">a.</span></span> <span data-ttu-id="72190-188">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="72190-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="72190-189">b.</span><span class="sxs-lookup"><span data-stu-id="72190-189">b.</span></span> <span data-ttu-id="72190-190">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="72190-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="72190-191">c.</span><span class="sxs-lookup"><span data-stu-id="72190-191">c.</span></span> <span data-ttu-id="72190-192">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="72190-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="72190-193">d.</span><span class="sxs-lookup"><span data-stu-id="72190-193">d.</span></span> <span data-ttu-id="72190-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="72190-194">Click **Create**.</span></span>
 
### <a name="creating-an-icertis-contract-management-platform-test-user"></a><span data-ttu-id="72190-195">Creación de un usuario de prueba de Icertis Contract Management Platform</span><span class="sxs-lookup"><span data-stu-id="72190-195">Creating an Icertis Contract Management Platform test user</span></span>

<span data-ttu-id="72190-196">En esta sección, creará un usuario llamado Britta Simon en Icertis Contract Management Platform.</span><span class="sxs-lookup"><span data-stu-id="72190-196">In this section, you create a user called Britta Simon in Icertis Contract Management Platform.</span></span> <span data-ttu-id="72190-197">Trabaje con el equipo de soporte técnico de [Icertis Contract Management Platform](https://www.icertis.com/company/contact/) para agregar usuarios a Icertis Contract Management Platform.</span><span class="sxs-lookup"><span data-stu-id="72190-197">Please work with [Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/) to add the users in the Icertis Contract Management Platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="72190-198">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="72190-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="72190-199">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure, para lo que se le concederá acceso a Icertis Contract Management Platform.</span><span class="sxs-lookup"><span data-stu-id="72190-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Icertis Contract Management Platform.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="72190-201">**Para asignar a Britta Simon a Icertis Contract Management Platform, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="72190-201">**To assign Britta Simon to Icertis Contract Management Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="72190-202">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="72190-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="72190-204">En la lista de aplicaciones, seleccione **Icertis Contract Management Platform**.</span><span class="sxs-lookup"><span data-stu-id="72190-204">In the applications list, select **Icertis Contract Management Platform**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_app.png) 

3. <span data-ttu-id="72190-206">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="72190-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="72190-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="72190-208">Click **Add** button.</span></span> <span data-ttu-id="72190-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="72190-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="72190-211">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="72190-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="72190-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="72190-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="72190-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="72190-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="72190-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="72190-214">Testing single sign-on</span></span>

<span data-ttu-id="72190-215">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="72190-215">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="72190-216">Al hacer clic en el icono de Icertis Contract Management Platform en el Panel de acceso, debería haber iniciado sesión automáticamente en la aplicación Icertis Contract Management Platform.</span><span class="sxs-lookup"><span data-stu-id="72190-216">When you click the Icertis Contract Management Platform tile in the Access Panel, you should get automatically signed-on to your Icertis Contract Management Platform application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="72190-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="72190-217">Additional resources</span></span>

* [<span data-ttu-id="72190-218">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="72190-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="72190-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="72190-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_203.png

