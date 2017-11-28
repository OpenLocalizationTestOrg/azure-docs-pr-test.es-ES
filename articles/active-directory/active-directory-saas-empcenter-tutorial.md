---
title: "Tutorial: Integración de Azure Active Directory con EmpCenter | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y EmpCenter."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a00ecf6e-917a-4284-b998-41506931585e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: aa27175165f4b15477bef4e70ad1c25016db31a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-empcenter"></a><span data-ttu-id="d6163-103">Tutorial: integración de Azure Active Directory con EmpCenter</span><span class="sxs-lookup"><span data-stu-id="d6163-103">Tutorial: Azure Active Directory integration with EmpCenter</span></span>

<span data-ttu-id="d6163-104">En este tutorial, obtendrá información sobre cómo integrar EmpCenter con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d6163-104">In this tutorial, you learn how to integrate EmpCenter with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d6163-105">La integración de EmpCenter con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d6163-105">Integrating EmpCenter with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d6163-106">Puede controlar en Azure AD quién tiene acceso a EmpCenter</span><span class="sxs-lookup"><span data-stu-id="d6163-106">You can control in Azure AD who has access to EmpCenter</span></span>
- <span data-ttu-id="d6163-107">Puede permitir que los usuarios inicien sesión automáticamente en EmpCenter (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6163-107">You can enable your users to automatically get signed-on to EmpCenter (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d6163-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d6163-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d6163-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d6163-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6163-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d6163-110">Prerequisites</span></span>

<span data-ttu-id="d6163-111">Para configurar la integración de Azure AD con EmpCenter, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d6163-111">To configure Azure AD integration with EmpCenter, you need the following items:</span></span>

- <span data-ttu-id="d6163-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6163-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d6163-113">Una suscripción habilitada para el inicio de sesión único en EmpCenter</span><span class="sxs-lookup"><span data-stu-id="d6163-113">An EmpCenter single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d6163-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="d6163-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d6163-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="d6163-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d6163-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d6163-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d6163-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d6163-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d6163-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="d6163-118">Scenario description</span></span>
<span data-ttu-id="d6163-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="d6163-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d6163-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="d6163-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d6163-121">Agregación de EmpCenter desde la galería</span><span class="sxs-lookup"><span data-stu-id="d6163-121">Adding EmpCenter from the gallery</span></span>
2. <span data-ttu-id="d6163-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6163-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-empcenter-from-the-gallery"></a><span data-ttu-id="d6163-123">Agregación de EmpCenter desde la galería</span><span class="sxs-lookup"><span data-stu-id="d6163-123">Adding EmpCenter from the gallery</span></span>
<span data-ttu-id="d6163-124">Para configurar la integración de EmpCenter en Azure AD, deberá agregar EmpCenter desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="d6163-124">To configure the integration of EmpCenter into Azure AD, you need to add EmpCenter from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d6163-125">**Para agregar EmpCenter desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d6163-125">**To add EmpCenter from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d6163-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d6163-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d6163-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="d6163-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d6163-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d6163-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="d6163-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d6163-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="d6163-133">En el cuadro de búsqueda, escriba **EmpCenter**.</span><span class="sxs-lookup"><span data-stu-id="d6163-133">In the search box, type **EmpCenter**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_search.png)

5. <span data-ttu-id="d6163-135">En el panel de resultados, seleccione **EmpCenter** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d6163-135">In the results panel, select **EmpCenter**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d6163-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6163-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d6163-138">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con EmpCenter con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d6163-138">In this section, you configure and test Azure AD single sign-on with EmpCenter based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d6163-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de EmpCenter para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6163-139">For single sign-on to work, Azure AD needs to know what the counterpart user in EmpCenter is to a user in Azure AD.</span></span> <span data-ttu-id="d6163-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="d6163-140">In other words, a link relationship between an Azure AD user and the related user in EmpCenter needs to be established.</span></span>

<span data-ttu-id="d6163-141">Para establecer la relación de vínculo, en EmpCenter, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="d6163-141">In EmpCenter, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d6163-142">Para configurar y probar el inicio de sesión único de Azure AD con EmpCenter, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d6163-142">To configure and test Azure AD single sign-on with EmpCenter, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d6163-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="d6163-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d6163-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d6163-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d6163-145">**[Creación de un usuario de prueba de EmpCenter](#creating-an-empcenter-test-user)**: para tener un homólogo de Britta Simon en EmpCenter que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6163-145">**[Creating an EmpCenter test user](#creating-an-empcenter-test-user)** - to have a counterpart of Britta Simon in EmpCenter that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d6163-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6163-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d6163-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="d6163-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d6163-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6163-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d6163-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="d6163-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EmpCenter application.</span></span>

<span data-ttu-id="d6163-150">**Para configurar el inicio de sesión único de Azure AD con EmpCenter, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d6163-150">**To configure Azure AD single sign-on with EmpCenter, perform the following steps:**</span></span>

1. <span data-ttu-id="d6163-151">En Azure Portal, en la página de integración de la aplicación **EmpCenter**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d6163-151">In the Azure portal, on the **EmpCenter** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="d6163-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d6163-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_samlbase.png)

3. <span data-ttu-id="d6163-155">En la sección **Dominio y direcciones URL de EmpCenter**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d6163-155">On the **EmpCenter Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_url.png)

    <span data-ttu-id="d6163-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="d6163-157">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.EmpCenter.com/<instancename>` |
    | `https://<subdomain>.workforcehosting.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="d6163-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="d6163-158">The value is not real.</span></span> <span data-ttu-id="d6163-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="d6163-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="d6163-160">Póngase en contacto con el [equipo de soporte técnico de EmpCenter](http://www.workforcesoftware.com/services/customer-support/) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="d6163-160">Contact [EmpCenter Client support team](http://www.workforcesoftware.com/services/customer-support/) to get the value.</span></span> 
 
4. <span data-ttu-id="d6163-161">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d6163-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_certificate.png) 

5. <span data-ttu-id="d6163-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="d6163-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d6163-165">Para configurar el inicio de sesión único en **EmpCenter**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de EmpCenter](http://www.workforcesoftware.com/services/customer-support/).</span><span class="sxs-lookup"><span data-stu-id="d6163-165">To configure single sign-on on **EmpCenter** side, you need to send the downloaded **Metadata XML** to [EmpCenter support team](http://www.workforcesoftware.com/services/customer-support/).</span></span> <span data-ttu-id="d6163-166">El equipo de soporte técnico lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="d6163-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d6163-167">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d6163-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d6163-168">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="d6163-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d6163-169">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d6163-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d6163-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6163-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="d6163-171">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d6163-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="d6163-173">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="d6163-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d6163-174">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d6163-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d6163-176">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d6163-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d6163-178">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d6163-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d6163-180">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="d6163-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d6163-182">a.</span><span class="sxs-lookup"><span data-stu-id="d6163-182">a.</span></span> <span data-ttu-id="d6163-183">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d6163-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d6163-184">b.</span><span class="sxs-lookup"><span data-stu-id="d6163-184">b.</span></span> <span data-ttu-id="d6163-185">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d6163-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d6163-186">c.</span><span class="sxs-lookup"><span data-stu-id="d6163-186">c.</span></span> <span data-ttu-id="d6163-187">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="d6163-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d6163-188">d.</span><span class="sxs-lookup"><span data-stu-id="d6163-188">d.</span></span> <span data-ttu-id="d6163-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d6163-189">Click **Create**.</span></span>
 
### <a name="creating-an-empcenter-test-user"></a><span data-ttu-id="d6163-190">Creación de un usuario de prueba EmpCenter</span><span class="sxs-lookup"><span data-stu-id="d6163-190">Creating an EmpCenter test user</span></span>

<span data-ttu-id="d6163-191">Para permitir que los usuarios de Azure AD inicien sesión en EmpCenter, deben aprovisionarse en EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="d6163-191">In order to enable Azure AD users to log in to EmpCenter, they must be provisioned into EmpCenter.</span></span> <span data-ttu-id="d6163-192">En el caso de EmpCenter, las cuentas de usuario debe crearlas el [equipo de soporte técnico de EmpCenter](http://www.workforcesoftware.com/services/customer-support/).</span><span class="sxs-lookup"><span data-stu-id="d6163-192">In the case of EmpCenter, the user accounts need to be created by your [EmpCenter support team](http://www.workforcesoftware.com/services/customer-support/).</span></span>

> [!NOTE]
> <span data-ttu-id="d6163-193">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de EmpCenter que proporcione EmpCenter para aprovisionar cuentas de usuario de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d6163-193">You can use any other EmpCenter user account creation tools or APIs provided by EmpCenter to provision Azure Active Directory user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d6163-194">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6163-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d6163-195">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="d6163-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EmpCenter.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="d6163-197">**Para asignar a Britta Simon a EmpCenter, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d6163-197">**To assign Britta Simon to EmpCenter, perform the following steps:**</span></span>

1. <span data-ttu-id="d6163-198">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d6163-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="d6163-200">En la lista de aplicaciones, seleccione **EmpCenter**.</span><span class="sxs-lookup"><span data-stu-id="d6163-200">In the applications list, select **EmpCenter**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_app.png) 

3. <span data-ttu-id="d6163-202">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d6163-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="d6163-204">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d6163-204">Click **Add** button.</span></span> <span data-ttu-id="d6163-205">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d6163-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="d6163-207">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="d6163-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d6163-208">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d6163-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d6163-209">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d6163-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d6163-210">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="d6163-210">Testing single sign-on</span></span>


<span data-ttu-id="d6163-211">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d6163-211">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d6163-212">Al hacer clic en el icono de EmpCenter en el panel de acceso, debe iniciar sesión automáticamente en su aplicación EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="d6163-212">When you click the EmpCenter tile in the Access Panel, you should get automatically signed-on to your EmpCenter application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d6163-213">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d6163-213">Additional resources</span></span>

* [<span data-ttu-id="d6163-214">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6163-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d6163-215">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d6163-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_203.png

