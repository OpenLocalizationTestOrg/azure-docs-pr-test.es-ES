---
title: "Tutorial: integración de Azure Active Directory con ADP eTime | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y ADP eTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 31fed307a32e629d00aab7cc9d5167ee16d83936
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="01d61-103">Tutorial: Integración de Azure Active Directory con ADP eTime</span><span class="sxs-lookup"><span data-stu-id="01d61-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="01d61-104">En este tutorial, obtendrá información sobre cómo integrar ADP eTime con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="01d61-104">In this tutorial, you learn how to integrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="01d61-105">La integración de ADP eTime con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="01d61-105">Integrating ADP eTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="01d61-106">Puede controlar en Azure AD quién tiene acceso a ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="01d61-106">You can control in Azure AD who has access to ADP eTime</span></span>
- <span data-ttu-id="01d61-107">Puede permitir que los usuarios inicien sesión automáticamente en ADP eTime (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01d61-107">You can enable your users to automatically get signed-on to ADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="01d61-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="01d61-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="01d61-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="01d61-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01d61-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="01d61-110">Prerequisites</span></span>

<span data-ttu-id="01d61-111">Para configurar la integración de Azure AD con ADP eTime, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="01d61-111">To configure Azure AD integration with ADP eTime, you need the following items:</span></span>

- <span data-ttu-id="01d61-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="01d61-112">An Azure AD subscription</span></span>
- <span data-ttu-id="01d61-113">Una suscripción habilitada para el inicio de sesión único en ADP eTime</span><span class="sxs-lookup"><span data-stu-id="01d61-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="01d61-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="01d61-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="01d61-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="01d61-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="01d61-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="01d61-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="01d61-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="01d61-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="01d61-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="01d61-118">Scenario description</span></span>
<span data-ttu-id="01d61-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="01d61-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="01d61-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="01d61-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="01d61-121">Adición de ADP eTime desde la galería</span><span class="sxs-lookup"><span data-stu-id="01d61-121">Adding ADP eTime from the gallery</span></span>
2. <span data-ttu-id="01d61-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="01d61-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-the-gallery"></a><span data-ttu-id="01d61-123">Adición de ADP eTime desde la galería</span><span class="sxs-lookup"><span data-stu-id="01d61-123">Adding ADP eTime from the gallery</span></span>
<span data-ttu-id="01d61-124">Para configurar la integración de ADP eTime en Azure AD, es preciso agregar ADP eTime desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="01d61-124">To configure the integration of ADP eTime into Azure AD, you need to add ADP eTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="01d61-125">**Para agregar ADP eTime desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="01d61-125">**To add ADP eTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="01d61-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="01d61-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="01d61-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="01d61-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="01d61-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="01d61-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="01d61-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="01d61-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="01d61-133">En el cuadro de búsqueda, escriba **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="01d61-133">In the search box, type **ADP eTime**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="01d61-135">En el panel de resultados, seleccione **ADP eTime** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="01d61-135">In the results panel, select **ADP eTime**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="01d61-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="01d61-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="01d61-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ADP eTime con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="01d61-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="01d61-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de ADP eTime para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01d61-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP eTime is to a user in Azure AD.</span></span> <span data-ttu-id="01d61-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="01d61-140">In other words, a link relationship between an Azure AD user and the related user in ADP eTime needs to be established.</span></span>

<span data-ttu-id="01d61-141">Esta relación de vínculo se establece asignando el valor del **nombre de usuario** en Azure AD como valor del **nombre de usuario** en ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="01d61-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP eTime.</span></span>

<span data-ttu-id="01d61-142">Para configurar y probar el inicio de sesión único de Azure AD con ADP eTime, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="01d61-142">To configure and test Azure AD single sign-on with ADP eTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="01d61-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="01d61-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="01d61-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="01d61-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="01d61-145">**[Creación de un usuario de prueba de ADP eTime](#creating-an-adp-etime-test-user)**: para tener un homólogo de Britta Simon en ADP eTime que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01d61-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - to have a counterpart of Britta Simon in ADP eTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="01d61-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01d61-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="01d61-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="01d61-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="01d61-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="01d61-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="01d61-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="01d61-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="01d61-150">**Para configurar el inicio de sesión único de Azure AD con ADP eTime, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="01d61-150">**To configure Azure AD single sign-on with ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="01d61-151">En Azure Portal, en la página de integración de la aplicación **ADP eTime**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="01d61-151">In the Azure portal, on the **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="01d61-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="01d61-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="01d61-155">En la sección **Dominio y direcciones URL de ADP eTime**, lleve a cabo el paso siguiente:</span><span class="sxs-lookup"><span data-stu-id="01d61-155">On the **ADP eTime Domain and URLs** section, perform the following step:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="01d61-157">a.</span><span class="sxs-lookup"><span data-stu-id="01d61-157">a.</span></span> <span data-ttu-id="01d61-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<servername>.adp.com`</span><span class="sxs-lookup"><span data-stu-id="01d61-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="01d61-159">b.</span><span class="sxs-lookup"><span data-stu-id="01d61-159">b.</span></span> <span data-ttu-id="01d61-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`.</span><span class="sxs-lookup"><span data-stu-id="01d61-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="01d61-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="01d61-161">These values are not the real.</span></span> <span data-ttu-id="01d61-162">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="01d61-162">Update these values with the actual Reply URL and Identifier.</span></span> <span data-ttu-id="01d61-163">Póngase en contacto con el [equipo de soporte técnico de ADP eTime](https://www.adp.com/contact-us/overview.aspx) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="01d61-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) to get these values.</span></span>

4. <span data-ttu-id="01d61-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="01d61-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="01d61-166">La aplicación ADP eTime espera las aserciones de SAML en un formato específico, que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los atributos del token de SAML.</span><span class="sxs-lookup"><span data-stu-id="01d61-166">The ADP eTime application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="01d61-167">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="01d61-167">The following screenshot shows an example for this.</span></span> <span data-ttu-id="01d61-168">El nombre de la notificación siempre será **"PersonImmutableID"** cuyo valor hemos asignado a ExtensionAttribute2 que contiene el EmployeeID del usuario.</span><span class="sxs-lookup"><span data-stu-id="01d61-168">The claim name will always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2 which contains the EmployeeID of the user.</span></span> 

    <span data-ttu-id="01d61-169">Aquí se realizará la asignación de usuario desde Azure AD a ADP eTime en el valor EmployeeID pero puede asignarlo a un valor diferente que también se base en la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="01d61-169">Here the user mapping from Azure AD to ADP eTime will be done on the EmployeeID but you can map this to a different value also based on your application settings.</span></span> <span data-ttu-id="01d61-170">Por tanto, colabore con el **equipo de soporte técnico de ADP eTime** primero para usar el identificador correcto de un usuario y asigne ese valor a la notificación ["PersonImmutableID"](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="01d61-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="01d61-172">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo token de SAML como muestra la imagen y siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="01d61-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="01d61-173">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="01d61-173">Attribute Name</span></span> | <span data-ttu-id="01d61-174">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="01d61-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="01d61-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="01d61-175">PersonImmutableID</span></span> | <span data-ttu-id="01d61-176">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="01d61-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="01d61-177">a.</span><span class="sxs-lookup"><span data-stu-id="01d61-177">a.</span></span> <span data-ttu-id="01d61-178">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="01d61-178">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="01d61-181">b.</span><span class="sxs-lookup"><span data-stu-id="01d61-181">b.</span></span> <span data-ttu-id="01d61-182">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="01d61-182">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="01d61-183">c.</span><span class="sxs-lookup"><span data-stu-id="01d61-183">c.</span></span> <span data-ttu-id="01d61-184">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="01d61-184">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="01d61-185">d.</span><span class="sxs-lookup"><span data-stu-id="01d61-185">d.</span></span> <span data-ttu-id="01d61-186">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="01d61-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="01d61-187">Antes de configurar la aserción SAML, debe ponerse en contacto con el [equipo de soporte técnico de ADP eTime](https://www.adp.com/contact-us/overview.aspx) y solicitar el valor del atributo de identificador único para el inquilino.</span><span class="sxs-lookup"><span data-stu-id="01d61-187">Before you can configure the SAML assertion, you need to contact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="01d61-188">Necesitará este valor para configurar la notificación personalizada para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="01d61-188">You need this value to configure the custom claim for your application.</span></span> 

7. <span data-ttu-id="01d61-189">En la sección **Configuración de ADP eTime**, haga clic en **Configurar ADP eTime** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="01d61-189">On the **ADP eTime Configuration** section, click **Configure ADP eTime** to open **Configure sign-on** window.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="01d61-191">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="01d61-191">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="01d61-193">Para configurar el inicio de sesión único en **ADP eTime**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de ADP eTime](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="01d61-193">To configure single sign-on on **ADP eTime** side, you need to send the downloaded **Metadata XML** to [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="01d61-194">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="01d61-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="01d61-195">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="01d61-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="01d61-196">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="01d61-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="01d61-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="01d61-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="01d61-198">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="01d61-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="01d61-200">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="01d61-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="01d61-201">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="01d61-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="01d61-203">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="01d61-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="01d61-205">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="01d61-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="01d61-207">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="01d61-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="01d61-209">a.</span><span class="sxs-lookup"><span data-stu-id="01d61-209">a.</span></span> <span data-ttu-id="01d61-210">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="01d61-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="01d61-211">b.</span><span class="sxs-lookup"><span data-stu-id="01d61-211">b.</span></span> <span data-ttu-id="01d61-212">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="01d61-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="01d61-213">c.</span><span class="sxs-lookup"><span data-stu-id="01d61-213">c.</span></span> <span data-ttu-id="01d61-214">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="01d61-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="01d61-215">d.</span><span class="sxs-lookup"><span data-stu-id="01d61-215">d.</span></span> <span data-ttu-id="01d61-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="01d61-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="01d61-217">Creación de un usuario de prueba de ADP eTime</span><span class="sxs-lookup"><span data-stu-id="01d61-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="01d61-218">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="01d61-218">The objective of this section is to create a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="01d61-219">Colabore con el [equipo de soporte técnico de ADP eTime](https://www.adp.com/contact-us/overview.aspx) para agregar usuarios a la cuenta de ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="01d61-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP eTime account.</span></span> 
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="01d61-220">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="01d61-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="01d61-221">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="01d61-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP eTime.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="01d61-223">**Para asignar a Britta Simon a ADP eTime, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="01d61-223">**To assign Britta Simon to ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="01d61-224">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="01d61-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="01d61-226">En la lista de aplicaciones, seleccione **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="01d61-226">In the applications list, select **ADP eTime**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="01d61-228">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="01d61-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="01d61-230">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="01d61-230">Click **Add** button.</span></span> <span data-ttu-id="01d61-231">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="01d61-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="01d61-233">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="01d61-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="01d61-234">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="01d61-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="01d61-235">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="01d61-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="01d61-236">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="01d61-236">Testing single sign-on</span></span>

<span data-ttu-id="01d61-237">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="01d61-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="01d61-238">Al hacer clic en el icono de ADP eTime en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="01d61-238">When you click the ADP eTime tile in the Access Panel, you should get automatically signed-on to your ADP eTime application.</span></span>
<span data-ttu-id="01d61-239">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="01d61-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="01d61-240">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="01d61-240">Additional resources</span></span>

* [<span data-ttu-id="01d61-241">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="01d61-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="01d61-242">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="01d61-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

