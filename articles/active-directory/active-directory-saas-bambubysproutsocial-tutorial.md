---
title: "Tutorial: Integración de Azure Active Directory con Bambu by Sprout Social | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Bambu by Sprout Social."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 985966d26f6ed0dcd4db47589abf94260ce62bf0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a><span data-ttu-id="867e3-103">Tutorial: Integración de Azure Active Directory con Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="867e3-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span></span>

<span data-ttu-id="867e3-104">En este tutorial, aprenderá a integrar Bambu by Sprout Social con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="867e3-104">In this tutorial, you learn how to integrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="867e3-105">La integración de Bambu by Sprout Social con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="867e3-105">Integrating Bambu by Sprout Social with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="867e3-106">Puede controlar en Azure AD quién tiene acceso a Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="867e3-106">You can control in Azure AD who has access to Bambu by Sprout Social</span></span>
- <span data-ttu-id="867e3-107">Puede permitir que los usuarios inicien sesión automáticamente en Bambu by Sprout Social (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="867e3-107">You can enable your users to automatically get signed-on to Bambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="867e3-108">Puede administrar sus cuentas en una ubicación central: el nuevo portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="867e3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="867e3-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="867e3-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Bambu by Sprout Social, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Bambu by Sprout Social.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="867e3-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="867e3-110">Prerequisites</span></span>

<span data-ttu-id="867e3-111">Para configurar la integración de Azure AD con Bambu by Sprout Social, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="867e3-111">To configure Azure AD integration with Bambu by Sprout Social, you need the following items:</span></span>

- <span data-ttu-id="867e3-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="867e3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="867e3-113">Una suscripción habilitada para el inicio de sesión único en Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="867e3-113">A Bambu by Sprout Social single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="867e3-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="867e3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="867e3-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="867e3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="867e3-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="867e3-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="867e3-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="867e3-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="867e3-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="867e3-118">Scenario description</span></span>
<span data-ttu-id="867e3-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="867e3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="867e3-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="867e3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="867e3-121">Adición de Bambu by Sprout Social desde la galería</span><span class="sxs-lookup"><span data-stu-id="867e3-121">Adding Bambu by Sprout Social from the gallery</span></span>
2. <span data-ttu-id="867e3-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="867e3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bambu-by-sprout-social-from-the-gallery"></a><span data-ttu-id="867e3-123">Adición de Bambu by Sprout Social desde la galería</span><span class="sxs-lookup"><span data-stu-id="867e3-123">Adding Bambu by Sprout Social from the gallery</span></span>
<span data-ttu-id="867e3-124">Para configurar la integración de Bambu by Sprout Social en Azure AD, debe agregar Bambu by Sprout Social desde la galería a su lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="867e3-124">To configure the integration of Bambu by Sprout Social into Azure AD, you need to add Bambu by Sprout Social from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="867e3-125">**Para agregar Bambu by Sprout Social desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="867e3-125">**To add Bambu by Sprout Social from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="867e3-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="867e3-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="867e3-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="867e3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="867e3-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="867e3-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="867e3-131">Haga clic en el botón **Nueva aplicación** en la parte superior del cuadro de diálogo para agregar la nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="867e3-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="867e3-133">En el cuadro de búsqueda, escriba **Bambu by Sprout Social**.</span><span class="sxs-lookup"><span data-stu-id="867e3-133">In the search box, type **Bambu by Sprout Social**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

5. <span data-ttu-id="867e3-135">En el panel de resultados, seleccione **Bambu by Sprout Social** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="867e3-135">In the results panel, select **Bambu by Sprout Social**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="867e3-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="867e3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="867e3-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Bambu by Sprout Social con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="867e3-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="867e3-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Bambu by Sprout Social para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="867e3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bambu by Sprout Social is to a user in Azure AD.</span></span> <span data-ttu-id="867e3-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="867e3-140">In other words, a link relationship between an Azure AD user and the related user in Bambu by Sprout Social needs to be established.</span></span>

<span data-ttu-id="867e3-141">Esta relación de vínculo se establece asignando el valor de **nombre de usuario** en Azure AD como el valor de **nombre de usuario** en Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="867e3-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bambu by Sprout Social.</span></span>

<span data-ttu-id="867e3-142">Para configurar y probar el inicio de sesión único de Azure AD con Bambu by Sprout Social, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="867e3-142">To configure and test Azure AD single sign-on with Bambu by Sprout Social, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="867e3-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="867e3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="867e3-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="867e3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="867e3-145">**[Creación de un usuario de prueba de Bambu by Sprout Social](#creating-a-bambu-by-sprout-social-test-user)**: para tener un homólogo de Britta Simon en Bambu by Sprout Social que esté vinculado a la representación de esta en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="867e3-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - to have a counterpart of Britta Simon in Bambu by Sprout Social that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="867e3-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="867e3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="867e3-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="867e3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="867e3-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="867e3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="867e3-149">En esta sección, habilitará el inicio de sesión único de Azure AD en el portal de Azure y configurará el inicio de sesión único en la aplicación Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="867e3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span></span>

<span data-ttu-id="867e3-150">**Para configurar el inicio de sesión único de Azure AD con Bambu by Sprout Social, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="867e3-150">**To configure Azure AD single sign-on with Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="867e3-151">En el portal de Azure, en la página de integración de la aplicación **Bambu by Sprout Social**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="867e3-151">In the Azure portal, on the **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="867e3-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="867e3-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

3. <span data-ttu-id="867e3-155">En la sección **Dominio y direcciones URL de Bambu by Sprout Social**, el usuario no tiene que realizar ningún paso ya que la aplicación se ha integrado previamente con Azure.</span><span class="sxs-lookup"><span data-stu-id="867e3-155">On the **Bambu by Sprout Social Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

4. <span data-ttu-id="867e3-157">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="867e3-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

5. <span data-ttu-id="867e3-159">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="867e3-159">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="867e3-161">En la sección **Configuración de Bambu by Sprout Social**, haga clic en **Configurar Bambu by Sprout Social** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="867e3-161">On the **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** to open **Configure sign-on** window.</span></span> <span data-ttu-id="867e3-162">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="867e3-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

7. <span data-ttu-id="867e3-164">Para configurar el inicio de sesión único en **Bambu by Sprout Social**, debe enviar el **XML de metadatos** y la **dirección URL de servicio de inicio de sesión de SAML** al [soporte técnico de Bambu by Sprout Social](mailto:support@getbambu.com).</span><span class="sxs-lookup"><span data-stu-id="867e3-164">To configure single sign-on on **Bambu by Sprout Social** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Bambu by Sprout Social support](mailto:support@getbambu.com).</span></span> <span data-ttu-id="867e3-165">Ellos realizarán esta operación para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="867e3-165">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="867e3-166">Ahora puede leer una versión resumida de estas instrucciones dentro del [portal de Azure](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="867e3-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="867e3-167">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="867e3-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click on the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="867e3-168">Puede leer más sobre la característica de documentación insertada aquí: [Documentación insertada sobre Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="867e3-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

<!--### Next steps

To ensure users can sign-in to Bambu by Sprout Social after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Bambu by Sprout Social in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="867e3-169">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="867e3-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="867e3-170">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="867e3-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="867e3-172">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="867e3-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="867e3-173">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="867e3-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="867e3-175">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="867e3-175">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="867e3-177">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="867e3-177">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="867e3-179">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="867e3-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="867e3-181">a.</span><span class="sxs-lookup"><span data-stu-id="867e3-181">a.</span></span> <span data-ttu-id="867e3-182">En el cuadro de texto **Nombre**, escriba **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="867e3-182">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="867e3-183">b.</span><span class="sxs-lookup"><span data-stu-id="867e3-183">b.</span></span> <span data-ttu-id="867e3-184">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="867e3-184">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="867e3-185">c.</span><span class="sxs-lookup"><span data-stu-id="867e3-185">c.</span></span> <span data-ttu-id="867e3-186">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="867e3-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="867e3-187">d.</span><span class="sxs-lookup"><span data-stu-id="867e3-187">d.</span></span> <span data-ttu-id="867e3-188">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="867e3-188">Click **Create**.</span></span>
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a><span data-ttu-id="867e3-189">Creación de un usuario de prueba de Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="867e3-189">Creating a Bambu by Sprout Social test user</span></span>

<span data-ttu-id="867e3-190">La aplicación admite aprovisionamiento de usuarios Just-In-Time y, tras la autenticación, los usuarios se crearán automáticamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="867e3-190">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="867e3-191">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="867e3-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="867e3-192">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="867e3-192">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Bambu by Sprout Social.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="867e3-194">**Para asignar a Britta Simon a Bambu by Sprout Social, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="867e3-194">**To assign Britta Simon to Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="867e3-195">En el portal de Azure, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="867e3-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="867e3-197">En la lista de aplicaciones, seleccione **Bambu by Sprout Social**.</span><span class="sxs-lookup"><span data-stu-id="867e3-197">In the applications list, select **Bambu by Sprout Social**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

3. <span data-ttu-id="867e3-199">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="867e3-199">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="867e3-201">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="867e3-201">Click **Add** button.</span></span> <span data-ttu-id="867e3-202">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="867e3-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="867e3-204">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="867e3-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="867e3-205">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="867e3-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="867e3-206">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="867e3-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="867e3-207">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="867e3-207">Testing single sign-on</span></span>

<span data-ttu-id="867e3-208">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="867e3-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="867e3-209">Al hacer clic en el icono de Bambu by Sprout Social en el Panel de acceso, iniciará sesión automáticamente en la aplicación Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="867e3-209">When you click the Bambu by Sprout Social tile in the Access Panel, you should get automatically signed-on to your Bambu by Sprout Social application.</span></span> <span data-ttu-id="867e3-210">Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="867e3-210">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="867e3-211">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="867e3-211">Additional resources</span></span>

* [<span data-ttu-id="867e3-212">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="867e3-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="867e3-213">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="867e3-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_203.png

