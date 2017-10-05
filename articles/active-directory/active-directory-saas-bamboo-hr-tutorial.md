---
title: "Tutorial: Integración de Azure Active Directory con BambooHR | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y BambooHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f826b5d2-9c64-47df-bbbf-0adf9eb0fa71
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: jeedes
ms.openlocfilehash: 06bf91b0e598fd3d8e644378efdb753611ee1ebc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bamboohr"></a><span data-ttu-id="e73bc-103">Tutorial: Integración de Azure Active Directory con BambooHR</span><span class="sxs-lookup"><span data-stu-id="e73bc-103">Tutorial: Azure Active Directory integration with BambooHR</span></span>

<span data-ttu-id="e73bc-104">En este tutorial, obtendrá información sobre cómo integrar BambooHR con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e73bc-104">In this tutorial, you learn how to integrate BambooHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e73bc-105">La integración de BambooHR con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e73bc-105">Integrating BambooHR with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e73bc-106">En Azure AD puede controlar quién tiene acceso a BambooHR</span><span class="sxs-lookup"><span data-stu-id="e73bc-106">You can control in Azure AD who has access to BambooHR</span></span>
- <span data-ttu-id="e73bc-107">Puede permitir que los usuarios inicien sesión automáticamente en BambooHR (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e73bc-107">You can enable your users to automatically get signed-on to BambooHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e73bc-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e73bc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e73bc-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e73bc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e73bc-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e73bc-110">Prerequisites</span></span>

<span data-ttu-id="e73bc-111">Para configurar la integración de Azure AD con BambooHR, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e73bc-111">To configure Azure AD integration with BambooHR, you need the following items:</span></span>

- <span data-ttu-id="e73bc-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e73bc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e73bc-113">Una suscripción habilitada para el inicio de sesión único en BambooHR</span><span class="sxs-lookup"><span data-stu-id="e73bc-113">A BambooHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e73bc-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e73bc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e73bc-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e73bc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e73bc-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e73bc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e73bc-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e73bc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e73bc-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e73bc-118">Scenario description</span></span>
<span data-ttu-id="e73bc-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e73bc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e73bc-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="e73bc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e73bc-121">Incorporación de BambooHR desde la galería</span><span class="sxs-lookup"><span data-stu-id="e73bc-121">Adding BambooHR from the gallery</span></span>
2. <span data-ttu-id="e73bc-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e73bc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bamboohr-from-the-gallery"></a><span data-ttu-id="e73bc-123">Incorporación de BambooHR desde la galería</span><span class="sxs-lookup"><span data-stu-id="e73bc-123">Adding BambooHR from the gallery</span></span>
<span data-ttu-id="e73bc-124">Para configurar la integración de BambooHR en Azure AD, deberá agregar BambooHR desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="e73bc-124">To configure the integration of BambooHR into Azure AD, you need to add BambooHR from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e73bc-125">**Para agregar BambooHR desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e73bc-125">**To add BambooHR from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e73bc-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e73bc-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e73bc-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e73bc-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e73bc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e73bc-133">En el cuadro de búsqueda, escriba **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-133">In the search box, type **BambooHR**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_search.png)

5. <span data-ttu-id="e73bc-135">En el panel de resultados, seleccione **BambooHR** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e73bc-135">In the results panel, select **BambooHR**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e73bc-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e73bc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e73bc-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con BambooHR con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e73bc-138">In this section, you configure and test Azure AD single sign-on with BambooHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e73bc-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de BambooHR para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e73bc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BambooHR is to a user in Azure AD.</span></span> <span data-ttu-id="e73bc-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de BambooHR.</span><span class="sxs-lookup"><span data-stu-id="e73bc-140">In other words, a link relationship between an Azure AD user and the related user in BambooHR needs to be established.</span></span>

<span data-ttu-id="e73bc-141">Para establecer la relación de vínculo, en BambooHR, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-141">In BambooHR, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e73bc-142">Para configurar y probar el inicio de sesión único de Azure AD con BambooHR, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e73bc-142">To configure and test Azure AD single sign-on with BambooHR, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e73bc-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="e73bc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e73bc-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e73bc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e73bc-145">**[Creación de un usuario de prueba de BambooHR](#creating-a-bamboohr-test-user)**: para tener un homólogo de Britta Simon en BambooHR que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e73bc-145">**[Creating a BambooHR test user](#creating-a-bamboohr-test-user)** - to have a counterpart of Britta Simon in BambooHR that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e73bc-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e73bc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e73bc-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e73bc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e73bc-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e73bc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e73bc-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación BambooHR.</span><span class="sxs-lookup"><span data-stu-id="e73bc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BambooHR application.</span></span>

<span data-ttu-id="e73bc-150">**Para configurar el inicio de sesión único de Azure AD con BambooHR, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e73bc-150">**To configure Azure AD single sign-on with BambooHR, perform the following steps:**</span></span>

1. <span data-ttu-id="e73bc-151">En Azure Portal, en la página de integración de la aplicación **BambooHR**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-151">In the Azure portal, on the **BambooHR** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e73bc-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e73bc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_samlbase.png)

3. <span data-ttu-id="e73bc-155">En la sección **Dominio y direcciones URL de BambooHR**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e73bc-155">On the **BambooHR Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_url.png)

    <span data-ttu-id="e73bc-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<company>.bamboohr.com`.</span><span class="sxs-lookup"><span data-stu-id="e73bc-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.bamboohr.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="e73bc-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="e73bc-158">This value is not real.</span></span> <span data-ttu-id="e73bc-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="e73bc-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="e73bc-160">Póngase en contacto con el [equipo de soporte técnico de cliente de BambooHR](https://www.bamboohr.com/contact.php) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="e73bc-160">Contact [BambooHR Client support team](https://www.bamboohr.com/contact.php) to get this value.</span></span> 
 
4. <span data-ttu-id="e73bc-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e73bc-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_certificate.png) 

5. <span data-ttu-id="e73bc-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e73bc-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e73bc-165">En la sección **Configuración de BambooHR**, haga clic en **Configurar BambooHR** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-165">On the **BambooHR Configuration** section, click **Configure BambooHR** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e73bc-166">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_configure.png) 

6. <span data-ttu-id="e73bc-168">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de BambooHR.</span><span class="sxs-lookup"><span data-stu-id="e73bc-168">In a different web browser window, log into your BambooHR company site as an administrator.</span></span>

7. <span data-ttu-id="e73bc-169">En la página principal realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e73bc-169">On the homepage, perform the following steps:</span></span>
   
    <span data-ttu-id="e73bc-170">![Inicio de sesión único](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="e73bc-170">![Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span></span>   

    <span data-ttu-id="e73bc-171">a.</span><span class="sxs-lookup"><span data-stu-id="e73bc-171">a.</span></span> <span data-ttu-id="e73bc-172">Haga clic en **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-172">Click **Apps**.</span></span>
   
    <span data-ttu-id="e73bc-173">b.</span><span class="sxs-lookup"><span data-stu-id="e73bc-173">b.</span></span> <span data-ttu-id="e73bc-174">En el menú de aplicaciones de la izquierda, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-174">In the apps menu on the left, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="e73bc-175">c.</span><span class="sxs-lookup"><span data-stu-id="e73bc-175">c.</span></span> <span data-ttu-id="e73bc-176">Haga clic en **Inicio de sesión único de SAML**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-176">Click **SAML Single Sign-On**.</span></span>

8. <span data-ttu-id="e73bc-177">En la sección **Inicio de sesión único de SAML** siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e73bc-177">In the **SAML Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="e73bc-178">![Inicio de sesión único SAML](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "Inicio de sesión único SAML")</span><span class="sxs-lookup"><span data-stu-id="e73bc-178">![SAML Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML Single Sign-On")</span></span>
   
    <span data-ttu-id="e73bc-179">a.</span><span class="sxs-lookup"><span data-stu-id="e73bc-179">a.</span></span> <span data-ttu-id="e73bc-180">Pegue el valor de la **dirección URL de servicio de inicio de sesión único de SAML** en el cuadro de texto **SSO Login Url** (Dirección URL de inicio de sesión de SSO).</span><span class="sxs-lookup"><span data-stu-id="e73bc-180">Paste the **SAML Single Sign-On Service URL** value into the **SSO Login Url** textbox.</span></span>
      
    <span data-ttu-id="e73bc-181">b.</span><span class="sxs-lookup"><span data-stu-id="e73bc-181">b.</span></span> <span data-ttu-id="e73bc-182">Abra el certificado codificado en Base 64 que descargó de Azure Portal en el Bloc de notas, copie el contenido en el Portapapeles y, luego, péguelo en el cuadro de texto **X.509 Certificate** (Certificado X.509)</span><span class="sxs-lookup"><span data-stu-id="e73bc-182">Open base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
   
    <span data-ttu-id="e73bc-183">c.</span><span class="sxs-lookup"><span data-stu-id="e73bc-183">c.</span></span> <span data-ttu-id="e73bc-184">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e73bc-185">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e73bc-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e73bc-186">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e73bc-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e73bc-187">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e73bc-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e73bc-188">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e73bc-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="e73bc-189">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e73bc-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="e73bc-191">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="e73bc-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e73bc-192">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e73bc-194">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e73bc-196">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e73bc-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e73bc-198">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="e73bc-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e73bc-200">a.</span><span class="sxs-lookup"><span data-stu-id="e73bc-200">a.</span></span> <span data-ttu-id="e73bc-201">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e73bc-202">b.</span><span class="sxs-lookup"><span data-stu-id="e73bc-202">b.</span></span> <span data-ttu-id="e73bc-203">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e73bc-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e73bc-204">c.</span><span class="sxs-lookup"><span data-stu-id="e73bc-204">c.</span></span> <span data-ttu-id="e73bc-205">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e73bc-206">d.</span><span class="sxs-lookup"><span data-stu-id="e73bc-206">d.</span></span> <span data-ttu-id="e73bc-207">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-207">Click **Create**.</span></span>
 
### <a name="creating-a-bamboohr-test-user"></a><span data-ttu-id="e73bc-208">Creación de un usuario de prueba de BambooHR</span><span class="sxs-lookup"><span data-stu-id="e73bc-208">Creating a BambooHR test user</span></span>

<span data-ttu-id="e73bc-209">Para permitir que los usuarios de Azure AD inicien sesión en BambooHR, deben aprovisionarse a BambooHR.</span><span class="sxs-lookup"><span data-stu-id="e73bc-209">To enable Azure AD users to log in to BambooHR, they must be provisioned into BambooHR.</span></span>  

<span data-ttu-id="e73bc-210">En el caso de BambooHR, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="e73bc-210">In the case of BambooHR, provisioning is a manual task.</span></span>

<span data-ttu-id="e73bc-211">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="e73bc-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="e73bc-212">Inicie sesión en su sitio de **BambooHR** como administrador.</span><span class="sxs-lookup"><span data-stu-id="e73bc-212">Log in to your **BambooHR** site as administrator.</span></span>

2. <span data-ttu-id="e73bc-213">En la barra de herramientas de la parte superior, haga clic en el icono de **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-213">In the toolbar on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="e73bc-214">![Configuración](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="e73bc-214">![Setting](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Setting")</span></span>

3. <span data-ttu-id="e73bc-215">Haga clic en **Descripción general**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-215">Click **Overview**.</span></span>

4. <span data-ttu-id="e73bc-216">En el panel de navegación izquierdo, vaya a **Seguridad \> Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-216">In the left navigation pane, go to **Security \> Users**.</span></span>

5. <span data-ttu-id="e73bc-217">Escriba el nombre de usuario, la contraseña y la dirección de correo electrónico de una cuenta válida de AAD que desee aprovisionar en los cuadros de texto relacionados.</span><span class="sxs-lookup"><span data-stu-id="e73bc-217">Type the user name, password, and email address of a valid AAD account you want to provision into the related textboxes.</span></span>

6. <span data-ttu-id="e73bc-218">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-218">Click **Save**.</span></span>
        
>[!NOTE]
><span data-ttu-id="e73bc-219">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de BambooHR para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="e73bc-219">You can use any other BambooHR user account creation tools or APIs provided by BambooHR to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e73bc-220">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e73bc-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e73bc-221">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a BambooHR.</span><span class="sxs-lookup"><span data-stu-id="e73bc-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BambooHR.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="e73bc-223">**Para asignar a Britta Simon a BambooHR, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e73bc-223">**To assign Britta Simon to BambooHR, perform the following steps:**</span></span>

1. <span data-ttu-id="e73bc-224">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e73bc-226">En la lista de aplicaciones, seleccione **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-226">In the applications list, select **BambooHR**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_app.png) 

3. <span data-ttu-id="e73bc-228">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="e73bc-230">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-230">Click **Add** button.</span></span> <span data-ttu-id="e73bc-231">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="e73bc-233">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="e73bc-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e73bc-234">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e73bc-235">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e73bc-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e73bc-236">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="e73bc-236">Testing single sign-on</span></span>

<span data-ttu-id="e73bc-237">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e73bc-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e73bc-238">Al hacer clic en el icono de BambooHR en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación BambooHR.</span><span class="sxs-lookup"><span data-stu-id="e73bc-238">When you click the BambooHR tile in the Access Panel, you should get automatically signed-on to your BambooHR application.</span></span>
<span data-ttu-id="e73bc-239">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e73bc-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e73bc-240">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e73bc-240">Additional resources</span></span>

* [<span data-ttu-id="e73bc-241">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e73bc-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e73bc-242">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e73bc-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_203.png

