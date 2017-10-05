---
title: "Tutorial: Integración de Azure Active Directory con Klue | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Klue."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 08341008-980b-4111-adb2-97bbabbf1e47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: c64417c136340b3ffa5d67c618c6fe037d2992b5
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-klue"></a><span data-ttu-id="d03f7-103">Tutorial: Integración de Azure Active Directory con Klue</span><span class="sxs-lookup"><span data-stu-id="d03f7-103">Tutorial: Azure Active Directory integration with Klue</span></span>

<span data-ttu-id="d03f7-104">En este tutorial, obtendrá información sobre cómo integrar Klue con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d03f7-104">In this tutorial, you learn how to integrate Klue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d03f7-105">La integración de Klue con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d03f7-105">Integrating Klue with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d03f7-106">Puede controlar en Azure AD quién tiene acceso a Klue</span><span class="sxs-lookup"><span data-stu-id="d03f7-106">You can control in Azure AD who has access to Klue</span></span>
- <span data-ttu-id="d03f7-107">Puede permitir que los usuarios inicien sesión automáticamente en Klue (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d03f7-107">You can enable your users to automatically get signed-on to Klue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d03f7-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d03f7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d03f7-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d03f7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d03f7-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d03f7-110">Prerequisites</span></span>

<span data-ttu-id="d03f7-111">Para configurar la integración de Azure AD con Klue, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d03f7-111">To configure Azure AD integration with Klue, you need the following items:</span></span>

- <span data-ttu-id="d03f7-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d03f7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d03f7-113">Una suscripción habilitada para el inicio de sesión único en Klue</span><span class="sxs-lookup"><span data-stu-id="d03f7-113">A Klue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d03f7-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="d03f7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d03f7-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="d03f7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d03f7-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d03f7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d03f7-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d03f7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d03f7-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="d03f7-118">Scenario description</span></span>
<span data-ttu-id="d03f7-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="d03f7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d03f7-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="d03f7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d03f7-121">Agregación de Klue desde la galería</span><span class="sxs-lookup"><span data-stu-id="d03f7-121">Adding Klue from the gallery</span></span>
2. <span data-ttu-id="d03f7-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d03f7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-klue-from-the-gallery"></a><span data-ttu-id="d03f7-123">Agregación de Klue desde la galería</span><span class="sxs-lookup"><span data-stu-id="d03f7-123">Adding Klue from the gallery</span></span>
<span data-ttu-id="d03f7-124">Para configurar la integración de Klue en Azure AD, deberá agregar Klue desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="d03f7-124">To configure the integration of Klue into Azure AD, you need to add Klue from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d03f7-125">**Para agregar Klue desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d03f7-125">**To add Klue from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d03f7-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d03f7-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d03f7-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="d03f7-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d03f7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="d03f7-133">En el cuadro de búsqueda, escriba **Klue**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-133">In the search box, type **Klue**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-klue-tutorial/tutorial_klue_search.png)

5. <span data-ttu-id="d03f7-135">En el panel de resultados, seleccione **Klue** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d03f7-135">In the results panel, select **Klue**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-klue-tutorial/tutorial_klue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d03f7-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d03f7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d03f7-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Klue con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d03f7-138">In this section, you configure and test Azure AD single sign-on with Klue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d03f7-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Klue para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d03f7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Klue is to a user in Azure AD.</span></span> <span data-ttu-id="d03f7-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Klue.</span><span class="sxs-lookup"><span data-stu-id="d03f7-140">In other words, a link relationship between an Azure AD user and the related user in Klue needs to be established.</span></span>

<span data-ttu-id="d03f7-141">Para establecer la relación de vínculo, en Klue, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-141">In Klue, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d03f7-142">Para configurar y probar el inicio de sesión único de Azure AD con Klue, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d03f7-142">To configure and test Azure AD single sign-on with Klue, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d03f7-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="d03f7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d03f7-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d03f7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d03f7-145">**[Creación de usuario de prueba de Klue](#creating-a-klue-test-user)**: para tener un homólogo de Britta Simon en Klue que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d03f7-145">**[Creating a Klue test user](#creating-a-klue-test-user)** - to have a counterpart of Britta Simon in Klue that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d03f7-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d03f7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d03f7-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="d03f7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d03f7-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d03f7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d03f7-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en su aplicación Klue.</span><span class="sxs-lookup"><span data-stu-id="d03f7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Klue application.</span></span>

<span data-ttu-id="d03f7-150">**Para configurar el inicio de sesión único de Azure AD con Klue, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d03f7-150">**To configure Azure AD single sign-on with Klue, perform the following steps:**</span></span>

1. <span data-ttu-id="d03f7-151">En Azure Portal, en la página de integración de la aplicación **Klue**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-151">In the Azure portal, on the **Klue** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="d03f7-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d03f7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/tutorial_klue_samlbase.png)

3. <span data-ttu-id="d03f7-155">Vaya a la sección **Dominio y direcciones URL de Klue**, si quiere configurar la aplicación en modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="d03f7-155">On the **Klue Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/tutorial_klue_url1.png)

    <span data-ttu-id="d03f7-157">a.</span><span class="sxs-lookup"><span data-stu-id="d03f7-157">a.</span></span> <span data-ttu-id="d03f7-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `urn:klue:<Customer ID>`</span><span class="sxs-lookup"><span data-stu-id="d03f7-158">In the **Identifier** textbox, type a URL using the following pattern: `urn:klue:<Customer ID>`</span></span>

    <span data-ttu-id="d03f7-159">b.</span><span class="sxs-lookup"><span data-stu-id="d03f7-159">b.</span></span> <span data-ttu-id="d03f7-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://app.klue.com/account/auth/saml/<Customer UUID>/callback`.</span><span class="sxs-lookup"><span data-stu-id="d03f7-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span></span>

4. <span data-ttu-id="d03f7-161">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="d03f7-162">Si quiere volver a configurar la aplicación en modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="d03f7-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/tutorial_klue_url2.png)

    <span data-ttu-id="d03f7-164">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://app.klue.com/account/auth/saml/<Customer UUID>/`.</span><span class="sxs-lookup"><span data-stu-id="d03f7-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="d03f7-165">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="d03f7-165">These values are not real.</span></span> <span data-ttu-id="d03f7-166">Actualícelos con la dirección URL de respuesta, el identificador y la dirección URL de inicio de sesión reales.</span><span class="sxs-lookup"><span data-stu-id="d03f7-166">Update these values with the actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="d03f7-167">Póngase en contacto con el [equipo de soporte técnico de Klue](mailto:support@klue.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="d03f7-167">Contact [Klue Client support team](mailto:support@klue.com) to get these values.</span></span>

5. <span data-ttu-id="d03f7-168">La aplicación Klue espera las aserciones de SAML en un formato específico, que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los atributos del token SAML.</span><span class="sxs-lookup"><span data-stu-id="d03f7-168">The Klue application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="d03f7-169">Puede administrar los valores de estos atributos en la sección "**Atributos de usuario**" de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d03f7-169">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/attribute.png)

6. <span data-ttu-id="d03f7-171">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo del token de SAML como muestra la imagen anterior y realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="d03f7-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="d03f7-172">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="d03f7-172">Attribute Name</span></span>      | <span data-ttu-id="d03f7-173">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="d03f7-173">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="d03f7-174">first_name</span><span class="sxs-lookup"><span data-stu-id="d03f7-174">first_name</span></span>          | <span data-ttu-id="d03f7-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="d03f7-175">user.givenname</span></span> |
    | <span data-ttu-id="d03f7-176">last_name</span><span class="sxs-lookup"><span data-stu-id="d03f7-176">last_name</span></span>           | <span data-ttu-id="d03f7-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="d03f7-177">user.surname</span></span> |
    | <span data-ttu-id="d03f7-178">email</span><span class="sxs-lookup"><span data-stu-id="d03f7-178">email</span></span>               | <span data-ttu-id="d03f7-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="d03f7-179">user.userprincipalname</span></span>|
    
    <span data-ttu-id="d03f7-180">a.</span><span class="sxs-lookup"><span data-stu-id="d03f7-180">a.</span></span> <span data-ttu-id="d03f7-181">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="d03f7-184">b.</span><span class="sxs-lookup"><span data-stu-id="d03f7-184">b.</span></span> <span data-ttu-id="d03f7-185">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="d03f7-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="d03f7-186">c.</span><span class="sxs-lookup"><span data-stu-id="d03f7-186">c.</span></span> <span data-ttu-id="d03f7-187">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="d03f7-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="d03f7-188">d.</span><span class="sxs-lookup"><span data-stu-id="d03f7-188">d.</span></span> <span data-ttu-id="d03f7-189">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-189">Click **Ok**.</span></span>

7. <span data-ttu-id="d03f7-190">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d03f7-190">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/tutorial_klue_certificate.png) 

8. <span data-ttu-id="d03f7-192">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="d03f7-192">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/tutorial_general_400.png)
    
9. <span data-ttu-id="d03f7-194">En la sección **Configuración de Klue**, haga clic en **Configurar Klue** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-194">On the **Klue Configuration** section, click **Configure Klue** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d03f7-195">Copie **SAML Entity ID and SAML Single Sign-On Service URL** (URL del servicio de inicio de sesión único de SAML e Identificador de entidad de SAML) de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-195">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/tutorial_klue_configure.png) 

10. <span data-ttu-id="d03f7-197">Para configurar el inicio de sesión único en **Klue**, debe enviar el **certificado (Base64) descargado, la dirección URL del servicio de inicio de sesión único de SAML y el identificador de entidad de SAML** al [equipo de soporte técnico de Klue](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="d03f7-197">To configure single sign-on on **Klue** side, you need to send the downloaded **Certificate(Base64), SAML Single Sign-On Service URL, and SAML Entity ID** to [Klue support team](mailto:support@klue.com).</span></span>

> [!TIP]
> <span data-ttu-id="d03f7-198">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d03f7-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d03f7-199">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="d03f7-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d03f7-200">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d03f7-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d03f7-201">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d03f7-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="d03f7-202">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d03f7-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="d03f7-204">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="d03f7-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d03f7-205">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d03f7-207">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d03f7-209">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d03f7-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d03f7-211">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="d03f7-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d03f7-213">a.</span><span class="sxs-lookup"><span data-stu-id="d03f7-213">a.</span></span> <span data-ttu-id="d03f7-214">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d03f7-215">b.</span><span class="sxs-lookup"><span data-stu-id="d03f7-215">b.</span></span> <span data-ttu-id="d03f7-216">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d03f7-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d03f7-217">c.</span><span class="sxs-lookup"><span data-stu-id="d03f7-217">c.</span></span> <span data-ttu-id="d03f7-218">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d03f7-219">d.</span><span class="sxs-lookup"><span data-stu-id="d03f7-219">d.</span></span> <span data-ttu-id="d03f7-220">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-220">Click **Create**.</span></span>
 
### <a name="creating-a-klue-test-user"></a><span data-ttu-id="d03f7-221">Creación de usuario de prueba de Klue</span><span class="sxs-lookup"><span data-stu-id="d03f7-221">Creating a Klue test user</span></span>

<span data-ttu-id="d03f7-222">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en Klue.</span><span class="sxs-lookup"><span data-stu-id="d03f7-222">The objective of this section is to create a user called Britta Simon in Klue.</span></span> <span data-ttu-id="d03f7-223">Klue admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d03f7-223">Klue supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="d03f7-224">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="d03f7-224">There is no action item for you in this section.</span></span> <span data-ttu-id="d03f7-225">Al intentar acceder a Klue, se crea un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="d03f7-225">A new user is created during an attempt to access Klue if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="d03f7-226">Si necesita crear manualmente un usuario, póngase en contacto con el [equipo de soporte técnico de Klue](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="d03f7-226">If you need to create a user manually, Contact [Klue support team](mailto:support@klue.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d03f7-227">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d03f7-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d03f7-228">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Klue.</span><span class="sxs-lookup"><span data-stu-id="d03f7-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Klue.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="d03f7-230">**Para asignar a Britta Simon a Klue, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="d03f7-230">**To assign Britta Simon to Klue, perform the following steps:**</span></span>

1. <span data-ttu-id="d03f7-231">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="d03f7-233">En la lista de aplicaciones, seleccione **Klue**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-233">In the applications list, select **Klue**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-klue-tutorial/tutorial_klue_app.png) 

3. <span data-ttu-id="d03f7-235">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="d03f7-237">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-237">Click **Add** button.</span></span> <span data-ttu-id="d03f7-238">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="d03f7-240">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="d03f7-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d03f7-241">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d03f7-242">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d03f7-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d03f7-243">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="d03f7-243">Testing single sign-on</span></span>

<span data-ttu-id="d03f7-244">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d03f7-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d03f7-245">Al hacer clic en el icono de Klue en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Klue.</span><span class="sxs-lookup"><span data-stu-id="d03f7-245">When you click the Klue tile in the Access Panel, you should get automatically signed-on to your Klue application.</span></span>
<span data-ttu-id="d03f7-246">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d03f7-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d03f7-247">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d03f7-247">Additional resources</span></span>

* [<span data-ttu-id="d03f7-248">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d03f7-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d03f7-249">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d03f7-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-klue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-klue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-klue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-klue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-klue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-klue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-klue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-klue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-klue-tutorial/tutorial_general_203.png

