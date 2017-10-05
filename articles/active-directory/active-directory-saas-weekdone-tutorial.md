---
title: "Tutorial: Integración de Azure Active Directory con Weekdone | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Weekdone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34921f9a-5637-4420-ab4c-9beb34421909
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 84aa0069dce55a6623398a99e1cac6bb21bf52f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-weekdone"></a><span data-ttu-id="50337-103">Tutorial: Integración de Azure Active Directory con Weekdone</span><span class="sxs-lookup"><span data-stu-id="50337-103">Tutorial: Azure Active Directory integration with Weekdone</span></span>

<span data-ttu-id="50337-104">En este tutorial, obtendrá información sobre cómo integrar Weekdone con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="50337-104">In this tutorial, you learn how to integrate Weekdone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="50337-105">La integración de Weekdone con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="50337-105">Integrating Weekdone with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="50337-106">Puede controlar en Azure AD quién tiene acceso a Weekdone.</span><span class="sxs-lookup"><span data-stu-id="50337-106">You can control in Azure AD who has access to Weekdone</span></span>
- <span data-ttu-id="50337-107">Puede permitir que los usuarios inicien sesión automáticamente en Weekdone (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50337-107">You can enable your users to automatically get signed-on to Weekdone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="50337-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="50337-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="50337-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="50337-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50337-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="50337-110">Prerequisites</span></span>

<span data-ttu-id="50337-111">Para configurar la integración de Azure AD con Weekdone, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="50337-111">To configure Azure AD integration with Weekdone, you need the following items:</span></span>

- <span data-ttu-id="50337-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="50337-112">An Azure AD subscription</span></span>
- <span data-ttu-id="50337-113">Una suscripción habilitada para inicio de sesión único en Weekdone</span><span class="sxs-lookup"><span data-stu-id="50337-113">A Weekdone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="50337-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="50337-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="50337-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="50337-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="50337-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="50337-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="50337-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="50337-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="50337-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="50337-118">Scenario description</span></span>
<span data-ttu-id="50337-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="50337-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="50337-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="50337-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="50337-121">Adición de Weekdone desde la Galería</span><span class="sxs-lookup"><span data-stu-id="50337-121">Adding Weekdone from the gallery</span></span>
2. <span data-ttu-id="50337-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="50337-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-weekdone-from-the-gallery"></a><span data-ttu-id="50337-123">Adición de Weekdone desde la Galería</span><span class="sxs-lookup"><span data-stu-id="50337-123">Adding Weekdone from the gallery</span></span>
<span data-ttu-id="50337-124">Para configurar la integración de Weekdone en Azure AD, deberá agregar Weekdone desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="50337-124">To configure the integration of Weekdone into Azure AD, you need to add Weekdone from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="50337-125">**Para agregar Weekdone desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="50337-125">**To add Weekdone from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="50337-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="50337-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="50337-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="50337-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="50337-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="50337-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="50337-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="50337-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="50337-133">En el cuadro de búsqueda, escriba **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="50337-133">In the search box, type **Weekdone**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_search.png)

5. <span data-ttu-id="50337-135">En el panel de resultados, seleccione **Weekdone** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="50337-135">In the results panel, select **Weekdone**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="50337-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="50337-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="50337-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Weekdone con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="50337-138">In this section, you configure and test Azure AD single sign-on with Weekdone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="50337-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Weekdone para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50337-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Weekdone is to a user in Azure AD.</span></span> <span data-ttu-id="50337-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Weekdone.</span><span class="sxs-lookup"><span data-stu-id="50337-140">In other words, a link relationship between an Azure AD user and the related user in Weekdone needs to be established.</span></span>

<span data-ttu-id="50337-141">Para establecer la relación de vínculo, en Weekdone, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="50337-141">In Weekdone, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="50337-142">Para configurar y probar el inicio de sesión único de Azure AD con Weekdone, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="50337-142">To configure and test Azure AD single sign-on with Weekdone, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="50337-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="50337-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="50337-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="50337-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="50337-145">**[Creación de un usuario de prueba de Weekdone](#creating-a-weekdone-test-user)**: para tener un homólogo de Britta Simon en Weekdone que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50337-145">**[Creating a Weekdone test user](#creating-a-weekdone-test-user)** - to have a counterpart of Britta Simon in Weekdone that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="50337-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50337-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="50337-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="50337-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="50337-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="50337-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="50337-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Weekdone.</span><span class="sxs-lookup"><span data-stu-id="50337-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Weekdone application.</span></span>

<span data-ttu-id="50337-150">**Para configurar el inicio de sesión único de Azure AD con Weekdone, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="50337-150">**To configure Azure AD single sign-on with Weekdone, perform the following steps:**</span></span>

1. <span data-ttu-id="50337-151">En Azure Portal, en la página de integración de la aplicación **Weekdone**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="50337-151">In the Azure portal, on the **Weekdone** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="50337-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="50337-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_samlbase.png)

3. <span data-ttu-id="50337-155">Vaya a la sección **Dominio y direcciones URL de Weekdone**, si quiere configurar la aplicación en modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="50337-155">On the **Weekdone Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url1.png)

    <span data-ttu-id="50337-157">a.</span><span class="sxs-lookup"><span data-stu-id="50337-157">a.</span></span> <span data-ttu-id="50337-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="50337-158">In the **Identifier** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

    <span data-ttu-id="50337-159">b.</span><span class="sxs-lookup"><span data-stu-id="50337-159">b.</span></span> <span data-ttu-id="50337-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://weekdone.com/a/<tenantname>`.</span><span class="sxs-lookup"><span data-stu-id="50337-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

4. <span data-ttu-id="50337-161">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="50337-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="50337-162">Si quiere volver a configurar la aplicación en modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="50337-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url2.png)

    <span data-ttu-id="50337-164">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://weekdone.com/a/<tenantname>`.</span><span class="sxs-lookup"><span data-stu-id="50337-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="50337-165">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="50337-165">These values are not real.</span></span> <span data-ttu-id="50337-166">Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="50337-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="50337-167">Póngase en contacto con el [equipo de soporte de cliente de Weekdone](mailto:hello@weekdone.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="50337-167">Contact [Weekdone Client support team](mailto:hello@weekdone.com) to get these values.</span></span> 

5. <span data-ttu-id="50337-168">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="50337-168">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_certificate.png) 

6. <span data-ttu-id="50337-170">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="50337-170">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-weekdone-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="50337-172">En la sección **Configuración de Weekdone**, haga clic en **Configurar Weekdone** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="50337-172">On the **Weekdone Configuration** section, click **Configure Weekdone** to open **Configure sign-on** window.</span></span> <span data-ttu-id="50337-173">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="50337-173">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_configure.png) 

8. <span data-ttu-id="50337-175">Para configurar el inicio de sesión único en **Weekdone**, es preciso enviar los valores descargados de **XML de metadatos, Dirección URL de cierre de sesión, SAML Entity ID (Identificador de entidad de SAML) y SAML Single Sign-On Service URL (Dirección URL del servicio de inicio de sesión único de SAML)** al [equipo de soporte técnico de Weekdone](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="50337-175">To configure single sign-on on **Weekdone** side, you need to send the downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Weekdone support team](mailto:hello@weekdone.com).</span></span>

> [!TIP]
> <span data-ttu-id="50337-176">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="50337-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="50337-177">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="50337-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="50337-178">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="50337-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="50337-179">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="50337-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="50337-180">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="50337-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="50337-182">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="50337-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="50337-183">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="50337-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="50337-185">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="50337-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="50337-187">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="50337-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="50337-189">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="50337-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="50337-191">a.</span><span class="sxs-lookup"><span data-stu-id="50337-191">a.</span></span> <span data-ttu-id="50337-192">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="50337-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="50337-193">b.</span><span class="sxs-lookup"><span data-stu-id="50337-193">b.</span></span> <span data-ttu-id="50337-194">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="50337-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="50337-195">c.</span><span class="sxs-lookup"><span data-stu-id="50337-195">c.</span></span> <span data-ttu-id="50337-196">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="50337-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="50337-197">d.</span><span class="sxs-lookup"><span data-stu-id="50337-197">d.</span></span> <span data-ttu-id="50337-198">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="50337-198">Click **Create**.</span></span>
 
### <a name="creating-a-weekdone-test-user"></a><span data-ttu-id="50337-199">Creación de un usuario de prueba de Weekdone</span><span class="sxs-lookup"><span data-stu-id="50337-199">Creating a Weekdone test user</span></span>

<span data-ttu-id="50337-200">El objetivo de esta sección es crear una usuaria de prueba llamada Britta Simon en Weekdone.</span><span class="sxs-lookup"><span data-stu-id="50337-200">The objective of this section is to create a user called Britta Simon in Weekdone.</span></span> <span data-ttu-id="50337-201">Weekdone admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="50337-201">Weekdone supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="50337-202">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="50337-202">There is no action item for you in this section.</span></span> <span data-ttu-id="50337-203">Durante un intento de acceso a Weekdone se crea un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="50337-203">A new user is created during an attempt to access Weekdone if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="50337-204">Si necesita crear manualmente un usuario, es preciso que se ponga en contacto con el [equipo de soporte técnico de Weekdone](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="50337-204">If you need to create a user manually, you need to contact the [Weekdone Client support team](mailto:hello@weekdone.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="50337-205">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="50337-205">Assigning the Azure AD test user</span></span>

<span data-ttu-id="50337-206">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Weekdone.</span><span class="sxs-lookup"><span data-stu-id="50337-206">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Weekdone.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="50337-208">**Para asignar a Britta Simon a Weekdone, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="50337-208">**To assign Britta Simon to Weekdone, perform the following steps:**</span></span>

1. <span data-ttu-id="50337-209">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="50337-209">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="50337-211">En la lista de aplicaciones, seleccione **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="50337-211">In the applications list, select **Weekdone**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_app.png) 

3. <span data-ttu-id="50337-213">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="50337-213">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="50337-215">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="50337-215">Click **Add** button.</span></span> <span data-ttu-id="50337-216">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="50337-216">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="50337-218">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="50337-218">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="50337-219">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="50337-219">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="50337-220">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="50337-220">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="50337-221">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="50337-221">Testing single sign-on</span></span>

<span data-ttu-id="50337-222">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="50337-222">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="50337-223">Al hacer clic en el icono de Weekdone en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Weekdone.</span><span class="sxs-lookup"><span data-stu-id="50337-223">When you click the Weekdone tile in the Access Panel, you should get automatically signed-on to your Weekdone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="50337-224">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="50337-224">Additional resources</span></span>

* [<span data-ttu-id="50337-225">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50337-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="50337-226">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="50337-226">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_203.png

