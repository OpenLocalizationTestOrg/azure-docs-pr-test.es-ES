---
title: "Tutorial: Integración de Azure Active Directory con CA PPM | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y CA PPM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca9d5e71-e429-4891-8d10-3498e7210e89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 4ca9268c26f681fcc96955b6161fe4a119b2dcf4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ca-ppm"></a><span data-ttu-id="8d897-103">Tutorial: Integración de Azure Active Directory con CA PPM</span><span class="sxs-lookup"><span data-stu-id="8d897-103">Tutorial: Azure Active Directory integration with CA PPM</span></span>

<span data-ttu-id="8d897-104">En este tutorial, obtendrá información sobre cómo integrar CA PPM con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8d897-104">In this tutorial, you learn how to integrate CA PPM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d897-105">Integrar CA PPM con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="8d897-105">Integrating CA PPM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8d897-106">Puede controlar en Azure AD quién tiene acceso a CA PPM</span><span class="sxs-lookup"><span data-stu-id="8d897-106">You can control in Azure AD who has access to CA PPM</span></span>
- <span data-ttu-id="8d897-107">Puede permitir que los usuarios inicien sesión automáticamente en CA PPM (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d897-107">You can enable your users to automatically get signed-on to CA PPM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8d897-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="8d897-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8d897-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8d897-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d897-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8d897-110">Prerequisites</span></span>

<span data-ttu-id="8d897-111">Para configurar la integración de Azure AD con CA PPM, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8d897-111">To configure Azure AD integration with CA PPM, you need the following items:</span></span>

- <span data-ttu-id="8d897-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d897-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d897-113">Una suscripción habilitada para el inicio de sesión único en CA PPM</span><span class="sxs-lookup"><span data-stu-id="8d897-113">A CA PPM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d897-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="8d897-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d897-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="8d897-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d897-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8d897-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d897-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d897-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d897-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="8d897-118">Scenario description</span></span>
<span data-ttu-id="8d897-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="8d897-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d897-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="8d897-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d897-121">Incorporación de CA PPM desde la galería</span><span class="sxs-lookup"><span data-stu-id="8d897-121">Adding CA PPM from the gallery</span></span>
2. <span data-ttu-id="8d897-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d897-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ca-ppm-from-the-gallery"></a><span data-ttu-id="8d897-123">Incorporación de CA PPM desde la galería</span><span class="sxs-lookup"><span data-stu-id="8d897-123">Adding CA PPM from the gallery</span></span>
<span data-ttu-id="8d897-124">Para configurar la integración de CA PPM en Azure AD, deberá agregar CA PPM desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="8d897-124">To configure the integration of CA PPM into Azure AD, you need to add CA PPM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8d897-125">**Para agregar CA PPM desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="8d897-125">**To add CA PPM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8d897-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8d897-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8d897-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="8d897-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8d897-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8d897-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="8d897-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8d897-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="8d897-133">En el cuadro de búsqueda, escriba **CA PPM**.</span><span class="sxs-lookup"><span data-stu-id="8d897-133">In the search box, type **CA PPM**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_search.png)

5. <span data-ttu-id="8d897-135">En el panel de resultados, seleccione **CA PPM** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8d897-135">In the results panel, select **CA PPM**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8d897-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d897-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8d897-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con CA PPM con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8d897-138">In this section, you configure and test Azure AD single sign-on with CA PPM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8d897-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de CA PPM para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d897-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CA PPM is to a user in Azure AD.</span></span> <span data-ttu-id="8d897-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de CA PPM.</span><span class="sxs-lookup"><span data-stu-id="8d897-140">In other words, a link relationship between an Azure AD user and the related user in CA PPM needs to be established.</span></span>

<span data-ttu-id="8d897-141">Para establecer la relación de vínculo, en CA PPM, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="8d897-141">In CA PPM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8d897-142">Para configurar y probar el inicio de sesión único de Azure AD con CA PPM, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="8d897-142">To configure and test Azure AD single sign-on with CA PPM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8d897-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="8d897-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8d897-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d897-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8d897-145">**[Creación de un usuario de prueba de CA PPM](#creating-a-ca-ppm-test-user)**: para tener un homólogo de Britta Simon en CA PPM que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d897-145">**[Creating a CA PPM test user](#creating-a-ca-ppm-test-user)** - to have a counterpart of Britta Simon in CA PPM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8d897-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d897-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8d897-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="8d897-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8d897-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d897-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8d897-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación CA PPM.</span><span class="sxs-lookup"><span data-stu-id="8d897-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CA PPM application.</span></span>

<span data-ttu-id="8d897-150">**Para configurar el inicio de sesión único de Azure AD con CA PPM, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="8d897-150">**To configure Azure AD single sign-on with CA PPM, perform the following steps:**</span></span>

1. <span data-ttu-id="8d897-151">En Azure Portal, en la página de integración de la aplicación **CA PPM**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="8d897-151">In the Azure portal, on the **CA PPM** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="8d897-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8d897-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_samlbase.png)

3. <span data-ttu-id="8d897-155">En la sección **Dominio y direcciones URL de CA PPM**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8d897-155">On the **CA PPM Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_url.png)

    <span data-ttu-id="8d897-157">a.</span><span class="sxs-lookup"><span data-stu-id="8d897-157">a.</span></span> <span data-ttu-id="8d897-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://ca.ondemand.saml.20.post.<companyname>`</span><span class="sxs-lookup"><span data-stu-id="8d897-158">In the **Identifier** textbox, type a URL using the following pattern: `https://ca.ondemand.saml.20.post.<companyname>`</span></span>
    
    <span data-ttu-id="8d897-159">b.</span><span class="sxs-lookup"><span data-stu-id="8d897-159">b.</span></span> <span data-ttu-id="8d897-160">En el cuadro de texto **URL de respuesta**, escriba: `https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="8d897-160">In the **Reply URL** textbox, type as: `https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8d897-161">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="8d897-161">This value is not real.</span></span> <span data-ttu-id="8d897-162">Actualícelo con el identificador real.</span><span class="sxs-lookup"><span data-stu-id="8d897-162">Update this value with the actual Identifier.</span></span> <span data-ttu-id="8d897-163">Póngase en contacto con el [equipo de soporte técnico de CA PPM](mailto:catechnicalsupport@ca.com) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="8d897-163">Contact [CA PPM support team](mailto:catechnicalsupport@ca.com) to get this value.</span></span>
 
4. <span data-ttu-id="8d897-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8d897-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_certificate.png) 

5. <span data-ttu-id="8d897-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="8d897-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cappm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8d897-168">En la sección **Configuración de CA PPM**, haga clic en **Configurar CA PPM** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="8d897-168">On the **CA PPM Configuration** section, click **Configure CA PPM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8d897-169">Copie el **identificador de entidad de SAML** de la **sección de referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="8d897-169">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_configure.png) 

7. <span data-ttu-id="8d897-171">Para configurar el inicio de sesión único en **CA PPM**, debe enviar el **certificado (Base64)** descargado y el **identificador de entidad de SAML** al [equipo de soporte técnico de CA PPM](mailto:catechnicalsupport@ca.com).</span><span class="sxs-lookup"><span data-stu-id="8d897-171">To configure single sign-on on **CA PPM** side, you need to send the downloaded **Certificate(Base64)** and **SAML Entity ID** to [CA PPM support team](mailto:catechnicalsupport@ca.com).</span></span>

> [!TIP]
> <span data-ttu-id="8d897-172">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8d897-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8d897-173">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="8d897-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8d897-174">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8d897-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8d897-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d897-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="8d897-176">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8d897-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="8d897-178">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="8d897-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8d897-179">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8d897-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8d897-181">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="8d897-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8d897-183">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8d897-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8d897-185">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="8d897-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d897-187">a.</span><span class="sxs-lookup"><span data-stu-id="8d897-187">a.</span></span> <span data-ttu-id="8d897-188">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8d897-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d897-189">b.</span><span class="sxs-lookup"><span data-stu-id="8d897-189">b.</span></span> <span data-ttu-id="8d897-190">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d897-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8d897-191">c.</span><span class="sxs-lookup"><span data-stu-id="8d897-191">c.</span></span> <span data-ttu-id="8d897-192">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="8d897-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8d897-193">d.</span><span class="sxs-lookup"><span data-stu-id="8d897-193">d.</span></span> <span data-ttu-id="8d897-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8d897-194">Click **Create**.</span></span>
 
### <a name="creating-a-ca-ppm-test-user"></a><span data-ttu-id="8d897-195">Creación de un usuario de prueba de CA PPM</span><span class="sxs-lookup"><span data-stu-id="8d897-195">Creating a CA PPM test user</span></span>

<span data-ttu-id="8d897-196">En esta sección, creará un usuario llamado Britta Simon en CA PPM.</span><span class="sxs-lookup"><span data-stu-id="8d897-196">In this section, you create a user called Britta Simon in CA PPM.</span></span> <span data-ttu-id="8d897-197">Colabore con el [equipo de soporte técnico de CA PPM](mailto:catechnicalsupport@ca.com) para agregar los usuarios en la plataforma de CA PPM.</span><span class="sxs-lookup"><span data-stu-id="8d897-197">Work with [CA PPM support team](mailto:catechnicalsupport@ca.com) to add the users in the CA PPM platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8d897-198">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d897-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8d897-199">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a CA PPM.</span><span class="sxs-lookup"><span data-stu-id="8d897-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CA PPM.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="8d897-201">**Para asignar a Britta Simon a CA PPM, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="8d897-201">**To assign Britta Simon to CA PPM, perform the following steps:**</span></span>

1. <span data-ttu-id="8d897-202">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8d897-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="8d897-204">En la lista de aplicaciones, seleccione **CA PPM**.</span><span class="sxs-lookup"><span data-stu-id="8d897-204">In the applications list, select **CA PPM**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_app.png) 

3. <span data-ttu-id="8d897-206">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8d897-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="8d897-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8d897-208">Click **Add** button.</span></span> <span data-ttu-id="8d897-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8d897-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="8d897-211">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="8d897-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8d897-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8d897-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8d897-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8d897-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8d897-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="8d897-214">Testing single sign-on</span></span>

<span data-ttu-id="8d897-215">En esta sección, probará la configuración de SSO de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="8d897-215">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8d897-216">Al hacer clic en el icono de CA PPM en el panel de acceso, debería iniciar sesión automáticamente en su aplicación CA PPM.</span><span class="sxs-lookup"><span data-stu-id="8d897-216">When you click the CA PPM tile in the Access Panel, you should get automatically signed-on to your CA PPM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8d897-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8d897-217">Additional resources</span></span>

* [<span data-ttu-id="8d897-218">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d897-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8d897-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8d897-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_203.png

