---
title: "Tutorial: Integración de Azure Active Directory con Domo | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Domo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 058626e4-73b3-4dc2-86ca-b060d002d70a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: 919d2262cf9f14159a13370037301005b5b69da2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-domo"></a><span data-ttu-id="bb446-103">Tutorial: integración de Azure Active Directory con Domo</span><span class="sxs-lookup"><span data-stu-id="bb446-103">Tutorial: Azure Active Directory integration with Domo</span></span>

<span data-ttu-id="bb446-104">En este tutorial, aprenderá a integrar Domo con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bb446-104">In this tutorial, you learn how to integrate Domo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bb446-105">Integrar Domo con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="bb446-105">Integrating Domo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bb446-106">Puede controlar en Azure AD quién tiene acceso a Domo.</span><span class="sxs-lookup"><span data-stu-id="bb446-106">You can control in Azure AD who has access to Domo</span></span>
- <span data-ttu-id="bb446-107">Puede permitir que los usuarios inicien sesión automáticamente en Domo (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb446-107">You can enable your users to automatically get signed-on to Domo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bb446-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="bb446-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bb446-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bb446-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb446-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bb446-110">Prerequisites</span></span>

<span data-ttu-id="bb446-111">Para configurar la integración de Azure AD con Domo, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="bb446-111">To configure Azure AD integration with Domo, you need the following items:</span></span>

- <span data-ttu-id="bb446-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb446-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bb446-113">Una suscripción habilitada para el inicio de sesión único en Domo</span><span class="sxs-lookup"><span data-stu-id="bb446-113">A Domo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bb446-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="bb446-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bb446-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="bb446-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bb446-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bb446-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bb446-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bb446-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bb446-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="bb446-118">Scenario description</span></span>
<span data-ttu-id="bb446-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="bb446-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bb446-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="bb446-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bb446-121">Adición de Domo desde la galería</span><span class="sxs-lookup"><span data-stu-id="bb446-121">Adding Domo from the gallery</span></span>
2. <span data-ttu-id="bb446-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb446-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-domo-from-the-gallery"></a><span data-ttu-id="bb446-123">Adición de Domo desde la galería</span><span class="sxs-lookup"><span data-stu-id="bb446-123">Adding Domo from the gallery</span></span>
<span data-ttu-id="bb446-124">Para configurar la integración de Domo en Azure AD, deberá agregar Domo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="bb446-124">To configure the integration of Domo into Azure AD, you need to add Domo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bb446-125">**Para agregar Domo desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="bb446-125">**To add Domo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bb446-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bb446-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bb446-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="bb446-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bb446-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bb446-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="bb446-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bb446-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="bb446-133">En el cuadro de búsqueda, escriba **Domo**.</span><span class="sxs-lookup"><span data-stu-id="bb446-133">In the search box, type **Domo**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-domo-tutorial/tutorial_domo_search.png)

5. <span data-ttu-id="bb446-135">En el panel de resultados, seleccione **Domo** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bb446-135">In the results panel, select **Domo**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-domo-tutorial/tutorial_domo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bb446-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb446-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bb446-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Domo con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bb446-138">In this section, you configure and test Azure AD single sign-on with Domo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bb446-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Domo para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb446-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Domo is to a user in Azure AD.</span></span> <span data-ttu-id="bb446-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario correspondiente de Domo.</span><span class="sxs-lookup"><span data-stu-id="bb446-140">In other words, a link relationship between an Azure AD user and the related user in Domo needs to be established.</span></span>

<span data-ttu-id="bb446-141">Para establecer la relación de vínculo, en Domo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="bb446-141">In Domo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bb446-142">Para configurar y probar el inicio de sesión único de Azure AD con Domo, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="bb446-142">To configure and test Azure AD single sign-on with Domo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bb446-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="bb446-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bb446-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bb446-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bb446-145">**[Creación de usuario de prueba de Domo](#creating-a-domo-test-user)**: para tener un homólogo de Britta Simon en Domo que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb446-145">**[Creating a Domo test user](#creating-a-domo-test-user)** - to have a counterpart of Britta Simon in Domo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bb446-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb446-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bb446-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="bb446-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bb446-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb446-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bb446-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Domo.</span><span class="sxs-lookup"><span data-stu-id="bb446-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Domo application.</span></span>

<span data-ttu-id="bb446-150">**Para configurar el inicio de sesión único de Azure AD con Domo, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="bb446-150">**To configure Azure AD single sign-on with Domo, perform the following steps:**</span></span>

1. <span data-ttu-id="bb446-151">En Azure Portal, en la página de integración de la aplicación **Domo**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="bb446-151">In the Azure portal, on the **Domo** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="bb446-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="bb446-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-domo-tutorial/tutorial_domo_samlbase.png)

3. <span data-ttu-id="bb446-155">En la sección **Dominio y direcciones URL de Domo**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bb446-155">On the **Domo Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-domo-tutorial/tutorial_domo_url.png)

    <span data-ttu-id="bb446-157">a.</span><span class="sxs-lookup"><span data-stu-id="bb446-157">a.</span></span> <span data-ttu-id="bb446-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.domo.com`.</span><span class="sxs-lookup"><span data-stu-id="bb446-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.domo.com`</span></span>

    <span data-ttu-id="bb446-159">b.</span><span class="sxs-lookup"><span data-stu-id="bb446-159">b.</span></span> <span data-ttu-id="bb446-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="bb446-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span>     

    | |
    |--|    
    | `https://<companyname>.domo.com` |
    | `https://<companyname>.beta.domo.com` |
    | `https://<companyname>.demo.domo.com` |
    | `https://<companyname>.dev.domo.com` | 
    | `https://<companyname>.fastage1.domo.com` |       
    | `https://<companyname>.frdev.domo.com` |       
    | `https://<companyname>.gastage.domo.com` |       
    | `https://<companyname>.load.domo.com` |       
    | `https://<companyname>.local.domo.com` |       
    | `https://<companyname>.qa.domo.com` |
    | `https://<companyname>.stage.domo.com` |
    
    > [!NOTE] 
    > <span data-ttu-id="bb446-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="bb446-161">These values are not real.</span></span> <span data-ttu-id="bb446-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="bb446-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bb446-163">Póngase en contacto con el [equipo de soporte técnico de Domo](mailto:support@domo.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="bb446-163">Contact [Domo Client support team](mailto:support@domo.com) to get these values.</span></span>

4. <span data-ttu-id="bb446-164">La aplicación Domo espera las aserciones de SAML en un formato específico.</span><span class="sxs-lookup"><span data-stu-id="bb446-164">Domo application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="bb446-165">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="bb446-165">Configure the following claims for this application.</span></span> <span data-ttu-id="bb446-166">Puede administrar los valores de estos atributos en la sección "**Atributos de usuario**" de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bb446-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="bb446-167">En la siguiente captura de pantalla se muestra un ejemplo de esta configuración.</span><span class="sxs-lookup"><span data-stu-id="bb446-167">The following screenshot shows an example for this configuration.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-domo-tutorial/tutorial_domo_attributes.png)
    
5. <span data-ttu-id="bb446-169">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo token de SAML como muestra la imagen y siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="bb446-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="bb446-170">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="bb446-170">Attribute Name</span></span> | <span data-ttu-id="bb446-171">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="bb446-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="bb446-172">name</span><span class="sxs-lookup"><span data-stu-id="bb446-172">name</span></span> | <span data-ttu-id="bb446-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="bb446-173">user.displayname</span></span> |
    | <span data-ttu-id="bb446-174">email</span><span class="sxs-lookup"><span data-stu-id="bb446-174">email</span></span> | <span data-ttu-id="bb446-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="bb446-175">user.mail</span></span> |
    
    <span data-ttu-id="bb446-176">a.</span><span class="sxs-lookup"><span data-stu-id="bb446-176">a.</span></span> <span data-ttu-id="bb446-177">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="bb446-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-domo-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-domo-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="bb446-180">b.</span><span class="sxs-lookup"><span data-stu-id="bb446-180">b.</span></span> <span data-ttu-id="bb446-181">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="bb446-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="bb446-182">c.</span><span class="sxs-lookup"><span data-stu-id="bb446-182">c.</span></span> <span data-ttu-id="bb446-183">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="bb446-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="bb446-184">d.</span><span class="sxs-lookup"><span data-stu-id="bb446-184">d.</span></span> <span data-ttu-id="bb446-185">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bb446-185">Click **Ok**.</span></span> 
 
6. <span data-ttu-id="bb446-186">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="bb446-186">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-domo-tutorial/tutorial_domo_certificate.png) 

7. <span data-ttu-id="bb446-188">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="bb446-188">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-domo-tutorial/tutorial_general_400.png)


8. <span data-ttu-id="bb446-190">En la sección **Configuración de Domo**, haga clic en **Configurar Domo** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="bb446-190">On the **Domo Configuration** section, click **Configure Domo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bb446-191">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="bb446-191">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>   

   ![Configurar inicio de sesión único](./media/active-directory-saas-domo-tutorial/tutorial_domo_configure.png) 

9. <span data-ttu-id="bb446-193">Para configurar el inicio de sesión único en **Domo**, es preciso enviar el **certificado** descargado, el **identificador de identidad de SAML**, la **dirección URL de cierre de sesión** y la **dirección URL del servicio de inicio de sesión único de SAML** al [equipo de soporte técnico de Domo](mailto:support@domo.com).</span><span class="sxs-lookup"><span data-stu-id="bb446-193">To configure single sign-on on **Domo** side, you need to send the downloaded **Certificate**, **SAML Entity ID**, the **SAML Single Sign-On Service URL** and the **Sign-Out URL** to [Domo support team](mailto:support@domo.com).</span></span> <span data-ttu-id="bb446-194">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="bb446-194">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="bb446-195">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bb446-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bb446-196">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="bb446-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bb446-197">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bb446-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bb446-198">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb446-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="bb446-199">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bb446-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="bb446-201">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="bb446-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bb446-202">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bb446-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bb446-204">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="bb446-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bb446-206">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bb446-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bb446-208">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="bb446-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-domo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bb446-210">a.</span><span class="sxs-lookup"><span data-stu-id="bb446-210">a.</span></span> <span data-ttu-id="bb446-211">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bb446-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bb446-212">b.</span><span class="sxs-lookup"><span data-stu-id="bb446-212">b.</span></span> <span data-ttu-id="bb446-213">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bb446-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bb446-214">c.</span><span class="sxs-lookup"><span data-stu-id="bb446-214">c.</span></span> <span data-ttu-id="bb446-215">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="bb446-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bb446-216">d.</span><span class="sxs-lookup"><span data-stu-id="bb446-216">d.</span></span> <span data-ttu-id="bb446-217">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bb446-217">Click **Create**.</span></span>
 
### <a name="creating-a-domo-test-user"></a><span data-ttu-id="bb446-218">Creación de usuario de prueba de Domo</span><span class="sxs-lookup"><span data-stu-id="bb446-218">Creating a Domo test user</span></span>

<span data-ttu-id="bb446-219">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en Domo.</span><span class="sxs-lookup"><span data-stu-id="bb446-219">The objective of this section is to create a user called Britta Simon in Domo.</span></span> <span data-ttu-id="bb446-220">Domo admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="bb446-220">Domo supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="bb446-221">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="bb446-221">There is no action item for you in this section.</span></span> <span data-ttu-id="bb446-222">Al intentar acceder a Domo, se crea un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="bb446-222">A new user is created during an attempt to access Domo if it doesn't exist yet.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bb446-223">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb446-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bb446-224">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Domo.</span><span class="sxs-lookup"><span data-stu-id="bb446-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Domo.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="bb446-226">**Para asignar a Britta Simon a Domo, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="bb446-226">**To assign Britta Simon to Domo, perform the following steps:**</span></span>

1. <span data-ttu-id="bb446-227">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bb446-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="bb446-229">En la lista de aplicaciones, seleccione **Domo**.</span><span class="sxs-lookup"><span data-stu-id="bb446-229">In the applications list, select **Domo**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-domo-tutorial/tutorial_domo_app.png) 

3. <span data-ttu-id="bb446-231">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bb446-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="bb446-233">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="bb446-233">Click **Add** button.</span></span> <span data-ttu-id="bb446-234">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bb446-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="bb446-236">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="bb446-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bb446-237">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bb446-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bb446-238">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bb446-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bb446-239">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="bb446-239">Testing single sign-on</span></span>

<span data-ttu-id="bb446-240">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="bb446-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="bb446-241">Al hacer clic en el icono de Domo en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Domo.</span><span class="sxs-lookup"><span data-stu-id="bb446-241">When you click the Domo tile in the Access Panel, you should get automatically signed-on to your Domo application.</span></span>

<span data-ttu-id="bb446-242">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bb446-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bb446-243">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="bb446-243">Additional resources</span></span>

* [<span data-ttu-id="bb446-244">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb446-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bb446-245">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bb446-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-domo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-domo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-domo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-domo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-domo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-domo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-domo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-domo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-domo-tutorial/tutorial_general_203.png

