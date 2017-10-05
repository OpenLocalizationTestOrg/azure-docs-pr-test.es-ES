---
title: "Tutorial: Integración de Azure Active Directory con LinkedIn Sales Navigator | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y LinkedIn Sales Navigator."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7a9fa8f3-d611-4ffe-8d50-04e9586b24da
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: ef26a16e79d9c9b0654634960b57dc59827b2c24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-sales-navigator"></a><span data-ttu-id="38a85-103">Tutorial: Integración de Azure Active Directory con LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="38a85-103">Tutorial: Azure Active Directory integration with LinkedIn Sales Navigator</span></span>

<span data-ttu-id="38a85-104">En este tutorial, aprenderá a integrar LinkedIn Sales Navigator con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="38a85-104">In this tutorial, you learn how to integrate LinkedIn Sales Navigator with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="38a85-105">La integración de LinkedIn Sales Navigator con Azure AD ofrece las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="38a85-105">Integrating LinkedIn Sales Navigator with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="38a85-106">Puede controlar en Azure AD quién tiene acceso a LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="38a85-106">You can control in Azure AD who has access to LinkedIn Sales Navigator</span></span>
- <span data-ttu-id="38a85-107">Puede permitir que los usuarios inicien sesión automáticamente en LinkedIn Sales Navigator (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38a85-107">You can enable your users to automatically get signed-on to LinkedIn Sales Navigator (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="38a85-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="38a85-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="38a85-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vaya a [¿Qué es el acceso a aplicaciones y el inicio de sesión único en Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="38a85-109">If you want to know more details about SaaS app integration with Azure AD, browse [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38a85-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="38a85-110">Prerequisites</span></span>

<span data-ttu-id="38a85-111">Para configurar la integración de Azure AD con LinkedIn Sales Navigator, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="38a85-111">To configure Azure AD integration with LinkedIn Sales Navigator, you need the following items:</span></span>

- <span data-ttu-id="38a85-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="38a85-112">An Azure AD subscription</span></span>
- <span data-ttu-id="38a85-113">Una suscripción habilitada para el inicio de sesión único en LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="38a85-113">A LinkedIn Sales Navigator single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="38a85-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="38a85-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="38a85-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="38a85-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="38a85-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="38a85-116">Avoid using your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="38a85-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="38a85-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="38a85-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="38a85-118">Scenario description</span></span>
<span data-ttu-id="38a85-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="38a85-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="38a85-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="38a85-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="38a85-121">Adición de LinkedIn Sales Navigator desde la galería</span><span class="sxs-lookup"><span data-stu-id="38a85-121">Adding LinkedIn Sales Navigator from the gallery</span></span>
2. <span data-ttu-id="38a85-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="38a85-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-sales-navigator-from-the-gallery"></a><span data-ttu-id="38a85-123">Adición de LinkedIn Sales Navigator desde la galería</span><span class="sxs-lookup"><span data-stu-id="38a85-123">Adding LinkedIn Sales Navigator from the gallery</span></span>
<span data-ttu-id="38a85-124">Para configurar la integración de LinkedIn Sales Navigator en Azure AD, deberá agregar LinkedIn Sales Navigator desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="38a85-124">To configure the integration of LinkedIn Sales Navigator into Azure AD, you need to add LinkedIn Sales Navigator from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="38a85-125">**Para agregar LinkedIn Sales Navigator desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="38a85-125">**To add LinkedIn Sales Navigator from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="38a85-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="38a85-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="38a85-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="38a85-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="38a85-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="38a85-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="38a85-131">Haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="38a85-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="38a85-133">En el cuadro de búsqueda, escriba **LinkedIn Sales Navigator**.</span><span class="sxs-lookup"><span data-stu-id="38a85-133">In the search box, type **LinkedIn Sales Navigator**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_search.png)

5. <span data-ttu-id="38a85-135">En el panel de resultados, seleccione **LinkedIn Sales Navigator** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="38a85-135">In the results panel, select **LinkedIn Sales Navigator**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="38a85-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="38a85-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="38a85-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con LinkedIn Sales Navigator con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="38a85-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Sales Navigator based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="38a85-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de LinkedIn Sales Navigator para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38a85-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Sales Navigator is to a user in Azure AD.</span></span> <span data-ttu-id="38a85-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="38a85-140">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Sales Navigator needs to be established.</span></span>

<span data-ttu-id="38a85-141">Esta relación de vínculo se establece mediante la asignación del valor de **nombre de usuario** en Azure AD como valor de **Username** (Nombre de usuario) en LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="38a85-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Sales Navigator.</span></span>

<span data-ttu-id="38a85-142">Para configurar y probar el inicio de sesión único de Azure AD con LinkedIn Sales Navigator, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="38a85-142">To configure and test Azure AD single sign-on with LinkedIn Sales Navigator, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="38a85-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="38a85-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="38a85-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="38a85-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="38a85-145">**[Creación de un usuario de prueba de LinkedIn Sales Navigator](#creating-a-linkedin-sales-navigator-test-user)**: para tener un homólogo de Britta Simon en LinkedIn Sales Navigator que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38a85-145">**[Creating a LinkedIn Sales Navigator test user](#creating-a-linkedin-sales-navigator-test-user)** - to have a counterpart of Britta Simon in LinkedIn Sales Navigator that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="38a85-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38a85-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="38a85-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="38a85-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="38a85-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="38a85-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="38a85-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="38a85-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Sales Navigator application.</span></span>

<span data-ttu-id="38a85-150">**Para configurar el inicio de sesión único de Azure AD con LinkedIn Sales Navigator, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="38a85-150">**To configure Azure AD single sign-on with LinkedIn Sales Navigator, perform the following steps:**</span></span>

1. <span data-ttu-id="38a85-151">En la página de integración de la aplicación **LinkedIn Sales Navigator** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="38a85-151">In the Azure portal, on the **LinkedIn Sales Navigator** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="38a85-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="38a85-153">On the **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_samlbase.png)

3. <span data-ttu-id="38a85-155">En otra ventana del explorador web, inicie sesión como administrador en el sitio web de **LinkedIn Sales Navigator**.</span><span class="sxs-lookup"><span data-stu-id="38a85-155">In a different web browser window, sign-on to your **LinkedIn Sales Navigator** website as an administrator.</span></span>

4. <span data-ttu-id="38a85-156">En **Account Center** (Centro de cuentas), haga clic en **Global Settings** (Configuración global) en **Settings** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="38a85-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="38a85-157">Además, seleccione **Sales Navigator** de la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="38a85-157">Also, select **Sales Navigator** from the dropdown list.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="38a85-159">Haga clic en **OR Click Here to load and copy individual fields from the form** (O haga clic aquí para cargar y copiar campos individuales del formulario) y copie el **Id.de entidad** y la **Assertion Consumer Access (ACS) Url** (Url de Acceso de consumidor de aserciones [ACS]).</span><span class="sxs-lookup"><span data-stu-id="38a85-159">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_031.png)

6. <span data-ttu-id="38a85-161">En la sección **Dominio y direcciones URL de LinkedIn Sales Navigator** de Azure Portal, realice los siguientes pasos si quiere configurar la aplicación en el modo iniciado por **IDP**.</span><span class="sxs-lookup"><span data-stu-id="38a85-161">On Azure portal, under **LinkedIn Sales Navigator Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url1.png)

    <span data-ttu-id="38a85-163">a.</span><span class="sxs-lookup"><span data-stu-id="38a85-163">a.</span></span> <span data-ttu-id="38a85-164">En el cuadro de texto **Identificador**, escriba el **Id.de entidad** que copió de LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="38a85-164">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="38a85-165">b.</span><span class="sxs-lookup"><span data-stu-id="38a85-165">b.</span></span> <span data-ttu-id="38a85-166">En el cuadro de texto **URL de respuesta**, escriba la **Assertion Consumer Access (ACS) Url** (Url de Acceso de consumidor de aserciones [ACS]) que copió de LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="38a85-166">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="38a85-167">Active **Mostrar configuración avanzada de URL**, si quiere configurar la aplicación en modo iniciado por **SP**.</span><span class="sxs-lookup"><span data-stu-id="38a85-167">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url2.png)

    <span data-ttu-id="38a85-169">En el cuadro de texto **URL de inicio de sesión**, escriba el valor con el siguiente patrón: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span><span class="sxs-lookup"><span data-stu-id="38a85-169">In the **Sign-on URL** textbox, type the value using the following pattern: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span></span>

8. <span data-ttu-id="38a85-170">La aplicación **LinkedIn Sales Navigator** espera las aserciones de SAML en un formato específico, lo que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los atributos del token de SAML.</span><span class="sxs-lookup"><span data-stu-id="38a85-170">Your **LinkedIn Sales Navigator** application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="38a85-171">La siguiente captura de pantalla muestra un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="38a85-171">The following screenshot shows an example.</span></span> <span data-ttu-id="38a85-172">El valor predeterminado de **Identificador de usuario** es **user.userprincipalname**, pero LinkedIn Sales Navigator espera que este valor se asigne a la dirección de correo del usuario.</span><span class="sxs-lookup"><span data-stu-id="38a85-172">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Sales Navigator expects it to be mapped with the user's email address.</span></span> <span data-ttu-id="38a85-173">Para ello, puede usar el atributo **user.mail** de la lista o usar el valor de atributo correspondiente en función de la configuración de su organización.</span><span class="sxs-lookup"><span data-stu-id="38a85-173">You can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/updateusermail.png)
    
9. <span data-ttu-id="38a85-175">En la sección **Atributos de usuario**, haga clic en **Ver y editar todos los demás atributos de usuario** y establezca los atributos.</span><span class="sxs-lookup"><span data-stu-id="38a85-175">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="38a85-176">El usuario debe agregar cuatro notificaciones denominadas **email**, **department**, **firstname** y **lastname**, y el valor que debe asignarse es **user.mail**, **user.department**, **user.givenname** y **user.surname**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="38a85-176">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="38a85-177">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="38a85-177">Attribute Name</span></span> | <span data-ttu-id="38a85-178">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="38a85-178">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="38a85-179">email</span><span class="sxs-lookup"><span data-stu-id="38a85-179">email</span></span>| <span data-ttu-id="38a85-180">user.mail</span><span class="sxs-lookup"><span data-stu-id="38a85-180">user.mail</span></span> |
    | <span data-ttu-id="38a85-181">department</span><span class="sxs-lookup"><span data-stu-id="38a85-181">department</span></span>| <span data-ttu-id="38a85-182">user.department</span><span class="sxs-lookup"><span data-stu-id="38a85-182">user.department</span></span> |
    | <span data-ttu-id="38a85-183">firstname</span><span class="sxs-lookup"><span data-stu-id="38a85-183">firstname</span></span>| <span data-ttu-id="38a85-184">user.givenname</span><span class="sxs-lookup"><span data-stu-id="38a85-184">user.givenname</span></span> |
    | <span data-ttu-id="38a85-185">lastname</span><span class="sxs-lookup"><span data-stu-id="38a85-185">lastname</span></span>| <span data-ttu-id="38a85-186">user.surname</span><span class="sxs-lookup"><span data-stu-id="38a85-186">user.surname</span></span> |
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/userattribute.png)
    
    <span data-ttu-id="38a85-188">a.</span><span class="sxs-lookup"><span data-stu-id="38a85-188">a.</span></span> <span data-ttu-id="38a85-189">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo de atributos.</span><span class="sxs-lookup"><span data-stu-id="38a85-189">Click on **Add Attribute** to open the attribute dialog.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_04.png)
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_05.png)
   
    <span data-ttu-id="38a85-192">b.</span><span class="sxs-lookup"><span data-stu-id="38a85-192">b.</span></span> <span data-ttu-id="38a85-193">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="38a85-193">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="38a85-194">c.</span><span class="sxs-lookup"><span data-stu-id="38a85-194">c.</span></span> <span data-ttu-id="38a85-195">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="38a85-195">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="38a85-196">d.</span><span class="sxs-lookup"><span data-stu-id="38a85-196">d.</span></span> <span data-ttu-id="38a85-197">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="38a85-197">Click **Ok**</span></span>

10. <span data-ttu-id="38a85-198">Realice los pasos siguientes en el atributo **name**.</span><span class="sxs-lookup"><span data-stu-id="38a85-198">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="38a85-199">a.</span><span class="sxs-lookup"><span data-stu-id="38a85-199">a.</span></span> <span data-ttu-id="38a85-200">Haga clic en el atributo para abrir la ventana **Editar atributo**.</span><span class="sxs-lookup"><span data-stu-id="38a85-200">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/url_update.png)

    <span data-ttu-id="38a85-202">b.</span><span class="sxs-lookup"><span data-stu-id="38a85-202">b.</span></span> <span data-ttu-id="38a85-203">Elimine el valor de dirección URL de **namespace**.</span><span class="sxs-lookup"><span data-stu-id="38a85-203">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="38a85-204">c.</span><span class="sxs-lookup"><span data-stu-id="38a85-204">c.</span></span> <span data-ttu-id="38a85-205">Haga clic en **Aceptar** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="38a85-205">Click **Ok** to save the setting.</span></span>

11. <span data-ttu-id="38a85-206">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="38a85-206">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_certificate.png) 

12. <span data-ttu-id="38a85-208">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="38a85-208">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="38a85-210">Vaya a la sección **LinkedIn Admin Settings** (Configuración de administrador de LinkedIn).</span><span class="sxs-lookup"><span data-stu-id="38a85-210">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="38a85-211">Haga clic en **Upload XML file** (Cargar archivo XML) para cargar el archivo XML de metadatos que acaba de descargar de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="38a85-211">Click **Upload XML file** to upload the Metadata XML file that you have downloaded from the Azure portal.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="38a85-213">Haga clic en **On** (Activar) para habilitar SSO.</span><span class="sxs-lookup"><span data-stu-id="38a85-213">Click **On** to enable SSO.</span></span> <span data-ttu-id="38a85-214">El estado de SSO cambiará de **Not Connected** (No conectado) a **Connected** (Conectado).</span><span class="sxs-lookup"><span data-stu-id="38a85-214">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_05.png)


> [!TIP]
> <span data-ttu-id="38a85-216">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="38a85-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="38a85-217">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="38a85-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="38a85-218">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="38a85-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="38a85-219">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="38a85-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="38a85-220">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="38a85-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="38a85-222">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="38a85-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="38a85-223">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="38a85-223">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="38a85-225">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="38a85-225">Go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="38a85-227">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="38a85-227">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="38a85-229">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="38a85-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="38a85-231">a.</span><span class="sxs-lookup"><span data-stu-id="38a85-231">a.</span></span> <span data-ttu-id="38a85-232">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="38a85-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="38a85-233">b.</span><span class="sxs-lookup"><span data-stu-id="38a85-233">b.</span></span> <span data-ttu-id="38a85-234">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="38a85-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="38a85-235">c.</span><span class="sxs-lookup"><span data-stu-id="38a85-235">c.</span></span> <span data-ttu-id="38a85-236">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="38a85-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="38a85-237">d.</span><span class="sxs-lookup"><span data-stu-id="38a85-237">d.</span></span> <span data-ttu-id="38a85-238">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="38a85-238">Click **Create**.</span></span>
 
### <a name="creating-a-linkedin-sales-navigator-test-user"></a><span data-ttu-id="38a85-239">Creación de un usuario de prueba de LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="38a85-239">Creating a LinkedIn Sales Navigator test user</span></span>

<span data-ttu-id="38a85-240">La aplicación LinkedIn Sales Navigator admite aprovisionamiento de usuarios Just-In-Time (JIT) y, tras la autenticación, los usuarios se crearán automáticamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="38a85-240">Linked Sales Navigator Application supports Just in Time (JIT) user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="38a85-241">Active **Automatically assign licenses** (Asignar licencias automáticamente) para asignar una licencia al usuario.</span><span class="sxs-lookup"><span data-stu-id="38a85-241">Activate **Automatically assign licenses** to assign a license to the user.</span></span>
   
   ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="38a85-243">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="38a85-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="38a85-244">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="38a85-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Sales Navigator.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="38a85-246">**Para asignar Britta Simon a LinkedIn Sales Navigator, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="38a85-246">**To assign Britta Simon to LinkedIn Sales Navigator, perform the following steps:**</span></span>

1. <span data-ttu-id="38a85-247">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="38a85-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="38a85-249">En la lista de aplicaciones, seleccione **LinkedIn Sales Navigator**.</span><span class="sxs-lookup"><span data-stu-id="38a85-249">In the applications list, select **LinkedIn Sales Navigator**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_app.png) 

3. <span data-ttu-id="38a85-251">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="38a85-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="38a85-253">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="38a85-253">Click **Add** button.</span></span> <span data-ttu-id="38a85-254">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="38a85-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="38a85-256">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="38a85-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="38a85-257">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="38a85-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="38a85-258">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="38a85-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="38a85-259">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="38a85-259">Testing single sign-on</span></span>

<span data-ttu-id="38a85-260">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="38a85-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="38a85-261">Al hacer clic en el icono de LinkedIn Sales Navigator del panel de acceso, debería redirigirse a la página de la organización donde tiene que indicar los detalles de su cuenta personal de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="38a85-261">When you click the LinkedIn Sales Navigator tile in the Access Panel, you should be redirected to Organizational page where you have to provide your personal LinkedIn account details.</span></span> <span data-ttu-id="38a85-262">Esta página vincula su cuenta personal con su cuenta empresarial de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="38a85-262">It links your personal account with your LinkedIn business account.</span></span> <span data-ttu-id="38a85-263">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="38a85-263">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="38a85-264">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="38a85-264">Additional resources</span></span>

* [<span data-ttu-id="38a85-265">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="38a85-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="38a85-266">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="38a85-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_203.png

