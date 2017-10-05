---
title: "Tutorial: Integración de Azure Active Directory con LinkedIn Learning | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y LinkedIn Learning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 6ad28cb3adaa63ddc3d3769a650d26ca6a7e2695
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="4c9b7-103">Tutorial: Integración de Azure Active Directory con LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="4c9b7-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="4c9b7-104">En este tutorial, aprenderá a integrar LinkedIn Learning con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4c9b7-104">In this tutorial, you learn how to integrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4c9b7-105">Integrar LinkedIn Learning con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="4c9b7-105">Integrating LinkedIn Learning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4c9b7-106">Puede controlar en Azure AD quién tiene acceso a LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="4c9b7-106">You can control in Azure AD who has access to LinkedIn Learning</span></span>
- <span data-ttu-id="4c9b7-107">Puede permitir que los usuarios inicien sesión automáticamente en LinkedIn Learning (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-107">You can enable your users to automatically get signed-on to LinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4c9b7-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4c9b7-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4c9b7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c9b7-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4c9b7-110">Prerequisites</span></span>

<span data-ttu-id="4c9b7-111">Para configurar la integración de Azure AD con LinkedIn Learning, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4c9b7-111">To configure Azure AD integration with LinkedIn Learning, you need the following items:</span></span>

- <span data-ttu-id="4c9b7-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c9b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4c9b7-113">Una suscripción habilitada para el inicio de sesión único en LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="4c9b7-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4c9b7-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4c9b7-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="4c9b7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4c9b7-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4c9b7-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c9b7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4c9b7-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="4c9b7-118">Scenario description</span></span>
<span data-ttu-id="4c9b7-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4c9b7-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="4c9b7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4c9b7-121">Agregar LinkedIn Learning desde la galería</span><span class="sxs-lookup"><span data-stu-id="4c9b7-121">Adding LinkedIn Learning from the gallery</span></span>
2. <span data-ttu-id="4c9b7-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c9b7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-the-gallery"></a><span data-ttu-id="4c9b7-123">Agregar LinkedIn Learning desde la galería</span><span class="sxs-lookup"><span data-stu-id="4c9b7-123">Adding LinkedIn Learning from the gallery</span></span>
<span data-ttu-id="4c9b7-124">Para configurar la integración de LinkedIn Learning en Azure AD, deberá agregar esta solución desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-124">To configure the integration of LinkedIn Learning into Azure AD, you need to add LinkedIn Learning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4c9b7-125">**Para agregar LinkedIn Learning desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="4c9b7-125">**To add LinkedIn Learning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4c9b7-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4c9b7-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4c9b7-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="4c9b7-131">Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="4c9b7-133">En el cuadro de búsqueda, escriba **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-133">In the search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="4c9b7-134">En el panel de resultados, haga clic en **LinkedIn Learning** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-134">From results panel, click **LinkedIn Learning** to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4c9b7-136">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c9b7-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4c9b7-137">En esta sección, configurará y probará el inicio de sesión único de Azure AD con LinkedIn Learning utilizando usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4c9b7-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4c9b7-138">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de LinkedIn Learning para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Learning is to a user in Azure AD.</span></span> <span data-ttu-id="4c9b7-139">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Learning needs to be established.</span></span>

<span data-ttu-id="4c9b7-140">Esta relación de vínculo se establece mediante la asignación del valor de **nombre de usuario** en Azure AD como valor de **Username** (Nombre de usuario) en LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="4c9b7-141">Para configurar y probar el inicio de sesión único de Azure AD con LinkedIn Learning, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="4c9b7-141">To configure and test Azure AD single sign-on with LinkedIn Learning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4c9b7-142">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4c9b7-143">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4c9b7-144">**[Creación de un usuario de prueba de LinkedIn Learning](#creating-a-linkedin-learning-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="4c9b7-145">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4c9b7-146">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4c9b7-147">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c9b7-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4c9b7-148">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="4c9b7-149">**Para configurar el inicio de sesión único de Azure AD con LinkedIn Learning, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="4c9b7-149">**To configure Azure AD single sign-on with LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="4c9b7-150">En la página de integración de la aplicación **LinkedIn Learning** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-150">In the Azure portal, on the **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="4c9b7-152">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="4c9b7-154">En otra ventana del explorador web, inicie sesión como administrador en el inquilino LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-154">In a different web browser window, sign-on to your LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="4c9b7-155">En **Account Center** (Centro de cuentas), haga clic en **Global Settings** (Configuración global) en **Settings** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="4c9b7-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="4c9b7-156">Seleccione también **Learning - Default** (Learning - Predeterminado) en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-156">Also, select **Learning - Default** from the dropdown list.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="4c9b7-158">Haga clic en **OR Click Here to load and copy individual fields from the form** (O haga clic aquí para cargar y copiar campos individuales del formulario) y copie el **Id.de entidad** y la **Assertion Consumer Access (ACS) Url** (Url de Acceso de consumidor de aserciones [ACS]).</span><span class="sxs-lookup"><span data-stu-id="4c9b7-158">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="4c9b7-160">En Azure Portal, en **Dominio y direcciones URL de LinkedIn Learning**, realice los pasos siguientes si quiere configurar SSO en modo **Iniciado por IdP**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="4c9b7-162">a.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-162">a.</span></span> <span data-ttu-id="4c9b7-163">En el cuadro de texto **Identificador**, escriba el **Id.de entidad** que copió de LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="4c9b7-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="4c9b7-164">b.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-164">b.</span></span> <span data-ttu-id="4c9b7-165">En el cuadro de texto **URL de respuesta**, escriba la **Assertion Consumer Access (ACS) Url** (Url de Acceso de consumidor de aserciones [ACS]) que copió de LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="4c9b7-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="4c9b7-166">Si quiere configurar SSO en modo **Iniciado por SP**, haga clic en la opción de configuración Mostrar configuración avanzada de URL en la sección de configuración y configure la URL de inicio de sesión con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="4c9b7-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign-on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="4c9b7-168">La aplicación LinkedIn Learning espera las aserciones de SAML en un formato específico, lo que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los atributos del token de SAML.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-168">Your LinkedIn Learning application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="4c9b7-169">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="4c9b7-170">El valor predeterminado de **Identificador de usuario** es **user.userprincipalname**, pero LinkedIn Learning espera que este valor se asigne a la dirección de correo del usuario.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="4c9b7-171">Para ello, puede usar el atributo **user.mail** de la lista o usar el valor de atributo correspondiente en función de la configuración de su organización.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="4c9b7-173">En la sección **Atributos de usuario**, haga clic en **Ver y editar todos los demás atributos de usuario** y establezca los atributos.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="4c9b7-174">El usuario debe agregar cuatro notificaciones denominadas **email**, **department**, **firstname** y **lastname**, y el valor que debe asignarse es **user.mail**, **user.department**, **user.givenname** y **user.surname**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-174">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="4c9b7-175">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="4c9b7-175">Attribute Name</span></span> | <span data-ttu-id="4c9b7-176">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="4c9b7-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="4c9b7-177">email</span><span class="sxs-lookup"><span data-stu-id="4c9b7-177">email</span></span>| <span data-ttu-id="4c9b7-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="4c9b7-178">user.mail</span></span> |    
    | <span data-ttu-id="4c9b7-179">department</span><span class="sxs-lookup"><span data-stu-id="4c9b7-179">department</span></span>| <span data-ttu-id="4c9b7-180">user.department</span><span class="sxs-lookup"><span data-stu-id="4c9b7-180">user.department</span></span> |
    | <span data-ttu-id="4c9b7-181">firstname</span><span class="sxs-lookup"><span data-stu-id="4c9b7-181">firstname</span></span>| <span data-ttu-id="4c9b7-182">user.givenname</span><span class="sxs-lookup"><span data-stu-id="4c9b7-182">user.givenname</span></span> |
    | <span data-ttu-id="4c9b7-183">lastname</span><span class="sxs-lookup"><span data-stu-id="4c9b7-183">lastname</span></span>| <span data-ttu-id="4c9b7-184">user.surname</span><span class="sxs-lookup"><span data-stu-id="4c9b7-184">user.surname</span></span> |
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="4c9b7-186">a.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-186">a.</span></span> <span data-ttu-id="4c9b7-187">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo de atributos.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-187">Click **Add Attribute** to open the attribute dialog.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="4c9b7-190">b.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-190">b.</span></span> <span data-ttu-id="4c9b7-191">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-191">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="4c9b7-192">c.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-192">c.</span></span> <span data-ttu-id="4c9b7-193">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-193">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="4c9b7-194">d.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-194">d.</span></span> <span data-ttu-id="4c9b7-195">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-195">Click **Ok**</span></span>

10. <span data-ttu-id="4c9b7-196">Realice los pasos siguientes en el atributo **name**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-196">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="4c9b7-197">a.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-197">a.</span></span> <span data-ttu-id="4c9b7-198">Haga clic en el atributo para abrir la ventana **Editar atributo**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-198">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    <span data-ttu-id="4c9b7-200">b.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-200">b.</span></span> <span data-ttu-id="4c9b7-201">Elimine el valor de dirección URL de **namespace**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-201">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="4c9b7-202">c.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-202">c.</span></span> <span data-ttu-id="4c9b7-203">Haga clic en **Aceptar** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-203">Click **Ok** to save the setting.</span></span>

11. <span data-ttu-id="4c9b7-204">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-204">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. <span data-ttu-id="4c9b7-206">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-206">Click **Save**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="4c9b7-208">Vaya a la sección **LinkedIn Admin Settings** (Configuración de administrador de LinkedIn).</span><span class="sxs-lookup"><span data-stu-id="4c9b7-208">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="4c9b7-209">Cargue el archivo XML que ha descargado de Azure Portal. Para ello, haga clic en la opción Upload XML file (Cargar archivo XML).</span><span class="sxs-lookup"><span data-stu-id="4c9b7-209">Upload the XML file you downloaded from the Azure portal by clicking the Upload XML file option.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="4c9b7-211">Haga clic en **On** (Activar) para habilitar SSO.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-211">Click **On** to enable SSO.</span></span> <span data-ttu-id="4c9b7-212">El estado de SSO cambiará de **Not Connected** (No conectado) a **Connected** (Conectado).</span><span class="sxs-lookup"><span data-stu-id="4c9b7-212">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4c9b7-214">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c9b7-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="4c9b7-215">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4c9b7-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="4c9b7-217">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="4c9b7-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4c9b7-218">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4c9b7-220">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4c9b7-222">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-222">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4c9b7-224">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="4c9b7-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4c9b7-226">a.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-226">a.</span></span> <span data-ttu-id="4c9b7-227">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4c9b7-228">b.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-228">b.</span></span> <span data-ttu-id="4c9b7-229">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4c9b7-230">c.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-230">c.</span></span> <span data-ttu-id="4c9b7-231">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4c9b7-232">d.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-232">d.</span></span> <span data-ttu-id="4c9b7-233">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-233">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="4c9b7-234">Creación de un usuario de prueba de LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="4c9b7-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="4c9b7-235">La aplicación LinkedIn Learning admite</span><span class="sxs-lookup"><span data-stu-id="4c9b7-235">Linked Learning Application supports.</span></span> <span data-ttu-id="4c9b7-236">aprovisionamiento de usuarios Just-In-Time y, tras la autenticación, los usuarios se crean automáticamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-236">Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="4c9b7-237">En la página de configuración del administrador del portal de LinkedIn Learning, invierta el conmutador **Automatically Assign licenses** (Asignar licencias automáticamente) a activo para habilitar el aprovisionamiento Just-In-Time y este también asignará una licencia al usuario.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-237">On the admin settings page on the LinkedIn Learning portal flip the switch **Automatically Assign licenses** to active to enable Just in time provisioning and this will also assign a license to the user.</span></span>
   
   ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4c9b7-239">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c9b7-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4c9b7-240">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Learning.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="4c9b7-242">**Para asignar Britta Simon a LinkedIn Learning, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="4c9b7-242">**To assign Britta Simon to LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="4c9b7-243">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="4c9b7-245">En la lista de aplicaciones, seleccione **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-245">In the applications list, select **LinkedIn Learning**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="4c9b7-247">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="4c9b7-249">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-249">Click **Add** button.</span></span> <span data-ttu-id="4c9b7-250">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="4c9b7-252">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4c9b7-253">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4c9b7-254">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4c9b7-255">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="4c9b7-255">Testing single sign-on</span></span>

<span data-ttu-id="4c9b7-256">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4c9b7-257">Al hacer clic en el icono de LinkedIn Learning del panel de acceso, debería abrirse la página de inicio de sesión único de Azure y, después de iniciar sesión, debería entrar en la aplicación LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="4c9b7-257">When you click the LinkedIn Learning tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4c9b7-258">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4c9b7-258">Additional resources</span></span>

* [<span data-ttu-id="4c9b7-259">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c9b7-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4c9b7-260">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4c9b7-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png