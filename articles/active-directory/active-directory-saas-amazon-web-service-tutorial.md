---
title: "Tutorial: Integración de Azure Active Directory con Amazon Web Services (AWS) | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y Amazon Web Services (AWS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 0fb9c8f428368271b548e3f174726fa01ea910c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="19531-103">Tutorial: integración de Azure Active Directory con Amazon Web Service (AWS)</span><span class="sxs-lookup"><span data-stu-id="19531-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="19531-104">En este tutorial, obtendrá información sobre cómo integrar Amazon Web Services (AWS) con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="19531-104">In this tutorial, you learn how to integrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="19531-105">La integración de Amazon Web Services (AWS) con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="19531-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="19531-106">Puede controlar en Azure AD quién tiene acceso a Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="19531-106">You can control in Azure AD who has access to Amazon Web Services (AWS)</span></span>
- <span data-ttu-id="19531-107">Puede permitir que los usuarios inicien sesión automáticamente en Amazon Web Services (AWS) (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19531-107">You can enable your users to automatically get signed-on to Amazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="19531-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="19531-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="19531-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="19531-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Amazon Web Services (AWS), it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="19531-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="19531-110">Prerequisites</span></span>

<span data-ttu-id="19531-111">Para configurar la integración de Azure AD con Amazon Web Services (AWS), necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="19531-111">To configure Azure AD integration with Amazon Web Services (AWS), you need the following items:</span></span>

- <span data-ttu-id="19531-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="19531-112">An Azure AD subscription</span></span>
- <span data-ttu-id="19531-113">Suscripción habilitada para el inicio de sesión único en Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="19531-113">Amazon Web Services (AWS) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="19531-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="19531-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="19531-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="19531-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="19531-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="19531-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="19531-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="19531-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="19531-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="19531-118">Scenario description</span></span>
<span data-ttu-id="19531-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="19531-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="19531-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="19531-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="19531-121">Adición de Amazon Web Services (AWS) desde la galería</span><span class="sxs-lookup"><span data-stu-id="19531-121">Adding Amazon Web Services (AWS) from the gallery</span></span>
2. <span data-ttu-id="19531-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="19531-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-the-gallery"></a><span data-ttu-id="19531-123">Adición de Amazon Web Services (AWS) desde la galería</span><span class="sxs-lookup"><span data-stu-id="19531-123">Adding Amazon Web Services (AWS) from the gallery</span></span>
<span data-ttu-id="19531-124">Para configurar la integración de Amazon Web Services (AWS) en Azure AD, es preciso agregar Amazon Web Services (AWS) desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="19531-124">To configure the integration of Amazon Web Services (AWS) into Azure AD, you need to add Amazon Web Services (AWS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="19531-125">**Para agregar Amazon Web Services (AWS) desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="19531-125">**To add Amazon Web Services (AWS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="19531-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="19531-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="19531-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="19531-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="19531-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="19531-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="19531-131">Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="19531-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="19531-133">En el cuadro de búsqueda, escriba **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="19531-133">In the search box, type **Amazon Web Services (AWS)**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. <span data-ttu-id="19531-135">En el panel de resultados, seleccione **Amazon Web Services (AWS)** y, después, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="19531-135">In the results panel, select **Amazon Web Services (AWS)**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="19531-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="19531-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="19531-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Amazon Web Services (AWS) con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="19531-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="19531-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Amazon Web Services (AWS) para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19531-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Amazon Web Services (AWS) is to a user in Azure AD.</span></span> <span data-ttu-id="19531-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="19531-140">In other words, a link relationship between an Azure AD user and the related user in Amazon Web Services (AWS) needs to be established.</span></span>

<span data-ttu-id="19531-141">Esta relación de vínculo se establece al asignar el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="19531-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="19531-142">Para configurar y probar el inicio de sesión único de Azure AD con Amazon Web Services (AWS), es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="19531-142">To configure and test Azure AD single sign-on with Amazon Web Services (AWS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="19531-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="19531-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="19531-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="19531-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="19531-145">**[Creación de un usuario de prueba de Amazon Web Services](#creating-an-amazon-web-services-test-user)**: para tener un homólogo de Britta Simon en Amazon Web Services (AWS) que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19531-145">**[Creating an Amazon Web Services test user](#creating-an-amazon-web-services-test-user)** - to have a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="19531-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19531-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="19531-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="19531-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="19531-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="19531-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="19531-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación de Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="19531-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="19531-150">**Para configurar el inicio de sesión único de Azure AD con Amazon Web Services (AWS), realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="19531-150">**To configure Azure AD single sign-on with Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="19531-151">En Azure Portal, en la página de integración de la aplicación de **Amazon Web Services (AWS)**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="19531-151">In the Azure Portal, on the **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="19531-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="19531-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. <span data-ttu-id="19531-155">En la sección **Dominio y direcciones URL de Amazon Web Services (AWS)**, el usuario no tiene que realizar ningún paso ya que la aplicación se ha integrado previamente con Azure.</span><span class="sxs-lookup"><span data-stu-id="19531-155">On the **Amazon Web Services (AWS) Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. <span data-ttu-id="19531-157">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="19531-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. <span data-ttu-id="19531-159">La aplicación de software de Amazon Web Services (AWS) espera las aserciones de SAML en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="19531-159">The Amazon Web Services (AWS) Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="19531-160">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="19531-160">Please configure the following claims for this application.</span></span> <span data-ttu-id="19531-161">Puede administrar los valores de estos atributos en la sección "**Atributos de usuario**" de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="19531-161">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="19531-162">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="19531-162">The following screenshot shows an example for this.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. <span data-ttu-id="19531-164">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo Token SAML como muestra la imagen anterior y realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="19531-164">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="19531-165">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="19531-165">Attribute Name</span></span>  | <span data-ttu-id="19531-166">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="19531-166">Attribute Value</span></span> | <span data-ttu-id="19531-167">Espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="19531-167">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="19531-168">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="19531-168">RoleSessionName</span></span> | <span data-ttu-id="19531-169">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="19531-169">user.userprincipalname</span></span> | <span data-ttu-id="19531-170">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="19531-170">https://aws.amazon.com/SAML/Attributes</span></span> |
    | <span data-ttu-id="19531-171">Rol</span><span class="sxs-lookup"><span data-stu-id="19531-171">Role</span></span>            | <span data-ttu-id="19531-172">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="19531-172">user.assignedroles</span></span> |  <span data-ttu-id="19531-173">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="19531-173">https://aws.amazon.com/SAML/Attributes</span></span> |
    
    >[!TIP]
    ><span data-ttu-id="19531-174">Debe configurar el aprovisionamiento de usuarios en Azure AD para capturar todos los roles de la consola de AWS.</span><span class="sxs-lookup"><span data-stu-id="19531-174">You need to configure the user provisioning in Azure AD to fetch all the roles from AWS Console.</span></span> <span data-ttu-id="19531-175">Consulte los pasos de aprovisionamiento a continuación.</span><span class="sxs-lookup"><span data-stu-id="19531-175">Please refer the provisioning steps below.</span></span>

    <span data-ttu-id="19531-176">a.</span><span class="sxs-lookup"><span data-stu-id="19531-176">a.</span></span> <span data-ttu-id="19531-177">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="19531-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="19531-179">b.</span><span class="sxs-lookup"><span data-stu-id="19531-179">b.</span></span> <span data-ttu-id="19531-180">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="19531-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="19531-182">c.</span><span class="sxs-lookup"><span data-stu-id="19531-182">c.</span></span> <span data-ttu-id="19531-183">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="19531-183">From the **Value** list, type the attribute value shown for that row.</span></span> <span data-ttu-id="19531-184">Agregue el valor del espacio de nombres tal como se ha indicado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="19531-184">Add the Namespace value as given above.</span></span>
    
    <span data-ttu-id="19531-185">d.</span><span class="sxs-lookup"><span data-stu-id="19531-185">d.</span></span> <span data-ttu-id="19531-186">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="19531-186">Click **Ok**.</span></span>

7. <span data-ttu-id="19531-187">Haga clic en el botón **Guardar** para guardar la configuración en Azure.</span><span class="sxs-lookup"><span data-stu-id="19531-187">Click **Save** button to save the settings on Azure.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="19531-189">En otra ventana del explorador, inicie sesión en su sitio de la compañía de Amazon Web Services (AWS) como administrador.</span><span class="sxs-lookup"><span data-stu-id="19531-189">In a different browser window, sign-on to your Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="19531-190">Haga clic en **Página principal de la consola**.</span><span class="sxs-lookup"><span data-stu-id="19531-190">Click **Console Home**.</span></span>
   
    ![Configurar inicio de sesión único][11]

10. <span data-ttu-id="19531-192">Haga clic en **IAM** en el servicio **Security, Identity & Compliance** (Seguridad, identidad y cumplimiento).</span><span class="sxs-lookup"><span data-stu-id="19531-192">Click **IAM** from **Security, Identity & Compliance** service.</span></span>
   
    ![Configurar inicio de sesión único][12]

11. <span data-ttu-id="19531-194">Haga clic en **Proveedores de identidades** y, después, en **Create Provider** (Crear proveedor).</span><span class="sxs-lookup"><span data-stu-id="19531-194">Click **Identity Providers**, and then click **Create Provider**.</span></span>
   
    ![Configurar inicio de sesión único][13]

12. <span data-ttu-id="19531-196">En la página de diálogo **Configure Provider** (Configurar proveedor), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="19531-196">On the **Configure Provider** dialog page, perform the following steps:</span></span>
   
    ![Configurar inicio de sesión único][14]
 
    <span data-ttu-id="19531-198">a.</span><span class="sxs-lookup"><span data-stu-id="19531-198">a.</span></span> <span data-ttu-id="19531-199">En **Tipo de proveedor**, seleccione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="19531-199">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="19531-200">b.</span><span class="sxs-lookup"><span data-stu-id="19531-200">b.</span></span> <span data-ttu-id="19531-201">En el cuadro de texto **Provider Name** (Nombre de proveedor), escriba un nombre de proveedor (por ejemplo, *WAAD*).</span><span class="sxs-lookup"><span data-stu-id="19531-201">In the **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>

    <span data-ttu-id="19531-202">c.</span><span class="sxs-lookup"><span data-stu-id="19531-202">c.</span></span> <span data-ttu-id="19531-203">Haga clic en **Elegir archivo**para cargar el archivo de metadatos descargado.</span><span class="sxs-lookup"><span data-stu-id="19531-203">To upload your downloaded metadata file, click **Choose File**.</span></span>

    <span data-ttu-id="19531-204">d.</span><span class="sxs-lookup"><span data-stu-id="19531-204">d.</span></span> <span data-ttu-id="19531-205">Haga clic en **Siguiente paso**.</span><span class="sxs-lookup"><span data-stu-id="19531-205">Click **Next Step**.</span></span>

13. <span data-ttu-id="19531-206">En la página de diálogo **Verify Provider Information** (Comprobar la información del proveedor), haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="19531-206">On the **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![Configurar inicio de sesión único][15]

14. <span data-ttu-id="19531-208">Haga clic en **Roles** y, después, en **Crear nuevo rol**.</span><span class="sxs-lookup"><span data-stu-id="19531-208">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![Configurar inicio de sesión único][16]

15. <span data-ttu-id="19531-210">En el cuadro de diálogo **Set Role Name** (Establecer nombre de rol), realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="19531-210">On the **Set Role Name** dialog, perform the following steps:</span></span> 
    
    ![Configurar inicio de sesión único][17] 

    <span data-ttu-id="19531-212">a.</span><span class="sxs-lookup"><span data-stu-id="19531-212">a.</span></span> <span data-ttu-id="19531-213">En el cuadro de texto **Nombre de rol**, escriba un nombre de rol (por ejemplo, *TestUser*).</span><span class="sxs-lookup"><span data-stu-id="19531-213">In the **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 

    <span data-ttu-id="19531-214">b.</span><span class="sxs-lookup"><span data-stu-id="19531-214">b.</span></span> <span data-ttu-id="19531-215">Haga clic en **Siguiente paso**.</span><span class="sxs-lookup"><span data-stu-id="19531-215">Click **Next Step**.</span></span>

16. <span data-ttu-id="19531-216">En el cuadro de diálogo **Select Role Type** (Seleccionar tipo de rol), realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="19531-216">On the **Select Role Type** dialog, perform the following steps:</span></span> 
    
    ![Configurar inicio de sesión único][18] 

    <span data-ttu-id="19531-218">a.</span><span class="sxs-lookup"><span data-stu-id="19531-218">a.</span></span> <span data-ttu-id="19531-219">Seleccione **Rol de acceso del proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="19531-219">Select **Role For Identity Provider Access**.</span></span> 

    <span data-ttu-id="19531-220">b.</span><span class="sxs-lookup"><span data-stu-id="19531-220">b.</span></span> <span data-ttu-id="19531-221">En la sección **Conceder acceso de inicio de sesión único web (WebSSO)** a los proveedores de SAML, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="19531-221">In the **Grant Web Single Sign-On (WebSSO) access to SAML providers** section, click **Select**.</span></span>

17. <span data-ttu-id="19531-222">En el cuadro de diálogo **Establecer confianza** , realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="19531-222">On the **Establish Trust** dialog, perform the following steps:</span></span>  
    
    ![Configurar inicio de sesión único][19] 

    <span data-ttu-id="19531-224">a.</span><span class="sxs-lookup"><span data-stu-id="19531-224">a.</span></span> <span data-ttu-id="19531-225">Como proveedor de SAML, seleccione el proveedor de SAML que ha creado antes (por ejemplo, *WAAD*).</span><span class="sxs-lookup"><span data-stu-id="19531-225">As SAML provider, select the SAML provider you have created previously (e.g.: *WAAD*)</span></span>
  
    <span data-ttu-id="19531-226">b.</span><span class="sxs-lookup"><span data-stu-id="19531-226">b.</span></span> <span data-ttu-id="19531-227">Haga clic en **Siguiente paso**.</span><span class="sxs-lookup"><span data-stu-id="19531-227">Click **Next Step**.</span></span>

18. <span data-ttu-id="19531-228">En el diálogo **Verify Role Trust** (Comprobar la confianza del rol), haga clic en **Paso siguiente**.</span><span class="sxs-lookup"><span data-stu-id="19531-228">On the **Verify Role Trust** dialog, click **Next Step**.</span></span>
    
    ![Configurar inicio de sesión único][32]

19. <span data-ttu-id="19531-230">En el diálogo **Attach Policy** (Adjuntar directiva), haga clic en **Paso siguiente**.</span><span class="sxs-lookup"><span data-stu-id="19531-230">On the **Attach Policy** dialog, click **Next Step**.</span></span>
    
    ![Configurar inicio de sesión único][33]

20. <span data-ttu-id="19531-232">En el cuadro de diálogo **Revisar** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="19531-232">On the **Review** dialog, perform the following steps:</span></span>
    
    ![Configurar inicio de sesión único][34]
 
    <span data-ttu-id="19531-234">a.</span><span class="sxs-lookup"><span data-stu-id="19531-234">a.</span></span> <span data-ttu-id="19531-235">Haga clic en **Crear rol**.</span><span class="sxs-lookup"><span data-stu-id="19531-235">Click **Create Role**.</span></span>

    <span data-ttu-id="19531-236">b.</span><span class="sxs-lookup"><span data-stu-id="19531-236">b.</span></span> <span data-ttu-id="19531-237">Cree tantos roles como sea necesario y asígnelos al proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="19531-237">Create as many roles as needed and map them to the Identity Provider.</span></span>

21. <span data-ttu-id="19531-238">Configure ahora el aprovisionamiento de usuarios para capturar todos los roles de AWS.</span><span class="sxs-lookup"><span data-stu-id="19531-238">Now configure the user provisioning to fetch all the roles from AWS</span></span>

    <span data-ttu-id="19531-239">a.</span><span class="sxs-lookup"><span data-stu-id="19531-239">a.</span></span> <span data-ttu-id="19531-240">En la consola de AWS, regístrese con la cuenta raíz.</span><span class="sxs-lookup"><span data-stu-id="19531-240">In the AWS Console login with your root account</span></span>

    <span data-ttu-id="19531-241">b.</span><span class="sxs-lookup"><span data-stu-id="19531-241">b.</span></span> <span data-ttu-id="19531-242">En la esquina superior derecha, haga clic en su nombre y después haga clic en la opción **My Security Credentials** (Mis credenciales de seguridad).</span><span class="sxs-lookup"><span data-stu-id="19531-242">In the top right corner click your name and then click the **My Security Credentials** option.</span></span> <span data-ttu-id="19531-243">Se abrirá una pantalla como un mensaje de advertencia.</span><span class="sxs-lookup"><span data-stu-id="19531-243">This will open up a screen as a warning message.</span></span> <span data-ttu-id="19531-244">Haga clic en el botón **Security Credentials** (Credenciales de seguridad) para pasar a la pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="19531-244">Click the button **Security Credentials** button to pass the screen.</span></span>
        
       ![Configurar inicio de sesión único][36]

       ![Configurar inicio de sesión único][37]

    <span data-ttu-id="19531-247">c.</span><span class="sxs-lookup"><span data-stu-id="19531-247">c.</span></span> <span data-ttu-id="19531-248">En la sección de claves de acceso, haga clic en el botón **Create New Access Key** (Crear clave de acceso).</span><span class="sxs-lookup"><span data-stu-id="19531-248">In the Access Keys section click the **Create New Access Key** button.</span></span> <span data-ttu-id="19531-249">Esto genera el identificador de clave de acceso y un valor de token.</span><span class="sxs-lookup"><span data-stu-id="19531-249">This generates the Access Key ID and a token value.</span></span>
    
       ![Configurar inicio de sesión único][38]

    <span data-ttu-id="19531-251">d.</span><span class="sxs-lookup"><span data-stu-id="19531-251">d.</span></span> <span data-ttu-id="19531-252">Copie estos dos valores y descárguelos para no perderlos.</span><span class="sxs-lookup"><span data-stu-id="19531-252">Copy both these values and also download it, so that you don't lose it.</span></span>

    <span data-ttu-id="19531-253">e.</span><span class="sxs-lookup"><span data-stu-id="19531-253">e.</span></span> <span data-ttu-id="19531-254">En Azure Portal, en la página de integración de la aplicación de Amazon Web Services (AWS), haga clic en **Aprovisionamiento**.</span><span class="sxs-lookup"><span data-stu-id="19531-254">In the Azure Portal, on the Amazon Web Services (AWS) application integration page, click **Provisioning**.</span></span>
        
       ![Configurar inicio de sesión único][35]

    <span data-ttu-id="19531-256">f.</span><span class="sxs-lookup"><span data-stu-id="19531-256">f.</span></span> <span data-ttu-id="19531-257">Establezca el modo de aprovisionamiento en **Automático**.</span><span class="sxs-lookup"><span data-stu-id="19531-257">Set the Provisioning mode to **Automatic**</span></span>
        
       ![Configurar inicio de sesión único][39]

    <span data-ttu-id="19531-259">g.</span><span class="sxs-lookup"><span data-stu-id="19531-259">g.</span></span> <span data-ttu-id="19531-260">Ahora, en los campos **clientsecret** y **Token secreto**, copie los valores correspondientes copiados de la consola de AWS.</span><span class="sxs-lookup"><span data-stu-id="19531-260">Now in the **clientsecret** and **Secret Token** paste the corresponding values, which you have copied from AWS Console.</span></span>
    
    <span data-ttu-id="19531-261">h.</span><span class="sxs-lookup"><span data-stu-id="19531-261">h.</span></span> <span data-ttu-id="19531-262">Puede hacer clic en el botón **Probar conexión** para probar la conectividad.</span><span class="sxs-lookup"><span data-stu-id="19531-262">You can click the **Test Connection** button to test the connectivity.</span></span> <span data-ttu-id="19531-263">Si la conexión es correcta, puede empezar con el aprovisionamiento del conector.</span><span class="sxs-lookup"><span data-stu-id="19531-263">Once that is successful then you can start the provisioning connector.</span></span>
       
       ![Configurar inicio de sesión único][40]

    <span data-ttu-id="19531-265">i.</span><span class="sxs-lookup"><span data-stu-id="19531-265">i.</span></span> <span data-ttu-id="19531-266">Ahora, habilite el Estado de aprovisionamiento en **Activado**.</span><span class="sxs-lookup"><span data-stu-id="19531-266">Now enable the Provisioning Status to **On**.</span></span> <span data-ttu-id="19531-267">Esto permite capturar los roles de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="19531-267">This starts fetching the roles from the application.</span></span>

       ![Configurar inicio de sesión único][41]

    > [!NOTE]
    > <span data-ttu-id="19531-269">El aprovisionamiento de Azure AD se ejecuta después de un tiempo determinado para sincronizar los roles de AWS.</span><span class="sxs-lookup"><span data-stu-id="19531-269">Azure AD Provisioning service runs every after some time to sync the roles from AWS.</span></span> <span data-ttu-id="19531-270">Debería ver todos los roles de AWS adjuntos al proveedor de identidades en Azure AD, a fin de poder usarlos al asignar la aplicación a usuarios o grupos.</span><span class="sxs-lookup"><span data-stu-id="19531-270">You should see all the Identity Provider attached AWS roles into Azure AD and you can use them while assigning the application to users or groups.</span></span>

<!--### Next steps

To ensure users can sign-in to Amazon Web Services (AWS) after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Amazon Web Services (AWS) in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="19531-271">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="19531-271">Creating an Azure AD test user</span></span>
<span data-ttu-id="19531-272">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="19531-272">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="19531-274">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="19531-274">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="19531-275">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="19531-275">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="19531-277">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="19531-277">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="19531-279">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="19531-279">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="19531-281">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="19531-281">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="19531-283">a.</span><span class="sxs-lookup"><span data-stu-id="19531-283">a.</span></span> <span data-ttu-id="19531-284">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="19531-284">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="19531-285">b.</span><span class="sxs-lookup"><span data-stu-id="19531-285">b.</span></span> <span data-ttu-id="19531-286">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="19531-286">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="19531-287">c.</span><span class="sxs-lookup"><span data-stu-id="19531-287">c.</span></span> <span data-ttu-id="19531-288">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="19531-288">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="19531-289">d.</span><span class="sxs-lookup"><span data-stu-id="19531-289">d.</span></span> <span data-ttu-id="19531-290">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="19531-290">Click **Create**.</span></span>
 
### <a name="creating-an-amazon-web-services-test-user"></a><span data-ttu-id="19531-291">Creación de un usuario de prueba de Amazon Web Services</span><span class="sxs-lookup"><span data-stu-id="19531-291">Creating an Amazon Web Services test user</span></span>

<span data-ttu-id="19531-292">Para permitir que los usuarios de Azure AD se registren en Amazon Web Services (AWS), es necesario aprovisionarlos en Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="19531-292">In order to enable Azure AD users to log in to Amazon Web Services (AWS), they must be provisioned into Amazon Web Services (AWS).</span></span> <span data-ttu-id="19531-293">En el caso de Amazon Web Services (AWS), el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="19531-293">In the case of Amazon Web Services (AWS), provisioning is a manual task.</span></span>

<span data-ttu-id="19531-294">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="19531-294">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="19531-295">Inicie sesión en su sitio de la compañía de **Amazon Web Services (AWS)** como administrador.</span><span class="sxs-lookup"><span data-stu-id="19531-295">Log in to your **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="19531-296">Haga clic en el icono de **Página principal de la consola** .</span><span class="sxs-lookup"><span data-stu-id="19531-296">Click the **Console Home** icon.</span></span> 
   
    ![Configurar inicio de sesión único][11]

3. <span data-ttu-id="19531-298">Haga clic en Administración de identidades y acceso.</span><span class="sxs-lookup"><span data-stu-id="19531-298">Click Identity and Access Management.</span></span> 
   
    ![Configurar inicio de sesión único][28]

4. <span data-ttu-id="19531-300">En el panel, haga clic en **Users** (Usuarios) y luego en **Create New Users** (Crear usuarios).</span><span class="sxs-lookup"><span data-stu-id="19531-300">In the Dashboard, click **Users**, and then click **Create New Users**.</span></span> 
   
    ![Configurar inicio de sesión único][29]

5. <span data-ttu-id="19531-302">En el cuadro de diálogo Crear usuario, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="19531-302">On the Create User dialog, perform the following steps:</span></span> 
   
    ![Configurar inicio de sesión único][30]   
    
    <span data-ttu-id="19531-304">a.</span><span class="sxs-lookup"><span data-stu-id="19531-304">a.</span></span> <span data-ttu-id="19531-305">En los cuadros de texto **Escribir nombres de usuario** , escriba el nombre de usuario de Brita Simon (userprincipalname) en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19531-305">In the **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span>

    <span data-ttu-id="19531-306">b.</span><span class="sxs-lookup"><span data-stu-id="19531-306">b.</span></span> <span data-ttu-id="19531-307">Haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="19531-307">Click **Create.**</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="19531-308">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="19531-308">Assigning the Azure AD test user</span></span>

<span data-ttu-id="19531-309">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="19531-309">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Amazon Web Services (AWS).</span></span>

![Asignar usuario][200] 

<span data-ttu-id="19531-311">**Para asignar Britta Simon a Amazon Web Services (AWS), realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="19531-311">**To assign Britta Simon to Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="19531-312">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="19531-312">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="19531-314">En la lista de aplicaciones, seleccione **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="19531-314">In the applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. <span data-ttu-id="19531-316">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="19531-316">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="19531-318">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="19531-318">Click **Add** button.</span></span> <span data-ttu-id="19531-319">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="19531-319">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="19531-321">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="19531-321">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="19531-322">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="19531-322">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="19531-323">En la pestaña **Seleccionar rol**, seleccione el rol apropiado para el usuario.</span><span class="sxs-lookup"><span data-stu-id="19531-323">On **Select Role** tab, select the appropriate role for the user.</span></span> <span data-ttu-id="19531-324">Todos estos roles se muestran con el nombre de rol y el nombre del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="19531-324">All these roles are shown with the role name and identity provider name.</span></span> <span data-ttu-id="19531-325">De esta forma, puede identificar con facilidad los roles de AWS.</span><span class="sxs-lookup"><span data-stu-id="19531-325">This way you can easily identify the roles from AWS.</span></span>

8. <span data-ttu-id="19531-326">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="19531-326">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="19531-327">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="19531-327">Testing single sign-on</span></span>

<span data-ttu-id="19531-328">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="19531-328">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="19531-329">Al hacer clic en el icono de Amazon Web Services (AWS) en el panel de acceso, automáticamente iniciará sesión en su aplicación de Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="19531-329">When you click the Amazon Web Services (AWS) tile in the Access Panel, you should get automatically signed-on to your Amazon Web Services (AWS) application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="19531-330">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="19531-330">Additional resources</span></span>

* [<span data-ttu-id="19531-331">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="19531-331">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="19531-332">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="19531-332">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
