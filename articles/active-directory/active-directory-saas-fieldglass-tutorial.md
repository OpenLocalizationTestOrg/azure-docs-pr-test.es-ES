---
title: "Tutorial: Integración de Azure Active Directory con Fieldglass | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Fieldglass."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2510195f-d5b1-4684-b3da-283fb8619df2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 18926dd88b19cd672f11ae05f18e354e79a6b397
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fieldglass"></a><span data-ttu-id="81996-103">Tutorial: Integración de Azure Active Directory con Fieldglass</span><span class="sxs-lookup"><span data-stu-id="81996-103">Tutorial: Azure Active Directory integration with Fieldglass</span></span>

<span data-ttu-id="81996-104">En este tutorial, aprenderá a integrar Fieldglass con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="81996-104">In this tutorial, you learn how to integrate Fieldglass with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="81996-105">La integración de Fieldglass con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="81996-105">Integrating Fieldglass with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="81996-106">En Azure AD se puede controlar quién tiene acceso a Fieldglass</span><span class="sxs-lookup"><span data-stu-id="81996-106">You can control in Azure AD who has access to Fieldglass</span></span>
- <span data-ttu-id="81996-107">Puede permitir que los usuarios inicien sesión automáticamente en Fieldglass (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81996-107">You can enable your users to automatically get signed-on to Fieldglass (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="81996-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="81996-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="81996-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="81996-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81996-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="81996-110">Prerequisites</span></span>

<span data-ttu-id="81996-111">Para configurar la integración de Azure AD con Fieldglass se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="81996-111">To configure Azure AD integration with Fieldglass, you need the following items:</span></span>

- <span data-ttu-id="81996-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81996-112">An Azure AD subscription</span></span>
- <span data-ttu-id="81996-113">Una suscripción habilitada para el inicio de sesión único en Fieldglass</span><span class="sxs-lookup"><span data-stu-id="81996-113">A Fieldglass single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="81996-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="81996-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="81996-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="81996-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="81996-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="81996-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="81996-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="81996-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="81996-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="81996-118">Scenario description</span></span>
<span data-ttu-id="81996-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="81996-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="81996-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="81996-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="81996-121">Incorporación de Fieldglass desde la galería</span><span class="sxs-lookup"><span data-stu-id="81996-121">Adding Fieldglass from the gallery</span></span>
2. <span data-ttu-id="81996-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81996-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fieldglass-from-the-gallery"></a><span data-ttu-id="81996-123">Incorporación de Fieldglass desde la galería</span><span class="sxs-lookup"><span data-stu-id="81996-123">Adding Fieldglass from the gallery</span></span>
<span data-ttu-id="81996-124">Para configurar la integración de Fieldglass en Azure AD, será preciso que agregue Fieldglass desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="81996-124">To configure the integration of Fieldglass into Azure AD, you need to add Fieldglass from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="81996-125">**Para agregar Fieldglass desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="81996-125">**To add Fieldglass from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="81996-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="81996-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="81996-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="81996-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="81996-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="81996-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="81996-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81996-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="81996-133">En el cuadro de búsqueda, escriba **Fieldglass**.</span><span class="sxs-lookup"><span data-stu-id="81996-133">In the search box, type **Fieldglass**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_search.png)

5. <span data-ttu-id="81996-135">En el panel de resultados, seleccione **Fieldglass** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="81996-135">In the results panel, select **Fieldglass**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="81996-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81996-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="81996-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Fieldglass con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="81996-138">In this section, you configure and test Azure AD single sign-on with Fieldglass based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="81996-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Fieldglass para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81996-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Fieldglass is to a user in Azure AD.</span></span> <span data-ttu-id="81996-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Fieldglass.</span><span class="sxs-lookup"><span data-stu-id="81996-140">In other words, a link relationship between an Azure AD user and the related user in Fieldglass needs to be established.</span></span>

<span data-ttu-id="81996-141">Para establecer la relación de vínculo, en Fieldglass, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="81996-141">In Fieldglass, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="81996-142">Para configurar y probar el inicio de sesión único de Azure AD con Fieldglass, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="81996-142">To configure and test Azure AD single sign-on with Fieldglass, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="81996-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="81996-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="81996-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81996-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="81996-145">**[Creación de un usuario de prueba en Fieldglass](#creating-a-fieldglass-test-user)**: para tener un homólogo de Britta Simon en Fieldglass que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81996-145">**[Creating a Fieldglass test user](#creating-a-fieldglass-test-user)** - to have a counterpart of Britta Simon in Fieldglass that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="81996-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81996-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="81996-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="81996-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="81996-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81996-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="81996-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Fieldglass.</span><span class="sxs-lookup"><span data-stu-id="81996-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Fieldglass application.</span></span>

<span data-ttu-id="81996-150">**Para configurar el inicio de sesión único de Azure AD con Fieldglass, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="81996-150">**To configure Azure AD single sign-on with Fieldglass, perform the following steps:**</span></span>

1. <span data-ttu-id="81996-151">En Azure Portal, en la página de integración de la aplicación **Fieldglass**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="81996-151">In the Azure portal, on the **Fieldglass** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="81996-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="81996-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_samlbase.png)

3. <span data-ttu-id="81996-155">En la sección de **dominio y direcciones URL de Fieldglass**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="81996-155">On the **Fieldglass Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_url.png)

    <span data-ttu-id="81996-157">a.</span><span class="sxs-lookup"><span data-stu-id="81996-157">a.</span></span> <span data-ttu-id="81996-158">En el cuadro de texto **Identificador**, escriba una dirección URL como `https://www.fieldglass.com` o siga el patrón: `https://<company name>.fgvms.com`</span><span class="sxs-lookup"><span data-stu-id="81996-158">In the **Identifier** textbox, type a URL as  `https://www.fieldglass.com` or follow the pattern:  `https://<company name>.fgvms.com`</span></span>

    <span data-ttu-id="81996-159">b.</span><span class="sxs-lookup"><span data-stu-id="81996-159">b.</span></span> <span data-ttu-id="81996-160">En el cuadro de texto **URL de respuesta** , escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="81996-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://www.fieldglass.net/<company name>`|
    | `https://<company name>.fgvms.com/<company name>`|

    > [!NOTE] 
    > <span data-ttu-id="81996-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="81996-161">These values are not real.</span></span> <span data-ttu-id="81996-162">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="81996-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="81996-163">Póngase en contacto con el [equipo de soporte técnico de Fieldglass](http://www.fieldglass.com/solutions/support) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="81996-163">Contact [Fieldglass support team](http://www.fieldglass.com/solutions/support) to get these values.</span></span>
 
4. <span data-ttu-id="81996-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="81996-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_certificate.png) 

5. <span data-ttu-id="81996-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="81996-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fieldglass-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="81996-168">En la sección **Configuración de Fieldglass**, haga clic en **Configurar Fieldglass** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="81996-168">On the **Fieldglass Configuration** section, click **Configure Fieldglass** to open **Configure sign-on** window.</span></span> <span data-ttu-id="81996-169">Copie los valores de **Sign-Out URL and SAML Entity ID** (Dirección URL de cierre de sesión e identificador de entidad de SAML) de la **sección Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="81996-169">Copy the **Sign-Out URL and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_configure.png) 

7. <span data-ttu-id="81996-171">Para configurar el inicio de sesión único en **Fieldglass**, debe enviar el **certificado (Base64)** descargado y la **dirección URL de cierre de sesión y el identificador de entidad de SAML** al [equipo de soporte técnico de Fieldglass](http://www.fieldglass.com/solutions/support).</span><span class="sxs-lookup"><span data-stu-id="81996-171">To configure single sign-on on **Fieldglass** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID** to [Fieldglass support team](http://www.fieldglass.com/solutions/support).</span></span> <span data-ttu-id="81996-172">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="81996-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="81996-173">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="81996-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="81996-174">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="81996-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="81996-175">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="81996-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="81996-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81996-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="81996-177">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="81996-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="81996-179">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="81996-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="81996-180">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="81996-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="81996-182">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="81996-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="81996-184">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81996-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="81996-186">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="81996-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="81996-188">a.</span><span class="sxs-lookup"><span data-stu-id="81996-188">a.</span></span> <span data-ttu-id="81996-189">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="81996-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="81996-190">b.</span><span class="sxs-lookup"><span data-stu-id="81996-190">b.</span></span> <span data-ttu-id="81996-191">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81996-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="81996-192">c.</span><span class="sxs-lookup"><span data-stu-id="81996-192">c.</span></span> <span data-ttu-id="81996-193">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="81996-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="81996-194">d.</span><span class="sxs-lookup"><span data-stu-id="81996-194">d.</span></span> <span data-ttu-id="81996-195">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="81996-195">Click **Create**.</span></span>
 
### <a name="creating-a-fieldglass-test-user"></a><span data-ttu-id="81996-196">Creación de un usuario de prueba en Fieldglass</span><span class="sxs-lookup"><span data-stu-id="81996-196">Creating a Fieldglass test user</span></span>

<span data-ttu-id="81996-197">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en Fieldglass.</span><span class="sxs-lookup"><span data-stu-id="81996-197">The objective of this section is to create a user called Britta Simon in FieldGlass.</span></span> <span data-ttu-id="81996-198">Trabaje con el [equipo de soporte técnico de Fieldglass](http://www.fieldglass.com/solutions/support) para agregar usuarios a la cuenta de ICIMS.</span><span class="sxs-lookup"><span data-stu-id="81996-198">Please work with your [Fieldglass support team](http://www.fieldglass.com/solutions/support) to add the users in the Fieldglass account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="81996-199">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81996-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="81996-200">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Fieldglass.</span><span class="sxs-lookup"><span data-stu-id="81996-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Fieldglass.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="81996-202">**Para asignar Britta Simon a Fieldglass, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="81996-202">**To assign Britta Simon to Fieldglass, perform the following steps:**</span></span>

1. <span data-ttu-id="81996-203">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="81996-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="81996-205">En la lista de aplicaciones, seleccione **Fieldglass**.</span><span class="sxs-lookup"><span data-stu-id="81996-205">In the applications list, select **Fieldglass**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_app.png) 

3. <span data-ttu-id="81996-207">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="81996-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="81996-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="81996-209">Click **Add** button.</span></span> <span data-ttu-id="81996-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="81996-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="81996-212">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="81996-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="81996-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="81996-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="81996-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="81996-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="81996-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="81996-215">Testing single sign-on</span></span>

<span data-ttu-id="81996-216">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="81996-216">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="81996-217">Al hacer clic en el icono de Fieldglass en el panel de acceso, debería iniciar sesión automáticamente en la aplicación Fieldglass.</span><span class="sxs-lookup"><span data-stu-id="81996-217">When you click the Fieldglass tile in the Access Panel, you should get automatically signed-on to your Fieldglass application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="81996-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="81996-218">Additional resources</span></span>

* [<span data-ttu-id="81996-219">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81996-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81996-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="81996-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_203.png

