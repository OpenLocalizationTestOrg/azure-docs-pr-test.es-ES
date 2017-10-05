---
title: "Tutorial: Integración de Azure Active Directory con myPolicies | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y myPolicies."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bf79e858-1dfb-4ab3-a6df-74b2d5a878d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: jeedes
ms.openlocfilehash: fcb403041cb3a8bd20ff7b34aa5cc4b7bf0c0a16
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mypolicies"></a><span data-ttu-id="204da-103">Tutorial: Integración de Azure Active Directory con myPolicies</span><span class="sxs-lookup"><span data-stu-id="204da-103">Tutorial: Azure Active Directory integration with myPolicies</span></span>

<span data-ttu-id="204da-104">En este tutorial, obtendrá información sobre cómo integrar myPolicies con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="204da-104">In this tutorial, you learn how to integrate myPolicies with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="204da-105">La integración de myPolicies con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="204da-105">Integrating myPolicies with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="204da-106">Puede controlar en Azure AD quién tiene acceso a myPolicies</span><span class="sxs-lookup"><span data-stu-id="204da-106">You can control in Azure AD who has access to myPolicies</span></span>
- <span data-ttu-id="204da-107">Puede permitir que los usuarios inicien sesión automáticamente en myPolicies (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="204da-107">You can enable your users to automatically get signed-on to myPolicies (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="204da-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="204da-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="204da-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="204da-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="204da-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="204da-110">Prerequisites</span></span>

<span data-ttu-id="204da-111">Para configurar la integración de Azure AD con myPolicies, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="204da-111">To configure Azure AD integration with myPolicies, you need the following items:</span></span>

- <span data-ttu-id="204da-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="204da-112">An Azure AD subscription</span></span>
- <span data-ttu-id="204da-113">Una suscripción habilitada para el inicio de sesión único en myPolicies</span><span class="sxs-lookup"><span data-stu-id="204da-113">A myPolicies single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="204da-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="204da-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="204da-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="204da-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="204da-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="204da-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="204da-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="204da-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="204da-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="204da-118">Scenario description</span></span>
<span data-ttu-id="204da-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="204da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="204da-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="204da-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="204da-121">Agregación de myPolicies desde la galería</span><span class="sxs-lookup"><span data-stu-id="204da-121">Adding myPolicies from the gallery</span></span>
2. <span data-ttu-id="204da-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="204da-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mypolicies-from-the-gallery"></a><span data-ttu-id="204da-123">Agregación de myPolicies desde la galería</span><span class="sxs-lookup"><span data-stu-id="204da-123">Adding myPolicies from the gallery</span></span>
<span data-ttu-id="204da-124">Para configurar la integración de myPolicies en Azure AD, será preciso que agregue myPolicies desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="204da-124">To configure the integration of myPolicies into Azure AD, you need to add myPolicies from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="204da-125">**Para agregar myPolicies desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="204da-125">**To add myPolicies from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="204da-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="204da-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="204da-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="204da-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="204da-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="204da-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="204da-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="204da-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="204da-133">En el cuadro de búsqueda, escriba **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="204da-133">In the search box, type **myPolicies**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_search.png)

5. <span data-ttu-id="204da-135">En el panel de resultados, seleccione **myPolicies** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="204da-135">In the results panel, select **myPolicies**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="204da-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="204da-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="204da-138">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con myPolicies con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="204da-138">In this section, you configure and test Azure AD single sign-on with myPolicies based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="204da-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de myPolicies para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="204da-139">For single sign-on to work, Azure AD needs to know what the counterpart user in myPolicies is to a user in Azure AD.</span></span> <span data-ttu-id="204da-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de myPolicies.</span><span class="sxs-lookup"><span data-stu-id="204da-140">In other words, a link relationship between an Azure AD user and the related user in myPolicies needs to be established.</span></span>

<span data-ttu-id="204da-141">Para establecer la relación de vínculo, en myPolicies, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="204da-141">In myPolicies, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="204da-142">Para configurar y probar el inicio de sesión único de Azure AD con myPolicies, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="204da-142">To configure and test Azure AD single sign-on with myPolicies, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="204da-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="204da-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="204da-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="204da-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="204da-145">**[Creación de un usuario de prueba de myPolicies](#creating-a-mypolicies-test-user)**: el objetivo es tener un homólogo de Britta Simon en myPolicies que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="204da-145">**[Creating a myPolicies test user](#creating-a-mypolicies-test-user)** - to have a counterpart of Britta Simon in myPolicies that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="204da-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="204da-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="204da-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="204da-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="204da-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="204da-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="204da-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación myPolicies.</span><span class="sxs-lookup"><span data-stu-id="204da-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your myPolicies application.</span></span>

<span data-ttu-id="204da-150">**Para configurar el inicio de sesión único de Azure AD con myPolicies, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="204da-150">**To configure Azure AD single sign-on with myPolicies, perform the following steps:**</span></span>

1. <span data-ttu-id="204da-151">En Azure Portal, en la página de integración de la aplicación **myPolicies**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="204da-151">In the Azure portal, on the **myPolicies** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="204da-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="204da-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_samlbase.png)

3. <span data-ttu-id="204da-155">En la sección **Dominio y direcciones URL de myPolicies**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="204da-155">On the **myPolicies Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_url.png)

    <span data-ttu-id="204da-157">a.</span><span class="sxs-lookup"><span data-stu-id="204da-157">a.</span></span> <span data-ttu-id="204da-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<tenantname>.mypolicies.com/`</span><span class="sxs-lookup"><span data-stu-id="204da-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.mypolicies.com/`</span></span>

    <span data-ttu-id="204da-159">b.</span><span class="sxs-lookup"><span data-stu-id="204da-159">b.</span></span> <span data-ttu-id="204da-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`.</span><span class="sxs-lookup"><span data-stu-id="204da-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="204da-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="204da-161">These values are not real.</span></span> <span data-ttu-id="204da-162">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="204da-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="204da-163">Póngase en contacto con el [equipo de soporte técnico de myPolicies](mailto:support@mypolicies.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="204da-163">Contact [myPolicies support team](mailto:support@mypolicies.com) to get these values.</span></span>

4. <span data-ttu-id="204da-164">La aplicación myPolicies espera las aserciones de SAML en un formato específico, que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los atributos del token SAML.</span><span class="sxs-lookup"><span data-stu-id="204da-164">The myPolicies application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="204da-165">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="204da-165">Configure the following claims for this application.</span></span> <span data-ttu-id="204da-166">Puede administrar los valores de estos atributos en la sección "**Atributos de usuario**" de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="204da-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="204da-167">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="204da-167">The following screenshot shows an example for this.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_attribute.png)

5. <span data-ttu-id="204da-169">En la sección **Atributos de usuario**, active la casilla **Ver y editar todos los demás atributos de usuario** para expandir los atributos.</span><span class="sxs-lookup"><span data-stu-id="204da-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="204da-170">Realice los pasos siguientes en cada uno de los atributos mostrados:</span><span class="sxs-lookup"><span data-stu-id="204da-170">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="204da-171">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="204da-171">Attribute Name</span></span> | <span data-ttu-id="204da-172">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="204da-172">Attribute Value</span></span> |
    | ------------------- | ---------- |
    | <span data-ttu-id="204da-173">givenname</span><span class="sxs-lookup"><span data-stu-id="204da-173">givenname</span></span> | <span data-ttu-id="204da-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="204da-174">user.givenname</span></span> |
    | <span data-ttu-id="204da-175">surname</span><span class="sxs-lookup"><span data-stu-id="204da-175">surname</span></span> | <span data-ttu-id="204da-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="204da-176">user.surname</span></span> |
    | <span data-ttu-id="204da-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="204da-177">emailaddress</span></span> | <span data-ttu-id="204da-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="204da-178">user.mail</span></span> |
    | <span data-ttu-id="204da-179">name</span><span class="sxs-lookup"><span data-stu-id="204da-179">name</span></span> | <span data-ttu-id="204da-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="204da-180">user.userprincipalname</span></span> |
    
    <span data-ttu-id="204da-181">a.</span><span class="sxs-lookup"><span data-stu-id="204da-181">a.</span></span> <span data-ttu-id="204da-182">Haga clic en el atributo para abrir el cuadro de diálogo **Editar atributo**.</span><span class="sxs-lookup"><span data-stu-id="204da-182">Click on the attribute to open the **Edit Attribute** dialog.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="204da-184">b.</span><span class="sxs-lookup"><span data-stu-id="204da-184">b.</span></span> <span data-ttu-id="204da-185">Elimine el valor de la dirección URL en **Espacio de nombres**.</span><span class="sxs-lookup"><span data-stu-id="204da-185">Delete the URL value from the **Namespace**.</span></span>
    
    <span data-ttu-id="204da-186">c.</span><span class="sxs-lookup"><span data-stu-id="204da-186">c.</span></span> <span data-ttu-id="204da-187">Haga clic en **Aceptar** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="204da-187">Click **Ok** to save the setting.</span></span>
    
6. <span data-ttu-id="204da-188">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="204da-188">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_certificate.png) 

7. <span data-ttu-id="204da-190">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="204da-190">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="204da-192">En la sección **Configuración de myPolicies**, haga clic en **Configurar myPolicies** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="204da-192">On the **myPolicies Configuration** section, click **Configure myPolicies** to open **Configure sign-on** window.</span></span> <span data-ttu-id="204da-193">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="204da-193">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_configure.png) 

9. <span data-ttu-id="204da-195">Para configurar el inicio de sesión único en **myPolicies**, es preciso enviar el **certificado (Base64)** descargado y la **dirección URL del servicio de inicio de sesión único de SAML** al [equipo de soporte técnico de myPolicies](mailto:support@mypolicies.com).</span><span class="sxs-lookup"><span data-stu-id="204da-195">To configure single sign-on on **myPolicies** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [myPolicies support team](mailto:support@mypolicies.com).</span></span> 

> [!TIP]
> <span data-ttu-id="204da-196">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="204da-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="204da-197">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="204da-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="204da-198">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="204da-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="204da-199">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="204da-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="204da-200">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="204da-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="204da-202">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="204da-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="204da-203">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="204da-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="204da-205">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="204da-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="204da-207">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="204da-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="204da-209">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="204da-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="204da-211">a.</span><span class="sxs-lookup"><span data-stu-id="204da-211">a.</span></span> <span data-ttu-id="204da-212">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="204da-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="204da-213">b.</span><span class="sxs-lookup"><span data-stu-id="204da-213">b.</span></span> <span data-ttu-id="204da-214">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="204da-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="204da-215">c.</span><span class="sxs-lookup"><span data-stu-id="204da-215">c.</span></span> <span data-ttu-id="204da-216">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="204da-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="204da-217">d.</span><span class="sxs-lookup"><span data-stu-id="204da-217">d.</span></span> <span data-ttu-id="204da-218">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="204da-218">Click **Create**.</span></span>
 
### <a name="creating-a-mypolicies-test-user"></a><span data-ttu-id="204da-219">Creación de un usuario de prueba de myPolicies</span><span class="sxs-lookup"><span data-stu-id="204da-219">Creating a myPolicies test user</span></span>

<span data-ttu-id="204da-220">En esta sección, se crea un usuario denominado Britta Simon en myPolicies.</span><span class="sxs-lookup"><span data-stu-id="204da-220">In this section, you create a user called Britta Simon in myPolicies.</span></span> <span data-ttu-id="204da-221">Trabaje con el [equipo de soporte técnico de myPolicies](mailto:support@mypolicies.com) para agregar los usuarios a la plataforma de myPolicies.</span><span class="sxs-lookup"><span data-stu-id="204da-221">Work with [myPolicies support team](mailto:support@mypolicies.com) to add the users in the myPolicies platform.</span></span> <span data-ttu-id="204da-222">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="204da-222">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="204da-223">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="204da-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="204da-224">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a myPolicies.</span><span class="sxs-lookup"><span data-stu-id="204da-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to myPolicies.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="204da-226">**Para asignar a Britta Simon a myPolicies, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="204da-226">**To assign Britta Simon to myPolicies, perform the following steps:**</span></span>

1. <span data-ttu-id="204da-227">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="204da-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="204da-229">En la lista de aplicaciones, seleccione **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="204da-229">In the applications list, select **myPolicies**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_app.png) 

3. <span data-ttu-id="204da-231">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="204da-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="204da-233">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="204da-233">Click **Add** button.</span></span> <span data-ttu-id="204da-234">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="204da-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="204da-236">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="204da-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="204da-237">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="204da-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="204da-238">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="204da-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="204da-239">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="204da-239">Testing single sign-on</span></span>

<span data-ttu-id="204da-240">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="204da-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="204da-241">Al hacer clic en el icono de myPolicies en el panel de acceso, debe iniciar sesión automáticamente en su aplicación de myPolicies.</span><span class="sxs-lookup"><span data-stu-id="204da-241">When you click the myPolicies tile in the Access Panel, you should get automatically signed-on to your myPolicies application.</span></span>
<span data-ttu-id="204da-242">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="204da-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="204da-243">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="204da-243">Additional resources</span></span>

* [<span data-ttu-id="204da-244">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="204da-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="204da-245">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="204da-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_203.png

