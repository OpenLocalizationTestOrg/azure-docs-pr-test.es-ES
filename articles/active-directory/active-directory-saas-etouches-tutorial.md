---
title: "Tutorial: Integración de Azure Active Directory con etouches | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y etouches."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 3cd9e9d6aae924369065ca492b1f6380c0ddc5fe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a><span data-ttu-id="e3200-103">Tutorial: Integración de Azure Active Directory con etouches</span><span class="sxs-lookup"><span data-stu-id="e3200-103">Tutorial: Azure Active Directory integration with etouches</span></span>

<span data-ttu-id="e3200-104">En este tutorial, obtendrá información sobre cómo integrar etouches con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e3200-104">In this tutorial, you learn how to integrate etouches with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e3200-105">La integración de etouches con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e3200-105">Integrating etouches with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e3200-106">Puede controlar en Azure AD quién tiene acceso a etouches.</span><span class="sxs-lookup"><span data-stu-id="e3200-106">You can control in Azure AD who has access to etouches</span></span>
- <span data-ttu-id="e3200-107">Puede permitir que los usuarios inicien sesión automáticamente en etouches (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3200-107">You can enable your users to automatically get signed-on to etouches (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e3200-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e3200-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e3200-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e3200-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3200-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e3200-110">Prerequisites</span></span>

<span data-ttu-id="e3200-111">Para configurar la integración de Azure AD con etouches, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e3200-111">To configure Azure AD integration with etouches, you need the following items:</span></span>

- <span data-ttu-id="e3200-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3200-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e3200-113">Una suscripción habilitada para el inicio de sesión único en etouches</span><span class="sxs-lookup"><span data-stu-id="e3200-113">An etouches single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e3200-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e3200-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e3200-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e3200-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e3200-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e3200-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e3200-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e3200-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e3200-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e3200-118">Scenario description</span></span>
<span data-ttu-id="e3200-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e3200-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e3200-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="e3200-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e3200-121">Incorporación de etouches desde la galería</span><span class="sxs-lookup"><span data-stu-id="e3200-121">Adding etouches from the gallery</span></span>
2. <span data-ttu-id="e3200-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3200-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-etouches-from-the-gallery"></a><span data-ttu-id="e3200-123">Incorporación de etouches desde la galería</span><span class="sxs-lookup"><span data-stu-id="e3200-123">Adding etouches from the gallery</span></span>
<span data-ttu-id="e3200-124">Para configurar la integración de etouches en Azure AD, deberá agregar etouches desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="e3200-124">To configure the integration of etouches into Azure AD, you need to add etouches from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e3200-125">**Para agregar etouches desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e3200-125">**To add etouches from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e3200-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e3200-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="e3200-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e3200-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e3200-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e3200-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="e3200-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e3200-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="e3200-133">En el cuadro de búsqueda, escriba **etouches**, seleccione **etouches** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e3200-133">In the search box, type **etouches**, select **etouches** from result panel then click **Add** button to add the application.</span></span>

    ![etouches en la lista de resultados](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e3200-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3200-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="e3200-136">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con etouches con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e3200-136">In this section, you configure and test Azure AD single sign-on with etouches based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e3200-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de etouches para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3200-137">For single sign-on to work, Azure AD needs to know what the counterpart user in etouches is to a user in Azure AD.</span></span> <span data-ttu-id="e3200-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de etouches.</span><span class="sxs-lookup"><span data-stu-id="e3200-138">In other words, a link relationship between an Azure AD user and the related user in etouches needs to be established.</span></span>

<span data-ttu-id="e3200-139">Para establecer la relación de vínculo, en etouches, asigne el valor del **nombre de usuario** de Azure AD como el valor del **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="e3200-139">In etouches, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e3200-140">Para configurar y probar el inicio de sesión único de Azure AD con etouches, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e3200-140">To configure and test Azure AD single sign-on with etouches, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e3200-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="e3200-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e3200-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e3200-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e3200-143">**[Creación de un usuario de prueba de etouches](#create-an-etouches-test-user)**: para tener un homólogo de Britta Simon en etouches que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3200-143">**[Create an etouches test user](#create-an-etouches-test-user)** - to have a counterpart of Britta Simon in etouches that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e3200-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3200-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e3200-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e3200-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e3200-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3200-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e3200-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación etouches.</span><span class="sxs-lookup"><span data-stu-id="e3200-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your etouches application.</span></span>

<span data-ttu-id="e3200-148">**Para configurar el inicio de sesión único de Azure AD con etouches, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e3200-148">**To configure Azure AD single sign-on with etouches, perform the following steps:**</span></span>

1. <span data-ttu-id="e3200-149">En Azure Portal, en la página de integración de la aplicación **etouches**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e3200-149">In the Azure portal, on the **etouches** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e3200-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e3200-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. <span data-ttu-id="e3200-153">En la sección **Dominio y direcciones URL de etouches**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e3200-153">On the **etouches Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    <span data-ttu-id="e3200-155">a.</span><span class="sxs-lookup"><span data-stu-id="e3200-155">a.</span></span> <span data-ttu-id="e3200-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`.</span><span class="sxs-lookup"><span data-stu-id="e3200-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span></span>

    <span data-ttu-id="e3200-157">b.</span><span class="sxs-lookup"><span data-stu-id="e3200-157">b.</span></span> <span data-ttu-id="e3200-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://www.eiseverywhere.com/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="e3200-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.eiseverywhere.com/<instance name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e3200-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="e3200-159">These values are not real.</span></span> <span data-ttu-id="e3200-160">El valor se actualizará con la dirección URL de inicio de sesión y el identificador reales, que se explican más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="e3200-160">You update the value with the actual Sign on URL and Identifier, which is explained later in the tutorial.</span></span>
    > 

4. <span data-ttu-id="e3200-161">La aplicación etouches espera las aserciones de SAML en un formato específico.</span><span class="sxs-lookup"><span data-stu-id="e3200-161">etouches application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="e3200-162">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="e3200-162">Configure the following claims for this application.</span></span> <span data-ttu-id="e3200-163">Puede administrar el valor de estos atributos desde la pestaña **Atributos de usuario** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e3200-163">You can manage the values of these attributes from the **User Attribute** of the application.</span></span> <span data-ttu-id="e3200-164">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="e3200-164">The following screenshot shows an example for this.</span></span> 

    ![Atributo de usuario](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. <span data-ttu-id="e3200-166">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo token de SAML como muestra la imagen y siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e3200-166">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="e3200-167">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="e3200-167">Attribute Name</span></span> | <span data-ttu-id="e3200-168">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="e3200-168">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="e3200-169">Email</span><span class="sxs-lookup"><span data-stu-id="e3200-169">Email</span></span> | <span data-ttu-id="e3200-170">user.mail</span><span class="sxs-lookup"><span data-stu-id="e3200-170">user.mail</span></span> |    
    
    <span data-ttu-id="e3200-171">a.</span><span class="sxs-lookup"><span data-stu-id="e3200-171">a.</span></span> <span data-ttu-id="e3200-172">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="e3200-172">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Agregar atributo](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![Cuadro de diálogo Agregar atributo](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="e3200-175">b.</span><span class="sxs-lookup"><span data-stu-id="e3200-175">b.</span></span> <span data-ttu-id="e3200-176">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="e3200-176">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="e3200-177">c.</span><span class="sxs-lookup"><span data-stu-id="e3200-177">c.</span></span> <span data-ttu-id="e3200-178">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="e3200-178">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="e3200-179">d.</span><span class="sxs-lookup"><span data-stu-id="e3200-179">d.</span></span> <span data-ttu-id="e3200-180">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e3200-180">Click **Ok**.</span></span> 

6. <span data-ttu-id="e3200-181">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e3200-181">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. <span data-ttu-id="e3200-183">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e3200-183">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e3200-185">Para que SSO se configure para su aplicación, siga estos pasos en la aplicación etouches:</span><span class="sxs-lookup"><span data-stu-id="e3200-185">To get SSO configured for your application, perform the following steps in the etouches application:</span></span> 

    ![Configuración de etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    <span data-ttu-id="e3200-187">a.</span><span class="sxs-lookup"><span data-stu-id="e3200-187">a.</span></span> <span data-ttu-id="e3200-188">Inicie sesión en la aplicación **etouches** con derechos de administrador.</span><span class="sxs-lookup"><span data-stu-id="e3200-188">Login to **etouches** application using the Admin rights.</span></span>
   
    <span data-ttu-id="e3200-189">b.</span><span class="sxs-lookup"><span data-stu-id="e3200-189">b.</span></span> <span data-ttu-id="e3200-190">Vaya a la configuración de **SAML**.</span><span class="sxs-lookup"><span data-stu-id="e3200-190">Go to the **SAML** Configuration.</span></span>

    <span data-ttu-id="e3200-191">c.</span><span class="sxs-lookup"><span data-stu-id="e3200-191">c.</span></span> <span data-ttu-id="e3200-192">En la sección **Configuración general**, abra el certificado descargado de Azure Portal en el Bloc de notas, copie el contenido y, luego, péguelo en el cuadro de texto de metadatos de IDP.</span><span class="sxs-lookup"><span data-stu-id="e3200-192">In the **General Settings** section, open your downloaded certificate from Azure portal in notepad, copy the content, and then paste it into the IDP metadata textbox.</span></span> 

    <span data-ttu-id="e3200-193">d.</span><span class="sxs-lookup"><span data-stu-id="e3200-193">d.</span></span> <span data-ttu-id="e3200-194">Haga clic en el botón **Save & Stay** (Guardar y permanecer).</span><span class="sxs-lookup"><span data-stu-id="e3200-194">Click on the **Save & Stay** button.</span></span>
  
    <span data-ttu-id="e3200-195">e.</span><span class="sxs-lookup"><span data-stu-id="e3200-195">e.</span></span> <span data-ttu-id="e3200-196">Haga clic en el botón **Update Metadata** (Actualizar metadatos) en la sección SAML Metadata (Metadatos de SAML).</span><span class="sxs-lookup"><span data-stu-id="e3200-196">Click on the **Update Metadata** button in the SAML Metadata section.</span></span> 

    <span data-ttu-id="e3200-197">f.</span><span class="sxs-lookup"><span data-stu-id="e3200-197">f.</span></span> <span data-ttu-id="e3200-198">Esta acción abre la página y se realiza el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e3200-198">This opens the page and perform SSO.</span></span> <span data-ttu-id="e3200-199">Cuando el inicio de sesión único esté funcionando, puede configurar el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="e3200-199">Once the SSO is working then you can set up the username.</span></span>

    <span data-ttu-id="e3200-200">g.</span><span class="sxs-lookup"><span data-stu-id="e3200-200">g.</span></span> <span data-ttu-id="e3200-201">En el campo Username (Nombre de usuario) seleccione **emailaddress**, como se muestra en la siguiente imagen.</span><span class="sxs-lookup"><span data-stu-id="e3200-201">In the Username field, select the **emailaddress** as shown in the image below.</span></span> 

    <span data-ttu-id="e3200-202">h.</span><span class="sxs-lookup"><span data-stu-id="e3200-202">h.</span></span> <span data-ttu-id="e3200-203">Copie el valor de **SP entity ID** (Identificador de entidad del proveedor de servicios) y péguelo en el cuadro de texto **Identifier** (Identificador), que se encuentra en la sección **Dominio y direcciones URL de etouches** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e3200-203">Copy the **SP entity ID** value and paste it into the **Identifier**  textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="e3200-204">i.</span><span class="sxs-lookup"><span data-stu-id="e3200-204">i.</span></span> <span data-ttu-id="e3200-205">Copie el valor de **SSO URL / ACS** (URL de SSO/ACS) y péguelo en el cuadro de texto **Sign on URL** (Dirección URL de inicio de sesión), que se encuentra en la sección **Dominio y direcciones URL de etouches** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e3200-205">Copy the **SSO URL / ACS** value and paste it into the **Sign on URL** textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>
   
> [!TIP]
> <span data-ttu-id="e3200-206">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e3200-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e3200-207">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e3200-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e3200-208">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e3200-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e3200-209">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3200-209">Create an Azure AD test user</span></span>
<span data-ttu-id="e3200-210">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e3200-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="e3200-212">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="e3200-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e3200-213">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e3200-213">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e3200-215">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e3200-215">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e3200-217">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e3200-217">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Botón Agregar](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e3200-219">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="e3200-219">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Cuadro de diálogo Usuario](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e3200-221">a.</span><span class="sxs-lookup"><span data-stu-id="e3200-221">a.</span></span> <span data-ttu-id="e3200-222">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e3200-222">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e3200-223">b.</span><span class="sxs-lookup"><span data-stu-id="e3200-223">b.</span></span> <span data-ttu-id="e3200-224">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e3200-224">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e3200-225">c.</span><span class="sxs-lookup"><span data-stu-id="e3200-225">c.</span></span> <span data-ttu-id="e3200-226">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e3200-226">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e3200-227">d.</span><span class="sxs-lookup"><span data-stu-id="e3200-227">d.</span></span> <span data-ttu-id="e3200-228">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e3200-228">Click **Create**.</span></span>
 
### <a name="create-an-etouches-test-user"></a><span data-ttu-id="e3200-229">Creación de un usuario de prueba de etouches</span><span class="sxs-lookup"><span data-stu-id="e3200-229">Create an etouches test user</span></span>

<span data-ttu-id="e3200-230">En esta sección, se crea un usuario denominado Britta Simon en etouches.</span><span class="sxs-lookup"><span data-stu-id="e3200-230">In this section, you create a user called Britta Simon in etouches.</span></span> <span data-ttu-id="e3200-231">Trabaje con el [equipo de soporte técnico de etouches](https://www.etouches.com/event-software/support/customer-support/) para agregar los usuarios a la plataforma de etouches.</span><span class="sxs-lookup"><span data-stu-id="e3200-231">Work with [etouches Client support team](https://www.etouches.com/event-software/support/customer-support/) to add the users in the etouches platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e3200-232">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3200-232">Assign the Azure AD test user</span></span>

<span data-ttu-id="e3200-233">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a etouches.</span><span class="sxs-lookup"><span data-stu-id="e3200-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to etouches.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="e3200-235">**Para asignar Britta Simon a etouches, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e3200-235">**To assign Britta Simon to etouches, perform the following steps:**</span></span>

1. <span data-ttu-id="e3200-236">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e3200-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e3200-238">En la lista de aplicaciones, seleccione **etouches**.</span><span class="sxs-lookup"><span data-stu-id="e3200-238">In the applications list, select **etouches**.</span></span>

    ![Vínculo a etouches en la lista de aplicaciones](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. <span data-ttu-id="e3200-240">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e3200-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202] 

4. <span data-ttu-id="e3200-242">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e3200-242">Click **Add** button.</span></span> <span data-ttu-id="e3200-243">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e3200-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="e3200-245">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="e3200-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e3200-246">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e3200-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e3200-247">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e3200-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e3200-248">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="e3200-248">Test single sign-on</span></span>


<span data-ttu-id="e3200-249">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e3200-249">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e3200-250">Al hacer clic en el icono de etouches en el panel de acceso, debe iniciar sesión automáticamente en su aplicación etouches.</span><span class="sxs-lookup"><span data-stu-id="e3200-250">When you click the etouches tile in the Access Panel, you should get automatically signed-on to your etouches application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e3200-251">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e3200-251">Additional resources</span></span>

* [<span data-ttu-id="e3200-252">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e3200-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e3200-253">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e3200-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

