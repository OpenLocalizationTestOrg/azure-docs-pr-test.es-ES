---
title: "Tutorial: integración de Azure Active Directory con Kudos | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Kudos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 353798fcfd4ad7ce017fc2fddf4110715db3ace2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="de59d-103">Tutorial: Integración de Azure Active Directory con Kudos</span><span class="sxs-lookup"><span data-stu-id="de59d-103">Tutorial: Azure Active Directory integration with Kudos</span></span>

<span data-ttu-id="de59d-104">En este tutorial, aprenderá a integrar Kudos con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="de59d-104">In this tutorial, you learn how to integrate Kudos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="de59d-105">La integración de Kudos con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="de59d-105">Integrating Kudos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="de59d-106">Puede controlar en Azure AD quién tiene acceso a Kudos.</span><span class="sxs-lookup"><span data-stu-id="de59d-106">You can control in Azure AD who has access to Kudos</span></span>
- <span data-ttu-id="de59d-107">Puede permitir que los usuarios inicien sesión automáticamente en Kudos (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de59d-107">You can enable your users to automatically get signed-on to Kudos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="de59d-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="de59d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="de59d-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="de59d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de59d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="de59d-110">Prerequisites</span></span>

<span data-ttu-id="de59d-111">Para configurar la integración de Azure AD con Kudos, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="de59d-111">To configure Azure AD integration with Kudos, you need the following items:</span></span>

- <span data-ttu-id="de59d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="de59d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="de59d-113">Una suscripción habilitada para el inicio de sesión único en Kudos</span><span class="sxs-lookup"><span data-stu-id="de59d-113">A Kudos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="de59d-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="de59d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="de59d-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="de59d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="de59d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="de59d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="de59d-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="de59d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="de59d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="de59d-118">Scenario description</span></span>
<span data-ttu-id="de59d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="de59d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="de59d-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="de59d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="de59d-121">Adición de Kudos desde la galería</span><span class="sxs-lookup"><span data-stu-id="de59d-121">Adding Kudos from the gallery</span></span>
2. <span data-ttu-id="de59d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="de59d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kudos-from-the-gallery"></a><span data-ttu-id="de59d-123">Adición de Kudos desde la galería</span><span class="sxs-lookup"><span data-stu-id="de59d-123">Adding Kudos from the gallery</span></span>
<span data-ttu-id="de59d-124">Para configurar la integración de Kudos en Azure AD, deberá agregar Kudos desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="de59d-124">To configure the integration of Kudos into Azure AD, you need to add Kudos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="de59d-125">**Para agregar Kudos desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="de59d-125">**To add Kudos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="de59d-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="de59d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="de59d-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="de59d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="de59d-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="de59d-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="de59d-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="de59d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="de59d-133">En el cuadro de búsqueda, escriba **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="de59d-133">In the search box, type **Kudos**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_search.png)

5. <span data-ttu-id="de59d-135">En el panel de resultados, seleccione **Kudos** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="de59d-135">In the results panel, select **Kudos**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="de59d-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="de59d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="de59d-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Kudos con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="de59d-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="de59d-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Kudos para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de59d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kudos is to a user in Azure AD.</span></span> <span data-ttu-id="de59d-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Kudos.</span><span class="sxs-lookup"><span data-stu-id="de59d-140">In other words, a link relationship between an Azure AD user and the related user in Kudos needs to be established.</span></span>

<span data-ttu-id="de59d-141">Para establecer la relación de vínculo, en Kudos, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="de59d-141">In Kudos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="de59d-142">Para configurar y probar el inicio de sesión único de Azure AD con Kudos, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="de59d-142">To configure and test Azure AD single sign-on with Kudos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="de59d-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="de59d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="de59d-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="de59d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="de59d-145">**[Creación de un usuario de prueba de Kudos](#creating-a-kudos-test-user)**: el objetivo es tener un homólogo de Britta Simon en Kudos que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de59d-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - to have a counterpart of Britta Simon in Kudos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="de59d-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de59d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="de59d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="de59d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="de59d-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="de59d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="de59d-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Kudos.</span><span class="sxs-lookup"><span data-stu-id="de59d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kudos application.</span></span>

<span data-ttu-id="de59d-150">**Para configurar el inicio de sesión único de Azure AD con Kudos, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="de59d-150">**To configure Azure AD single sign-on with Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="de59d-151">En la página de integración de la aplicación **Kudos** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="de59d-151">In the Azure portal, on the **Kudos** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="de59d-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="de59d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_samlbase.png)

3. <span data-ttu-id="de59d-155">En la sección **Dominio y direcciones URL de Kudos**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="de59d-155">On the **Kudos Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_url.png)

    <span data-ttu-id="de59d-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<company>.kudosnow.com`.</span><span class="sxs-lookup"><span data-stu-id="de59d-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.kudosnow.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="de59d-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="de59d-158">This value is not real.</span></span> <span data-ttu-id="de59d-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="de59d-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="de59d-160">Póngase en contacto con el [equipo de atención al cliente de Kudos](http://success.kudosnow.com/home) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="de59d-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) to get this value.</span></span> 
 
4. <span data-ttu-id="de59d-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="de59d-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_certificate.png) 

5. <span data-ttu-id="de59d-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="de59d-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kudos-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="de59d-165">En la sección **Configuración de Kudos**, haga clic en **Configurar Kudos** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="de59d-165">On the **Kudos Configuration** section, click **Configure Kudos** to open **Configure sign-on** window.</span></span> <span data-ttu-id="de59d-166">Copie las **direcciones URL del servicio de inicio de sesión único de SAML y de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="de59d-166">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_configure.png) 

7. <span data-ttu-id="de59d-168">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Kudos.</span><span class="sxs-lookup"><span data-stu-id="de59d-168">In a different web browser window, log into your Kudos company site as an administrator.</span></span>

8. <span data-ttu-id="de59d-169">En el menú de la parte superior, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="de59d-169">In the menu on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="de59d-170">![Configuración](./media/active-directory-saas-kudos-tutorial/ic787806.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="de59d-170">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

9. <span data-ttu-id="de59d-171">Haga clic en **Integrations \> SSO** (Integraciones > SSO).</span><span class="sxs-lookup"><span data-stu-id="de59d-171">Click **Integrations \> SSO**.</span></span>

10. <span data-ttu-id="de59d-172">En la sección **SSO** , siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="de59d-172">In the **SSO** section, perform the following steps:</span></span>
   
    <span data-ttu-id="de59d-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span><span class="sxs-lookup"><span data-stu-id="de59d-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span></span>
   
    <span data-ttu-id="de59d-174">a.</span><span class="sxs-lookup"><span data-stu-id="de59d-174">a.</span></span> <span data-ttu-id="de59d-175">En el cuadro de texto **Dirección URL de inicio de sesión**, pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="de59d-175">In **Sign on URL** textbox, paste the value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="de59d-176">b.</span><span class="sxs-lookup"><span data-stu-id="de59d-176">b.</span></span> <span data-ttu-id="de59d-177">Abra el certificado codificado en base 64 en el Bloc de notas, copie el contenido del mismo en el Portapapeles y luego péguelo en el cuadro de texto **Certificado X.509** .</span><span class="sxs-lookup"><span data-stu-id="de59d-177">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 certificate** textbox</span></span>
   
    <span data-ttu-id="de59d-178">c.</span><span class="sxs-lookup"><span data-stu-id="de59d-178">c.</span></span> <span data-ttu-id="de59d-179">En el cuadro de texto **Logout URL** (Dirección URL de cierre de sesión), pegue el valor de **Sign-Out URL** (URL de cierre de sesión) que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="de59d-179">In **Logout To URL**, paste the value of  **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="de59d-180">d.</span><span class="sxs-lookup"><span data-stu-id="de59d-180">d.</span></span> <span data-ttu-id="de59d-181">En el cuadro de texto **Su dirección URL de Kudos** , escriba el nombre de su compañía.</span><span class="sxs-lookup"><span data-stu-id="de59d-181">In the **Your Kudos URL** textbox, type your company name.</span></span>
   
    <span data-ttu-id="de59d-182">e.</span><span class="sxs-lookup"><span data-stu-id="de59d-182">e.</span></span> <span data-ttu-id="de59d-183">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="de59d-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="de59d-184">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="de59d-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="de59d-185">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="de59d-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="de59d-186">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="de59d-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="de59d-187">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="de59d-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="de59d-188">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="de59d-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="de59d-190">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="de59d-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="de59d-191">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="de59d-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="de59d-193">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="de59d-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="de59d-195">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="de59d-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="de59d-197">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="de59d-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="de59d-199">a.</span><span class="sxs-lookup"><span data-stu-id="de59d-199">a.</span></span> <span data-ttu-id="de59d-200">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="de59d-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="de59d-201">b.</span><span class="sxs-lookup"><span data-stu-id="de59d-201">b.</span></span> <span data-ttu-id="de59d-202">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="de59d-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="de59d-203">c.</span><span class="sxs-lookup"><span data-stu-id="de59d-203">c.</span></span> <span data-ttu-id="de59d-204">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="de59d-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="de59d-205">d.</span><span class="sxs-lookup"><span data-stu-id="de59d-205">d.</span></span> <span data-ttu-id="de59d-206">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="de59d-206">Click **Create**.</span></span>
 
### <a name="creating-a-kudos-test-user"></a><span data-ttu-id="de59d-207">Creación de un usuario de prueba de Kudos</span><span class="sxs-lookup"><span data-stu-id="de59d-207">Creating a Kudos test user</span></span>

<span data-ttu-id="de59d-208">Para permitir que los usuarios de Azure AD inicien sesión en Kudos, deben aprovisionarse en Kudos.</span><span class="sxs-lookup"><span data-stu-id="de59d-208">In order to enable Azure AD users to log into Kudos, they must be provisioned into Kudos.</span></span> 

<span data-ttu-id="de59d-209">En el caso de Kudos, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="de59d-209">In the case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="de59d-210">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="de59d-210">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="de59d-211">Inicie sesión como administrador en el sitio de la compañía de **Kudos** .</span><span class="sxs-lookup"><span data-stu-id="de59d-211">Log in to your **Kudos** company site as administrator.</span></span>

2. <span data-ttu-id="de59d-212">En el menú de la parte superior, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="de59d-212">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="de59d-213">![Configuración](./media/active-directory-saas-kudos-tutorial/ic787806.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="de59d-213">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

3. <span data-ttu-id="de59d-214">Haga clic en **Administrador de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="de59d-214">Click **User Admin**.</span></span>

4. <span data-ttu-id="de59d-215">Haga clic en la pestaña **Users** (Usuarios) y, a continuación, haga clic en **Add user** (Agregar un usuario).</span><span class="sxs-lookup"><span data-stu-id="de59d-215">Click the **Users** tab, and then click **Add a User**.</span></span>
   
   <span data-ttu-id="de59d-216">![Administración de usuarios](./media/active-directory-saas-kudos-tutorial/ic787809.png "Administración de usuarios")</span><span class="sxs-lookup"><span data-stu-id="de59d-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span></span>

5. <span data-ttu-id="de59d-217">En la sección **Agregar un usuario** , realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="de59d-217">In the **Add a User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="de59d-218">![Agregar un usuario](./media/active-directory-saas-kudos-tutorial/ic787810.png "Agregar un usuario")</span><span class="sxs-lookup"><span data-stu-id="de59d-218">![Add a User](./media/active-directory-saas-kudos-tutorial/ic787810.png "Add a User")</span></span>
   
    <span data-ttu-id="de59d-219">a.</span><span class="sxs-lookup"><span data-stu-id="de59d-219">a.</span></span> <span data-ttu-id="de59d-220">Escriba en los cuadros de texto correspondientes el **nombre**, los **apellidos**, el **correo electrónico** y otros detalles de la cuenta de Azure Active Directory válida que desee aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="de59d-220">Type the **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="de59d-221">b.</span><span class="sxs-lookup"><span data-stu-id="de59d-221">b.</span></span> <span data-ttu-id="de59d-222">Haga clic en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="de59d-222">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="de59d-223">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Kudos ofrecida por Kudos para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="de59d-223">You can use any other Kudos user account creation tools or APIs provided by Kudos to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="de59d-224">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="de59d-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="de59d-225">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Kudos.</span><span class="sxs-lookup"><span data-stu-id="de59d-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kudos.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="de59d-227">**Para asignar a Britta Simon a Kudos, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="de59d-227">**To assign Britta Simon to Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="de59d-228">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="de59d-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="de59d-230">En la lista de aplicaciones, seleccione **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="de59d-230">In the applications list, select **Kudos**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_app.png) 

3. <span data-ttu-id="de59d-232">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="de59d-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="de59d-234">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="de59d-234">Click **Add** button.</span></span> <span data-ttu-id="de59d-235">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="de59d-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="de59d-237">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="de59d-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="de59d-238">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="de59d-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="de59d-239">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="de59d-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="de59d-240">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="de59d-240">Testing single sign-on</span></span>

<span data-ttu-id="de59d-241">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="de59d-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="de59d-242">Al hacer clic en el icono de Kudos en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Kudos.</span><span class="sxs-lookup"><span data-stu-id="de59d-242">When you click the Kudos tile in the Access Panel, you should get automatically signed-on to your Kudos application.</span></span> <span data-ttu-id="de59d-243">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="de59d-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="de59d-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="de59d-244">Additional resources</span></span>

* [<span data-ttu-id="de59d-245">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="de59d-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="de59d-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="de59d-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_203.png

