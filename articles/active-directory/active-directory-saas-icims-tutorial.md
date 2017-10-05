---
title: "Tutorial: integración de Azure Active Directory con ICIMS | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory e ICIMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 72dbd649-e4b1-4d72-ad76-636d84922596
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 26a6b41a0e59924d007855ca548f22ed00bd7e23
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icims"></a><span data-ttu-id="aa042-103">Tutorial: integración de Azure Active Directory con ICIMS</span><span class="sxs-lookup"><span data-stu-id="aa042-103">Tutorial: Azure Active Directory integration with ICIMS</span></span>

<span data-ttu-id="aa042-104">En este tutorial, obtendrá información sobre cómo integrar ICIMS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aa042-104">In this tutorial, you learn how to integrate ICIMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aa042-105">Integrar ICIMS con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="aa042-105">Integrating ICIMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="aa042-106">Puede controlar en Azure AD quién tiene acceso a ICIMS.</span><span class="sxs-lookup"><span data-stu-id="aa042-106">You can control in Azure AD who has access to ICIMS</span></span>
- <span data-ttu-id="aa042-107">Puede permitir que los usuarios inicien sesión automáticamente en ICIMS (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa042-107">You can enable your users to automatically get signed-on to ICIMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aa042-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="aa042-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="aa042-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aa042-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa042-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="aa042-110">Prerequisites</span></span>

<span data-ttu-id="aa042-111">Para configurar la integración de Azure AD con ICIMS, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="aa042-111">To configure Azure AD integration with ICIMS, you need the following items:</span></span>

- <span data-ttu-id="aa042-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa042-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aa042-113">Una suscripción habilitada para el inicio de sesión único en ICIMS</span><span class="sxs-lookup"><span data-stu-id="aa042-113">An ICIMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aa042-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="aa042-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aa042-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="aa042-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aa042-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="aa042-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aa042-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aa042-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aa042-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="aa042-118">Scenario description</span></span>
<span data-ttu-id="aa042-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="aa042-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aa042-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="aa042-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aa042-121">Incorporación de ICIMS desde la galería</span><span class="sxs-lookup"><span data-stu-id="aa042-121">Adding ICIMS from the gallery</span></span>
2. <span data-ttu-id="aa042-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa042-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icims-from-the-gallery"></a><span data-ttu-id="aa042-123">Incorporación de ICIMS desde la galería</span><span class="sxs-lookup"><span data-stu-id="aa042-123">Adding ICIMS from the gallery</span></span>
<span data-ttu-id="aa042-124">Para configurar la integración de ICIMS en Azure AD, deberá agregar ICIMS desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="aa042-124">To configure the integration of ICIMS into Azure AD, you need to add ICIMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="aa042-125">**Para agregar ICIMS desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="aa042-125">**To add ICIMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="aa042-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aa042-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="aa042-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="aa042-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="aa042-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="aa042-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="aa042-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa042-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="aa042-133">En el cuadro de búsqueda, escriba **ICIMS**, seleccione **ICIMS** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aa042-133">In the search box, type **ICIMS**, select **ICIMS** from result panel then click **Add** button to add the application.</span></span>

    ![ICIMS en la lista de resultados](./media/active-directory-saas-icims-tutorial/tutorial_icims_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="aa042-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa042-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="aa042-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ICIMS con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="aa042-136">In this section, you configure and test Azure AD single sign-on with ICIMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="aa042-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de ICIMS para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa042-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ICIMS is to a user in Azure AD.</span></span> <span data-ttu-id="aa042-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de ICIMS.</span><span class="sxs-lookup"><span data-stu-id="aa042-138">In other words, a link relationship between an Azure AD user and the related user in ICIMS needs to be established.</span></span>

<span data-ttu-id="aa042-139">Para establecer la relación de vínculo, en ICIMS, asigne el valor del **nombre de usuario** de Azure AD como el valor del **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="aa042-139">In ICIMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="aa042-140">Para configurar y probar el inicio de sesión único de Azure AD con ICIMS, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="aa042-140">To configure and test Azure AD single sign-on with ICIMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="aa042-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="aa042-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="aa042-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aa042-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aa042-143">**[Creación de un usuario de prueba de ICIMS](#create-an-icims-test-user)**: para tener un homólogo de Britta Simon en ICIMS que esté vinculado a la representación de esta en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa042-143">**[Create an ICIMS test user](#create-an-icims-test-user)** - to have a counterpart of Britta Simon in ICIMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="aa042-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa042-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aa042-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="aa042-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="aa042-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa042-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="aa042-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en su aplicación ICIMS.</span><span class="sxs-lookup"><span data-stu-id="aa042-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ICIMS application.</span></span>

<span data-ttu-id="aa042-148">**Para configurar el inicio de sesión único de Azure AD con ICIMS, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="aa042-148">**To configure Azure AD single sign-on with ICIMS, perform the following steps:**</span></span>

1. <span data-ttu-id="aa042-149">En Azure Portal, en la página de integración de la aplicación **ICIMS**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="aa042-149">In the Azure portal, on the **ICIMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="aa042-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="aa042-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-icims-tutorial/tutorial_icims_samlbase.png)

3. <span data-ttu-id="aa042-153">En la sección **Dominio y direcciones URL de ICIMS**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="aa042-153">On the **ICIMS Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_url.png)

    <span data-ttu-id="aa042-155">a.</span><span class="sxs-lookup"><span data-stu-id="aa042-155">a.</span></span> <span data-ttu-id="aa042-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<tenant name>.icims.com`.</span><span class="sxs-lookup"><span data-stu-id="aa042-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant name>.icims.com`</span></span>

    <span data-ttu-id="aa042-157">b.</span><span class="sxs-lookup"><span data-stu-id="aa042-157">b.</span></span> <span data-ttu-id="aa042-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="aa042-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant name>.icims.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="aa042-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="aa042-159">These values are not real.</span></span> <span data-ttu-id="aa042-160">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="aa042-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="aa042-161">Póngase en contacto con el [equipo de soporte técnico de ICIMS](https://www.icims.com/contact-us) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="aa042-161">Contact [ICIMS Client support team](https://www.icims.com/contact-us) to get these values.</span></span> 
 
4. <span data-ttu-id="aa042-162">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="aa042-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-icims-tutorial/tutorial_icims_certificate.png) 

5. <span data-ttu-id="aa042-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="aa042-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-icims-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="aa042-166">En la sección **Configuración de ICIMS**, haga clic en **Configurar ICIMS** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="aa042-166">On the **ICIMS Configuration** section, click **Configure ICIMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="aa042-167">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="aa042-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_configure.png) 

7. <span data-ttu-id="aa042-169">Para configurar el inicio de sesión único en **ICIMS**, es preciso enviar los valores descargados de **XML de metadatos**, **Dirección URL de cierre de sesión, SAML Entity ID (Identificador de entidad de SAML) y SAML Single Sign-On Service URL (Dirección URL del servicio de inicio de sesión único de SAML)** al [equipo de soporte técnico de ICIMS](https://www.icims.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="aa042-169">To configure single sign-on on **ICIMS** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [ICIMS support team](https://www.icims.com/contact-us).</span></span> <span data-ttu-id="aa042-170">El equipo de soporte técnico lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="aa042-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="aa042-171">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aa042-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="aa042-172">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="aa042-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="aa042-173">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="aa042-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="aa042-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa042-174">Create an Azure AD test user</span></span>
<span data-ttu-id="aa042-175">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="aa042-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="aa042-177">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="aa042-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="aa042-178">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aa042-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-icims-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aa042-180">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="aa042-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-icims-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aa042-182">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa042-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Botón Agregar](./media/active-directory-saas-icims-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aa042-184">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="aa042-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Cuadro de diálogo Usuario](./media/active-directory-saas-icims-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aa042-186">a.</span><span class="sxs-lookup"><span data-stu-id="aa042-186">a.</span></span> <span data-ttu-id="aa042-187">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aa042-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aa042-188">b.</span><span class="sxs-lookup"><span data-stu-id="aa042-188">b.</span></span> <span data-ttu-id="aa042-189">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aa042-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aa042-190">c.</span><span class="sxs-lookup"><span data-stu-id="aa042-190">c.</span></span> <span data-ttu-id="aa042-191">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="aa042-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="aa042-192">d.</span><span class="sxs-lookup"><span data-stu-id="aa042-192">d.</span></span> <span data-ttu-id="aa042-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="aa042-193">Click **Create**.</span></span>
 
### <a name="create-an-icims-test-user"></a><span data-ttu-id="aa042-194">Creación de un usuario de prueba de ICIMS</span><span class="sxs-lookup"><span data-stu-id="aa042-194">Create an ICIMS test user</span></span>

<span data-ttu-id="aa042-195">El objetivo de esta sección es crear una usuaria llamada llamado Britta Simon en ICIMS.</span><span class="sxs-lookup"><span data-stu-id="aa042-195">The objective of this section is to create a user called Britta Simon in ICIMS.</span></span> <span data-ttu-id="aa042-196">Trabaje con el [equipo de soporte técnico de ICIMS](https://www.icims.com/contact-us) para agregar usuarios a la cuenta de ICIMS.</span><span class="sxs-lookup"><span data-stu-id="aa042-196">Work with [ICIMS support team](https://www.icims.com/contact-us) to add the users in the ICIMS account.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="aa042-197">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa042-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="aa042-198">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a ICIMS.</span><span class="sxs-lookup"><span data-stu-id="aa042-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ICIMS.</span></span>

![Asignación del rol de usuario][200]

<span data-ttu-id="aa042-200">**Para asignar la usuaria Britta Simon a ICIMS, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="aa042-200">**To assign Britta Simon to ICIMS, perform the following steps:**</span></span>

1. <span data-ttu-id="aa042-201">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="aa042-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="aa042-203">En la lista de aplicaciones, seleccione **ICIMS**.</span><span class="sxs-lookup"><span data-stu-id="aa042-203">In the applications list, select **ICIMS**.</span></span>

    ![Vínculo a ICIMS en la lista de aplicaciones](./media/active-directory-saas-icims-tutorial/tutorial_icims_app.png) 

3. <span data-ttu-id="aa042-205">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="aa042-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202] 

4. <span data-ttu-id="aa042-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="aa042-207">Click **Add** button.</span></span> <span data-ttu-id="aa042-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="aa042-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="aa042-210">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="aa042-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="aa042-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="aa042-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aa042-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="aa042-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="aa042-213">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="aa042-213">Test single sign-on</span></span>

<span data-ttu-id="aa042-214">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="aa042-214">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="aa042-215">Al hacer clic en el icono de ICIMS en el panel de acceso, debería iniciar sesión automáticamente en su aplicación de ICIMS.</span><span class="sxs-lookup"><span data-stu-id="aa042-215">When you click the ICIMS tile in the Access Panel, you should get automatically signed-on to your ICIMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="aa042-216">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="aa042-216">Additional resources</span></span>

* [<span data-ttu-id="aa042-217">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aa042-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aa042-218">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="aa042-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icims-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icims-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icims-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icims-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icims-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icims-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icims-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icims-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icims-tutorial/tutorial_general_203.png

