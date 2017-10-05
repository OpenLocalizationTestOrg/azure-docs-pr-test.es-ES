---
title: "Tutorial: Integración de Azure Active Directory con LinkedIn Lookup | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y LinkedIn Lookup."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: e296431866a8611b30e72f286884890adf0f7e50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a><span data-ttu-id="47299-103">Tutorial: Integración de Azure Active Directory con LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="47299-103">Tutorial: Azure Active Directory integration with LinkedIn Lookup</span></span>

<span data-ttu-id="47299-104">En este tutorial, aprenderá a integrar LinkedIn Lookup con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="47299-104">In this tutorial, you learn how to integrate LinkedIn Lookup with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="47299-105">Integrar LinkedIn Lookup con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="47299-105">Integrating LinkedIn Lookup with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="47299-106">Puede controlar en Azure AD quién tiene acceso a LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="47299-106">You can control in Azure AD who has access to LinkedIn Lookup</span></span>
- <span data-ttu-id="47299-107">Puede permitir que los usuarios inicien sesión automáticamente en LinkedIn Lookup (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47299-107">You can enable your users to automatically get signed-on to LinkedIn Lookup (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="47299-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="47299-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="47299-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="47299-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47299-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="47299-110">Prerequisites</span></span>

<span data-ttu-id="47299-111">Para configurar la integración de Azure AD con LinkedIn Lookup, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="47299-111">To configure Azure AD integration with LinkedIn Lookup, you need the following items:</span></span>

- <span data-ttu-id="47299-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="47299-112">An Azure AD subscription</span></span>
- <span data-ttu-id="47299-113">Una suscripción habilitada para el inicio de sesión único en LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="47299-113">An LinkedIn Lookup single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="47299-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="47299-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="47299-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="47299-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="47299-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="47299-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="47299-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="47299-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="47299-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="47299-118">Scenario description</span></span>
<span data-ttu-id="47299-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="47299-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="47299-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="47299-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="47299-121">Adición de LinkedIn Lookup desde la galería</span><span class="sxs-lookup"><span data-stu-id="47299-121">Adding LinkedIn Lookup from the gallery</span></span>
2. <span data-ttu-id="47299-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="47299-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-lookup-from-the-gallery"></a><span data-ttu-id="47299-123">Adición de LinkedIn Lookup desde la galería</span><span class="sxs-lookup"><span data-stu-id="47299-123">Adding LinkedIn Lookup from the gallery</span></span>
<span data-ttu-id="47299-124">Para configurar la integración de LinkedIn Lookup en Azure AD, deberá agregar esta solución desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="47299-124">To configure the integration of LinkedIn Lookup into Azure AD, you need to add LinkedIn Lookup from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="47299-125">**Para agregar LinkedIn Lookup desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="47299-125">**To add LinkedIn Lookup from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="47299-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="47299-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="47299-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="47299-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="47299-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="47299-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="47299-131">Haga clic en el botón **Nueva aplicación** en la parte superior del cuadro de diálogo para agregar la nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="47299-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="47299-133">En el cuadro de búsqueda, escriba **LinkedIn Lookup**.</span><span class="sxs-lookup"><span data-stu-id="47299-133">In the search box, type **LinkedIn Lookup**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. <span data-ttu-id="47299-135">En el panel de resultados, seleccione **LinkedIn Lookup** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="47299-135">In the results panel, select **LinkedIn Lookup**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="47299-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="47299-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="47299-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con LinkedIn Lookup utilizando un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="47299-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Lookup based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="47299-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de LinkedIn Lookup para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47299-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Lookup is to a user in Azure AD.</span></span> <span data-ttu-id="47299-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="47299-140">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Lookup needs to be established.</span></span>

<span data-ttu-id="47299-141">Esta relación de vínculo se establece mediante la asignación del valor de **nombre de usuario** en Azure AD como valor de **Username** (Nombre de usuario) en LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="47299-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Lookup.</span></span>

<span data-ttu-id="47299-142">Para configurar y probar el inicio de sesión único de Azure AD con LinkedIn Lookup, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="47299-142">To configure and test Azure AD single sign-on with LinkedIn Lookup, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="47299-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="47299-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="47299-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="47299-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="47299-145">**[Creación de un usuario de prueba de LinkedIn Lookup](#creating-an-linkedin-lookup-test-user)**: para tener un homólogo de Britta Simon en LinkedIn Lookup que esté vinculado a la representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47299-145">**[Creating an LinkedIn Lookup test user](#creating-an-linkedin-lookup-test-user)** - to have a counterpart of Britta Simon in LinkedIn Lookup that is linked to the Azure AD representation.</span></span>
4. <span data-ttu-id="47299-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47299-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="47299-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="47299-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="47299-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="47299-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="47299-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="47299-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Lookup application.</span></span>

<span data-ttu-id="47299-150">**Para configurar el inicio de sesión único de Azure AD con LinkedIn Lookup, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="47299-150">**To configure Azure AD single sign-on with LinkedIn Lookup, perform the following steps:**</span></span>

1. <span data-ttu-id="47299-151">En la página de integración de la aplicación **LinkedIn Lookup** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="47299-151">In the Azure portal, on the **LinkedIn Lookup** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="47299-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="47299-153">On the **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. <span data-ttu-id="47299-155">En otra ventana del explorador web, inicie sesión como administrador en el sitio web de **LinkedIn Lookup**.</span><span class="sxs-lookup"><span data-stu-id="47299-155">In a different web browser window, sign-on to your **LinkedIn Lookup** website as an administrator.</span></span>

4. <span data-ttu-id="47299-156">En **Account Center** (Centro de cuentas), haga clic en **Global Settings** (Configuración global) en **Settings** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="47299-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="47299-157">Seleccione también **Lookup** en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="47299-157">Also, select **Lookup** from the dropdown list.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. <span data-ttu-id="47299-159">Haga clic en **OR Click Here to load and copy individual fields from the form** (O haga clic aquí para cargar y copiar campos individuales del formulario) y copie el **Id.de entidad** y la **Assertion Consumer Access (ACS) Url** (Url de Acceso de consumidor de aserciones [ACS]).</span><span class="sxs-lookup"><span data-stu-id="47299-159">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. <span data-ttu-id="47299-161">En la sección **Dominio y direcciones URL de LinkedIn Lookup** de Azure Portal, realice los siguientes pasos si quiere configurar la aplicación en el modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="47299-161">On Azure portal, under **LinkedIn Lookup Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    <span data-ttu-id="47299-163">a.</span><span class="sxs-lookup"><span data-stu-id="47299-163">a.</span></span> <span data-ttu-id="47299-164">En el cuadro de texto **Identificador**, escriba el **Id.de entidad** que copió de LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="47299-164">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="47299-165">b.</span><span class="sxs-lookup"><span data-stu-id="47299-165">b.</span></span> <span data-ttu-id="47299-166">En el cuadro de texto **URL de respuesta**, escriba la **Assertion Consumer Access (ACS) Url** (Url de Acceso de consumidor de aserciones [ACS]) que copió de LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="47299-166">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="47299-167">Active **Mostrar configuración avanzada de URL**, si desea volver a configurar la aplicación en modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="47299-167">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    <span data-ttu-id="47299-169">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`.</span><span class="sxs-lookup"><span data-stu-id="47299-169">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="47299-170">Este no es un valor real.</span><span class="sxs-lookup"><span data-stu-id="47299-170">This is not real value.</span></span> <span data-ttu-id="47299-171">El usuario tiene que actualizar estos valores con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="47299-171">The user has to update these values with the actual Sign-On URL.</span></span> <span data-ttu-id="47299-172">Póngase en contacto con el [equipo de soporte de cliente de LinkedIn Lookup](https://business.LinkedIn.com/lookup) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="47299-172">Contact [LinkedIn Lookup Client support team](https://business.LinkedIn.com/lookup) to get this value.</span></span>

8. <span data-ttu-id="47299-173">La aplicación **LinkedIn Lookup** espera las aserciones de SAML en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="47299-173">Your **LinkedIn Lookup** application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="47299-174">El usuario tiene que agregar asignaciones de atributo personalizadas a la configuración de atributos de token de SAML.</span><span class="sxs-lookup"><span data-stu-id="47299-174">The user has to add custom attribute mappings to the SAML token attributes configuration.</span></span> <span data-ttu-id="47299-175">La siguiente captura de pantalla muestra un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="47299-175">The following screenshot shows an example.</span></span> <span data-ttu-id="47299-176">El valor predeterminado de **Identificador de usuario** es **user.userprincipalname**, pero LinkedIn Lookup espera que este valor se asigne a la dirección de correo del usuario.</span><span class="sxs-lookup"><span data-stu-id="47299-176">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Lookup expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="47299-177">Para ello, puede usar el atributo **user.mail** de la lista o usar el valor de atributo correspondiente en función de la configuración de su organización.</span><span class="sxs-lookup"><span data-stu-id="47299-177">You can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. <span data-ttu-id="47299-179">En la sección **Atributos de usuario**, haga clic en **Ver y editar todos los demás atributos de usuario** y establezca los atributos.</span><span class="sxs-lookup"><span data-stu-id="47299-179">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="47299-180">El usuario debe agregar cuatro notificaciones denominadas **email**, **department**, **firstname** y **lastname**, y el valor que debe asignarse es **user.mail**, **user.department**, **user.givenname** y **user.surname**, respectivamente</span><span class="sxs-lookup"><span data-stu-id="47299-180">The user needs to add four claims named **email**,  **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="47299-181">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="47299-181">Attribute Name</span></span> | <span data-ttu-id="47299-182">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="47299-182">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="47299-183">email</span><span class="sxs-lookup"><span data-stu-id="47299-183">email</span></span>| <span data-ttu-id="47299-184">user.mail</span><span class="sxs-lookup"><span data-stu-id="47299-184">user.mail</span></span> |    
    | <span data-ttu-id="47299-185">department</span><span class="sxs-lookup"><span data-stu-id="47299-185">department</span></span>| <span data-ttu-id="47299-186">user.department</span><span class="sxs-lookup"><span data-stu-id="47299-186">user.department</span></span> |
    | <span data-ttu-id="47299-187">firstname</span><span class="sxs-lookup"><span data-stu-id="47299-187">firstname</span></span>| <span data-ttu-id="47299-188">user.givenname</span><span class="sxs-lookup"><span data-stu-id="47299-188">user.givenname</span></span> |
    | <span data-ttu-id="47299-189">lastname</span><span class="sxs-lookup"><span data-stu-id="47299-189">lastname</span></span>| <span data-ttu-id="47299-190">user.surname</span><span class="sxs-lookup"><span data-stu-id="47299-190">user.surname</span></span> |

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    <span data-ttu-id="47299-192">a.</span><span class="sxs-lookup"><span data-stu-id="47299-192">a.</span></span> <span data-ttu-id="47299-193">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="47299-193">Click **Add Attribute** to open the **Add Attribute** dialog.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    <span data-ttu-id="47299-196">b.</span><span class="sxs-lookup"><span data-stu-id="47299-196">b.</span></span> <span data-ttu-id="47299-197">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="47299-197">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="47299-198">c.</span><span class="sxs-lookup"><span data-stu-id="47299-198">c.</span></span> <span data-ttu-id="47299-199">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="47299-199">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="47299-200">d.</span><span class="sxs-lookup"><span data-stu-id="47299-200">d.</span></span> <span data-ttu-id="47299-201">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="47299-201">Click **Ok**</span></span>

10. <span data-ttu-id="47299-202">Realice los pasos siguientes en el atributo **name**.</span><span class="sxs-lookup"><span data-stu-id="47299-202">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="47299-203">a.</span><span class="sxs-lookup"><span data-stu-id="47299-203">a.</span></span> <span data-ttu-id="47299-204">Haga clic en el atributo para abrir la ventana **Editar atributo**.</span><span class="sxs-lookup"><span data-stu-id="47299-204">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    <span data-ttu-id="47299-206">b.</span><span class="sxs-lookup"><span data-stu-id="47299-206">b.</span></span> <span data-ttu-id="47299-207">Elimine el valor de dirección URL de **namespace**.</span><span class="sxs-lookup"><span data-stu-id="47299-207">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="47299-208">c.</span><span class="sxs-lookup"><span data-stu-id="47299-208">c.</span></span> <span data-ttu-id="47299-209">Haga clic en **Aceptar** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="47299-209">Click **Ok** to save the setting.</span></span>

10. <span data-ttu-id="47299-210">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="47299-210">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. <span data-ttu-id="47299-212">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="47299-212">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="47299-214">Vaya a la sección **LinkedIn Admin Settings** (Configuración de administrador de LinkedIn).</span><span class="sxs-lookup"><span data-stu-id="47299-214">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="47299-215">Cargue el archivo XML que ha descargado de Azure Portal haciendo clic en la opción **Upload XML file** (Cargar archivo XML).</span><span class="sxs-lookup"><span data-stu-id="47299-215">Upload the XML file you downloaded from the Azure portal by clicking the **Upload XML file** option.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. <span data-ttu-id="47299-217">Haga clic en **On** (Activar) para habilitar SSO.</span><span class="sxs-lookup"><span data-stu-id="47299-217">Click **On** to enable SSO.</span></span> <span data-ttu-id="47299-218">El estado de SSO cambiará de **Not Connected** (No conectado) a **Connected** (Conectado).</span><span class="sxs-lookup"><span data-stu-id="47299-218">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> <span data-ttu-id="47299-220">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="47299-220">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="47299-221">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="47299-221">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="47299-222">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="47299-222">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="47299-223">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="47299-223">Creating an Azure AD test user</span></span>
<span data-ttu-id="47299-224">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="47299-224">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="47299-226">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="47299-226">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="47299-227">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="47299-227">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="47299-229">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="47299-229">Go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="47299-231">Haga clic en **Agregar** para abrir el cuadro de diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="47299-231">Click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="47299-233">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="47299-233">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="47299-235">a.</span><span class="sxs-lookup"><span data-stu-id="47299-235">a.</span></span> <span data-ttu-id="47299-236">En el cuadro de texto **Nombre**, escriba **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="47299-236">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="47299-237">b.</span><span class="sxs-lookup"><span data-stu-id="47299-237">b.</span></span> <span data-ttu-id="47299-238">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="47299-238">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="47299-239">c.</span><span class="sxs-lookup"><span data-stu-id="47299-239">c.</span></span> <span data-ttu-id="47299-240">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="47299-240">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="47299-241">d.</span><span class="sxs-lookup"><span data-stu-id="47299-241">d.</span></span> <span data-ttu-id="47299-242">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="47299-242">Click **Create**.</span></span>
 
### <a name="creating-an-linkedin-lookup-test-user"></a><span data-ttu-id="47299-243">Creación de un usuario de prueba de LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="47299-243">Creating an LinkedIn Lookup test user</span></span>

<span data-ttu-id="47299-244">La aplicación Linked Lookup admite aprovisionamiento de usuarios Just-In-Time (JIT) y, tras la autenticación, los usuarios se crean automáticamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="47299-244">Linked Lookup Application supports Just in Time (JIT) user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="47299-245">Active **Automatically assign licenses** (Asignar licencias automáticamente) para asignar una licencia al usuario.</span><span class="sxs-lookup"><span data-stu-id="47299-245">Activate **Automatically assign licenses** to assign a license to the user.</span></span>
   
   ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="47299-247">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="47299-247">Assigning the Azure AD test user</span></span>

<span data-ttu-id="47299-248">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="47299-248">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Lookup.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="47299-250">**Para asignar Britta Simon a LinkedIn Lookup, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="47299-250">**To assign Britta Simon to LinkedIn Lookup, perform the following steps:**</span></span>

1. <span data-ttu-id="47299-251">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="47299-251">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="47299-253">En la lista de aplicaciones, seleccione **LinkedIn Lookup**.</span><span class="sxs-lookup"><span data-stu-id="47299-253">In the applications list, select **LinkedIn Lookup**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. <span data-ttu-id="47299-255">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="47299-255">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="47299-257">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="47299-257">Click **Add** button.</span></span> <span data-ttu-id="47299-258">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="47299-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="47299-260">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="47299-260">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="47299-261">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="47299-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="47299-262">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="47299-262">Click **Assign** button on **Add Assignment** dialog.</span></span>

    
### <a name="testing-single-sign-on"></a><span data-ttu-id="47299-263">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="47299-263">Testing single sign-on</span></span>

<span data-ttu-id="47299-264">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="47299-264">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="47299-265">Al hacer clic en el icono de LinkedIn Lookup del panel de acceso, debería redirigirse a la página de la organización donde tiene que indicar los detalles de su cuenta personal de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="47299-265">When you click the LinkedIn Lookup tile in the Access Panel, you should be redirected to Organizational page where you have to provide your personal LinkedIn account details.</span></span> <span data-ttu-id="47299-266">Esta página vincula su cuenta personal con su cuenta empresarial de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="47299-266">It links your personal account with your LinkedIn business account.</span></span> 

<span data-ttu-id="47299-267">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="47299-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="47299-268">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="47299-268">Additional resources</span></span>

* [<span data-ttu-id="47299-269">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47299-269">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="47299-270">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="47299-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

