---
title: "Tutorial: Integración de Azure Active Directory con Learningpool Act | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Learningpool Act."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 51e8695f-31e1-4d09-8eb3-13241999d99f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 932f5f12c75299e532d3fa2c31f1805a7df30158
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learningpool-act"></a><span data-ttu-id="0201e-103">Tutorial: Integración de Azure Active Directory con Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="0201e-103">Tutorial: Azure Active Directory integration with Learningpool Act</span></span>

<span data-ttu-id="0201e-104">En este tutorial, obtendrá información sobre cómo integrar Learningpool Act con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0201e-104">In this tutorial, you learn how to integrate Learningpool Act with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0201e-105">La integración de Learningpool Act con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0201e-105">Integrating Learningpool Act with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0201e-106">Puede controlar en Azure AD quién tiene acceso a Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="0201e-106">You can control in Azure AD who has access to Learningpool Act</span></span>
- <span data-ttu-id="0201e-107">Puede permitir que los usuarios inicien sesión automáticamente en Learningpool Act (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0201e-107">You can enable your users to automatically get signed-on to Learningpool Act (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0201e-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0201e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0201e-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0201e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0201e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0201e-110">Prerequisites</span></span>

<span data-ttu-id="0201e-111">Para configurar la integración de Azure AD con Learningpool Act, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0201e-111">To configure Azure AD integration with Learningpool Act, you need the following items:</span></span>

- <span data-ttu-id="0201e-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0201e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0201e-113">Una suscripción habilitada para inicio de sesión único en Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="0201e-113">A Learningpool Act single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0201e-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0201e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0201e-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0201e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0201e-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0201e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0201e-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0201e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0201e-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0201e-118">Scenario description</span></span>
<span data-ttu-id="0201e-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0201e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0201e-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="0201e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0201e-121">Incorporación de Learningpool Act desde la galería</span><span class="sxs-lookup"><span data-stu-id="0201e-121">Adding Learningpool Act from the gallery</span></span>
2. <span data-ttu-id="0201e-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0201e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learningpool-act-from-the-gallery"></a><span data-ttu-id="0201e-123">Incorporación de Learningpool Act desde la galería</span><span class="sxs-lookup"><span data-stu-id="0201e-123">Adding Learningpool Act from the gallery</span></span>
<span data-ttu-id="0201e-124">Para configurar la integración de Learningpool Act en Azure AD, deberá agregar Learningpool Act desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="0201e-124">To configure the integration of Learningpool Act into Azure AD, you need to add Learningpool Act from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0201e-125">**Para agregar Learningpool Act desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="0201e-125">**To add Learningpool Act from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0201e-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0201e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0201e-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0201e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0201e-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0201e-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0201e-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0201e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0201e-133">En el cuadro de búsqueda, escriba **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="0201e-133">In the search box, type **Learningpool Act**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_search.png)

5. <span data-ttu-id="0201e-135">En el panel de resultados, seleccione **Learningpool Act** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0201e-135">In the results panel, select **Learningpool Act**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0201e-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0201e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0201e-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Learningpool Act con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0201e-138">In this section, you configure and test Azure AD single sign-on with Learningpool Act based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0201e-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Learningpool Act para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0201e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learningpool Act is to a user in Azure AD.</span></span> <span data-ttu-id="0201e-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="0201e-140">In other words, a link relationship between an Azure AD user and the related user in Learningpool Act needs to be established.</span></span>

<span data-ttu-id="0201e-141">En Learningpool Act, para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="0201e-141">In Learningpool Act, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0201e-142">Para configurar y probar el inicio de sesión único de Azure AD con Learningpool Act, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0201e-142">To configure and test Azure AD single sign-on with Learningpool Act, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0201e-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="0201e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0201e-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0201e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0201e-145">**[Creación de un usuario de prueba de Learningpool Act](#creating-a-learningpool-act-test-user)**: para tener un homólogo de Britta Simon en Learningpool Act vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0201e-145">**[Creating a Learningpool Act test user](#creating-a-learningpool-act-test-user)** - to have a counterpart of Britta Simon in Learningpool Act that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0201e-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0201e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0201e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0201e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0201e-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0201e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0201e-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="0201e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learningpool Act application.</span></span>

<span data-ttu-id="0201e-150">**Para configurar el inicio de sesión único de Azure AD con Learningpool Act, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="0201e-150">**To configure Azure AD single sign-on with Learningpool Act, perform the following steps:**</span></span>

1. <span data-ttu-id="0201e-151">En Azure Portal, en la página de integración de la aplicación **Learningpool Act**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0201e-151">In the Azure portal, on the **Learningpool Act** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0201e-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0201e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_samlbase.png)

3. <span data-ttu-id="0201e-155">En la sección **Dominio y direcciones URL de Learningpool Act**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="0201e-155">On the **Learningpool Act Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_url.png)

    <span data-ttu-id="0201e-157">a.</span><span class="sxs-lookup"><span data-stu-id="0201e-157">a.</span></span> <span data-ttu-id="0201e-158">En el cuadro de texto **URL de inicio de sesión**, escriba la dirección URL: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span><span class="sxs-lookup"><span data-stu-id="0201e-158">In the **Sign-on URL** textbox, type the URL: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span></span>

    <span data-ttu-id="0201e-159">b.</span><span class="sxs-lookup"><span data-stu-id="0201e-159">b.</span></span> <span data-ttu-id="0201e-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="0201e-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.Learningpool.com/shibboleth` |
    | `https://<subdomain>.preview.Learningpool.com/shibboleth` |

    > [!NOTE] 
    > <span data-ttu-id="0201e-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="0201e-161">These values are not real.</span></span> <span data-ttu-id="0201e-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="0201e-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0201e-163">Póngase en contacto con el [equipo de soporte técnico de Learningpool Act](https://www.Learningpool.com/support) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="0201e-163">Contact [Learningpool Act Client support team](https://www.Learningpool.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="0201e-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0201e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_certificate.png) 

5. <span data-ttu-id="0201e-166">La aplicación Learningpool Act espera las aserciones de SAML en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="0201e-166">Learningpool Act application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="0201e-167">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="0201e-167">Please configure the following claims for this application.</span></span> <span data-ttu-id="0201e-168">Puede administrar el valor de estos atributos desde la pestaña **"Atributo"** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0201e-168">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="0201e-169">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="0201e-169">The following screenshot shows an example for this.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_attribute.png) 

6. <span data-ttu-id="0201e-171">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo token de SAML como muestra la imagen y siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0201e-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="0201e-172">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="0201e-172">Attribute Name</span></span> | <span data-ttu-id="0201e-173">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="0201e-173">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="0201e-174">urn:oid:1.2.840.113556.1.4.221</span><span class="sxs-lookup"><span data-stu-id="0201e-174">urn:oid:1.2.840.113556.1.4.221</span></span> | <span data-ttu-id="0201e-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="0201e-175">user.userprincipalname</span></span> |
    | <span data-ttu-id="0201e-176">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="0201e-176">urn:oid:2.5.4.42</span></span> | <span data-ttu-id="0201e-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="0201e-177">user.givenname</span></span> |
    | <span data-ttu-id="0201e-178">urn:oid:0.9.2342.19200300.100.1.3</span><span class="sxs-lookup"><span data-stu-id="0201e-178">urn:oid:0.9.2342.19200300.100.1.3</span></span> | <span data-ttu-id="0201e-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="0201e-179">user.mail</span></span> |    
    | <span data-ttu-id="0201e-180">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="0201e-180">urn:oid:2.5.4.4</span></span> | <span data-ttu-id="0201e-181">user.surname</span><span class="sxs-lookup"><span data-stu-id="0201e-181">user.surname</span></span> |
    
    <span data-ttu-id="0201e-182">a.</span><span class="sxs-lookup"><span data-stu-id="0201e-182">a.</span></span> <span data-ttu-id="0201e-183">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="0201e-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="0201e-186">b.</span><span class="sxs-lookup"><span data-stu-id="0201e-186">b.</span></span> <span data-ttu-id="0201e-187">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="0201e-187">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="0201e-188">c.</span><span class="sxs-lookup"><span data-stu-id="0201e-188">c.</span></span> <span data-ttu-id="0201e-189">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="0201e-189">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="0201e-190">d.</span><span class="sxs-lookup"><span data-stu-id="0201e-190">d.</span></span> <span data-ttu-id="0201e-191">Deje **Espacio de nombres** en blanco.</span><span class="sxs-lookup"><span data-stu-id="0201e-191">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="0201e-192">e.</span><span class="sxs-lookup"><span data-stu-id="0201e-192">e.</span></span> <span data-ttu-id="0201e-193">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0201e-193">Click **Ok**.</span></span>

7. <span data-ttu-id="0201e-194">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0201e-194">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Learningpool-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="0201e-196">Para configurar el inicio de sesión único en **Learningpool Act**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="0201e-196">To configure single sign-on on **Learningpool Act** side, you need to send the downloaded **Metadata XML** to [Learningpool Act support team](https://www.Learningpool.com/support).</span></span> <span data-ttu-id="0201e-197">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="0201e-197">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0201e-198">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0201e-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0201e-199">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="0201e-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0201e-200">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0201e-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0201e-201">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0201e-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="0201e-202">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0201e-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0201e-204">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="0201e-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0201e-205">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0201e-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0201e-207">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0201e-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0201e-209">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0201e-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0201e-211">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="0201e-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0201e-213">a.</span><span class="sxs-lookup"><span data-stu-id="0201e-213">a.</span></span> <span data-ttu-id="0201e-214">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0201e-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0201e-215">b.</span><span class="sxs-lookup"><span data-stu-id="0201e-215">b.</span></span> <span data-ttu-id="0201e-216">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0201e-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0201e-217">c.</span><span class="sxs-lookup"><span data-stu-id="0201e-217">c.</span></span> <span data-ttu-id="0201e-218">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0201e-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0201e-219">d.</span><span class="sxs-lookup"><span data-stu-id="0201e-219">d.</span></span> <span data-ttu-id="0201e-220">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0201e-220">Click **Create**.</span></span>
 
### <a name="creating-a-learningpool-act-test-user"></a><span data-ttu-id="0201e-221">Creación de un usuario de prueba de Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="0201e-221">Creating a Learningpool Act test user</span></span>

<span data-ttu-id="0201e-222">Para permitir que los usuarios de Azure AD inicien sesión en Learningpool Act, deben aprovisionarse en Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="0201e-222">To enable Azure AD users to log in to Learningpool Act, they must be provisioned into Learningpool Act.</span></span>

<span data-ttu-id="0201e-223">No hay ningún elemento de acción para deba realizar para configurar el aprovisionamiento de usuarios en Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="0201e-223">There is no action item for you to configure user provisioning to Learningpool Act.</span></span>  
<span data-ttu-id="0201e-224">Los usuarios deben ser creados por el [equipo de soporte técnico de Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="0201e-224">Users need to be created by your [Learningpool Act support team](https://www.Learningpool.com/support).</span></span>

>[!NOTE]
><span data-ttu-id="0201e-225">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Learningpool Act ofrecida por Learningpool Act para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="0201e-225">You can use any other Learningpool Act user account creation tools or APIs provided by Learningpool Act to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0201e-226">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0201e-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0201e-227">En esta sección, concederá acceso a Britta Simon a Learningpool Act para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="0201e-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learningpool Act.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0201e-229">**Para asignar a Britta Simon a Learningpool Act, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="0201e-229">**To assign Britta Simon to Learningpool Act, perform the following steps:**</span></span>

1. <span data-ttu-id="0201e-230">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0201e-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0201e-232">En la lista de aplicaciones, seleccione **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="0201e-232">In the applications list, select **Learningpool Act**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_app.png) 

3. <span data-ttu-id="0201e-234">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0201e-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0201e-236">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0201e-236">Click **Add** button.</span></span> <span data-ttu-id="0201e-237">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0201e-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0201e-239">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="0201e-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0201e-240">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0201e-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0201e-241">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0201e-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0201e-242">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="0201e-242">Testing single sign-on</span></span>

<span data-ttu-id="0201e-243">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0201e-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0201e-244">Al hacer clic en el icono de Learningpool Act en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="0201e-244">When you click the Learningpool Act tile in the Access Panel, you should get automatically signed-on to your Learningpool Act application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0201e-245">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0201e-245">Additional resources</span></span>

* [<span data-ttu-id="0201e-246">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0201e-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0201e-247">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0201e-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_203.png

