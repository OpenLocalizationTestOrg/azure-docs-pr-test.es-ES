---
title: "Tutorial: Integración de Azure Active Directory con RunMyProcess | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y RunMyProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f8a08ef4f90d5cb98e7648ae6001055a3f4696e8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="40821-103">Tutorial: Integración de Azure Active Directory con RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="40821-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>

<span data-ttu-id="40821-104">En este tutorial, aprenderá a integrar RunMyProcess con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="40821-104">In this tutorial, you learn how to integrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="40821-105">La integración de RunMyProcess con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="40821-105">Integrating RunMyProcess with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="40821-106">Puede controlar en Azure AD quién tiene acceso a RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="40821-106">You can control in Azure AD who has access to RunMyProcess</span></span>
- <span data-ttu-id="40821-107">Puede permitir que los usuarios inicien sesión automáticamente en RunMyProcess (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="40821-107">You can enable your users to automatically get signed-on to RunMyProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="40821-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="40821-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="40821-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="40821-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40821-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="40821-110">Prerequisites</span></span>

<span data-ttu-id="40821-111">Para configurar la integración de Azure AD con RunMyProcess se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="40821-111">To configure Azure AD integration with RunMyProcess, you need the following items:</span></span>

- <span data-ttu-id="40821-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="40821-112">An Azure AD subscription</span></span>
- <span data-ttu-id="40821-113">Una suscripción habilitada para inicio de sesión único en RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="40821-113">A RunMyProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="40821-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="40821-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="40821-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="40821-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="40821-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="40821-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="40821-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="40821-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="40821-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="40821-118">Scenario description</span></span>
<span data-ttu-id="40821-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="40821-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="40821-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="40821-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="40821-121">Adición de RunMyProcess desde la galería</span><span class="sxs-lookup"><span data-stu-id="40821-121">Adding RunMyProcess from the gallery</span></span>
2. <span data-ttu-id="40821-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="40821-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-runmyprocess-from-the-gallery"></a><span data-ttu-id="40821-123">Adición de RunMyProcess desde la galería</span><span class="sxs-lookup"><span data-stu-id="40821-123">Adding RunMyProcess from the gallery</span></span>
<span data-ttu-id="40821-124">Para configurar la integración de RunMyProcess en Azure AD, será preciso que agregue RunMyProcess desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="40821-124">To configure the integration of RunMyProcess into Azure AD, you need to add RunMyProcess from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="40821-125">**Para agregar RunMyProcess desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="40821-125">**To add RunMyProcess from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="40821-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="40821-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="40821-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="40821-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="40821-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="40821-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="40821-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="40821-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="40821-133">En el cuadro de búsqueda, escriba **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="40821-133">In the search box, type **RunMyProcess**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. <span data-ttu-id="40821-135">En el panel de resultados, seleccione **RunMyProcess** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="40821-135">In the results panel, select **RunMyProcess**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="40821-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="40821-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="40821-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con RunMyProcess con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="40821-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="40821-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de RunMyProcess para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40821-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RunMyProcess is to a user in Azure AD.</span></span> <span data-ttu-id="40821-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="40821-140">In other words, a link relationship between an Azure AD user and the related user in RunMyProcess needs to be established.</span></span>

<span data-ttu-id="40821-141">Para establecer la relación de vínculo, en RunMyProcess, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="40821-141">In RunMyProcess, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="40821-142">Para configurar y probar el inicio de sesión único de Azure AD con RunMyProcess, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="40821-142">To configure and test Azure AD single sign-on with RunMyProcess, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="40821-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="40821-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="40821-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="40821-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="40821-145">**[Creación de un usuario de prueba de RunMyProcess](#creating-a-runmyprocess-test-user)**: para tener un homólogo de Britta Simon en RunMyProcess que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40821-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - to have a counterpart of Britta Simon in RunMyProcess that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="40821-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40821-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="40821-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="40821-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="40821-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="40821-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="40821-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="40821-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RunMyProcess application.</span></span>

<span data-ttu-id="40821-150">**Para configurar el inicio de sesión único de Azure AD con RunMyProcess, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="40821-150">**To configure Azure AD single sign-on with RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="40821-151">En Azure Portal, en la página de integración de la aplicación **RunMyProcess**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="40821-151">In the Azure portal, on the **RunMyProcess** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="40821-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="40821-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. <span data-ttu-id="40821-155">En la sección **Dominio y direcciones URL de RunMyProcess**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="40821-155">On the **RunMyProcess Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    <span data-ttu-id="40821-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://live.runmyprocess.com/live/<tenant id>`.</span><span class="sxs-lookup"><span data-stu-id="40821-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="40821-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="40821-158">The value is not real.</span></span> <span data-ttu-id="40821-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="40821-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="40821-160">Póngase en contacto con el [equipo de soporte al cliente de RunMyProcess](mailto:support@runmyprocess.com) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="40821-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) to get the value.</span></span> 

4. <span data-ttu-id="40821-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="40821-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. <span data-ttu-id="40821-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="40821-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="40821-165">En la sección **Configuración de RunMyProcess**, haga clic en **Configurar RunMyProcess** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="40821-165">On the **RunMyProcess Configuration** section, click **Configure RunMyProcess** to open **Configure sign-on** window.</span></span> <span data-ttu-id="40821-166">Copie los valores **Sign-Out URL y SAML Single Sign-On Service URL** (Dirección URL de cierre de sesión y Dirección URL del servicio de inicio de sesión único de SAML) de la **sección de referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="40821-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. <span data-ttu-id="40821-168">En otra ventana del explorador web, inicie sesión en su inquilino de RunMyProcess como administrador.</span><span class="sxs-lookup"><span data-stu-id="40821-168">In a different web browser window, sign-on to your RunMyProcess tenant as an administrator.</span></span>

8. <span data-ttu-id="40821-169">En el panel de navegación izquierdo, haga clic en **Account** (Cuenta) y seleccione **Configuration** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="40821-169">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. <span data-ttu-id="40821-171">Vaya a la sección **Authentication method** (Método de autenticación) y realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="40821-171">Go to **Authentication method** section and perform below steps:</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    <span data-ttu-id="40821-173">a.</span><span class="sxs-lookup"><span data-stu-id="40821-173">a.</span></span> <span data-ttu-id="40821-174">En **Método**, seleccione **SSO con Samlv2**.</span><span class="sxs-lookup"><span data-stu-id="40821-174">As **Method**, select **SSO with Samlv2**.</span></span> 

    <span data-ttu-id="40821-175">b.</span><span class="sxs-lookup"><span data-stu-id="40821-175">b.</span></span> <span data-ttu-id="40821-176">En el cuadro de texto **SSO redirect** (Redirección de SSO), pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="40821-176">In the **SSO redirect** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="40821-177">c.</span><span class="sxs-lookup"><span data-stu-id="40821-177">c.</span></span> <span data-ttu-id="40821-178">En el cuadro de texto **Logout redirect** (Redirección de cierre de sesión), pegue el valor de la **dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="40821-178">In the **Logout redirect** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="40821-179">d.</span><span class="sxs-lookup"><span data-stu-id="40821-179">d.</span></span> <span data-ttu-id="40821-180">En el cuadro de texto **Name Id Format** (Formato de identificador de nombre), escriba el valor del **formato de identificador de nombre** como en **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="40821-180">In the **Name Id Format** textbox, type the value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="40821-181">e.</span><span class="sxs-lookup"><span data-stu-id="40821-181">e.</span></span> <span data-ttu-id="40821-182">Copie el contenido del archivo de certificado descargado y péguelo en el cuadro de texto **Certificate** (Certificado).</span><span class="sxs-lookup"><span data-stu-id="40821-182">Copy the content of the downloaded certificate file and then paste it into the **Certificate** textbox.</span></span> 
 
    <span data-ttu-id="40821-183">f.</span><span class="sxs-lookup"><span data-stu-id="40821-183">f.</span></span> <span data-ttu-id="40821-184">Haga clic en el icono **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="40821-184">Click **Save** icon.</span></span>

> [!TIP]
> <span data-ttu-id="40821-185">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="40821-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="40821-186">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="40821-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="40821-187">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="40821-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="40821-188">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="40821-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="40821-189">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="40821-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="40821-191">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="40821-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="40821-192">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="40821-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="40821-194">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="40821-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="40821-196">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="40821-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="40821-198">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="40821-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="40821-200">a.</span><span class="sxs-lookup"><span data-stu-id="40821-200">a.</span></span> <span data-ttu-id="40821-201">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="40821-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="40821-202">b.</span><span class="sxs-lookup"><span data-stu-id="40821-202">b.</span></span> <span data-ttu-id="40821-203">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="40821-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="40821-204">c.</span><span class="sxs-lookup"><span data-stu-id="40821-204">c.</span></span> <span data-ttu-id="40821-205">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="40821-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="40821-206">d.</span><span class="sxs-lookup"><span data-stu-id="40821-206">d.</span></span> <span data-ttu-id="40821-207">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="40821-207">Click **Create**.</span></span>
 
### <a name="creating-a-runmyprocess-test-user"></a><span data-ttu-id="40821-208">Creación de un usuario de prueba de RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="40821-208">Creating a RunMyProcess test user</span></span>

<span data-ttu-id="40821-209">Para permitir que los usuarios de Azure AD inicien sesión en RunMyProcess, deben aprovisionarse en RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="40821-209">In order to enable Azure AD users to log in to RunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="40821-210">En el caso de RunMyProcess, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="40821-210">In the case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="40821-211">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="40821-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="40821-212">Inicie sesión en su sitio de la compañía de RunMyProcess como administrador.</span><span class="sxs-lookup"><span data-stu-id="40821-212">Log in to your RunMyProcess company site as an administrator.</span></span>

2. <span data-ttu-id="40821-213">Haga clic en **Account** (Cuenta) y seleccione **Users** (Usuarios) en el panel de navegación izquierdo y, a continuación, haga clic en **New User** (Usuario nuevo).</span><span class="sxs-lookup"><span data-stu-id="40821-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
    <span data-ttu-id="40821-214">![Nuevo usuario](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="40821-214">![New User](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>

3. <span data-ttu-id="40821-215">En la sección **Configuración del usuario** , lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="40821-215">In the **User Settings** section, perform the following steps:</span></span>
   
    <span data-ttu-id="40821-216">![Perfil](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Perfil")</span><span class="sxs-lookup"><span data-stu-id="40821-216">![Profile](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span> 
  
    <span data-ttu-id="40821-217">a.</span><span class="sxs-lookup"><span data-stu-id="40821-217">a.</span></span> <span data-ttu-id="40821-218">Escriba el **nombre** y la **dirección de correo electrónico** de una cuenta de Azure AD válida que quiera aprovisionar en los cuadros de texto correspondientes.</span><span class="sxs-lookup"><span data-stu-id="40821-218">Type the **Name** and **E-mail** of a valid Azure AD account you want to provision into the related textboxes.</span></span> 

    <span data-ttu-id="40821-219">b.</span><span class="sxs-lookup"><span data-stu-id="40821-219">b.</span></span> <span data-ttu-id="40821-220">Seleccione un **lenguaje IDE**, un **lenguaje** y un **perfil**.</span><span class="sxs-lookup"><span data-stu-id="40821-220">Select an **IDE language**, **Language**, and **Profile**.</span></span> 

    <span data-ttu-id="40821-221">c.</span><span class="sxs-lookup"><span data-stu-id="40821-221">c.</span></span> <span data-ttu-id="40821-222">Seleccione **Enviarme mensaje de correo electrónico de creación de cuenta**.</span><span class="sxs-lookup"><span data-stu-id="40821-222">Select **Send account creation e-mail to me**.</span></span> 

    <span data-ttu-id="40821-223">d.</span><span class="sxs-lookup"><span data-stu-id="40821-223">d.</span></span> <span data-ttu-id="40821-224">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="40821-224">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="40821-225">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de RunMyProcess que proporcione RunMyProcess para aprovisionar cuentas de usuario de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="40821-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess to provision Azure Active Directory user accounts.</span></span> 
    > 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="40821-226">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="40821-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="40821-227">En esta sección, concederá acceso a Britta Simon a RunMyProcess para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="40821-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RunMyProcess.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="40821-229">**Para asignar Britta Simon a RunMyProcess, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="40821-229">**To assign Britta Simon to RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="40821-230">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="40821-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="40821-232">En la lista de aplicaciones, seleccione **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="40821-232">In the applications list, select **RunMyProcess**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. <span data-ttu-id="40821-234">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="40821-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="40821-236">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="40821-236">Click **Add** button.</span></span> <span data-ttu-id="40821-237">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="40821-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="40821-239">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="40821-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="40821-240">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="40821-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="40821-241">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="40821-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="40821-242">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="40821-242">Testing single sign-on</span></span>

<span data-ttu-id="40821-243">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="40821-243">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="40821-244">Al hacer clic en el icono de RunMyProcess en el panel de acceso, debería iniciar sesión automáticamente en su aplicación RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="40821-244">When you click the RunMyProcess tile in the Access Panel, you should get automatically signed-on to your RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="40821-245">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="40821-245">Additional resources</span></span>

* [<span data-ttu-id="40821-246">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40821-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="40821-247">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="40821-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

