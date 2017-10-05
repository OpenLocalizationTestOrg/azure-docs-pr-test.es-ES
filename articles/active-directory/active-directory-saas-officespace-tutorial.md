---
title: "Tutorial: Integración de Azure Active Directory con OfficeSpace Software | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y OfficeSpace Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 43d2ecfe851d8f6c43cd4ce7fc4bd872818f4137
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a><span data-ttu-id="846f5-103">Tutorial: Integración de Azure Active Directory con OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="846f5-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span></span>

<span data-ttu-id="846f5-104">En este tutorial, obtendrá información sobre cómo integrar OfficeSpace Software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="846f5-104">In this tutorial, you learn how to integrate OfficeSpace Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="846f5-105">La integración de OfficeSpace Software con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="846f5-105">Integrating OfficeSpace Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="846f5-106">Puede controlar en Azure AD quién tiene acceso a OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="846f5-106">You can control in Azure AD who has access to OfficeSpace Software.</span></span>
- <span data-ttu-id="846f5-107">Puede permitir que los usuarios inicien sesión automáticamente en OfficeSpace Software (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="846f5-107">You can enable your users to automatically get signed-on to OfficeSpace Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="846f5-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="846f5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="846f5-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="846f5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="846f5-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="846f5-110">Prerequisites</span></span>

<span data-ttu-id="846f5-111">Para configurar la integración de Azure AD con OfficeSpace Software, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="846f5-111">To configure Azure AD integration with OfficeSpace Software, you need the following items:</span></span>

- <span data-ttu-id="846f5-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="846f5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="846f5-113">Un suscripción habilitada para el inicio de sesión único en OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="846f5-113">A OfficeSpace Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="846f5-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="846f5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="846f5-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="846f5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="846f5-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="846f5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="846f5-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="846f5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="846f5-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="846f5-118">Scenario description</span></span>
<span data-ttu-id="846f5-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="846f5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="846f5-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="846f5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="846f5-121">Adición de OfficeSpace Software desde la galería</span><span class="sxs-lookup"><span data-stu-id="846f5-121">Adding OfficeSpace Software from the gallery</span></span>
2. <span data-ttu-id="846f5-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="846f5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-officespace-software-from-the-gallery"></a><span data-ttu-id="846f5-123">Adición de OfficeSpace Software desde la galería</span><span class="sxs-lookup"><span data-stu-id="846f5-123">Adding OfficeSpace Software from the gallery</span></span>
<span data-ttu-id="846f5-124">Para configurar la integración de OfficeSpace Software en Azure AD, deberá agregarlo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="846f5-124">To configure the integration of OfficeSpace Software into Azure AD, you need to add OfficeSpace Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="846f5-125">**Para agregar OfficeSpace Software desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="846f5-125">**To add OfficeSpace Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="846f5-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="846f5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="846f5-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="846f5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="846f5-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="846f5-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="846f5-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="846f5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="846f5-133">En el cuadro de búsqueda, escriba **OfficeSpace Software**, seleccione **OfficeSpace Software** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="846f5-133">In the search box, type **OfficeSpace Software**, select **OfficeSpace Software** from result panel then click **Add** button to add the application.</span></span>

    ![OfficeSpace Software en la lista de resultados](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="846f5-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="846f5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="846f5-136">En esta sección, configurará y probará el inicio de sesión único de Azure AD con OfficeSpace Software con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="846f5-136">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="846f5-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de OfficeSpace Software para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="846f5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in OfficeSpace Software is to a user in Azure AD.</span></span> <span data-ttu-id="846f5-138">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="846f5-138">In other words, a link relationship between an Azure AD user and the related user in OfficeSpace Software needs to be established.</span></span>

<span data-ttu-id="846f5-139">En OfficeSpace Software, asigne el valor del **nombre de usuario** en Azure AD como valor de **Nombre de usuario** para establecer la relación de vínculo.</span><span class="sxs-lookup"><span data-stu-id="846f5-139">In OfficeSpace Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="846f5-140">Para configurar y probar el inicio de sesión único de Azure AD con OfficeSpace Software, debe completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="846f5-140">To configure and test Azure AD single sign-on with OfficeSpace Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="846f5-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="846f5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="846f5-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="846f5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="846f5-143">**[Creación de un usuario de prueba de OfficeSpace Software](#create-a-officespace-software-test-user)**: para tener en OfficeSpace Software un homólogo de Britta Simon que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="846f5-143">**[Create a OfficeSpace Software test user](#create-a-officespace-software-test-user)** - to have a counterpart of Britta Simon in OfficeSpace Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="846f5-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="846f5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="846f5-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="846f5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="846f5-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="846f5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="846f5-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="846f5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OfficeSpace Software application.</span></span>

<span data-ttu-id="846f5-148">**Para configurar el inicio de sesión único de Azure AD con OfficeSpace Software, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="846f5-148">**To configure Azure AD single sign-on with OfficeSpace Software, perform the following steps:**</span></span>

1. <span data-ttu-id="846f5-149">En Azure Portal, en la página de integración de la aplicación **OfficeSpace Software**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="846f5-149">In the Azure portal, on the **OfficeSpace Software** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="846f5-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="846f5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. <span data-ttu-id="846f5-153">En la sección **Dominio y direcciones URL de OfficeSpace Software**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="846f5-153">On the **OfficeSpace Software Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    <span data-ttu-id="846f5-155">a.</span><span class="sxs-lookup"><span data-stu-id="846f5-155">a.</span></span> <span data-ttu-id="846f5-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<company name>.officespacesoftware.com/users/sign_in/saml`.</span><span class="sxs-lookup"><span data-stu-id="846f5-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span></span>

    <span data-ttu-id="846f5-157">b.</span><span class="sxs-lookup"><span data-stu-id="846f5-157">b.</span></span> <span data-ttu-id="846f5-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `<company name>.officespacesoftware.com`</span><span class="sxs-lookup"><span data-stu-id="846f5-158">In the **Identifier** textbox, type a URL using the following pattern: `<company name>.officespacesoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="846f5-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="846f5-159">These values are not real.</span></span> <span data-ttu-id="846f5-160">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="846f5-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="846f5-161">Póngase en contacto con el [equipo de soporte técnico de OfficeSpace Software](mailto:support@officespacesoftware.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="846f5-161">Contact [OfficeSpace Software Client support team](mailto:support@officespacesoftware.com) to get these values.</span></span> 

4. <span data-ttu-id="846f5-162">La aplicación OfficeSpace Software espera las aserciones de SAML en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="846f5-162">OfficeSpace Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="846f5-163">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="846f5-163">Please configure the following claims for this application.</span></span> <span data-ttu-id="846f5-164">Puede administrar los valores de estos atributos en la sección "**Atributos de usuario**" de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="846f5-164">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="846f5-165">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="846f5-165">The following screenshot shows an example for this.</span></span>
    
    ![Configuración del atributo](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. <span data-ttu-id="846f5-167">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, seleccione **user.mail** como **identificador de usuario**, y para cada fila se muestra en la tabla siguiente, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="846f5-167">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="846f5-168">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="846f5-168">Attribute Name</span></span> | <span data-ttu-id="846f5-169">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="846f5-169">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="846f5-170">email</span><span class="sxs-lookup"><span data-stu-id="846f5-170">email</span></span> | <span data-ttu-id="846f5-171">user.mail</span><span class="sxs-lookup"><span data-stu-id="846f5-171">user.mail</span></span> |
    | <span data-ttu-id="846f5-172">name</span><span class="sxs-lookup"><span data-stu-id="846f5-172">name</span></span> | <span data-ttu-id="846f5-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="846f5-173">user.displayname</span></span> |
    | <span data-ttu-id="846f5-174">first_name</span><span class="sxs-lookup"><span data-stu-id="846f5-174">first_name</span></span> | <span data-ttu-id="846f5-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="846f5-175">user.givenname</span></span> |
    | <span data-ttu-id="846f5-176">last_name</span><span class="sxs-lookup"><span data-stu-id="846f5-176">last_name</span></span> | <span data-ttu-id="846f5-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="846f5-177">user.surname</span></span> |

    <span data-ttu-id="846f5-178">a.</span><span class="sxs-lookup"><span data-stu-id="846f5-178">a.</span></span> <span data-ttu-id="846f5-179">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="846f5-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![<span data-ttu-id="846f5-180">Configuración de la agregación</span><span class="sxs-lookup"><span data-stu-id="846f5-180">Configure Add</span></span> ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![Configuración del atributo](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="846f5-182">b.</span><span class="sxs-lookup"><span data-stu-id="846f5-182">b.</span></span> <span data-ttu-id="846f5-183">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="846f5-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="846f5-184">c.</span><span class="sxs-lookup"><span data-stu-id="846f5-184">c.</span></span> <span data-ttu-id="846f5-185">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="846f5-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="846f5-186">d.</span><span class="sxs-lookup"><span data-stu-id="846f5-186">d.</span></span> <span data-ttu-id="846f5-187">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="846f5-187">Click **Ok**</span></span>
 
6. <span data-ttu-id="846f5-188">En la sección **Certificado de firma de SAML**, copie el valor de **HUELLA DIGITAL** del certificado.</span><span class="sxs-lookup"><span data-stu-id="846f5-188">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of the certificate.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. <span data-ttu-id="846f5-190">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="846f5-190">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="846f5-192">En la sección **Configuración de OfficeSpace Software**, haga clic en **Configurar OfficeSpace Software** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="846f5-192">On the **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="846f5-193">Copie la **dirección URL de cierre de sesión y la dirección URL del servicio de inicio de sesión único de SAML** de la **sección de referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="846f5-193">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. <span data-ttu-id="846f5-195">En otra ventana del explorador web, inicie sesión en como administrador en el inquilino de OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="846f5-195">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span></span>

10. <span data-ttu-id="846f5-196">Vaya a **Settings** (Configuración) y haga clic en **Connectors** (Conectores).</span><span class="sxs-lookup"><span data-stu-id="846f5-196">Go to **Settings** and click **Connectors**.</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. <span data-ttu-id="846f5-198">Haga clic en **Autenticación SAML**.</span><span class="sxs-lookup"><span data-stu-id="846f5-198">Click **SAML Authentication**.</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. <span data-ttu-id="846f5-200">En la sección **Autenticación SAML** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="846f5-200">In the **SAML Authentication** section, perform the following steps:</span></span>

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    <span data-ttu-id="846f5-202">a.</span><span class="sxs-lookup"><span data-stu-id="846f5-202">a.</span></span> <span data-ttu-id="846f5-203">En el cuadro de texto **Logout provider URL** (Dirección URL del proveedor de cierre de sesión), pegue el valor de **dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="846f5-203">In the **Logout provider url** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="846f5-204">b.</span><span class="sxs-lookup"><span data-stu-id="846f5-204">b.</span></span> <span data-ttu-id="846f5-205">En el cuadro de texto **Client idp target url** (Dirección URL de destino del IDP del cliente), pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="846f5-205">In the **Client idp target url** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="846f5-206">c.</span><span class="sxs-lookup"><span data-stu-id="846f5-206">c.</span></span> <span data-ttu-id="846f5-207">En el cuadro de texto **Client IDP certificate fingerprint** (Huella digital del certificado de IDP del cliente), pegue el valor de **Huella digital** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="846f5-207">Paste the **Thumbprint** value which you have copied from Azure portal, into the **Client IDP certificate fingerprint** textbox.</span></span> 

    <span data-ttu-id="846f5-208">d.</span><span class="sxs-lookup"><span data-stu-id="846f5-208">d.</span></span> <span data-ttu-id="846f5-209">Haga clic en **Guardar configuración**.</span><span class="sxs-lookup"><span data-stu-id="846f5-209">Click **Save Settings**.</span></span>


> [!TIP]
> <span data-ttu-id="846f5-210">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="846f5-210">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="846f5-211">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="846f5-211">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="846f5-212">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="846f5-212">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="846f5-213">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="846f5-213">Create an Azure AD test user</span></span>

<span data-ttu-id="846f5-214">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="846f5-214">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="846f5-216">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="846f5-216">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="846f5-217">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="846f5-217">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="846f5-219">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="846f5-219">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="846f5-221">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="846f5-221">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="846f5-223">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="846f5-223">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="846f5-225">a.</span><span class="sxs-lookup"><span data-stu-id="846f5-225">a.</span></span> <span data-ttu-id="846f5-226">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="846f5-226">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="846f5-227">b.</span><span class="sxs-lookup"><span data-stu-id="846f5-227">b.</span></span> <span data-ttu-id="846f5-228">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="846f5-228">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="846f5-229">c.</span><span class="sxs-lookup"><span data-stu-id="846f5-229">c.</span></span> <span data-ttu-id="846f5-230">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="846f5-230">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="846f5-231">d.</span><span class="sxs-lookup"><span data-stu-id="846f5-231">d.</span></span> <span data-ttu-id="846f5-232">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="846f5-232">Click **Create**.</span></span>
 
### <a name="create-a-officespace-software-test-user"></a><span data-ttu-id="846f5-233">Creación de un usuario de prueba de OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="846f5-233">Create a OfficeSpace Software test user</span></span>

<span data-ttu-id="846f5-234">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="846f5-234">The objective of this section is to create a user called Britta Simon in OfficeSpace Software.</span></span> <span data-ttu-id="846f5-235">OfficeSpace Software admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="846f5-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="846f5-236">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="846f5-236">There is no action item for you in this section.</span></span> <span data-ttu-id="846f5-237">Durante un intento de acceder a OfficeSpace Software se creará un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="846f5-237">A new user will be created during an attempt to access OfficeSpace Software if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="846f5-238">Si necesita crear manualmente un usuario, es preciso que se ponga contacto con el [equipo de soporte técnico de OfficeSpace Software](mailto:support@officespacesoftware.com).</span><span class="sxs-lookup"><span data-stu-id="846f5-238">If you need to create an user manually, you need to Contact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="846f5-239">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="846f5-239">Assign the Azure AD test user</span></span>

<span data-ttu-id="846f5-240">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="846f5-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OfficeSpace Software.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="846f5-242">**Para asignar un usuario llamado Britta Simon a OfficeSpace Software, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="846f5-242">**To assign Britta Simon to OfficeSpace Software, perform the following steps:**</span></span>

1. <span data-ttu-id="846f5-243">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="846f5-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="846f5-245">En la lista de aplicaciones, seleccione **OfficeSpace Software**.</span><span class="sxs-lookup"><span data-stu-id="846f5-245">In the applications list, select **OfficeSpace Software**.</span></span>

    ![Vínculo a OfficeSpace Software en la lista de aplicaciones](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. <span data-ttu-id="846f5-247">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="846f5-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="846f5-249">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="846f5-249">Click **Add** button.</span></span> <span data-ttu-id="846f5-250">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="846f5-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="846f5-252">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="846f5-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="846f5-253">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="846f5-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="846f5-254">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="846f5-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="846f5-255">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="846f5-255">Test single sign-on</span></span>

<span data-ttu-id="846f5-256">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="846f5-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="846f5-257">Al hacer clic en el icono OfficeSpace Software en el panel de acceso, debería iniciar sesión automáticamente en la aplicación OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="846f5-257">When you click the OfficeSpace Software tile in the Access Panel, you should get automatically signed-on to your OfficeSpace Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="846f5-258">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="846f5-258">Additional resources</span></span>

* [<span data-ttu-id="846f5-259">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="846f5-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="846f5-260">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="846f5-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png

