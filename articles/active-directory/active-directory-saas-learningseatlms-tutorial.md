---
title: "Tutorial: Integración de Azure Active Directory con Learning Seat LMS | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Learning Seat LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bb056fcf-4135-478e-85b1-5015d1f07b85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: jeedes
ms.openlocfilehash: 877e0288fdd1f590acf064c204aff0741539b112
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-seat-lms"></a><span data-ttu-id="0a377-103">Tutorial: Integración de Azure Active Directory con Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="0a377-103">Tutorial: Azure Active Directory integration with Learning Seat LMS</span></span>

<span data-ttu-id="0a377-104">En este tutorial, obtendrá información sobre cómo integrar Learning Seat LMS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a377-104">In this tutorial, you learn how to integrate Learning Seat LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a377-105">La integración de Learning Seat LMS con Azure AD ofrece las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0a377-105">Integrating Learning Seat LMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0a377-106">Puede controlar en Azure AD quién tiene acceso a Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="0a377-106">You can control in Azure AD who has access to Learning Seat LMS</span></span>
- <span data-ttu-id="0a377-107">Puede permitir que los usuarios inicien sesión automáticamente en Learning Seat LMS (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a377-107">You can enable your users to automatically get signed-on to Learning Seat LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0a377-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0a377-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0a377-109">Si quiere conocer más detalles sobre la integración de aplicaciones SaaS con Azure AD, vea:</span><span class="sxs-lookup"><span data-stu-id="0a377-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="0a377-110">[¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="0a377-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a377-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0a377-111">Prerequisites</span></span>

<span data-ttu-id="0a377-112">Para configurar la integración de Azure AD con Learning Seat LMS, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0a377-112">To configure Azure AD integration with Learning Seat LMS, you need the following items:</span></span>

- <span data-ttu-id="0a377-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a377-113">An Azure AD subscription</span></span>
- <span data-ttu-id="0a377-114">Una suscripción habilitada para el inicio de sesión único en Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="0a377-114">A Learning Seat LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a377-115">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0a377-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a377-116">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0a377-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a377-117">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0a377-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a377-118">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a377-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a377-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0a377-119">Scenario description</span></span>
<span data-ttu-id="0a377-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0a377-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a377-121">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="0a377-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a377-122">Incorporación de Learning Seat LMS desde la galería</span><span class="sxs-lookup"><span data-stu-id="0a377-122">Adding Learning Seat LMS from the gallery</span></span>
2. <span data-ttu-id="0a377-123">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a377-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-seat-lms-from-the-gallery"></a><span data-ttu-id="0a377-124">Incorporación de Learning Seat LMS desde la galería</span><span class="sxs-lookup"><span data-stu-id="0a377-124">Adding Learning Seat LMS from the gallery</span></span>
<span data-ttu-id="0a377-125">Para configurar la integración de Learning Seat LMS en Azure AD, deberá agregar Learning Seat LMS desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="0a377-125">To configure the integration of Learning Seat LMS into Azure AD, you need to add Learning Seat LMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0a377-126">**Para agregar Learning Seat LMS desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="0a377-126">**To add Learning Seat LMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0a377-127">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0a377-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0a377-129">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0a377-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0a377-130">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0a377-130">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0a377-132">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a377-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0a377-134">En el cuadro de búsqueda, escriba **Learning Seat LMS**.</span><span class="sxs-lookup"><span data-stu-id="0a377-134">In the search box, type **Learning Seat LMS**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_search.png)

5. <span data-ttu-id="0a377-136">En el panel de resultados, seleccione **Learning Seat LMS** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a377-136">In the results panel, select **Learning Seat LMS**, and then click **Add** button to add the application.</span></span>


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0a377-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a377-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0a377-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Learning Seat LMS con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0a377-138">In this section, you configure and test Azure AD single sign-on with Learning Seat LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0a377-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Learning Seat LMS para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a377-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learning Seat LMS is to a user in Azure AD.</span></span> <span data-ttu-id="0a377-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="0a377-140">In other words, a link relationship between an Azure AD user and the related user in Learning Seat LMS needs to be established.</span></span>

<span data-ttu-id="0a377-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor de **Nombre de usuario** en Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="0a377-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Learning Seat LMS.</span></span>

<span data-ttu-id="0a377-142">Para configurar y probar el inicio de sesión único de Azure AD con Learning Seat LMS, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0a377-142">To configure and test Azure AD single sign-on with Learning Seat LMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0a377-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="0a377-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0a377-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a377-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0a377-145">**[Creación de un usuario de prueba de Learning Seat LMS](#creating-a-learnconnect-test-user)**: el objetivo es tener un homólogo de Britta Simon en Learning Seat LMS que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a377-145">**[Creating a Learning Seat LMS test user](#creating-a-learnconnect-test-user)** - to have a counterpart of Britta Simon in Learning Seat LMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0a377-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a377-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0a377-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0a377-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0a377-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a377-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0a377-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="0a377-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learning Seat LMS application.</span></span>

<span data-ttu-id="0a377-150">**Para configurar el inicio de sesión único de Azure AD con Learning Seat LMS, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="0a377-150">**To configure Azure AD single sign-on with Learning Seat LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="0a377-151">En la página de integración de la aplicación **Learning Seat LMS** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0a377-151">In the Azure portal, on the **Learning Seat LMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0a377-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0a377-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_samlbase.png)

3. <span data-ttu-id="0a377-155">En la sección **Dominio y direcciones URL de Learning Seat LMS**, realice los siguientes pasos si quiere configurar la aplicación en el modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="0a377-155">On the **Learning Seat LMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url.png)

    <span data-ttu-id="0a377-157">a.</span><span class="sxs-lookup"><span data-stu-id="0a377-157">a.</span></span> <span data-ttu-id="0a377-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="0a377-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com`</span></span>

    <span data-ttu-id="0a377-159">b.</span><span class="sxs-lookup"><span data-stu-id="0a377-159">b.</span></span> <span data-ttu-id="0a377-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`.</span><span class="sxs-lookup"><span data-stu-id="0a377-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span></span>

4. <span data-ttu-id="0a377-161">Active **Mostrar configuración avanzada de URL**, si desea volver a configurar la aplicación en modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="0a377-161">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url2.png)

    <span data-ttu-id="0a377-163">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.learningseatlms.com`.</span><span class="sxs-lookup"><span data-stu-id="0a377-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="0a377-164">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="0a377-164">These values are not the real values.</span></span> <span data-ttu-id="0a377-165">Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="0a377-165">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="0a377-166">Póngase en contacto con el [equipo de soporte técnico de Learning Seat LMS](http://help.learningseatlms.com/help) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="0a377-166">Contact [Learning Seat support team](http://help.learningseatlms.com/help) to get these values.</span></span> 

5. <span data-ttu-id="0a377-167">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0a377-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_certificate.png) 

6. <span data-ttu-id="0a377-169">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0a377-169">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnconnect-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="0a377-171">Para configurar el inicio de sesión único en **Learning Seat LMS**, es preciso enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Learning Seat LMS](http://help.learningseatlms.com/help).</span><span class="sxs-lookup"><span data-stu-id="0a377-171">To configure single sign-on on **Learning Seat LMS** side, you need to send the downloaded **Metadata XML** to [Learning Seat support team](http://help.learningseatlms.com/help).</span></span>

> [!TIP]
> <span data-ttu-id="0a377-172">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0a377-172">You can now read a concise version of these instructions inside the [Azure  portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0a377-173">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="0a377-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0a377-174">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0a377-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0a377-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a377-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="0a377-176">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0a377-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0a377-178">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="0a377-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0a377-179">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0a377-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0a377-181">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0a377-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0a377-183">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a377-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0a377-185">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="0a377-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0a377-187">a.</span><span class="sxs-lookup"><span data-stu-id="0a377-187">a.</span></span> <span data-ttu-id="0a377-188">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0a377-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a377-189">b.</span><span class="sxs-lookup"><span data-stu-id="0a377-189">b.</span></span> <span data-ttu-id="0a377-190">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a377-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0a377-191">c.</span><span class="sxs-lookup"><span data-stu-id="0a377-191">c.</span></span> <span data-ttu-id="0a377-192">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0a377-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0a377-193">d.</span><span class="sxs-lookup"><span data-stu-id="0a377-193">d.</span></span> <span data-ttu-id="0a377-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0a377-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-seat-lms-test-user"></a><span data-ttu-id="0a377-195">Creación de un usuario de prueba de Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="0a377-195">Creating a Learning Seat LMS test user</span></span>

<span data-ttu-id="0a377-196">En esta sección, creará un usuario llamado Britta Simon en Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="0a377-196">In this section, you create a user called Britta Simon in Learning Seat LMS.</span></span> <span data-ttu-id="0a377-197">Póngase en contacto con el [equipo de soporte técnico de Learning Seat LMS](http://help.learningseatlms.com/help) con toda la información de usuario para agregar los usuarios en la aplicación Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="0a377-197">Contact [Learning Seat support team](http://help.learningseatlms.com/help) with all the user information to add the users in the Learning Seat LMS application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0a377-198">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a377-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0a377-199">En esta sección, concederá acceso a Britta Simon a Learning Seat LMS para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="0a377-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learning Seat LMS.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0a377-201">**Para asignar a Britta Simon a Learning Seat LMS, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="0a377-201">**To assign Britta Simon to Learning Seat LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="0a377-202">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0a377-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0a377-204">En la lista de aplicaciones, seleccione **Learning Seat LMS**.</span><span class="sxs-lookup"><span data-stu-id="0a377-204">In the applications list, select **Learning Seat LMS**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_app.png) 

3. <span data-ttu-id="0a377-206">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0a377-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0a377-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0a377-208">Click **Add** button.</span></span> <span data-ttu-id="0a377-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0a377-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0a377-211">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="0a377-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0a377-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0a377-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0a377-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0a377-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0a377-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="0a377-214">Testing single sign-on</span></span>

<span data-ttu-id="0a377-215">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0a377-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> 

<span data-ttu-id="0a377-216">Al hacer clic en el icono de Learning Seat LMS en el panel de acceso, debería iniciar sesión automáticamente en la aplicación Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="0a377-216">Click the Learning Seat LMS tile in the Access Panel, you will be automatically signed-on to your Learning Seat LMS application.</span></span> <span data-ttu-id="0a377-217">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="0a377-217">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0a377-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0a377-218">Additional resources</span></span>

* [<span data-ttu-id="0a377-219">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a377-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0a377-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0a377-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_203.png

