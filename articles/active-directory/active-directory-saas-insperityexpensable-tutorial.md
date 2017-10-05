---
title: "Tutorial: Integración de Azure Active Directory con Insperity ExpensAble | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory e Insperity ExpensAble."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c579c453-580e-417d-8a5e-9b6b352795c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: b50e10be54b1fc413be10bee5b58631790629335
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insperity-expensable"></a><span data-ttu-id="43969-103">Tutorial: integración de Azure Active Directory con Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="43969-103">Tutorial: Azure Active Directory integration with Insperity ExpensAble</span></span>

<span data-ttu-id="43969-104">En este tutorial, obtendrá información sobre cómo integrar Insperity ExpensAble con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="43969-104">In this tutorial, you learn how to integrate Insperity ExpensAble with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="43969-105">Integrar Insperity ExpensAble con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="43969-105">Integrating Insperity ExpensAble with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="43969-106">Puede controlar en Azure AD quién tiene acceso a Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="43969-106">You can control in Azure AD who has access to Insperity ExpensAble</span></span>
- <span data-ttu-id="43969-107">Puede permitir que los usuarios inicien sesión automáticamente en Insperity ExpensAble (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43969-107">You can enable your users to automatically get signed-on to Insperity ExpensAble (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="43969-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="43969-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="43969-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="43969-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43969-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="43969-110">Prerequisites</span></span>

<span data-ttu-id="43969-111">Para configurar la integración de Azure AD con Insperity ExpensAble, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="43969-111">To configure Azure AD integration with Insperity ExpensAble, you need the following items:</span></span>

- <span data-ttu-id="43969-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="43969-112">An Azure AD subscription</span></span>
- <span data-ttu-id="43969-113">Una suscripción habilitada para el inicio de sesión único en Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="43969-113">An Insperity ExpensAble single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="43969-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="43969-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="43969-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="43969-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="43969-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="43969-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="43969-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="43969-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="43969-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="43969-118">Scenario description</span></span>
<span data-ttu-id="43969-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="43969-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="43969-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="43969-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="43969-121">Incorporación de Insperity ExpensAble desde la galería</span><span class="sxs-lookup"><span data-stu-id="43969-121">Adding Insperity ExpensAble from the gallery</span></span>
2. <span data-ttu-id="43969-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="43969-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insperity-expensable-from-the-gallery"></a><span data-ttu-id="43969-123">Incorporación de Insperity ExpensAble desde la galería</span><span class="sxs-lookup"><span data-stu-id="43969-123">Adding Insperity ExpensAble from the gallery</span></span>
<span data-ttu-id="43969-124">Para configurar la integración de Insperity ExpensAble en Azure AD, deberá agregar Insperity ExpensAble desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="43969-124">To configure the integration of Insperity ExpensAble into Azure AD, you need to add Insperity ExpensAble from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="43969-125">**Para agregar Insperity ExpensAble desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="43969-125">**To add Insperity ExpensAble from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="43969-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="43969-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="43969-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="43969-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="43969-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="43969-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="43969-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="43969-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="43969-133">En el cuadro de búsqueda, escriba **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="43969-133">In the search box, type **Insperity ExpensAble**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_search.png)

5. <span data-ttu-id="43969-135">En el panel de resultados, seleccione **Insperity ExpensAble** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="43969-135">In the results panel, select **Insperity ExpensAble**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="43969-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="43969-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="43969-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Insperity ExpensAble con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="43969-138">In this section, you configure and test Azure AD single sign-on with Insperity ExpensAble based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="43969-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Insperity ExpensAble para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43969-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Insperity ExpensAble is to a user in Azure AD.</span></span> <span data-ttu-id="43969-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="43969-140">In other words, a link relationship between an Azure AD user and the related user in Insperity ExpensAble needs to be established.</span></span>

<span data-ttu-id="43969-141">Para establecer la relación de vínculo, en Insperity ExpensAble, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="43969-141">In Insperity ExpensAble, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="43969-142">Para configurar y probar el inicio de sesión único de Azure AD con Insperity ExpensAble, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="43969-142">To configure and test Azure AD single sign-on with Insperity ExpensAble, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="43969-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="43969-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="43969-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="43969-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="43969-145">**[Creación de un usuario de prueba de Insperity ExpensAble](#creating-an-insperity-expensable-test-user)**: para tener un homólogo de Britta Simon en Insperity ExpensAble que esté vinculado a la representación de usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43969-145">**[Creating an Insperity ExpensAble test user](#creating-an-insperity-expensable-test-user)** - to have a counterpart of Britta Simon in Insperity ExpensAble that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="43969-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43969-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="43969-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="43969-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="43969-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="43969-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="43969-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="43969-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Insperity ExpensAble application.</span></span>

<span data-ttu-id="43969-150">**Para configurar el inicio de sesión único de Azure AD con Insperity ExpensAble, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="43969-150">**To configure Azure AD single sign-on with Insperity ExpensAble, perform the following steps:**</span></span>

1. <span data-ttu-id="43969-151">En Azure Portal, en la página de integración de la aplicación **Insperity ExpensAble**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="43969-151">In the Azure portal, on the **Insperity ExpensAble** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="43969-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="43969-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_samlbase.png)

3. <span data-ttu-id="43969-155">En la sección **Dominio y direcciones URL de Insperity ExpensAble**, lleve a cabo los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="43969-155">On the **Insperity ExpensAble Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_url.png)

    <span data-ttu-id="43969-157">a.</span><span class="sxs-lookup"><span data-stu-id="43969-157">a.</span></span> <span data-ttu-id="43969-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`.</span><span class="sxs-lookup"><span data-stu-id="43969-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="43969-159">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="43969-159">This value is not real.</span></span> <span data-ttu-id="43969-160">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="43969-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="43969-161">Póngase en contacto con el [equipo de soporte técnico de Insperity ExpensAble](http://expensable.com/support/support-overview) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="43969-161">Contact [Insperity ExpensAble Client support team](http://expensable.com/support/support-overview) to get this value.</span></span> 
 
4. <span data-ttu-id="43969-162">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="43969-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_certificate.png) 

5. <span data-ttu-id="43969-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="43969-164">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="43969-166">En la sección de **configuración Insperity ExpensAble**, haga clic en **Configurar Insperity ExpensAble** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="43969-166">On the **Insperity ExpensAble Configuration** section, click **Configure Insperity ExpensAble** to open **Configure sign-on** window.</span></span> <span data-ttu-id="43969-167">Copie los valores de **SAML Entity ID y SAML Single Sign-On Service URL** (Identificador de entidad de SAML y URL del servicio de inicio de sesión único de SAML) de la sección de **referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="43969-167">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_configure.png) 

7. <span data-ttu-id="43969-169">Para configurar el inicio de sesión único en **Insperity ExpensAble**, es preciso enviar los valores descargados de **XML de metadatos**, **SAML Single Sign-On Service URL** (URL del servicio de inicio de sesión único de SAML) y **SAML Entity ID** (Id. de entidad SAML) al [equipo de soporte técnico de Insperity ExpensAble](http://expensable.com/support/support-overview).</span><span class="sxs-lookup"><span data-stu-id="43969-169">To configure single sign-on on **Insperity ExpensAble** side, you need to send the downloaded **Metadata XML**, **SAML Single Sign-On Service URL** and **SAML Entity ID** to [Insperity ExpensAble support team](http://expensable.com/support/support-overview).</span></span> <span data-ttu-id="43969-170">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="43969-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="43969-171">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="43969-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="43969-172">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="43969-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="43969-173">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="43969-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="43969-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="43969-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="43969-175">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="43969-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="43969-177">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="43969-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="43969-178">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="43969-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="43969-180">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="43969-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="43969-182">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="43969-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="43969-184">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="43969-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="43969-186">a.</span><span class="sxs-lookup"><span data-stu-id="43969-186">a.</span></span> <span data-ttu-id="43969-187">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="43969-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="43969-188">b.</span><span class="sxs-lookup"><span data-stu-id="43969-188">b.</span></span> <span data-ttu-id="43969-189">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="43969-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="43969-190">c.</span><span class="sxs-lookup"><span data-stu-id="43969-190">c.</span></span> <span data-ttu-id="43969-191">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="43969-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="43969-192">d.</span><span class="sxs-lookup"><span data-stu-id="43969-192">d.</span></span> <span data-ttu-id="43969-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="43969-193">Click **Create**.</span></span>
 
### <a name="creating-an-insperity-expensable-test-user"></a><span data-ttu-id="43969-194">Creación de un usuario de prueba de Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="43969-194">Creating an Insperity ExpensAble test user</span></span>

<span data-ttu-id="43969-195">El objetivo de esta sección es crear una usuaria llamada llamado Britta Simon en Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="43969-195">The objective of this section is to create a user called Britta Simon in Insperity ExpensAble.</span></span> <span data-ttu-id="43969-196">Trabaje con el [equipo de soporte técnico correspondiente](http://expensable.com/support/support-overview) para agregar usuarios en la cuenta de Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="43969-196">Please work with [Insperity ExpensAble support team](http://expensable.com/support/support-overview) to add the users in the Insperity ExpensAble account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="43969-197">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="43969-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="43969-198">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="43969-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Insperity ExpensAble.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="43969-200">**Para asignar a Britta Simon a Insperity ExpensAble, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="43969-200">**To assign Britta Simon to Insperity ExpensAble, perform the following steps:**</span></span>

1. <span data-ttu-id="43969-201">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="43969-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="43969-203">En la lista de aplicaciones, seleccione **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="43969-203">In the applications list, select **Insperity ExpensAble**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_app.png) 

3. <span data-ttu-id="43969-205">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="43969-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="43969-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="43969-207">Click **Add** button.</span></span> <span data-ttu-id="43969-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="43969-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="43969-210">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="43969-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="43969-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="43969-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="43969-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="43969-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="43969-213">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="43969-213">Testing single sign-on</span></span>

<span data-ttu-id="43969-214">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="43969-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="43969-215">Al hacer clic en el icono de Insperity ExpensAble en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="43969-215">When you click the Insperity ExpensAble tile in the Access Panel, you should get automatically signed-on to your Insperity ExpensAble application.</span></span>
<span data-ttu-id="43969-216">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="43969-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="43969-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="43969-217">Additional resources</span></span>

* [<span data-ttu-id="43969-218">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="43969-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="43969-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="43969-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_203.png

