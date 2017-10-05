---
title: "Tutorial: Integración de Azure Active Directory con Slack | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Slack."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 5aca630b2077d3f7d4ce9273ee668ed6a5f9843d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="cb755-103">Tutorial: Integración de Azure Active Directory con Slack</span><span class="sxs-lookup"><span data-stu-id="cb755-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="cb755-104">En este tutorial, obtendrá información sobre cómo integrar Slack con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cb755-104">In this tutorial, you learn how to integrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb755-105">La integración de Slack con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="cb755-105">Integrating Slack with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cb755-106">Puede controlar en Azure AD quién tiene acceso a Slack</span><span class="sxs-lookup"><span data-stu-id="cb755-106">You can control in Azure AD who has access to Slack</span></span>
- <span data-ttu-id="cb755-107">Puede permitir que los usuarios inicien sesión automáticamente en Slack (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb755-107">You can enable your users to automatically get signed-on to Slack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cb755-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cb755-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cb755-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cb755-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb755-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cb755-110">Prerequisites</span></span>

<span data-ttu-id="cb755-111">Para configurar la integración de Azure AD con Slack, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="cb755-111">To configure Azure AD integration with Slack, you need the following items:</span></span>

- <span data-ttu-id="cb755-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb755-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cb755-113">Una suscripción habilitada para el inicio de sesión único en Slack</span><span class="sxs-lookup"><span data-stu-id="cb755-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cb755-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="cb755-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cb755-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="cb755-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cb755-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="cb755-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cb755-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cb755-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cb755-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="cb755-118">Scenario description</span></span>
<span data-ttu-id="cb755-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="cb755-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cb755-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="cb755-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cb755-121">Adición de Slack desde la galería</span><span class="sxs-lookup"><span data-stu-id="cb755-121">Adding Slack from the gallery</span></span>
2. <span data-ttu-id="cb755-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb755-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-the-gallery"></a><span data-ttu-id="cb755-123">Adición de Slack desde la galería</span><span class="sxs-lookup"><span data-stu-id="cb755-123">Adding Slack from the gallery</span></span>
<span data-ttu-id="cb755-124">Para configurar la integración de Slack en Azure AD, tendrá que agregar Slack desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="cb755-124">To configure the integration of Slack into Azure AD, you need to add Slack from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cb755-125">**Para agregar Slack desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="cb755-125">**To add Slack from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cb755-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cb755-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cb755-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="cb755-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cb755-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cb755-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="cb755-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb755-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="cb755-133">En el cuadro de búsqueda, escriba **Slack**.</span><span class="sxs-lookup"><span data-stu-id="cb755-133">In the search box, type **Slack**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="cb755-135">En el panel de resultados, seleccione **Slack** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb755-135">In the results panel, select **Slack**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cb755-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb755-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cb755-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Slack con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cb755-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cb755-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Slack para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb755-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Slack is to a user in Azure AD.</span></span> <span data-ttu-id="cb755-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Slack.</span><span class="sxs-lookup"><span data-stu-id="cb755-140">In other words, a link relationship between an Azure AD user and the related user in Slack needs to be established.</span></span>

<span data-ttu-id="cb755-141">Para establecer la relación de vínculo, en Slack, asigne el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="cb755-141">In Slack, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cb755-142">Para configurar y probar el inicio de sesión único de Azure AD con Slack, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="cb755-142">To configure and test Azure AD single sign-on with Slack, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cb755-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="cb755-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cb755-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cb755-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cb755-145">**[Creación de un usuario de prueba de Slack](#creating-a-slack-test-user)**: para tener un homólogo de Britta Simon en Slack que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb755-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - to have a counterpart of Britta Simon in Slack that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cb755-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb755-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cb755-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="cb755-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cb755-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb755-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cb755-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Slack.</span><span class="sxs-lookup"><span data-stu-id="cb755-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="cb755-150">**Para configurar el inicio de sesión único de Azure AD con Slack, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="cb755-150">**To configure Azure AD single sign-on with Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="cb755-151">En Azure Portal, en la página de integración de la aplicación **Slack**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="cb755-151">In the Azure portal, on the **Slack** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="cb755-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cb755-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="cb755-155">En la sección **Dominio y direcciones URL de Slack**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="cb755-155">On the **Slack Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="cb755-157">a.</span><span class="sxs-lookup"><span data-stu-id="cb755-157">a.</span></span> <span data-ttu-id="cb755-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.slack.com`.</span><span class="sxs-lookup"><span data-stu-id="cb755-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="cb755-159">b.</span><span class="sxs-lookup"><span data-stu-id="cb755-159">b.</span></span> <span data-ttu-id="cb755-160">En el cuadro de texto **Identificador**, escriba la dirección URL: `https://slack.com`</span><span class="sxs-lookup"><span data-stu-id="cb755-160">In the **Identifier** textbox, type the URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cb755-161">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="cb755-161">The value is not real.</span></span> <span data-ttu-id="cb755-162">Tiene que actualizar este valor con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="cb755-162">You have to update the value with the actual Sign On URL.</span></span> <span data-ttu-id="cb755-163">Póngase en contacto con el [equipo de soporte técnico de Slack](https://slack.com/help/contact) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="cb755-163">Contact [Slack support team](https://slack.com/help/contact) to get the value</span></span>
     
4. <span data-ttu-id="cb755-164">La aplicación Slack espera las aserciones de SAML en un formato específico.</span><span class="sxs-lookup"><span data-stu-id="cb755-164">Slack application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="cb755-165">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb755-165">Configure the following claims for this application.</span></span> <span data-ttu-id="cb755-166">Puede administrar los valores de estos atributos en la sección "**Atributos de usuario**" de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="cb755-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="cb755-167">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="cb755-167">The following screenshot shows an example for this.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="cb755-169">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, seleccione **user.mail** como **identificador de usuario**, y para cada fila se muestra en la tabla siguiente, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="cb755-169">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="cb755-170">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="cb755-170">Attribute Name</span></span> | <span data-ttu-id="cb755-171">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="cb755-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="cb755-172">first_name</span><span class="sxs-lookup"><span data-stu-id="cb755-172">first_name</span></span> | <span data-ttu-id="cb755-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="cb755-173">user.givenname</span></span> |
    | <span data-ttu-id="cb755-174">last_name</span><span class="sxs-lookup"><span data-stu-id="cb755-174">last_name</span></span> | <span data-ttu-id="cb755-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="cb755-175">user.surname</span></span> |
    | <span data-ttu-id="cb755-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="cb755-176">User.Email</span></span> | <span data-ttu-id="cb755-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="cb755-177">user.mail</span></span> |  
    | <span data-ttu-id="cb755-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="cb755-178">User.Username</span></span> | <span data-ttu-id="cb755-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="cb755-179">user.userprincipalname</span></span> |

    <span data-ttu-id="cb755-180">a.</span><span class="sxs-lookup"><span data-stu-id="cb755-180">a.</span></span> <span data-ttu-id="cb755-181">Haga clic en **Atributo** para abrir el cuadro de diálogo **Editar atributo** y realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="cb755-181">Click on **Attribute** to open **Edit Attribute** dialog box and perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="cb755-183">a.</span><span class="sxs-lookup"><span data-stu-id="cb755-183">a.</span></span> <span data-ttu-id="cb755-184">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="cb755-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="cb755-185">b.</span><span class="sxs-lookup"><span data-stu-id="cb755-185">b.</span></span> <span data-ttu-id="cb755-186">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="cb755-186">From the **Value** list, select the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="cb755-187">c.</span><span class="sxs-lookup"><span data-stu-id="cb755-187">c.</span></span> <span data-ttu-id="cb755-188">Haga clic en **Aceptar**</span><span class="sxs-lookup"><span data-stu-id="cb755-188">Click **OK**</span></span>

6. <span data-ttu-id="cb755-189">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="cb755-189">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="cb755-191">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="cb755-191">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="cb755-193">En la sección **Configuración de Slack**, haga clic en **Configurar Slack** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="cb755-193">On the **Slack Configuration** section, click **Configure Slack** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cb755-194">Copie los valores de **SAML Entity ID y SAML Single Sign-On Service URL** (Identificador de entidad de SAML y URL del servicio de inicio de sesión único de SAML) de la sección de **referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="cb755-194">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="cb755-196">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de Slack como administrador.</span><span class="sxs-lookup"><span data-stu-id="cb755-196">In a different web browser window, log in to your Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="cb755-197">Vaya a **Microsoft Azure AD** y luego a **Configuración del equipo**.</span><span class="sxs-lookup"><span data-stu-id="cb755-197">Navigate to **Microsoft Azure AD** then go to **Team Settings**.</span></span>

     ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="cb755-199">En la sección **Configuración del equipo**, haga clic en la pestaña **Autenticación** y luego en **Cambiar configuración**.</span><span class="sxs-lookup"><span data-stu-id="cb755-199">In the **Team Settings** section, click the **Authentication** tab, and then click **Change Settings**.</span></span>

     ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="cb755-201">En el cuadro de diálogo **Configuración de la autenticación SAML** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="cb755-201">On the **SAML Authentication Settings** dialog, perform the following steps:</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="cb755-203">a.</span><span class="sxs-lookup"><span data-stu-id="cb755-203">a.</span></span>  <span data-ttu-id="cb755-204">En el cuadro de texto **SAML 2.0 Endpoint (HTTP)** (Punto de conexión SAML 2.0 (HTTP)), pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cb755-204">In the **SAML 2.0 Endpoint (HTTP)** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cb755-205">b.</span><span class="sxs-lookup"><span data-stu-id="cb755-205">b.</span></span>  <span data-ttu-id="cb755-206">En el cuadro de texto **Emisor de proveedor de identidades**, pegue el valor del **identificador de entidad de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cb755-206">In the **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cb755-207">c.</span><span class="sxs-lookup"><span data-stu-id="cb755-207">c.</span></span>  <span data-ttu-id="cb755-208">Abra el archivo de certificado descargado en el Bloc de notas, copie el contenido del mismo en el Portapapeles y luego péguelo en el cuadro de texto **Certificado público**.</span><span class="sxs-lookup"><span data-stu-id="cb755-208">Open your downloaded certificate file in notepad, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>

    <span data-ttu-id="cb755-209">d.</span><span class="sxs-lookup"><span data-stu-id="cb755-209">d.</span></span> <span data-ttu-id="cb755-210">Configure las tres opciones anteriores según corresponda para su equipo de Slack.</span><span class="sxs-lookup"><span data-stu-id="cb755-210">Configure the above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="cb755-211">Para obtener más información sobre la configuración, busque la **Guía de configuración de SSO de Slack** aquí.</span><span class="sxs-lookup"><span data-stu-id="cb755-211">For more information about the settings, please find the **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="cb755-212">e.</span><span class="sxs-lookup"><span data-stu-id="cb755-212">e.</span></span>  <span data-ttu-id="cb755-213">Haga clic en **Guardar configuración**.</span><span class="sxs-lookup"><span data-stu-id="cb755-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users to change their email address**.

    e.  Select **Allow users to choose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="cb755-214">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb755-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cb755-215">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="cb755-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cb755-216">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cb755-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cb755-217">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb755-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="cb755-218">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cb755-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="cb755-220">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="cb755-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cb755-221">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cb755-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cb755-223">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="cb755-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cb755-225">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb755-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cb755-227">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="cb755-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cb755-229">a.</span><span class="sxs-lookup"><span data-stu-id="cb755-229">a.</span></span> <span data-ttu-id="cb755-230">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cb755-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cb755-231">b.</span><span class="sxs-lookup"><span data-stu-id="cb755-231">b.</span></span> <span data-ttu-id="cb755-232">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cb755-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cb755-233">c.</span><span class="sxs-lookup"><span data-stu-id="cb755-233">c.</span></span> <span data-ttu-id="cb755-234">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="cb755-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cb755-235">d.</span><span class="sxs-lookup"><span data-stu-id="cb755-235">d.</span></span> <span data-ttu-id="cb755-236">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cb755-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="cb755-237">Creación de usuario de prueba de Slack</span><span class="sxs-lookup"><span data-stu-id="cb755-237">Creating a Slack test user</span></span>

<span data-ttu-id="cb755-238">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en Slack.</span><span class="sxs-lookup"><span data-stu-id="cb755-238">The objective of this section is to create a user called Britta Simon in Slack.</span></span> <span data-ttu-id="cb755-239">Slack admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="cb755-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="cb755-240">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="cb755-240">There is no action item for you in this section.</span></span> <span data-ttu-id="cb755-241">Al intentar acceder a Slack, se crea un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="cb755-241">A new user is created during an attempt to access Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="cb755-242">Si necesita crear manualmente un usuario, es preciso que se ponga en contacto con el [equipo de soporte técnico de Slack](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="cb755-242">If you need to create a user manually, you need to Contact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cb755-243">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb755-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cb755-244">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Slack.</span><span class="sxs-lookup"><span data-stu-id="cb755-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Slack.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="cb755-246">**Para asignar a Britta Simon a Slack, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="cb755-246">**To assign Britta Simon to Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="cb755-247">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cb755-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="cb755-249">En la lista de aplicaciones, seleccione **Slack**.</span><span class="sxs-lookup"><span data-stu-id="cb755-249">In the applications list, select **Slack**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="cb755-251">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cb755-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="cb755-253">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="cb755-253">Click **Add** button.</span></span> <span data-ttu-id="cb755-254">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cb755-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="cb755-256">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="cb755-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cb755-257">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cb755-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cb755-258">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cb755-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cb755-259">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="cb755-259">Testing single sign-on</span></span>

<span data-ttu-id="cb755-260">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="cb755-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cb755-261">Al hacer clic en el icono de Slack en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Slack.</span><span class="sxs-lookup"><span data-stu-id="cb755-261">When you click the Slack tile in the Access Panel, you should get automatically signed-on to your Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cb755-262">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="cb755-262">Additional resources</span></span>

* [<span data-ttu-id="cb755-263">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb755-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cb755-264">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cb755-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

