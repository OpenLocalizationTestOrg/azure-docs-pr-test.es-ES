---
title: "Tutorial: Integración de Azure Active Directory con Bonusly | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y Bonusly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 29a88b2efdb9f0f33f7933bc654a5a0fdf589c5a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="d2838-103">Tutorial: Integración de Azure Active Directory con Bonusly</span><span class="sxs-lookup"><span data-stu-id="d2838-103">Tutorial: Azure Active Directory integration with Bonusly</span></span>

<span data-ttu-id="d2838-104">En este tutorial, obtendrá información sobre cómo integrar Bonusly con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d2838-104">In this tutorial, you learn how to integrate Bonusly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d2838-105">La integración de Bonusly con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d2838-105">Integrating Bonusly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d2838-106">Puede controlar en Azure AD quién tiene acceso a Bonusly.</span><span class="sxs-lookup"><span data-stu-id="d2838-106">You can control in Azure AD who has access to Bonusly</span></span>
- <span data-ttu-id="d2838-107">Puede permitir que los usuarios inicien sesión automáticamente en Bonusly (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2838-107">You can enable your users to automatically get signed-on to Bonusly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d2838-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d2838-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d2838-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d2838-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2838-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d2838-110">Prerequisites</span></span>

<span data-ttu-id="d2838-111">Para configurar la integración de Azure AD con Bonusly, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d2838-111">To configure Azure AD integration with Bonusly, you need the following items:</span></span>

- <span data-ttu-id="d2838-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2838-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d2838-113">Una suscripción habilitada para el inicio de sesión único en Bonusly</span><span class="sxs-lookup"><span data-stu-id="d2838-113">A Bonusly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d2838-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="d2838-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d2838-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="d2838-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d2838-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d2838-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d2838-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d2838-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d2838-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="d2838-118">Scenario description</span></span>
<span data-ttu-id="d2838-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="d2838-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d2838-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="d2838-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d2838-121">Adición de Bonusly desde la galería</span><span class="sxs-lookup"><span data-stu-id="d2838-121">Adding Bonusly from the gallery</span></span>
2. <span data-ttu-id="d2838-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2838-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bonusly-from-the-gallery"></a><span data-ttu-id="d2838-123">Adición de Bonusly desde la galería</span><span class="sxs-lookup"><span data-stu-id="d2838-123">Adding Bonusly from the gallery</span></span>
<span data-ttu-id="d2838-124">Para configurar la integración de Bonusly en Azure AD, debe agregar Bonusly desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="d2838-124">To configure the integration of Bonusly into Azure AD, you need to add Bonusly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d2838-125">**Para agregar Bonusly desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d2838-125">**To add Bonusly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d2838-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d2838-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="d2838-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="d2838-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d2838-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d2838-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="d2838-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d2838-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="d2838-133">En el cuadro de búsqueda, escriba **Bonusly**, seleccione **Bonusly** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2838-133">In the search box, type **Bonusly**, select **Bonusly** from result panel then click **Add** button to add the application.</span></span>

    ![Bonusly en la lista de resultados](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d2838-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2838-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d2838-136">En esta sección, puede configurar y probar el inicio de sesión único de Azure AD con Bonusly con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d2838-136">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d2838-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Bonusly para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2838-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Bonusly is to a user in Azure AD.</span></span> <span data-ttu-id="d2838-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Bonusly.</span><span class="sxs-lookup"><span data-stu-id="d2838-138">In other words, a link relationship between an Azure AD user and the related user in Bonusly needs to be established.</span></span>

<span data-ttu-id="d2838-139">Para establecer la relación de vínculo, en Bonusly, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="d2838-139">In Bonusly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d2838-140">Para configurar y probar el inicio de sesión único de Azure AD con Bonusly, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d2838-140">To configure and test Azure AD single sign-on with Bonusly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d2838-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="d2838-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d2838-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d2838-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d2838-143">**[Creación de un usuario de prueba de Bonusly](#create-a-bonusly-test-user)**: para tener un homólogo de Britta Simon en Bonusly que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2838-143">**[Create a Bonusly test user](#create-a-bonusly-test-user)** - to have a counterpart of Britta Simon in Bonusly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d2838-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2838-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d2838-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="d2838-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d2838-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2838-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d2838-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Bonusly.</span><span class="sxs-lookup"><span data-stu-id="d2838-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bonusly application.</span></span>

<span data-ttu-id="d2838-148">**Para configurar el inicio de sesión único de Azure AD con Bonusly, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d2838-148">**To configure Azure AD single sign-on with Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="d2838-149">En Azure Portal, en la página de integración de la aplicación **Bonusly**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d2838-149">In the Azure portal, on the **Bonusly** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="d2838-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d2838-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. <span data-ttu-id="d2838-153">En la sección **Dominio y direcciones URL de Bonusly**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d2838-153">On the **Bonusly Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    <span data-ttu-id="d2838-155">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://Bonus.ly/saml/<tenant-name>`.</span><span class="sxs-lookup"><span data-stu-id="d2838-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://Bonus.ly/saml/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d2838-156">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="d2838-156">The value is not real.</span></span> <span data-ttu-id="d2838-157">Actualícelo con la dirección URL de respuesta real.</span><span class="sxs-lookup"><span data-stu-id="d2838-157">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="d2838-158">Póngase en contacto con el [equipo de soporte técnico al cliente de Bonusly](https://Bonusly/contact) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="d2838-158">Contact [Bonusly support team](https://Bonusly/contact) to get the value.</span></span>
 
4. <span data-ttu-id="d2838-159">En la sección **Certificado de firma de SAML**, copie el valor de **HUELLA DIGITAL** del certificado.</span><span class="sxs-lookup"><span data-stu-id="d2838-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. <span data-ttu-id="d2838-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="d2838-161">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d2838-163">En la sección **Configuración de Bonusly**, haga clic en **Configurar Bonusly** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="d2838-163">On the **Bonusly Configuration** section, click **Configure Bonusly** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d2838-164">Copie los valores de **SAML Entity ID y SAML Single Sign-On Service URL** (Identificador de entidad de SAML y URL del servicio de inicio de sesión único de SAML) de la sección de **referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="d2838-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. <span data-ttu-id="d2838-166">En una ventana del explorador diferente, inicie sesión en su inquilino de **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="d2838-166">In a different browser window, log in to your **Bonusly** tenant.</span></span>

8. <span data-ttu-id="d2838-167">En la barra de herramientas de la parte superior, haga clic en **Configuración** y seleccione **Integraciones y aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d2838-167">In the toolbar on the top, click **Settings**, and then select **Integrations and apps**.</span></span>
   
    <span data-ttu-id="d2838-168">![Sección Bonusly Social](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="d2838-168">![Bonusly Social Section](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span></span>
9. <span data-ttu-id="d2838-169">En **Inicio de sesión único**, seleccione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="d2838-169">Under **Single Sign-On**, select **SAML**.</span></span>

10. <span data-ttu-id="d2838-170">En la página de diálogo **SAML** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d2838-170">On the **SAML** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="d2838-171">![Página de diálogo Saml Bonusly](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="d2838-171">![Bonusly Saml Dialog page](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span></span>
   
    <span data-ttu-id="d2838-172">a.</span><span class="sxs-lookup"><span data-stu-id="d2838-172">a.</span></span> <span data-ttu-id="d2838-173">En el cuadro de texto **IdP SSO Target URL** (Dirección URL de destino de SSO de IdP), pegue el valor de la **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d2838-173">In the **IdP SSO target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="d2838-174">b.</span><span class="sxs-lookup"><span data-stu-id="d2838-174">b.</span></span> <span data-ttu-id="d2838-175">En el cuadro de texto **IdP Issuer** (Emisor de IdP), pegue el valor de **SAML Entity ID** (Identificador de entidad de SAML) que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d2838-175">In the **IdP Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="d2838-176">c.</span><span class="sxs-lookup"><span data-stu-id="d2838-176">c.</span></span> <span data-ttu-id="d2838-177">En el cuadro de texto **IdP Login URL** (Dirección URL de inicio de sesión de IdP), pegue el valor de la **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d2838-177">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d2838-178">d.</span><span class="sxs-lookup"><span data-stu-id="d2838-178">d.</span></span> <span data-ttu-id="d2838-179">Pegue el valor de **Huella digital** de Azure Portal en el cuadro de texto **Cert Fingerprint** (Huella digital de certificado).</span><span class="sxs-lookup"><span data-stu-id="d2838-179">Paste the **Thumbprint** value copied from Azure portal into the **Cert Fingerprint** textbox.</span></span>
   
11. <span data-ttu-id="d2838-180">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d2838-180">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d2838-181">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2838-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d2838-182">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="d2838-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d2838-183">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d2838-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d2838-184">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2838-184">Create an Azure AD test user</span></span>
<span data-ttu-id="d2838-185">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d2838-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="d2838-187">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="d2838-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d2838-188">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d2838-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d2838-190">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d2838-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d2838-192">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d2838-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Botón Agregar](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d2838-194">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="d2838-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Cuadro de diálogo Usuario](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d2838-196">a.</span><span class="sxs-lookup"><span data-stu-id="d2838-196">a.</span></span> <span data-ttu-id="d2838-197">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d2838-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d2838-198">b.</span><span class="sxs-lookup"><span data-stu-id="d2838-198">b.</span></span> <span data-ttu-id="d2838-199">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d2838-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d2838-200">c.</span><span class="sxs-lookup"><span data-stu-id="d2838-200">c.</span></span> <span data-ttu-id="d2838-201">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="d2838-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d2838-202">d.</span><span class="sxs-lookup"><span data-stu-id="d2838-202">d.</span></span> <span data-ttu-id="d2838-203">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d2838-203">Click **Create**.</span></span>
 
### <a name="create-a-bonusly-test-user"></a><span data-ttu-id="d2838-204">Creación de un usuario de prueba de Bonusly</span><span class="sxs-lookup"><span data-stu-id="d2838-204">Create a Bonusly test user</span></span>

<span data-ttu-id="d2838-205">Para permitir que los usuarios de Azure AD inicien sesión en Bonusly, tienen que aprovisionarse en Bonusly.</span><span class="sxs-lookup"><span data-stu-id="d2838-205">In order to enable Azure AD users to log in to Bonusly, they must be provisioned into Bonusly.</span></span> <span data-ttu-id="d2838-206">En el caso de Bonusly, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="d2838-206">In the case of Bonusly, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="d2838-207">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Bonusly que proporcione Bonusly para aprovisionar cuentas de usuario de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d2838-207">You can use any other Bonusly user account creation tools or APIs provided by Bonusly to provision AAD user accounts.</span></span>
>  

<span data-ttu-id="d2838-208">**Siga estos pasos para configurar el aprovisionamiento de usuario:**</span><span class="sxs-lookup"><span data-stu-id="d2838-208">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="d2838-209">En una ventana de explorador web diferente, inicie sesión en su inquilino de Bonusly.</span><span class="sxs-lookup"><span data-stu-id="d2838-209">In a web browser window, log in to your Bonusly tenant.</span></span>

2. <span data-ttu-id="d2838-210">Haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="d2838-210">Click **Settings**.</span></span>
 
    <span data-ttu-id="d2838-211">![Configuración](./media/active-directory-saas-bonus-tutorial/ic781041.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="d2838-211">![Settings](./media/active-directory-saas-bonus-tutorial/ic781041.png "Settings")</span></span>

3. <span data-ttu-id="d2838-212">Haga clic en la pestaña **Usuarios y bonificaciones** .</span><span class="sxs-lookup"><span data-stu-id="d2838-212">Click the **Users and bonuses** tab.</span></span>
   
    <span data-ttu-id="d2838-213">![Usuarios y bonificaciones](./media/active-directory-saas-bonus-tutorial/ic781042.png "Usuarios y bonificaciones")</span><span class="sxs-lookup"><span data-stu-id="d2838-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span></span>

4. <span data-ttu-id="d2838-214">Haga clic en **Administrar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d2838-214">Click **Manage Users**.</span></span>
   
    <span data-ttu-id="d2838-215">![Administración de usuarios](./media/active-directory-saas-bonus-tutorial/ic781043.png "Administración de usuarios")</span><span class="sxs-lookup"><span data-stu-id="d2838-215">![Manage Users](./media/active-directory-saas-bonus-tutorial/ic781043.png "Manage Users")</span></span>

5. <span data-ttu-id="d2838-216">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="d2838-216">Click **Add User**.</span></span>
   
    <span data-ttu-id="d2838-217">![Agregar usuario](./media/active-directory-saas-bonus-tutorial/ic781044.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="d2838-217">![Add User](./media/active-directory-saas-bonus-tutorial/ic781044.png "Add User")</span></span>

6. <span data-ttu-id="d2838-218">En el cuadro de diálogo **Agregar usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d2838-218">On the **Add User** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="d2838-219">![Agregar usuario](./media/active-directory-saas-bonus-tutorial/ic781045.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="d2838-219">![Add User](./media/active-directory-saas-bonus-tutorial/ic781045.png "Add User")</span></span>  

    <span data-ttu-id="d2838-220">a.</span><span class="sxs-lookup"><span data-stu-id="d2838-220">a.</span></span> <span data-ttu-id="d2838-221">En el cuadro de texto **Nombre**, escriba el nombre de usuario, en este caso **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d2838-221">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="d2838-222">b.</span><span class="sxs-lookup"><span data-stu-id="d2838-222">b.</span></span> <span data-ttu-id="d2838-223">En el cuadro de texto **Apellidos**, escriba el apellido del usuario, en este caso **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d2838-223">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="d2838-224">c.</span><span class="sxs-lookup"><span data-stu-id="d2838-224">c.</span></span> <span data-ttu-id="d2838-225">En el cuadro de texto **E-mail** (Correo electrónico), escriba el correo electrónico del usuario con el siguiente formato **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="d2838-225">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="d2838-226">d.</span><span class="sxs-lookup"><span data-stu-id="d2838-226">d.</span></span> <span data-ttu-id="d2838-227">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d2838-227">Click **Save**.</span></span>
   
     >[!NOTE]
     ><span data-ttu-id="d2838-228">El titular de la cuenta de Azure AD recibirá un mensaje de correo electrónico que incluye un vínculo para confirmar la cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="d2838-228">The Azure AD account holder receives an email that includes a link to confirm the account before it becomes active.</span></span>
     >  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d2838-229">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2838-229">Assign the Azure AD test user</span></span>

<span data-ttu-id="d2838-230">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Bonusly.</span><span class="sxs-lookup"><span data-stu-id="d2838-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bonusly.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="d2838-232">**Para asignar Britta Simon a Bonusly, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d2838-232">**To assign Britta Simon to Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="d2838-233">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d2838-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="d2838-235">En la lista de aplicaciones, seleccione **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="d2838-235">In the applications list, select **Bonusly**.</span></span>

    ![Vínculo a Bonusly en la lista de aplicaciones](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. <span data-ttu-id="d2838-237">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d2838-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202] 

4. <span data-ttu-id="d2838-239">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d2838-239">Click **Add** button.</span></span> <span data-ttu-id="d2838-240">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d2838-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="d2838-242">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="d2838-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d2838-243">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d2838-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d2838-244">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d2838-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d2838-245">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="d2838-245">Test single sign-on</span></span>

<span data-ttu-id="d2838-246">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d2838-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d2838-247">Al hacer clic en el icono de Bonusly en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Bonusly.</span><span class="sxs-lookup"><span data-stu-id="d2838-247">When you click the Bonusly tile in the Access Panel, you should get automatically signed-on to your Bonusly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d2838-248">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d2838-248">Additional resources</span></span>

* [<span data-ttu-id="d2838-249">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d2838-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d2838-250">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d2838-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

