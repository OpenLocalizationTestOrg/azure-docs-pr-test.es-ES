---
title: "Tutorial: integración de Azure Active Directory con Pluralsight | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Pluralsight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 62429643a108665544e42001d264046b5db1ec97
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a><span data-ttu-id="0364a-103">Tutorial: Integración de Azure Active Directory con Pluralsight</span><span class="sxs-lookup"><span data-stu-id="0364a-103">Tutorial: Azure Active Directory integration with Pluralsight</span></span>

<span data-ttu-id="0364a-104">En este tutorial, aprenderá a integrar Pluralsight con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0364a-104">In this tutorial, you learn how to integrate Pluralsight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0364a-105">Integrar Pluralsight con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0364a-105">Integrating Pluralsight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0364a-106">Puede controlar en Azure AD quién tiene acceso a Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="0364a-106">You can control in Azure AD who has access to Pluralsight</span></span>
- <span data-ttu-id="0364a-107">Puede permitir que los usuarios inicien sesión automáticamente en Pluralsight (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0364a-107">You can enable your users to automatically get signed-on to Pluralsight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0364a-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0364a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0364a-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0364a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0364a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0364a-110">Prerequisites</span></span>

<span data-ttu-id="0364a-111">Para configurar la integración de Azure AD con Pluralsight, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0364a-111">To configure Azure AD integration with Pluralsight, you need the following items:</span></span>

- <span data-ttu-id="0364a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0364a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0364a-113">Una suscripción habilitada para el inicio de sesión único en Pluralsight</span><span class="sxs-lookup"><span data-stu-id="0364a-113">A Pluralsight single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0364a-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0364a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0364a-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0364a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0364a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0364a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0364a-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0364a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0364a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0364a-118">Scenario description</span></span>
<span data-ttu-id="0364a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0364a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0364a-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="0364a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0364a-121">Incorporación de Pluralsight desde la galería</span><span class="sxs-lookup"><span data-stu-id="0364a-121">Adding Pluralsight from the gallery</span></span>
2. <span data-ttu-id="0364a-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0364a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pluralsight-from-the-gallery"></a><span data-ttu-id="0364a-123">Incorporación de Pluralsight desde la galería</span><span class="sxs-lookup"><span data-stu-id="0364a-123">Adding Pluralsight from the gallery</span></span>
<span data-ttu-id="0364a-124">Para configurar la integración de Pluralsight en Azure AD, deberá agregar Pluralsight desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="0364a-124">To configure the integration of Pluralsight into Azure AD, you need to add Pluralsight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0364a-125">**Para agregar Pluralsight desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="0364a-125">**To add Pluralsight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0364a-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0364a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0364a-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0364a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0364a-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0364a-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0364a-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0364a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0364a-133">En el cuadro de búsqueda, escriba **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="0364a-133">In the search box, type **Pluralsight**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_search.png)

5. <span data-ttu-id="0364a-135">En el panel de resultados, seleccione **Pluralsight** y, después, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0364a-135">In the results panel, select **Pluralsight**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0364a-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0364a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0364a-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Pluralsight con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0364a-138">In this section, you configure and test Azure AD single sign-on with Pluralsight based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0364a-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Pluralsight para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0364a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pluralsight is to a user in Azure AD.</span></span> <span data-ttu-id="0364a-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="0364a-140">In other words, a link relationship between an Azure AD user and the related user in Pluralsight needs to be established.</span></span>

<span data-ttu-id="0364a-141">Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario** de Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="0364a-141">In Pluralsight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0364a-142">Para configurar y probar el inicio de sesión único de Azure AD con Pluralsight, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0364a-142">To configure and test Azure AD single sign-on with Pluralsight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0364a-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="0364a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0364a-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0364a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0364a-145">**[Creación de un usuario de prueba de Pluralsight](#creating-a-pluralsight-test-user)**: el objetivo es tener un homólogo de Britta Simon en Pluralsight que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0364a-145">**[Creating a Pluralsight test user](#creating-a-pluralsight-test-user)** - to have a counterpart of Britta Simon in Pluralsight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0364a-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0364a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0364a-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0364a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0364a-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0364a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0364a-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="0364a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pluralsight application.</span></span>

<span data-ttu-id="0364a-150">**Para configurar el inicio de sesión único de Azure AD con Pluralsight, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="0364a-150">**To configure Azure AD single sign-on with Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="0364a-151">En la página de integración de la aplicación **Pluralsight** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0364a-151">In the Azure portal, on the **Pluralsight** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0364a-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0364a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

3. <span data-ttu-id="0364a-155">En la sección **Dominio y direcciones URL de Pluralsight**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="0364a-155">On the **Pluralsight Domain and URLs** section, perform the following:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_url.png)

    <span data-ttu-id="0364a-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<instance name>.pluralsight.com/sso/<company name>`.</span><span class="sxs-lookup"><span data-stu-id="0364a-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.pluralsight.com/sso/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0364a-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="0364a-158">This value is not real.</span></span> <span data-ttu-id="0364a-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="0364a-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="0364a-160">Póngase en contacto con el [equipo de atención al cliente de Pluralsight](mailto:support@pluralsight.com) para obtenerlo.</span><span class="sxs-lookup"><span data-stu-id="0364a-160">Contact [Pluralsight Client support team](mailto:support@pluralsight.com) to get this value.</span></span> 
 


4. <span data-ttu-id="0364a-161">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0364a-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

5. <span data-ttu-id="0364a-163">El objetivo de esta sección es habilitar el inicio de sesión único de Azure AD en Azure Portal y configurarlo en la aplicación Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="0364a-163">The objective of this section is to enable Azure AD single sign-on in the Azure portal and to configure SSO in the Pluralsight application.</span></span>

    <span data-ttu-id="0364a-164">La aplicación Pluralsight espera las aserciones de SAML en un formato específico, lo cual requiere que se agreguen asignaciones de atributos personalizados a la configuración de los atributos del token de SAML.</span><span class="sxs-lookup"><span data-stu-id="0364a-164">The Pluralsight application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="0364a-165">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="0364a-165">The following screenshot shows an example for this.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    ><span data-ttu-id="0364a-167">También puede agregar el atributo **"Id. exclusivo"** con el valor correspondiente como EmployeeID o cualquier otro aspecto que se adapte a su organización.</span><span class="sxs-lookup"><span data-stu-id="0364a-167">You can also add the **"Unique ID"** attribute with the appropriate value like EmployeeID or something else which suits for your organization.</span></span> <span data-ttu-id="0364a-168">Tenga en cuenta que no es un atributo obligatorio, pero puede agregarlo para identificar al usuario único.</span><span class="sxs-lookup"><span data-stu-id="0364a-168">Also note that this is not the required attribute; however, you can add it to  identify the unique user.</span></span> 

6. <span data-ttu-id="0364a-169">Para agregar los **atributos de token de SAML**requeridos, para cada fila mostrada en la tabla siguiente, realice los pasos que se indican a continuación:</span><span class="sxs-lookup"><span data-stu-id="0364a-169">To add the required **SAML token attributes**, for each row shown in the table below, perform the following steps:</span></span>
   
   | <span data-ttu-id="0364a-170">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="0364a-170">Attribute Name</span></span> | <span data-ttu-id="0364a-171">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="0364a-171">Attribute Value</span></span> |
   | ---| --- |
   | <span data-ttu-id="0364a-172">Nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="0364a-172">First Name</span></span> |<span data-ttu-id="0364a-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="0364a-173">user.givenname</span></span> |
   | <span data-ttu-id="0364a-174">Apellidos</span><span class="sxs-lookup"><span data-stu-id="0364a-174">Last Name</span></span> |<span data-ttu-id="0364a-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="0364a-175">user.surname</span></span> |
   | <span data-ttu-id="0364a-176">Email</span><span class="sxs-lookup"><span data-stu-id="0364a-176">Email</span></span> |<span data-ttu-id="0364a-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="0364a-177">user.mail</span></span> |
   
   <span data-ttu-id="0364a-178">a.</span><span class="sxs-lookup"><span data-stu-id="0364a-178">a.</span></span> <span data-ttu-id="0364a-179">Haga clic en **agregar atributo de usuario** para abrir el cuadro de diálogo **Agregar atributo de usuario**.</span><span class="sxs-lookup"><span data-stu-id="0364a-179">Click **add user attribute** to open the **Add User Attribure** dialog.</span></span>
    
     ![Configurar inicio de sesión único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   <span data-ttu-id="0364a-181">b.</span><span class="sxs-lookup"><span data-stu-id="0364a-181">b.</span></span> <span data-ttu-id="0364a-182">En el cuadro de texto **Nombre de atributo** , escriba el nombre de atributo que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="0364a-182">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
  
   <span data-ttu-id="0364a-183">c.</span><span class="sxs-lookup"><span data-stu-id="0364a-183">c.</span></span> <span data-ttu-id="0364a-184">En la lista **Valor de atributo** , seleccione el valor de atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="0364a-184">From the **Attribute Value** list, select the attribute value shown for that row.</span></span>
  
   <span data-ttu-id="0364a-185">d.</span><span class="sxs-lookup"><span data-stu-id="0364a-185">d.</span></span> <span data-ttu-id="0364a-186">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0364a-186">Click **Ok**.</span></span>    

7. <span data-ttu-id="0364a-187">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0364a-187">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pluralsight-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="0364a-189">Para configurar el inicio de sesión único para la aplicación, póngase en contacto con el equipo de [servicios profesionales de Pluralsight](mailTo:professionalservices@pluralsight.com) y proporcione el archivo de metadatos descargado.</span><span class="sxs-lookup"><span data-stu-id="0364a-189">To get SSO configured for your application, contact [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team and provide the downloaded metadata file.</span></span>

> [!TIP]
> <span data-ttu-id="0364a-190">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0364a-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0364a-191">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="0364a-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0364a-192">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0364a-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0364a-193">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0364a-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="0364a-194">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0364a-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0364a-196">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="0364a-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0364a-197">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0364a-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0364a-199">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0364a-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0364a-201">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0364a-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0364a-203">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="0364a-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0364a-205">a.</span><span class="sxs-lookup"><span data-stu-id="0364a-205">a.</span></span> <span data-ttu-id="0364a-206">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0364a-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0364a-207">b.</span><span class="sxs-lookup"><span data-stu-id="0364a-207">b.</span></span> <span data-ttu-id="0364a-208">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0364a-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0364a-209">c.</span><span class="sxs-lookup"><span data-stu-id="0364a-209">c.</span></span> <span data-ttu-id="0364a-210">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0364a-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0364a-211">d.</span><span class="sxs-lookup"><span data-stu-id="0364a-211">d.</span></span> <span data-ttu-id="0364a-212">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0364a-212">Click **Create**.</span></span>
 
### <a name="creating-a-pluralsight-test-user"></a><span data-ttu-id="0364a-213">Creación de un usuario de prueba de Pluralsight</span><span class="sxs-lookup"><span data-stu-id="0364a-213">Creating a Pluralsight test user</span></span>

<span data-ttu-id="0364a-214">El objetivo de esta sección es crear un usuario llamado Britta Simon en Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="0364a-214">The objective of this section is to create a user called Britta Simon in Pluralsight.</span></span> <span data-ttu-id="0364a-215">Colabore con el [equipo de soporte técnico de Pluralsight](mailto:support@pluralsight.com) para agregar los usuarios en la cuenta de Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="0364a-215">Please work with [Pluralsight Client support team](mailto:support@pluralsight.com) to add the users in the Pluralsight account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0364a-216">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0364a-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0364a-217">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="0364a-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pluralsight.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0364a-219">**Para asignar a Britta Simon a Pluralsight, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="0364a-219">**To assign Britta Simon to Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="0364a-220">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0364a-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0364a-222">En la lista de aplicaciones, seleccione **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="0364a-222">In the applications list, select **Pluralsight**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_app.png) 

3. <span data-ttu-id="0364a-224">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0364a-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0364a-226">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0364a-226">Click **Add** button.</span></span> <span data-ttu-id="0364a-227">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0364a-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0364a-229">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="0364a-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0364a-230">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0364a-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0364a-231">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0364a-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0364a-232">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="0364a-232">Testing single sign-on</span></span>

<span data-ttu-id="0364a-233">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0364a-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0364a-234">Al hacer clic en el icono de Pluralsight en el panel de acceso, debería iniciar sesión automáticamente en su aplicación de Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="0364a-234">When you click the Pluralsight tile in the Access Panel, you should get automatically signed-on to your Pluralsight application.</span></span> <span data-ttu-id="0364a-235">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0364a-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0364a-236">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0364a-236">Additional resources</span></span>

* [<span data-ttu-id="0364a-237">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0364a-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0364a-238">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0364a-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png

