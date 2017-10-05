---
title: "Tutorial: Integración de Azure Active Directory con SD Elements | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y SD Elements."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 624eff0a0da8f548877e4a4346b21df89cd37b67
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a><span data-ttu-id="1dac6-103">Tutorial: Integración de Azure Active Directory con SD Elements</span><span class="sxs-lookup"><span data-stu-id="1dac6-103">Tutorial: Azure Active Directory integration with SD Elements</span></span>

<span data-ttu-id="1dac6-104">En este tutorial, aprenderá cómo integrar SD Elements con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1dac6-104">In this tutorial, you learn how to integrate SD Elements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1dac6-105">La integración de SD Elements con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="1dac6-105">Integrating SD Elements with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1dac6-106">Puede controlar en Azure AD quién tiene acceso a SD Elements.</span><span class="sxs-lookup"><span data-stu-id="1dac6-106">You can control in Azure AD who has access to SD Elements</span></span>
- <span data-ttu-id="1dac6-107">Puede permitir que los usuarios inicien sesión automáticamente en SD Elements (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1dac6-107">You can enable your users to automatically get signed-on to SD Elements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1dac6-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1dac6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1dac6-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1dac6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1dac6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1dac6-110">Prerequisites</span></span>

<span data-ttu-id="1dac6-111">Para configurar la integración de Azure AD con SD Elements, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1dac6-111">To configure Azure AD integration with SD Elements, you need the following items:</span></span>

- <span data-ttu-id="1dac6-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dac6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1dac6-113">Una suscripción habilitada para el inicio de sesión único en SD Elements</span><span class="sxs-lookup"><span data-stu-id="1dac6-113">A SD Elements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1dac6-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="1dac6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1dac6-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="1dac6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1dac6-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1dac6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1dac6-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1dac6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1dac6-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="1dac6-118">Scenario description</span></span>
<span data-ttu-id="1dac6-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="1dac6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1dac6-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="1dac6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1dac6-121">Incorporación de SD Elements desde la galería</span><span class="sxs-lookup"><span data-stu-id="1dac6-121">Adding SD Elements from the gallery</span></span>
2. <span data-ttu-id="1dac6-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dac6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sd-elements-from-the-gallery"></a><span data-ttu-id="1dac6-123">Incorporación de SD Elements desde la galería</span><span class="sxs-lookup"><span data-stu-id="1dac6-123">Adding SD Elements from the gallery</span></span>
<span data-ttu-id="1dac6-124">Para configurar la integración de SD Elements en Azure AD, deberá agregar SD Elements desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="1dac6-124">To configure the integration of SD Elements into Azure AD, you need to add SD Elements from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1dac6-125">**Para agregar SD Elements desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="1dac6-125">**To add SD Elements from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1dac6-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1dac6-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1dac6-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="1dac6-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1dac6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="1dac6-133">En el cuadro Buscar, escriba **SD Elements**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-133">In the search box, type **SD Elements**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. <span data-ttu-id="1dac6-135">En el panel de resultados, seleccione **SD Elements**  y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1dac6-135">In the results panel, select **SD Elements**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1dac6-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dac6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1dac6-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SD Elements con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1dac6-138">In this section, you configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1dac6-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de SD Elements para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1dac6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SD Elements is to a user in Azure AD.</span></span> <span data-ttu-id="1dac6-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de SD Elements.</span><span class="sxs-lookup"><span data-stu-id="1dac6-140">In other words, a link relationship between an Azure AD user and the related user in SD Elements needs to be established.</span></span>

<span data-ttu-id="1dac6-141">Para establecer la relación de vínculo, en SD Elements, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-141">In SD Elements, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1dac6-142">Para configurar y probar el inicio de sesión único de Azure AD con SD Elements, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="1dac6-142">To configure and test Azure AD single sign-on with SD Elements, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1dac6-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="1dac6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1dac6-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1dac6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1dac6-145">**[Creación de un usuario de prueba de SD Elements](#creating-a-sd-elements-test-user)**: para tener un homólogo de Britta Simon en SD Elements que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1dac6-145">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - to have a counterpart of Britta Simon in SD Elements that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1dac6-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1dac6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1dac6-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="1dac6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1dac6-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dac6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1dac6-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación SD Elements.</span><span class="sxs-lookup"><span data-stu-id="1dac6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SD Elements application.</span></span>

<span data-ttu-id="1dac6-150">**Para configurar el inicio de sesión único de Azure AD con SD Elements, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="1dac6-150">**To configure Azure AD single sign-on with SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="1dac6-151">En Azure Portal, en la página de integración de la aplicación **SD Elements**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-151">In the Azure portal, on the **SD Elements** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="1dac6-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1dac6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. <span data-ttu-id="1dac6-155">En la sección **Dominio y direcciones URL de SD Elements** , lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1dac6-155">On the **SD Elements Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    <span data-ttu-id="1dac6-157">a.</span><span class="sxs-lookup"><span data-stu-id="1dac6-157">a.</span></span> <span data-ttu-id="1dac6-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span><span class="sxs-lookup"><span data-stu-id="1dac6-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span></span>

    <span data-ttu-id="1dac6-159">b.</span><span class="sxs-lookup"><span data-stu-id="1dac6-159">b.</span></span> <span data-ttu-id="1dac6-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<tenantname>.sdelements.com/sso/saml2/acs/`.</span><span class="sxs-lookup"><span data-stu-id="1dac6-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1dac6-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="1dac6-161">These values are not real.</span></span> <span data-ttu-id="1dac6-162">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="1dac6-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="1dac6-163">Póngase en contacto con el [equipo de soporte técnico de SD Elements](mailto:support@sdelements.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="1dac6-163">Contact [SD Elements support team](mailto:support@sdelements.com) to get these values.</span></span>

4. <span data-ttu-id="1dac6-164">La aplicación SD Elements espera que las aserciones SAML se encuentren en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="1dac6-164">SD Elements application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="1dac6-165">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="1dac6-165">Configure the following claims for this application.</span></span> <span data-ttu-id="1dac6-166">Puede administrar el valor de estos atributos desde la pestaña **"Atributo de usuario"** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1dac6-166">You can manage the values of these attributes from the **"User Attribute"** tab of the application.</span></span> <span data-ttu-id="1dac6-167">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="1dac6-167">The following screenshot shows an example for this.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. <span data-ttu-id="1dac6-169">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo token de SAML como muestra la imagen y siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="1dac6-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span> 

    | <span data-ttu-id="1dac6-170">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="1dac6-170">Attribute Name</span></span> | <span data-ttu-id="1dac6-171">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="1dac6-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="1dac6-172">email</span><span class="sxs-lookup"><span data-stu-id="1dac6-172">email</span></span> |<span data-ttu-id="1dac6-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="1dac6-173">user.mail</span></span> |
    | <span data-ttu-id="1dac6-174">firstname</span><span class="sxs-lookup"><span data-stu-id="1dac6-174">firstname</span></span> |<span data-ttu-id="1dac6-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="1dac6-175">user.givenname</span></span> |
    | <span data-ttu-id="1dac6-176">lastname</span><span class="sxs-lookup"><span data-stu-id="1dac6-176">lastname</span></span> |<span data-ttu-id="1dac6-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="1dac6-177">user.surname</span></span> |

    <span data-ttu-id="1dac6-178">a.</span><span class="sxs-lookup"><span data-stu-id="1dac6-178">a.</span></span> <span data-ttu-id="1dac6-179">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="1dac6-182">b.</span><span class="sxs-lookup"><span data-stu-id="1dac6-182">b.</span></span> <span data-ttu-id="1dac6-183">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="1dac6-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="1dac6-184">c.</span><span class="sxs-lookup"><span data-stu-id="1dac6-184">c.</span></span> <span data-ttu-id="1dac6-185">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="1dac6-185">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="1dac6-186">d.</span><span class="sxs-lookup"><span data-stu-id="1dac6-186">d.</span></span> <span data-ttu-id="1dac6-187">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-187">Click **Ok**.</span></span>
 
6. <span data-ttu-id="1dac6-188">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="1dac6-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. <span data-ttu-id="1dac6-190">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="1dac6-190">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1dac6-192">En la sección **Configuración de SD Elements**, haga clic en **Configurar SD Elements** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-192">On the **SD Elements Configuration** section, click **Configure SD Elements** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1dac6-193">Copie los valores de **SAML Entity ID y SAML Single Sign-On Service URL** (Identificador de entidad de SAML y URL del servicio de inicio de sesión único de SAML) de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-193">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. <span data-ttu-id="1dac6-195">Para que le habiliten el inicio de sesión único, póngase en contacto con su [equipo de soporte técnico de SD Elements](mailto:support@sdelements.com) y proporcióneles el archivo de certificado descargado.</span><span class="sxs-lookup"><span data-stu-id="1dac6-195">To get single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with the downloaded certificate file.</span></span> 

10. <span data-ttu-id="1dac6-196">En una ventana diferente del explorador, inicie sesión en su inquilino de SD Elements como administrador.</span><span class="sxs-lookup"><span data-stu-id="1dac6-196">In a different browser window, sign-on to your SD Elements tenant as an administrator.</span></span>

11. <span data-ttu-id="1dac6-197">En el menú de la parte superior, haga clic en **Sistema** y luego en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-197">In the menu on the top, click **System**, and then **Single Sign-on**.</span></span> 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. <span data-ttu-id="1dac6-199">En el cuadro de diálogo **Configuración de inicio de sesión único** , siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="1dac6-199">On the **Single Sign-On Settings** dialog, perform the following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    <span data-ttu-id="1dac6-201">a.</span><span class="sxs-lookup"><span data-stu-id="1dac6-201">a.</span></span> <span data-ttu-id="1dac6-202">Como **Tipo de inicio de sesión único**, seleccione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-202">As **SSO Type**, select **SAML**.</span></span>
   
    <span data-ttu-id="1dac6-203">b.</span><span class="sxs-lookup"><span data-stu-id="1dac6-203">b.</span></span> <span data-ttu-id="1dac6-204">En el cuadro de texto **Identity Provider Entity ID)** (Identificador de entidad del proveedor de identidad), pegue el valor del **Identificador de entidad de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1dac6-204">In the **Identity Provider Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="1dac6-205">c.</span><span class="sxs-lookup"><span data-stu-id="1dac6-205">c.</span></span> <span data-ttu-id="1dac6-206">En el cuadro de texto **Identity Provider Single Sign-On Service** (Servicio de inicio de sesión único del proveedor de identidades), pegue el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1dac6-206">In the **Identity Provider Single Sign-On Service** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="1dac6-207">d.</span><span class="sxs-lookup"><span data-stu-id="1dac6-207">d.</span></span> <span data-ttu-id="1dac6-208">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-208">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1dac6-209">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1dac6-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1dac6-210">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="1dac6-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1dac6-211">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1dac6-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1dac6-212">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dac6-212">Creating an Azure AD test user</span></span>
<span data-ttu-id="1dac6-213">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1dac6-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="1dac6-215">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="1dac6-215">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1dac6-216">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-216">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1dac6-218">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-218">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1dac6-220">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1dac6-220">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1dac6-222">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="1dac6-222">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1dac6-224">a.</span><span class="sxs-lookup"><span data-stu-id="1dac6-224">a.</span></span> <span data-ttu-id="1dac6-225">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-225">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1dac6-226">b.</span><span class="sxs-lookup"><span data-stu-id="1dac6-226">b.</span></span> <span data-ttu-id="1dac6-227">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1dac6-227">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1dac6-228">c.</span><span class="sxs-lookup"><span data-stu-id="1dac6-228">c.</span></span> <span data-ttu-id="1dac6-229">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-229">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1dac6-230">d.</span><span class="sxs-lookup"><span data-stu-id="1dac6-230">d.</span></span> <span data-ttu-id="1dac6-231">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-231">Click **Create**.</span></span>
 
### <a name="creating-a-sd-elements-test-user"></a><span data-ttu-id="1dac6-232">Creación de un usuario de prueba de SD Elements</span><span class="sxs-lookup"><span data-stu-id="1dac6-232">Creating a SD Elements test user</span></span>

<span data-ttu-id="1dac6-233">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en SD Elements.</span><span class="sxs-lookup"><span data-stu-id="1dac6-233">The objective of this section is to create a user called Britta Simon in SD Elements.</span></span> <span data-ttu-id="1dac6-234">En el caso de SD Elements, la creación de usuarios de SD Elements es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="1dac6-234">In the case of SD Elements, creating SD Elements users is a manual task.</span></span>

<span data-ttu-id="1dac6-235">**Para crear a Britta Simon en SD Elements, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="1dac6-235">**To create Britta Simon in SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="1dac6-236">En una ventana de explorador web, inicie sesión como administrador en el sitio de la empresa de SD Elements.</span><span class="sxs-lookup"><span data-stu-id="1dac6-236">In a web browser window, sign-on to your SD Elements company site as an administrator.</span></span>

2. <span data-ttu-id="1dac6-237">En el menú de la parte superior, haga clic en **User Management** (Administración de usuarios) y luego en **Users** (Usuarios).</span><span class="sxs-lookup"><span data-stu-id="1dac6-237">In the menu on the top, click **User Management**, and then **Users**.</span></span>
   
    ![Creación de un usuario de prueba de SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. <span data-ttu-id="1dac6-239">Haga clic en **Add New User**(Agregar nuevo usuario).</span><span class="sxs-lookup"><span data-stu-id="1dac6-239">Click **Add New User**.</span></span>
   
    ![Creación de un usuario de prueba de SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. <span data-ttu-id="1dac6-241">En el cuadro de diálogo **Add New User** (Agregar nuevo usuario), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1dac6-241">On the **Add New User** dialog, perform the following steps:</span></span>
   
    ![Creación de un usuario de prueba de SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    <span data-ttu-id="1dac6-243">a.</span><span class="sxs-lookup"><span data-stu-id="1dac6-243">a.</span></span> <span data-ttu-id="1dac6-244">En el cuadro de texto **E-mail** (Correo electrónico), escriba el correo electrónico del usuario con el siguiente formato **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-244">In the **E-mail** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="1dac6-245">b.</span><span class="sxs-lookup"><span data-stu-id="1dac6-245">b.</span></span> <span data-ttu-id="1dac6-246">En el cuadro de texto **First Name** (Nombre), escriba el nombre de usuario, en este caso **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-246">In the **First Name** textbox, enter the first name of user like **Britta**.</span></span>
   
    <span data-ttu-id="1dac6-247">c.</span><span class="sxs-lookup"><span data-stu-id="1dac6-247">c.</span></span> <span data-ttu-id="1dac6-248">En el cuadro de texto **Last Name** (Apellidos), escriba el apellido del usuario, en este caso **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-248">In the **Last Name** textbox, enter the last name of user like **Simon**.</span></span>
   
    <span data-ttu-id="1dac6-249">d.</span><span class="sxs-lookup"><span data-stu-id="1dac6-249">d.</span></span> <span data-ttu-id="1dac6-250">Como **Rol**, seleccione **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-250">As **Role**, select **User**.</span></span> 
   
    <span data-ttu-id="1dac6-251">e.</span><span class="sxs-lookup"><span data-stu-id="1dac6-251">e.</span></span> <span data-ttu-id="1dac6-252">Haga clic en **Create User**(Crear usuario).</span><span class="sxs-lookup"><span data-stu-id="1dac6-252">Click **Create User**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1dac6-253">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dac6-253">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1dac6-254">En esta sección, concederá acceso a Britta Simon a SD Elements para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="1dac6-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SD Elements.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="1dac6-256">**Para asignar a Britta Simon a SD Elements, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="1dac6-256">**To assign Britta Simon to SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="1dac6-257">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="1dac6-259">En la lista de aplicaciones, seleccione **SD Elements**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-259">In the applications list, select **SD Elements**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. <span data-ttu-id="1dac6-261">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-261">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="1dac6-263">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-263">Click **Add** button.</span></span> <span data-ttu-id="1dac6-264">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="1dac6-266">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="1dac6-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1dac6-267">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1dac6-268">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1dac6-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1dac6-269">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="1dac6-269">Testing single sign-on</span></span>

<span data-ttu-id="1dac6-270">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="1dac6-270">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
  
<span data-ttu-id="1dac6-271">Al hacer clic en el icono de SD Elements en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación SD Elements.</span><span class="sxs-lookup"><span data-stu-id="1dac6-271">When you click the SD Elements tile in the Access Panel, you should get automatically signed-on to your SD Elements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1dac6-272">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="1dac6-272">Additional resources</span></span>

* [<span data-ttu-id="1dac6-273">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1dac6-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1dac6-274">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1dac6-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

