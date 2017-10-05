---
title: "Tutorial: Integración de Azure Active Directory con HireVue | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y HireVue."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aadfc342-14db-4d74-a83d-f0c76f0cf63c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 682d88d3010f5781948a9adde0e1351471608a5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hirevue"></a><span data-ttu-id="3d856-103">Tutorial: Integración de Azure Active Directory con HireVue</span><span class="sxs-lookup"><span data-stu-id="3d856-103">Tutorial: Azure Active Directory integration with HireVue</span></span>

<span data-ttu-id="3d856-104">En este tutorial, obtendrá información sobre cómo integrar HireVue con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3d856-104">In this tutorial, you learn how to integrate HireVue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3d856-105">Integrar HireVue con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3d856-105">Integrating HireVue with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3d856-106">Puede controlar en Azure AD quién tiene acceso a HireVue.</span><span class="sxs-lookup"><span data-stu-id="3d856-106">You can control in Azure AD who has access to HireVue</span></span>
- <span data-ttu-id="3d856-107">Puede permitir que los usuarios inicien sesión automáticamente en HireVue (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d856-107">You can enable your users to automatically get signed-on to HireVue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3d856-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3d856-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3d856-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3d856-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d856-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3d856-110">Prerequisites</span></span>

<span data-ttu-id="3d856-111">Para configurar la integración de Azure AD con HireVue, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3d856-111">To configure Azure AD integration with HireVue, you need the following items:</span></span>

- <span data-ttu-id="3d856-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d856-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3d856-113">Una suscripción habilitada para inicio de sesión único en HireVue</span><span class="sxs-lookup"><span data-stu-id="3d856-113">A HireVue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3d856-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3d856-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3d856-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3d856-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3d856-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3d856-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3d856-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d856-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3d856-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3d856-118">Scenario description</span></span>
<span data-ttu-id="3d856-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3d856-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3d856-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="3d856-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3d856-121">Adición de HireVue desde la galería</span><span class="sxs-lookup"><span data-stu-id="3d856-121">Adding HireVue from the gallery</span></span>
2. <span data-ttu-id="3d856-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d856-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hirevue-from-the-gallery"></a><span data-ttu-id="3d856-123">Adición de HireVue desde la galería</span><span class="sxs-lookup"><span data-stu-id="3d856-123">Adding HireVue from the gallery</span></span>
<span data-ttu-id="3d856-124">Para configurar la integración de HireVue en Azure AD, deberá agregar HireVue desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="3d856-124">To configure the integration of HireVue into Azure AD, you need to add HireVue from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3d856-125">**Para agregar HireVue desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3d856-125">**To add HireVue from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3d856-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3d856-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3d856-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3d856-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3d856-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3d856-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="3d856-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3d856-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="3d856-133">En el cuadro de búsqueda, escriba **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="3d856-133">In the search box, type **HireVue**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_search.png)

5. <span data-ttu-id="3d856-135">En el panel de resultados, seleccione **HireVue** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3d856-135">In the results panel, select **HireVue**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3d856-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d856-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3d856-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con HireVue con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3d856-138">In this section, you configure and test Azure AD single sign-on with HireVue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3d856-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de HireVue para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d856-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HireVue is to a user in Azure AD.</span></span> <span data-ttu-id="3d856-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de HireVue.</span><span class="sxs-lookup"><span data-stu-id="3d856-140">In other words, a link relationship between an Azure AD user and the related user in HireVue needs to be established.</span></span>

<span data-ttu-id="3d856-141">Para establecer la relación de vínculo, en HireVue, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="3d856-141">In HireVue, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3d856-142">Para configurar y probar el inicio de sesión único de Azure AD con HireVue, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3d856-142">To configure and test Azure AD single sign-on with HireVue, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3d856-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="3d856-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3d856-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d856-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3d856-145">**[Creación de un usuario de prueba de HireVue](#creating-a-hirevue-test-user)**: para tener un homólogo de Britta Simon en HireVue que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d856-145">**[Creating a HireVue test user](#creating-a-hirevue-test-user)** - to have a counterpart of Britta Simon in HireVue that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3d856-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d856-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3d856-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3d856-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3d856-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d856-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3d856-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación HireVue.</span><span class="sxs-lookup"><span data-stu-id="3d856-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HireVue application.</span></span>

<span data-ttu-id="3d856-150">**Para configurar el inicio de sesión único de Azure AD con HireVue, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3d856-150">**To configure Azure AD single sign-on with HireVue, perform the following steps:**</span></span>

1. <span data-ttu-id="3d856-151">En Azure Portal, en la página de integración de la aplicación **HireVue**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3d856-151">In the Azure portal, on the **HireVue** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="3d856-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3d856-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_samlbase.png)

3. <span data-ttu-id="3d856-155">En la sección **Dominio y direcciones URL de HireVue**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3d856-155">On the **HireVue Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_url.png)

    <span data-ttu-id="3d856-157">a.</span><span class="sxs-lookup"><span data-stu-id="3d856-157">a.</span></span> <span data-ttu-id="3d856-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="3d856-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>

    | <span data-ttu-id="3d856-159">Environment</span><span class="sxs-lookup"><span data-stu-id="3d856-159">Environment</span></span> | <span data-ttu-id="3d856-160">URL</span><span class="sxs-lookup"><span data-stu-id="3d856-160">URL</span></span> |
    |-------------|---|
    | <span data-ttu-id="3d856-161">Producción</span><span class="sxs-lookup"><span data-stu-id="3d856-161">Production</span></span> | `https://<companyname>.hirevue.com` |
    | <span data-ttu-id="3d856-162">Ensayo</span><span class="sxs-lookup"><span data-stu-id="3d856-162">Staging</span></span>    | `https://<companyname>.stghv.com` |
    
    <span data-ttu-id="3d856-163">b.</span><span class="sxs-lookup"><span data-stu-id="3d856-163">b.</span></span> <span data-ttu-id="3d856-164">En el cuadro de texto **Identificador**, escriba una dirección URL como:</span><span class="sxs-lookup"><span data-stu-id="3d856-164">In the **Identifier** textbox, type a URL as:</span></span>
    
    | <span data-ttu-id="3d856-165">Environment</span><span class="sxs-lookup"><span data-stu-id="3d856-165">Environment</span></span> | <span data-ttu-id="3d856-166">URN</span><span class="sxs-lookup"><span data-stu-id="3d856-166">URN</span></span> |
    |-------------|-----|
    | <span data-ttu-id="3d856-167">Producción</span><span class="sxs-lookup"><span data-stu-id="3d856-167">Production</span></span> |`urn:federation:hirevue.com:saml:sp:prod` |
    | <span data-ttu-id="3d856-168">Ensayo</span><span class="sxs-lookup"><span data-stu-id="3d856-168">Staging</span></span>    | `urn:federation:hirevue.com:saml:sp:staging`|
    
    > [!NOTE] 
    > <span data-ttu-id="3d856-169">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="3d856-169">These values are not real.</span></span> <span data-ttu-id="3d856-170">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="3d856-170">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3d856-171">Para obtener estos valores, póngase en contacto con el [equipo de soporte técnico de clientes de HireVue](mailto:samlsupport@hirevue.com).</span><span class="sxs-lookup"><span data-stu-id="3d856-171">Contact [HireVue Client support team](mailto:samlsupport@hirevue.com) to get these values.</span></span> 
 
4. <span data-ttu-id="3d856-172">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3d856-172">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_certificate.png) 

5. <span data-ttu-id="3d856-174">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3d856-174">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hirevue-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3d856-176">En la sección **Configuración de HireVue**, haga clic en **Configurar HireVue** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="3d856-176">On the **HireVue Configuration** section, click **Configure HireVue** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3d856-177">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="3d856-177">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_configure.png) 

7. <span data-ttu-id="3d856-179">Para configurar el inicio de sesión único en **HireVue**, es preciso enviar el **Certificado (Base64)** descargado, la **dirección URL de cierre de sesión, el identificador de identidad de SAML y la dirección URL del servicio de inicio de sesión único de SAML** al [equipo de soporte técnico de HireVue](mailto:samlsupport@hirevue.com).</span><span class="sxs-lookup"><span data-stu-id="3d856-179">To configure single sign-on on **HireVue** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [HireVue support team](mailto:samlsupport@hirevue.com).</span></span> <span data-ttu-id="3d856-180">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="3d856-180">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3d856-181">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3d856-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3d856-182">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3d856-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3d856-183">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3d856-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3d856-184">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d856-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="3d856-185">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3d856-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="3d856-187">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="3d856-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3d856-188">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3d856-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3d856-190">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3d856-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3d856-192">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3d856-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3d856-194">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="3d856-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3d856-196">a.</span><span class="sxs-lookup"><span data-stu-id="3d856-196">a.</span></span> <span data-ttu-id="3d856-197">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3d856-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3d856-198">b.</span><span class="sxs-lookup"><span data-stu-id="3d856-198">b.</span></span> <span data-ttu-id="3d856-199">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d856-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3d856-200">c.</span><span class="sxs-lookup"><span data-stu-id="3d856-200">c.</span></span> <span data-ttu-id="3d856-201">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3d856-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3d856-202">d.</span><span class="sxs-lookup"><span data-stu-id="3d856-202">d.</span></span> <span data-ttu-id="3d856-203">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3d856-203">Click **Create**.</span></span>
 
### <a name="creating-a-hirevue-test-user"></a><span data-ttu-id="3d856-204">Creación de un usuario de prueba de HireVue</span><span class="sxs-lookup"><span data-stu-id="3d856-204">Creating a HireVue test user</span></span>

<span data-ttu-id="3d856-205">En esta sección, creará un usuario llamado Britta Simon en HireVue.</span><span class="sxs-lookup"><span data-stu-id="3d856-205">In this section, you create a user called Britta Simon in HireVue.</span></span> <span data-ttu-id="3d856-206">Trabaje con el [equipo de soporte técnico de HireVue](mailto:samlsupport@hirevue.com) para agregar los usuarios a la plataforma de HireVue.</span><span class="sxs-lookup"><span data-stu-id="3d856-206">Please work with [HireVue support team](mailto:samlsupport@hirevue.com) to add the users in the HireVue platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3d856-207">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d856-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3d856-208">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediendo acceso a HireVue.</span><span class="sxs-lookup"><span data-stu-id="3d856-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HireVue.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3d856-210">**Para asignar a Britta Simon a HireVue, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3d856-210">**To assign Britta Simon to HireVue, perform the following steps:**</span></span>

1. <span data-ttu-id="3d856-211">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3d856-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3d856-213">En la lista de aplicaciones, seleccione **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="3d856-213">In the applications list, select **HireVue**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_app.png) 

3. <span data-ttu-id="3d856-215">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3d856-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3d856-217">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3d856-217">Click **Add** button.</span></span> <span data-ttu-id="3d856-218">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3d856-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3d856-220">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="3d856-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3d856-221">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3d856-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3d856-222">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3d856-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3d856-223">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3d856-223">Testing single sign-on</span></span>

<span data-ttu-id="3d856-224">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3d856-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3d856-225">Al hacer clic en el icono de HireVue en el panel de acceso, debería iniciar sesión automáticamente en su aplicación HireVue.</span><span class="sxs-lookup"><span data-stu-id="3d856-225">When you click the HireVue tile in the Access Panel, you should get automatically signed-on to your HireVue application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3d856-226">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3d856-226">Additional resources</span></span>

* [<span data-ttu-id="3d856-227">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3d856-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3d856-228">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3d856-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_203.png

