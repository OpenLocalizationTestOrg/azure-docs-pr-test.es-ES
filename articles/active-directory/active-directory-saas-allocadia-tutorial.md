---
title: "Tutorial: integración de Azure Active Directory con Allocadia | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Allocadia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c415fc55-6dc1-49f2-a8a2-2fc6e3790d65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: jeedes
ms.openlocfilehash: 8e97c365383ecdb72cc1cd449b522b75875fc1db
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-allocadia"></a><span data-ttu-id="ef2b8-103">Tutorial: Integración de Azure Active Directory con Allocadia</span><span class="sxs-lookup"><span data-stu-id="ef2b8-103">Tutorial: Azure Active Directory integration with Allocadia</span></span>

<span data-ttu-id="ef2b8-104">En este tutorial, obtendrá información sobre cómo integrar Allocadia con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ef2b8-104">In this tutorial, you learn how to integrate Allocadia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ef2b8-105">Integración de Allocadia con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ef2b8-105">Integrating Allocadia with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ef2b8-106">Puede controlar en Azure AD quién tiene acceso a Allocadia</span><span class="sxs-lookup"><span data-stu-id="ef2b8-106">You can control in Azure AD who has access to Allocadia</span></span>
- <span data-ttu-id="ef2b8-107">Puede permitir que los usuarios inicien sesión automáticamente en Allocadia (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef2b8-107">You can enable your users to automatically get signed-on to Allocadia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ef2b8-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ef2b8-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ef2b8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef2b8-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ef2b8-110">Prerequisites</span></span>

<span data-ttu-id="ef2b8-111">Para configurar la integración de Azure AD con Allocadia, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ef2b8-111">To configure Azure AD integration with Allocadia, you need the following items:</span></span>

- <span data-ttu-id="ef2b8-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef2b8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ef2b8-113">Una suscripción habilitada para el inicio de sesión único en Allocadia</span><span class="sxs-lookup"><span data-stu-id="ef2b8-113">An Allocadia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ef2b8-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ef2b8-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ef2b8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ef2b8-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ef2b8-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ef2b8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ef2b8-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="ef2b8-118">Scenario description</span></span>
<span data-ttu-id="ef2b8-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ef2b8-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="ef2b8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ef2b8-121">Incorporación de Allocadia desde la galería</span><span class="sxs-lookup"><span data-stu-id="ef2b8-121">Adding Allocadia from the gallery</span></span>
2. <span data-ttu-id="ef2b8-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef2b8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-allocadia-from-the-gallery"></a><span data-ttu-id="ef2b8-123">Incorporación de Allocadia desde la galería</span><span class="sxs-lookup"><span data-stu-id="ef2b8-123">Adding Allocadia from the gallery</span></span>
<span data-ttu-id="ef2b8-124">Para configurar la integración de Allocadia en Azure AD, es preciso agregar Allocadia desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-124">To configure the integration of Allocadia into Azure AD, you need to add Allocadia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ef2b8-125">**Para agregar Allocadia desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="ef2b8-125">**To add Allocadia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ef2b8-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ef2b8-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ef2b8-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="ef2b8-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="ef2b8-133">En el cuadro de búsqueda, escriba **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-133">In the search box, type **Allocadia**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_search.png)

5. <span data-ttu-id="ef2b8-135">En el panel de resultados, seleccione **Allocadia** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-135">In the results panel, select **Allocadia**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ef2b8-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef2b8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ef2b8-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Allocadia con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ef2b8-138">In this section, you configure and test Azure AD single sign-on with Allocadia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ef2b8-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Allocadia para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Allocadia is to a user in Azure AD.</span></span> <span data-ttu-id="ef2b8-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Allocadia.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-140">In other words, a link relationship between an Azure AD user and the related user in Allocadia needs to be established.</span></span>

<span data-ttu-id="ef2b8-141">Para establecer la relación de vínculo, en Allocadia, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-141">In Allocadia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ef2b8-142">Para configurar y probar el inicio de sesión único de Azure AD con Allocadia, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ef2b8-142">To configure and test Azure AD single sign-on with Allocadia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ef2b8-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ef2b8-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ef2b8-145">**[Creación de un usuario de prueba de Allocadia](#creating-an-allocadia-test-user)**: para tener un homólogo de Britta Simon en Allocadia que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-145">**[Creating an Allocadia test user](#creating-an-allocadia-test-user)** - to have a counterpart of Britta Simon in Allocadia that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ef2b8-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ef2b8-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ef2b8-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef2b8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ef2b8-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Allocadia.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Allocadia application.</span></span>

<span data-ttu-id="ef2b8-150">**Para configurar el inicio de sesión único de Azure AD con Allocadia, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="ef2b8-150">**To configure Azure AD single sign-on with Allocadia, perform the following steps:**</span></span>

1. <span data-ttu-id="ef2b8-151">En Azure Portal, en la página de integración de la aplicación **Allocadia**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-151">In the Azure portal, on the **Allocadia** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="ef2b8-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_samlbase.png)

3. <span data-ttu-id="ef2b8-155">En la sección **Dominio y direcciones URL de Allocadia**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ef2b8-155">On the **Allocadia Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_url.png)

    <span data-ttu-id="ef2b8-157">a.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-157">a.</span></span> <span data-ttu-id="ef2b8-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="ef2b8-158">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
       
     <span data-ttu-id="ef2b8-159">Para el entorno de prueba - `https://na2standby.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="ef2b8-159">For test environment -  `https://na2standby.allocadia.com`</span></span>
    
     <span data-ttu-id="ef2b8-160">Para el entorno de producción - `https://na2.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="ef2b8-160">For production environment - `https://na2.allocadia.com`</span></span>

    <span data-ttu-id="ef2b8-161">b.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-161">b.</span></span> <span data-ttu-id="ef2b8-162">En el cuadro de texto **URL de respuesta** , escriba una dirección URL con los siguientes patrones:</span><span class="sxs-lookup"><span data-stu-id="ef2b8-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    
     <span data-ttu-id="ef2b8-163">Para el entorno de prueba - `https://na2standby.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="ef2b8-163">For test environment - `https://na2standby.allocadia.com/allocadia/saml/SSO`</span></span>
    
     <span data-ttu-id="ef2b8-164">Para el entorno de producción - `https://na2.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="ef2b8-164">For production environment - `https://na2.allocadia.com/allocadia/saml/SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ef2b8-165">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-165">These values are not real.</span></span> <span data-ttu-id="ef2b8-166">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-166">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="ef2b8-167">Póngase en contacto con el [equipo de soporte técnico de Allocadia](mailTo:support@allocadia.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-167">Contact [Allocadia support team](mailTo:support@allocadia.com) to get these values.</span></span>

4. <span data-ttu-id="ef2b8-168">La aplicación Allocadia espera las aserciones de SAML en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-168">Allocadia application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="ef2b8-169">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-169">Configure the following claims for this application.</span></span> <span data-ttu-id="ef2b8-170">Puede administrar los valores de estos atributos en la sección "**Atributos de usuario**" de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="ef2b8-171">En la siguiente captura de pantalla se muestra un ejemplo de esta configuración.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-171">The following screenshot shows an example for this configuration.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_attributes.png)
    
5. <span data-ttu-id="ef2b8-173">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo token de SAML como muestra la imagen y siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ef2b8-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="ef2b8-174">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="ef2b8-174">Attribute Name</span></span> | <span data-ttu-id="ef2b8-175">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="ef2b8-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="ef2b8-176">firstname</span><span class="sxs-lookup"><span data-stu-id="ef2b8-176">firstname</span></span> | <span data-ttu-id="ef2b8-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="ef2b8-177">user.givenname</span></span> |
    | <span data-ttu-id="ef2b8-178">lastname</span><span class="sxs-lookup"><span data-stu-id="ef2b8-178">lastname</span></span> | <span data-ttu-id="ef2b8-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="ef2b8-179">user.surname</span></span> |
    | <span data-ttu-id="ef2b8-180">email</span><span class="sxs-lookup"><span data-stu-id="ef2b8-180">email</span></span> | <span data-ttu-id="ef2b8-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="ef2b8-181">user.mail</span></span> |
    
    <span data-ttu-id="ef2b8-182">a.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-182">a.</span></span> <span data-ttu-id="ef2b8-183">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="ef2b8-185">b.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-185">b.</span></span> <span data-ttu-id="ef2b8-186">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ef2b8-188">c.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-188">c.</span></span> <span data-ttu-id="ef2b8-189">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-189">From the **Value** list, type the attribute value shown for that row.</span></span>
 
    <span data-ttu-id="ef2b8-190">d.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-190">d.</span></span> <span data-ttu-id="ef2b8-191">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-191">Click **Ok**.</span></span>



6. <span data-ttu-id="ef2b8-192">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-192">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_certificate.png) 


7. <span data-ttu-id="ef2b8-194">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="ef2b8-194">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-allocadia-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ef2b8-196">Para configurar el inicio de sesión único en **Allocadia**, debe enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Allocadia](mailTo:support@allocadia.com).</span><span class="sxs-lookup"><span data-stu-id="ef2b8-196">To configure single sign-on on **Allocadia** side, you need to send the downloaded **Metadata XML** to [Allocadia support team](mailTo:support@allocadia.com).</span></span> <span data-ttu-id="ef2b8-197">Ellos se encargan de realizar esta configuración para que la conexión de SSO de SAML esté establecida correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-197">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ef2b8-198">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ef2b8-199">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ef2b8-200">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ef2b8-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ef2b8-201">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef2b8-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="ef2b8-202">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ef2b8-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="ef2b8-204">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="ef2b8-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ef2b8-205">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ef2b8-207">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ef2b8-209">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ef2b8-211">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="ef2b8-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ef2b8-213">a.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-213">a.</span></span> <span data-ttu-id="ef2b8-214">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ef2b8-215">b.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-215">b.</span></span> <span data-ttu-id="ef2b8-216">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ef2b8-217">c.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-217">c.</span></span> <span data-ttu-id="ef2b8-218">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ef2b8-219">d.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-219">d.</span></span> <span data-ttu-id="ef2b8-220">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-220">Click **Create**.</span></span>
 
### <a name="creating-an-allocadia-test-user"></a><span data-ttu-id="ef2b8-221">Creación de un usuario de prueba de Allocadia</span><span class="sxs-lookup"><span data-stu-id="ef2b8-221">Creating an Allocadia test user</span></span>

<span data-ttu-id="ef2b8-222">La aplicación admite aprovisionamiento de usuarios Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-222">Application supports Just in time user provisioning.</span></span> <span data-ttu-id="ef2b8-223">Después se crean usuarios de autenticación en la aplicación automáticamente.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-223">After authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ef2b8-224">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef2b8-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ef2b8-225">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Allocadia.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Allocadia.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="ef2b8-227">**Para asignar Britta Simon a Allocadia, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="ef2b8-227">**To assign Britta Simon to Allocadia, perform the following steps:**</span></span>

1. <span data-ttu-id="ef2b8-228">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="ef2b8-230">En la lista de aplicaciones, seleccione **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-230">In the applications list, select **Allocadia**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_app.png) 

3. <span data-ttu-id="ef2b8-232">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="ef2b8-234">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-234">Click **Add** button.</span></span> <span data-ttu-id="ef2b8-235">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="ef2b8-237">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ef2b8-238">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ef2b8-239">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ef2b8-240">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="ef2b8-240">Testing single sign-on</span></span>

<span data-ttu-id="ef2b8-241">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ef2b8-242">Al hacer clic en el icono de Allocadia en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Allocadia.</span><span class="sxs-lookup"><span data-stu-id="ef2b8-242">When you click the Allocadia tile in the Access Panel, you should get automatically signed-on to your Allocadia application.</span></span>
<span data-ttu-id="ef2b8-243">Para más información sobre el Panel de acceso, consulte la [introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ef2b8-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ef2b8-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ef2b8-244">Additional resources</span></span>

* [<span data-ttu-id="ef2b8-245">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ef2b8-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ef2b8-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ef2b8-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_203.png

