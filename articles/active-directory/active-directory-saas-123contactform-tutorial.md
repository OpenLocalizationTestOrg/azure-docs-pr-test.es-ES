---
title: "Tutorial: Integración de Azure Active Directory con 123ContactForm | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y 123ContactForm."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3a99f0841c3e0d973168991f5dbee40e54c1d054
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a><span data-ttu-id="9efbd-103">Tutorial: integración de Azure Active Directory con 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="9efbd-103">Tutorial: Azure Active Directory integration with 123ContactForm</span></span>

<span data-ttu-id="9efbd-104">En este tutorial, obtendrá información sobre cómo integrar 123ContactForm con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9efbd-104">In this tutorial, you learn how to integrate 123ContactForm with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9efbd-105">La integración de 123ContactForm con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9efbd-105">Integrating 123ContactForm with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9efbd-106">Puede controlar en Azure AD quién tiene acceso a 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="9efbd-106">You can control in Azure AD who has access to 123ContactForm</span></span>
- <span data-ttu-id="9efbd-107">Puede permitir que los usuarios inicien sesión automáticamente en 123ContactForm (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9efbd-107">You can enable your users to automatically get signed-on to 123ContactForm (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9efbd-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9efbd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9efbd-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9efbd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9efbd-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9efbd-110">Prerequisites</span></span>

<span data-ttu-id="9efbd-111">Para configurar la integración de Azure AD con 123ContactForm, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9efbd-111">To configure Azure AD integration with 123ContactForm, you need the following items:</span></span>

- <span data-ttu-id="9efbd-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9efbd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9efbd-113">Una suscripción habilitada para el inicio de sesión único en 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="9efbd-113">A 123ContactForm single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9efbd-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9efbd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9efbd-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9efbd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9efbd-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9efbd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9efbd-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9efbd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9efbd-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9efbd-118">Scenario description</span></span>
<span data-ttu-id="9efbd-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9efbd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9efbd-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="9efbd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9efbd-121">Agregar 123ContactForm desde la galería</span><span class="sxs-lookup"><span data-stu-id="9efbd-121">Adding 123ContactForm from the gallery</span></span>
2. <span data-ttu-id="9efbd-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9efbd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-123contactform-from-the-gallery"></a><span data-ttu-id="9efbd-123">Agregar 123ContactForm desde la galería</span><span class="sxs-lookup"><span data-stu-id="9efbd-123">Adding 123ContactForm from the gallery</span></span>
<span data-ttu-id="9efbd-124">Para configurar la integración de 123ContactForm en Azure AD, será preciso que agregue 123ContactForm desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="9efbd-124">To configure the integration of 123ContactForm into Azure AD, you need to add 123ContactForm from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9efbd-125">**Para agregar 123ContactForm desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9efbd-125">**To add 123ContactForm from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9efbd-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9efbd-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9efbd-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9efbd-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9efbd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9efbd-133">En el cuadro de búsqueda, escriba **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-133">In the search box, type **123ContactForm**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. <span data-ttu-id="9efbd-135">En el panel de resultados, seleccione **123ContactForm** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9efbd-135">In the results panel, select **123ContactForm**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9efbd-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9efbd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9efbd-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con 123ContactForm con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9efbd-138">In this section, you configure and test Azure AD single sign-on with 123ContactForm based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9efbd-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de 123ContactForm para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9efbd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 123ContactForm is to a user in Azure AD.</span></span> <span data-ttu-id="9efbd-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="9efbd-140">In other words, a link relationship between an Azure AD user and the related user in 123ContactForm needs to be established.</span></span>

<span data-ttu-id="9efbd-141">Para establecer la relación de vínculo, en 123ContactForm, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-141">In 123ContactForm, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9efbd-142">Para configurar y probar el inicio de sesión único de Azure AD con 123ContactForm, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9efbd-142">To configure and test Azure AD single sign-on with 123ContactForm, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9efbd-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="9efbd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9efbd-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9efbd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9efbd-145">**[Creación de un usuario de prueba de 123ContactForm](#creating-a-123contactform-test-user)**: para tener un homólogo de Britta Simon en 123ContactForm que esté vinculado a la representación de Azure AD de usuario.</span><span class="sxs-lookup"><span data-stu-id="9efbd-145">**[Creating a 123ContactForm test user](#creating-a-123contactform-test-user)** - to have a counterpart of Britta Simon in 123ContactForm that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9efbd-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9efbd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9efbd-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9efbd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9efbd-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9efbd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9efbd-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="9efbd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 123ContactForm application.</span></span>

<span data-ttu-id="9efbd-150">**Para configurar el inicio de sesión único de Azure AD con 123ContactForm, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9efbd-150">**To configure Azure AD single sign-on with 123ContactForm, perform the following steps:**</span></span>

1. <span data-ttu-id="9efbd-151">En Azure Portal, en la página de integración de la aplicación **123ContactForm**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-151">In the Azure portal, on the **123ContactForm** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9efbd-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9efbd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. <span data-ttu-id="9efbd-155">En la sección **Dominio y direcciones URL de 123ContactForm**, si quiere configurar la aplicación en el **modo iniciado por IDP**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9efbd-155">On the **123ContactForm Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-123contactform-tutorial/url1.png)

    <span data-ttu-id="9efbd-157">a.</span><span class="sxs-lookup"><span data-stu-id="9efbd-157">a.</span></span> <span data-ttu-id="9efbd-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span><span class="sxs-lookup"><span data-stu-id="9efbd-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span></span>

    <span data-ttu-id="9efbd-159">b.</span><span class="sxs-lookup"><span data-stu-id="9efbd-159">b.</span></span> <span data-ttu-id="9efbd-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`.</span><span class="sxs-lookup"><span data-stu-id="9efbd-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span></span>

4. <span data-ttu-id="9efbd-161">Si quiere configurar la aplicación en **modo iniciado por SP**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9efbd-161">If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-123contactform-tutorial/url2.png)

    <span data-ttu-id="9efbd-163">a.</span><span class="sxs-lookup"><span data-stu-id="9efbd-163">a.</span></span> <span data-ttu-id="9efbd-164">Haga clic en la opción **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-164">Click the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="9efbd-165">b.</span><span class="sxs-lookup"><span data-stu-id="9efbd-165">b.</span></span> <span data-ttu-id="9efbd-166">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL como: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span><span class="sxs-lookup"><span data-stu-id="9efbd-166">In the **Sign On URL** textbox, type a URL as: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9efbd-167">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="9efbd-167">These values are not real.</span></span> <span data-ttu-id="9efbd-168">Debe actualizar este valor con las direcciones URL y el identificador reales, como se explica más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="9efbd-168">You'll need to update these value from actual URLs and Identifier which is explained later in the tutorial.</span></span>
    
5. <span data-ttu-id="9efbd-169">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9efbd-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. <span data-ttu-id="9efbd-171">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9efbd-171">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="9efbd-173">Para configurar el inicio de sesión único en **123ContactForm**, vaya a [https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) y realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9efbd-173">To configure single sign-on on **123ContactForm** side, go to [https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) and perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    <span data-ttu-id="9efbd-175">a.</span><span class="sxs-lookup"><span data-stu-id="9efbd-175">a.</span></span> <span data-ttu-id="9efbd-176">En el cuadro de texto **Correo electrónico**, escriba el correo electrónico del usuario, es decir,</span><span class="sxs-lookup"><span data-stu-id="9efbd-176">In the **Email** textbox, type the email of the user i.e</span></span> <span data-ttu-id="9efbd-177">**BrittaSimon@Contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-177">**BrittaSimon@Contoso.com**.</span></span>

    <span data-ttu-id="9efbd-178">b.</span><span class="sxs-lookup"><span data-stu-id="9efbd-178">b.</span></span> <span data-ttu-id="9efbd-179">Haga clic en **Cargar** y vaya al archivo XML de metadatos que ha descargado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9efbd-179">Click **Upload** and browse the Metadata XML file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="9efbd-180">c.</span><span class="sxs-lookup"><span data-stu-id="9efbd-180">c.</span></span> <span data-ttu-id="9efbd-181">Haga clic en **ENVIAR FORMULARIO**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-181">Click **SUBMIT FORM**.</span></span>

8. <span data-ttu-id="9efbd-182">En **Microsoft Azure AD - Inicio de sesión único - Configurar las opciones de la aplicación**, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9efbd-182">On the **Microsoft Azure AD - Single sign-on - Configure App Settings** perform the following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-123contactform-tutorial/url3.png)

    <span data-ttu-id="9efbd-184">a.</span><span class="sxs-lookup"><span data-stu-id="9efbd-184">a.</span></span> <span data-ttu-id="9efbd-185">Si quiere configurar la aplicación en **modo iniciado por IDP**, copie el valor de **IDENTIFICADOR** de la instancia y péguelo en el cuadro de texto **Identificador** en la sección **Dominio y direcciones URL de 123ContactForm** en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9efbd-185">If you wish to configure the application in **IDP initiated mode**, copy the **IDENTIFIER** value for your instance and paste it in **Identifier** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="9efbd-186">b.</span><span class="sxs-lookup"><span data-stu-id="9efbd-186">b.</span></span> <span data-ttu-id="9efbd-187">Si quiere configurar la aplicación en **modo iniciado por IDP**, copie el valor de **URL DE RESPUESTA** de la instancia y péguelo en el cuadro de texto **URL de respuesta** en la sección **Dominio y direcciones URL de 123ContactForm** en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9efbd-187">If you wish to configure the application in **IDP initiated mode**, copy the **REPLY URL** value for your instance and paste it in **Reply URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="9efbd-188">c.</span><span class="sxs-lookup"><span data-stu-id="9efbd-188">c.</span></span> <span data-ttu-id="9efbd-189">Si quiere configurar la aplicación en **modo iniciado por SP**, copie el valor de **URL de inicio de sesión** de la instancia y péguelo en el cuadro de texto **URL de inicio de sesión** en la sección **Dominio y direcciones URL de 123ContactForm** en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9efbd-189">If you wish to configure the application in **SP initiated mode**, copy the **SIGN ON URL** value for your instance and paste it in **Sign On URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="9efbd-190">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9efbd-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9efbd-191">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="9efbd-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9efbd-192">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9efbd-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9efbd-193">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9efbd-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="9efbd-194">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9efbd-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9efbd-196">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="9efbd-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9efbd-197">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9efbd-199">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9efbd-201">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9efbd-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9efbd-203">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9efbd-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9efbd-205">a.</span><span class="sxs-lookup"><span data-stu-id="9efbd-205">a.</span></span> <span data-ttu-id="9efbd-206">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9efbd-207">b.</span><span class="sxs-lookup"><span data-stu-id="9efbd-207">b.</span></span> <span data-ttu-id="9efbd-208">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9efbd-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9efbd-209">c.</span><span class="sxs-lookup"><span data-stu-id="9efbd-209">c.</span></span> <span data-ttu-id="9efbd-210">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9efbd-211">d.</span><span class="sxs-lookup"><span data-stu-id="9efbd-211">d.</span></span> <span data-ttu-id="9efbd-212">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-212">Click **Create**.</span></span>
 
### <a name="creating-a-123contactform-test-user"></a><span data-ttu-id="9efbd-213">Crear un usuario de prueba de 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="9efbd-213">Creating a 123ContactForm test user</span></span>

<span data-ttu-id="9efbd-214">La aplicación admite aprovisionamiento de usuarios Just-In-Time y, tras la autenticación, los usuarios se crearán automáticamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9efbd-214">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9efbd-215">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9efbd-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9efbd-216">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="9efbd-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 123ContactForm.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9efbd-218">**Para asignar el usuario Britta Simon a 123ContactForm, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="9efbd-218">**To assign Britta Simon to 123ContactForm, perform the following steps:**</span></span>

1. <span data-ttu-id="9efbd-219">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9efbd-221">En la lista de aplicaciones, seleccione **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-221">In the applications list, select **123ContactForm**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. <span data-ttu-id="9efbd-223">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9efbd-225">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-225">Click **Add** button.</span></span> <span data-ttu-id="9efbd-226">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9efbd-228">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="9efbd-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9efbd-229">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9efbd-230">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9efbd-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9efbd-231">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9efbd-231">Testing single sign-on</span></span>

<span data-ttu-id="9efbd-232">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9efbd-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9efbd-233">Al hacer clic en el icono de 123ContactForm en el Panel de acceso, debería iniciar sesión automáticamente en la aplicación 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="9efbd-233">When you click the 123ContactForm tile in the Access Panel, you should get automatically signed-on to your 123ContactForm application.</span></span>
<span data-ttu-id="9efbd-234">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9efbd-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9efbd-235">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9efbd-235">Additional resources</span></span>

* [<span data-ttu-id="9efbd-236">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9efbd-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9efbd-237">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9efbd-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png

