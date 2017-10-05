---
title: "Tutorial: Integración de Azure Active Directory con Huddle | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Huddle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 59d4019545d39ec76bf401696338140f430630c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="b2171-103">Tutorial: integración de Azure Active Directory con Huddle</span><span class="sxs-lookup"><span data-stu-id="b2171-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="b2171-104">En este tutorial, obtendrá información sobre cómo integrar Huddle con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b2171-104">In this tutorial, you learn how to integrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b2171-105">La integración de Huddle con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="b2171-105">Integrating Huddle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b2171-106">En Azure AD se puede controlar quién tiene acceso a Huddle</span><span class="sxs-lookup"><span data-stu-id="b2171-106">You can control in Azure AD who has access to Huddle</span></span>
- <span data-ttu-id="b2171-107">Puede permitir que los usuarios inicien sesión automáticamente en Huddle (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2171-107">You can enable your users to automatically get signed-on to Huddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b2171-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b2171-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b2171-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b2171-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2171-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b2171-110">Prerequisites</span></span>

<span data-ttu-id="b2171-111">Para configurar la integración de Azure AD con Huddle, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="b2171-111">To configure Azure AD integration with Huddle, you need the following items:</span></span>

- <span data-ttu-id="b2171-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2171-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b2171-113">Una suscripción habilitada para el inicio de sesión único en Huddle</span><span class="sxs-lookup"><span data-stu-id="b2171-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b2171-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="b2171-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b2171-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="b2171-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b2171-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b2171-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b2171-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b2171-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b2171-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="b2171-118">Scenario description</span></span>

<span data-ttu-id="b2171-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="b2171-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b2171-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="b2171-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b2171-121">Incorporación de Huddle desde la Galería</span><span class="sxs-lookup"><span data-stu-id="b2171-121">Adding Huddle from the gallery</span></span>
2. <span data-ttu-id="b2171-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2171-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-the-gallery"></a><span data-ttu-id="b2171-123">Incorporación de Huddle desde la Galería</span><span class="sxs-lookup"><span data-stu-id="b2171-123">Adding Huddle from the gallery</span></span>
<span data-ttu-id="b2171-124">Para configurar la integración de Huddle en Azure AD, deberá agregar Huddle desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="b2171-124">To configure the integration of Huddle into Azure AD, you need to add Huddle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b2171-125">**Para agregar Huddle desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b2171-125">**To add Huddle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b2171-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b2171-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b2171-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="b2171-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b2171-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b2171-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="b2171-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b2171-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="b2171-133">En el cuadro de búsqueda, escriba **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="b2171-133">In the search box, type **Huddle**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="b2171-135">En el panel de resultados, seleccione **Huddle** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b2171-135">In the results panel, select **Huddle**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b2171-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2171-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="b2171-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Huddle con un usuario de prueba llamado "Britta Simon"</span><span class="sxs-lookup"><span data-stu-id="b2171-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b2171-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Huddle para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b2171-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Huddle is to a user in Azure AD.</span></span> <span data-ttu-id="b2171-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Huddle.</span><span class="sxs-lookup"><span data-stu-id="b2171-140">In other words, a link relationship between an Azure AD user and the related user in Huddle needs to be established.</span></span>

<span data-ttu-id="b2171-141">Para establecer la relación de vínculo, en Huddle, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="b2171-141">In Huddle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b2171-142">Para configurar y probar el inicio de sesión único de Azure AD con Huddle, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="b2171-142">To configure and test Azure AD single sign-on with Huddle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b2171-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="b2171-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>

2. <span data-ttu-id="b2171-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b2171-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="b2171-145">**[Creación de un usuario de prueba de Huddle](#creating-a-huddle-test-user)**: para tener un homólogo de Britta Simon en Huddle que esté vinculado a la representación de Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="b2171-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - to have a counterpart of Britta Simon in Huddle that is linked to the Azure AD representation of user.</span></span>

4. <span data-ttu-id="b2171-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b2171-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>

5. <span data-ttu-id="b2171-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="b2171-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b2171-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2171-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b2171-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación de Huddle.</span><span class="sxs-lookup"><span data-stu-id="b2171-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="b2171-150">**Para configurar el inicio de sesión único de Azure AD con Huddle, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b2171-150">**To configure Azure AD single sign-on with Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="b2171-151">En Azure Portal, en la página de integración de la aplicación **Huddle**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="b2171-151">In the Azure portal, on the **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="b2171-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b2171-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="b2171-155">En la sección **Dominio y direcciones URL de Huddle**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b2171-155">On the **Huddle Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="b2171-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `http://<company name>.huddle.com`.</span><span class="sxs-lookup"><span data-stu-id="b2171-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<company name>.huddle.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b2171-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="b2171-158">This value is not real.</span></span> <span data-ttu-id="b2171-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="b2171-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="b2171-160">Póngase en contacto con el [equipo de soporte técnico de Huddle](https://huddle.zendesk.com) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="b2171-160">Contact [Huddle Client support team](https://huddle.zendesk.com) to get this value.</span></span> 

4. <span data-ttu-id="b2171-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b2171-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. <span data-ttu-id="b2171-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="b2171-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b2171-165">En la sección **Configuración de Huddle**, haga clic en **Configurar Huddle** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="b2171-165">On the **Huddle Configuration** section, click **Configure Huddle** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b2171-166">Copie los valores de **SAML Entity ID y SAML Single Sign-On Service URL** (Identificador de entidad de SAML y URL del servicio de inicio de sesión único de SAML) de la sección de **referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="b2171-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. <span data-ttu-id="b2171-168">Para configurar el inicio de sesión único en Huddle, es preciso enviar el **certificado** descargado, la **dirección URL de inicio de sesión único de SAML** y el **identificador de entidad de SAML** al [equipo de soporte técnico de Huddle](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="b2171-168">To configure single sign-on on Huddle side, you need to send the downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** to [Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="b2171-169">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="b2171-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="b2171-170">El inicio de sesión único debe habilitarlo el equipo de soporte técnico de Huddle.</span><span class="sxs-lookup"><span data-stu-id="b2171-170">Single sign-on needs to be enabled by the Huddle support team.</span></span> <span data-ttu-id="b2171-171">Cuando se haya completado la configuración, recibirá una notificación.</span><span class="sxs-lookup"><span data-stu-id="b2171-171">You get a notification when the configuration has been completed.</span></span> 
    > 

> [!TIP]
> <span data-ttu-id="b2171-172">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b2171-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b2171-173">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="b2171-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b2171-174">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b2171-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
   
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b2171-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2171-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="b2171-176">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b2171-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="b2171-178">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="b2171-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b2171-179">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b2171-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b2171-181">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="b2171-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b2171-183">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b2171-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b2171-185">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="b2171-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b2171-187">a.</span><span class="sxs-lookup"><span data-stu-id="b2171-187">a.</span></span> <span data-ttu-id="b2171-188">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b2171-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b2171-189">b.</span><span class="sxs-lookup"><span data-stu-id="b2171-189">b.</span></span> <span data-ttu-id="b2171-190">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b2171-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b2171-191">c.</span><span class="sxs-lookup"><span data-stu-id="b2171-191">c.</span></span> <span data-ttu-id="b2171-192">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="b2171-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b2171-193">d.</span><span class="sxs-lookup"><span data-stu-id="b2171-193">d.</span></span> <span data-ttu-id="b2171-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b2171-194">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="b2171-195">Creación de un usuario de prueba de Huddle</span><span class="sxs-lookup"><span data-stu-id="b2171-195">Creating a Huddle test user</span></span>

<span data-ttu-id="b2171-196">Para permitir que los usuarios de Azure AD inicien sesión en Huddle, deben aprovisionarse en Huddle.</span><span class="sxs-lookup"><span data-stu-id="b2171-196">To enable Azure AD users to log in to Huddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="b2171-197">En el caso de Huddle, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="b2171-197">In the case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="b2171-198">**Siga estos pasos para configurar el aprovisionamiento de usuario:**</span><span class="sxs-lookup"><span data-stu-id="b2171-198">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="b2171-199">Inicie sesión en el sitio de compañía de **Huddle** como administrador.</span><span class="sxs-lookup"><span data-stu-id="b2171-199">Log in to your **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="b2171-200">Haga clic en **Área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="b2171-200">Click **Workspace**.</span></span>
3. <span data-ttu-id="b2171-201">Haga clic en **Contactos\>Invitar a contactos**.</span><span class="sxs-lookup"><span data-stu-id="b2171-201">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="b2171-202">![Personas](./media/active-directory-saas-huddle-tutorial/IC787838.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="b2171-202">![People](./media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="b2171-203">En la sección **Crear nueva invitación** , lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="b2171-203">In the **Create a new invitation** section, perform the following steps:</span></span>
   
   <span data-ttu-id="b2171-204">![Nueva invitación](./media/active-directory-saas-huddle-tutorial/IC787839.png "Nueva invitación")</span><span class="sxs-lookup"><span data-stu-id="b2171-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   <span data-ttu-id="b2171-205">a.</span><span class="sxs-lookup"><span data-stu-id="b2171-205">a.</span></span> <span data-ttu-id="b2171-206">En la lista **Choose a team to invite people to join** (Elegir un equipo al que invitar a unirse a los contactos), seleccione **equipo**.</span><span class="sxs-lookup"><span data-stu-id="b2171-206">In the **Choose a team to invite people to join** list, select **team**.</span></span>

   <span data-ttu-id="b2171-207">b.</span><span class="sxs-lookup"><span data-stu-id="b2171-207">b.</span></span> <span data-ttu-id="b2171-208">Escriba la **dirección de correo electrónico** de una cuenta de Azure AD válida que desee aprovisionar en el cuadro de texto **Escriba la dirección de correo electrónico de las personas que desea invitar**.</span><span class="sxs-lookup"><span data-stu-id="b2171-208">Type the **Email Address** of a valid Azure AD account you want to provision in to **Enter email address for people you'd like to invite** textbox.</span></span>

   <span data-ttu-id="b2171-209">c.</span><span class="sxs-lookup"><span data-stu-id="b2171-209">c.</span></span> <span data-ttu-id="b2171-210">Haga clic en **Invitar**.</span><span class="sxs-lookup"><span data-stu-id="b2171-210">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="b2171-211">El titular de la cuenta de Azure AD recibirá un mensaje de correo electrónico con un vínculo para confirmar la cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="b2171-211">The Azure AD account holder will receive an email including a link to confirm the account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="b2171-212">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Huddle que proporcione Huddle para aprovisionar cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b2171-212">You can use any other Huddle user account creation tools or APIs provided by Huddle to provision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b2171-213">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2171-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b2171-214">En esta sección, concederá acceso a Britta Simon a Huddle para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="b2171-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Huddle.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="b2171-216">**Para asignar a Britta Simon a Huddle, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b2171-216">**To assign Britta Simon to Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="b2171-217">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b2171-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="b2171-219">En la lista de aplicaciones, seleccione **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="b2171-219">In the applications list, select **Huddle**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="b2171-221">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b2171-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="b2171-223">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b2171-223">Click **Add** button.</span></span> <span data-ttu-id="b2171-224">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b2171-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="b2171-226">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="b2171-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b2171-227">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b2171-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b2171-228">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b2171-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b2171-229">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="b2171-229">Testing single sign-on</span></span>

<span data-ttu-id="b2171-230">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="b2171-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b2171-231">Al hacer clic en el icono de Huddle en el panel de acceso, debería iniciar sesión automáticamente en su aplicación de Huddle.</span><span class="sxs-lookup"><span data-stu-id="b2171-231">When you click the Huddle tile in the Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="b2171-232">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b2171-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b2171-233">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b2171-233">Additional resources</span></span>

* [<span data-ttu-id="b2171-234">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b2171-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b2171-235">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b2171-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png
