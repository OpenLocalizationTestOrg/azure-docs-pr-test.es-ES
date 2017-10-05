---
title: "Tutorial: Integración de Azure Active Directory con Asset Bank | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Asset Bank."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3006ad6e-8831-41cd-94aa-7e7ae770ce7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 17bc0082e3721b50269cb4b17884c0e4a4cbcb5d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asset-bank"></a><span data-ttu-id="21253-103">Tutorial: Integración de Azure Active Directory con Asset Bank</span><span class="sxs-lookup"><span data-stu-id="21253-103">Tutorial: Azure Active Directory integration with Asset Bank</span></span>

<span data-ttu-id="21253-104">En este tutorial, obtendrá información sobre cómo integrar Asset Bank con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="21253-104">In this tutorial, you learn how to integrate Asset Bank with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="21253-105">La integración de Asset Bank con Azure AD ofrece las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="21253-105">Integrating Asset Bank with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="21253-106">Puede controlar en Azure AD quién tiene acceso a Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="21253-106">You can control in Azure AD who has access to Asset Bank</span></span>
- <span data-ttu-id="21253-107">Puede permitir que los usuarios inicien sesión automáticamente en Asset Bank (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="21253-107">You can enable your users to automatically get signed-on to Asset Bank (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="21253-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="21253-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="21253-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="21253-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21253-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="21253-110">Prerequisites</span></span>

<span data-ttu-id="21253-111">Para configurar la integración de Azure AD con Asset Bank, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="21253-111">To configure Azure AD integration with Asset Bank, you need the following items:</span></span>

- <span data-ttu-id="21253-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="21253-112">An Azure AD subscription</span></span>
- <span data-ttu-id="21253-113">Una suscripción habilitada para el inicio de sesión único en Asset Bank</span><span class="sxs-lookup"><span data-stu-id="21253-113">An Asset Bank single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="21253-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="21253-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="21253-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="21253-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="21253-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="21253-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="21253-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="21253-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="21253-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="21253-118">Scenario description</span></span>
<span data-ttu-id="21253-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="21253-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="21253-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="21253-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="21253-121">Adición de Asset Bank desde la galería</span><span class="sxs-lookup"><span data-stu-id="21253-121">Adding Asset Bank from the gallery</span></span>
2. <span data-ttu-id="21253-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="21253-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asset-bank-from-the-gallery"></a><span data-ttu-id="21253-123">Adición de Asset Bank desde la galería</span><span class="sxs-lookup"><span data-stu-id="21253-123">Adding Asset Bank from the gallery</span></span>
<span data-ttu-id="21253-124">Para configurar la integración de Asset Bank en Azure AD, será preciso que agregue Asset Bank desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="21253-124">To configure the integration of Asset Bank into Azure AD, you need to add Asset Bank from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="21253-125">**Para agregar Asset Bank desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="21253-125">**To add Asset Bank from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="21253-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="21253-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="21253-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="21253-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="21253-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="21253-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="21253-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="21253-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="21253-133">En el cuadro de búsqueda, escriba **Asset Bank**.</span><span class="sxs-lookup"><span data-stu-id="21253-133">In the search box, type **Asset Bank**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_search.png)

5. <span data-ttu-id="21253-135">En el panel de resultados, seleccione **Asset Bank** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="21253-135">In the results panel, select **Asset Bank**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="21253-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="21253-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="21253-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Asset Bank con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="21253-138">In this section, you configure and test Azure AD single sign-on with Asset Bank based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="21253-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Asset Bank para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="21253-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Asset Bank is to a user in Azure AD.</span></span> <span data-ttu-id="21253-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="21253-140">In other words, a link relationship between an Azure AD user and the related user in Asset Bank needs to be established.</span></span>

<span data-ttu-id="21253-141">Para establecer la relación de vínculo, en Asset Bank, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="21253-141">In Asset Bank, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="21253-142">Para configurar y probar el inicio de sesión único de Azure AD con Asset Bank, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="21253-142">To configure and test Azure AD single sign-on with Asset Bank, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="21253-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="21253-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="21253-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="21253-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="21253-145">**[Creación de un usuario de prueba de Asset Bank](#creating-an-asset-bank-test-user)**: para tener un homólogo de Britta Simon en Asset Bank que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="21253-145">**[Creating an Asset Bank test user](#creating-an-asset-bank-test-user)** - to have a counterpart of Britta Simon in Asset Bank that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="21253-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="21253-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="21253-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="21253-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="21253-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="21253-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="21253-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="21253-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Asset Bank application.</span></span>

<span data-ttu-id="21253-150">**Para configurar el inicio de sesión único de Azure AD con Asset Bank, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="21253-150">**To configure Azure AD single sign-on with Asset Bank, perform the following steps:**</span></span>

1. <span data-ttu-id="21253-151">En Azure Portal, en la página de integración de la aplicación **Asset Bank**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="21253-151">In the Azure portal, on the **Asset Bank** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="21253-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="21253-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_samlbase.png)

3. <span data-ttu-id="21253-155">En la sección **Dominio y direcciones URL de Asset Bank**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="21253-155">On the **Asset Bank Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_url.png)

    <span data-ttu-id="21253-157">a.</span><span class="sxs-lookup"><span data-stu-id="21253-157">a.</span></span> <span data-ttu-id="21253-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.assetbank-server.com`.</span><span class="sxs-lookup"><span data-stu-id="21253-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.assetbank-server.com`</span></span>

    <span data-ttu-id="21253-159">b.</span><span class="sxs-lookup"><span data-stu-id="21253-159">b.</span></span> <span data-ttu-id="21253-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.assetbank-server.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="21253-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.assetbank-server.com/shibboleth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="21253-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="21253-161">These values are not real.</span></span> <span data-ttu-id="21253-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="21253-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="21253-163">Póngase en contacto con el [equipo de soporte de cliente de Asset Bank](mailto:support@assetbank.co.uk) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="21253-163">Contact [Asset Bank Client support team](mailto:support@assetbank.co.uk) to get these values.</span></span> 
 
4. <span data-ttu-id="21253-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="21253-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_certificate.png) 

5. <span data-ttu-id="21253-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="21253-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-assetbank-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="21253-168">Para configurar el inicio de sesión único en **Asset Bank**, es preciso enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Asset Bank](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="21253-168">To configure single sign-on on **Asset Bank** side, you need to send the downloaded **Metadata XML** to [Asset Bank support team](mailto:support@assetbank.co.uk).</span></span> 


> [!TIP]
> <span data-ttu-id="21253-169">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="21253-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="21253-170">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="21253-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="21253-171">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="21253-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="21253-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="21253-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="21253-173">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="21253-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="21253-175">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="21253-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="21253-176">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="21253-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="21253-178">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="21253-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="21253-180">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="21253-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="21253-182">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="21253-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="21253-184">a.</span><span class="sxs-lookup"><span data-stu-id="21253-184">a.</span></span> <span data-ttu-id="21253-185">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="21253-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="21253-186">b.</span><span class="sxs-lookup"><span data-stu-id="21253-186">b.</span></span> <span data-ttu-id="21253-187">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="21253-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="21253-188">c.</span><span class="sxs-lookup"><span data-stu-id="21253-188">c.</span></span> <span data-ttu-id="21253-189">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="21253-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="21253-190">d.</span><span class="sxs-lookup"><span data-stu-id="21253-190">d.</span></span> <span data-ttu-id="21253-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="21253-191">Click **Create**.</span></span>
 
### <a name="creating-an-asset-bank-test-user"></a><span data-ttu-id="21253-192">Creación de un usuario de prueba de Asset Bank</span><span class="sxs-lookup"><span data-stu-id="21253-192">Creating an Asset Bank test user</span></span>

<span data-ttu-id="21253-193">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="21253-193">The objective of this section is to create a user called Britta Simon in Asset Bank.</span></span> <span data-ttu-id="21253-194">Asset Bank admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="21253-194">Asset Bank supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="21253-195">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="21253-195">There is no action item for you in this section.</span></span> <span data-ttu-id="21253-196">Durante un intento de acceder a Asset Bank se crea un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="21253-196">A new user is created during an attempt to access Asset Bank if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="21253-197">Si necesita crear manualmente un usuario, es preciso que se ponga contacto con el [equipo de soporte técnico de Asset Bank](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="21253-197">If you need to create a user manually, you need to contact the [Asset Bank support team](mailto:support@assetbank.co.uk).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="21253-198">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="21253-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="21253-199">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="21253-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Asset Bank.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="21253-201">**Para asignar a Britta Simon a Asset Bank, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="21253-201">**To assign Britta Simon to Asset Bank, perform the following steps:**</span></span>

1. <span data-ttu-id="21253-202">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="21253-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="21253-204">En la lista de aplicaciones, seleccione **Asset Bank**.</span><span class="sxs-lookup"><span data-stu-id="21253-204">In the applications list, select **Asset Bank**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_app.png) 

3. <span data-ttu-id="21253-206">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="21253-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="21253-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="21253-208">Click **Add** button.</span></span> <span data-ttu-id="21253-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="21253-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="21253-211">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="21253-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="21253-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="21253-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="21253-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="21253-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="21253-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="21253-214">Testing single sign-on</span></span>

<span data-ttu-id="21253-215">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="21253-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="21253-216">Al hacer clic en el icono de Asset Bank en el panel de acceso, debería iniciar sesión automáticamente en la aplicación Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="21253-216">When you click the Asset Bank tile in the Access Panel, you should get automatically signed-on to your Asset Bank application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="21253-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="21253-217">Additional resources</span></span>

* [<span data-ttu-id="21253-218">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="21253-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="21253-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="21253-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_203.png
