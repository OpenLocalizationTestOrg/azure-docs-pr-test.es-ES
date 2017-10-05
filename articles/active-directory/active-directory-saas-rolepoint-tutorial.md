---
title: "Tutorial: Integración de Azure Active Directory con RolePoint | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y RolePoint."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68d37f40-15da-45f5-a9e1-d53f78e786d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: jeedes
ms.openlocfilehash: fcde562484f4401e9f936614b9978f839f4aa290
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rolepoint"></a><span data-ttu-id="d7ac0-103">Tutorial: Integración de Azure Active Directory con RolePoint</span><span class="sxs-lookup"><span data-stu-id="d7ac0-103">Tutorial: Azure Active Directory integration with RolePoint</span></span>

<span data-ttu-id="d7ac0-104">En este tutorial, aprenderá a integrar RolePoint con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d7ac0-104">In this tutorial, you learn how to integrate RolePoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d7ac0-105">La integración de RolePoint con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d7ac0-105">Integrating RolePoint with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d7ac0-106">Puede controlar en Azure AD quién tiene acceso a RolePoint.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-106">You can control in Azure AD who has access to RolePoint</span></span>
- <span data-ttu-id="d7ac0-107">Puede permitir que los usuarios inicien sesión automáticamente en RolePoint (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-107">You can enable your users to automatically get signed-on to RolePoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d7ac0-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d7ac0-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d7ac0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7ac0-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d7ac0-110">Prerequisites</span></span>

<span data-ttu-id="d7ac0-111">Para configurar la integración de Azure AD con RolePoint, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d7ac0-111">To configure Azure AD integration with RolePoint, you need the following items:</span></span>

- <span data-ttu-id="d7ac0-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7ac0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d7ac0-113">Una suscripción habilitada para el inicio de sesión único en RolePoint.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-113">A RolePoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d7ac0-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d7ac0-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="d7ac0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d7ac0-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d7ac0-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d7ac0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d7ac0-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="d7ac0-118">Scenario description</span></span>
<span data-ttu-id="d7ac0-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d7ac0-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="d7ac0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d7ac0-121">Adición de RolePoint desde la galería</span><span class="sxs-lookup"><span data-stu-id="d7ac0-121">Adding RolePoint from the gallery</span></span>
2. <span data-ttu-id="d7ac0-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7ac0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rolepoint-from-the-gallery"></a><span data-ttu-id="d7ac0-123">Adición de RolePoint desde la galería</span><span class="sxs-lookup"><span data-stu-id="d7ac0-123">Adding RolePoint from the gallery</span></span>
<span data-ttu-id="d7ac0-124">Para configurar la integración de RolePoint en Azure AD, deberá agregar RolePoint desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-124">To configure the integration of RolePoint into Azure AD, you need to add RolePoint from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d7ac0-125">**Para agregar RolePoint desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="d7ac0-125">**To add RolePoint from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d7ac0-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d7ac0-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d7ac0-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="d7ac0-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="d7ac0-133">En el cuadro de búsqueda, escriba **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-133">In the search box, type **RolePoint**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_search.png)

5. <span data-ttu-id="d7ac0-135">En el panel de resultados, seleccione **RolePoint** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-135">In the results panel, select **RolePoint**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d7ac0-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7ac0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d7ac0-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con RolePoint con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d7ac0-138">In this section, you configure and test Azure AD single sign-on with RolePoint based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d7ac0-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de RolePoint para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RolePoint is to a user in Azure AD.</span></span> <span data-ttu-id="d7ac0-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de RolePoint.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-140">In other words, a link relationship between an Azure AD user and the related user in RolePoint needs to be established.</span></span>

<span data-ttu-id="d7ac0-141">Esta relación de vínculo se establece asignando el valor de **nombre de usuario** de Azure AD como el valor de **nombre de usuario** de RolePoint.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in RolePoint.</span></span>

<span data-ttu-id="d7ac0-142">Para configurar y probar el inicio de sesión único de Azure AD con RolePoint, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d7ac0-142">To configure and test Azure AD single sign-on with RolePoint, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d7ac0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d7ac0-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d7ac0-145">**[Creación de un usuario de prueba de RolePoint](#creating-a-rolepoint-test-user)**: el objetivo es tener un homólogo de Britta Simon en RolePoint que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-145">**[Creating a RolePoint test user](#creating-a-rolepoint-test-user)** - to have a counterpart of Britta Simon in RolePoint that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d7ac0-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d7ac0-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d7ac0-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7ac0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d7ac0-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación RolePoint.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RolePoint application.</span></span>

<span data-ttu-id="d7ac0-150">**Para configurar el inicio de sesión único de Azure AD con RolePoint, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d7ac0-150">**To configure Azure AD single sign-on with RolePoint, perform the following steps:**</span></span>

1. <span data-ttu-id="d7ac0-151">En la página de integración de la aplicación **RolePoint** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-151">In the Azure portal, on the **RolePoint** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="d7ac0-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_samlbase.png)

3. <span data-ttu-id="d7ac0-155">En la sección **Dominio y direcciones URL de RolePoint**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d7ac0-155">On the **RolePoint Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_url.png)

    <span data-ttu-id="d7ac0-157">a.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-157">a.</span></span> <span data-ttu-id="d7ac0-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.rolepoint.com/login`.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.rolepoint.com/login`</span></span>
    
    <span data-ttu-id="d7ac0-159">b.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-159">b.</span></span> <span data-ttu-id="d7ac0-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://app.rolepoint.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="d7ac0-160">In the **Identifier** textbox, type a URL using the following pattern: `https://app.rolepoint.com/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d7ac0-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-161">These values are not the real.</span></span> <span data-ttu-id="d7ac0-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="d7ac0-163">Aquí se recomienda usar el valor de cadena único en el identificador. Póngase en contacto con el [equipo de soporte técnico de RolePoint](mailto:info@rolepoint.com) para obtener el valor.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-163">Here we suggest you to use the unique value of string in the Identifier.Contact [RolePoint support team](mailto:info@rolepoint.com) to get the value.</span></span> 
 
4. <span data-ttu-id="d7ac0-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_certificate.png) 

5. <span data-ttu-id="d7ac0-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="d7ac0-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rolepoint-tutorial/tutorial_general_400.png)


6. <span data-ttu-id="d7ac0-168">Para configurar el inicio de sesión único en **RolePoint**, debe enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de RolePoint](mailto:info@rolepoint.com).</span><span class="sxs-lookup"><span data-stu-id="d7ac0-168">To configure single sign-on on **RolePoint** side, you need to send the downloaded **Metadata XML** to [RolePoint support team](mailto:info@rolepoint.com).</span></span>

> [!TIP]
> <span data-ttu-id="d7ac0-169">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d7ac0-170">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d7ac0-171">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d7ac0-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d7ac0-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7ac0-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="d7ac0-173">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d7ac0-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="d7ac0-175">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="d7ac0-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d7ac0-176">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d7ac0-178">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d7ac0-180">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d7ac0-182">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="d7ac0-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d7ac0-184">a.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-184">a.</span></span> <span data-ttu-id="d7ac0-185">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d7ac0-186">b.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-186">b.</span></span> <span data-ttu-id="d7ac0-187">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d7ac0-188">c.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-188">c.</span></span> <span data-ttu-id="d7ac0-189">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d7ac0-190">d.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-190">d.</span></span> <span data-ttu-id="d7ac0-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-191">Click **Create**.</span></span>
 
### <a name="creating-a-rolepoint-test-user"></a><span data-ttu-id="d7ac0-192">Creación de un usuario de prueba de RolePoint</span><span class="sxs-lookup"><span data-stu-id="d7ac0-192">Creating a RolePoint test user</span></span>

<span data-ttu-id="d7ac0-193">En esta sección, se crea un usuario denominado Britta Simon en RolePoint.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-193">In this section, you create a user called Britta Simon in RolePoint.</span></span> <span data-ttu-id="d7ac0-194">Trabaje con el [equipo de soporte técnico de RolePoint](mailto:info@rolepoint.com) para agregar los usuarios a la plataforma RolePoint.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-194">Work with [RolePoint support team](mailto:info@rolepoint.com) to add the users in the RolePoint platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d7ac0-195">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7ac0-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d7ac0-196">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a RolePoint.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RolePoint.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="d7ac0-198">**Para asignar Britta Simon a RolePoint, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d7ac0-198">**To assign Britta Simon to RolePoint, perform the following steps:**</span></span>

1. <span data-ttu-id="d7ac0-199">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="d7ac0-201">En la lista de aplicaciones, seleccione **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-201">In the applications list, select **RolePoint**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_app.png) 

3. <span data-ttu-id="d7ac0-203">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="d7ac0-205">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-205">Click **Add** button.</span></span> <span data-ttu-id="d7ac0-206">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="d7ac0-208">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d7ac0-209">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d7ac0-210">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d7ac0-211">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="d7ac0-211">Testing single sign-on</span></span>

<span data-ttu-id="d7ac0-212">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d7ac0-213">Al hacer clic en el icono de RolePoint en el panel de acceso, debería iniciar sesión automáticamente en su aplicación de RolePoint.</span><span class="sxs-lookup"><span data-stu-id="d7ac0-213">When you click the RolePoint tile in the Access Panel, you should get automatically signed-on to your RolePoint application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d7ac0-214">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d7ac0-214">Additional resources</span></span>

* [<span data-ttu-id="d7ac0-215">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7ac0-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d7ac0-216">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d7ac0-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_203.png

