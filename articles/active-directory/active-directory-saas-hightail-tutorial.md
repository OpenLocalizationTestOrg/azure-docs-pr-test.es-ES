---
title: "Tutorial: integración de Azure Active Directory con Hightail | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Hightail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: ba55f9b62d274aa3eb91723c62b53f54de0891b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="61770-103">Tutorial: Integración de Azure Active Directory con Hightail</span><span class="sxs-lookup"><span data-stu-id="61770-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="61770-104">En este tutorial, aprenderá a integrar Hightail con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="61770-104">In this tutorial, you learn how to integrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="61770-105">Integrar Hightail con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="61770-105">Integrating Hightail with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="61770-106">Puede controlar en Azure AD quién tiene acceso a Hightail.</span><span class="sxs-lookup"><span data-stu-id="61770-106">You can control in Azure AD who has access to Hightail</span></span>
- <span data-ttu-id="61770-107">Puede permitir que los usuarios inicien sesión automáticamente en Hightail (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61770-107">You can enable your users to automatically get signed-on to Hightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="61770-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="61770-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="61770-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="61770-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61770-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="61770-110">Prerequisites</span></span>

<span data-ttu-id="61770-111">Para configurar la integración de Azure AD con Hightail, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="61770-111">To configure Azure AD integration with Hightail, you need the following items:</span></span>

- <span data-ttu-id="61770-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="61770-112">An Azure AD subscription</span></span>
- <span data-ttu-id="61770-113">Una suscripción habilitada para el inicio de sesión único en Hightail</span><span class="sxs-lookup"><span data-stu-id="61770-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="61770-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="61770-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="61770-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="61770-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="61770-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="61770-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="61770-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="61770-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="61770-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="61770-118">Scenario description</span></span>
<span data-ttu-id="61770-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="61770-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="61770-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="61770-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="61770-121">Adición de Hightail desde la galería</span><span class="sxs-lookup"><span data-stu-id="61770-121">Adding Hightail from the gallery</span></span>
2. <span data-ttu-id="61770-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="61770-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-the-gallery"></a><span data-ttu-id="61770-123">Adición de Hightail desde la galería</span><span class="sxs-lookup"><span data-stu-id="61770-123">Adding Hightail from the gallery</span></span>
<span data-ttu-id="61770-124">Para configurar la integración de Hightail en Azure AD, será preciso que agregue Hightail desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="61770-124">To configure the integration of Hightail into Azure AD, you need to add Hightail from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="61770-125">**Para agregar Hightail desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="61770-125">**To add Hightail from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="61770-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="61770-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="61770-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="61770-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="61770-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="61770-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="61770-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="61770-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="61770-133">En el cuadro de búsqueda, escriba **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="61770-133">In the search box, type **Hightail**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. <span data-ttu-id="61770-135">En el panel de resultados, seleccione **Hightail** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61770-135">In the results panel, select **Hightail**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="61770-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="61770-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="61770-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Hightail con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="61770-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="61770-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Hightail para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61770-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Hightail is to a user in Azure AD.</span></span> <span data-ttu-id="61770-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Hightail.</span><span class="sxs-lookup"><span data-stu-id="61770-140">In other words, a link relationship between an Azure AD user and the related user in Hightail needs to be established.</span></span>

<span data-ttu-id="61770-141">Para establecer la relación de vínculo, en Hightail, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="61770-141">In Hightail, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="61770-142">Para configurar y probar el inicio de sesión único de Azure AD con Hightail, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="61770-142">To configure and test Azure AD single sign-on with Hightail, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="61770-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="61770-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="61770-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="61770-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="61770-145">**[Crear un usuario de prueba de Hightail](#creating-a-hightail-test-user)** : para tener un homólogo de Britta Simon en Hightail que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61770-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - to have a counterpart of Britta Simon in Hightail that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="61770-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61770-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="61770-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="61770-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="61770-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="61770-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="61770-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Hightail.</span><span class="sxs-lookup"><span data-stu-id="61770-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="61770-150">**Para configurar el inicio de sesión único de Azure AD con Hightail, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="61770-150">**To configure Azure AD single sign-on with Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="61770-151">En Azure Portal, en la página de integración de la aplicación **Hightail**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="61770-151">In the Azure portal, on the **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="61770-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="61770-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. <span data-ttu-id="61770-155">En la sección **Dominio y direcciones URL de Hightail**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="61770-155">On the **Hightail Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     <span data-ttu-id="61770-157">En el cuadro de texto **URL de respuesta**, escriba la dirección URL como se muestra a continuación: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span><span class="sxs-lookup"><span data-stu-id="61770-157">In the **Reply URL** textbox, type the URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="61770-158">El valor anterior no es real.</span><span class="sxs-lookup"><span data-stu-id="61770-158">The preceding value is not real value.</span></span> <span data-ttu-id="61770-159">El valor se actualizará con la dirección URL de respuesta real, que se explica más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="61770-159">You will update the value with the actual Reply URL, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="61770-160">En la sección **Dominio y direcciones URL de Hightail**, si quiere configurar la aplicación en **SP initiated mode** (Modo iniciado por SP), realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="61770-160">On the **Hightail Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="61770-162">a.</span><span class="sxs-lookup"><span data-stu-id="61770-162">a.</span></span> <span data-ttu-id="61770-163">Haga clic en **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="61770-163">Click the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="61770-164">b.</span><span class="sxs-lookup"><span data-stu-id="61770-164">b.</span></span> <span data-ttu-id="61770-165">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL similar a la siguiente: `https://www.hightail.com/loginSSO`</span><span class="sxs-lookup"><span data-stu-id="61770-165">In the **Sign On URL** textbox, type the URL as: `https://www.hightail.com/loginSSO`</span></span>

4. <span data-ttu-id="61770-166">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="61770-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. <span data-ttu-id="61770-168">La aplicación Hightail espera las aserciones de SAML en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="61770-168">Hightail application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="61770-169">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="61770-169">Please configure the following claims for this application.</span></span> <span data-ttu-id="61770-170">Puede administrar el valor de estos atributos desde la pestaña **"Atributo"** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61770-170">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="61770-171">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="61770-171">The following screenshot shows an example for this.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. <span data-ttu-id="61770-173">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo token de SAML como muestra la imagen y siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="61770-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="61770-174">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="61770-174">Attribute Name</span></span> | <span data-ttu-id="61770-175">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="61770-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="61770-176">Nombre</span><span class="sxs-lookup"><span data-stu-id="61770-176">FirstName</span></span> | <span data-ttu-id="61770-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="61770-177">user.givenname</span></span> |
    | <span data-ttu-id="61770-178">Apellidos</span><span class="sxs-lookup"><span data-stu-id="61770-178">LastName</span></span> | <span data-ttu-id="61770-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="61770-179">user.surname</span></span> |
    | <span data-ttu-id="61770-180">Email</span><span class="sxs-lookup"><span data-stu-id="61770-180">Email</span></span> | <span data-ttu-id="61770-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="61770-181">user.mail</span></span> |    
    | <span data-ttu-id="61770-182">UserIdentity</span><span class="sxs-lookup"><span data-stu-id="61770-182">UserIdentity</span></span> | <span data-ttu-id="61770-183">user.mail</span><span class="sxs-lookup"><span data-stu-id="61770-183">user.mail</span></span> |
    
    <span data-ttu-id="61770-184">a.</span><span class="sxs-lookup"><span data-stu-id="61770-184">a.</span></span> <span data-ttu-id="61770-185">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="61770-185">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="61770-188">b.</span><span class="sxs-lookup"><span data-stu-id="61770-188">b.</span></span> <span data-ttu-id="61770-189">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="61770-189">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="61770-190">c.</span><span class="sxs-lookup"><span data-stu-id="61770-190">c.</span></span> <span data-ttu-id="61770-191">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="61770-191">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="61770-192">d.</span><span class="sxs-lookup"><span data-stu-id="61770-192">d.</span></span> <span data-ttu-id="61770-193">Deje **Espacio de nombres** en blanco.</span><span class="sxs-lookup"><span data-stu-id="61770-193">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="61770-194">e.</span><span class="sxs-lookup"><span data-stu-id="61770-194">e.</span></span> <span data-ttu-id="61770-195">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="61770-195">Click **Ok**.</span></span>

7. <span data-ttu-id="61770-196">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="61770-196">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="61770-198">En la sección **Configuración de Hightail**, haga clic en **Configurar Hightail** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="61770-198">On the **Hightail Configuration** section, click **Configure Hightail** to open **Configure sign-on** window.</span></span> <span data-ttu-id="61770-199">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="61770-199">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    ><span data-ttu-id="61770-201">Antes de configurar el inicio de sesión único en la aplicación Hightail, incluya su dominio de correo electrónico en la lista de permitidos con el equipo Hightail para que todos aquellos que utilicen este dominio puedan emplear la funcionalidad de inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="61770-201">Before configuring the Single Sign On at Hightail app, please white list your email domain with Hightail team so that all the users who are using this domain can use Single Sign On functionality.</span></span>


9. <span data-ttu-id="61770-202">Para configurar SSO para la aplicación, debe iniciar sesión en su inquilino de Hightail como administrador.</span><span class="sxs-lookup"><span data-stu-id="61770-202">To get SSO configured for your application, you need to sign-on to your Hightail tenant as an administrator.</span></span>
   
    <span data-ttu-id="61770-203">a.</span><span class="sxs-lookup"><span data-stu-id="61770-203">a.</span></span> <span data-ttu-id="61770-204">En el menú de la parte superior, haga clic en la pestaña **Account** (Cuenta) y seleccione **Configure SAML** (Configurar SAML).</span><span class="sxs-lookup"><span data-stu-id="61770-204">In the menu on the top, click the **Account** tab and select **Configure SAML**.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    <span data-ttu-id="61770-206">b.</span><span class="sxs-lookup"><span data-stu-id="61770-206">b.</span></span> <span data-ttu-id="61770-207">Active la casilla **Enable SAML Authentication**(Habilitar autenticación SAML).</span><span class="sxs-lookup"><span data-stu-id="61770-207">Select the checkbox of **Enable SAML Authentication**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    <span data-ttu-id="61770-209">c.</span><span class="sxs-lookup"><span data-stu-id="61770-209">c.</span></span> <span data-ttu-id="61770-210">Abra el certificado codificado en base 64 descargado de Azure Portal en el Bloc de notas, copie su contenido en el Portapapeles y luego péguelo en el cuadro de texto **SAML Token Signing Certificate** (Certificado de firmas de token SAML).</span><span class="sxs-lookup"><span data-stu-id="61770-210">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Token Signing Certificate** textbox.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    <span data-ttu-id="61770-212">d.</span><span class="sxs-lookup"><span data-stu-id="61770-212">d.</span></span> <span data-ttu-id="61770-213">En el cuadro de texto **SAML Authority (Identity Provider)** [Autoridad de SAML (proveedor de identidades)], pegue el valor de **Dirección URL de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="61770-213">In the **SAML Authority (Identity Provider)** textbox, paste the value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    <span data-ttu-id="61770-215">e.</span><span class="sxs-lookup"><span data-stu-id="61770-215">e.</span></span> <span data-ttu-id="61770-216">Si desea configurar la aplicación en el **modo iniciado por el proveedor de identidades**, seleccione **"Identity Provider (IdP) initiated log in"** ("Inicio de sesión iniciado por el proveedor de identidades").</span><span class="sxs-lookup"><span data-stu-id="61770-216">If you wish to configure the application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="61770-217">Si prefiere el **modo iniciado por el proveedor de servicios**, seleccione **"Service Provider (SP) initiated log in"** ("Inicio de sesión iniciado por el proveedor de servicios").</span><span class="sxs-lookup"><span data-stu-id="61770-217">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    <span data-ttu-id="61770-219">f.</span><span class="sxs-lookup"><span data-stu-id="61770-219">f.</span></span> <span data-ttu-id="61770-220">Copie la dirección URL del consumidor de SAML de la instancia y péguela en el cuadro de texto **URL de respuesta** de la sección **Dominio y direcciones URL de Hightail** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="61770-220">Copy the SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="61770-221">g.</span><span class="sxs-lookup"><span data-stu-id="61770-221">g.</span></span> <span data-ttu-id="61770-222">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="61770-222">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="61770-223">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61770-223">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="61770-224">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="61770-224">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="61770-225">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="61770-225">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="61770-226">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="61770-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="61770-227">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="61770-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="61770-229">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="61770-229">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="61770-230">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="61770-230">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="61770-232">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="61770-232">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="61770-234">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="61770-234">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="61770-236">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="61770-236">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="61770-238">a.</span><span class="sxs-lookup"><span data-stu-id="61770-238">a.</span></span> <span data-ttu-id="61770-239">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="61770-239">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="61770-240">b.</span><span class="sxs-lookup"><span data-stu-id="61770-240">b.</span></span> <span data-ttu-id="61770-241">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="61770-241">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="61770-242">c.</span><span class="sxs-lookup"><span data-stu-id="61770-242">c.</span></span> <span data-ttu-id="61770-243">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="61770-243">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="61770-244">d.</span><span class="sxs-lookup"><span data-stu-id="61770-244">d.</span></span> <span data-ttu-id="61770-245">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="61770-245">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="61770-246">Crear un usuario de prueba de Hightail</span><span class="sxs-lookup"><span data-stu-id="61770-246">Creating a Hightail test user</span></span>

<span data-ttu-id="61770-247">El objetivo de esta sección es crear un usuario llamado Britta Simon en Hightail.</span><span class="sxs-lookup"><span data-stu-id="61770-247">The objective of this section is to create a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="61770-248">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="61770-248">There is no action item for you in this section.</span></span> <span data-ttu-id="61770-249">Hightail admite el aprovisionamiento Just-In-Time de usuarios en función de las notificaciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="61770-249">Hightail supports just-in-time user provisioning based on the custom claims.</span></span> <span data-ttu-id="61770-250">Si ha configurado las notificaciones personalizadas como se muestra en la anterior sección **[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** , se creará automáticamente un usuario en la aplicación, si es que todavía no existe uno.</span><span class="sxs-lookup"><span data-stu-id="61770-250">If you have configured the custom claims as shown in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in the application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="61770-251">Si necesita crear un usuario manualmente, debe ponerse en contacto con el [equipo de soporte técnico de Hightail](mailto:support@hightail.com).</span><span class="sxs-lookup"><span data-stu-id="61770-251">If you need to create a user manually, you need to contact the [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="61770-252">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="61770-252">Assigning the Azure AD test user</span></span>

<span data-ttu-id="61770-253">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure, para lo que le concederá acceso a Hightail.</span><span class="sxs-lookup"><span data-stu-id="61770-253">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Hightail.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="61770-255">**Para asignar a Britta Simon a Hightail, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="61770-255">**To assign Britta Simon to Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="61770-256">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="61770-256">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="61770-258">En la lista de aplicaciones, seleccione **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="61770-258">In the applications list, select **Hightail**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. <span data-ttu-id="61770-260">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="61770-260">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="61770-262">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="61770-262">Click **Add** button.</span></span> <span data-ttu-id="61770-263">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="61770-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="61770-265">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="61770-265">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="61770-266">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="61770-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="61770-267">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="61770-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="61770-268">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="61770-268">Testing single sign-on</span></span>

<span data-ttu-id="61770-269">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="61770-269">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="61770-270">Al hacer clic en el icono de Hightail en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Hightail.</span><span class="sxs-lookup"><span data-stu-id="61770-270">When you click the Hightail tile in the Access Panel, you should get automatically signed-on to your Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="61770-271">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="61770-271">Additional resources</span></span>

* [<span data-ttu-id="61770-272">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="61770-272">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="61770-273">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="61770-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

