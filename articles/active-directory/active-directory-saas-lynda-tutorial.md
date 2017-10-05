---
title: "Tutorial: Integración de Azure Active Directory con Lynda.com | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Lynda.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 84ed2adcc2d49ddbb6bd2e9cc3b93b967ebed063
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a><span data-ttu-id="476b6-103">Tutorial: Integración de Azure Active Directory con Lynda.com</span><span class="sxs-lookup"><span data-stu-id="476b6-103">Tutorial: Azure Active Directory integration with Lynda.com</span></span>

<span data-ttu-id="476b6-104">En este tutorial, obtendrá información sobre cómo integrar Lynda.com con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="476b6-104">In this tutorial, you learn how to integrate Lynda.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="476b6-105">La integración de Lynda.com con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="476b6-105">Integrating Lynda.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="476b6-106">Puede controlar en Azure AD quién tiene acceso a Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="476b6-106">You can control in Azure AD who has access to Lynda.com</span></span>
- <span data-ttu-id="476b6-107">Puede permitir que los usuarios inicien sesión automáticamente en Lynda.com (inicio de sesión único) con las cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="476b6-107">You can enable your users to automatically get signed-on to Lynda.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="476b6-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="476b6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="476b6-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="476b6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="476b6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="476b6-110">Prerequisites</span></span>

<span data-ttu-id="476b6-111">Para configurar la integración de Azure AD con Lynda.com, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="476b6-111">To configure Azure AD integration with Lynda.com, you need the following items:</span></span>

- <span data-ttu-id="476b6-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="476b6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="476b6-113">Una suscripción habilitada para el inicio de sesión único en Lynda.com</span><span class="sxs-lookup"><span data-stu-id="476b6-113">A Lynda.com single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="476b6-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="476b6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="476b6-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="476b6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="476b6-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="476b6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="476b6-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="476b6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="476b6-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="476b6-118">Scenario description</span></span>
<span data-ttu-id="476b6-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="476b6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="476b6-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="476b6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="476b6-121">Adición de Lynda.com desde la galería</span><span class="sxs-lookup"><span data-stu-id="476b6-121">Adding Lynda.com from the gallery</span></span>
2. <span data-ttu-id="476b6-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="476b6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lyndacom-from-the-gallery"></a><span data-ttu-id="476b6-123">Adición de Lynda.com desde la galería</span><span class="sxs-lookup"><span data-stu-id="476b6-123">Adding Lynda.com from the gallery</span></span>
<span data-ttu-id="476b6-124">Para configurar la integración de Lynda.com en Azure AD, debe agregar Lynda.com desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="476b6-124">To configure the integration of Lynda.com into Azure AD, you need to add Lynda.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="476b6-125">**Para agregar Lynda.com desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="476b6-125">**To add Lynda.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="476b6-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="476b6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="476b6-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="476b6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="476b6-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="476b6-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="476b6-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="476b6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="476b6-133">En el cuadro de búsqueda, escriba **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="476b6-133">In the search box, type **Lynda.com**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_search.png)

5. <span data-ttu-id="476b6-135">En el panel de resultados, seleccione **Lynda.com** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="476b6-135">In the results panel, select **Lynda.com**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="476b6-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="476b6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="476b6-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Lynda.com con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="476b6-138">In this section, you configure and test Azure AD single sign-on with Lynda.com based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="476b6-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Lynda.com para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="476b6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lynda.com is to a user in Azure AD.</span></span> <span data-ttu-id="476b6-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="476b6-140">In other words, a link relationship between an Azure AD user and the related user in Lynda.com needs to be established.</span></span>

<span data-ttu-id="476b6-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como valor de **nombre de usuario** en Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="476b6-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lynda.com.</span></span>

<span data-ttu-id="476b6-142">Para configurar y probar el inicio de sesión único de Azure AD con Lynda.com, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="476b6-142">To configure and test Azure AD single sign-on with Lynda.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="476b6-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="476b6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="476b6-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="476b6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="476b6-145">**[Creación de un usuario de prueba de Lynda.com](#creating-a-lyndacom-test-user)**: el objetivo es tener un homólogo de Britta Simon en Lynda.com que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="476b6-145">**[Creating a Lynda.com test user](#creating-a-lyndacom-test-user)** - to have a counterpart of Britta Simon in Lynda.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="476b6-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="476b6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="476b6-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="476b6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="476b6-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="476b6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="476b6-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="476b6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lynda.com application.</span></span>

<span data-ttu-id="476b6-150">**Para configurar el inicio de sesión único de Azure AD con Lynda.com, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="476b6-150">**To configure Azure AD single sign-on with Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="476b6-151">En la página de integración de la aplicación **Lynda.com** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="476b6-151">In the Azure portal, on the **Lynda.com** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="476b6-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="476b6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_samlbase.png)

3. <span data-ttu-id="476b6-155">En la sección **Dominio y direcciones URL de Lynda.com**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="476b6-155">On the **Lynda.com Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_url.png)

    <span data-ttu-id="476b6-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `.</span><span class="sxs-lookup"><span data-stu-id="476b6-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="476b6-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="476b6-158">This value is not real.</span></span> <span data-ttu-id="476b6-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="476b6-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="476b6-160">Póngase en contacto con el [equipo de atención al cliente de Lynda.com](https://www.linkedin.com/help/lynda/ask) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="476b6-160">Contact [Lynda.com Client support team](https://www.linkedin.com/help/lynda/ask) to get these values.</span></span> 
 
4. <span data-ttu-id="476b6-161">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="476b6-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_certificate.png) 

5. <span data-ttu-id="476b6-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="476b6-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lynda-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="476b6-165">Para configurar el inicio de sesión único en **Lynda.com**, necesita enviar el archivo **XML de metadatos** descargado al [soporte técnico de Lynda.com](https://www.linkedin.com/help/lynda/ask).</span><span class="sxs-lookup"><span data-stu-id="476b6-165">To configure single sign-on on **Lynda.com** side, you need to send the downloaded **Metadata XML** [Lynda.com support](https://www.linkedin.com/help/lynda/ask).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="476b6-166">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="476b6-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="476b6-167">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="476b6-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="476b6-169">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="476b6-169">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="476b6-170">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="476b6-170">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="476b6-172">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="476b6-172">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="476b6-174">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="476b6-174">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="476b6-176">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="476b6-176">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="476b6-178">a.</span><span class="sxs-lookup"><span data-stu-id="476b6-178">a.</span></span> <span data-ttu-id="476b6-179">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="476b6-179">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="476b6-180">b.</span><span class="sxs-lookup"><span data-stu-id="476b6-180">b.</span></span> <span data-ttu-id="476b6-181">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="476b6-181">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="476b6-182">c.</span><span class="sxs-lookup"><span data-stu-id="476b6-182">c.</span></span> <span data-ttu-id="476b6-183">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="476b6-183">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="476b6-184">d.</span><span class="sxs-lookup"><span data-stu-id="476b6-184">d.</span></span> <span data-ttu-id="476b6-185">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="476b6-185">Click **Create**.</span></span>
 
### <a name="creating-a-lyndacom-test-user"></a><span data-ttu-id="476b6-186">Creación de un usuario de prueba de Lynda.com</span><span class="sxs-lookup"><span data-stu-id="476b6-186">Creating a Lynda.com test user</span></span>

<span data-ttu-id="476b6-187">No hay ningún elemento de acción para que configure el aprovisionamiento de usuarios para Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="476b6-187">There is no action item for you to configure user provisioning to Lynda.com.</span></span>  
<span data-ttu-id="476b6-188">Cuando un usuario asignado intenta iniciar sesión en Lynda.com desde el Panel de acceso, Lynda.com comprueba si el usuario existe.</span><span class="sxs-lookup"><span data-stu-id="476b6-188">When an assigned user tries to log in to Lynda.com using the access panel, Lynda.com checks whether the user exists.</span></span>  

<span data-ttu-id="476b6-189">Si no hay cuentas de usuario disponibles, Lynda.com crea una automáticamente.</span><span class="sxs-lookup"><span data-stu-id="476b6-189">If there is no user account available yet, it is automatically created by Lynda.com.</span></span>

>[!NOTE]
><span data-ttu-id="476b6-190">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Lynda.com ofrecida por Lynda.com para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="476b6-190">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="476b6-191">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="476b6-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="476b6-192">En esta sección, permitirá que Britta Simon use el inicio de sesión único de Azure concediéndole acceso a Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="476b6-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lynda.com.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="476b6-194">**Para asignar a Britta Simon a Lynda.com, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="476b6-194">**To assign Britta Simon to Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="476b6-195">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="476b6-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="476b6-197">En la lista de aplicaciones, seleccione **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="476b6-197">In the applications list, select **Lynda.com**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_app.png) 

3. <span data-ttu-id="476b6-199">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="476b6-199">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="476b6-201">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="476b6-201">Click **Add** button.</span></span> <span data-ttu-id="476b6-202">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="476b6-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="476b6-204">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="476b6-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="476b6-205">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="476b6-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="476b6-206">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="476b6-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="476b6-207">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="476b6-207">Testing single sign-on</span></span>

<span data-ttu-id="476b6-208">Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="476b6-208">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="476b6-209">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="476b6-209">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="476b6-210">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="476b6-210">Additional resources</span></span>

* [<span data-ttu-id="476b6-211">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="476b6-211">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="476b6-212">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="476b6-212">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_203.png

