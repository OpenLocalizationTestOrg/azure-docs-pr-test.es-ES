---
title: "Tutorial: Integración de Azure Active Directory con Atomic Learning | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Atomic Learning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 495f54a6-e6c4-41b0-aafa-a6283d33efc8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 6cce8fc839e60eb6498ab48bf68e9906c98889a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atomic-learning"></a><span data-ttu-id="365b1-103">Tutorial: integración de Azure Active Directory con Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="365b1-103">Tutorial: Azure Active Directory integration with Atomic Learning</span></span>

<span data-ttu-id="365b1-104">En este tutorial, obtendrá información sobre cómo integrar Atomic Learning con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="365b1-104">In this tutorial, you learn how to integrate Atomic Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="365b1-105">Integrar Atomic Learning con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="365b1-105">Integrating Atomic Learning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="365b1-106">Puede controlar en Azure AD quién tiene acceso a Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="365b1-106">You can control in Azure AD who has access to Atomic Learning</span></span>
- <span data-ttu-id="365b1-107">Puede permitir que los usuarios inicien sesión automáticamente en Atomic Learning (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="365b1-107">You can enable your users to automatically get signed-on to Atomic Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="365b1-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="365b1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="365b1-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="365b1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="365b1-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="365b1-110">Prerequisites</span></span>

<span data-ttu-id="365b1-111">Para configurar la integración de Azure AD con Atomic Learning, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="365b1-111">To configure Azure AD integration with Atomic Learning, you need the following items:</span></span>

- <span data-ttu-id="365b1-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="365b1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="365b1-113">Una suscripción habilitada para el inicio de sesión único en Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="365b1-113">An Atomic Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="365b1-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="365b1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="365b1-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="365b1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="365b1-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="365b1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="365b1-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="365b1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="365b1-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="365b1-118">Scenario description</span></span>
<span data-ttu-id="365b1-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="365b1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="365b1-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="365b1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="365b1-121">Adición de Atomic Learning desde la galería</span><span class="sxs-lookup"><span data-stu-id="365b1-121">Adding Atomic Learning from the gallery</span></span>
2. <span data-ttu-id="365b1-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="365b1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atomic-learning-from-the-gallery"></a><span data-ttu-id="365b1-123">Adición de Atomic Learning desde la galería</span><span class="sxs-lookup"><span data-stu-id="365b1-123">Adding Atomic Learning from the gallery</span></span>
<span data-ttu-id="365b1-124">Para configurar la integración de Atomic Learning en Azure AD, deberá agregar esta solución desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="365b1-124">To configure the integration of Atomic Learning into Azure AD, you need to add Atomic Learning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="365b1-125">**Para agregar Atomic Learning desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="365b1-125">**To add Atomic Learning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="365b1-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="365b1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="365b1-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="365b1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="365b1-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="365b1-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="365b1-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="365b1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="365b1-133">En el cuadro de búsqueda, escriba **Atomic Learning**.</span><span class="sxs-lookup"><span data-stu-id="365b1-133">In the search box, type **Atomic Learning**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_search.png)

5. <span data-ttu-id="365b1-135">En el panel de resultados, seleccione **Atomic Learning** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="365b1-135">In the results panel, select **Atomic Learning**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="365b1-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="365b1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="365b1-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Atomic Learning utilizando el usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="365b1-138">In this section, you configure and test Azure AD single sign-on with Atomic Learning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="365b1-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Atomic Learning para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="365b1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Atomic Learning is to a user in Azure AD.</span></span> <span data-ttu-id="365b1-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="365b1-140">In other words, a link relationship between an Azure AD user and the related user in Atomic Learning needs to be established.</span></span>

<span data-ttu-id="365b1-141">Para establecer la relación de vínculo, en Atomic Learning , asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="365b1-141">In Atomic Learning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="365b1-142">Para configurar y probar el inicio de sesión único de Azure AD con Atomic Learning, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="365b1-142">To configure and test Azure AD single sign-on with Atomic Learning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="365b1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="365b1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="365b1-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="365b1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="365b1-145">**[Creación de un usuario de prueba de Atomic Learning](#creating-an-atomic-learning-test-user)**: para tener un homólogo de Britta Simon en Atomic Learning que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="365b1-145">**[Creating an Atomic Learning test user](#creating-an-atomic-learning-test-user)** - to have a counterpart of Britta Simon in Atomic Learning that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="365b1-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="365b1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="365b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="365b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="365b1-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="365b1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="365b1-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="365b1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Atomic Learning application.</span></span>

<span data-ttu-id="365b1-150">**Para configurar el inicio de sesión único de Azure AD con Atomic Learning, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="365b1-150">**To configure Azure AD single sign-on with Atomic Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="365b1-151">En la página de integración de la aplicación **Atomic Learning** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="365b1-151">In the Azure portal, on the **Atomic Learning** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="365b1-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="365b1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_samlbase.png)

3. <span data-ttu-id="365b1-155">En la sección **Dominio y direcciones URL de Atomic Learning**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="365b1-155">On the **Atomic Learning Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_url.png)

     <span data-ttu-id="365b1-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="365b1-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="365b1-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="365b1-158">This value is not real.</span></span> <span data-ttu-id="365b1-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="365b1-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="365b1-160">Póngase en contacto con el [equipo de soporte al cliente de Atomic Learning](mailto:cs@atomiclearning.com) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="365b1-160">Contact [Atomic Learning Client support team](mailto:cs@atomiclearning.com) to get this value.</span></span> 
 
4. <span data-ttu-id="365b1-161">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="365b1-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_certificate.png) 

5. <span data-ttu-id="365b1-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="365b1-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="365b1-165">Para configurar el inicio de sesión único en el lado de **Atomic Learning**, es preciso enviar los datos descargados de **XML de metadatos** al [equipo de soporte técnico de Atomic Learning](mailto:cs@atomiclearning.com).</span><span class="sxs-lookup"><span data-stu-id="365b1-165">To configure single sign-on on **Atomic Learning** side, you need to send the downloaded **Metadata XML** to [Atomic Learning support team](mailto:cs@atomiclearning.com).</span></span> <span data-ttu-id="365b1-166">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="365b1-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="365b1-167">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="365b1-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="365b1-168">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="365b1-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="365b1-169">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="365b1-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="365b1-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="365b1-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="365b1-171">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="365b1-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="365b1-173">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="365b1-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="365b1-174">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="365b1-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="365b1-176">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="365b1-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="365b1-178">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="365b1-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="365b1-180">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="365b1-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="365b1-182">a.</span><span class="sxs-lookup"><span data-stu-id="365b1-182">a.</span></span> <span data-ttu-id="365b1-183">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="365b1-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="365b1-184">b.</span><span class="sxs-lookup"><span data-stu-id="365b1-184">b.</span></span> <span data-ttu-id="365b1-185">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="365b1-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="365b1-186">c.</span><span class="sxs-lookup"><span data-stu-id="365b1-186">c.</span></span> <span data-ttu-id="365b1-187">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="365b1-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="365b1-188">d.</span><span class="sxs-lookup"><span data-stu-id="365b1-188">d.</span></span> <span data-ttu-id="365b1-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="365b1-189">Click **Create**.</span></span>
 
### <a name="creating-an-atomic-learning-test-user"></a><span data-ttu-id="365b1-190">Creación de un usuario de prueba de Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="365b1-190">Creating an Atomic Learning test user</span></span>

<span data-ttu-id="365b1-191">En esta sección, creará un usuario llamado Britta Simon en Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="365b1-191">In this section, you create a user called Britta Simon in Atomic Learning.</span></span> <span data-ttu-id="365b1-192">Atomic Learning admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="365b1-192">Atomic Learning supports just-in-time provisioning, which is by default enabled.</span></span> 

<span data-ttu-id="365b1-193">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="365b1-193">There is no action item for you in this section.</span></span> <span data-ttu-id="365b1-194">Durante un intento de acceder a Atomic Learning se crea un nuevo usuario, si aún no existe, utilizando la dirección de correo electrónico de dicho usuario.</span><span class="sxs-lookup"><span data-stu-id="365b1-194">A new user is created during an attempt to access Atomic Learning if it doesn't exist yet using the email address for the user.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="365b1-195">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="365b1-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="365b1-196">En esta sección, permitirá que Britta Simon use el inicio de sesión único de Azure concediéndole acceso a Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="365b1-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Atomic Learning.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="365b1-198">**Para asignar Britta Simon a Atomic Learning, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="365b1-198">**To assign Britta Simon to Atomic Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="365b1-199">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="365b1-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="365b1-201">En la lista de aplicaciones, seleccione **Atomic Learning**.</span><span class="sxs-lookup"><span data-stu-id="365b1-201">In the applications list, select **Atomic Learning**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_app.png) 

3. <span data-ttu-id="365b1-203">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="365b1-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="365b1-205">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="365b1-205">Click **Add** button.</span></span> <span data-ttu-id="365b1-206">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="365b1-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="365b1-208">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="365b1-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="365b1-209">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="365b1-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="365b1-210">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="365b1-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="365b1-211">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="365b1-211">Testing single sign-on</span></span>

<span data-ttu-id="365b1-212">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="365b1-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="365b1-213">Al hacer clic en el icono de Atomic Learning del panel de acceso, debería iniciar sesión automáticamente en la aplicación Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="365b1-213">When you click the Atomic Learning tile in the Access Panel, you should get automatically signed-on to your Atomic Learning application.</span></span>
<span data-ttu-id="365b1-214">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="365b1-214">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="365b1-215">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="365b1-215">Additional resources</span></span>

* [<span data-ttu-id="365b1-216">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="365b1-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="365b1-217">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="365b1-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_203.png
