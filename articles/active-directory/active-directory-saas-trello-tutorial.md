---
title: "Tutorial: integración de Azure Active Directory con Trello | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Trello."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: d93667f16f2d72995e4a42e79e9125b8e3f6b07c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="64a0e-103">Tutorial: integración de Azure Active Directory con Trello</span><span class="sxs-lookup"><span data-stu-id="64a0e-103">Tutorial: Azure Active Directory integration with Trello</span></span>

<span data-ttu-id="64a0e-104">En este tutorial, obtendrá información sobre cómo integrar Trello con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="64a0e-104">In this tutorial, you learn how to integrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="64a0e-105">Integrar Trello con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="64a0e-105">Integrating Trello with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="64a0e-106">Puede controlar en Azure AD quién tiene acceso a Trello.</span><span class="sxs-lookup"><span data-stu-id="64a0e-106">You can control in Azure AD who has access to Trello</span></span>
- <span data-ttu-id="64a0e-107">Puede permitir que los usuarios inicien sesión automáticamente en Trello (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64a0e-107">You can enable your users to automatically get signed-on to Trello (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="64a0e-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="64a0e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="64a0e-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="64a0e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64a0e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="64a0e-110">Prerequisites</span></span>

<span data-ttu-id="64a0e-111">Para configurar la integración de Azure AD con Trello, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="64a0e-111">To configure Azure AD integration with Trello, you need the following items:</span></span>

- <span data-ttu-id="64a0e-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="64a0e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="64a0e-113">Una suscripción habilitada para inicio de sesión único en Trello</span><span class="sxs-lookup"><span data-stu-id="64a0e-113">A Trello single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="64a0e-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="64a0e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="64a0e-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="64a0e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="64a0e-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="64a0e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="64a0e-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="64a0e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="64a0e-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="64a0e-118">Scenario description</span></span>
<span data-ttu-id="64a0e-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="64a0e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="64a0e-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="64a0e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="64a0e-121">Adición de Trello desde la galería</span><span class="sxs-lookup"><span data-stu-id="64a0e-121">Adding Trello from the gallery</span></span>
2. <span data-ttu-id="64a0e-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="64a0e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trello-from-the-gallery"></a><span data-ttu-id="64a0e-123">Adición de Trello desde la galería</span><span class="sxs-lookup"><span data-stu-id="64a0e-123">Adding Trello from the gallery</span></span>
<span data-ttu-id="64a0e-124">Para configurar la integración de Trello en Azure AD, deberá agregar Trello desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="64a0e-124">To configure the integration of Trello into Azure AD, you need to add Trello from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="64a0e-125">**Para agregar Trello desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="64a0e-125">**To add Trello from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="64a0e-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="64a0e-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="64a0e-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="64a0e-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="64a0e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="64a0e-133">En el cuadro de búsqueda, escriba **Trello**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-133">In the search box, type **Trello**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. <span data-ttu-id="64a0e-135">En el panel de resultados, seleccione **Trello** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="64a0e-135">In the results panel, select **Trello**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="64a0e-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="64a0e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="64a0e-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Trello con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="64a0e-138">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="64a0e-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Trello para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64a0e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Trello is to a user in Azure AD.</span></span> <span data-ttu-id="64a0e-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario correspondiente de Trello.</span><span class="sxs-lookup"><span data-stu-id="64a0e-140">In other words, a link relationship between an Azure AD user and the related user in Trello needs to be established.</span></span>

<span data-ttu-id="64a0e-141">Para establecer la relación de vínculo, en Trello, asigne el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-141">In Trello, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="64a0e-142">Para configurar y probar el inicio de sesión único de Azure AD con Trello, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="64a0e-142">To configure and test Azure AD single sign-on with Trello, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="64a0e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="64a0e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="64a0e-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64a0e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="64a0e-145">**[Creación de usuario de prueba de Trello](#creating-a-trello-test-user)**: para tener un homólogo de Britta Simon en Trello que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64a0e-145">**[Creating a Trello test user](#creating-a-trello-test-user)** - to have a counterpart of Britta Simon in Trello that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="64a0e-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64a0e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="64a0e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="64a0e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="64a0e-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="64a0e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="64a0e-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en su aplicación Trello.</span><span class="sxs-lookup"><span data-stu-id="64a0e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trello application.</span></span>

<span data-ttu-id="64a0e-150">**Para configurar el inicio de sesión único de Azure AD con Trello, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="64a0e-150">**To configure Azure AD single sign-on with Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="64a0e-151">En Azure Portal, en la página de integración de la aplicación **Trello**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-151">In the Azure portal, on the **Trello** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="64a0e-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="64a0e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. <span data-ttu-id="64a0e-155">En la sección **Dominio y direcciones URL de Trello**, si quiere configurar la aplicación en el modo iniciado por **IDP**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="64a0e-155">On the **Trello Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    <span data-ttu-id="64a0e-157">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://trello.com/auth/saml/consume/<enterprise>`.</span><span class="sxs-lookup"><span data-stu-id="64a0e-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

4. <span data-ttu-id="64a0e-158">En la sección **Dominio y direcciones URL de Trello**, si quiere configurar la aplicación en **SP initiated mode** (Modo iniciado por SP), realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="64a0e-158">On the **Trello Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    <span data-ttu-id="64a0e-160">a.</span><span class="sxs-lookup"><span data-stu-id="64a0e-160">a.</span></span> <span data-ttu-id="64a0e-161">Haga clic en la opción **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-161">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="64a0e-162">b.</span><span class="sxs-lookup"><span data-stu-id="64a0e-162">b.</span></span> <span data-ttu-id="64a0e-163">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://trello.com/auth/saml/consume/<enterprise>`.</span><span class="sxs-lookup"><span data-stu-id="64a0e-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

    >[!NOTE]
    ><span data-ttu-id="64a0e-164">Debe obtener el campo de datos dinámico **\<enterprise\>** desde Trello.</span><span class="sxs-lookup"><span data-stu-id="64a0e-164">You should get the **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="64a0e-165">Si no tiene el valor del campo de datos dinámico, póngase en contacto con el [equipo de soporte técnico de Trello](mailto:support@trello.com) para obtenerlo.</span><span class="sxs-lookup"><span data-stu-id="64a0e-165">If you don't have the slug value, contact [Trello support team](mailto:support@trello.com) to get the slug for you enterprise.</span></span>
    > 

5. <span data-ttu-id="64a0e-166">La aplicación de Trello espera que las aserciones SAML contengan un atributo denominado "email".</span><span class="sxs-lookup"><span data-stu-id="64a0e-166">Trello application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="64a0e-167">Configure los siguientes atributos para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="64a0e-167">Configure the following attributes  for this application.</span></span> <span data-ttu-id="64a0e-168">Puede administrar el valor de estos atributos desde la pestaña "**Atributos de usuario**" de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="64a0e-168">You can manage the values of these attributes from the **"User Attributes"** of the application.</span></span> <span data-ttu-id="64a0e-169">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="64a0e-169">The following screenshot shows an example for this.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. <span data-ttu-id="64a0e-171">En el cuadro de diálogo **Atributos de token de SAML** , para cada fila de la tabla siguiente, realice los pasos que se indican a continuación:</span><span class="sxs-lookup"><span data-stu-id="64a0e-171">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
    | <span data-ttu-id="64a0e-172">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="64a0e-172">Attribute Name</span></span> | <span data-ttu-id="64a0e-173">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="64a0e-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="64a0e-174">User.Email</span><span class="sxs-lookup"><span data-stu-id="64a0e-174">User.Email</span></span> | <span data-ttu-id="64a0e-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="64a0e-175">user.mail</span></span> |
    | <span data-ttu-id="64a0e-176">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="64a0e-176">User.FirstName</span></span> | <span data-ttu-id="64a0e-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="64a0e-177">user.givenname</span></span> |
    | <span data-ttu-id="64a0e-178">User.LastName</span><span class="sxs-lookup"><span data-stu-id="64a0e-178">User.LastName</span></span> | <span data-ttu-id="64a0e-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="64a0e-179">user.surname</span></span> |

    <span data-ttu-id="64a0e-180">a.</span><span class="sxs-lookup"><span data-stu-id="64a0e-180">a.</span></span> <span data-ttu-id="64a0e-181">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="64a0e-184">b.</span><span class="sxs-lookup"><span data-stu-id="64a0e-184">b.</span></span> <span data-ttu-id="64a0e-185">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="64a0e-185">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

    <span data-ttu-id="64a0e-186">c.</span><span class="sxs-lookup"><span data-stu-id="64a0e-186">c.</span></span> <span data-ttu-id="64a0e-187">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="64a0e-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="64a0e-188">d.</span><span class="sxs-lookup"><span data-stu-id="64a0e-188">d.</span></span> <span data-ttu-id="64a0e-189">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-189">Click **Ok**.</span></span> 
 
7. <span data-ttu-id="64a0e-190">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="64a0e-190">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. <span data-ttu-id="64a0e-192">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="64a0e-192">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="64a0e-194">En la sección **Configuración de Trello**, haga clic en **Configurar Trello** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-194">On the **Trello Configuration** section, click **Configure Trello** to open **Configure sign-on** window.</span></span> <span data-ttu-id="64a0e-195">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-195">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. <span data-ttu-id="64a0e-197">Con el fin de que se configure el inicio de sesión único para la aplicación, vaya a la página de [configuración de SSO empresarial de Trello](https://trello.com/sso-configuration) para enviar la **URL del servicio de inicio de sesión único de SAML** al [equipo de soporte técnico de Trello](mailto:support@trello.com) y adjuntar el **certificado (Base64)**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-197">To get SSO configured for your application, go to [Trello enterprise SSO configuration](https://trello.com/sso-configuration) page to send [Trello support team](mailto:support@trello.com) the **SAML Single Sign-On Service URL** and attach the **Certificate (Base64)**.</span></span>

> [!TIP]
> <span data-ttu-id="64a0e-198">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="64a0e-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="64a0e-199">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="64a0e-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="64a0e-200">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="64a0e-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="64a0e-201">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="64a0e-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="64a0e-202">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="64a0e-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="64a0e-204">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="64a0e-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="64a0e-205">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="64a0e-207">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="64a0e-209">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="64a0e-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="64a0e-211">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="64a0e-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="64a0e-213">a.</span><span class="sxs-lookup"><span data-stu-id="64a0e-213">a.</span></span> <span data-ttu-id="64a0e-214">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="64a0e-215">b.</span><span class="sxs-lookup"><span data-stu-id="64a0e-215">b.</span></span> <span data-ttu-id="64a0e-216">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64a0e-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="64a0e-217">c.</span><span class="sxs-lookup"><span data-stu-id="64a0e-217">c.</span></span> <span data-ttu-id="64a0e-218">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="64a0e-219">d.</span><span class="sxs-lookup"><span data-stu-id="64a0e-219">d.</span></span> <span data-ttu-id="64a0e-220">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-220">Click **Create**.</span></span>
 
### <a name="creating-a-trello-test-user"></a><span data-ttu-id="64a0e-221">Creación de usuario de prueba de Trello</span><span class="sxs-lookup"><span data-stu-id="64a0e-221">Creating a Trello test user</span></span>

<span data-ttu-id="64a0e-222">En esta sección, creará un usuario llamado Britta Simon en Trello.</span><span class="sxs-lookup"><span data-stu-id="64a0e-222">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="64a0e-223">En esta sección, creará un usuario llamado Britta Simon en Trello.</span><span class="sxs-lookup"><span data-stu-id="64a0e-223">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="64a0e-224">Trello admite el aprovisionamiento Just-In-Time y se creará una nueva cuenta la primera vez que inicie una sesión en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64a0e-224">Trello supports just-in-time provisioning and a new account is created the first time you sign in from Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="64a0e-225">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="64a0e-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="64a0e-226">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Trello.</span><span class="sxs-lookup"><span data-stu-id="64a0e-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trello.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="64a0e-228">**Para asignar Britta Simon a Trello, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="64a0e-228">**To assign Britta Simon to Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="64a0e-229">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="64a0e-231">En la lista de aplicaciones, seleccione **Trello**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-231">In the applications list, select **Trello**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. <span data-ttu-id="64a0e-233">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="64a0e-235">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-235">Click **Add** button.</span></span> <span data-ttu-id="64a0e-236">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="64a0e-238">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="64a0e-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="64a0e-239">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="64a0e-240">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="64a0e-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="64a0e-241">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="64a0e-241">Testing single sign-on</span></span>

<span data-ttu-id="64a0e-242">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="64a0e-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="64a0e-243">Al hacer clic en el icono de Trello en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Trello.</span><span class="sxs-lookup"><span data-stu-id="64a0e-243">When you click the Trello tile in the Access Panel, you should get automatically signed-on to your Trello application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="64a0e-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="64a0e-244">Additional resources</span></span>

* [<span data-ttu-id="64a0e-245">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="64a0e-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="64a0e-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="64a0e-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png

