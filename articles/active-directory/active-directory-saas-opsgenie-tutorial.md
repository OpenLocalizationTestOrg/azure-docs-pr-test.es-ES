---
title: "Tutorial: Integración de Azure Active Directory con OpsGenie | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y OpsGenie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: ce63726d2406d2f1415d29786f0ef92ca95b9b90
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a><span data-ttu-id="f6604-103">Tutorial: Integración de Azure Active Directory con OpsGenie</span><span class="sxs-lookup"><span data-stu-id="f6604-103">Tutorial: Azure Active Directory integration with OpsGenie</span></span>

<span data-ttu-id="f6604-104">En este tutorial, aprenderá a integrar Pluralsight con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f6604-104">In this tutorial, you learn how to integrate OpsGenie with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f6604-105">La integración de OpsGenie con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="f6604-105">Integrating OpsGenie with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f6604-106">Puede controlar en Azure AD quién tiene acceso a OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="f6604-106">You can control in Azure AD who has access to OpsGenie</span></span>
- <span data-ttu-id="f6604-107">Puede permitir que los usuarios inicien sesión automáticamente en OpsGenie (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6604-107">You can enable your users to automatically get signed-on to OpsGenie (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f6604-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f6604-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f6604-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f6604-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6604-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f6604-110">Prerequisites</span></span>

<span data-ttu-id="f6604-111">Para configurar la integración de Azure AD con OpsGenie, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f6604-111">To configure Azure AD integration with OpsGenie, you need the following items:</span></span>

- <span data-ttu-id="f6604-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6604-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f6604-113">Una suscripción habilitada para inicio de sesión único en Pluralsight</span><span class="sxs-lookup"><span data-stu-id="f6604-113">A OpsGenie single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f6604-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="f6604-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f6604-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="f6604-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f6604-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f6604-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f6604-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f6604-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f6604-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="f6604-118">Scenario description</span></span>
<span data-ttu-id="f6604-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="f6604-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f6604-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="f6604-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f6604-121">Adición de OpsGenie desde la galería</span><span class="sxs-lookup"><span data-stu-id="f6604-121">Adding OpsGenie from the gallery</span></span>
2. <span data-ttu-id="f6604-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6604-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-opsgenie-from-the-gallery"></a><span data-ttu-id="f6604-123">Adición de OpsGenie desde la galería</span><span class="sxs-lookup"><span data-stu-id="f6604-123">Adding OpsGenie from the gallery</span></span>
<span data-ttu-id="f6604-124">Para configurar la integración de OpsGenie en Azure AD, deberá agregar OpsGenie desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="f6604-124">To configure the integration of OpsGenie into Azure AD, you need to add OpsGenie from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f6604-125">**Para agregar OpsGenie desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f6604-125">**To add OpsGenie from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f6604-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f6604-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f6604-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="f6604-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f6604-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f6604-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="f6604-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f6604-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="f6604-133">En el cuadro de búsqueda, escriba **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="f6604-133">In the search box, type **OpsGenie**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_search.png)

5. <span data-ttu-id="f6604-135">En el panel de resultados, seleccione **OpsGenie** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f6604-135">In the results panel, select **OpsGenie**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f6604-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6604-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f6604-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con OpsGenie con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f6604-138">In this section, you configure and test Azure AD single sign-on with OpsGenie based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f6604-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de OpsGenie para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6604-139">For single sign-on to work, Azure AD needs to know what the counterpart user in OpsGenie is to a user in Azure AD.</span></span> <span data-ttu-id="f6604-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="f6604-140">In other words, a link relationship between an Azure AD user and the related user in OpsGenie needs to be established.</span></span>

<span data-ttu-id="f6604-141">Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario** de OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="f6604-141">In OpsGenie, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f6604-142">Para configurar y probar el inicio de sesión único de Azure AD con OpsGenie, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="f6604-142">To configure and test Azure AD single sign-on with OpsGenie, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f6604-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="f6604-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f6604-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f6604-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f6604-145">**[Creación de un usuario de prueba de OpsGenie](#creating-a-opsgenie-test-user)**: el objetivo es tener un homólogo de Britta Simon en OpsGenie que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6604-145">**[Creating a OpsGenie test user](#creating-a-opsgenie-test-user)** - to have a counterpart of Britta Simon in OpsGenie that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f6604-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6604-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f6604-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="f6604-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f6604-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6604-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f6604-149">En esta sección, habilitará el inicio de sesión único de Azure AD en el portal de Azure y lo configurará en la aplicación OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="f6604-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OpsGenie application.</span></span>

<span data-ttu-id="f6604-150">**Para configurar el inicio de sesión único de Azure AD con OpsGenie, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f6604-150">**To configure Azure AD single sign-on with OpsGenie, perform the following steps:**</span></span>

1. <span data-ttu-id="f6604-151">En la página de integración de la aplicación **OpsGenie** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f6604-151">In the Azure portal, on the **OpsGenie** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="f6604-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f6604-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

3. <span data-ttu-id="f6604-155">En la sección **Dominio y direcciones URL de OpsGenie**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f6604-155">On the **OpsGenie Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_url.png)

    <span data-ttu-id="f6604-157">En el cuadro de texto **URL de inicio de sesión**, escriba la dirección URL: `https://app.opsgenie.com/auth/login`</span><span class="sxs-lookup"><span data-stu-id="f6604-157">In the **Sign-on URL** textbox, type the URL: `https://app.opsgenie.com/auth/login`</span></span>

4. <span data-ttu-id="f6604-158">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f6604-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_certificate.png) 

5. <span data-ttu-id="f6604-160">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="f6604-160">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-opsgenie-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f6604-162">En la sección **Configuración de OpsGenie**, haga clic en **Configurar OpsGenie** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="f6604-162">On the **OpsGenie Configuration** section, click **Configure OpsGenie** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f6604-163">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="f6604-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_configure.png) 

7. <span data-ttu-id="f6604-165">Abra otra instancia del explorador y después inicie sesión en OpsGenie como administrador.</span><span class="sxs-lookup"><span data-stu-id="f6604-165">Open another browser instance, and then log-in to OpsGenie as an administrator.</span></span>

8. <span data-ttu-id="f6604-166">Haga clic en **Configuración** y después en la pestaña **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f6604-166">Click **Settings**, and then click the **Single Sign On** tab.</span></span>
   
    ![Inicio de sesión único de OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_06.png)

9. <span data-ttu-id="f6604-168">Para habilitar SSO, seleccione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="f6604-168">To enable SSO, select **Enabled**.</span></span>
   
    ![Configuración de OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_07.png) 

10. <span data-ttu-id="f6604-170">En la sección **Proveedor**, haga clic en la pestaña **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f6604-170">In the **Provider** section, click the **Azure Active Directory** tab.</span></span>
   
    ![Configuración de OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_08.png) 

11. <span data-ttu-id="f6604-172">En la página de diálogo de Azure Active Directory, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="f6604-172">On the Azure Active Directory dialog page, perform the following steps:</span></span>
   
    ![Configuración de OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    <span data-ttu-id="f6604-174">a.</span><span class="sxs-lookup"><span data-stu-id="f6604-174">a.</span></span> <span data-ttu-id="f6604-175">Pegue la **dirección URL del servicio de inicio de sesión** que ha copiado de Azure Portal en el cuadro de texto **SAML 2.0 Endpoint** (Punto de conexión de SAML 2.0).</span><span class="sxs-lookup"><span data-stu-id="f6604-175">Paste **Single Sign On Service URL**, which you have copied from the Azure portal into the **SAML 2.0 Endpoint** textbox.</span></span>
    
    <span data-ttu-id="f6604-176">b.</span><span class="sxs-lookup"><span data-stu-id="f6604-176">b.</span></span> <span data-ttu-id="f6604-177">Abra el certificado codificado en base 64 descargado en el Bloc de notas, copie su contenido en el Portapapeles y, a continuación, péguelo en el cuadro de texto **Certificado X.500**.</span><span class="sxs-lookup"><span data-stu-id="f6604-177">Open your downloaded base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **X.500 Certificate** textbox.</span></span>
    
    <span data-ttu-id="f6604-178">c.</span><span class="sxs-lookup"><span data-stu-id="f6604-178">c.</span></span> <span data-ttu-id="f6604-179">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="f6604-179">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="f6604-180">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f6604-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f6604-181">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="f6604-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f6604-182">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f6604-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f6604-183">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6604-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="f6604-184">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f6604-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="f6604-186">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="f6604-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f6604-187">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f6604-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f6604-189">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f6604-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f6604-191">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f6604-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f6604-193">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="f6604-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f6604-195">a.</span><span class="sxs-lookup"><span data-stu-id="f6604-195">a.</span></span> <span data-ttu-id="f6604-196">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f6604-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f6604-197">b.</span><span class="sxs-lookup"><span data-stu-id="f6604-197">b.</span></span> <span data-ttu-id="f6604-198">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f6604-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f6604-199">c.</span><span class="sxs-lookup"><span data-stu-id="f6604-199">c.</span></span> <span data-ttu-id="f6604-200">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="f6604-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f6604-201">d.</span><span class="sxs-lookup"><span data-stu-id="f6604-201">d.</span></span> <span data-ttu-id="f6604-202">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f6604-202">Click **Create**.</span></span>
 
### <a name="creating-a-opsgenie-test-user"></a><span data-ttu-id="f6604-203">Creación de un usuario de prueba de OpsGenie</span><span class="sxs-lookup"><span data-stu-id="f6604-203">Creating a OpsGenie test user</span></span>

<span data-ttu-id="f6604-204">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="f6604-204">The objective of this section is to create a user called Britta Simon in OpsGenie.</span></span> 

1. <span data-ttu-id="f6604-205">En una ventana del explorador web, inicie sesión en el inquilino de OpsGenie como administrador.</span><span class="sxs-lookup"><span data-stu-id="f6604-205">In a web browser window, log into your OpsGenie tenant as an administrator.</span></span>

2. <span data-ttu-id="f6604-206">Vaya a la lista Usuarios haciendo clic en **Usuario** en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="f6604-206">Navigate to Users list by clicking **User** in left panel.</span></span>
   
   ![Configuración de OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_10.png) 

3. <span data-ttu-id="f6604-208">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="f6604-208">Click **Add User**.</span></span>

4. <span data-ttu-id="f6604-209">En el cuadro de diálogo **Agregar usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f6604-209">On the **Add User** dialog, perform the following steps:</span></span>
   
   ![Configuración de OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   <span data-ttu-id="f6604-211">a.</span><span class="sxs-lookup"><span data-stu-id="f6604-211">a.</span></span> <span data-ttu-id="f6604-212">En el cuadro de texto **Email** (Correo electrónico), escriba la dirección de correo electrónico de BrittaSimon en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6604-212">In the **Email** textbox, type the email address of BrittaSimon addressed in Azure Active Directory.</span></span>
   
   <span data-ttu-id="f6604-213">b.</span><span class="sxs-lookup"><span data-stu-id="f6604-213">b.</span></span> <span data-ttu-id="f6604-214">En el cuadro de texto **Nombre completo**, escriba **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f6604-214">In the **Full Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="f6604-215">c.</span><span class="sxs-lookup"><span data-stu-id="f6604-215">c.</span></span> <span data-ttu-id="f6604-216">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f6604-216">Click **Save**.</span></span> 

>[!NOTE]
><span data-ttu-id="f6604-217">Britta recibirá un correo electrónico con instrucciones sobre cómo configurar su perfil.</span><span class="sxs-lookup"><span data-stu-id="f6604-217">Britta gets an email with instructions for setting up her profile.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f6604-218">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6604-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f6604-219">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="f6604-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OpsGenie.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="f6604-221">**Para asignar a Britta Simon a OpsGenie, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f6604-221">**To assign Britta Simon to OpsGenie, perform the following steps:**</span></span>

1. <span data-ttu-id="f6604-222">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f6604-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="f6604-224">En la lista de aplicaciones, seleccione **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="f6604-224">In the applications list, select **OpsGenie**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_app.png) 

3. <span data-ttu-id="f6604-226">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f6604-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="f6604-228">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f6604-228">Click **Add** button.</span></span> <span data-ttu-id="f6604-229">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f6604-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="f6604-231">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="f6604-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f6604-232">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f6604-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f6604-233">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f6604-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f6604-234">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="f6604-234">Testing single sign-on</span></span>

<span data-ttu-id="f6604-235">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="f6604-235">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="f6604-236">Al hacer clic en el icono de OpsGenie en el panel de acceso, debería iniciar sesión automáticamente en su aplicación OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="f6604-236">When you click the OpsGenie tile in the Access Panel, you should get automatically signed-on to your OpsGenie application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f6604-237">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f6604-237">Additional resources</span></span>

* [<span data-ttu-id="f6604-238">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6604-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f6604-239">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f6604-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_203.png

