---
title: "Tutorial: Integración de Azure Active Directory con RightAnswers | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y RightAnswers."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7f09e25a-a716-41e1-8ca3-fd00e3d1b8cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: e5985831598a0e5b1277d2c6cd02b03c919aad4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightanswers"></a><span data-ttu-id="5a93d-103">Tutorial: Integración de Azure Active Directory con RightAnswers</span><span class="sxs-lookup"><span data-stu-id="5a93d-103">Tutorial: Azure Active Directory integration with RightAnswers</span></span>

<span data-ttu-id="5a93d-104">En este tutorial, aprenderá a integrar RightAnswers con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5a93d-104">In this tutorial, you learn how to integrate RightAnswers with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5a93d-105">La integración de RightAnswers con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="5a93d-105">Integrating RightAnswers with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5a93d-106">Puede controlar en Azure AD quién tiene acceso a RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="5a93d-106">You can control in Azure AD who has access to RightAnswers</span></span>
- <span data-ttu-id="5a93d-107">Puede permitir que los usuarios inicien sesión automáticamente en RightAnswers (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a93d-107">You can enable your users to automatically get signed-on to RightAnswers (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5a93d-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5a93d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5a93d-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5a93d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a93d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5a93d-110">Prerequisites</span></span>

<span data-ttu-id="5a93d-111">Para configurar la integración de Azure AD con RightAnswers, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="5a93d-111">To configure Azure AD integration with RightAnswers, you need the following items:</span></span>

- <span data-ttu-id="5a93d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a93d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5a93d-113">Una suscripción habilitada para el inicio de sesión único en RightAnswers</span><span class="sxs-lookup"><span data-stu-id="5a93d-113">A RightAnswers single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5a93d-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="5a93d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5a93d-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="5a93d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5a93d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="5a93d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5a93d-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5a93d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5a93d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="5a93d-118">Scenario description</span></span>
<span data-ttu-id="5a93d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="5a93d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5a93d-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="5a93d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5a93d-121">Adición de RightAnswers desde la galería</span><span class="sxs-lookup"><span data-stu-id="5a93d-121">Adding RightAnswers from the gallery</span></span>
2. <span data-ttu-id="5a93d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a93d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightanswers-from-the-gallery"></a><span data-ttu-id="5a93d-123">Adición de RightAnswers desde la galería</span><span class="sxs-lookup"><span data-stu-id="5a93d-123">Adding RightAnswers from the gallery</span></span>
<span data-ttu-id="5a93d-124">Para configurar la integración de RightAnswers en Azure AD, será preciso que agregue RightAnswers desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="5a93d-124">To configure the integration of RightAnswers into Azure AD, you need to add RightAnswers from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5a93d-125">**Para agregar RightAnswers desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="5a93d-125">**To add RightAnswers from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5a93d-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5a93d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5a93d-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="5a93d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5a93d-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5a93d-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="5a93d-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5a93d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="5a93d-133">En el cuadro de búsqueda, escriba **RightAnswers**.</span><span class="sxs-lookup"><span data-stu-id="5a93d-133">In the search box, type **RightAnswers**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_search.png)

5. <span data-ttu-id="5a93d-135">En el panel de resultados, seleccione **RightAnswers** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5a93d-135">In the results panel, select **RightAnswers**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5a93d-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a93d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5a93d-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con RightAnswers con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5a93d-138">In this section, you configure and test Azure AD single sign-on with RightAnswers based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5a93d-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de RightAnswers para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a93d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RightAnswers is to a user in Azure AD.</span></span> <span data-ttu-id="5a93d-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="5a93d-140">In other words, a link relationship between an Azure AD user and the related user in RightAnswers needs to be established.</span></span>

<span data-ttu-id="5a93d-141">Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario** de RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="5a93d-141">In RightAnswers, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5a93d-142">Para configurar y probar el inicio de sesión único de Azure AD con RightAnswers, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="5a93d-142">To configure and test Azure AD single sign-on with RightAnswers, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5a93d-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="5a93d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5a93d-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5a93d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5a93d-145">**[Creación de un usuario de prueba de RightAnswers](#creating-a-rightanswers-test-user)**: el objetivo es tener un homólogo de Britta Simon en RightAnswers que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a93d-145">**[Creating a RightAnswers test user](#creating-a-rightanswers-test-user)** - to have a counterpart of Britta Simon in RightAnswers that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5a93d-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a93d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5a93d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="5a93d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5a93d-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a93d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5a93d-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="5a93d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RightAnswers application.</span></span>

<span data-ttu-id="5a93d-150">**Para configurar el inicio de sesión único de Azure AD con RightAnswers, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="5a93d-150">**To configure Azure AD single sign-on with RightAnswers, perform the following steps:**</span></span>

1. <span data-ttu-id="5a93d-151">En la página de integración de la aplicación **RightAnswers** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="5a93d-151">In the Azure portal, on the **RightAnswers** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="5a93d-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5a93d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_samlbase.png)

3. <span data-ttu-id="5a93d-155">En la sección **Dominio y direcciones URL de RightAnswers**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5a93d-155">On the **RightAnswers Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_url.png)

    <span data-ttu-id="5a93d-157">a.</span><span class="sxs-lookup"><span data-stu-id="5a93d-157">a.</span></span> <span data-ttu-id="5a93d-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.rightanswers.com/portal/ss/`.</span><span class="sxs-lookup"><span data-stu-id="5a93d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.rightanswers.com/portal/ss/`</span></span>

    <span data-ttu-id="5a93d-159">b.</span><span class="sxs-lookup"><span data-stu-id="5a93d-159">b.</span></span> <span data-ttu-id="5a93d-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.rightanswers.com:<identifier>/portal`</span><span class="sxs-lookup"><span data-stu-id="5a93d-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.rightanswers.com:<identifier>/portal`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5a93d-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="5a93d-161">These values are not real.</span></span> <span data-ttu-id="5a93d-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="5a93d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5a93d-163">Póngase en contacto con el [equipo de atención al cliente de RightAnswers](https://www.rightanswers.com/contact-us/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="5a93d-163">Contact [RightAnswers Client support team](https://www.rightanswers.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="5a93d-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="5a93d-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_certificate.png) 

5. <span data-ttu-id="5a93d-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="5a93d-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rightanswers-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5a93d-168">Para configurar el inicio de sesión único en **RightAnswers**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de RightAnswers](https://www.rightanswers.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="5a93d-168">To configure single sign-on on **RightAnswers** side, you need to send the downloaded **Metadata XML** to [RightAnswers support team](https://www.rightanswers.com/contact-us/).</span></span>

    >[!NOTE]
    ><span data-ttu-id="5a93d-169">El equipo de soporte técnico de RightAnswers es el que tiene que realizar la configuración real de SSO.</span><span class="sxs-lookup"><span data-stu-id="5a93d-169">Your RightAnswers support team has to do the actual SSO configuration.</span></span>
    ><span data-ttu-id="5a93d-170">Cuando SSO se haya habilitado en su suscripción recibirá una notificación.</span><span class="sxs-lookup"><span data-stu-id="5a93d-170">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="5a93d-171">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5a93d-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5a93d-172">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="5a93d-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5a93d-173">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5a93d-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5a93d-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a93d-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="5a93d-175">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5a93d-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="5a93d-177">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="5a93d-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5a93d-178">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5a93d-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5a93d-180">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5a93d-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5a93d-182">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5a93d-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5a93d-184">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="5a93d-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5a93d-186">a.</span><span class="sxs-lookup"><span data-stu-id="5a93d-186">a.</span></span> <span data-ttu-id="5a93d-187">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5a93d-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5a93d-188">b.</span><span class="sxs-lookup"><span data-stu-id="5a93d-188">b.</span></span> <span data-ttu-id="5a93d-189">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5a93d-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5a93d-190">c.</span><span class="sxs-lookup"><span data-stu-id="5a93d-190">c.</span></span> <span data-ttu-id="5a93d-191">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="5a93d-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5a93d-192">d.</span><span class="sxs-lookup"><span data-stu-id="5a93d-192">d.</span></span> <span data-ttu-id="5a93d-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5a93d-193">Click **Create**.</span></span>
 
### <a name="creating-a-rightanswers-test-user"></a><span data-ttu-id="5a93d-194">Creación de un usuario de prueba de RightAnswers</span><span class="sxs-lookup"><span data-stu-id="5a93d-194">Creating a RightAnswers test user</span></span>

<span data-ttu-id="5a93d-195">Para permitir que los usuarios de Azure AD inicien sesión en RightAnswers, deben aprovisionarse en RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="5a93d-195">To enable Azure AD users to log in to RightAnswers, they must be provisioned into RightAnswers.</span></span> <span data-ttu-id="5a93d-196">En el caso de RightAnswers, el aprovisionamiento constituye una tarea automatizada, por lo que no se requiere ninguna acción por su parte.</span><span class="sxs-lookup"><span data-stu-id="5a93d-196">When RightAnswers, provisioning is an automated task so there is no action item for you.</span></span>

<span data-ttu-id="5a93d-197">Los usuarios se crean automáticamente si es necesario durante el primer intento de inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5a93d-197">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="5a93d-198">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de RightAnswers ofrecida por RightAnswers para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="5a93d-198">You can use any other RightAnswers user account creation tools or APIs provided by RightAnswers to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5a93d-199">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a93d-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5a93d-200">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="5a93d-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RightAnswers.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="5a93d-202">**Para asignar a Britta Simon a RightAnswers, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="5a93d-202">**To assign Britta Simon to RightAnswers, perform the following steps:**</span></span>

1. <span data-ttu-id="5a93d-203">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5a93d-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="5a93d-205">En la lista de aplicaciones, seleccione **RightAnswers**.</span><span class="sxs-lookup"><span data-stu-id="5a93d-205">In the applications list, select **RightAnswers**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_app.png) 

3. <span data-ttu-id="5a93d-207">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5a93d-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="5a93d-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5a93d-209">Click **Add** button.</span></span> <span data-ttu-id="5a93d-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5a93d-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="5a93d-212">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="5a93d-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5a93d-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5a93d-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5a93d-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5a93d-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5a93d-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="5a93d-215">Testing single sign-on</span></span>

<span data-ttu-id="5a93d-216">Si desea probar la configuración de inicio de sesión único (SSO), abra el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="5a93d-216">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="5a93d-217">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5a93d-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>
## <a name="additional-resources"></a><span data-ttu-id="5a93d-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="5a93d-218">Additional resources</span></span>

* [<span data-ttu-id="5a93d-219">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5a93d-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5a93d-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5a93d-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_203.png

