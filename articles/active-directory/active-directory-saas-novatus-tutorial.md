---
title: "Tutorial: Integración de Azure Active Directory con Novatus | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Novatus."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2f13779-bdb7-4408-9738-be67ed3de4e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: jeedes
ms.openlocfilehash: ec67e96309a8877e6fb65b30da1501e4f34a9ee4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-novatus"></a><span data-ttu-id="fef12-103">Tutorial: integración de Azure Active Directory con Novatus</span><span class="sxs-lookup"><span data-stu-id="fef12-103">Tutorial: Azure Active Directory integration with Novatus</span></span>

<span data-ttu-id="fef12-104">En este tutorial, aprenderá a integrar Novatus con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fef12-104">In this tutorial, you learn how to integrate Novatus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fef12-105">La integración de Novatus con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="fef12-105">Integrating Novatus with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fef12-106">Puede controlar en Azure AD quién tiene acceso a Novatus.</span><span class="sxs-lookup"><span data-stu-id="fef12-106">You can control in Azure AD who has access to Novatus</span></span>
- <span data-ttu-id="fef12-107">Puede permitir que los usuarios inicien sesión automáticamente en Novatus (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fef12-107">You can enable your users to automatically get signed-on to Novatus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fef12-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fef12-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fef12-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fef12-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fef12-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fef12-110">Prerequisites</span></span>

<span data-ttu-id="fef12-111">Para configurar la integración de Azure AD con Novatus, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="fef12-111">To configure Azure AD integration with Novatus, you need the following items:</span></span>

- <span data-ttu-id="fef12-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fef12-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fef12-113">Una suscripción habilitada para el inicio de sesión único en Novatus</span><span class="sxs-lookup"><span data-stu-id="fef12-113">A Novatus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fef12-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="fef12-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fef12-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="fef12-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fef12-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="fef12-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fef12-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fef12-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fef12-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="fef12-118">Scenario description</span></span>
<span data-ttu-id="fef12-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="fef12-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fef12-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="fef12-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fef12-121">Adición de Novatus desde la galería</span><span class="sxs-lookup"><span data-stu-id="fef12-121">Adding Novatus from the gallery</span></span>
2. <span data-ttu-id="fef12-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fef12-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-novatus-from-the-gallery"></a><span data-ttu-id="fef12-123">Adición de Novatus desde la galería</span><span class="sxs-lookup"><span data-stu-id="fef12-123">Adding Novatus from the gallery</span></span>
<span data-ttu-id="fef12-124">Para configurar la integración de Novatus en Azure AD, será preciso que agregue Novatus desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="fef12-124">To configure the integration of Novatus into Azure AD, you need to add Novatus from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fef12-125">**Para agregar Novatus desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="fef12-125">**To add Novatus from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fef12-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fef12-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fef12-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="fef12-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fef12-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fef12-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="fef12-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fef12-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="fef12-133">En el cuadro de búsqueda, escriba **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="fef12-133">In the search box, type **Novatus**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_search.png)

5. <span data-ttu-id="fef12-135">En el panel de resultados, seleccione **Novatus** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fef12-135">In the results panel, select **Novatus**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fef12-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fef12-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fef12-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Novatus con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fef12-138">In this section, you configure and test Azure AD single sign-on with Novatus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fef12-139">Para que el inicio de sesión único funcione, Azure AD necesita saber cuál es el usuario homólogo de Novatus para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fef12-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Novatus is to a user in Azure AD.</span></span> <span data-ttu-id="fef12-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Novatus.</span><span class="sxs-lookup"><span data-stu-id="fef12-140">In other words, a link relationship between an Azure AD user and the related user in Novatus needs to be established.</span></span>

<span data-ttu-id="fef12-141">Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario** de Novatus.</span><span class="sxs-lookup"><span data-stu-id="fef12-141">In Novatus, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fef12-142">Para configurar y probar el inicio de sesión único de Azure AD con Novatus, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="fef12-142">To configure and test Azure AD single sign-on with Novatus, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fef12-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="fef12-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fef12-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fef12-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fef12-145">**[Creación de un usuario de prueba de Novatus](#creating-a-novatus-test-user)**: el objetivo es tener un homólogo de Britta Simon en Novatus que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fef12-145">**[Creating a Novatus test user](#creating-a-novatus-test-user)** - to have a counterpart of Britta Simon in Novatus that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fef12-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fef12-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fef12-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="fef12-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fef12-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fef12-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fef12-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Novatus.</span><span class="sxs-lookup"><span data-stu-id="fef12-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Novatus application.</span></span>

<span data-ttu-id="fef12-150">**Para configurar el inicio de sesión único de Azure AD con Novatus, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="fef12-150">**To configure Azure AD single sign-on with Novatus, perform the following steps:**</span></span>

1. <span data-ttu-id="fef12-151">En la página de integración de la aplicación **Novatus** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="fef12-151">In the Azure portal, on the **Novatus** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="fef12-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fef12-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_samlbase.png)

3. <span data-ttu-id="fef12-155">En la sección **Dominio y direcciones URL de Novatus**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="fef12-155">On the **Novatus Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_url.png)

     <span data-ttu-id="fef12-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://sso.novatuscontracts.com/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="fef12-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.novatuscontracts.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fef12-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="fef12-158">This value is not real.</span></span> <span data-ttu-id="fef12-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="fef12-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="fef12-160">Póngase en contacto con el [equipo de atención al cliente de Novatus](mailto:jvinci@novatusinc.com) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="fef12-160">Contact [Novatus Client support team](mailto:jvinci@novatusinc.com) to get this value.</span></span> 
 


4. <span data-ttu-id="fef12-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="fef12-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_certificate.png) 

5. <span data-ttu-id="fef12-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="fef12-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-novatus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fef12-165">En la sección **Configuración de Novatus**, haga clic en **Configurar Novatus** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="fef12-165">On the **Novatus Configuration** section, click **Configure Novatus** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fef12-166">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="fef12-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_configure.png) 

7. <span data-ttu-id="fef12-168">Para configurar el inicio de sesión único para su aplicación, póngase en contacto con el [equipo de soporte técnico de Novatus](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="fef12-168">To get SSO configured for your application, contact your [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> <span data-ttu-id="fef12-169">Adjunte el archivo de **certificado descargado** a su correo y comparta las **direcciones URL de metadatos** (**URL de cierre de sesión, identificador de entidad de SAML y dirección URL del servicio de inicio de sesión único de SAML**) con el equipo de Novatus para que le configuren el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fef12-169">Attach the **downloaded certificate** file to your mail and share the **metadata urls** (**Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL**) with Novatus team to set up SSO on their side.</span></span>

> [!TIP]
> <span data-ttu-id="fef12-170">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fef12-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fef12-171">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="fef12-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fef12-172">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fef12-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fef12-173">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fef12-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="fef12-174">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fef12-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="fef12-176">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="fef12-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fef12-177">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fef12-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fef12-179">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fef12-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fef12-181">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fef12-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fef12-183">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="fef12-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fef12-185">a.</span><span class="sxs-lookup"><span data-stu-id="fef12-185">a.</span></span> <span data-ttu-id="fef12-186">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fef12-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fef12-187">b.</span><span class="sxs-lookup"><span data-stu-id="fef12-187">b.</span></span> <span data-ttu-id="fef12-188">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fef12-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fef12-189">c.</span><span class="sxs-lookup"><span data-stu-id="fef12-189">c.</span></span> <span data-ttu-id="fef12-190">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="fef12-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fef12-191">d.</span><span class="sxs-lookup"><span data-stu-id="fef12-191">d.</span></span> <span data-ttu-id="fef12-192">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fef12-192">Click **Create**.</span></span>
 
### <a name="creating-a-novatus-test-user"></a><span data-ttu-id="fef12-193">Creación de un usuario de prueba de Novatus</span><span class="sxs-lookup"><span data-stu-id="fef12-193">Creating a Novatus test user</span></span>

<span data-ttu-id="fef12-194">El objetivo de esta sección es crear un usuario llamado Britta Simon en Novatus.</span><span class="sxs-lookup"><span data-stu-id="fef12-194">The objective of this section is to create a user called Britta Simon in Novatus.</span></span> <span data-ttu-id="fef12-195">Novatus admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="fef12-195">Novatus supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="fef12-196">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="fef12-196">There is no action item for you in this section.</span></span> <span data-ttu-id="fef12-197">Durante un intento de acceder a Novatus se creará un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="fef12-197">A new user will be created during an attempt to access Novatus if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="fef12-198">Si necesita crear manualmente un usuario, es preciso que se ponga contacto con el [equipo de soporte técnico de Novatus](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="fef12-198">If you need to create an user manually, you need to contact the [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fef12-199">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fef12-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fef12-200">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Novatus.</span><span class="sxs-lookup"><span data-stu-id="fef12-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Novatus.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="fef12-202">**Para asignar Britta Simon a Novatus, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="fef12-202">**To assign Britta Simon to Novatus, perform the following steps:**</span></span>

1. <span data-ttu-id="fef12-203">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fef12-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="fef12-205">En la lista de aplicaciones, seleccione **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="fef12-205">In the applications list, select **Novatus**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_app.png) 

3. <span data-ttu-id="fef12-207">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fef12-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="fef12-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fef12-209">Click **Add** button.</span></span> <span data-ttu-id="fef12-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fef12-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="fef12-212">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="fef12-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fef12-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fef12-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fef12-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fef12-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fef12-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="fef12-215">Testing single sign-on</span></span>

<span data-ttu-id="fef12-216">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="fef12-216">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fef12-217">Al hacer clic en el icono de Novatus en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Novatus.</span><span class="sxs-lookup"><span data-stu-id="fef12-217">When you click the Novatus tile in the Access Panel, you should get automatically signed-on to your Novatus application.</span></span> <span data-ttu-id="fef12-218">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fef12-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fef12-219">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="fef12-219">Additional resources</span></span>

* [<span data-ttu-id="fef12-220">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fef12-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fef12-221">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fef12-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_203.png

