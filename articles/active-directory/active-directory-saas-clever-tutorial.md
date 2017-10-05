---
title: "Tutorial: integración de Azure Active Directory con Clever | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Clever."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 84082ff567e37d7fff80be9e089c67cfab911861
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="2786b-103">Tutorial: integración de Azure Active Directory con Clever</span><span class="sxs-lookup"><span data-stu-id="2786b-103">Tutorial: Azure Active Directory integration with Clever</span></span>

<span data-ttu-id="2786b-104">En este tutorial, obtendrá información sobre cómo integrar Clever con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2786b-104">In this tutorial, you learn how to integrate Clever with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2786b-105">Integrar Clever con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="2786b-105">Integrating Clever with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2786b-106">Puede controlar en Azure AD quién tiene acceso a Clever.</span><span class="sxs-lookup"><span data-stu-id="2786b-106">You can control in Azure AD who has access to Clever.</span></span>
- <span data-ttu-id="2786b-107">Puede permitir que los usuarios inicien sesión automáticamente en Clever (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2786b-107">You can enable your users to automatically get signed-on to Clever (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2786b-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2786b-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="2786b-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2786b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2786b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2786b-110">Prerequisites</span></span>

<span data-ttu-id="2786b-111">Para configurar la integración de Azure AD con Clever, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2786b-111">To configure Azure AD integration with Clever, you need the following items:</span></span>

- <span data-ttu-id="2786b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2786b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2786b-113">Una suscripción habilitada para el inicio de sesión único en Clever</span><span class="sxs-lookup"><span data-stu-id="2786b-113">A Clever single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2786b-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="2786b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2786b-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="2786b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2786b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2786b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2786b-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2786b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2786b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="2786b-118">Scenario description</span></span>
<span data-ttu-id="2786b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="2786b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2786b-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="2786b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2786b-121">Incorporación de Clever desde la galería</span><span class="sxs-lookup"><span data-stu-id="2786b-121">Adding Clever from the gallery</span></span>
2. <span data-ttu-id="2786b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2786b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clever-from-the-gallery"></a><span data-ttu-id="2786b-123">Incorporación de Clever desde la galería</span><span class="sxs-lookup"><span data-stu-id="2786b-123">Adding Clever from the gallery</span></span>
<span data-ttu-id="2786b-124">Para configurar la integración de Clever en Azure AD, tendrá que agregar Clever desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="2786b-124">To configure the integration of Clever into Azure AD, you need to add Clever from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2786b-125">**Para agregar Clever desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2786b-125">**To add Clever from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2786b-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2786b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="2786b-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="2786b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2786b-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2786b-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="2786b-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2786b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="2786b-133">En el cuadro de búsqueda, escriba **Clever**, seleccione **Clever** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2786b-133">In the search box, type **Clever**, select **Clever** from result panel then click **Add** button to add the application.</span></span>

    ![Clever en la lista de resultados](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2786b-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="2786b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2786b-136">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Clever con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2786b-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2786b-137">Para que el inicio de sesión único funcione, Azure AD tiene que saber cuál es el usuario homólogo de Clever para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2786b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Clever is to a user in Azure AD.</span></span> <span data-ttu-id="2786b-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Clever.</span><span class="sxs-lookup"><span data-stu-id="2786b-138">In other words, a link relationship between an Azure AD user and the related user in Clever needs to be established.</span></span>

<span data-ttu-id="2786b-139">Para establecer la relación de vínculo, en Clever, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="2786b-139">In Clever, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2786b-140">Para configurar y probar el inicio de sesión único de Azure AD con Clever, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="2786b-140">To configure and test Azure AD single sign-on with Clever, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2786b-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="2786b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2786b-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2786b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2786b-143">**[Creación de un usuario de prueba de Clever](#create-a-clever-test-user)**: para tener un homólogo de Britta Simon en Clever que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2786b-143">**[Create a Clever test user](#create-a-clever-test-user)** - to have a counterpart of Britta Simon in Clever that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2786b-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2786b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2786b-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="2786b-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2786b-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2786b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2786b-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en su aplicación Clever.</span><span class="sxs-lookup"><span data-stu-id="2786b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clever application.</span></span>

<span data-ttu-id="2786b-148">**Para configurar el inicio de sesión único de Azure AD con Clever, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2786b-148">**To configure Azure AD single sign-on with Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="2786b-149">En Azure Portal, en la página de integración de la aplicación **Clever**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2786b-149">In the Azure portal, on the **Clever** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="2786b-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2786b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. <span data-ttu-id="2786b-153">En la sección **Dominio y direcciones URL de Clever**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2786b-153">On the **Clever Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Clever](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    <span data-ttu-id="2786b-155">a.</span><span class="sxs-lookup"><span data-stu-id="2786b-155">a.</span></span> <span data-ttu-id="2786b-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://clever.com/in/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="2786b-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://clever.com/in/<companyname>`</span></span>

    <span data-ttu-id="2786b-157">b.</span><span class="sxs-lookup"><span data-stu-id="2786b-157">b.</span></span> <span data-ttu-id="2786b-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://clever.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="2786b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://clever.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2786b-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="2786b-159">These values are not real.</span></span> <span data-ttu-id="2786b-160">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="2786b-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2786b-161">Póngase en contacto con el [equipo de soporte técnico al cliente de Clever](https://clever.com/about/contact/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="2786b-161">Contact [Clever Client support team](https://clever.com/about/contact/) to get these values.</span></span>

4. <span data-ttu-id="2786b-162">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2786b-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. <span data-ttu-id="2786b-164">La aplicación Clever espera las aserciones de SAML en un formato específico, lo que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los **atributos del token SAML**.</span><span class="sxs-lookup"><span data-stu-id="2786b-164">The Clever application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>

    <span data-ttu-id="2786b-165">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="2786b-165">The following screenshot shows an example for this.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. <span data-ttu-id="2786b-167">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo Token SAML como muestra la imagen anterior y realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="2786b-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="2786b-168">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="2786b-168">Attribute Name</span></span>  | <span data-ttu-id="2786b-169">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="2786b-169">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="2786b-170">clever.student.credentials.district\_username</span><span class="sxs-lookup"><span data-stu-id="2786b-170">clever.student.credentials.district\_username</span></span>  | <span data-ttu-id="2786b-171">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="2786b-171">user.userprincipalname</span></span> |
    | <span data-ttu-id="2786b-172">Firstname</span><span class="sxs-lookup"><span data-stu-id="2786b-172">Firstname</span></span>  | <span data-ttu-id="2786b-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="2786b-173">user.givenname</span></span> |
    | <span data-ttu-id="2786b-174">Lastname</span><span class="sxs-lookup"><span data-stu-id="2786b-174">Lastname</span></span>  | <span data-ttu-id="2786b-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="2786b-175">user.surname</span></span> |    

    <span data-ttu-id="2786b-176">a.</span><span class="sxs-lookup"><span data-stu-id="2786b-176">a.</span></span> <span data-ttu-id="2786b-177">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="2786b-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="2786b-180">b.</span><span class="sxs-lookup"><span data-stu-id="2786b-180">b.</span></span> <span data-ttu-id="2786b-181">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="2786b-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="2786b-182">c.</span><span class="sxs-lookup"><span data-stu-id="2786b-182">c.</span></span> <span data-ttu-id="2786b-183">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="2786b-183">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="2786b-184">d.</span><span class="sxs-lookup"><span data-stu-id="2786b-184">d.</span></span> <span data-ttu-id="2786b-185">Deje el cuadro de texto **Espacio de nombres** en blanco.</span><span class="sxs-lookup"><span data-stu-id="2786b-185">Leave the **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="2786b-186">d.</span><span class="sxs-lookup"><span data-stu-id="2786b-186">d.</span></span> <span data-ttu-id="2786b-187">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2786b-187">Click **Ok**.</span></span>     

5. <span data-ttu-id="2786b-188">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="2786b-188">Click **Save** button.</span></span>

    ![Botón Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="2786b-190">Para generar la dirección URL de **Metadatos**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2786b-190">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="2786b-191">a.</span><span class="sxs-lookup"><span data-stu-id="2786b-191">a.</span></span> <span data-ttu-id="2786b-192">Haga clic en **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2786b-192">Click **App registrations**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    <span data-ttu-id="2786b-194">b.</span><span class="sxs-lookup"><span data-stu-id="2786b-194">b.</span></span> <span data-ttu-id="2786b-195">Haga clic en **Puntos de conexión** para abrir el cuadro de diálogo **Puntos de conexión**.</span><span class="sxs-lookup"><span data-stu-id="2786b-195">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    <span data-ttu-id="2786b-197">c.</span><span class="sxs-lookup"><span data-stu-id="2786b-197">c.</span></span> <span data-ttu-id="2786b-198">Haga clic en el botón Copiar para copiar la dirección URL del **DOCUMENTO DE METADATOS DE FEDERACIÓN** y péguela en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="2786b-198">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    <span data-ttu-id="2786b-200">d.</span><span class="sxs-lookup"><span data-stu-id="2786b-200">d.</span></span> <span data-ttu-id="2786b-201">Ahora, vaya a la página de propiedades de **Clever** y copie el **Identificador de la aplicación** con el botón **Copiar** y péguelo en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="2786b-201">Now go to the property page of **Clever** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    <span data-ttu-id="2786b-203">e.</span><span class="sxs-lookup"><span data-stu-id="2786b-203">e.</span></span> <span data-ttu-id="2786b-204">Genere la **Dirección URL de metadatos** con el patrón siguiente: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="2786b-204">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>   

9. <span data-ttu-id="2786b-205">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía en Clever.</span><span class="sxs-lookup"><span data-stu-id="2786b-205">In a different web browser window, log in to your Clever company site as an administrator.</span></span>

10. <span data-ttu-id="2786b-206">En la barra de herramientas, haga clic en **Inicio de sesión instantáneo**.</span><span class="sxs-lookup"><span data-stu-id="2786b-206">In the toolbar, click **Instant Login**.</span></span>

    <span data-ttu-id="2786b-207">![Inicio de sesión instantáneo](./media/active-directory-saas-clever-tutorial/ic798984.png "Inicio de sesión instantáneo")</span><span class="sxs-lookup"><span data-stu-id="2786b-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span></span>

11. <span data-ttu-id="2786b-208">En la página **Instant Login** (Inicio de sesión instantáneo), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2786b-208">On the **Instant Login** page, perform the following steps:</span></span>
      
      <span data-ttu-id="2786b-209">![Inicio de sesión instantáneo](./media/active-directory-saas-clever-tutorial/ic798985.png "Inicio de sesión instantáneo")</span><span class="sxs-lookup"><span data-stu-id="2786b-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span></span>
      
      <span data-ttu-id="2786b-210">a.</span><span class="sxs-lookup"><span data-stu-id="2786b-210">a.</span></span> <span data-ttu-id="2786b-211">Escriba la **Dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="2786b-211">Type the **Login URL**.</span></span>
      
      >[!NOTE]
      ><span data-ttu-id="2786b-212">La **URL de inicio de sesión** es un valor personalizado.</span><span class="sxs-lookup"><span data-stu-id="2786b-212">The **Login URL** is a custom value.</span></span> <span data-ttu-id="2786b-213">Póngase en contacto con el [equipo de soporte técnico al cliente de Clever](https://clever.com/about/contact/) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="2786b-213">Contact [Clever Client support team](https://clever.com/about/contact/) to get this value.</span></span>
      
      <span data-ttu-id="2786b-214">b.</span><span class="sxs-lookup"><span data-stu-id="2786b-214">b.</span></span> <span data-ttu-id="2786b-215">En **Identity System** (Sistema de identidades), seleccione **ADFS**.</span><span class="sxs-lookup"><span data-stu-id="2786b-215">As **Identity System**, select **ADFS**.</span></span>

      <span data-ttu-id="2786b-216">c.</span><span class="sxs-lookup"><span data-stu-id="2786b-216">c.</span></span> <span data-ttu-id="2786b-217">Escriba la **dirección URL de metadatos** en el cuadro de texto **Metadata URL** (Dirección URL de metadatos).</span><span class="sxs-lookup"><span data-stu-id="2786b-217">Type the **Metadata URL** in the **Metadata URL** textbox.</span></span>
      
      <span data-ttu-id="2786b-218">d.</span><span class="sxs-lookup"><span data-stu-id="2786b-218">d.</span></span> <span data-ttu-id="2786b-219">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="2786b-219">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2786b-220">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2786b-220">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2786b-221">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="2786b-221">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2786b-222">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2786b-222">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2786b-223">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2786b-223">Create an Azure AD test user</span></span>

<span data-ttu-id="2786b-224">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2786b-224">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="2786b-226">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="2786b-226">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2786b-227">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2786b-227">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="2786b-229">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2786b-229">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="2786b-231">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2786b-231">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="2786b-233">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2786b-233">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    <span data-ttu-id="2786b-235">a.</span><span class="sxs-lookup"><span data-stu-id="2786b-235">a.</span></span> <span data-ttu-id="2786b-236">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2786b-236">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2786b-237">b.</span><span class="sxs-lookup"><span data-stu-id="2786b-237">b.</span></span> <span data-ttu-id="2786b-238">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2786b-238">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="2786b-239">c.</span><span class="sxs-lookup"><span data-stu-id="2786b-239">c.</span></span> <span data-ttu-id="2786b-240">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="2786b-240">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="2786b-241">d.</span><span class="sxs-lookup"><span data-stu-id="2786b-241">d.</span></span> <span data-ttu-id="2786b-242">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2786b-242">Click **Create**.</span></span>
 
### <a name="create-a-clever-test-user"></a><span data-ttu-id="2786b-243">Creación de un usuario de prueba de Clever</span><span class="sxs-lookup"><span data-stu-id="2786b-243">Create a Clever test user</span></span>

<span data-ttu-id="2786b-244">Para habilitar a los usuarios de Azure AD para que inicien sesión en Clever, tienen que aprovisionarse en Clever.</span><span class="sxs-lookup"><span data-stu-id="2786b-244">To enable Azure AD users to log in to Clever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="2786b-245">Para ello trabaje con el [equipo de soporte técnico al cliente de Clever](https://clever.com/about/contact/) para agregar los usuarios a la plataforma de Clever.</span><span class="sxs-lookup"><span data-stu-id="2786b-245">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add the users in the Clever platform.</span></span> <span data-ttu-id="2786b-246">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2786b-246">Users must be created and activated before you use single sign-on.</span></span> 

>[!NOTE]
><span data-ttu-id="2786b-247">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Clever ofrecida por Clever para aprovisionar cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2786b-247">You can use any other Clever user account creation tools or APIs provided by Clever to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="2786b-248">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2786b-248">Assign the Azure AD test user</span></span>

<span data-ttu-id="2786b-249">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Clever.</span><span class="sxs-lookup"><span data-stu-id="2786b-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Clever.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="2786b-251">**Para asignar Britta Simon a Clever, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2786b-251">**To assign Britta Simon to Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="2786b-252">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2786b-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="2786b-254">En la lista de aplicaciones, seleccione **Clever**.</span><span class="sxs-lookup"><span data-stu-id="2786b-254">In the applications list, select **Clever**.</span></span>

    ![Vínculo a Clever en la lista de aplicaciones](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. <span data-ttu-id="2786b-256">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2786b-256">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="2786b-258">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2786b-258">Click **Add** button.</span></span> <span data-ttu-id="2786b-259">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2786b-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="2786b-261">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="2786b-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2786b-262">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2786b-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2786b-263">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2786b-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2786b-264">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="2786b-264">Test single sign-on</span></span>

<span data-ttu-id="2786b-265">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="2786b-265">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2786b-266">Al hacer clic en el icono de Clever en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Clever.</span><span class="sxs-lookup"><span data-stu-id="2786b-266">When you click the Clever tile in the Access Panel, you should get automatically signed-on to your Clever application.</span></span>
<span data-ttu-id="2786b-267">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2786b-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2786b-268">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2786b-268">Additional resources</span></span>

* [<span data-ttu-id="2786b-269">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2786b-269">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2786b-270">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2786b-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

