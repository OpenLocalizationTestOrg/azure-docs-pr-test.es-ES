---
title: "Tutorial: Integración de Azure Active Directory con Symantec Web Security Service (WSS) | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Symantec Web Security Service (WSS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 61576d3a915d209e7355e04432e586dcf66e7c5a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="11c90-103">Tutorial: Integración de Azure Active Directory con Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="11c90-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="11c90-104">En este tutorial aprenderá cómo integrar su cuenta de Symantec Web Security Service (WSS) con su cuenta de Azure Active Directory (Azure AD) para que WSS pueda autenticar un usuario final que se aprovisiona en Azure AD mediante la autenticación de SAML y aplicar reglas de directiva de nivel de usuario o grupo.</span><span class="sxs-lookup"><span data-stu-id="11c90-104">In this tutorial, you will learn how to integrate your Symantec Web Security Service (WSS) account with your Azure Active Directory (Azure AD) account so that WSS can authenticate an end user provisioned in the Azure AD using SAML authentication and enforce user or group level policy rules.</span></span>

<span data-ttu-id="11c90-105">La integración de Symantec Web Security Service (WSS) con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="11c90-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="11c90-106">Administrar todos los usuarios finales y los grupos que usan la cuenta de WSS desde el portal de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11c90-106">Manage all of the end users and groups used by your WSS account from your Azure AD portal.</span></span> 

- <span data-ttu-id="11c90-107">Permitir que los usuarios finales se autentiquen en WSS con sus credenciales de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11c90-107">Allow the end users to authenticate themselves in WSS using their Azure AD credentials.</span></span>

- <span data-ttu-id="11c90-108">Habilitar la aplicación de reglas de directiva de nivel de grupo y usuario definidas en la cuenta de WSS.</span><span class="sxs-lookup"><span data-stu-id="11c90-108">Enable the enforcement of user and group level policy rules defined in your WSS account.</span></span>

<span data-ttu-id="11c90-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="11c90-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11c90-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="11c90-110">Prerequisites</span></span>

<span data-ttu-id="11c90-111">Para configurar la integración de Azure AD con Symantec Web Security Service (WSS), necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="11c90-111">To configure Azure AD integration with Symantec Web Security Service (WSS), you need the following items:</span></span>

- <span data-ttu-id="11c90-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="11c90-112">An Azure AD subscription</span></span>
- <span data-ttu-id="11c90-113">Una cuenta de Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="11c90-113">A Symantec Web Security Service (WSS) account</span></span>

> [!NOTE]
> <span data-ttu-id="11c90-114">Para probar los pasos de este tutorial, se recomienda no utilizar una cuenta de WSS que se esté usando actualmente en producción.</span><span class="sxs-lookup"><span data-stu-id="11c90-114">To test the steps in this tutorial, we do not recommend using a WSS account that is currently being used for production purpose.</span></span>

<span data-ttu-id="11c90-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="11c90-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="11c90-116">No use una cuenta de WSS que se esté usando actualmente en producción para esta prueba a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="11c90-116">Do not use your WSS account that is currently being used for production purpose for this test unless it is necessary.</span></span>
- <span data-ttu-id="11c90-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="11c90-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="11c90-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="11c90-118">Scenario description</span></span>
<span data-ttu-id="11c90-119">En este tutorial, va a configurar Azure AD para habilitar el inicio de sesión único con WSS utilizando las credenciales de usuario final definidas en la cuenta de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11c90-119">In this tutorial, you will configure your Azure AD to enable single sign-on to WSS using the end user credentials defined in your Azure AD account.</span></span>
<span data-ttu-id="11c90-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="11c90-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="11c90-121">Agregación de Symantec Web Security Service (WSS) desde la galería</span><span class="sxs-lookup"><span data-stu-id="11c90-121">Adding the Symantec Web Security Service (WSS) app from the gallery</span></span>
2. <span data-ttu-id="11c90-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="11c90-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-the-gallery"></a><span data-ttu-id="11c90-123">Agregación de Symantec Web Security Service (WSS) desde la galería</span><span class="sxs-lookup"><span data-stu-id="11c90-123">Adding Symantec Web Security Service (WSS) from the gallery</span></span>
<span data-ttu-id="11c90-124">Para configurar la integración de Symantec Web Security Service (WSS) en Azure AD, es preciso agregar Symantec Web Security Service (WSS) desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="11c90-124">To configure the integration of Symantec Web Security Service (WSS) into Azure AD, you need to add Symantec Web Security Service (WSS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="11c90-125">**Para agregar Symantec Web Security Service (WSS) desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="11c90-125">**To add Symantec Web Security Service (WSS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="11c90-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="11c90-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="11c90-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="11c90-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="11c90-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="11c90-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="11c90-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="11c90-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="11c90-133">En el cuadro de búsqueda, escriba **Symantec Web Security Service (WSS)**, seleccione **Symantec Web Security Service (WSS)** en el panel de resultados y, a continuación, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="11c90-133">In the search box, type **Symantec Web Security Service (WSS)**, select **Symantec Web Security Service (WSS)** from result panel then click **Add** button to add the application.</span></span>

    ![Symantec Web Security Service (WSS) en la lista de resultados](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="11c90-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="11c90-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="11c90-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Symantec Web Security Service (WSS) con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="11c90-136">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="11c90-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Symantec Web Security Service (WSS) para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11c90-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Symantec Web Security Service (WSS) is to a user in Azure AD.</span></span> <span data-ttu-id="11c90-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="11c90-138">In other words, a link relationship between an Azure AD user and the related user in Symantec Web Security Service (WSS) needs to be established.</span></span>

<span data-ttu-id="11c90-139">Para establecer la relación de vínculo, en Symantec Web Security Service (WSS), asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="11c90-139">In Symantec Web Security Service (WSS), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="11c90-140">Para configurar y probar el inicio de sesión único de Azure AD con Symantec Web Security Service (WSS), es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="11c90-140">To configure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="11c90-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="11c90-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="11c90-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11c90-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="11c90-143">**[Creación de un usuario de prueba de Symantec Web Security Service (WSS)](#create-a-symantec-web-security-service-wss-test-user)**: para tener un homólogo de Britta Simon en Symantec Web Security Service (WSS) que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11c90-143">**[Create a Symantec Web Security Service (WSS) test user](#create-a-symantec-web-security-service-wss-test-user)** - to have a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="11c90-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11c90-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="11c90-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="11c90-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="11c90-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="11c90-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="11c90-147">En esta sección habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="11c90-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="11c90-148">**Para configurar el inicio de sesión único de Azure AD con Symantec Web Security Service (WSS), siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="11c90-148">**To configure Azure AD single sign-on with Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="11c90-149">En Azure Portal, en la página de integración de la aplicación **Symantec Web Security Service (WSS)**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="11c90-149">In the Azure portal, on the **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="11c90-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="11c90-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="11c90-153">En la sección **Dominio y direcciones URL de Symantec Web Security Service (WSS)**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="11c90-153">On the **Symantec Web Security Service (WSS) Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Symantec Web Security Service (WSS)](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="11c90-155">a.</span><span class="sxs-lookup"><span data-stu-id="11c90-155">a.</span></span> <span data-ttu-id="11c90-156">En el cuadro de texto **Identificador**, escriba la dirección URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="11c90-156">In the **Identifier** textbox, type the URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    <span data-ttu-id="11c90-157">b.</span><span class="sxs-lookup"><span data-stu-id="11c90-157">b.</span></span> <span data-ttu-id="11c90-158">En el cuadro de texto **URL de respuesta**, escriba la siguiente dirección URL: `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span><span class="sxs-lookup"><span data-stu-id="11c90-158">In the **Reply URL** textbox, type the URL: `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span></span>

    > [!NOTE]
    > <span data-ttu-id="11c90-159">Póngase en contacto con el [equipo de soporte técnico de Symantec Web Security Service (WSS)](https://www.symantec.com/contact-us) si los valores para el **identificador** y **dirección URL de respuesta** no funcionasen por algún motivo.</span><span class="sxs-lookup"><span data-stu-id="11c90-159">Please contact the [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) if the values for the **Identifier** and **Reply URL** are not working for some reason.</span></span>

4. <span data-ttu-id="11c90-160">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="11c90-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="11c90-162">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="11c90-162">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="11c90-164">Para configurar el inicio de sesión único en Symantec Web Security Service (WSS), consulte la documentación en línea de WSS.</span><span class="sxs-lookup"><span data-stu-id="11c90-164">To configure single sign-on on the Symantec Web Security Service (WSS) side, refer to the WSS online documentation.</span></span> <span data-ttu-id="11c90-165">El archivo **XML de metadatos** descargado debe ser importado en el portal de WSS.</span><span class="sxs-lookup"><span data-stu-id="11c90-165">The downloaded **Metadata XML** file will need to be imported into the WSS portal.</span></span> <span data-ttu-id="11c90-166">Póngase en contacto con el [equipo de soporte técnico de Symantec Web Security Service (WSS)](https://www.symantec.com/contact-us) si necesita ayuda con la configuración en el portal de WSS.</span><span class="sxs-lookup"><span data-stu-id="11c90-166">Contact the [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) if you need assistance with the configuration on the WSS portal.</span></span>

> [!TIP]
> <span data-ttu-id="11c90-167">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="11c90-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="11c90-168">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="11c90-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="11c90-169">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="11c90-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="11c90-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="11c90-170">Create an Azure AD test user</span></span>

<span data-ttu-id="11c90-171">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="11c90-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="11c90-173">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="11c90-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="11c90-174">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="11c90-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="11c90-176">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="11c90-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="11c90-178">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="11c90-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="11c90-180">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="11c90-180">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    <span data-ttu-id="11c90-182">a.</span><span class="sxs-lookup"><span data-stu-id="11c90-182">a.</span></span> <span data-ttu-id="11c90-183">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="11c90-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="11c90-184">b.</span><span class="sxs-lookup"><span data-stu-id="11c90-184">b.</span></span> <span data-ttu-id="11c90-185">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11c90-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="11c90-186">c.</span><span class="sxs-lookup"><span data-stu-id="11c90-186">c.</span></span> <span data-ttu-id="11c90-187">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="11c90-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="11c90-188">d.</span><span class="sxs-lookup"><span data-stu-id="11c90-188">d.</span></span> <span data-ttu-id="11c90-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="11c90-189">Click **Create**.</span></span>
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="11c90-190">Creación de un usuario de prueba de Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="11c90-190">Create a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="11c90-191">En esta sección, creará un usuario llamado Britta Simon en Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="11c90-191">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="11c90-192">El nombre de usuario final correspondiente se puede crear manualmente en el portal de WSS o puede esperar a que los usuarios y grupos que se han aprovisionado en Azure AD se sincronicen con el portal de WSS transcurridos unos minutos (unos 15 minutos).</span><span class="sxs-lookup"><span data-stu-id="11c90-192">The corresponding end username can be manually created in the WSS portal or you can wait for the users/groups provisioned in the Azure AD to be synchronized to the WSS portal after a few minutes (~15 minutes).</span></span> <span data-ttu-id="11c90-193">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="11c90-193">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="11c90-194">La dirección IP pública del equipo del usuario final, que se utilizará para examinar sitios web, también debe aprovisionarse en el portal de Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="11c90-194">The public IP address of the end user machine, which will be used to browse websites also need to be provisioned in the Symantec Web Security Service (WSS) portal.</span></span>

> [!NOTE]
> <span data-ttu-id="11c90-195">[Haga clic aquí](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) para obtener la dirección IP pública del equipo.</span><span class="sxs-lookup"><span data-stu-id="11c90-195">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) to get your machine's public IPaddress.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="11c90-196">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="11c90-196">Assign the Azure AD test user</span></span>

<span data-ttu-id="11c90-197">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="11c90-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Symantec Web Security Service (WSS).</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="11c90-199">**Para asignar a Britta Simon a Symantec Web Security Service (WSS), siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="11c90-199">**To assign Britta Simon to Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="11c90-200">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="11c90-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="11c90-202">En la lista de aplicaciones, seleccione **Symantec Web Security Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="11c90-202">In the applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![Vínculo a Symantec Web Security Service (WSS) en la lista de aplicaciones](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. <span data-ttu-id="11c90-204">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="11c90-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="11c90-206">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="11c90-206">Click **Add** button.</span></span> <span data-ttu-id="11c90-207">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="11c90-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="11c90-209">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="11c90-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="11c90-210">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="11c90-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="11c90-211">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="11c90-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="11c90-212">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="11c90-212">Test single sign-on</span></span>

<span data-ttu-id="11c90-213">Ahora que ha configurado su cuenta de WSS para usar Azure AD para la autenticación de SAML, en esta sección, probará la funcionalidad de inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="11c90-213">In this section, you'll test the single sign-on functionality now that you've configured your WSS account to use your Azure AD for SAML authentication.</span></span>

<span data-ttu-id="11c90-214">Después de haber configurado el explorador web para canalizar el tráfico hacia WSS, cuando se abra el explorador web y se intente ir a un sitio, se le redirigirá a la página de inicio de sesión de Azure.</span><span class="sxs-lookup"><span data-stu-id="11c90-214">After you have configured your web browser to proxy traffic to WSS, when you open your web browser and try to browse to a site then you'll be redirected to the Azure sign-on page.</span></span> <span data-ttu-id="11c90-215">Escriba las credenciales del usuario final de prueba que se ha aprovisionado en Azure AD (es decir, BrittaSimon) y la contraseña asociada.</span><span class="sxs-lookup"><span data-stu-id="11c90-215">Enter the credentials of the test end user that has been provisioned in the Azure AD (that is, BrittaSimon) and associated password.</span></span> <span data-ttu-id="11c90-216">Una vez autenticado, podrá visitar el sitio web que eligió.</span><span class="sxs-lookup"><span data-stu-id="11c90-216">Once authenticated, you'll be able to browse to the website that you chose.</span></span> <span data-ttu-id="11c90-217">Debe crear una regla de directiva en WSS para bloquear la exploración de un sitio determinado a BrittaSimon y, a continuación, debería ver la página de bloqueo de WSS al intentar ir a ese sitio como el usuario BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="11c90-217">Should you create a policy rule on the WSS side to block BrittaSimon from browsing to a particular site then you should see the WSS block page when you attempt to browse to that site as user BrittaSimon.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="11c90-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="11c90-218">Additional resources</span></span>

* [<span data-ttu-id="11c90-219">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="11c90-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="11c90-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="11c90-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

