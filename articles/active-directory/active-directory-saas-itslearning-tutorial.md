---
title: "Tutorial: Integración de Azure Active Directory con itslearning | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory e itslearning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 60587ba3-1396-4b8a-9ac1-e22a98e5e0ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 32c8a8dff533f726784fb52b9496c2cb50ecfde7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itslearning"></a><span data-ttu-id="e7144-103">Tutorial: Integración de Azure Active Directory con itslearning</span><span class="sxs-lookup"><span data-stu-id="e7144-103">Tutorial: Azure Active Directory integration with itslearning</span></span>

<span data-ttu-id="e7144-104">En este tutorial, obtendrá información sobre cómo integrar itslearning con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e7144-104">In this tutorial, you learn how to integrate itslearning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e7144-105">La integración de itslearning con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e7144-105">Integrating itslearning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e7144-106">Puede controlar en Azure AD quién tiene acceso a itslearning.</span><span class="sxs-lookup"><span data-stu-id="e7144-106">You can control in Azure AD who has access to itslearning</span></span>
- <span data-ttu-id="e7144-107">Puede permitir que los usuarios inicien sesión automáticamente en itslearning (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7144-107">You can enable your users to automatically get signed-on to itslearning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e7144-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e7144-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e7144-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e7144-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7144-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e7144-110">Prerequisites</span></span>

<span data-ttu-id="e7144-111">Para configurar la integración de Azure AD con itslearning, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e7144-111">To configure Azure AD integration with itslearning, you need the following items:</span></span>

- <span data-ttu-id="e7144-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7144-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e7144-113">Una suscripción habilitada para el inicio de sesión único en itslearning</span><span class="sxs-lookup"><span data-stu-id="e7144-113">An itslearning single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e7144-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e7144-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e7144-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e7144-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e7144-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e7144-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e7144-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7144-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e7144-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e7144-118">Scenario description</span></span>
<span data-ttu-id="e7144-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e7144-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e7144-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="e7144-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e7144-121">Adición de itslearning desde la galería</span><span class="sxs-lookup"><span data-stu-id="e7144-121">Adding itslearning from the gallery</span></span>
2. <span data-ttu-id="e7144-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7144-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itslearning-from-the-gallery"></a><span data-ttu-id="e7144-123">Adición de itslearning desde la galería</span><span class="sxs-lookup"><span data-stu-id="e7144-123">Adding itslearning from the gallery</span></span>
<span data-ttu-id="e7144-124">Para configurar la integración de itslearning en Azure AD, deberá agregar itslearning desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="e7144-124">To configure the integration of itslearning into Azure AD, you need to add itslearning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e7144-125">**Para agregar itslearning desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e7144-125">**To add itslearning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e7144-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e7144-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e7144-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e7144-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e7144-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e7144-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e7144-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e7144-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e7144-133">En el cuadro de búsqueda, escriba **itslearning**.</span><span class="sxs-lookup"><span data-stu-id="e7144-133">In the search box, type **itslearning**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_search.png)

5. <span data-ttu-id="e7144-135">En el panel de resultados, seleccione **itslearning** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e7144-135">In the results panel, select **itslearning**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e7144-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7144-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e7144-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con itslearning utilizando un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e7144-138">In this section, you configure and test Azure AD single sign-on with itslearning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e7144-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de itslearning para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7144-139">For single sign-on to work, Azure AD needs to know what the counterpart user in itslearning is to a user in Azure AD.</span></span> <span data-ttu-id="e7144-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de itslearning.</span><span class="sxs-lookup"><span data-stu-id="e7144-140">In other words, a link relationship between an Azure AD user and the related user in itslearning needs to be established.</span></span>

<span data-ttu-id="e7144-141">Para establecer la relación de vínculo, en itslearning, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="e7144-141">In itslearning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e7144-142">Para configurar y probar el inicio de sesión único de Azure AD con itslearning, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e7144-142">To configure and test Azure AD single sign-on with itslearning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e7144-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="e7144-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e7144-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7144-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e7144-145">**[Creación de un usuario de prueba de itslearning](#creating-an-itslearning-test-user)**: para tener un homólogo de Britta Simon en itslearning que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7144-145">**[Creating an itslearning test user](#creating-an-itslearning-test-user)** - to have a counterpart of Britta Simon in itslearning that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e7144-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7144-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e7144-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e7144-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e7144-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7144-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e7144-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación itslearning.</span><span class="sxs-lookup"><span data-stu-id="e7144-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your itslearning application.</span></span>

<span data-ttu-id="e7144-150">**Para configurar el inicio de sesión único de Azure AD con itslearning, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e7144-150">**To configure Azure AD single sign-on with itslearning, perform the following steps:**</span></span>

1. <span data-ttu-id="e7144-151">En Azure Portal, en la página de integración de la aplicación **itslearning**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e7144-151">In the Azure portal, on the **itslearning** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e7144-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e7144-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_samlbase.png)

3. <span data-ttu-id="e7144-155">En la sección **Dominio y direcciones URL de itslearning**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e7144-155">On the **itslearning Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_url.png)

    <span data-ttu-id="e7144-157">a.</span><span class="sxs-lookup"><span data-stu-id="e7144-157">a.</span></span> <span data-ttu-id="e7144-158">En el cuadro de texto **URL de inicio de sesión**, escriba una URL como:</span><span class="sxs-lookup"><span data-stu-id="e7144-158">In the **Sign-on URL** textbox, type a URL as:</span></span>
    | |
    |--| 
    | `https://www.itslearning.com/index.aspx`|
    | `https://us1.itslearning.com/index.aspx`|

    <span data-ttu-id="e7144-159">b.</span><span class="sxs-lookup"><span data-stu-id="e7144-159">b.</span></span> <span data-ttu-id="e7144-160">En el cuadro de texto **Identificador**, escriba una dirección URL como: `urn:mace:saml2v2.no:services:com.itslearning`</span><span class="sxs-lookup"><span data-stu-id="e7144-160">In the **Identifier** textbox, type a URL as: `urn:mace:saml2v2.no:services:com.itslearning`</span></span>

4. <span data-ttu-id="e7144-161">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e7144-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_certificate.png) 

5. <span data-ttu-id="e7144-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e7144-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-itslearning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e7144-165">Para configurar el inicio de sesión único en el lado de **itslearning**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de itslearning](mailto:support@itslearning.com).</span><span class="sxs-lookup"><span data-stu-id="e7144-165">To configure single sign-on on **itslearning** side, you need to send the downloaded **Metadata XML** to [itslearning support team](mailto:support@itslearning.com).</span></span> <span data-ttu-id="e7144-166">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="e7144-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e7144-167">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e7144-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e7144-168">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e7144-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e7144-169">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e7144-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e7144-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7144-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="e7144-171">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e7144-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="e7144-173">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="e7144-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e7144-174">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e7144-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itslearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e7144-176">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e7144-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itslearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e7144-178">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e7144-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itslearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e7144-180">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="e7144-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-itslearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e7144-182">a.</span><span class="sxs-lookup"><span data-stu-id="e7144-182">a.</span></span> <span data-ttu-id="e7144-183">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7144-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e7144-184">b.</span><span class="sxs-lookup"><span data-stu-id="e7144-184">b.</span></span> <span data-ttu-id="e7144-185">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7144-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e7144-186">c.</span><span class="sxs-lookup"><span data-stu-id="e7144-186">c.</span></span> <span data-ttu-id="e7144-187">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e7144-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e7144-188">d.</span><span class="sxs-lookup"><span data-stu-id="e7144-188">d.</span></span> <span data-ttu-id="e7144-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e7144-189">Click **Create**.</span></span>
 
### <a name="creating-an-itslearning-test-user"></a><span data-ttu-id="e7144-190">Creación de un usuario de prueba de itslearning</span><span class="sxs-lookup"><span data-stu-id="e7144-190">Creating an itslearning test user</span></span>

<span data-ttu-id="e7144-191">En esta sección, creará un usuario llamado Britta Simon en itslearning.</span><span class="sxs-lookup"><span data-stu-id="e7144-191">In this section, you create a user called Britta Simon in itslearning.</span></span> <span data-ttu-id="e7144-192">Colabore con el [equipo de soporte técnico de cliente de itslearning](mailto:support@itslearning.com) para agregar los usuarios a la plataforma de itslearning.</span><span class="sxs-lookup"><span data-stu-id="e7144-192">Work with [itslearning Client support team](mailto:support@itslearning.com) to add the users in the itslearning platform.</span></span> <span data-ttu-id="e7144-193">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e7144-193">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e7144-194">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7144-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e7144-195">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a itslearning.</span><span class="sxs-lookup"><span data-stu-id="e7144-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to itslearning.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="e7144-197">**Para asignar Britta Simon a itslearning, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e7144-197">**To assign Britta Simon to itslearning, perform the following steps:**</span></span>

1. <span data-ttu-id="e7144-198">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e7144-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e7144-200">En la lista de aplicaciones, seleccione **itslearning**.</span><span class="sxs-lookup"><span data-stu-id="e7144-200">In the applications list, select **itslearning**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_app.png) 

3. <span data-ttu-id="e7144-202">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e7144-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="e7144-204">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e7144-204">Click **Add** button.</span></span> <span data-ttu-id="e7144-205">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e7144-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="e7144-207">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="e7144-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e7144-208">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e7144-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e7144-209">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e7144-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e7144-210">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="e7144-210">Testing single sign-on</span></span>

<span data-ttu-id="e7144-211">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e7144-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e7144-212">Al hacer clic en el icono de itslearning del Panel de acceso, debería entrar en la página de inicio de sesión de la aplicación itslearning.</span><span class="sxs-lookup"><span data-stu-id="e7144-212">When you click the itslearning tile in the Access Panel, you should get login page of itslearning application.</span></span> <span data-ttu-id="e7144-213">Haga clic en **Iniciar sesión con Windows Azure ACS1** para iniciar sesión correctamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e7144-213">Click **Log in with Windows Azure ACS1** for successful login into the application.</span></span>

  ![Inicio de sesión](./media/active-directory-saas-itslearning-tutorial/login.png)

<span data-ttu-id="e7144-215">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e7144-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e7144-216">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e7144-216">Additional resources</span></span>

* [<span data-ttu-id="e7144-217">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7144-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e7144-218">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e7144-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_203.png

