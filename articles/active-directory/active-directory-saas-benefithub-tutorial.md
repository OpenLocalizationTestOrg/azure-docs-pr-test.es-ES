---
title: "Tutorial: Integración de Azure Active Directory con BenefitHub | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y BenefitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4069fe32-a452-463f-973e-7aa0baa4c2fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 8df9c0d8443d6685253207ed1915c780275014fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefithub"></a><span data-ttu-id="fd438-103">Tutorial: Integración de Azure Active Directory con BenefitHub</span><span class="sxs-lookup"><span data-stu-id="fd438-103">Tutorial: Azure Active Directory integration with BenefitHub</span></span>

<span data-ttu-id="fd438-104">En este tutorial, obtendrá información sobre cómo integrar BenefitHub con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fd438-104">In this tutorial, you learn how to integrate BenefitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fd438-105">Integrar BenefitHub con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="fd438-105">Integrating BenefitHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fd438-106">En Azure AD se puede controlar quién tiene acceso a BenefitHub</span><span class="sxs-lookup"><span data-stu-id="fd438-106">You can control in Azure AD who has access to BenefitHub</span></span>
- <span data-ttu-id="fd438-107">Puede permitir que los usuarios inicien sesión automáticamente en BenefitHub (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd438-107">You can enable your users to automatically get signed-on to BenefitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fd438-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fd438-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fd438-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fd438-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd438-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fd438-110">Prerequisites</span></span>

<span data-ttu-id="fd438-111">Para configurar la integración de Azure AD con BenefitHub, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="fd438-111">To configure Azure AD integration with BenefitHub, you need the following items:</span></span>

- <span data-ttu-id="fd438-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd438-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fd438-113">Una suscripción habilitada para el inicio de sesión único en BenefitHub</span><span class="sxs-lookup"><span data-stu-id="fd438-113">A BenefitHub single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fd438-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="fd438-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fd438-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="fd438-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fd438-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="fd438-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fd438-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fd438-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fd438-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="fd438-118">Scenario description</span></span>
<span data-ttu-id="fd438-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="fd438-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fd438-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="fd438-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fd438-121">Agregar BenefitHub desde la galería</span><span class="sxs-lookup"><span data-stu-id="fd438-121">Adding BenefitHub from the gallery</span></span>
2. <span data-ttu-id="fd438-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd438-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benefithub-from-the-gallery"></a><span data-ttu-id="fd438-123">Agregar BenefitHub desde la galería</span><span class="sxs-lookup"><span data-stu-id="fd438-123">Adding BenefitHub from the gallery</span></span>
<span data-ttu-id="fd438-124">Para configurar la integración de BenefitHub en Azure AD, deberá agregar BenefitHub desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="fd438-124">To configure the integration of BenefitHub into Azure AD, you need to add BenefitHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fd438-125">**Para agregar BenefitHub desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="fd438-125">**To add BenefitHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fd438-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fd438-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fd438-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="fd438-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fd438-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fd438-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="fd438-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fd438-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="fd438-133">En el cuadro de búsqueda, escriba **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="fd438-133">In the search box, type **BenefitHub**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_search.png)

5. <span data-ttu-id="fd438-135">En el panel de resultados, seleccione **BenefitHub** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fd438-135">In the results panel, select **BenefitHub**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fd438-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd438-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fd438-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con BenefitHub con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fd438-138">In this section, you configure and test Azure AD single sign-on with BenefitHub based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fd438-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de BenefitHub para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd438-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenefitHub is to a user in Azure AD.</span></span> <span data-ttu-id="fd438-140">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="fd438-140">In other words, a link relationship between an Azure AD user and the related user in BenefitHub needs to be established.</span></span>

<span data-ttu-id="fd438-141">Para establecer la relación de vínculo, en BenefitHub, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="fd438-141">In BenefitHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fd438-142">Para configurar y probar el inicio de sesión único de Azure AD con BenefitHub, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="fd438-142">To configure and test Azure AD single sign-on with BenefitHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fd438-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="fd438-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fd438-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fd438-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fd438-145">**[Creación de un usuario de prueba de BenefitHub](#creating-a-benefithub-test-user)**: para tener un homólogo de Britta Simon en LBenefitHub que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd438-145">**[Creating a BenefitHub test user](#creating-a-benefithub-test-user)** - to have a counterpart of Britta Simon in BenefitHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fd438-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd438-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fd438-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="fd438-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fd438-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd438-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fd438-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="fd438-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenefitHub application.</span></span>

<span data-ttu-id="fd438-150">**Para configurar el inicio de sesión único de Azure AD con BenefitHub, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="fd438-150">**To configure Azure AD single sign-on with BenefitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="fd438-151">En Azure Portal, en la página de integración de la aplicación **BenefitHub**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="fd438-151">In the Azure portal, on the **BenefitHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="fd438-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fd438-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_samlbase.png)

3. <span data-ttu-id="fd438-155">En la sección de **Dominio y direcciones URL de BenefitHub**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="fd438-155">On the **BenefitHub Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_url1.png)
  
    <span data-ttu-id="fd438-157">a.</span><span class="sxs-lookup"><span data-stu-id="fd438-157">a.</span></span> <span data-ttu-id="fd438-158">En el cuadro de texto **Identificador**, escriba: `urn:benefithub:passport`</span><span class="sxs-lookup"><span data-stu-id="fd438-158">In the **Identifier** textbox, type: `urn:benefithub:passport`</span></span>
    
    <span data-ttu-id="fd438-159">b.</span><span class="sxs-lookup"><span data-stu-id="fd438-159">b.</span></span> <span data-ttu-id="fd438-160">En el cuadro de texto **URL de respuesta**, escriba: `https://passport.benefithub.info/saml/post/ac`</span><span class="sxs-lookup"><span data-stu-id="fd438-160">In the **Reply URL** textbox, type: `https://passport.benefithub.info/saml/post/ac`</span></span>

4. <span data-ttu-id="fd438-161">La aplicación BenefitHub espera las aserciones de SAML en un formato específico, que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los atributos del token de SAML.</span><span class="sxs-lookup"><span data-stu-id="fd438-161">The BenefitHub application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="fd438-162">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="fd438-162">Configure the following claims for this application.</span></span> <span data-ttu-id="fd438-163">Puede administrar los valores de estos atributos en la sección "**Atributos de usuario**" de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="fd438-163">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_attribute.png)

5. <span data-ttu-id="fd438-165">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo del token de SAML como muestra la imagen anterior y realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="fd438-165">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="fd438-166">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="fd438-166">Attribute Name</span></span> | <span data-ttu-id="fd438-167">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="fd438-167">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="fd438-168">organizationid</span><span class="sxs-lookup"><span data-stu-id="fd438-168">organizationid</span></span> | <span data-ttu-id="fd438-169">< identificador de organización ></span><span class="sxs-lookup"><span data-stu-id="fd438-169">< organizationid ></span></span> |

    > [!NOTE]
    > <span data-ttu-id="fd438-170">Este valor de atributo no es real.</span><span class="sxs-lookup"><span data-stu-id="fd438-170">This attribute value is not real.</span></span> <span data-ttu-id="fd438-171">Actualícelo con el identificador de organización real.</span><span class="sxs-lookup"><span data-stu-id="fd438-171">Update this value with actual organizationid.</span></span> <span data-ttu-id="fd438-172">Póngase en contacto con el [equipo de soporte técnico de BenefitHub](https://www.benefithub.com/Home/ContactUs) para obtener el identificador real.</span><span class="sxs-lookup"><span data-stu-id="fd438-172">Contact [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to get the actual organizationid.</span></span>
    
    <span data-ttu-id="fd438-173">a.</span><span class="sxs-lookup"><span data-stu-id="fd438-173">a.</span></span> <span data-ttu-id="fd438-174">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="fd438-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="fd438-177">b.</span><span class="sxs-lookup"><span data-stu-id="fd438-177">b.</span></span> <span data-ttu-id="fd438-178">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="fd438-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="fd438-179">c.</span><span class="sxs-lookup"><span data-stu-id="fd438-179">c.</span></span> <span data-ttu-id="fd438-180">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="fd438-180">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="fd438-181">d.</span><span class="sxs-lookup"><span data-stu-id="fd438-181">d.</span></span> <span data-ttu-id="fd438-182">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fd438-182">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fd438-183">Antes de configurar la aserción SAML, debe ponerse en contacto con el [equipo de soporte técnico de BenefitHub](https://www.benefithub.com/Home/ContactUs) y solicitar el valor del atributo de identificador único para el inquilino.</span><span class="sxs-lookup"><span data-stu-id="fd438-183">Before you can configure the SAML assertion, you need to contact your [BenefitHub support](https://www.benefithub.com/Home/ContactUs) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="fd438-184">Necesitará este valor para configurar la notificación personalizada para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="fd438-184">You need this value to configure the custom claim for your application.</span></span>

6. <span data-ttu-id="fd438-185">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="fd438-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_certificate.png) 

7. <span data-ttu-id="fd438-187">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="fd438-187">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benefithub-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="fd438-189">Para configurar el inicio de sesión único en el lado de **BenefitHub**, es preciso enviar los datos descargados de **XML de metadatos** al [equipo de soporte técnico de BenefitHub](https://www.benefithub.com/Home/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="fd438-189">To configure single sign-on on **BenefitHub** side, you need to send the downloaded **Metadata XML** to [BenefitHub support team](https://www.benefithub.com/Home/ContactUs).</span></span> <span data-ttu-id="fd438-190">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="fd438-190">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="fd438-191">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fd438-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fd438-192">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="fd438-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fd438-193">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fd438-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fd438-194">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd438-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="fd438-195">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fd438-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="fd438-197">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="fd438-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fd438-198">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fd438-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fd438-200">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fd438-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fd438-202">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fd438-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fd438-204">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="fd438-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fd438-206">a.</span><span class="sxs-lookup"><span data-stu-id="fd438-206">a.</span></span> <span data-ttu-id="fd438-207">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fd438-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fd438-208">b.</span><span class="sxs-lookup"><span data-stu-id="fd438-208">b.</span></span> <span data-ttu-id="fd438-209">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fd438-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fd438-210">c.</span><span class="sxs-lookup"><span data-stu-id="fd438-210">c.</span></span> <span data-ttu-id="fd438-211">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="fd438-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fd438-212">d.</span><span class="sxs-lookup"><span data-stu-id="fd438-212">d.</span></span> <span data-ttu-id="fd438-213">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fd438-213">Click **Create**.</span></span>
 
### <a name="creating-a-benefithub-test-user"></a><span data-ttu-id="fd438-214">Creación de un usuario de prueba de BenefitHub</span><span class="sxs-lookup"><span data-stu-id="fd438-214">Creating a BenefitHub test user</span></span>

<span data-ttu-id="fd438-215">En esta sección, creará un usuario llamado Britta Simon en BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="fd438-215">In this section, you create a user called Britta Simon in BenefitHub.</span></span> <span data-ttu-id="fd438-216">Trabaje con el [equipo de soporte técnico de BenefitHub](https://www.benefithub.com/Home/ContactUs) para agregar usuarios a la plataforma de BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="fd438-216">Work with [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to add the users in the BenefitHub platform.</span></span> <span data-ttu-id="fd438-217">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fd438-217">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fd438-218">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd438-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fd438-219">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="fd438-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenefitHub.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="fd438-221">**Para asignar a Britta Simon a BenefitHub, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="fd438-221">**To assign Britta Simon to BenefitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="fd438-222">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fd438-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="fd438-224">En la lista de aplicaciones, seleccione **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="fd438-224">In the applications list, select **BenefitHub**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_app.png) 

3. <span data-ttu-id="fd438-226">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fd438-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="fd438-228">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fd438-228">Click **Add** button.</span></span> <span data-ttu-id="fd438-229">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fd438-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="fd438-231">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="fd438-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fd438-232">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fd438-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fd438-233">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fd438-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fd438-234">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="fd438-234">Testing single sign-on</span></span>

<span data-ttu-id="fd438-235">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="fd438-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fd438-236">Al hacer clic en el icono de BenefitHub en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="fd438-236">When you click the BenefitHub tile in the Access Panel, you should get automatically signed-on to your BenefitHub application.</span></span>
<span data-ttu-id="fd438-237">Para más información sobre el Panel de acceso, vea la [introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="fd438-237">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fd438-238">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="fd438-238">Additional resources</span></span>

* [<span data-ttu-id="fd438-239">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fd438-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fd438-240">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fd438-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_203.png
