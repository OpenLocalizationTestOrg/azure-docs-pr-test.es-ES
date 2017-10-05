---
title: "Tutorial: Integración de Azure Active Directory con Inkling | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory e Inkling."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 64c7ee45-ee8a-42f7-bf04-fd0e00833ea9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 7b0639c6515298731f88346c2e4ca82664653a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-inkling"></a><span data-ttu-id="ae571-103">Tutorial: Integración de Azure Active Directory con Inkling</span><span class="sxs-lookup"><span data-stu-id="ae571-103">Tutorial: Azure Active Directory integration with Inkling</span></span>

<span data-ttu-id="ae571-104">En este tutorial, obtendrá información sobre cómo integrar Inkling con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae571-104">In this tutorial, you learn how to integrate Inkling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae571-105">La integración de Inkling con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ae571-105">Integrating Inkling with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ae571-106">Puede controlar en Azure AD quién tiene acceso a Inkling.</span><span class="sxs-lookup"><span data-stu-id="ae571-106">You can control in Azure AD who has access to Inkling</span></span>
- <span data-ttu-id="ae571-107">Puede permitir que los usuarios inicien sesión automáticamente en Inkling (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae571-107">You can enable your users to automatically get signed-on to Inkling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae571-108">Puede administrar sus cuentas en una ubicación central: el Portal de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="ae571-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="ae571-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ae571-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae571-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ae571-110">Prerequisites</span></span>

<span data-ttu-id="ae571-111">Para configurar la integración de Azure AD con Inkling, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ae571-111">To configure Azure AD integration with Inkling, you need the following items:</span></span>

- <span data-ttu-id="ae571-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae571-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae571-113">Una suscripción habilitada para inicio de sesión único en Inkling</span><span class="sxs-lookup"><span data-stu-id="ae571-113">An Inkling single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="ae571-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ae571-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="ae571-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ae571-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae571-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ae571-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ae571-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae571-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="ae571-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="ae571-118">Scenario description</span></span>
<span data-ttu-id="ae571-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="ae571-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae571-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="ae571-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae571-121">Incorporación de Inkling desde la galería</span><span class="sxs-lookup"><span data-stu-id="ae571-121">Adding Inkling from the gallery</span></span>
2. <span data-ttu-id="ae571-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae571-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-inkling-from-the-gallery"></a><span data-ttu-id="ae571-123">Incorporación de Inkling desde la galería</span><span class="sxs-lookup"><span data-stu-id="ae571-123">Adding Inkling from the gallery</span></span>
<span data-ttu-id="ae571-124">Para configurar la integración de Inkling en Azure AD, será preciso agregar Inkling desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="ae571-124">To configure the integration of Inkling into Azure AD, you need to add Inkling from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ae571-125">**Para agregar Inkling desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="ae571-125">**To add Inkling from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ae571-126">En el panel de navegación izquierdo del **[Portal de administración de Azure](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae571-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ae571-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="ae571-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ae571-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ae571-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="ae571-131">Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ae571-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="ae571-133">En el cuadro de búsqueda, escriba **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="ae571-133">In the search box, type **Inkling**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_001.png)

5. <span data-ttu-id="ae571-135">En el panel de resultados, seleccione **Inkling** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ae571-135">In the results panel, select **Inkling**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ae571-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae571-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ae571-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Inkling con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ae571-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ae571-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Inkling para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae571-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Inkling is to a user in Azure AD.</span></span> <span data-ttu-id="ae571-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Inkling.</span><span class="sxs-lookup"><span data-stu-id="ae571-140">In other words, a link relationship between an Azure AD user and the related user in Inkling needs to be established.</span></span>

<span data-ttu-id="ae571-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Inkling.</span><span class="sxs-lookup"><span data-stu-id="ae571-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Inkling.</span></span>

<span data-ttu-id="ae571-142">Para configurar y probar el inicio de sesión único de Azure AD con Inkling, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ae571-142">To configure and test Azure AD single sign-on with Inkling, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ae571-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="ae571-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ae571-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae571-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ae571-145">**[Creación de un usuario de prueba de Inkling](#creating-an-inkling-test-user)**: para tener un homólogo de Britta Simon en Inkling que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae571-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - to have a counterpart of Britta Simon in Inkling that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="ae571-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae571-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ae571-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="ae571-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ae571-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae571-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ae571-149">En esta sección, habilitará el inicio de sesión único de Azure AD en el Portal de administración de Azure y configurará el inicio de sesión único en la aplicación Inkling.</span><span class="sxs-lookup"><span data-stu-id="ae571-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Inkling application.</span></span>

<span data-ttu-id="ae571-150">**Para configurar el inicio de sesión único de Azure AD con Inkling, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="ae571-150">**To configure Azure AD single sign-on with Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="ae571-151">En el Portal de administración de Azure, en la página de integración de la aplicación **Inkling**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ae571-151">In the Azure Management portal, on the **Inkling** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="ae571-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ae571-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-inkling-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="ae571-155">En la sección **Dominio y direcciones URL de Inkling**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ae571-155">On the **Inkling Domain and URLs** section, perform the following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_01.png)

    <span data-ttu-id="ae571-157">a.</span><span class="sxs-lookup"><span data-stu-id="ae571-157">a.</span></span> <span data-ttu-id="ae571-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="ae571-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span></span>

    <span data-ttu-id="ae571-159">b.</span><span class="sxs-lookup"><span data-stu-id="ae571-159">b.</span></span> <span data-ttu-id="ae571-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://api.inkling.com/saml/v2/acs/<user-id>`.</span><span class="sxs-lookup"><span data-stu-id="ae571-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ae571-161">Tenga en cuenta que estos no son valores reales.</span><span class="sxs-lookup"><span data-stu-id="ae571-161">Please note that these are not the real values.</span></span> <span data-ttu-id="ae571-162">Estos valores se tienen que actualizar con los valores reales de Identificador y URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="ae571-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="ae571-163">Póngase en contacto con el [equipo de soporte técnico de Inkling](mailto:press@inkling.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="ae571-163">Contact [Inkling support team](mailto:press@inkling.com) to get these values.</span></span>

4. <span data-ttu-id="ae571-164">En la sección **Certificado de firma de SAML**, haga clic en **Crear nuevo certificado**.</span><span class="sxs-lookup"><span data-stu-id="ae571-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-inkling-tutorial/tutorial_general_400.png)    

5. <span data-ttu-id="ae571-166">En el cuadro de diálogo **Crear nuevo certificado**, haga clic en el icono del calendario y seleccione una valor en **Fecha de expiración**.</span><span class="sxs-lookup"><span data-stu-id="ae571-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="ae571-167">Luego haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ae571-167">Then click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-inkling-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="ae571-169">En la sección **Certificado de firma de SAML**, seleccione **Make new certificate active** (Activar el nuevo certificado) y haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ae571-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_02.png)

7. <span data-ttu-id="ae571-171">En la ventana emergente **Rollover certificate** (Certificado de sustitución), haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ae571-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-inkling-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="ae571-173">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ae571-173">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_03.png) 

9. <span data-ttu-id="ae571-175">Para configurar SSO para su aplicación, póngase en contacto con el [equipo de soporte técnico de Inkling](mailto:press@inkling.com) y proporcione los **metadatos** descargados.</span><span class="sxs-lookup"><span data-stu-id="ae571-175">To get SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ae571-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae571-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="ae571-177">El objetivo de esta sección es crear un usuario de prueba en el Portal de administración de Azure llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae571-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="ae571-179">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="ae571-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ae571-180">En el panel de navegación izquierdo del **Portal de administración de Azure**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae571-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ae571-182">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="ae571-182">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ae571-184">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="ae571-184">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ae571-186">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="ae571-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae571-188">a.</span><span class="sxs-lookup"><span data-stu-id="ae571-188">a.</span></span> <span data-ttu-id="ae571-189">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae571-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae571-190">b.</span><span class="sxs-lookup"><span data-stu-id="ae571-190">b.</span></span> <span data-ttu-id="ae571-191">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae571-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae571-192">c.</span><span class="sxs-lookup"><span data-stu-id="ae571-192">c.</span></span> <span data-ttu-id="ae571-193">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ae571-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ae571-194">d.</span><span class="sxs-lookup"><span data-stu-id="ae571-194">d.</span></span> <span data-ttu-id="ae571-195">Haga clic en **Create**(Crear).</span><span class="sxs-lookup"><span data-stu-id="ae571-195">Click **Create**.</span></span> 



### <a name="creating-an-inkling-test-user"></a><span data-ttu-id="ae571-196">Creación de un usuario de prueba de Inkling</span><span class="sxs-lookup"><span data-stu-id="ae571-196">Creating an Inkling test user</span></span>

<span data-ttu-id="ae571-197">En esta sección, creará un usuario llamado Britta Simon en Inkling.</span><span class="sxs-lookup"><span data-stu-id="ae571-197">In this section, you create a user called Britta Simon in Inkling.</span></span> <span data-ttu-id="ae571-198">Trabaje con el equipo de [soporte técnico de Inkling](mailto:press@inkling.com) para agregar los usuarios a la plataforma de Inkling.</span><span class="sxs-lookup"><span data-stu-id="ae571-198">Please work with [Inkling support team](mailto:press@inkling.com) to add the users in the Inkling platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ae571-199">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae571-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ae571-200">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Inkling.</span><span class="sxs-lookup"><span data-stu-id="ae571-200">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Inkling.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="ae571-202">**Para asignar a Britta Simon a Inkling, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="ae571-202">**To assign Britta Simon to Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="ae571-203">En el Portal de administración de Azure, abra la vista de aplicaciones, vaya a la vista de directorio y seleccione **Aplicaciones empresariales**. Después, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ae571-203">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="ae571-205">En la lista de aplicaciones, seleccione **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="ae571-205">In the applications list, select **Inkling**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_50.png) 

3. <span data-ttu-id="ae571-207">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ae571-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="ae571-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ae571-209">Click **Add** button.</span></span> <span data-ttu-id="ae571-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ae571-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="ae571-212">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="ae571-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ae571-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ae571-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ae571-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ae571-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="ae571-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="ae571-215">Testing single sign-on</span></span>

<span data-ttu-id="ae571-216">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ae571-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ae571-217">Al hacer clic en el icono de Inkling en el panel de acceso, debería iniciar sesión automáticamente en su aplicación de Inkling.</span><span class="sxs-lookup"><span data-stu-id="ae571-217">When you click the Inkling tile in the Access Panel, you should get automatically signed-on to your Inkling application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ae571-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ae571-218">Additional resources</span></span>

* [<span data-ttu-id="ae571-219">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae571-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae571-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ae571-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_203.png