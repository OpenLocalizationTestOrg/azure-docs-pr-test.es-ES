---
title: "Tutorial: Integración de Azure Active Directory con Dow Jones Factiva | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Dow Jones Factiva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b36e97e8-37a6-4096-a894-530427ee1331
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: dab48c24ff25fd68df1ee540bb8f0929e7e81bcb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dow-jones-factiva"></a><span data-ttu-id="8e8cc-103">Tutorial: Integración de Azure Active Directory con Dow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="8e8cc-103">Tutorial: Azure Active Directory integration with Dow Jones Factiva</span></span>

<span data-ttu-id="8e8cc-104">En este tutorial, obtendrá información sobre cómo integrar Dow Jones Factiva con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8e8cc-104">In this tutorial, you learn how to integrate Dow Jones Factiva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8e8cc-105">Integrar Dow Jones Factiva con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="8e8cc-105">Integrating Dow Jones Factiva with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8e8cc-106">Puede controlar en Azure AD quién tiene acceso a Dow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="8e8cc-106">You can control in Azure AD who has access to Dow Jones Factiva</span></span>
- <span data-ttu-id="8e8cc-107">Puede permitir que los usuarios inicien sesión automáticamente en Dow Jones Factiva (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e8cc-107">You can enable your users to automatically get signed-on to Dow Jones Factiva (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8e8cc-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8e8cc-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8e8cc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e8cc-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8e8cc-110">Prerequisites</span></span>

<span data-ttu-id="8e8cc-111">Para configurar la integración de Azure AD con Dow Jones Factiva, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8e8cc-111">To configure Azure AD integration with Dow Jones Factiva, you need the following items:</span></span>

- <span data-ttu-id="8e8cc-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e8cc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8e8cc-113">Una suscripción habilitada para el inicio de sesión único en Dow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="8e8cc-113">A Dow Jones Factiva single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8e8cc-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8e8cc-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="8e8cc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8e8cc-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8e8cc-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8e8cc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8e8cc-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="8e8cc-118">Scenario description</span></span>
<span data-ttu-id="8e8cc-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8e8cc-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="8e8cc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8e8cc-121">Agregar Dow Jones Factiva desde la Galería</span><span class="sxs-lookup"><span data-stu-id="8e8cc-121">Adding Dow Jones Factiva from the gallery</span></span>
2. <span data-ttu-id="8e8cc-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e8cc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dow-jones-factiva-from-the-gallery"></a><span data-ttu-id="8e8cc-123">Agregar Dow Jones Factiva desde la Galería</span><span class="sxs-lookup"><span data-stu-id="8e8cc-123">Adding Dow Jones Factiva from the gallery</span></span>
<span data-ttu-id="8e8cc-124">Para configurar la integración de Dow Jones Factiva en Azure AD, deberá agregar Dow Jones Factiva desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-124">To configure the integration of Dow Jones Factiva into Azure AD, you need to add Dow Jones Factiva from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8e8cc-125">**Para agregar Dow Jones Factiva desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="8e8cc-125">**To add Dow Jones Factiva from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8e8cc-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8e8cc-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8e8cc-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="8e8cc-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="8e8cc-133">En el cuadro de búsqueda, escriba **Dow Jones Factiva**.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-133">In the search box, type **Dow Jones Factiva**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_search.png)

5. <span data-ttu-id="8e8cc-135">En el panel de resultados, seleccione **Dow Jones Factiva** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-135">In the results panel, select **Dow Jones Factiva**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8e8cc-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e8cc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8e8cc-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Dow Jones Factiva con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8e8cc-138">In this section, you configure and test Azure AD single sign-on with Dow Jones Factiva based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8e8cc-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Dow Jones Factiva para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Dow Jones Factiva is to a user in Azure AD.</span></span> <span data-ttu-id="8e8cc-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario correspondiente de Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-140">In other words, a link relationship between an Azure AD user and the related user in Dow Jones Factiva needs to be established.</span></span>

<span data-ttu-id="8e8cc-141">Para establecer la relación de vínculo, en Dow Jones Factiva, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-141">In Dow Jones Factiva, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8e8cc-142">Para configurar y probar el inicio de sesión único de Azure AD con Dow Jones Factiva, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="8e8cc-142">To configure and test Azure AD single sign-on with Dow Jones Factiva, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8e8cc-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8e8cc-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8e8cc-145">**[Creación de un usuario de prueba de Dow Jones Factiva](#creating-a-dow-jones-factiva-test-user)**: para tener un homólogo de Britta Simon en Dow Jones Factiva que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-145">**[Creating a Dow Jones Factiva test user](#creating-a-dow-jones-factiva-test-user)** - to have a counterpart of Britta Simon in Dow Jones Factiva that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8e8cc-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8e8cc-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8e8cc-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e8cc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8e8cc-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dow Jones Factiva application.</span></span>

<span data-ttu-id="8e8cc-150">**Para configurar el inicio de sesión único de Azure AD con Dow Jones Factiva, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="8e8cc-150">**To configure Azure AD single sign-on with Dow Jones Factiva, perform the following steps:**</span></span>

1. <span data-ttu-id="8e8cc-151">En Azure Portal, en la página de integración de aplicaciones de **Dow Jones Factiva**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-151">In the Azure portal, on the **Dow Jones Factiva** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="8e8cc-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_samlbase.png)

3. <span data-ttu-id="8e8cc-155">En la sección **Dominio y direcciones URL de Dow Jones Factiva**, el usuario no tiene que realizar ningún paso ya que la aplicación se ha integrado previamente con Azure.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-155">On the **Dow Jones Factiva Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_url.png)

4. <span data-ttu-id="8e8cc-157">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_certificate.png) 

5. <span data-ttu-id="8e8cc-159">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="8e8cc-159">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8e8cc-161">Para configurar el inicio de sesión único en **Dow Jones Factiva**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Dow Jones Factiva](https://www.dowjones.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="8e8cc-161">To configure single sign-on on **Dow Jones Factiva** side, you need to send the downloaded **Metadata XML** to [Dow Jones Factiva support team](https://www.dowjones.com/contact/).</span></span> <span data-ttu-id="8e8cc-162">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-162">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8e8cc-163">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-163">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8e8cc-164">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-164">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8e8cc-165">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8e8cc-165">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8e8cc-166">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e8cc-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="8e8cc-167">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8e8cc-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="8e8cc-169">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="8e8cc-169">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8e8cc-170">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-170">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8e8cc-172">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-172">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8e8cc-174">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-174">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8e8cc-176">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="8e8cc-176">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8e8cc-178">a.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-178">a.</span></span> <span data-ttu-id="8e8cc-179">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-179">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8e8cc-180">b.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-180">b.</span></span> <span data-ttu-id="8e8cc-181">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-181">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8e8cc-182">c.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-182">c.</span></span> <span data-ttu-id="8e8cc-183">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-183">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8e8cc-184">d.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-184">d.</span></span> <span data-ttu-id="8e8cc-185">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-185">Click **Create**.</span></span>
 
### <a name="creating-a-dow-jones-factiva-test-user"></a><span data-ttu-id="8e8cc-186">Creación de un usuario de prueba de Dow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="8e8cc-186">Creating a Dow Jones Factiva test user</span></span>

<span data-ttu-id="8e8cc-187">En esta sección, creará un usuario llamado Britta Simon en Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-187">In this section, you create a user called Britta Simon in Dow Jones Factiva.</span></span> <span data-ttu-id="8e8cc-188">Trabaje con el [equipo de soporte técnico de Dow Jones Factiva](https://www.dowjones.com/contact/) para agregar los usuarios en la plataforma Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-188">Please work with Dow [Jones Factiva support team](https://www.dowjones.com/contact/) to add the users in the Dow Jones Factiva platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8e8cc-189">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e8cc-189">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8e8cc-190">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-190">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dow Jones Factiva.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="8e8cc-192">**Para asignar a Britta Simon a Dow Jones Factiva, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="8e8cc-192">**To assign Britta Simon to Dow Jones Factiva, perform the following steps:**</span></span>

1. <span data-ttu-id="8e8cc-193">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-193">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="8e8cc-195">En la lista de aplicaciones, seleccione **Dow Jones Factiva**.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-195">In the applications list, select **Dow Jones Factiva**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_app.png) 

3. <span data-ttu-id="8e8cc-197">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-197">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="8e8cc-199">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-199">Click **Add** button.</span></span> <span data-ttu-id="8e8cc-200">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-200">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="8e8cc-202">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-202">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8e8cc-203">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-203">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8e8cc-204">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-204">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8e8cc-205">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="8e8cc-205">Testing single sign-on</span></span>

<span data-ttu-id="8e8cc-206">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-206">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8e8cc-207">Al hacer clic en el icono de Dow Jones Factiva en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="8e8cc-207">When you click the Dow Jones Factiva tile in the Access Panel, you should get automatically signed-on to your Dow Jones Factiva application.</span></span>
<span data-ttu-id="8e8cc-208">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8e8cc-208">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8e8cc-209">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8e8cc-209">Additional resources</span></span>

* [<span data-ttu-id="8e8cc-210">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e8cc-210">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8e8cc-211">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8e8cc-211">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_203.png

