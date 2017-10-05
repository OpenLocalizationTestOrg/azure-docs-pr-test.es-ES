---
title: "Tutorial: Integración de Azure Active Directory con Jobbadmin | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Jobbadmin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c5208b0d-66a3-49ed-9aad-70d21f54aee0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 848a6d6d0f072bc3f697ff57756714fc45e7dcc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobbadmin"></a><span data-ttu-id="bb161-103">Tutorial: Integración de Azure Active Directory con Jobbadmin</span><span class="sxs-lookup"><span data-stu-id="bb161-103">Tutorial: Azure Active Directory integration with Jobbadmin</span></span>

<span data-ttu-id="bb161-104">En este tutorial, obtendrá información sobre cómo integrar Jobbadmin con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bb161-104">In this tutorial, you learn how to integrate Jobbadmin with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bb161-105">Integrar Jobbadmin con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="bb161-105">Integrating Jobbadmin with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bb161-106">En Azure AD se puede controlar quién tiene acceso a Jobbadmin</span><span class="sxs-lookup"><span data-stu-id="bb161-106">You can control in Azure AD who has access to Jobbadmin</span></span>
- <span data-ttu-id="bb161-107">Puede permitir que los usuarios inicien sesión automáticamente en Jobbadmin (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb161-107">You can enable your users to automatically get signed-on to Jobbadmin (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bb161-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="bb161-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bb161-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bb161-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb161-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bb161-110">Prerequisites</span></span>

<span data-ttu-id="bb161-111">Para configurar la integración de Azure AD con Jobbadmin, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="bb161-111">To configure Azure AD integration with Jobbadmin, you need the following items:</span></span>

- <span data-ttu-id="bb161-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb161-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bb161-113">Una suscripción habilitada para el inicio de sesión único en Jobbadmin</span><span class="sxs-lookup"><span data-stu-id="bb161-113">A Jobbadmin single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bb161-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="bb161-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bb161-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="bb161-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bb161-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bb161-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bb161-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bb161-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bb161-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="bb161-118">Scenario description</span></span>
<span data-ttu-id="bb161-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="bb161-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bb161-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="bb161-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bb161-121">Adición de Jobbadmin desde la galería</span><span class="sxs-lookup"><span data-stu-id="bb161-121">Adding Jobbadmin from the gallery</span></span>
2. <span data-ttu-id="bb161-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb161-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobbadmin-from-the-gallery"></a><span data-ttu-id="bb161-123">Adición de Jobbadmin desde la galería</span><span class="sxs-lookup"><span data-stu-id="bb161-123">Adding Jobbadmin from the gallery</span></span>
<span data-ttu-id="bb161-124">Para configurar la integración de Jobbadmin en Azure AD, será preciso que agregue Jobbadmin desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="bb161-124">To configure the integration of Jobbadmin into Azure AD, you need to add Jobbadmin from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bb161-125">**Para agregar Jobbadmin desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="bb161-125">**To add Jobbadmin from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bb161-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bb161-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bb161-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="bb161-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bb161-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bb161-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="bb161-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bb161-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="bb161-133">En el cuadro de búsqueda, escriba **Jobbadmin**.</span><span class="sxs-lookup"><span data-stu-id="bb161-133">In the search box, type **Jobbadmin**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_search.png)

5. <span data-ttu-id="bb161-135">En el panel de resultados, seleccione **Jobbadmin** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bb161-135">In the results panel, select **Jobbadmin**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bb161-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb161-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bb161-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Jobbadmin con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bb161-138">In this section, you configure and test Azure AD single sign-on with Jobbadmin based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bb161-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Jobbadmin para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb161-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jobbadmin is to a user in Azure AD.</span></span> <span data-ttu-id="bb161-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="bb161-140">In other words, a link relationship between an Azure AD user and the related user in Jobbadmin needs to be established.</span></span>

<span data-ttu-id="bb161-141">Para establecer la relación de vínculo, en Jobbadmin, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="bb161-141">In Jobbadmin, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bb161-142">Para configurar y probar el inicio de sesión único de Azure AD con Jobbadmin, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="bb161-142">To configure and test Azure AD single sign-on with Jobbadmin, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bb161-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="bb161-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bb161-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bb161-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bb161-145">**[Creación de un usuario de prueba de Jobbadmin](#creating-a-jobbadmin-test-user)**: para tener un homólogo de Britta Simon en Jobbadmin que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb161-145">**[Creating a Jobbadmin test user](#creating-a-jobbadmin-test-user)** - to have a counterpart of Britta Simon in Jobbadmin that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bb161-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb161-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bb161-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="bb161-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bb161-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb161-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bb161-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="bb161-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jobbadmin application.</span></span>

<span data-ttu-id="bb161-150">**Para configurar el inicio de sesión único de Azure AD con Jobbadmin, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="bb161-150">**To configure Azure AD single sign-on with Jobbadmin, perform the following steps:**</span></span>

1. <span data-ttu-id="bb161-151">En Azure Portal, en la página de integración de la aplicación **Jobbadmin**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="bb161-151">In the Azure portal, on the **Jobbadmin** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="bb161-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="bb161-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_samlbase.png)

3. <span data-ttu-id="bb161-155">En la sección **Dominio y direcciones URL de Jobbadmin**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bb161-155">On the **Jobbadmin Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_url.png)

    <span data-ttu-id="bb161-157">a.</span><span class="sxs-lookup"><span data-stu-id="bb161-157">a.</span></span> <span data-ttu-id="bb161-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`.</span><span class="sxs-lookup"><span data-stu-id="bb161-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span></span>

    <span data-ttu-id="bb161-159">b.</span><span class="sxs-lookup"><span data-stu-id="bb161-159">b.</span></span> <span data-ttu-id="bb161-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<instancename>.jobnorge.no`</span><span class="sxs-lookup"><span data-stu-id="bb161-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.jobnorge.no`</span></span>

    <span data-ttu-id="bb161-161">c.</span><span class="sxs-lookup"><span data-stu-id="bb161-161">c.</span></span> <span data-ttu-id="bb161-162">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`.</span><span class="sxs-lookup"><span data-stu-id="bb161-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bb161-163">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="bb161-163">These values are not real.</span></span> <span data-ttu-id="bb161-164">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="bb161-164">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bb161-165">Póngase en contacto con el [equipo de soporte de cliente de Jobbadmin](https://www.jobbnorge.no/om-oss/kontakt-oss) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="bb161-165">Contact [Jobbadmin Client support team](https://www.jobbnorge.no/om-oss/kontakt-oss) to get these values.</span></span> 
 


4. <span data-ttu-id="bb161-166">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="bb161-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_certificate.png) 

5. <span data-ttu-id="bb161-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="bb161-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bb161-170">Para configurar el inicio de sesión único en el lado de **Jobbadmin**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Jobbadmin](https://www.jobbnorge.no/om-oss/kontakt-oss).</span><span class="sxs-lookup"><span data-stu-id="bb161-170">To configure single sign-on on **Jobbadmin** side, you need to send the downloaded **Metadata XML** to [Jobbadmin support team](https://www.jobbnorge.no/om-oss/kontakt-oss).</span></span> <span data-ttu-id="bb161-171">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="bb161-171">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="bb161-172">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bb161-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bb161-173">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="bb161-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bb161-174">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bb161-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bb161-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb161-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="bb161-176">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bb161-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="bb161-178">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="bb161-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bb161-179">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bb161-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bb161-181">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="bb161-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bb161-183">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bb161-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bb161-185">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="bb161-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bb161-187">a.</span><span class="sxs-lookup"><span data-stu-id="bb161-187">a.</span></span> <span data-ttu-id="bb161-188">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bb161-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bb161-189">b.</span><span class="sxs-lookup"><span data-stu-id="bb161-189">b.</span></span> <span data-ttu-id="bb161-190">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bb161-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bb161-191">c.</span><span class="sxs-lookup"><span data-stu-id="bb161-191">c.</span></span> <span data-ttu-id="bb161-192">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="bb161-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bb161-193">d.</span><span class="sxs-lookup"><span data-stu-id="bb161-193">d.</span></span> <span data-ttu-id="bb161-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bb161-194">Click **Create**.</span></span>
 
### <a name="creating-a-jobbadmin-test-user"></a><span data-ttu-id="bb161-195">Creación de un usuario de prueba de Jobbadmin</span><span class="sxs-lookup"><span data-stu-id="bb161-195">Creating a Jobbadmin test user</span></span>

<span data-ttu-id="bb161-196">Para permitir que los usuarios de Azure AD inicien sesión en Jobbadmin, es necesario que se aprovisionen en Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="bb161-196">To enable Azure AD users to log in to Jobbadmin, they must be provisioned into Jobbadmin.</span></span>
 
<span data-ttu-id="bb161-197">Póngase en contacto con el [equipo de soporte técnico de Jobbadmin](https://www.jobbnorge.no/om-oss/kontakt-oss) para obtener los usuarios agregados en su lado.</span><span class="sxs-lookup"><span data-stu-id="bb161-197">Please contact [Jobbadmin support team](https://www.jobbnorge.no/om-oss/kontakt-oss) to get the users added on their side.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bb161-198">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb161-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bb161-199">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="bb161-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jobbadmin.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="bb161-201">**Para asignar a Britta Simon a Jobbadmin, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="bb161-201">**To assign Britta Simon to Jobbadmin, perform the following steps:**</span></span>

1. <span data-ttu-id="bb161-202">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bb161-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="bb161-204">En la lista de aplicaciones, seleccione **Jobbadmin**.</span><span class="sxs-lookup"><span data-stu-id="bb161-204">In the applications list, select **Jobbadmin**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_app.png) 

3. <span data-ttu-id="bb161-206">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bb161-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="bb161-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="bb161-208">Click **Add** button.</span></span> <span data-ttu-id="bb161-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bb161-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="bb161-211">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="bb161-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bb161-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bb161-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bb161-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bb161-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bb161-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="bb161-214">Testing single sign-on</span></span>

<span data-ttu-id="bb161-215">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="bb161-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bb161-216">Al hacer clic en el icono de Jobbadmin del Panel de acceso, debería entrar en la página de inicio de sesión de la aplicación Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="bb161-216">When you click the Jobbadmin tile in the Access Panel, you should get login page of Jobbadmin application.</span></span>
<span data-ttu-id="bb161-217">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bb161-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bb161-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="bb161-218">Additional resources</span></span>

* [<span data-ttu-id="bb161-219">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb161-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bb161-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bb161-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_203.png

