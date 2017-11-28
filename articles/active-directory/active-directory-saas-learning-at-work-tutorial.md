---
title: "Tutorial: Integración de Azure Active Directory con Learning at Work | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Learning at Work."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d607174-bea1-4f40-8233-54cabe02c66a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: 941832740689c583a8e857d706c35f3076fa754f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-at-work"></a><span data-ttu-id="e943b-103">Tutorial: integración de Azure Active Directory con Learning at Work</span><span class="sxs-lookup"><span data-stu-id="e943b-103">Tutorial: Azure Active Directory integration with Learning at Work</span></span>

<span data-ttu-id="e943b-104">En este tutorial, obtendrá información sobre cómo integrar Learning at Work con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e943b-104">In this tutorial, you learn how to integrate Learning at Work with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e943b-105">La integración de Learning at Work con Azure AD ofrece las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e943b-105">Integrating Learning at Work with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e943b-106">Puede controlar en Azure AD quién tiene acceso a Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="e943b-106">You can control in Azure AD who has access to Learning at Work</span></span>
- <span data-ttu-id="e943b-107">Puede permitir que los usuarios inicien sesión automáticamente en Learning at Work (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e943b-107">You can enable your users to automatically get signed-on to Learning at Work (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e943b-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e943b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e943b-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e943b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e943b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e943b-110">Prerequisites</span></span>

<span data-ttu-id="e943b-111">Para configurar la integración de Azure AD con Learning at Work, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e943b-111">To configure Azure AD integration with Learning at Work, you need the following items:</span></span>

- <span data-ttu-id="e943b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e943b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e943b-113">Una suscripción habilitada para el inicio de sesión único en Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="e943b-113">A Learning at Work single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e943b-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e943b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e943b-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e943b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e943b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e943b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e943b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e943b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e943b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e943b-118">Scenario description</span></span>
<span data-ttu-id="e943b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e943b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e943b-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="e943b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e943b-121">Adición de Learning at Work desde la galería</span><span class="sxs-lookup"><span data-stu-id="e943b-121">Adding Learning at Work from the gallery</span></span>
2. <span data-ttu-id="e943b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e943b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-at-work-from-the-gallery"></a><span data-ttu-id="e943b-123">Adición de Learning at Work desde la galería</span><span class="sxs-lookup"><span data-stu-id="e943b-123">Adding Learning at Work from the gallery</span></span>
<span data-ttu-id="e943b-124">Para configurar la integración de Learning at Work en Azure AD, deberá agregar Learning at Work desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="e943b-124">To configure the integration of Learning at Work into Azure AD, you need to add Learning at Work from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e943b-125">**Para agregar Learning at Work desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e943b-125">**To add Learning at Work from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e943b-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e943b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e943b-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e943b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e943b-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e943b-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e943b-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e943b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e943b-133">En el cuadro de búsqueda, escriba **Learning at Work**.</span><span class="sxs-lookup"><span data-stu-id="e943b-133">In the search box, type **Learning at Work**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_search.png)

5. <span data-ttu-id="e943b-135">En el panel de resultados, seleccione **Learning at Work** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e943b-135">In the results panel, select **Learning at Work**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e943b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e943b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e943b-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Learning at Work con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e943b-138">In this section, you configure and test Azure AD single sign-on with Learning at Work based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e943b-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Learning at Work para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e943b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learning at Work is to a user in Azure AD.</span></span> <span data-ttu-id="e943b-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="e943b-140">In other words, a link relationship between an Azure AD user and the related user in Learning at Work needs to be established.</span></span>

<span data-ttu-id="e943b-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor de **Username** en Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="e943b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Learning at Work.</span></span>

<span data-ttu-id="e943b-142">Para configurar y probar el inicio de sesión único de Azure AD con Learning at Work, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e943b-142">To configure and test Azure AD single sign-on with Learning at Work, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e943b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="e943b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e943b-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e943b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e943b-145">**[Creación de un usuario de prueba de Learning at Work](#creating-a-learning-at-work-test-user)**: el objetivo es tener un homólogo de Britta Simon en Learning at Work que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e943b-145">**[Creating a Learning at Work test user](#creating-a-learning-at-work-test-user)** - to have a counterpart of Britta Simon in Learning at Work that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e943b-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e943b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e943b-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e943b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e943b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e943b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e943b-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="e943b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learning at Work application.</span></span>

<span data-ttu-id="e943b-150">**Para configurar el inicio de sesión único de Azure AD con Learning at Work, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e943b-150">**To configure Azure AD single sign-on with Learning at Work, perform the following steps:**</span></span>

1. <span data-ttu-id="e943b-151">En la página de integración de la aplicación **Learning at Work** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e943b-151">In the Azure portal, on the **Learning at Work** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e943b-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e943b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_samlbase.png)

3. <span data-ttu-id="e943b-155">En la sección **Dominios y direcciones URL de Learning at Work**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e943b-155">On the **Learning at Work Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_url.png)

    <span data-ttu-id="e943b-157">a.</span><span class="sxs-lookup"><span data-stu-id="e943b-157">a.</span></span> <span data-ttu-id="e943b-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.sabacloud.com/Saba/Web/<company code>`.</span><span class="sxs-lookup"><span data-stu-id="e943b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span></span>

    <span data-ttu-id="e943b-159">b.</span><span class="sxs-lookup"><span data-stu-id="e943b-159">b.</span></span> <span data-ttu-id="e943b-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span><span class="sxs-lookup"><span data-stu-id="e943b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e943b-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="e943b-161">These values are not the real.</span></span> <span data-ttu-id="e943b-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="e943b-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e943b-163">Póngase en contacto con el [equipo de atención al cliente de Learning at Work](https://www.learninga-z.com/site/contact/support) obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="e943b-163">Contact [Learning at Work Client support team](https://www.learninga-z.com/site/contact/support) to get these values.</span></span> 
 
4. <span data-ttu-id="e943b-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e943b-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_certificate.png) 

5. <span data-ttu-id="e943b-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e943b-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e943b-168">En la sección **Configuración de Learning at Work**, haga clic en **Configurar Learning at Work** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="e943b-168">On the **Learning at Work Configuration** section, click **Configure Learning at Work** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e943b-169">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="e943b-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_configure.png) 

7. <span data-ttu-id="e943b-171">Para configurar el inicio de sesión único en **Learning at Work**, debe enviar el **XML de metadatos** descargado, el **id. de entidad de SAML**, la **dirección URL del servicio de inicio de sesión único de SAML** y la **URL de cierre de sesión** al [soporte técnico de Learning at Work](https://www.learninga-z.com/site/contact/support).</span><span class="sxs-lookup"><span data-stu-id="e943b-171">To configure single sign-on on **Learning at Work** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL**, and **Sign-Out URL** to [Learning at Work support](https://www.learninga-z.com/site/contact/support).</span></span>

> [!TIP]
> <span data-ttu-id="e943b-172">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e943b-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e943b-173">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e943b-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e943b-174">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e943b-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e943b-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e943b-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="e943b-176">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e943b-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="e943b-178">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="e943b-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e943b-179">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e943b-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e943b-181">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e943b-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e943b-183">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e943b-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e943b-185">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="e943b-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e943b-187">a.</span><span class="sxs-lookup"><span data-stu-id="e943b-187">a.</span></span> <span data-ttu-id="e943b-188">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e943b-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e943b-189">b.</span><span class="sxs-lookup"><span data-stu-id="e943b-189">b.</span></span> <span data-ttu-id="e943b-190">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e943b-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e943b-191">c.</span><span class="sxs-lookup"><span data-stu-id="e943b-191">c.</span></span> <span data-ttu-id="e943b-192">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e943b-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e943b-193">d.</span><span class="sxs-lookup"><span data-stu-id="e943b-193">d.</span></span> <span data-ttu-id="e943b-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e943b-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-at-work-test-user"></a><span data-ttu-id="e943b-195">Creación de un usuario de prueba de Learning at Work</span><span class="sxs-lookup"><span data-stu-id="e943b-195">Creating a Learning at Work test user</span></span>

<span data-ttu-id="e943b-196">En esta sección, creará un usuario llamado Britta Simon en Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="e943b-196">In this section, you create a user called Britta Simon in Learning at Work.</span></span> <span data-ttu-id="e943b-197">Trabaje con el [equipo de soporte técnico de Learning at Work](https://www.learninga-z.com/site/contact/support) para agregar a los usuarios a la plataforma Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="e943b-197">Work with [Learning at Work support](https://www.learninga-z.com/site/contact/support) to add the users in the Learning at Work platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e943b-198">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e943b-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e943b-199">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="e943b-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learning at Work.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="e943b-201">**Para asignar Britta Simon a Learning at Work, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e943b-201">**To assign Britta Simon to Learning at Work, perform the following steps:**</span></span>

1. <span data-ttu-id="e943b-202">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e943b-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e943b-204">En la lista de aplicaciones, seleccione **Learning at Work**.</span><span class="sxs-lookup"><span data-stu-id="e943b-204">In the applications list, select **Learning at Work**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_app.png) 

3. <span data-ttu-id="e943b-206">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e943b-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="e943b-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e943b-208">Click **Add** button.</span></span> <span data-ttu-id="e943b-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e943b-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="e943b-211">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="e943b-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e943b-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e943b-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e943b-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e943b-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e943b-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="e943b-214">Testing single sign-on</span></span>

<span data-ttu-id="e943b-215">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e943b-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e943b-216">Al hacer clic en el icono de Learning at Work en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="e943b-216">When you click the Learning at Work tile in the Access Panel, you should get automatically signed-on to your Learning at Work application.</span></span>
<span data-ttu-id="e943b-217">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e943b-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e943b-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e943b-218">Additional resources</span></span>

* [<span data-ttu-id="e943b-219">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e943b-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e943b-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e943b-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_203.png

