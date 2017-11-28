---
title: "Tutorial: Integración de Azure Active Directory con LinkedIn Elevate | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y LinkedIn Elevate."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 5336543e06d60be555722a615568b12048c2aa2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a><span data-ttu-id="4d2ba-103">Tutorial: Integración de Azure Active Directory con LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="4d2ba-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span></span>

<span data-ttu-id="4d2ba-104">En este tutorial, aprenderá a integrar LinkedIn Elevate con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4d2ba-104">In this tutorial, you learn how to integrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4d2ba-105">Integrar LinkedIn Elevate con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="4d2ba-105">Integrating LinkedIn Elevate with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4d2ba-106">Puede controlar en Azure AD quién tiene acceso a LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="4d2ba-106">You can control in Azure AD who has access to LinkedIn Elevate</span></span>
- <span data-ttu-id="4d2ba-107">Puede permitir que los usuarios inicien sesión automáticamente en LinkedIn Elevate (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-107">You can enable your users to automatically get signed-on to LinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4d2ba-108">Puede administrar sus cuentas en una ubicación central: el Portal de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="4d2ba-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4d2ba-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d2ba-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4d2ba-110">Prerequisites</span></span>

<span data-ttu-id="4d2ba-111">Para configurar la integración de Azure AD con LinkedIn Elevate, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4d2ba-111">To configure Azure AD integration with LinkedIn Elevate, you need the following items:</span></span>

- <span data-ttu-id="4d2ba-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d2ba-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4d2ba-113">Una suscripción habilitada para el inicio de sesión único en LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="4d2ba-113">A LinkedIn Elevate single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4d2ba-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4d2ba-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="4d2ba-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4d2ba-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="4d2ba-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4d2ba-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4d2ba-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="4d2ba-118">Scenario description</span></span>
<span data-ttu-id="4d2ba-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4d2ba-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="4d2ba-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4d2ba-121">Agregar LinkedIn Elevate desde la galería</span><span class="sxs-lookup"><span data-stu-id="4d2ba-121">Adding LinkedIn Elevate from the gallery</span></span>
2. <span data-ttu-id="4d2ba-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d2ba-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-elevate-from-the-gallery"></a><span data-ttu-id="4d2ba-123">Agregar LinkedIn Elevate desde la galería</span><span class="sxs-lookup"><span data-stu-id="4d2ba-123">Adding LinkedIn Elevate from the gallery</span></span>
<span data-ttu-id="4d2ba-124">Para configurar la integración de LinkedIn Elevate en Azure AD, deberá agregar LinkedIn Elevate desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-124">To configure the integration of LinkedIn Elevate into Azure AD, you need to add LinkedIn Elevate from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4d2ba-125">**Para agregar LinkedIn Elevate desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="4d2ba-125">**To add LinkedIn Elevate from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4d2ba-126">En el panel de navegación izquierdo del **[Portal de administración de Azure](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4d2ba-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4d2ba-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="4d2ba-131">Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="4d2ba-133">En el cuadro de búsqueda, escriba **LinkedIn Elevate**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-133">In the search box, type **LinkedIn Elevate**.</span></span> <span data-ttu-id="4d2ba-134">En el panel de resultados, haga clic en **LinkedIn Elevate** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-134">From results panel, click **LinkedIn Elevate** to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4d2ba-136">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d2ba-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4d2ba-137">En esta sección, configurará y probará el inicio de sesión único de Azure AD con LinkedIn Elevate utilizando usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4d2ba-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4d2ba-138">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de LinkedIn Elevate para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Elevate is to a user in Azure AD.</span></span> <span data-ttu-id="4d2ba-139">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Elevate needs to be established.</span></span>

<span data-ttu-id="4d2ba-140">Esta relación de vínculo se establece mediante la asignación del valor de **nombre de usuario** en Azure AD como valor de **Username** (Nombre de usuario) en LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Elevate.</span></span>

<span data-ttu-id="4d2ba-141">Para configurar y probar el inicio de sesión único de Azure AD con LinkedIn Elevate, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="4d2ba-141">To configure and test Azure AD single sign-on with LinkedIn Elevate, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4d2ba-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4d2ba-143">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4d2ba-144">**[Creación de un usuario de prueba de LinkedIn Elevate](#creating-a-linkedin-elevate-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="4d2ba-145">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4d2ba-146">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4d2ba-147">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d2ba-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4d2ba-148">En esta sección, habilitará el inicio de sesión único de Azure AD en el Portal de administración de Azure y configurará el inicio de sesión único en la aplicación LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-148">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span></span>

<span data-ttu-id="4d2ba-149">**Para configurar el inicio de sesión único de Azure AD con LinkedIn Elevate, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="4d2ba-149">**To configure Azure AD single sign-on with LinkedIn Elevate, perform the following steps:**</span></span>

1. <span data-ttu-id="4d2ba-150">En el Portal de administración de Azure, en la página de integración de la aplicación **LinkedIn Elevate**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-150">In the Azure Management portal, on the **LinkedIn Elevate** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="4d2ba-152">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-152">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="4d2ba-154">En otra ventana del explorador web, inicie sesión como administrador en el inquilino LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-154">In a different web browser window, sign-on to your LinkedIn Elevate tenant as an administrator.</span></span>

4. <span data-ttu-id="4d2ba-155">En **Account Center** (Centro de cuentas), haga clic en **Global Settings** (Configuración global) en **Settings** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="4d2ba-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="4d2ba-156">Además, seleccione **Elevate - Elevate AAD Test** en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-156">Also, select **Elevate - Elevate AAD Test** from the dropdown list.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="4d2ba-158">Haga clic en **OR Click Here to load and copy individual fields from the form** (O haga clic aquí para cargar y copiar campos individuales del formulario) y copie el **Id.de entidad** y la **Assertion Consumer Access (ACS) Url** (Url de Acceso de consumidor de aserciones [ACS])</span><span class="sxs-lookup"><span data-stu-id="4d2ba-158">Click on **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="4d2ba-160">En Azure Portal, en **Dominio y direcciones URL de LinkedIn Elevate**, realice los pasos siguientes si quiere configurar SSO en modo **Iniciado por IDP**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="4d2ba-162">a.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-162">a.</span></span> <span data-ttu-id="4d2ba-163">En el cuadro de texto **Identificador**, escriba el **Id.de entidad** que copió de LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="4d2ba-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="4d2ba-164">b.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-164">b.</span></span> <span data-ttu-id="4d2ba-165">En el cuadro de texto **URL de respuesta**, escriba la **Assertion Consumer Access (ACS) Url** (Url de Acceso de consumidor de aserciones [ACS]) que copió de LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="4d2ba-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="4d2ba-166">Si quiere configurar SSO en modo **SP Initiated**, haga clic en la opción de configuración Mostrar configuración avanzada de URL en la sección de configuración y configure la URL de inicio de sesión con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="4d2ba-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. <span data-ttu-id="4d2ba-168">La aplicación LinkedIn Elevate espera las aserciones de SAML en un formato específico, lo que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los atributos del token de SAML.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-168">Your LinkedIn Elevate application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="4d2ba-169">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="4d2ba-170">El valor predeterminado de **Identificador de usuario** es **user.userprincipalname**, pero LinkedIn Elevate espera que este valor se asigne a la dirección de correo del usuario.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="4d2ba-171">Para ello, puede usar el atributo **user.mail** de la lista o usar el valor de atributo correspondiente en función de la configuración de su organización.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. <span data-ttu-id="4d2ba-173">En la sección **Atributos de usuario**, haga clic en **Ver y editar todos los demás atributos de usuario** y establezca los atributos.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="4d2ba-174">Tiene que agregar otra notificación denominada **department** y hay que asignar el valor a **user.department**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-174">You need to add another claim named **department** and the value needs to be mapped to **user.department**.</span></span>

    | <span data-ttu-id="4d2ba-175">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="4d2ba-175">Attribute Name</span></span> | <span data-ttu-id="4d2ba-176">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="4d2ba-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="4d2ba-177">department</span><span class="sxs-lookup"><span data-stu-id="4d2ba-177">department</span></span>| <span data-ttu-id="4d2ba-178">user.department</span><span class="sxs-lookup"><span data-stu-id="4d2ba-178">user.department</span></span> |

      ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      <span data-ttu-id="4d2ba-180">a.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-180">a.</span></span> <span data-ttu-id="4d2ba-181">Haga clic en Agregar atributo para abrir la página de detalles del atributo y agregue el atributo department tal como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="4d2ba-181">Click on Add attribute to open the attribute details page add the department attribute as shown below-</span></span>

      ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      <span data-ttu-id="4d2ba-183">b.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-183">b.</span></span> <span data-ttu-id="4d2ba-184">Haga clic en **Aceptar** para guardar el atributo.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-184">Click on **Ok** to save the attribute.</span></span>

      <span data-ttu-id="4d2ba-185">c.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-185">c.</span></span> <span data-ttu-id="4d2ba-186">Cambie el nombre del atributo **emailaddress** a **email**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-186">Change the name of the attribute **emailaddress** to **email**.</span></span>


10. <span data-ttu-id="4d2ba-187">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-187">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. <span data-ttu-id="4d2ba-189">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-189">Click **Save**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="4d2ba-191">Vaya a la sección **LinkedIn Admin Settings** (Configuración de administrador de LinkedIn).</span><span class="sxs-lookup"><span data-stu-id="4d2ba-191">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="4d2ba-192">Cargue el archivo XML que acaba de descargar de Azure Portal haciendo clic en la opción Upload XML file (Cargar archivo XML).</span><span class="sxs-lookup"><span data-stu-id="4d2ba-192">Upload the XML file you just downloaded from the Azure portal by clicking on the Upload XML file option.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. <span data-ttu-id="4d2ba-194">Haga clic en **On** (Activar) para habilitar SSO.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-194">Click **On** to enable SSO.</span></span> <span data-ttu-id="4d2ba-195">El estado de SSO cambiará de **Not Connected** (No conectado) a **Connected** (Conectado)</span><span class="sxs-lookup"><span data-stu-id="4d2ba-195">SSO status will change from **Not Connected** to **Connected**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4d2ba-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d2ba-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="4d2ba-198">El objetivo de esta sección es crear un usuario de prueba en el Portal de administración de Azure llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-198">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="4d2ba-200">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="4d2ba-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4d2ba-201">En el panel de navegación izquierdo del **Portal de administración de Azure**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-201">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4d2ba-203">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-203">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4d2ba-205">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-205">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4d2ba-207">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="4d2ba-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4d2ba-209">a.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-209">a.</span></span> <span data-ttu-id="4d2ba-210">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4d2ba-211">b.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-211">b.</span></span> <span data-ttu-id="4d2ba-212">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4d2ba-213">c.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-213">c.</span></span> <span data-ttu-id="4d2ba-214">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4d2ba-215">d.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-215">d.</span></span> <span data-ttu-id="4d2ba-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-216">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-elevate-test-user"></a><span data-ttu-id="4d2ba-217">Creación de un usuario de prueba de LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="4d2ba-217">Creating a LinkedIn Elevate test user</span></span>

<span data-ttu-id="4d2ba-218">La aplicación Linked Elevate admite aprovisionamiento de usuarios Just-In-Time y, tras la autenticación, los usuarios se crearán automáticamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-218">Linked Elevate Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="4d2ba-219">En la página de configuración del administrador del portal de LinkedIn Elevate, invierta el conmutador **Automatically Assign licenses** (Asignar licencias automáticamente) a activo para habilitar el aprovisionamiento Just-In-Time y este también asignará una licencia al usuario.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-219">On the admin settings page on the LinkedIn Elevate portal flip the switch **Automatically Assign licenses** to active to enable Just in time provisioning and this will also assign a license to the user.</span></span>

   ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4d2ba-221">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d2ba-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4d2ba-222">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-222">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to LinkedIn Elevate.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="4d2ba-224">**Para asignar Britta Simon a LinkedIn Elevate, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="4d2ba-224">**To assign Britta Simon to LinkedIn Elevate, perform the following steps:**</span></span>

1. <span data-ttu-id="4d2ba-225">En el Portal de administración de Azure, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. A continuación, haga clic en **All applications** (Todas las aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="4d2ba-225">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="4d2ba-227">En la lista de aplicaciones, seleccione **LinkedIn Elevate**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-227">In the applications list, select **LinkedIn Elevate**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. <span data-ttu-id="4d2ba-229">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="4d2ba-231">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-231">Click **Add** button.</span></span> <span data-ttu-id="4d2ba-232">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="4d2ba-234">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4d2ba-235">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4d2ba-236">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4d2ba-237">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="4d2ba-237">Testing single sign-on</span></span>

<span data-ttu-id="4d2ba-238">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4d2ba-239">Al hacer clic en el icono de LinkedIn Elevate en el Panel de acceso, debe abrirse la página de inicio de sesión único de Azure y, después de acceder, debe entrar a la aplicación LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="4d2ba-239">When you click the LinkedIn Elevate tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4d2ba-240">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4d2ba-240">Additional resources</span></span>

* [<span data-ttu-id="4d2ba-241">Tutorial: configuración de LinkedIn Elevate para el aprovisionamiento automático de usuarios con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d2ba-241">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span></span>](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [<span data-ttu-id="4d2ba-242">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d2ba-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4d2ba-243">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4d2ba-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
