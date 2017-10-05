---
title: "Tutorial: Integración de Azure Active Directory con FilesAnywhere | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y FilesAnywhere."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 4153056bd21006061c6ad8ff9cf3c17de9248628
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a><span data-ttu-id="3337e-103">Tutorial: Integración de Azure Active Directory con FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="3337e-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span></span>

<span data-ttu-id="3337e-104">En este tutorial, aprenderá a integrar FilesAnywhere con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3337e-104">In this tutorial, you learn how to integrate FilesAnywhere with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3337e-105">La integración de FilesAnywhere con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3337e-105">Integrating FilesAnywhere with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3337e-106">Puede controlar en Azure AD quién tiene acceso a FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="3337e-106">You can control in Azure AD who has access to FilesAnywhere</span></span>
- <span data-ttu-id="3337e-107">Puede permitir que los usuarios inicien sesión automáticamente en FilesAnywhere (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3337e-107">You can enable your users to automatically get signed-on to FilesAnywhere (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3337e-108">Puede administrar sus cuentas en una ubicación central: el Portal de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="3337e-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="3337e-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3337e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3337e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3337e-110">Prerequisites</span></span>

<span data-ttu-id="3337e-111">Para configurar la integración de Azure AD con FilesAnywhere, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3337e-111">To configure Azure AD integration with FilesAnywhere, you need the following items:</span></span>

- <span data-ttu-id="3337e-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3337e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3337e-113">Una suscripción habilitada para el inicio de sesión único en FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="3337e-113">A FilesAnywhere single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="3337e-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3337e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="3337e-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3337e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3337e-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3337e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="3337e-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3337e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="3337e-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3337e-118">Scenario description</span></span>
<span data-ttu-id="3337e-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3337e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3337e-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="3337e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3337e-121">Agregar FilesAnywhere desde la galería</span><span class="sxs-lookup"><span data-stu-id="3337e-121">Adding FilesAnywhere from the gallery</span></span>
2. <span data-ttu-id="3337e-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3337e-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-filesanywhere-from-the-gallery"></a><span data-ttu-id="3337e-123">Agregar FilesAnywhere desde la galería</span><span class="sxs-lookup"><span data-stu-id="3337e-123">Adding FilesAnywhere from the gallery</span></span>
<span data-ttu-id="3337e-124">Para configurar la integración de FilesAnywhere en Azure AD, será preciso que agregue FilesAnywhere desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="3337e-124">To configure the integration of FilesAnywhere into Azure AD, you need to add FilesAnywhere from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3337e-125">**Para agregar FilesAnywhere desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3337e-125">**To add FilesAnywhere from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3337e-126">En el panel de navegación izquierdo del **[Portal de administración de Azure](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3337e-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3337e-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3337e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3337e-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3337e-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="3337e-131">Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3337e-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="3337e-133">En el cuadro de búsqueda, escriba **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="3337e-133">In the search box, type **FilesAnywhere**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. <span data-ttu-id="3337e-135">En el panel de resultados, seleccione **FilesAnywhere** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3337e-135">In the results panel, select **FilesAnywhere**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3337e-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3337e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3337e-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con FilesAnywhere con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3337e-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3337e-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de FilesAnywhere para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3337e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FilesAnywhere is to a user in Azure AD.</span></span> <span data-ttu-id="3337e-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="3337e-140">In other words, a link relationship between an Azure AD user and the related user in FilesAnywhere needs to be established.</span></span>

<span data-ttu-id="3337e-141">Esta relación de vínculo se establece asignando el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="3337e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FilesAnywhere.</span></span>

<span data-ttu-id="3337e-142">Para configurar y probar el inicio de sesión único de Azure AD con FilesAnywhere, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3337e-142">To configure and test Azure AD single sign-on with FilesAnywhere, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3337e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="3337e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3337e-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3337e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3337e-145">**[Creación de un usuario de prueba para FilesAnywhere](#creating-a-filesanywhere-test-user)**: para tener un homólogo de Britta Simon en FilesAnywhere que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3337e-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - to have a counterpart of Britta Simon in FilesAnywhere that is linked to the Azure AD representation of her.</span></span>
3. <span data-ttu-id="3337e-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3337e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
4. <span data-ttu-id="3337e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3337e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3337e-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3337e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3337e-149">En esta sección, habilitará el inicio de sesión único de Azure AD en el Portal de administración de Azure y configurará el inicio de sesión único en la aplicación FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="3337e-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FilesAnywhere application.</span></span>

<span data-ttu-id="3337e-150">**Para configurar el inicio de sesión único de Azure AD con FilesAnywhere, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3337e-150">**To configure Azure AD single sign-on with FilesAnywhere, perform the following steps:**</span></span>

1. <span data-ttu-id="3337e-151">En el Portal de administración de Azure, en la página de integración de la aplicación **FilesAnywhere**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3337e-151">In the Azure Management portal, on the **FilesAnywhere** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="3337e-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3337e-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. <span data-ttu-id="3337e-155">En la sección **Dominio y direcciones URL de FilesAnywhere**, si quiere configurar la aplicación en **modo iniciado por ID**:</span><span class="sxs-lookup"><span data-stu-id="3337e-155">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    <span data-ttu-id="3337e-157">a.</span><span class="sxs-lookup"><span data-stu-id="3337e-157">a.</span></span> <span data-ttu-id="3337e-158">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`.</span><span class="sxs-lookup"><span data-stu-id="3337e-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span></span>
> [!NOTE]
> <span data-ttu-id="3337e-159">Tenga en cuenta que el valor **215** de **clientid** es simplemente un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3337e-159">Please note that the value **215** is a **clientid** and is just an example.</span></span> <span data-ttu-id="3337e-160">Es necesario reemplazarlo con el valor de clientid real.</span><span class="sxs-lookup"><span data-stu-id="3337e-160">You need to replace it with the actual clientid value.</span></span>

4. <span data-ttu-id="3337e-161">En la sección **Dominio y direcciones URL de FilesAnywhere**, si quiere configurar la aplicación en **modo iniciado por SP**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="3337e-161">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    <span data-ttu-id="3337e-163">a.</span><span class="sxs-lookup"><span data-stu-id="3337e-163">a.</span></span> <span data-ttu-id="3337e-164">Haga clic en la opción **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="3337e-164">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="3337e-165">b.</span><span class="sxs-lookup"><span data-stu-id="3337e-165">b.</span></span> <span data-ttu-id="3337e-166">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<sub domain>.filesanywhere.com/`.</span><span class="sxs-lookup"><span data-stu-id="3337e-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<sub domain>.filesanywhere.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3337e-167">Tenga en cuenta que estos no son valores reales.</span><span class="sxs-lookup"><span data-stu-id="3337e-167">Please note that these are not the real values.</span></span> <span data-ttu-id="3337e-168">Tendrá que actualizar estos valores con la dirección URL de inicio de sesión y la dirección URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="3337e-168">You have to update these values with the actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="3337e-169">Póngase en contacto con el [equipo de soporte técnico de FilesAnywhere](mailto:support@FilesAnywhere.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="3337e-169">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) to get these values.</span></span> 

5. <span data-ttu-id="3337e-170">La aplicación FilesAnywhere espera las aserciones de SAML en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="3337e-170">FilesAnywhere Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="3337e-171">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="3337e-171">Please configure the following claims for this application.</span></span> <span data-ttu-id="3337e-172">Puede administrar los valores de estos atributos en la sección "**Atributos de usuario**" de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3337e-172">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="3337e-173">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="3337e-173">The following screenshot shows an example for this.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    <span data-ttu-id="3337e-175">Cuando los usuarios se suscriben con FilesAnywhere obtienen el valor del atributo **clientid** del equipo de [FilesAnywhere](mailto:support@FilesAnywhere.com).</span><span class="sxs-lookup"><span data-stu-id="3337e-175">When the users signs up with FilesAnywhere they get the value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span></span> <span data-ttu-id="3337e-176">Tendrá que agregar el atributo "Client Id" con el valor único proporcionado por FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="3337e-176">You have to add the "Client Id" attribute with the unique value provided by FilesAnywhere.</span></span> <span data-ttu-id="3337e-177">Todos estos atributos mostrados anteriormente son obligatorios.</span><span class="sxs-lookup"><span data-stu-id="3337e-177">All these attributes shown above are required.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="3337e-178">Tenga en cuenta que el valor **2331** de **clientid** es simplemente un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3337e-178">Please note that the value **2331** of **clientid** is just an example.</span></span> <span data-ttu-id="3337e-179">Debe proporcionar el valor real.</span><span class="sxs-lookup"><span data-stu-id="3337e-179">You need to provide the actual value.</span></span>


6. <span data-ttu-id="3337e-180">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo Token SAML como muestra la imagen anterior y realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="3337e-180">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="3337e-181">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="3337e-181">Attribute Name</span></span> | <span data-ttu-id="3337e-182">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="3337e-182">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="3337e-183">clientid</span><span class="sxs-lookup"><span data-stu-id="3337e-183">clientid</span></span> | <span data-ttu-id="3337e-184">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="3337e-184">*"uniquevalue"*</span></span> |

    <span data-ttu-id="3337e-185">a.</span><span class="sxs-lookup"><span data-stu-id="3337e-185">a.</span></span> <span data-ttu-id="3337e-186">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="3337e-186">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    <span data-ttu-id="3337e-189">b.</span><span class="sxs-lookup"><span data-stu-id="3337e-189">b.</span></span> <span data-ttu-id="3337e-190">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="3337e-190">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="3337e-191">c.</span><span class="sxs-lookup"><span data-stu-id="3337e-191">c.</span></span> <span data-ttu-id="3337e-192">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="3337e-192">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="3337e-193">d.</span><span class="sxs-lookup"><span data-stu-id="3337e-193">d.</span></span> <span data-ttu-id="3337e-194">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3337e-194">Click **Ok**</span></span>

7. <span data-ttu-id="3337e-195">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3337e-195">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3337e-197">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3337e-197">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. <span data-ttu-id="3337e-199">En la sección **Configuración de FilesAnywhere**, haga clic en **Configurar FilesAnywhere** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="3337e-199">On the **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** to open **Configure sign-on** window.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. <span data-ttu-id="3337e-202">Para completar la configuración de SSO para su aplicación en FilesAnywhere, póngase en contacto con el [equipo de soporte técnico de FilesAnywhere](mailto:support@FilesAnywhere.com) y proporcióneles el certificado de firma de tokens SAML descargado y la dirección URL de inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3337e-202">To get SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them the downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3337e-203">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3337e-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="3337e-204">El objetivo de esta sección es crear un usuario de prueba en el Portal de administración de Azure llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3337e-204">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="3337e-206">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="3337e-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3337e-207">En el panel de navegación izquierdo del **Portal de administración de Azure**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3337e-207">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3337e-209">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="3337e-209">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3337e-211">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="3337e-211">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3337e-213">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="3337e-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3337e-215">a.</span><span class="sxs-lookup"><span data-stu-id="3337e-215">a.</span></span> <span data-ttu-id="3337e-216">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3337e-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3337e-217">b.</span><span class="sxs-lookup"><span data-stu-id="3337e-217">b.</span></span> <span data-ttu-id="3337e-218">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3337e-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3337e-219">c.</span><span class="sxs-lookup"><span data-stu-id="3337e-219">c.</span></span> <span data-ttu-id="3337e-220">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3337e-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3337e-221">d.</span><span class="sxs-lookup"><span data-stu-id="3337e-221">d.</span></span> <span data-ttu-id="3337e-222">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3337e-222">Click **Create**.</span></span> 



### <a name="creating-a-filesanywhere-test-user"></a><span data-ttu-id="3337e-223">Creación de un usuario de prueba para FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="3337e-223">Creating a FilesAnywhere test user</span></span>

<span data-ttu-id="3337e-224">La aplicación admite el aprovisionamiento de usuarios Just-In-Time y, tras la autenticación, los usuarios se crearán automáticamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3337e-224">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3337e-225">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3337e-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3337e-226">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="3337e-226">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FilesAnywhere.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3337e-228">**Para asignar Britta Simon a FilesAnywhere, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="3337e-228">**To assign Britta Simon to FilesAnywhere, perform the following steps:**</span></span>

1. <span data-ttu-id="3337e-229">En el Portal de administración de Azure, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. A continuación, haga clic en **All applications** (Todas las aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="3337e-229">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3337e-231">En la lista de aplicaciones, seleccione **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="3337e-231">In the applications list, select **FilesAnywhere**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. <span data-ttu-id="3337e-233">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3337e-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3337e-235">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3337e-235">Click **Add** button.</span></span> <span data-ttu-id="3337e-236">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3337e-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3337e-238">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="3337e-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3337e-239">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3337e-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3337e-240">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3337e-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="3337e-241">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3337e-241">Testing single sign-on</span></span>

<span data-ttu-id="3337e-242">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3337e-242">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3337e-243">Al hacer clic en el icono de FilesAnywhere en el panel de acceso, debería iniciar sesión automáticamente en la aplicación FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="3337e-243">When you click the FilesAnywhere tile in the Access Panel, you should get automatically signed-on to your FilesAnywhere application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="3337e-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3337e-244">Additional resources</span></span>

* [<span data-ttu-id="3337e-245">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3337e-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3337e-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3337e-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
