---
title: "Tutorial: Integración de Azure Active Directory con 360 Online | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y 360 Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cda8eba6-843f-4a09-8c55-0aaf6e593d75
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 629c7db04b0f9c880da6dfa8eac7fe14ecd8a215
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-360-online"></a><span data-ttu-id="d69db-103">Tutorial: Integración de Azure Active Directory con 360 Online</span><span class="sxs-lookup"><span data-stu-id="d69db-103">Tutorial: Azure Active Directory integration with 360 Online</span></span>

<span data-ttu-id="d69db-104">En este tutorial, aprenderá a integrar 360 Online con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d69db-104">In this tutorial, you learn how to integrate 360 Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d69db-105">Integrar 360 Online con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d69db-105">Integrating 360 Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d69db-106">Puede controlar en Azure AD quién tiene acceso a 360 Online</span><span class="sxs-lookup"><span data-stu-id="d69db-106">You can control in Azure AD who has access to 360 Online</span></span>
- <span data-ttu-id="d69db-107">Puede permitir que los usuarios inicien sesión automáticamente en 360 Online (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d69db-107">You can enable your users to automatically get signed-on to 360 Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d69db-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d69db-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d69db-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d69db-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d69db-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d69db-110">Prerequisites</span></span>

<span data-ttu-id="d69db-111">Para configurar la integración de Azure AD con 360 Online, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d69db-111">To configure Azure AD integration with 360 Online, you need the following items:</span></span>

- <span data-ttu-id="d69db-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d69db-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d69db-113">Una suscripción habilitada para el inicio de sesión único en 360 Online</span><span class="sxs-lookup"><span data-stu-id="d69db-113">A 360 Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d69db-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="d69db-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d69db-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="d69db-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d69db-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d69db-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d69db-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d69db-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d69db-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="d69db-118">Scenario description</span></span>
<span data-ttu-id="d69db-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="d69db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d69db-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="d69db-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d69db-121">Adición de 360 Online desde la Galería</span><span class="sxs-lookup"><span data-stu-id="d69db-121">Adding 360 Online from the gallery</span></span>
2. <span data-ttu-id="d69db-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d69db-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-360-online-from-the-gallery"></a><span data-ttu-id="d69db-123">Adición de 360 Online desde la Galería</span><span class="sxs-lookup"><span data-stu-id="d69db-123">Adding 360 Online from the gallery</span></span>
<span data-ttu-id="d69db-124">Para configurar la integración de 360 Online en Azure AD, deberá agregar 360 Online desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="d69db-124">To configure the integration of 360 Online into Azure AD, you need to add 360 Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d69db-125">**Para agregar 360 Online desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d69db-125">**To add 360 Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d69db-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d69db-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d69db-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="d69db-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d69db-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d69db-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="d69db-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d69db-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="d69db-133">En el cuadro Buscar, escriba **360 Online**.</span><span class="sxs-lookup"><span data-stu-id="d69db-133">In the search box, type **360 Online**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-360online-tutorial/tutorial_360online_search.png)

5. <span data-ttu-id="d69db-135">En el panel de resultados, seleccione **360 Online** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d69db-135">In the results panel, select **360 Online**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-360online-tutorial/tutorial_360online_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d69db-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d69db-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d69db-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con 360 Online mediante un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d69db-138">In this section, you configure and test Azure AD single sign-on with 360 Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d69db-139">Para que el inicio de sesión único funcione, Azure AD tiene que saber cuál es el usuario homólogo de 360 Online para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d69db-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 360 Online is to a user in Azure AD.</span></span> <span data-ttu-id="d69db-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de 360 Online.</span><span class="sxs-lookup"><span data-stu-id="d69db-140">In other words, a link relationship between an Azure AD user and the related user in 360 Online needs to be established.</span></span>

<span data-ttu-id="d69db-141">Para establecer la relación de vínculo, en 360 Online, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="d69db-141">In 360 Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d69db-142">Para configurar y probar el inicio de sesión único de Azure AD con 360 Online, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d69db-142">To configure and test Azure AD single sign-on with 360 Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d69db-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="d69db-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d69db-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d69db-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d69db-145">**[Creación de un usuario de prueba de 360 Online](#creating-a-360-online-test-user)**: para tener un homólogo de Britta Simon en 360 Online que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d69db-145">**[Creating a 360 Online test user](#creating-a-360-online-test-user)** - to have a counterpart of Britta Simon in 360 Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d69db-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d69db-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d69db-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="d69db-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d69db-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d69db-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d69db-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación 360 Online.</span><span class="sxs-lookup"><span data-stu-id="d69db-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 360 Online application.</span></span>

<span data-ttu-id="d69db-150">**Para configurar el inicio de sesión único de Azure AD con 360 Online, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d69db-150">**To configure Azure AD single sign-on with 360 Online, perform the following steps:**</span></span>

1. <span data-ttu-id="d69db-151">En Azure Portal, en la página de integración de la aplicación **360 Online**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d69db-151">In the Azure portal, on the **360 Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="d69db-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d69db-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-360online-tutorial/tutorial_360online_samlbase.png)

3. <span data-ttu-id="d69db-155">En la sección **Dominio y direcciones URL de 360 Online**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d69db-155">On the **360 Online Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-360online-tutorial/tutorial_360online_url.png)

    <span data-ttu-id="d69db-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<company name>.public360online.com`.</span><span class="sxs-lookup"><span data-stu-id="d69db-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.public360online.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d69db-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="d69db-158">The value is not real.</span></span> <span data-ttu-id="d69db-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="d69db-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="d69db-160">Póngase en contacto con el [equipo de soporte técnico de 360 Online](mailto:360online@software-innovation.com) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="d69db-160">Contact [360 Online Client support team](mailto:360online@software-innovation.com) to get the value.</span></span> 
 
4. <span data-ttu-id="d69db-161">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d69db-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-360online-tutorial/tutorial_360online_certificate.png) 

5. <span data-ttu-id="d69db-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="d69db-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-360online-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d69db-165">Para configurar el inicio de sesión único en el lado de **360 Online**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de 360 Online](mailto:360online@software-innovation.com).</span><span class="sxs-lookup"><span data-stu-id="d69db-165">To configure single sign-on on **360 Online** side, you need to send the downloaded **Metadata XML** to [360 Online support team](mailto:360online@software-innovation.com).</span></span> 

> [!TIP]
> <span data-ttu-id="d69db-166">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d69db-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d69db-167">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="d69db-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d69db-168">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d69db-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d69db-169">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d69db-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="d69db-170">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d69db-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="d69db-172">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="d69db-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d69db-173">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d69db-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-360online-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d69db-175">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d69db-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-360online-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d69db-177">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d69db-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-360online-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d69db-179">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="d69db-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-360online-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d69db-181">a.</span><span class="sxs-lookup"><span data-stu-id="d69db-181">a.</span></span> <span data-ttu-id="d69db-182">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d69db-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d69db-183">b.</span><span class="sxs-lookup"><span data-stu-id="d69db-183">b.</span></span> <span data-ttu-id="d69db-184">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d69db-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d69db-185">c.</span><span class="sxs-lookup"><span data-stu-id="d69db-185">c.</span></span> <span data-ttu-id="d69db-186">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="d69db-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d69db-187">d.</span><span class="sxs-lookup"><span data-stu-id="d69db-187">d.</span></span> <span data-ttu-id="d69db-188">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d69db-188">Click **Create**.</span></span>
 
### <a name="creating-a-360-online-test-user"></a><span data-ttu-id="d69db-189">Creación de un usuario de prueba de 360 Online</span><span class="sxs-lookup"><span data-stu-id="d69db-189">Creating a 360 Online test user</span></span>

<span data-ttu-id="d69db-190">En esta sección, creará un usuario llamado Britta Simon en 360 Online.</span><span class="sxs-lookup"><span data-stu-id="d69db-190">In this section, you create a user called Britta Simon in 360 Online.</span></span> <span data-ttu-id="d69db-191">Tiene que ponerse en contacto con [equipo de soporte técnico de 360 Online](mailto:360online@software-innovation.com).</span><span class="sxs-lookup"><span data-stu-id="d69db-191">you need to contact [360 Online support team](mailto:360online@software-innovation.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d69db-192">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d69db-192">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d69db-193">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a 360 Online.</span><span class="sxs-lookup"><span data-stu-id="d69db-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 360 Online.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="d69db-195">**Para asignar a Britta Simon a 360 Online, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="d69db-195">**To assign Britta Simon to 360 Online, perform the following steps:**</span></span>

1. <span data-ttu-id="d69db-196">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d69db-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="d69db-198">En la lista de aplicaciones. seleccione **360 Online**.</span><span class="sxs-lookup"><span data-stu-id="d69db-198">In the applications list, select **360 Online**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-360online-tutorial/tutorial_360online_app.png) 

3. <span data-ttu-id="d69db-200">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d69db-200">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="d69db-202">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d69db-202">Click **Add** button.</span></span> <span data-ttu-id="d69db-203">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d69db-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="d69db-205">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="d69db-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d69db-206">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d69db-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d69db-207">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d69db-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d69db-208">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="d69db-208">Testing single sign-on</span></span>

<span data-ttu-id="d69db-209">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d69db-209">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d69db-210">Al hacer clic en el icono de 360 Online en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación 360 Online.</span><span class="sxs-lookup"><span data-stu-id="d69db-210">When you click the 360 Online tile in the Access Panel, you should get automatically signed-on to your 360 Online application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d69db-211">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d69db-211">Additional resources</span></span>

* [<span data-ttu-id="d69db-212">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d69db-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d69db-213">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d69db-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-360online-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-360online-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-360online-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-360online-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-360online-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-360online-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-360online-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-360online-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-360online-tutorial/tutorial_general_203.png
